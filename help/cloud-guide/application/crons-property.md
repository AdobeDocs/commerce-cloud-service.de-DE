---
title: Crons-Eigenschaft
description: Siehe Beispiele zum Konfigurieren der Eigenschaft "crons"im [!DNL Commerce] Anwendungskonfigurationsdatei.
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 0%

---

# Crons-Eigenschaft

Adobe Commerce verwendet die `crons` -Eigenschaft, um sich wiederholende Aktivitäten zu planen. Es ist ideal, eine bestimmte Aufgabe zu bestimmten Tageszeiten zu planen. Aufgrund der Art schreibgeschützter Umgebungen kann für Adobe Commerce jeweils nur ein Cron-Auftrag für Cloud-Infrastrukturprojekte auf der Webinstanz ausgeführt werden. Es empfiehlt sich, langwierige Aufgaben in kleinere Aufgaben in der Warteschlange zu unterteilen. Alternativ können Sie eine [Worker-Instanz](workers-property.md).

Adobe empfiehlt, dass Sie `crons` als [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html). Do _not_ run `crons` as `root` oder als Webserver-Benutzer.

Diese Konfiguration unterscheidet sich von lokalen Implementierungen von Adobe Commerce, die mehrere standardmäßige Cron-Aufträge haben. Siehe [Konfigurieren von Cron-Aufträgen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) im _Konfigurationshandbuch_.

## Einrichten von Cron-Aufträgen

Die `crons` -Eigenschaft beschreibt Prozesse, die nach einem Zeitplan ausgelöst werden. Jeder Auftrag erfordert einen Namen und die folgenden Optionen:

- `spec`—Der für die Planung verwendete Cron-Ausdruck.
- `cmd`—Der Befehl, auf dem ausgeführt werden soll `start` und `stop`.
- `shutdown_timeout`—(_Optional_) Wenn ein Cron-Auftrag abgebrochen wird, ist dies die Anzahl der Sekunden, nach denen ein SIGKILL-Signal gesendet wird, um den Auftrag oder Prozess zu stoppen. Der Standardwert beträgt 10 Sekunden.
- `timeout`—(_Optional_) Die maximale Zeit, die ein Cron-Auftrag vor der Zeitüberschreitung ausgeführt werden kann. Die Standardeinstellung ist der maximal zulässige Wert von 86400 Sekunden (24 Stunden).

