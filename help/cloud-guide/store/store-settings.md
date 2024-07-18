---
title: Speicherkonfigurationsverwaltung
description: Erfahren Sie, wie Sie Store-Konfigurationseinstellungen in allen Adobe Commerce-Umgebungen in Cloud-Infrastrukturumgebungen verwalten und synchronisieren.
feature: Cloud, Configuration, SCD
exl-id: f2dd876d-24ee-4d47-b9ac-44fcf77b61b5
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Speicherkonfigurationsverwaltung

Die Standardkonfigurationen für Ihren Store werden in einem `config.xml` für das entsprechende Modul gespeichert. Wenn Sie die Einstellungen im Commerce Admin- oder CLI `bin/magento config:set`-Befehl ändern, werden die Änderungen in der Hauptdatenbank, insbesondere in der Tabelle `core_config_data`, übernommen. Diese Einstellungen überschreiben die Standardkonfigurationen, die in der Datei `config.xml` gespeichert sind.

Speichereinstellungen, die auf die Konfigurationen im Abschnitt Admin **Stores** > **Einstellungen** > **Konfiguration** verweisen, werden je nach Konfigurationstyp in den Konfigurationsdateien der Bereitstellung gespeichert:

- `app/etc/config.php` - Konfigurationseinstellungen für Stores, Websites, Module oder Erweiterungen, statische Dateioptimierung und Systemwerte für die Bereitstellung statischer Inhalte. Weitere Informationen finden Sie unter [config.php reference](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) im _Konfigurationshandbuch_.
- `app/etc/env.php` - Werte für systemspezifische Überschreibungen und vertrauliche Einstellungen, die _NOT_ in der Quell-Code-Verwaltung gespeichert werden sollen. Siehe den [env.php-Verweis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) im _Konfigurationshandbuch_.

>[!NOTE]
>
>Da Adobe Commerce in der Cloud-Infrastruktur nur die Produktions- und Wartungsmodi unterstützt, ist der Abschnitt **Erweitert** > **Entwickler** nicht im Admin verfügbar. Sie müssen über [Umgebungsadministratorberechtigungen](../project/user-access.md) verfügen, um Konfigurationsverwaltungsaufgaben durchzuführen. Sie können zusätzliche Einstellungen mithilfe von [Umgebungsvariablen](../environment/configure-env-yaml.md) konfigurieren.

Das Konfigurationsmanagement bietet eine Möglichkeit, konsistente Speichereinstellungen in all Ihren Umgebungen bereitzustellen, ohne dass die Pipeline-Bereitstellung zu minimalen Ausfallzeiten führt. Das Projekt Adobe Commerce on Cloud-Infrastruktur umfasst den Build-Server, das Erstellen und Bereitstellen von Skripten sowie Bereitstellungsumgebungen, die unter Berücksichtigung der [Pipeline-Bereitstellungsstrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) entwickelt wurden.

## Konfigurationsüberschreibungsschema

Alle Systemkonfigurationen werden während der Build- und Bereitstellungsphasen gemäß dem folgenden Überschreibungsschema festgelegt:

1. Wenn eine Umgebungsvariable vorhanden ist, verwenden Sie die benutzerdefinierte Konfiguration und ignorieren Sie die Standardkonfiguration.
1. Wenn keine Umgebungsvariable vorhanden ist, verwenden Sie die Konfiguration aus einem `MAGENTO_CLOUD_RELATIONSHIPS` Name-Wert-Paar in der [`.magento.app.yaml` Datei](../application/configure-app-yaml.md) . Ignorieren Sie die Standardkonfiguration.
1. Wenn keine Umgebungsvariable vorhanden ist und `MAGENTO_CLOUD_RELATIONSHIPS` kein Name-Wert-Paar enthält, entfernen Sie alle angepassten Konfigurationen und verwenden Sie die Werte aus der Standardkonfiguration.

Zusammenfassend lässt sich sagen, dass Umgebungsvariablen alle anderen Werte außer Kraft setzen.

>[!TIP]
>
>Weitere Informationen zum Überschreibungsschema für die Pipelinebereitstellung finden Sie unter [Konfigurationsverwaltung](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) im _Konfigurationshandbuch_ .

