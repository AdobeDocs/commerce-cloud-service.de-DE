---
title: Speicherkonfigurationsverwaltung
description: Erfahren Sie, wie Sie Store-Konfigurationseinstellungen in allen Adobe Commerce-Umgebungen in Cloud-Infrastrukturumgebungen verwalten und synchronisieren.
feature: Cloud, Configuration, SCD
exl-id: f2dd876d-24ee-4d47-b9ac-44fcf77b61b5
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Speicherkonfigurationsverwaltung

Die Standardkonfigurationen für Ihren Store werden in einer `config.xml` für das entsprechende Modul. Wenn Sie Einstellungen in Commerce Admin oder CLI ändern `bin/magento config:set` angegeben ist, werden die Änderungen in der Hauptdatenbank, insbesondere in der `core_config_data` Tabelle. Diese Einstellungen überschreiben die Standardkonfigurationen, die in der Datei `config.xml` -Datei.

Speichereinstellungen, die auf die Konfigurationen in der Admin-Konsole verweisen **Stores** > **Einstellungen** > **Konfiguration** -Abschnitt in den Konfigurationsdateien der Bereitstellung gespeichert werden, die auf dem Konfigurationstyp basieren:

- `app/etc/config.php`—Konfigurationseinstellungen für Stores, Websites, Module oder Erweiterungen, statische Dateioptimierung und Systemwerte für die Bereitstellung statischer Inhalte. Siehe [config.php-Referenz](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) im _Konfigurationshandbuch_.
- `app/etc/env.php`—Werte für systemspezifische Außerkraftsetzungen und vertrauliche Einstellungen, die _NOT_ in der Quell-Code-Verwaltung gespeichert werden. Siehe [env.php-Referenz](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) im _Konfigurationshandbuch_.

>[!NOTE]
>
>Da Adobe Commerce in der Cloud-Infrastruktur nur die Produktions- und Wartungsmodi unterstützt, wird die **Erweitert** > **Entwickler** nicht in Admin verfügbar ist. Sie müssen [Umgebungsadministratorberechtigungen](../project/user-access.md) , um Konfigurationsverwaltungsaufgaben abzuschließen. Sie können zusätzliche Einstellungen konfigurieren, indem Sie [Umgebungsvariablen](../environment/configure-env-yaml.md).

Das Konfigurationsmanagement bietet eine Möglichkeit, konsistente Speichereinstellungen in all Ihren Umgebungen bereitzustellen, ohne dass die Pipeline-Bereitstellung zu minimalen Ausfallzeiten führt. Das Projekt Adobe Commerce on Cloud-Infrastruktur umfasst die Build-Server-, Build- und Bereitstellungsumgebungen sowie die Bereitstellungsumgebungen, die mit dem [Pipeline-Bereitstellungsstrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) im Hinterkopf.

## Konfigurationsüberschreibungsschema

Alle Systemkonfigurationen werden während der Build- und Bereitstellungsphasen gemäß dem folgenden Überschreibungsschema festgelegt:

1. Wenn eine Umgebungsvariable vorhanden ist, verwenden Sie die benutzerdefinierte Konfiguration und ignorieren Sie die Standardkonfiguration.
1. Wenn keine Umgebungsvariable vorhanden ist, verwenden Sie die Konfiguration aus einer `MAGENTO_CLOUD_RELATIONSHIPS` Name-Wert-Paar in der [`.magento.app.yaml` file](../application/configure-app-yaml.md). Ignorieren Sie die Standardkonfiguration.
1. Wenn keine Umgebungsvariable vorhanden ist und `MAGENTO_CLOUD_RELATIONSHIPS` enthält kein Name-Wert-Paar, entfernen Sie alle angepassten Konfigurationen und verwenden Sie die Werte aus der Standardkonfiguration.

Zusammenfassend lässt sich sagen, dass Umgebungsvariablen alle anderen Werte außer Kraft setzen.

>[!TIP]
>
>Siehe [Konfigurationsverwaltung](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) im _Konfigurationshandbuch_ Weitere Informationen zum Überschreibungsschema für die Pipelinebereitstellung.

Wenn dieselbe Einstellung an mehreren Stellen konfiguriert ist, verlässt sich die Anwendung auf die folgende Konfigurationshierarchie, um zu bestimmen, welcher Wert auf die Umgebung angewendet werden soll:

