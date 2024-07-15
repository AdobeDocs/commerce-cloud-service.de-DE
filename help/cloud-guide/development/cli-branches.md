---
title: Verwalten von Zweigen mit der CLI
description: Erfahren Sie, wie Sie die Umgebungsverzweigungen für Adobe Commerce in der Cloud-Infrastruktur mithilfe der Cloud-CLI verwalten.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Verwalten von Zweigen mit der CLI

Informationen zum Installieren der `magento-cloud`-CLI finden Sie in der [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md). Nachdem Sie die `magento-cloud` -CLI installiert und SSH-Schlüssel für den Remote-Zugriff auf Ihre Cloud-Infrastruktur eingerichtet haben, können Sie die Umgebungen für Ihre Projekte mit `magento-cloud` -CLI-Befehlen verwalten. Informationen zur Umgebungsarchitektur finden Sie unter [Starter Architecture](../architecture/starter-architecture.md) oder [Pro Architecture](../architecture/pro-architecture.md).

Informationen zum Verwalten der Verzweigungen und Umgebungen mit dem [!DNL Cloud Console] finden Sie unter [Verwalten von Verzweigungen mit dem  [!DNL Cloud Console]](../project/console-branches.md).

## CLI-Befehle verwenden

Die `magento-cloud` CLI-Befehle ähneln den Git-Befehlen. Sie können sie verwenden, um eine Verbindung zu Ihrem Projekt herzustellen und Ihre Umgebungen zu verwalten. Sie können die Befehle zwar aus einem beliebigen Verzeichnis ausführen, es wird jedoch empfohlen, sie in einem Projektverzeichnis auszuführen. Wenn Sie von einem Projektverzeichnis aus ausgeführt werden, können Sie den Parameter `-p <project-ID>` auslassen. Siehe [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md).

## Projekt klonen

Die folgenden Anweisungen verwenden eine Kombination aus `magento-cloud` CLI-Befehlen und Git-Befehlen, um Ihr Projekt auf Ihrer lokalen Workstation zu klonen. Verwenden Sie den Befehl `magento-cloud list` , um eine vollständige Liste der Befehle von `magento-cloud` CLI anzuzeigen.

>[!IMPORTANT]
>
>Einige Git-Befehle können keine Aktion in Ihrem Adobe Commerce-Projekt zur Cloud-Infrastruktur durchführen. Sie können beispielsweise eine Verzweigung mithilfe eines Git-Befehls erstellen, eine neue Umgebung jedoch nicht erstellen und aktivieren. Sie müssen eine Umgebung mit dem Befehl `magento-cloud environment:branch <branch-name>` erstellen, damit die Umgebung _aktiv_ wird. Alternativ können Sie die [!DNL Cloud Console] verwenden, um aktive Umgebungen zu erstellen. Siehe [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md#git-commands).

**So klonen Sie ein Projekt `master` environment**:

1. Melden Sie sich mit einem [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) -Konto bei Ihrer lokalen Workstation an.

1. Wechseln Sie zum Ordner &quot;_docroot_&quot;des Webservers oder virtuellen Hosts.

1. Melden Sie sich mit der CLI `magento-cloud` an.

   ```bash
   magento-cloud login
   ```

1. Geben Sie Ihre Projekte an.

   ```bash
   magento-cloud project:list
   ```

1. Klonen Sie ein Projekt.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Geben Sie bei Aufforderung einen Ordnernamen an.

1. Wechseln Sie zum Ordner &quot;`magento2`&quot;.

1. Liste der verfügbaren Umgebungen für das Projekt.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >Der Befehl `magento-cloud environment:list` zeigt Umgebungshierarchien an, der Befehl `git branch` dagegen nicht.

1. Rufen Sie die Remote-Zweige ab.

   ```bash
   git fetch origin
   ```

1. Aktualisierten Code abrufen.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Informationen zur Verwendung von Git-basierten Hosting-Diensten mit Adobe Commerce in der Cloud-Infrastruktur finden Sie unter [Integrationen](../integrations/overview.md) .

## Erstellen einer Verzweigung für die Entwicklung

Nachdem Sie Ihr Projekt geklont und die Konfiguration des Adobe Commerce-Administratorkontos aktualisiert haben, können Sie zur Entwicklung verzweigen. Wie bereits erwähnt, müssen Sie eine Umgebung mit dem Befehl `magento-cloud environment:branch <branch-name>` oder dem Befehl [!DNL Cloud Console] erstellen, damit die Umgebung _aktiv_ wird.

- Für [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch) sollten Sie eine Verzweigung für `staging` erstellen und dann eine Entwicklungsverzweigung erstellen, die auf der Verzweigung `staging` basiert.
- Erstellen Sie für [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow) Entwicklungszweige basierend auf der `Integration` -Verzweigung.

**So erstellen Sie einen Entwicklungszweig**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Erstellen Sie eine Umgebung basierend auf der für Ihren Projekt-Workflow empfohlenen Verzweigung.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Aktualisieren von Abhängigkeiten.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_optional_] Erstellen Sie eine [Sicherung](../storage/snapshots.md) der Umgebung.

### Zusammenführen einer Verzweigung

Führen Sie nach Abschluss der Entwicklung diesen Zweig mit dem übergeordneten Element zusammen:

1. Änderungen an Zustimmungs- und Push-Code:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Mit der übergeordneten Umgebung zusammenführen:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Löschen einer Umgebung

Löschen Sie eine Umgebung nur, wenn Sie sicher sind, dass Sie sie nicht mehr benötigen. Eine Umgebung kann nach dem Löschen nicht mehr wiederhergestellt werden.

>[!WARNING]
>
>Sie können den Zweig `master` eines Projekts nicht löschen.

Sie müssen ein Projekt-Administrator, ein Umgebungsadministrator oder Kontoinhaber sein, um diese Aufgabe durchführen zu können. Siehe [Verwalten des Benutzerzugriffs auf Cloud-Projekte](../project/user-access.md).

Wenn Sie eine Umgebung löschen, wird die Umgebung auf _inactive_ gesetzt. Der Code ist weiterhin in der Git-Verzweigung verfügbar, enthält jedoch nicht mehr die Dienste oder die Datenbank. Um die Umgebung vollständig zu löschen, müssen Sie auch die entsprechende Remote-Git-Verzweigung löschen.

**Löschen einer Umgebung**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Rufen Sie Aktualisierungen vom Remote-Server ab.

   ```bash
   git fetch
   ```

1. Löschen Sie die Umgebungsverzweigung.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   Optional können Sie mehrere Umgebungen gleichzeitig löschen, indem Sie dem Löschbefehl mehrere Umgebungs-IDs hinzufügen.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Beantworten Sie die Anweisungen zum Löschen der lokalen Umgebung und der entsprechenden Remote-Umgebung.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   Durch Löschen der Umgebung wird sie in den Status _inactive_ versetzt.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   Durch Löschen der Remote-Git-Verzweigung wird die Umgebung aus dem Projekt entfernt.

1. Warten Sie, bis die Umgebung gelöscht ist.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Verwenden Sie den Befehl `magento-cloud environment:activate` , um eine inaktive Umgebung zu aktivieren.

## Interagieren mit Remote-Umgebungen

Nachdem Sie [ SSH-Schlüssel eingerichtet haben](../development/secure-connections.md), können Sie [ eine Verbindung von Ihrem lokalen Arbeitsbereich zu einer Remote-Umgebung herstellen](../development/secure-connections.md#connect-to-a-remote-environment), mit Ihren Projektdiensten interagieren und Einstellungen ändern.
