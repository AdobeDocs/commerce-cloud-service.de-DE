---
title: Crons-Eigenschaft
description: Siehe Beispiele zum Konfigurieren der Eigenschaft "crons"in der Konfigurationsdatei der Anwendung. [!DNL Commerce]
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Crons-Eigenschaft

Adobe Commerce verwendet die `crons` -Eigenschaft, um sich wiederholende Aktivitäten zu planen. Es ist ideal, eine bestimmte Aufgabe zu bestimmten Tageszeiten zu planen. Aufgrund der Art schreibgeschützter Umgebungen kann für Adobe Commerce jeweils nur ein Cron-Auftrag für Cloud-Infrastrukturprojekte auf der Webinstanz ausgeführt werden. Es empfiehlt sich, langwierige Aufgaben in kleinere Aufgaben in der Warteschlange zu unterteilen. Alternativ können Sie eine [Worker-Instanz](workers-property.md) erstellen.

Adobe empfiehlt, `crons` als [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) auszuführen. Führen Sie _nicht_ `crons` als `root` oder als Webserver-Benutzer aus.

Diese Konfiguration unterscheidet sich von lokalen Implementierungen von Adobe Commerce, die mehrere standardmäßige Cron-Aufträge haben. Siehe [Konfigurieren von Cron-Aufträgen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) im _Konfigurationshandbuch_.

## Einrichten von Cron-Aufträgen

Die Eigenschaft `crons` beschreibt Prozesse, die nach einem Zeitplan ausgelöst werden. Jeder Auftrag erfordert einen Namen und die folgenden Optionen:

- `spec` - Der für die Planung verwendete Cron-Ausdruck.
- `cmd`—Der Befehl, der auf `start` und `stop` ausgeführt werden soll.
- `shutdown_timeout`—(_Optional_) Wenn ein Cron-Auftrag abgebrochen wird, ist dies die Anzahl der Sekunden, nach denen ein SIGKILL-Signal gesendet wird, um den Auftrag oder Prozess zu stoppen. Der Standardwert beträgt 10 Sekunden.
- `timeout`—(_Optional_) Die maximale Zeit, die ein Cron-Auftrag vor der Zeitüberschreitung ausgeführt werden kann. Die Standardeinstellung ist der maximal zulässige Wert von 86400 Sekunden (24 Stunden).