Wenn dieselbe Einstellung an mehreren Stellen konfiguriert ist, verlässt sich die Anwendung auf die folgende Konfigurationshierarchie, um zu bestimmen, welcher Wert auf die Umgebung angewendet werden soll:

| Priorität | Konfigurationsmethode<br>Methode | Beschreibung |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br>Umgebungsvariablen | Werte, die auf der Registerkarte _Variablen_ der Umgebungskonfiguration im [!DNL Cloud Console] hinzugefügt wurden. Geben Sie hier Werte für sensible oder umgebungsspezifische Konfigurationen an. Die hier angegebenen Einstellungen können nicht über den Administrator bearbeitet werden. Siehe [Umgebungskonfigurationsvariablen](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Werte, die im Abschnitt `variables` der Datei `.magento.app.yaml` hinzugefügt wurden. Geben Sie hier Werte an, um eine konsistente Konfiguration in allen Umgebungen sicherzustellen. **Geben Sie keine sensiblen Werte in der Datei `.magento.app.yaml` an.** Siehe [Anwendungseinstellungen](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | Die hier gespeicherten umgebungsspezifischen Konfigurationswerte werden mit dem Befehl `app:config:dump` hinzugefügt. Legen Sie die systemspezifischen und sensiblen Werte mithilfe von Umgebungsvariablen oder der CLI fest. Siehe [Sensible Daten](#sensitive-data). Die Datei `env.php` ist **nicht** im Quellcode-Steuerelement enthalten. |
| 4 | `app/etc/config.php` | Die hier gespeicherten Werte werden mit dem Befehl `app:config:dump` hinzugefügt. Gemeinsame Konfigurationswerte werden `config.php` hinzugefügt. Legen Sie die freigegebene Konfiguration über den Administrator oder mithilfe der CLI fest. Die Datei &quot;`config.php`&quot; ist im Quell-Code enthalten. |
| 5 | Datenbank | Die hier gespeicherten Werte werden durch Festlegen von Konfigurationen im Admin hinzugefügt. Konfigurationen, die mit einer der vorhergehenden Methoden festgelegt wurden, sind gesperrt (grau ausgeblendet) und können nicht über den Administrator bearbeitet werden. |
| 6 | `config.xml` | Bei vielen Konfigurationen werden in der Datei `config.xml` für ein Modul Standardwerte festgelegt. Wenn Adobe Commerce keinen Wert finden kann, der von einer der vorangehenden Methoden festgelegt wurde, wird der Standardwert zurückgesetzt, sofern festgelegt. |

{style="table-layout:auto"}

## Konfigurations-Dump

Sie können den folgenden `ece-tools`-Befehl verwenden, um eine `config.php` -Datei zu generieren, die alle aktuellen Speicherkonfigurationen enthält:

```bash
./vendor/bin/ece-tools config:dump
```

Die in die Datei &quot;`app/etc/config.php`&quot; übertragenen Daten werden zu &quot;_locked_&quot;, was bedeutet, dass das entsprechende Feld im Commerce-Admin &quot;**schreibgeschützt**&quot; wird. Die Datei `config.php` enthält nur die Einstellungen, die Sie konfigurieren. Die Standardwerte werden nicht gesperrt. Durch das Sperren nur der von Ihnen aktualisierten Werte wird außerdem sichergestellt, dass alle in der Staging- und Produktionsumgebung verwendeten Erweiterungen aufgrund schreibgeschützter Konfigurationen nicht beschädigt werden, insbesondere schnell.

>[!WARNING]
>
>Der Befehl `ece-tools config:dump` ruft keine detaillierten Konfigurationen für Module ab, z. B. B2B. Wenn Sie eine umfassende Konfigurationsablage benötigen, verwenden Sie den Befehl `app:config:dump` , aber dieser Befehl sperrt die Konfigurationswerte in einem schreibgeschützten Status.

### Sensible Daten

Alle sensiblen Konfigurationen werden in die Datei `app/etc/env.php` exportiert, wenn Sie den Befehl `bin/magento app:config:dump` verwenden. Sie können sensible Werte mithilfe des CLI-Befehls festlegen: `bin/magento config:sensitive:set`. Unter [Vertrauliche und umgebungsspezifische Einstellungen](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) im Handbuch _Commerce PHP Extensions_ erfahren Sie, wie Konfigurationseinstellungen als vertraulich oder systemspezifisch gekennzeichnet werden.

Eine Liste der [vertraulichen oder systemspezifischen Einstellungen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) finden Sie im _Konfigurationshandbuch_.

### SCD-Leistung

Abhängig von der Größe Ihres Stores können Sie eine große Anzahl statischer Inhaltsdateien bereitstellen. Normalerweise werden statische Inhalte während der Bereitstellungsphase bereitgestellt, wenn sich die Anwendung im Wartungsmodus befindet. Die optimale Konfiguration besteht darin, während der Build-Phase statischen Inhalt zu generieren. Siehe [Auswählen einer Bereitstellungsstrategie](../deploy/static-content.md).

Wenn Sie Configuration Management nach dem Ablegen der Konfigurationen aktiviert haben, sollten Sie die SCD_*-Variablen aus der Bereitstellungsphase in die Build-Phase verschieben, um während der Build-Phase die statische Inhaltserstellung ordnungsgemäß zu aktivieren. Siehe [Umgebungsvariablen](../environment/configure-env-yaml.md#environment-variables).

**Vor der Konfigurationsverwaltung**:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

**Nach Aktivierung der Konfigurationsverwaltung**:

Verschieben Sie die SCD_*-Variablen in die Build-Phase:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```

>[!NOTE]
>
>Vor der Bereitstellung statischer Dateien werden statische Inhalte mithilfe von GZIP durch Erstellen und Bereitstellen komprimiert. Durch das Komprimieren statischer Dateien werden Server-Ladevorgänge reduziert und die Site-Leistung erhöht. Weitere Informationen zum Anpassen oder Deaktivieren der Dateikomprimierung finden Sie unter [Build-Optionen](../environment/variables-build.md) .

## Verfahren zur Verwaltung Ihrer Einstellungen

Die folgende Abbildung zeigt einen allgemeinen Überblick über diesen Prozess:

![Überblick über die Verwaltung der Starter-Konfiguration](../../assets/starter/configuration-management-flow.png)

**So konfigurieren Sie Ihren Speicher und generieren eine Konfigurationsdatei**:

1. Schließen Sie alle Konfigurationen für Ihre Stores in Admin für eine der Umgebungen ab:

   - Starter: Eine aktive Entwicklungsverzweigung
   - Pro: Eine aktive Verzweigung in der Integrationsumgebung

   Diese Konfigurationen umfassen nicht die eigentlichen Produkte, es sei denn, Sie planen, die Datenbank aus dieser Umgebung in Staging- und Produktionsumgebungen zu lagern. In der Regel enthalten Entwicklungsdatenbanken nicht die vollständigen Store-Daten.

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Erstellen Sie einen lokalen Dump der Remote-Datenbank.

   ```bash
   magento-cloud db:dump
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen und pushen Sie diese, um eine Remote-Umgebung zu aktualisieren.

   ```bash
   git add app/etc/config.php
   ```

   ```bash
   git commit -m "Add system-specific configuration"
   ```

   ```bash
   git push origin <branch-name>
   ```

Melden Sie sich nach Abschluss der Bereitstellung beim Administrator für die aktualisierte Umgebung an, um die Einstellungen zu überprüfen. Führen Sie bei Bedarf weitere Konfigurationen mit den Staging- und Produktionsumgebungen zusammen.

### Konfigurationen aktualisieren

Wenn Sie Ihre Umgebung über den Admin ändern und den Befehl erneut ausführen, werden neue Konfigurationen an den Code in der Datei `config.php` angehängt.

>[!WARNING]
>
>Sie können die Datei &quot;`config.php`&quot; zwar in der Staging- und Produktionsumgebung manuell bearbeiten, jedoch wird dies **nicht** empfohlen. Die Datei hilft dabei, alle Konfigurationen in allen Umgebungen konsistent zu halten. Löschen Sie nie die Datei &quot;`config.php`&quot;, um sie neu zu erstellen. Durch Löschen der Datei können spezifische Konfigurationen und Einstellungen entfernt werden, die für Build- und Bereitstellungsprozesse erforderlich sind.

### Konfigurationsdateien wiederherstellen

Kopien der ursprünglichen `app/etc/env.php` - und `app/etc/config.php` -Dateien wurden während des Bereitstellungsprozesses erstellt und im selben Ordner gespeichert. Im Folgenden werden die BAK (Backup-Dateien) und PHP (Originaldateien) im selben Ordner `app/etc` dargestellt:

```
...
config.php.bak
di.xml
env.php.bak
vendor_path.php
config.php
db_schema.xml
env.php
...
```

Ältere Konfigurationen verwendeten die Datei &quot;`app/etc/config.local.php`&quot;. Siehe [Migration älterer Konfigurationen](#migrate-older-configurations).

**So stellen Sie Konfigurationsdateien wieder her**:

1. Verwenden Sie auf Ihrer lokalen Workstation SSH, um sich beim Remote-Projekt und der Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Überprüfen Sie den Speicherort und die Verfügbarkeit der Backup-Dateien.

   ```bash
   ./vendor/bin/ece-tools backup:list
   ```

   Beispielantwort:

   ```
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Wiederherstellen von Sicherungsdateien.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Migration älterer Konfigurationen

Wenn Sie auf Adobe Commerce in der Cloud-Infrastruktur 2.2 oder höher aktualisieren, sollten Sie Einstellungen aus der `config.local.php` -Datei in Ihre neue `config.php` -Datei migrieren. Wenn die Konfigurationseinstellungen in Ihrem Admin mit dem Inhalt der Datei übereinstimmen, befolgen Sie die Anweisungen zum Generieren und Hinzufügen der Datei &quot;`config.php`&quot;.

Wenn sie sich unterscheiden, können Sie Inhalt aus der `config.local.php`-Datei an Ihre neue `config.php`-Datei anhängen:

1. Befolgen Sie die Anweisungen zum Generieren der Datei &quot;`config.php`&quot;.

1. Öffnen Sie die Datei &quot;`config.php`&quot; und löschen Sie die letzte Zeile.

1. Öffnen Sie die Datei &quot;`config.local.php`&quot; und kopieren Sie den Inhalt.

1. Fügen Sie den Inhalt in die Datei `config.php` ein, speichern Sie sie und schließen Sie das Hinzufügen zu Git ab.

1. Bereitstellen in allen Umgebungen.

Sie führen diese Migration nur einmal durch. Verwenden Sie nach der Migration die Datei &quot;`config.php`&quot;.

### Gebietsschemata ändern

Sie können Ihre Store-Gebietsschemata ändern, ohne einen komplexen Konfigurationsimport- und -export-Prozess zu befolgen, _wenn_ Sie [SCD_ON_DEMAND](../environment/variables-global.md#scd_on_demand) aktiviert haben. Sie können die Gebietsschemata mithilfe des Administrators aktualisieren.

Sie können der Staging- oder Produktionsumgebung ein anderes Gebietsschema hinzufügen, indem Sie in einer Integrationsverzweigung die Option `SCD_ON_DEMAND` aktivieren, eine aktualisierte `config.php` -Datei mit den neuen Gebietsschemainformationen generieren und die Konfigurationsdatei in die Zielumgebung kopieren.

>[!WARNING]
>
>Durch diesen Prozess wird **die Speicherkonfiguration überschrieben. Führen Sie die folgenden Schritte nur aus, wenn die Umgebungen dieselben Stores enthalten.**

1. Aktivieren Sie in der Integrationsumgebung die Variable `SCD_ON_DEMAND` mit der Datei [`.magento.env.yaml`](../environment/configure-env-yaml.md).

1. Fügen Sie die erforderlichen Gebietsschemata mithilfe Ihres Administrators hinzu.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden und die `/app/etc/config.php`-Datei mit allen Gebietsschemas zu generieren.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Kopieren Sie die neue Konfigurationsdatei aus der Remote-Integrationsumgebung in den lokalen Umgebungsordner.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen und pushen Sie diese, um eine Remote-Umgebung zu aktualisieren.
