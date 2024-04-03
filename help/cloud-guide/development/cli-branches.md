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

So installieren Sie die `magento-cloud` CLI, siehe [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md). Nach der Installation `magento-cloud` CLI verwenden und SSH-Schlüssel für den Remote-Zugriff auf Ihre Cloud-Infrastruktur einrichten, können Sie `magento-cloud` CLI-Befehle zum Verwalten der Umgebungen für Ihre Projekte. Informationen zur Umgebungsarchitektur finden Sie unter [Starterarchitektur](../architecture/starter-architecture.md) oder [Pro Architektur](../architecture/pro-architecture.md).

So verwalten Sie Zweige und Umgebungen mit dem [!DNL Cloud Console], siehe [Verwalten von Verzweigungen mit [!DNL Cloud Console]](../project/console-branches.md).

## CLI-Befehle verwenden

Die `magento-cloud` CLI-Befehle ähneln Git-Befehlen. Sie können sie verwenden, um eine Verbindung zu Ihrem Projekt herzustellen und Ihre Umgebungen zu verwalten. Sie können die Befehle zwar aus einem beliebigen Verzeichnis ausführen, es wird jedoch empfohlen, sie in einem Projektverzeichnis auszuführen. Bei Ausführung in einem Projektverzeichnis können Sie die `-p <project-ID>` -Parameter. Siehe [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md).

## Projekt klonen

Die folgenden Anweisungen verwenden eine Kombination aus `magento-cloud` CLI-Befehle und Git-Befehle zum Klonen Ihres Projekts auf Ihrer lokalen Workstation. Die vollständige Liste der `magento-cloud` CLI-Befehle, verwenden Sie `magento-cloud list` Befehl.

>[!IMPORTANT]
>
>Einige Git-Befehle können keine Aktion in Ihrem Adobe Commerce-Projekt zur Cloud-Infrastruktur durchführen. Sie können beispielsweise eine Verzweigung mithilfe eines Git-Befehls erstellen, eine neue Umgebung jedoch nicht erstellen und aktivieren. Sie müssen eine Umgebung mit dem `magento-cloud environment:branch <branch-name>` -Befehl, damit die Umgebung _active_. Alternativ können Sie die [!DNL Cloud Console] , um aktive Umgebungen zu erstellen. Siehe [Cloud-CLI-Referenz](../dev-tools/cloud-cli-overview.md#git-commands).

**Klonen eines Projekts `master` Umgebung**:

1. Melden Sie sich bei Ihrer lokalen Workstation mit einer [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) -Konto.

1. Wechsel zum Webserver oder virtuellen Host _docroot_ Verzeichnis.

1. Mit der `magento-cloud` CLI.

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

1. Ändern Sie die `magento2` Verzeichnis.

1. Liste der verfügbaren Umgebungen für das Projekt.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >Die `magento-cloud environment:list` -Befehl zeigt Umgebungshierarchien an, während der `git branch` nicht.

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
>Siehe [Integrationen](../integrations/overview.md) für Informationen zur Verwendung von Git-basierten Hosting-Diensten mit Adobe Commerce in der Cloud-Infrastruktur.

## Erstellen einer Verzweigung für die Entwicklung

Nachdem Sie Ihr Projekt geklont und die Konfiguration des Adobe Commerce-Administratorkontos aktualisiert haben, können Sie zur Entwicklung verzweigen. Wie bereits erwähnt, müssen Sie eine Umgebung mit dem `magento-cloud environment:branch <branch-name>` oder [!DNL Cloud Console] für die Umwelt _active_.

- Für [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch)sollten Sie erwägen, eine Verzweigung für `staging`, erstellen Sie dann eine Entwicklungsverzweigung basierend auf der `staging` -Verzweigung.
- Für [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), erstellen Sie Entwicklungszweige basierend auf dem `Integration` -Verzweigung.

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

1. [_optional_] Erstellen Sie eine [Backup](../storage/snapshots.md) der Umwelt.

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
>Sie können die `master` -Verzweigung eines Projekts.

Sie müssen ein Projekt-Administrator, ein Umgebungsadministrator oder Kontoinhaber sein, um diese Aufgabe durchführen zu können. Siehe [Benutzerzugriff auf Cloud-Projekte verwalten](../project/user-access.md).

Wenn Sie eine Umgebung löschen, wird die Umgebung auf _inactive_. Der Code ist weiterhin in der Git-Verzweigung verfügbar, enthält jedoch nicht mehr die Dienste oder die Datenbank. Um die Umgebung vollständig zu löschen, müssen Sie auch die entsprechende Remote-Git-Verzweigung löschen.

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

   Durch Löschen der Umgebung wird sie in einer _inactive_ state.

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
>Um eine inaktive Umgebung zu aktivieren, verwenden Sie die `magento-cloud environment:activate` Befehl.

## Interagieren mit Remote-Umgebungen

Nach [SSH-Schlüssel einrichten](../development/secure-connections.md), können Sie [Verbindung von Ihrem lokalen Arbeitsbereich zu einer Remote-Umgebung herstellen](../development/secure-connections.md#connect-to-a-remote-environment) und interagieren Sie mit Ihren Projektdiensten und ändern Sie die Einstellungen.