Standardmäßig verfügt jedes Commerce-Cloud-Projekt in der Datei `.magento.app.yaml` über die folgende standardmäßige `crons` -Konfiguration:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Wenn für Ihr Projekt benutzerdefinierte Cron-Aufträge erforderlich sind, können Sie sie zur standardmäßigen `crons`-Konfiguration hinzufügen. Siehe [Erstellen eines Cron-Auftrags](#build-a-cron-job).

### `crontab`

Adobe Commerce hat Pro-Projekten nur eine Konfigurationsoption für automatische Kronen hinzugefügt, um die Self-Service-Konfiguration `crons` in den Staging- und Produktionsumgebungen zu unterstützen. Wenn diese Option aktiviert ist, können Sie `crontab` verwenden, um die Cron-Konfiguration zu überprüfen. Dies ist _nicht_ für Starter-Projekte verfügbar.

Sie können zwar `crontab` verwenden, um die Konfiguration für Pro-Projekte zu überprüfen, Adobe Commerce verwendet jedoch nicht `crontab`, um Cron-Aufträge für Sites auszuführen, die in der Cloud-Infrastruktur bereitgestellt werden.

**Überprüfen der Cron-Konfiguration in Pro-Umgebungen**:

1. Verwenden Sie [SSH](../development/secure-connections.md#use-an-ssh-command) , um sich bei der Remote-Umgebung anzumelden.

1. Listen Sie die geplanten Cron-Prozesse auf.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Wenn der Befehl `crontab -l` einen Fehler vom Typ `Command not found` zurückgibt (nur in den Staging- und Produktionsumgebungen von Pro), müssen Sie [ein Adobe Commerce-Supportticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Konfigurationsoption für die automatische Abspielfunktion in Ihrem Projekt zu aktivieren.

Das folgende Beispiel zeigt die Ausgabe `crontab` für eine Umgebung, die nur über die standardmäßige `crons` -Konfiguration verfügt:

```
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Cron-Auftrag erstellen

Ein Cron-Auftrag umfasst die Zeitplan- und Zeitspezifikation sowie den Befehl, der zur geplanten Zeit ausgeführt werden soll. Bei Starterumgebungen und Pro `integration`-Umgebungen beträgt das Mindestintervall einmal pro fünf Minuten. Für Pro-Staging- und Produktionsumgebungen beträgt das Mindestintervall einmal pro Minute. In Adobe Commerce in der Cloud-Infrastruktur fügen Sie benutzerdefinierte Cron-Aufträge zur Datei &quot;`.magento.app.yaml`&quot;im Abschnitt &quot;`crons`&quot;hinzu. Das allgemeine Format lautet für die Planung `spec` und für die Angabe des auszuführenden Befehls oder benutzerdefinierten Skripts `cmd`.

### Spezifikation

Adobe Commerce verwendet einen Ausdruck mit fünf Werten für eine `crons`-Spezifikation (Spezifikation): `* * * * *`

1. Minute (0 bis 59) Für alle Starter- und Pro-Umgebungen beträgt die Mindestfrequenz, die für Cron-Aufträge unterstützt wird, fünf Minuten. Möglicherweise müssen Sie die Einstellungen in Ihrem Admin konfigurieren.
2. Stunde (0 bis 23)
3. Tag des Monats (1 bis 31)
4. Monat (1 bis 12)
5. Wochentag (0 bis 6) (Sonntag bis Samstag; 7 ist auf einigen Systemen auch Sonntag)

Beispiele:

- `00 */3 * * *` wird alle drei Stunden in der ersten Minute ausgeführt (12:00 Uhr, 3:00 Uhr, 6:00 Uhr)
- `20 */8 * * *` wird alle 8 Stunden bei Minute 20 ausgeführt (12:20, 8:20 Uhr, 16:20 Uhr)
- `00 00 * * *` läuft einmal am Tag um Mitternacht
- `00 * * * 1` läuft einmal pro Woche am Montag um Mitternacht.

>[!NOTE]
>
>Die in der Datei `.magento.app.yaml` angegebene `crons` Zeit basiert auf der Zeitzone des Servers und nicht auf der Zeitzone, die in den Speicherkonfigurationswerten in der Datenbank angegeben ist.

Berücksichtigen Sie bei der Festlegung der Planung die Zeit, die zum Abschließen der Aufgabe benötigt wird. Wenn Sie z. B. alle drei Stunden einen Auftrag ausführen und die Aufgabe 40 Minuten dauert, können Sie die geplante Zeit ändern.

### Befehl

Der `cmd` gibt den auszuführenden Befehl oder das benutzerdefinierte Skript an. Das Befehlsskriptformat kann Folgendes enthalten:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Beispiel:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In diesem Beispiel ist `<path-to-php-binary>` `/usr/bin/php`. Der Installationsordner, der die Projekt-ID enthält, ist `/app/abc123edf890/bin/magento` und die Skriptaktion ist `export:start catalog_category_product`.

### Hinzufügen benutzerdefinierter Cron-Aufträge zu Ihrem Projekt

Auf der Adobe Commerce-Plattform für Cloud-Infrastruktur können Sie Anpassungen zum Abschnitt &quot;`crons`&quot;der Datei &quot;[`.magento.app.yaml`](../application/configure-app-yaml.md)&quot;hinzufügen.

>[!NOTE]
>
>Bei Starterumgebungen und Pro `integration`-Umgebungen beträgt das Mindestintervall einmal pro fünf Minuten. Für Pro-Staging- und Produktionsumgebungen beträgt das Mindestintervall einmal pro Minute. Es ist nicht möglich, häufigere Intervalle als die Standardmindestwerte zu konfigurieren.

Bei Adobe Commerce Pro-Projekten muss die Funktion [Auto-Crons Feature](#set-up-cron-jobs) für Ihr Projekt aktiviert sein, bevor Sie benutzerdefinierte Cron-Aufträge über die Datei `.magento.app.yaml` zu Staging- und Produktionsumgebungen hinzufügen können. Wenn diese Funktion nicht aktiviert ist, senden Sie [ein Adobe Commerce-Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um automatische Kronen zu aktivieren.

**Hinzufügen benutzerdefinierter Cron-Aufträge**:

1. Bearbeiten Sie in Ihrer lokalen Entwicklungsumgebung die Datei &quot;`.magento.app.yaml`&quot;im Ordner &quot;Adobe Commerce `/app`&quot;.

1. Fügen Sie im Abschnitt `crons` Ihre Anpassung im folgenden Format hinzu:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   Im folgenden Beispiel exportiert der Auftrag `productcatalog` den Produktkatalog alle acht Stunden, also 20 Minuten nach der Stunde.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

### Cron-Aufträge aktualisieren

Um einen benutzerdefinierten Auftrag hinzuzufügen, zu entfernen oder zu aktualisieren, ändern Sie die Konfiguration im Abschnitt &quot;`crons`&quot;der Datei &quot;`.magento.app.yaml`&quot;. Testen Sie dann die Aktualisierungen in der Remote-Umgebung `integration` , bevor Sie die Änderungen in die Staging- und Produktionsumgebungen verschieben.

## Deaktivieren von Cron-Aufträgen

Sie können Cron-Aufträge manuell deaktivieren, bevor Sie Wartungsaufgaben wie die Neuindizierung oder die Cache-Bereinigung durchführen, um Leistungsprobleme zu vermeiden. Sie können den Befehl `ece-tools` CLI `cron:disable` verwenden, um alle Cron-Aufträge zu deaktivieren und alle aktiven Cron-Prozesse zu stoppen.

**So deaktivieren Sie cron-Aufträge**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Deaktivieren Sie Cron-Aufträge und stoppen Sie aktive Cron-Prozesse.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. Nachdem Sie alle erforderlichen Wartungsaufgaben ausgeführt haben, stellen Sie sicher, dass Sie die Cron-Aufträge erneut aktivieren.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Fehlerbehebung bei Cron-Aufträgen

Adobe hat das Adobe Commerce-Paket zur Cloud-Infrastruktur aktualisiert, um die Cron-Verarbeitung auf der Adobe Commerce-Cloud-Infrastrukturplattform zu optimieren und Kron-bezogene Probleme zu beheben. Wenn Probleme mit der Cron-Verarbeitung auftreten, stellen Sie sicher, dass Ihr Projekt die neueste Version des `ece-tools`-Pakets verwendet. Siehe [ECE-Tools aktualisieren](../dev-tools/update-package.md).

Sie können die Informationen zur Cron-Verarbeitung in den Protokolldateien auf Anwendungsebene für jede Umgebung überprüfen. Siehe [Anwendungsprotokolle](../test/log-locations.md#application-logs).

In den folgenden Adobe Commerce-Supportartikeln finden Sie Hilfe zur Fehlerbehebung bei Problemen mit Cron-Angriffen:

- [Cron-Aufgaben sperren Aufgaben von anderen Gruppen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Zurücksetzen von blockierten Cron-Aufträgen manuell auf der Cloud zurücksetzen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
