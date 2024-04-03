---
title: Sichere Verbindungen
description: Erfahren Sie, wie Sie SSH-Schlüssel auf Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anwenden und sich bei Remote-Umgebungen anmelden.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: b5780e8e-e3da-4b10-8ca3-2778085acd4a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Sichere Verbindungen zu Remote-Umgebungen

Secure Shell (SSH) ist ein gängiges Protokoll, das zur sicheren Anmeldung bei Remote-Servern und -Systemen verwendet wird. Sie können SSH verwenden, um auf Ihre Remote-Umgebungen zuzugreifen, um die Adobe Commerce-Anwendung zu verwalten und auf Remote-Umgebungsprotokolle zuzugreifen. Adobe unterstützt nur sichere FTP-Verbindungen (sFTP) mit Ihrem öffentlichen SSH-Schlüssel. FTP-Verbindungen werden nicht unterstützt.

## Generieren eines SSH-Schlüsselpaars

Erstellen Sie auf jedem Computer und Arbeitsbereich ein SSH-Schlüsselpaar, das Zugriff auf Ihren Projektquell-Code und Ihre Umgebungen erfordert. Mit dem SSH-Schlüssel können Sie eine Verbindung zu GitHub herstellen, um Quellcode zu verwalten und eine Verbindung zu Cloud-Servern herzustellen, ohne ständig Ihren Benutzernamen und Ihr Passwort angeben zu müssen. Siehe [Verbindung zu GitHub mit SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) für weitere Anweisungen zum Erstellen eines SSH-Schlüsselpaars.

- Die _öffentlicher Schlüssel_ ist sicher, um den Zugriff auf eine Site, SSH und sFTP bereitzustellen.
- Die _privater Schlüssel_ bleibt auf der Workstation privat.

>[!CAUTION]
>
>**Geben Sie nie Ihren privaten Schlüssel frei.** Fügen Sie es nicht zu einem Ticket hinzu, kopieren Sie es in einen Chat oder fügen Sie es an E-Mails an.

## Hinzufügen eines öffentlichen SSH-Schlüssels zu Ihrem Konto

Nachdem Sie Ihren öffentlichen SSH-Schlüssel zu Ihrem Adobe Commerce-Konto für die Cloud-Infrastruktur hinzugefügt haben, stellen Sie alle aktiven Umgebungen auf Ihrem Konto erneut bereit, um den Schlüssel zu installieren.

Sie können Ihrem Konto SSH-Schlüssel mit einer der folgenden Methoden hinzufügen: Cloud CLI oder [!DNL Cloud Console].

>[!BEGINTABS]

>[!TAB CLI]

### SSH-Schlüssel mithilfe der Cloud CLI hinzufügen

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Melden Sie sich bei Ihrem Projekt an:

   ```bash
   magento-cloud login
   ```

1. Fügen Sie den öffentlichen Schlüssel hinzu.

   ```bash
   magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
   ```

>[!TIP]
>
>Sie können SSH-Schlüssel mithilfe der Cloud CLI-Befehle auflisten und löschen `ssh-key:list` und `ssh-key:delete`.

>[!TAB Konsole]

### Fügen Sie Ihren SSH-Schlüssel mithilfe der [!DNL Cloud Console]

**So fügen Sie einem neuen Projekt einen SSH-Schlüssel hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klicks **[!UICONTROL No SSH key]**. Dieses Symbol befindet sich rechts neben dem Befehlsfeld und ist sichtbar, wenn das Projekt keinen SSH-Schlüssel enthält.

1. Kopieren Sie den Inhalt Ihres öffentlichen SSH-Schlüssels und fügen Sie ihn in die **Öffentlicher Schlüssel** -Feld.

1. Befolgen Sie die restlichen Anweisungen.

**So fügen Sie Ihrem Cloud-Profil einen SSH-Schlüssel hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klicken Sie oben rechts im Kontomenü auf **Mein Profil**.

1. Im _SSH-Schlüssel_ Ansicht, klicken Sie **Öffentlichen Schlüssel hinzufügen**.

1. Im _SSH-Schlüssel hinzufügen_ Formular, geben Sie Ihrem Schlüssel einen **Titel** und fügen Sie den öffentlichen SSH-Schlüssel in die **Schlüssel** -Feld.

1. Klicks **Speichern**.

>[!ENDTABS]

## Herstellen einer Verbindung zu einer Remote-Umgebung

Sie können eine Verbindung zu einer Remote-Umgebung über die `magento-cloud` CLI oder SSH-Befehl. Die `magento-cloud` CLI-Befehle können nur in Integrationsumgebungen von Starter und Pro verwendet werden.

### Verwenden der Cloud-CLI

