---
title: Backup-Management
description: Erfahren Sie, wie Sie ein Backup für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur manuell erstellen und wiederherstellen.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: 4c3f3f2775e8327476233520e52b589f7264786f
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Backup-Management

Sie können eine manuelle Sicherung aktiver Starterumgebungen jederzeit mithilfe des **[!UICONTROL Backup]** im [!DNL Cloud Console] oder unter Verwendung der `magento-cloud snapshot:create` Befehl.

Ein Backup oder _Schnappschuss_ ist eine vollständige Sicherung der Umgebungsdaten, die alle persistenten Daten aus laufenden Diensten (MySQL-Datenbank) und allen Dateien enthält, die auf den bereitgestellten Volumes gespeichert sind (var, pub/media, app/etc). Der Schnappschuss _not_ Code einschließen, da der Code bereits im Git-basierten Repository gespeichert ist. Sie können keine Kopie einer Momentaufnahme herunterladen.

Die Sicherungs-/Snapshot-Funktion **not** gelten für die Staging- und Produktionsumgebungen von Pro, die standardmäßig regelmäßige Backups für Disaster Recovery erhalten. Siehe Abschnitt [Pro Backup und Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery) für weitere Informationen. Im Gegensatz zu automatischen Live-Backups in der Pro Staging- und Produktionsumgebung sind Backups **not** automatisch. Es ist _Ihre_ Verantwortung für die manuelle Erstellung eines Backups oder die Einrichtung eines Cron-Auftrags, um regelmäßig eine Sicherung Ihrer Starter- oder Pro-Integrationsumgebungen zu erstellen.

## Manuelles Backup erstellen

Sie können eine manuelle Sicherung einer aktiven Starter-Umgebung und einer Integration Pro-Umgebung aus dem [!DNL Cloud Console] oder erstellen Sie einen Schnappschuss aus der Cloud-CLI. Sie müssen über eine [Administratorrolle](../project/user-access.md) für die Umwelt.

**So erstellen Sie eine Sicherung einer Starter-Umgebung mit dem[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Wählen Sie in der Projektnavigationsleiste eine Umgebung aus. Die Umgebung muss aktiv sein.
1. Im _Backups_ Ansicht, klicken Sie **[!UICONTROL Backup]**. Diese Option ist in einer Pro-Umgebung nicht verfügbar.

   ![Backup](../../assets/button-backup.png){width="150"}

**So erstellen Sie eine Sicherung einer Integrationsumgebung mit dem[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Wählen Sie in der Projektnavigationsleiste eine Integration/Entwicklungsumgebung aus. Die Umgebung muss aktiv sein.
1. Wählen Sie die **[!UICONTROL Backup]** im Menü oben rechts. Diese Option ist sowohl für Starter- als auch für Pro-Umgebungen verfügbar.
1. Klicken Sie auf **[!UICONTROL Yes]** Schaltfläche.

**So erstellen Sie einen Schnappschuss mit dem `magento-cloud` CLI**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Sehen Sie sich die zu Momentaufnahmen gehörige Umgebungsverzweigung an.
1. Erstellen Sie den Schnappschuss.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Alternativ können Sie die `magento-cloud backup` short -Befehl. Die `--live` lässt die Umgebung laufen, um Ausfallzeiten zu vermeiden. Eine vollständige Liste der Optionen erhalten Sie durch Eingabe von `magento-cloud snapshot:create --help`.

   Beispielantwort:

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Überprüfen Sie die neuesten Momentaufnahmen.

   ```bash
   magento-cloud snapshot:list
   ```

   Die Liste gibt Informationen zum Snapshot-Status zurück:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Manuelles Backup wiederherstellen

Sie müssen [Administratorzugriff](../project/user-access.md) in die Umwelt. Sie können **sieben Tage** nach _Wiederherstellen_ eine manuelle Sicherung. Beim Wiederherstellen einer Sicherung wird der Code der aktuellen Git-Verzweigung nicht geändert. Die Wiederherstellung einer Sicherung auf diese Weise gilt nicht für Staging- und Produktionsumgebungen von Pro; siehe [Pro Backup und Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Die Wiederherstellungszeiten variieren je nach Größe Ihrer Datenbank:

- Eine große Datenbank (200+ GB) kann 5 Stunden dauern
- mittlere Datenbank (150 GB) kann 2 1/2 Stunden dauern
- Eine kleine Datenbank (60 GB) kann eine Stunde dauern

>[!TIP]
>
>Wiederherstellung ohne Sicherung:
>
>- Informationen zum Zurücksetzen auf vorherigen Code oder zum Entfernen hinzugefügter Erweiterungen in einer Umgebung finden Sie unter [Zurücksetzen-Code](#roll-back-code).
>- Wiederherstellung einer instabilen Umgebung, die _not_ eine Sicherung haben, siehe [Wiederherstellen einer Umgebung](../development/restore-environment.md).

**So stellen Sie eine Sicherung mithilfe der[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Wählen Sie in der Projektnavigationsleiste eine Umgebung aus.
1. Im _Backups_ Ansicht, wählen Sie ein Backup aus der _Gespeichert_ Liste. Die Sicherungsfunktion **not** gelten für die Pro-Umgebungen.
1. Im ![Mehr](../../assets/icon-more.png){width="32"} (_more_), klicken Sie auf **Wiederherstellen**.
1. Überprüfen Sie die Sicherungsinformationen und klicken Sie auf **Ja, wiederherstellen**.

**So stellen Sie einen Schnappschuss mithilfe der Cloud CLI wieder her**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Sehen Sie sich die wiederherzustellende Umgebungsverzweigung an.
1. Auflisten aller verfügbaren Momentaufnahmen.

   ```bash
   magento-cloud snapshot:list
   ```

   Die Liste gibt Informationen zu den verfügbaren Momentaufnahmen zurück:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Wiederherstellen eines Snapshots mithilfe der Snapshot-ID aus der Liste.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Wiederherstellen eines Snapshots zur Notfallwiederherstellung

So stellen Sie den Snapshot zur Notfallwiederherstellung in der Staging- und Produktionsumgebung von Pro wieder her: [Importieren Sie die Datenbank-Dump direkt vom Server.](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3).

## Zurücksetzen-Code

Sicherungen und Momentaufnahmen tun dies _not_ eine Kopie Ihres Codes enthalten. Ihr Code ist bereits im Git-basierten Repository gespeichert, sodass Sie Git-basierte Befehle verwenden können, um den Code zurückzusetzen (oder wiederherzustellen). Verwenden Sie beispielsweise `git log --oneline` zum Scrollen durch vorherige Commands und dann [`git revert`](https://git-scm.com/docs/git-revert) um Code aus einem bestimmten Commit wiederherzustellen.

Außerdem können Sie Code in einem _inactive_ -Verzweigung. Verwenden Sie Git-Befehle, um eine Verzweigung zu erstellen, anstatt `magento-cloud` Befehle. Siehe auch [Git-Befehle](../dev-tools/cloud-cli-overview.md#git-commands) im Cloud-CLI-Thema.
