---
title: Cloud-CLI
description: Erfahren Sie mehr über die Befehlszeilenschnittstelle von magento-cloud und wie Sie damit lokale Entwicklungsumgebungen für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur verwalten können.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Cloud-CLI

Die `magento-cloud` Das CLI-Tool ermöglicht es Entwicklern und Systemadministratoren, Cloud-Projekte und -Umgebungen zu verwalten, Routinen durchzuführen und Automatisierungsaufgaben durchzuführen. Die `magento-cloud` CLI erweitert die Funktionen der [[!DNL Cloud Console]](../../get-started/cloud-console.md). Nach der Installation `magento-cloud` CLI auf Ihrer lokalen Workstation können Sie damit Ihre Adobe Commerce in Cloud-Infrastruktur-Starter- und Pro-Integrationsumgebungen verwalten.

**So installieren Sie die `magento-cloud` CLI**:

1. Wechseln Sie auf Ihrer lokalen Workstation zu dem Ordner, in dem Sie das Cloud-Projekt klonen möchten, und zu dem Speicherort der [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) has _schreiben_ Zugriff.

1. Installieren Sie die `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Hinzufügen `magento-cloud` CLI zum Bash-Profil.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Laden Sie das aktualisierte Bash-Profil erneut.

   ```bash
   . ~/.bash_profile
   ```

1. Um die CLI zu starten, rufen Sie `magento-cloud` und geben Sie bei Aufforderung Ihre Anmeldedaten für das Cloud-Konto ein.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Überprüfen Sie die `magento-cloud` -Befehl sich in Ihrem Pfad befindet. Im folgenden Beispiel werden die verfügbaren Befehle aufgelistet.

   ```bash
   magento-cloud list
   ```

## Allgemeine Befehle

Adobe hat diese Befehle zum Verwalten von Cloud-Integrationsumgebungen entwickelt und empfiehlt, dass Sie die `magento-cloud` CLI aus einem Projektverzeichnis, damit Sie die `-p <project-ID>` -Parameter.

Die folgende Liste der häufig verwendeten `magento-cloud` CLI-Befehle enthalten nur erforderliche Optionen. Sie können die `--help` -Option mit jedem Befehl, um weitere Informationen anzuzeigen.

| Befehl | Beschreibung |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Melden Sie sich beim Projekt an. |
| `magento-cloud list` | Geben Sie die verfügbaren Befehle für das CLI-Tool an. |
| `magento-cloud environment:list` | Geben Sie die Umgebungen im aktuellen Projekt an. |
| `magento-cloud environment:checkout` | Sehen Sie sich eine vorhandene Umgebung an. |
| `magento-cloud environment:merge -e` | Zusammenführen von Änderungen in dieser Umgebung mit der übergeordneten Umgebung. |
| `magento-cloud variables` | Listenvariablen in dieser Umgebung. |
| `magento-cloud ssh` | Verwenden Sie SSH, um eine Verbindung zur Remote-Umgebung herzustellen. |
| `magento-cloud url` | Öffnen Sie die Adobe Commerce-Storefront in einem Browser. |
| `magento-cloud web` | Öffnen Sie die [!DNL Cloud Console]. |

## Umgebungsbefehle

Umwelt _name_ unterscheidet sich von der Umgebung _ID_ nur, wenn Sie Leerzeichen oder Großbuchstaben im Umgebungsnamen verwenden. Eine Umgebungs-ID besteht aus allen Kleinbuchstaben, Zahlen und zulässigen Symbolen. Großbuchstaben in einem Umgebungsnamen werden in der ID in Kleinbuchstaben umgewandelt; Leerzeichen in einem Umgebungsnamen werden in Bindestriche umgewandelt.

Ein Umgebungsname _cannot_ -Zeichen einschließen, die für Ihre Linux-Shell oder reguläre Ausdrücke reserviert sind. Unzulässige Zeichen sind geschweifte Klammern (`{ }`), Klammern, Sternchen (`*`), spitze Klammern (`< >`), Und-Zeichen (`&`), Prozent (`%`) und anderen Zeichen.

Die `magento-cloud environment:list` -Befehl zeigt Umgebungshierarchien an, während `git branch` nicht. Wenn Sie verschachtelte Umgebungen haben, verwenden Sie Folgendes:

```bash
magento-cloud environment:list
```

### Bereitstellung der Umgebung

Trigger einer Neuimplementierung ohne Push-Benachrichtigung. Überprüfen und bestätigen Sie die Umgebung für die erneute Bereitstellung. Verwenden Sie keine Neubereitstellung, wenn ein Build in einem ausstehenden Status vorliegt.

```bash
magento-cloud environment:redeploy
```

Beispielantwort:

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Git-Befehle

Sie werden feststellen, dass einige dieser Befehle Git-Befehlen ähneln. Die `magento-cloud` -Befehle stellen eine direkte Verbindung zum Git-basierten Cloud-Projekt mit zusätzlichen Funktionen her. Wenn Sie eine Verzweigung erstellen, ohne die `magento-cloud` CLI: Es wird nicht &quot;aktiviert&quot;und wird nicht automatisch erstellt, wenn Sie Änderungen an die Remote-Umgebung pushen. Die `magento-cloud` Der CLI-Befehl beinhaltet die Aktivierung.

Verwenden Sie zum Erstellen einer Verzweigung die `magento-cloud` -Befehl, damit die Verzweigung aktiviert ist.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Für den Zweigstatus:

- Verwenden Sie die `magento-cloud env` -Befehl, um eine Liste der Verzweigungen der Umgebung und deren Status anzuzeigen: aktiv oder inaktiv.
- Verwenden Sie die `magento-cloud environment:activate` -Befehl zum Aktivieren einer Umgebungsverzweigung.

Senden Sie eine leere Git-Bestätigung an den Trigger einer Bereitstellung. Beispiel:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Einige Aktionen, wie das Hinzufügen eines Benutzers, führen nicht zur Bereitstellung.

### Umgebungsverzweigung erstellen

Die folgenden Schritte zeigen die Verwendung der Befehle CLI und Git zur austauschbaren Verwaltung Ihrer lokalen Umgebung:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Wechseln Sie zu [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Melden Sie sich bei Ihrem Projekt an.

   ```bash
   magento-cloud login
   ```

1. Geben Sie Ihre Projekte an.

   ```bash
   magento-cloud project:list
   ```

1. Auflisten von Umgebungen im Projekt. Jede Umgebung enthält eine aktive Git-Verzweigung, die Ihren Code, Ihre Datenbank, Umgebungsvariablen, Konfigurationen und Dienste enthält.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >Es ist wichtig, die `magento-cloud environment:list` -Befehl, da er Umgebungshierarchien anzeigt, während die `git branch` nicht.

1. Rufen Sie die Ausgangsverzweigungen ab, um den neuesten Code zu erhalten.

   ```bash
   git fetch origin
   ```

1. Checken Sie einen bestimmten Zweig und eine bestimmte Umgebung aus oder wechseln Sie zu dieser.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git-Befehle checken nur die Git-Verzweigung aus. Die `magento-cloud checkout` -Befehl checkt den Zweig aus und wechselt zur aktiven Umgebung.

   >[!TIP]
   >
   >Sie können eine Umgebungsverzweigung mit der `magento-cloud environment:branch <environment-name> <parent-environment-ID>` -Befehlssyntax fest. Es kann einige zusätzliche Zeit in Anspruch nehmen, einen Umgebungs-Zweig zu erstellen und zu aktivieren.

1. Verwenden Sie die Umgebungs-ID, um jeden aktualisierten Code zu Ihrem lokalen Speicherort abzurufen. Dies ist nicht erforderlich, wenn der Umgebungszweig neu ist.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Optional_) Erstellen Sie eine [Schnappschuss](../storage/snapshots.md) der Umgebung als Sicherung.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## CLI aktualisieren

Die `magento-cloud` Die CLI sucht nach verfügbaren Updates, wenn Sie sich anmelden. Sie können jedoch mithilfe der `self:update` Befehl. Wenn ein Update verfügbar ist, befolgen Sie die Anweisungen zum Aktualisieren der CLI.

Wenn `magento-cloud` Die CLI ist aktuell und Sie sehen die folgende Antwort:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
