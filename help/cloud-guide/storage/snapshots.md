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

Sie können eine manuelle Sicherung aktiver Starterumgebungen jederzeit mithilfe der Schaltfläche **[!UICONTROL Backup]** im Befehl [!DNL Cloud Console] oder mithilfe des Befehls `magento-cloud snapshot:create` durchführen.

Ein Backup oder _Schnappschuss_ ist eine vollständige Sicherung von Umgebungsdaten, die alle persistenten Daten aus laufenden Diensten (MySQL-Datenbank) sowie alle Dateien enthält, die auf den bereitgestellten Volumes gespeichert sind (var, pub/media, app/etc). Der Snapshot enthält den Code _nicht_ , da der Code bereits im Git-basierten Repository gespeichert ist. Sie können keine Kopie einer Momentaufnahme herunterladen.

Die Sicherungs-/Snapshot-Funktion gilt **nicht** für die Pro-Staging- und Produktionsumgebungen, die standardmäßig regelmäßige Backups für Disaster Recovery erhalten. Weitere Informationen finden Sie unter [Pro Backup &amp; Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery) . Im Gegensatz zu den automatischen Live-Backups in den Pro Staging- und Produktionsumgebungen sind Backups **nicht** automatisch. Es liegt in der Verantwortung von _Ihrer_, manuell eine Sicherung zu erstellen oder einen Cron-Auftrag einzurichten, um regelmäßig eine Sicherung Ihrer Starter- oder Pro-Integrationsumgebungen zu erstellen.

## Manuelles Backup erstellen

Sie können eine manuelle Sicherung einer aktiven Starter-Umgebung und einer Integration Pro-Umgebung aus der Umgebung [!DNL Cloud Console] erstellen oder einen Schnappschuss aus der Cloud-CLI erstellen. Sie müssen über eine [Administratorrolle](../project/user-access.md) für die Umgebung verfügen.

**So erstellen Sie eine Sicherung einer Starterumgebung mit dem[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.
1. Wählen Sie in der Projektnavigationsleiste eine Umgebung aus. Die Umgebung muss aktiv sein.
1. Klicken Sie in der Ansicht _Backups_ auf **[!UICONTROL Backup]**. Diese Option ist in einer Pro-Umgebung nicht verfügbar.

   ![Backup](../../assets/button-backup.png){width="150"}

**So erstellen Sie eine Sicherung einer Integrationsumgebung mit dem[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.
1. Wählen Sie in der Projektnavigationsleiste eine Integration/Entwicklungsumgebung aus. Die Umgebung muss aktiv sein.
1. Wählen Sie im Menü oben rechts die Option **[!UICONTROL Backup]** aus. Diese Option ist sowohl für Starter- als auch für Pro-Umgebungen verfügbar.
1. Klicken Sie auf die Schaltfläche **[!UICONTROL Yes]** .

**So erstellen Sie einen Schnappschuss mit der `magento-cloud` CLI**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Sehen Sie sich die zu Momentaufnahmen gehörige Umgebungsverzweigung an.
1. Erstellen Sie den Schnappschuss.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Alternativ können Sie den Befehl `magento-cloud backup` short verwenden. Die Option `--live` lässt die Umgebung laufen, um Ausfallzeiten zu vermeiden. Geben Sie `magento-cloud snapshot:create --help` ein, um eine vollständige Liste der Optionen anzuzeigen.

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

Sie benötigen [Administratorzugriff](../project/user-access.md) auf die Umgebung. Sie haben bis zu **sieben Tage**, um _ein manuelles Backup wiederherzustellen_. Beim Wiederherstellen einer Sicherung wird der Code der aktuellen Git-Verzweigung nicht geändert. Das Wiederherstellen einer Sicherung auf diese Weise gilt nicht für Pro-Staging- und Produktionsumgebungen; siehe [Pro-Sicherung und Disaster Recovery](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Die Wiederherstellungszeiten variieren je nach Größe Ihrer Datenbank:

- Eine große Datenbank (200+ GB) kann 5 Stunden dauern
- mittlere Datenbank (150 GB) kann 2 1/2 Stunden dauern
- Eine kleine Datenbank (60 GB) kann eine Stunde dauern

>[!TIP]
>
>Wiederherstellung ohne Sicherung:
>
>- Weitere Informationen zum Zurücksetzen auf vorherigen Code oder zum Entfernen hinzugefügter Erweiterungen in einer Umgebung finden Sie unter [Zurücksetzen des Codes](#roll-back-code).
>- Informationen zum Wiederherstellen einer instabilen Umgebung, in der _nicht_ gesichert ist, finden Sie unter [Wiederherstellen einer Umgebung](../development/restore-environment.md).

**So stellen Sie eine Sicherung mit dem[!DNL Cloud Console]** wieder her:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.
1. Wählen Sie in der Projektnavigationsleiste eine Umgebung aus.
1. Wählen Sie in der Ansicht _Backups_ ein Backup aus der Liste _Gespeichert_ aus. Die Sicherungsfunktion gilt für die Pro-Umgebungen nicht mehr als **.**
1. Klicken Sie im Menü ![Mehr](../../assets/icon-more.png){width="32"} (_mehr_) auf **Wiederherstellen**.
1. Überprüfen Sie die Informationen zur Wiederherstellung aus der Sicherung und klicken Sie auf **Ja, stellen Sie** wieder her.

**So stellen Sie einen Schnappschuss mithilfe der Cloud-CLI wieder her**:

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

Um den Schnappschuss zur Notfallwiederherstellung in Pro Staging- und Produktionsumgebungen wiederherzustellen, importieren Sie die Datenbank-Dump direkt vom Server](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3).[

## Zurücksetzen-Code

Sicherungen und Momentaufnahmen enthalten _nicht_ eine Kopie Ihres Codes. Ihr Code ist bereits im Git-basierten Repository gespeichert, sodass Sie Git-basierte Befehle verwenden können, um den Code zurückzusetzen (oder wiederherzustellen). Verwenden Sie beispielsweise &quot;`git log --oneline`&quot;, um durch vorherige Commits zu blättern, und verwenden Sie dann &quot;[`git revert`](https://git-scm.com/docs/git-revert)&quot;, um den Code aus einem bestimmten Commit wiederherzustellen.

Außerdem können Sie Code in einer _inaktiven_ -Verzweigung speichern. Verwenden Sie Git-Befehle, um eine Verzweigung zu erstellen, anstatt `magento-cloud`-Befehle zu verwenden. Weitere Informationen zu [Git-Befehlen](../dev-tools/cloud-cli-overview.md#git-commands) finden Sie im Thema zur Cloud-CLI.