| Priorität | Konfiguration<br>Methode | Beschreibung |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br>Umgebungsvariablen | Werte, die aus dem _Variablen_ Registerkarte der Umgebungskonfiguration im [!DNL Cloud Console]. Geben Sie hier Werte für sensible oder umgebungsspezifische Konfigurationen an. Die hier angegebenen Einstellungen können nicht über den Administrator bearbeitet werden. Siehe [Umgebungskonfigurationsvariablen](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Werte, die im `variables` Abschnitt `.magento.app.yaml` -Datei. Geben Sie hier Werte an, um eine konsistente Konfiguration in allen Umgebungen sicherzustellen. **Geben Sie keine sensiblen Werte im `.magento.app.yaml` -Datei.** Siehe [Anwendungseinstellungen](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | Die hier gespeicherten umgebungsspezifischen Konfigurationswerte werden mithilfe der Variablen `app:config:dump` Befehl. Legen Sie die systemspezifischen und sensiblen Werte mithilfe von Umgebungsvariablen oder der CLI fest. Siehe [Sensible Daten](#sensitive-data). Die `env.php` Datei ist **not** in der Quell-Code-Verwaltung enthalten ist. |
| 4 | `app/etc/config.php` | Die hier gespeicherten Werte werden mithilfe der Variablen `app:config:dump` Befehl. Freigegebene Konfigurationswerte werden zu `config.php`. Legen Sie die freigegebene Konfiguration über den Administrator oder mithilfe der CLI fest. Die `config.php` -Datei ist in der Quell-Code-Verwaltung enthalten. |
| 5 | Datenbank | Die hier gespeicherten Werte werden durch Festlegen von Konfigurationen im Admin hinzugefügt. Konfigurationen, die mit einer der vorhergehenden Methoden festgelegt wurden, sind gesperrt (grau ausgeblendet) und können nicht über den Administrator bearbeitet werden. |
| 6 | `config.xml` | Bei vielen Konfigurationen werden die Standardwerte in der `config.xml` -Datei für ein Modul. Wenn Adobe Commerce keinen Wert finden kann, der von einer der vorangehenden Methoden festgelegt wurde, wird der Standardwert zurückgesetzt, sofern festgelegt. |

{style="table-layout:auto"}

## Konfigurations-Dump

Sie können Folgendes verwenden: `ece-tools` -Befehl zum Generieren einer `config.php` -Datei, die alle aktuellen Speicherkonfigurationen enthält:

```bash
./vendor/bin/ece-tools config:dump
```

Die Daten wurden in die `app/etc/config.php` wird _locked_, was bedeutet, dass das entsprechende Feld im Commerce Admin **schreibgeschützt**. Die `config.php` enthält nur die Einstellungen, die Sie konfigurieren. Die Standardwerte werden nicht gesperrt. Durch das Sperren nur der von Ihnen aktualisierten Werte wird außerdem sichergestellt, dass alle in der Staging- und Produktionsumgebung verwendeten Erweiterungen aufgrund schreibgeschützter Konfigurationen nicht beschädigt werden, insbesondere schnell.

>[!WARNING]
>
>Die `ece-tools config:dump` -Befehl ruft keine detaillierten Konfigurationen für Module ab, z. B. B2B. Wenn Sie eine umfassende Konfigurationsablage benötigen, verwenden Sie die `app:config:dump` -Befehl, aber dieser Befehl sperrt Konfigurationswerte in einem schreibgeschützten Status.

### Sensible Daten

Alle sensiblen Konfigurationen, die in `app/etc/env.php` -Datei, wenn Sie die `bin/magento app:config:dump` Befehl. Sie können sensible Werte mithilfe des CLI-Befehls festlegen: `bin/magento config:sensitive:set`. Siehe  [Sensible und umgebungsspezifische Einstellungen](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) im _Commerce-PHP-Erweiterungen_ Anleitung, um zu erfahren, wie Sie Konfigurationseinstellungen als vertraulich oder systemspezifisch festlegen.

Liste mit [Sensible oder systemspezifische Einstellungen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) im _Konfigurationshandbuch_.

### SCD-Leistung

Abhängig von der Größe Ihres Stores können Sie eine große Anzahl statischer Inhaltsdateien bereitstellen. Normalerweise werden statische Inhalte während der Bereitstellungsphase bereitgestellt, wenn sich die Anwendung im Wartungsmodus befindet. Die optimale Konfiguration besteht darin, während der Build-Phase statischen Inhalt zu generieren. Siehe [Implementierungsstrategie auswählen](../deploy/static-content.md).

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

**Nach der Aktivierung der Konfigurationsverwaltung**:

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
>Vor der Bereitstellung statischer Dateien werden statische Inhalte mithilfe von GZIP durch Erstellen und Bereitstellen komprimiert. Durch das Komprimieren statischer Dateien werden Server-Ladevorgänge reduziert und die Site-Leistung erhöht. Siehe [Build-Optionen](../environment/variables-build.md) , um mehr über das Anpassen oder Deaktivieren der Dateikomprimierung zu erfahren.

## Verfahren zur Verwaltung Ihrer Einstellungen

Die folgende Abbildung zeigt einen allgemeinen Überblick über diesen Prozess:

![Übersicht über die Verwaltung der Starter-Konfiguration](../../assets/starter/configuration-management-flow.png)

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

Wenn Sie Ihre Umgebung über den Admin ändern und den Befehl erneut ausführen, werden neue Konfigurationen an den Code im `config.php` -Datei.

>[!WARNING]
>
>Während Sie die `config.php` in den Staging- und Produktionsumgebungen **not** empfohlen. Die Datei hilft dabei, alle Konfigurationen in allen Umgebungen konsistent zu halten. Löschen Sie niemals die `config.php` -Datei, um sie neu zu erstellen. Durch Löschen der Datei können spezifische Konfigurationen und Einstellungen entfernt werden, die für Build- und Bereitstellungsprozesse erforderlich sind.

### Konfigurationsdateien wiederherstellen

Kopien des Originals `app/etc/env.php` und `app/etc/config.php` -Dateien wurden während des Bereitstellungsprozesses erstellt und im selben Ordner gespeichert. Im Folgenden werden die BAK (Backup-Dateien) und PHP (Original-Dateien) im selben `app/etc` Ordner:

```terminal
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

Ältere Konfigurationen verwendeten die `app/etc/config.local.php` -Datei. Siehe [Migration älterer Konfigurationen](#migrate-older-configurations).

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

   ```terminal
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Wiederherstellen von Sicherungsdateien.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Migration älterer Konfigurationen

Wenn Sie auf Adobe Commerce in Cloud-Infrastruktur 2.2 oder höher aktualisieren, sollten Sie Einstellungen aus dem `config.local.php` in der neuen `config.php` -Datei. Wenn die Konfigurationseinstellungen in Ihrem Admin mit dem Inhalt der Datei übereinstimmen, befolgen Sie die Anweisungen zum Generieren und Hinzufügen der `config.php` -Datei.

Unterscheiden sich diese, können Sie Inhalte aus der `config.local.php` in der neuen `config.php` Datei:

1. Befolgen Sie die Anweisungen zum Generieren der `config.php` -Datei.

1. Öffnen Sie die `config.php` und löschen Sie die letzte Zeile.

1. Öffnen Sie die `config.local.php` und kopieren Sie den Inhalt.

1. Fügen Sie den Inhalt in die `config.php` Datei speichern und abschließen, um sie Git hinzuzufügen.

1. Bereitstellen in allen Umgebungen.

Sie führen diese Migration nur einmal durch. Verwenden Sie nach der Migration die `config.php` -Datei.

### Gebietsschemata ändern

Sie können Ihre Store-Gebietsschemata ändern, ohne einen komplexen Konfigurationsimport- und -exportprozess zu befolgen. _if_ Sie haben [SCD_ON_DEMAND](../environment/variables-global.md#scd_on_demand) aktiviert. Sie können die Gebietsschemata mithilfe des Administrators aktualisieren.

Sie können ein anderes Gebietsschema zur Staging- oder Produktionsumgebung hinzufügen, indem Sie `SCD_ON_DEMAND` in einer Integrationsverzweigung eine aktualisierte `config.php` -Datei mit den neuen Gebietsschema-Informationen und kopieren Sie die Konfigurationsdatei in die Zielumgebung.

>[!WARNING]
>
>Dieser Prozess **overwrites** die Speicherkonfiguration; führen Sie nur Folgendes aus, wenn die Umgebungen dieselben Stores enthalten.

1. Aktivieren Sie in der Integrationsumgebung die `SCD_ON_DEMAND` -Variable mithilfe der [`.magento.env.yaml` file](../environment/configure-env-yaml.md).

1. Fügen Sie die erforderlichen Gebietsschemata mithilfe Ihres Administrators hinzu.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden und die `/app/etc/config.php` -Datei, die alle Gebietsschemas enthält.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Kopieren Sie die neue Konfigurationsdatei aus der Remote-Integrationsumgebung in den lokalen Umgebungsordner.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen und pushen Sie diese, um eine Remote-Umgebung zu aktualisieren.