Standardmäßig hat jedes Commerce-Cloud-Projekt die folgende Standardeinstellung `crons` Konfiguration in der `.magento.app.yaml` Datei:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Wenn für Ihr Projekt benutzerdefinierte Cron-Aufträge erforderlich sind, können Sie sie zum Standard hinzufügen `crons` Konfiguration. Siehe [Cron-Auftrag erstellen](#build-a-cron-job).

### `crontab`

Adobe Commerce hat Pro-Projekten nur eine Konfigurationsoption für automatische Kronen hinzugefügt, um die Selbstbedienung zu unterstützen `crons` Konfiguration in den Staging- und Produktionsumgebungen. Wenn diese Option aktiviert ist, können Sie `crontab` , um die Cron-Konfiguration zu überprüfen. Dies ist _not_ verfügbar mit Starter-Projekten.

Sie können `crontab` zur Überprüfung der Konfiguration für Pro-Projekte verwendet Adobe Commerce nicht `crontab` zum Ausführen von Cron-Aufträgen für Sites, die in der Cloud-Infrastruktur bereitgestellt werden.

**Überprüfen der Cron-Konfiguration in Pro-Umgebungen**:

1. Verwendung [SSH](../development/secure-connections.md#use-an-ssh-command) , um sich bei der Remote-Umgebung anzumelden.

1. Listen Sie die geplanten Cron-Prozesse auf.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Wenn die Variable `crontab -l` gibt einen `Command not found` -Fehler, müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Konfigurationsoption &quot;Auto-Crons Self-Service&quot;in Ihrem Pro-Projekt zu aktivieren.

Das folgende Beispiel zeigt die `crontab` Ausgabe für eine Umgebung, die nur über die Standardeinstellung verfügt `crons` Konfiguration:

```terminal
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Cron-Auftrag erstellen

Ein Cron-Auftrag umfasst die Zeitplan- und Zeitspezifikation sowie den Befehl, der zur geplanten Zeit ausgeführt werden soll. Für Starterumgebungen und Pro `integration` -Umgebungen entspricht, beträgt das Mindestintervall einmal pro fünf Minuten. Für Pro-Staging- und Produktionsumgebungen beträgt das Mindestintervall einmal pro Minute. In Adobe Commerce in der Cloud-Infrastruktur fügen Sie benutzerdefinierte Cron-Aufträge zur `.magento.app.yaml` in der Datei `crons` Abschnitt. Das allgemeine Format lautet `spec` für die Planung und `cmd` , um den auszuführenden Befehl oder das benutzerdefinierte Skript anzugeben.

### Spezifikation

Adobe Commerce verwendet einen Ausdruck mit fünf Werten für einen `crons` Spezifikation (Spezifikation): `* * * * *`

1. Minute (0 bis 59) Für alle Starter- und Pro-Umgebungen beträgt die Mindestfrequenz, die für Cron-Aufträge unterstützt wird, fünf Minuten. Möglicherweise müssen Sie die Einstellungen in Ihrem Admin konfigurieren.
2. Stunde (0 bis 23)
3. Tag des Monats (1 bis 31)
4. Monat (1 bis 12)
5. Wochentag (0 bis 6) (Sonntag bis Samstag; 7 ist auf einigen Systemen auch Sonntag)

Beispiele:

- `00 */3 * * *` wird alle drei Stunden in der ersten Minute ausgeführt (12:00 Uhr, 3:00 Uhr, 6:00 Uhr)
- `20 */8 * * *` wird alle 8 Stunden bei Minute 20 ausgeführt (12:20 Uhr, 8:20 Uhr, 16:20 Uhr)
- `00 00 * * *` läuft einmal am Tag um Mitternacht
- `00 * * * 1` läuft einmal pro Woche am Montag um Mitternacht.

>[!NOTE]
>
>Die `crons` die in der `.magento.app.yaml` -Datei basiert auf der Zeitzone des Servers und nicht auf der Zeitzone, die in den Speicherkonfigurationswerten in der Datenbank angegeben ist.

Berücksichtigen Sie bei der Festlegung der Planung die Zeit, die zum Abschließen der Aufgabe benötigt wird. Wenn Sie z. B. alle drei Stunden einen Auftrag ausführen und die Aufgabe 40 Minuten dauert, können Sie die geplante Zeit ändern.

### Befehl

Die `cmd` gibt den auszuführenden Befehl oder das benutzerdefinierte Skript an. Das Befehlsskriptformat kann Folgendes enthalten:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Beispiel:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In diesem Beispiel `<path-to-php-binary>` is `/usr/bin/php`. Das Installationsverzeichnis, das die Projekt-ID enthält, lautet `/app/abc123edf890/bin/magento`und die Skriptaktion lautet `export:start catalog_category_product`.

### Hinzufügen benutzerdefinierter Cron-Aufträge zu Ihrem Projekt

Auf der Adobe Commerce-Plattform für Cloud-Infrastruktur können Sie Anpassungen zur `crons` Abschnitt [`.magento.app.yaml`](../application/configure-app-yaml.md) -Datei.

>[!NOTE]
>
>Für Starterumgebungen und Pro `integration` -Umgebungen entspricht, beträgt das Mindestintervall einmal pro fünf Minuten. Für Pro-Staging- und Produktionsumgebungen beträgt das Mindestintervall einmal pro Minute. Es ist nicht möglich, häufigere Intervalle als die Standardmindestwerte zu konfigurieren.

Bei Adobe Commerce Pro-Projekten wird die [Funktion &quot;Auto-Crons&quot;](#set-up-cron-jobs) muss für Ihr Projekt aktiviert sein, bevor Sie benutzerdefinierte Cron-Aufträge zu Staging- und Produktionsumgebungen hinzufügen können, indem Sie die `.magento.app.yaml` -Datei. Wenn diese Funktion nicht aktiviert ist, [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um Autocrons zu aktivieren.

**Hinzufügen benutzerdefinierter Cron-Aufträge**:

1. Bearbeiten Sie in Ihrer lokalen Entwicklungsumgebung das `.magento.app.yaml` in der Adobe Commerce `/app` Verzeichnis.

1. Im `crons` hinzufügen, fügen Sie Ihre Anpassung im folgenden Format hinzu:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   Im folgenden Beispiel wird die `productcatalog` -Auftrag exportiert den Produktkatalog alle acht Stunden, 20 Minuten nach der Stunde.

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

Um einen benutzerdefinierten Auftrag hinzuzufügen, zu entfernen oder zu aktualisieren, ändern Sie die Konfiguration in der `crons` Abschnitt `.magento.app.yaml` -Datei. Testen Sie dann die Updates auf der Remote-Seite. `integration` Umgebung vor dem Übertragen der Änderungen in die Staging- und Produktionsumgebungen.

## Deaktivieren von Cron-Aufträgen

Sie können Cron-Aufträge manuell deaktivieren, bevor Sie Wartungsaufgaben wie die Neuindizierung oder die Cache-Bereinigung durchführen, um Leistungsprobleme zu vermeiden. Sie können die `ece-tools` CLI, Befehl `cron:disable` um alle Cron-Aufträge zu deaktivieren und alle aktiven Cron-Prozesse zu beenden.

**So deaktivieren Sie Cron-Aufträge**:

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

Adobe hat das Adobe Commerce-Paket zur Cloud-Infrastruktur aktualisiert, um die Cron-Verarbeitung auf der Adobe Commerce-Cloud-Infrastrukturplattform zu optimieren und Kron-bezogene Probleme zu beheben. Wenn Probleme mit der Cron-Verarbeitung auftreten, stellen Sie sicher, dass Ihr Projekt die neueste Version des `ece-tools` Paket. Siehe [ECE-Tools aktualisieren](../dev-tools/update-package.md).

Sie können die Informationen zur Cron-Verarbeitung in den Protokolldateien auf Anwendungsebene für jede Umgebung überprüfen. Siehe [Anwendungsprotokolle](../test/log-locations.md#application-logs).

In den folgenden Adobe Commerce-Supportartikeln finden Sie Hilfe zur Fehlerbehebung bei Problemen mit Cron-Angriffen:

- [Cron-Aufgaben sperren Aufgaben von anderen Gruppen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Zurücksetzen von Cron-Aufträgen manuell in der Cloud zurücksetzen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
