---
title: Datenbank sichern
description: Erfahren Sie, wie Sie mit ECE-Tools eine Sicherung der Datenbank für ein Adobe Commerce-Projekt zur Cloud-Infrastruktur erstellen.
feature: Cloud, Iaas, Storage
exl-id: 8a96effe-a587-4edf-b0c7-e73ca8d3b56c
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Datenbank sichern

Sie können eine Kopie Ihrer Datenbank mithilfe der Variablen `ece-tools db-dump` ohne alle Umgebungsdaten aus Diensten und Bereitstellungen zu erfassen. Standardmäßig erstellt dieser Befehl Backups im `/app/var/dump-main` für alle Datenbankverbindungen, die in der Umgebungskonfiguration angegeben sind. Der DB-Dump-Vorgang wechselt die Anwendung in den Wartungsmodus, stoppt Prozesse in der Verbraucherwarteschlange und deaktiviert Cron-Aufträge, bevor der Dump beginnt.

Beachten Sie die folgenden Richtlinien für DB-Dump:

- Für Produktionsumgebungen empfiehlt Adobe, Datenbankabbildvorgänge außerhalb der Spitzenzeiten durchzuführen, um Dienstunterbrechungen zu minimieren, die auftreten, wenn sich die Site im Wartungsmodus befindet.
- Wenn während des Dump-Vorgangs ein Fehler auftritt, löscht der Befehl die Dump-Datei, um Speicherplatz zu sparen. Überprüfen Sie die Protokolle auf Details (`var/log/cloud.log`).
- In Pro-Produktionsumgebungen werden mit diesem Befehl nur Daten aus _one_ von den drei Hochverfügbarkeitsknoten, sodass Produktionsdaten, die während des Dump in einen anderen Knoten geschrieben wurden, möglicherweise nicht kopiert werden. Der Befehl generiert eine `var/dbdump.lock` -Datei, um zu verhindern, dass der Befehl auf mehr als einem Knoten ausgeführt wird.
- Für eine Sicherung aller Umgebungsdienste empfiehlt Adobe die Erstellung einer [Backup](snapshots.md).

Sie können mehrere Datenbanken sichern, indem Sie die Datenbanknamen an den Befehl anhängen. Im folgenden Beispiel werden zwei Datenbanken gesichert: `main` und `sales`:

```bash
php vendor/bin/ece-tools db-dump main sales
```

Verwenden Sie die `php vendor/bin/ece-tools db-dump --help` für weitere Optionen:

- `--dump-directory=<dir>`—Wählen Sie ein Zielverzeichnis für die Datenbank-Dump aus.
- `--remove-definers`—DEFINER-Anweisungen aus der Datenbank-Dump entfernen

**Erstellen einer Datenbank-Dump in der Staging- oder Produktionsumgebung**:

1. [Verwenden Sie SSH, um sich anzumelden oder einen Tunnel zu erstellen, um eine Verbindung zur Remote-Umgebung herzustellen.](../development/secure-connections.md) , die die zu kopierende Datenbank enthält.

1. Führen Sie die Umgebungsbeziehungen auf und notieren Sie sich die Informationen zur Datenbankanmeldung.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   oder

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Erstellen Sie eine Sicherung der Datenbank. Um ein Zielverzeichnis für den DB-Dump auszuwählen, verwenden Sie die `--dump-directory` -Option.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Beispielantwort:

   ```terminal
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. Die `db-dump` -Befehl erstellt eine `dump-<timestamp>.sql.gz` Archivdatei im Remote-Projektverzeichnis.

>[!TIP]
>
>Wenn Sie diese Daten in eine bestimmte Umgebung übertragen möchten, lesen Sie [Migrieren von Daten und statischen Dateien](../deploy/staging-production.md#migrate-static-files).
