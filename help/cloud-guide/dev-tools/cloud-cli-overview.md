---
title: Cloud-CLI
description: Erfahren Sie mehr über die Befehlszeilenschnittstelle von magento-cloud und wie Sie damit lokale Entwicklungsumgebungen für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur verwalten können.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Cloud-CLI

Mit dem CLI-Tool `magento-cloud` können Entwickler und Systemadministratoren Cloud-Projekte und -Umgebungen verwalten, Routinen durchführen und Automatisierungsaufgaben ausführen. Die CLI `magento-cloud` erweitert die Funktionen und Funktionen von [[!DNL Cloud Console]](../../get-started/cloud-console.md). Nachdem Sie die `magento-cloud`-CLI auf Ihrer lokalen Workstation installiert haben, können Sie damit Ihre Adobe Commerce in den Integrationsumgebungen &quot;Cloud Infrastructure Starter&quot;und &quot;Pro&quot;verwalten.

**Installieren der `magento-cloud` CLI**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Ordner, in dem Sie das Cloud-Projekt klonen möchten und in dem der [Dateisysteminhaber](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) über den Zugriff auf _write_ verfügt.

1. Installieren Sie die CLI `magento-cloud` .

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Fügen Sie `magento-cloud` CLI zum Bash-Profil hinzu.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Laden Sie das aktualisierte Bash-Profil erneut.

   ```bash
   . ~/.bash_profile
   ```

1. Um die CLI zu starten, rufen Sie `magento-cloud` auf und geben Sie bei Aufforderung Ihre Anmeldedaten für das Cloud-Konto ein.

   ```bash
   magento-cloud
   ```

   ```
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Stellen Sie sicher, dass sich der Befehl `magento-cloud` in Ihrem Pfad befindet. Im folgenden Beispiel werden die verfügbaren Befehle aufgelistet.

   ```bash
   magento-cloud list
   ```

## Allgemeine Befehle

Adobe hat diese Befehle zum Verwalten von Cloud-Integrationsumgebungen entwickelt und empfiehlt, die `magento-cloud`-CLI aus einem Projektverzeichnis auszuführen, damit Sie den Parameter `-p <project-ID>` weglassen können.

Die folgende Liste häufig verwendeter `magento-cloud` CLI-Befehle enthält nur erforderliche Optionen. Sie können die Option `--help` mit jedem Befehl verwenden, um weitere Informationen anzuzeigen.

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

Die Umgebung _name_ unterscheidet sich nur dann von der Umgebung _ID_, wenn Sie Leerzeichen oder Großbuchstaben im Umgebungsnamen verwenden. Eine Umgebungs-ID besteht aus allen Kleinbuchstaben, Zahlen und zulässigen Symbolen. Großbuchstaben in einem Umgebungsnamen werden in der ID in Kleinbuchstaben umgewandelt; Leerzeichen in einem Umgebungsnamen werden in Bindestriche umgewandelt.

Der Umgebungsname _kann keine Zeichen enthalten, die für Ihre Linux-Shell oder reguläre Ausdrücke reserviert sind._ Unzulässige Zeichen sind geschweifte Klammern (`{ }`), Klammern, Sternchen (`*`), spitze Klammern (`< >`), Und-Zeichen (`&`), Prozentzeichen (`%`) und andere Zeichen.

Der Befehl `magento-cloud environment:list` zeigt Umgebungshierarchien an, `git branch` dagegen nicht. Wenn Sie verschachtelte Umgebungen haben, verwenden Sie Folgendes:

```bash
magento-cloud environment:list
```

### Bereitstellung der Umgebung

Trigger einer Neuimplementierung ohne Push-Benachrichtigung. Überprüfen und bestätigen Sie die Umgebung für die erneute Bereitstellung. Verwenden Sie keine Neubereitstellung, wenn ein Build in einem ausstehenden Status vorliegt.

```bash
magento-cloud environment:redeploy
```

Beispielantwort:

```
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Git-Befehle

Sie werden feststellen, dass einige dieser Befehle Git-Befehlen ähneln. Die Befehle `magento-cloud` stellen eine direkte Verbindung zum Git-basierten Cloud-Projekt mit zusätzlichen Funktionen her. Wenn Sie eine Verzweigung ohne Verwendung der CLI `magento-cloud` erstellen, wird diese nicht &quot;aktiviert&quot;und beim Pushen von Änderungen an die Remote-Umgebung nicht automatisch erstellt. Der CLI-Befehl `magento-cloud` beinhaltet die Aktivierung.

Verwenden Sie zum Erstellen einer Verzweigung den Befehl `magento-cloud` , damit die Verzweigung aktiviert wird.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Für den Zweigstatus:

- Verwenden Sie den Befehl `magento-cloud env` , um eine Liste der Verzweigungen der Umgebung und deren Status anzuzeigen: aktiv oder inaktiv.
- Verwenden Sie den Befehl `magento-cloud environment:activate` , um einen Umgebungszweig zu aktivieren.

Senden Sie eine leere Git-Bestätigung an den Trigger einer Bereitstellung. Beispiel:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Einige Aktionen, wie das Hinzufügen eines Benutzers, führen nicht zur Bereitstellung.

### Umgebungsverzweigung erstellen

Die folgenden Schritte zeigen die Verwendung der Befehle CLI und Git zur austauschbaren Verwaltung Ihrer lokalen Umgebung:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Wechseln Sie zum Besitzer des [Dateisystems](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

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
   >Es ist wichtig, den Befehl `magento-cloud environment:list` zu verwenden, da er Umgebungshierarchien anzeigt, während der Befehl `git branch` dies nicht tut.

1. Rufen Sie die Ausgangsverzweigungen ab, um den neuesten Code zu erhalten.

   ```bash
   git fetch origin
   ```

1. Checken Sie einen bestimmten Zweig und eine bestimmte Umgebung aus oder wechseln Sie zu dieser.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git-Befehle checken nur die Git-Verzweigung aus. Der Befehl `magento-cloud checkout` checkt den Zweig aus und wechselt zur aktiven Umgebung.

   >[!TIP]
   >
   >Sie können eine Umgebungsverzweigung mithilfe der Befehlssyntax `magento-cloud environment:branch <environment-name> <parent-environment-ID>` erstellen. Es kann einige zusätzliche Zeit in Anspruch nehmen, einen Umgebungs-Zweig zu erstellen und zu aktivieren.

1. Verwenden Sie die Umgebungs-ID, um jeden aktualisierten Code zu Ihrem lokalen Speicherort abzurufen. Dies ist nicht erforderlich, wenn der Umgebungszweig neu ist.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Optional_) Erstellen Sie einen [Schnappschuss](../storage/snapshots.md) der Umgebung als Sicherung.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## CLI aktualisieren

Die Befehlszeilenschnittstelle &quot;`magento-cloud`&quot;sucht nach verfügbaren Updates, wenn Sie sich anmelden. Sie können jedoch mithilfe des Befehls `self:update` nach Aktualisierungen suchen. Wenn ein Update verfügbar ist, befolgen Sie die Anweisungen zum Aktualisieren der CLI.

Wenn Ihre `magento-cloud` -CLI aktuell ist, sehen Sie die folgende Antwort:

```bash
magento-cloud update
```

```
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