**So melden Sie sich bei einer Remote-Integrationsumgebung an**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Geben Sie die Umgebungen in diesem Projekt an.

   ```bash
   magento-cloud environment:list -p <project-ID>
   ```

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh -p <project-ID> -e <environment-ID>
   ```

### SSH-Befehl verwenden

Die [!DNL Cloud Console] enthält eine Liste der Web- und SSH-Zugriffsbefehle für jede Umgebung.

**So kopieren Sie den SSH-Befehl**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie eine Umgebung aus.

1. Klicks **[!UICONTROL SSH]**.

1. Im _SSH_ klicken Sie auf die Schaltfläche &quot;Kopieren&quot;, um den vollständigen SSH-Befehl in die Zwischenablage zu kopieren.

1. Öffnen Sie ein Terminal und fügen Sie den SSH-Befehl ein, um eine Verbindung zu erstellen.

   ```bash
   ssh abcdefg123abc-branch-a12b34c--mymagento@ssh.us-2.magento.cloud
   ```

>[!TIP]
>
>In Pro-Staging- und Produktionsumgebungen kann der SSH-Befehl wie folgt aussehen:
>
>```bash
>ssh <node>.ent-<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
>```

## sFTP

Adobe Commerce in der Cloud-Infrastruktur unterstützt den Zugriff auf Ihre Umgebungen über sFTP (sicheres FTP) mit SSH-Authentifizierung. Verwenden Sie einen Client, der die SSH-Schlüsselauthentifizierung für sFTP unterstützt, und verwenden Sie Ihren öffentlichen SSH-Schlüssel. Ihr öffentlicher SSH-Schlüssel muss zur Zielumgebung hinzugefügt werden. In Starter-Umgebungen und Pro-Integrationsumgebungen können Sie [Fügen Sie ihn über die [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface).

Schreibgeschützte sFTP-Verbindungen sind _not_ unterstützt. Der sFTP-Zugriff wird mit _schreiben_ -Berechtigung standardmäßig aus.

Verwenden Sie beim Konfigurieren von sFTP die Informationen aus Ihrem SSH-Zugriffsumgebungsbefehl: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Benutzername**: Alle Inhalte vor dem `@` in Ihrem SSH-Zugriffsziel.
- **Passwort**: Sie benötigen kein Kennwort für sFTP. Der FTP-Zugriff verwendet die SSH-Schlüsselauthentifizierung.
- **Host**: Alle Inhalte nach dem `@` in Ihrem SSH-Zugriff.
- **Port**: 22, der standardmäßige SSH-Port.
- **SSH** Privater Schlüssel: Geben Sie bei Bedarf den Speicherort Ihres privaten Schlüssels für den sFTP-Client an. Standardmäßig werden private Schlüssel im `~/.ssh` Verzeichnis.

Je nach Client sind möglicherweise zusätzliche Optionen erforderlich, um die SSH-Authentifizierung für sFTP abzuschließen. Überprüfen Sie die Dokumentation für Ihren ausgewählten Client.

Für **Starterumgebungen und Pro-Integration-Umgebungen**, können Sie auch [Hinzufügen von `mount`](../application/properties.md#mounts) für den Zugriff auf einen bestimmten Ordner. Sie würden die -Bereitstellung zu Ihrem `.magento.app.yaml` -Datei. Eine Liste der beschreibbaren Verzeichnisse finden Sie unter [Projektstruktur](../project/file-structure.md). Dieser Bereitstellungspunkt funktioniert nur in diesen Umgebungen.

Für **Pro Staging- und Produktionsumgebungen** Wenn Sie keinen SSH-Zugriff auf die Umgebung haben, müssen Sie [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) um den sFTP-Zugriff und einen Bereitstellungspunkt für den Zugriff auf den jeweiligen Ordner anzufordern, z. B. `pub/media`.

>[!NOTE]
>Für Pro Staging und Produktion, wenn die sFTP-Verbindung für eine _generisch_ Benutzer, der **not** müssen [zum Cloud-Projekt hinzugefügt](../project/user-access.md)müssen Sie [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) mit **öffentlich** Schlüssel angehängt. **Geben Sie niemals Ihren privaten SSH-Schlüssel an.**

## SSH-Tunnel

Sie können SSH-Tunnel verwenden, um von Ihrer lokalen Entwicklungsumgebung aus eine Verbindung zu einem Dienst herzustellen, als wäre der Dienst lokal. Konfigurieren Sie vor dem Tunneln Ihre [SSH](#add-an-ssh-public-key-to-your-account).

Verwenden Sie eine Terminal-Anwendung, um sich anzumelden und Befehle auszugeben.

```bash
magento-cloud login
```

Überprüfen Sie, ob Tunnel mit geöffnet sind.

```bash
magento-cloud tunnel:list
```

Um einen Tunnel zu bauen, müssen Sie die [Anwendungsname](../application/properties.md#name). Sie können den Anwendungsnamen mithilfe der CLI überprüfen:

```bash
magento-cloud apps
```

### Einrichten des SSH-Tunnels

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Um beispielsweise einen Tunnel zum `sprint5` Verzweigung in einem Projekt mit einer App mit dem Namen `mymagento`, eingeben

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Beispielantwort:

```terminal
SSH tunnel opened on port 30004 to relationship: redis
SSH tunnel opened on port 30005 to relationship: database
Logs are written to: /home/magento_user/.magento/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close
```

**So zeigen Sie Informationen zu Ihrem Tunnel an**:

```bash
magento-cloud tunnel:info -e <environment-ID>
```

### Verbindung zu Diensten

Nach der Einrichtung eines SSH-Tunnels können Sie eine Verbindung zu Diensten herstellen, als ob sie lokal ausgeführt würden. Verwenden Sie beispielsweise den folgenden Befehl, um eine Verbindung zur Datenbank herzustellen:

```bash
mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
```
