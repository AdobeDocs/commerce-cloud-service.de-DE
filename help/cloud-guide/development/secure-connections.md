---
title: Sichere Verbindungen
description: Erfahren Sie, wie Sie SSH-Schlüssel auf Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anwenden und sich bei Remote-Umgebungen anmelden.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: b5780e8e-e3da-4b10-8ca3-2778085acd4a
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Sichere Verbindungen zu Remote-Umgebungen

Secure Shell (SSH) ist ein gängiges Protokoll, das zur sicheren Anmeldung bei Remote-Servern und -Systemen verwendet wird. Sie können SSH verwenden, um auf Ihre Remote-Umgebungen zuzugreifen, um die Adobe Commerce-Anwendung zu verwalten und auf Remote-Umgebungsprotokolle zuzugreifen. Adobe unterstützt nur sichere FTP-Verbindungen (sFTP) mit Ihrem öffentlichen SSH-Schlüssel. FTP-Verbindungen werden nicht unterstützt.

## Generieren eines SSH-Schlüsselpaars

Erstellen Sie auf jedem Computer und Arbeitsbereich ein SSH-Schlüsselpaar, das Zugriff auf Ihren Projektquell-Code und Ihre Umgebungen erfordert. Mit dem SSH-Schlüssel können Sie eine Verbindung zu GitHub herstellen, um Quellcode zu verwalten und eine Verbindung zu Cloud-Servern herzustellen, ohne ständig Ihren Benutzernamen und Ihr Passwort angeben zu müssen. Weitere Informationen zum Erstellen eines SSH-Schlüsselpaars finden Sie unter [Herstellen einer Verbindung zu GitHub mit SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) .

- Der _öffentliche Schlüssel_ ist sicher, um auf eine Site, SSH und sFTP zuzugreifen.
- Der _private Schlüssel_ bleibt auf der Workstation privat.

>[!CAUTION]
>
>**Geben Sie Ihren privaten Schlüssel nie frei.** Fügen Sie es nicht zu einem Ticket hinzu, kopieren Sie es in einen Chat oder fügen Sie es an E-Mails an.

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
>Sie können SSH-Schlüssel mit den Cloud CLI-Befehlen `ssh-key:list` und `ssh-key:delete` auflisten und löschen.

>[!TAB Konsole]

### Fügen Sie Ihren SSH-Schlüssel mit dem [!DNL Cloud Console] hinzu.

**So fügen Sie einem neuen Projekt einen SSH-Schlüssel hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Klicken Sie auf **[!UICONTROL No SSH key]**. Dieses Symbol befindet sich rechts neben dem Befehlsfeld und ist sichtbar, wenn das Projekt keinen SSH-Schlüssel enthält.

1. Kopieren Sie den Inhalt Ihres öffentlichen SSH-Schlüssels und fügen Sie ihn in das Feld **Öffentlicher Schlüssel** ein.

1. Befolgen Sie die restlichen Anweisungen.

**So fügen Sie Ihrem Cloud-Profil einen SSH-Schlüssel hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Klicken Sie oben rechts im Kontomenü auf **Mein Profil**.

1. Klicken Sie in der Ansicht _SSH-Schlüssel_ auf **öffentlichen Schlüssel hinzufügen**.

1. Geben Sie im Formular _SSH-Schlüssel hinzufügen_ Ihrem Schlüssel einen **Titel** und fügen Sie den öffentlichen SSH-Schlüssel in das Feld **Schlüssel** ein.

1. Klicken Sie auf **Speichern**.

>[!ENDTABS]

## Herstellen einer Verbindung zu einer Remote-Umgebung

Sie können eine Verbindung zu einer Remote-Umgebung über den Befehl `magento-cloud` CLI oder SSH herstellen. Die `magento-cloud` CLI-Befehle können nur in Starter- und Pro-Integrationsumgebungen verwendet werden.

### Verwenden der Cloud-CLI

**Anmelden bei einer Remote-Integrationsumgebung**:

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

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie eine Umgebung aus.

1. Klicken Sie auf **[!UICONTROL SSH]**.

1. Klicken Sie auf der Registerkarte _SSH_ auf die Schaltfläche &quot;Kopieren&quot;, um den vollständigen SSH-Befehl in die Zwischenablage zu kopieren.

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

Adobe Commerce in der Cloud-Infrastruktur unterstützt den Zugriff auf Ihre Umgebungen über sFTP (sicheres FTP) mit SSH-Authentifizierung. Verwenden Sie einen Client, der die SSH-Schlüsselauthentifizierung für sFTP unterstützt, und verwenden Sie Ihren öffentlichen SSH-Schlüssel. Ihr öffentlicher SSH-Schlüssel muss zur Zielumgebung hinzugefügt werden. Bei Starterumgebungen und Pro-Integrationsumgebungen können Sie [über den Abschnitt  [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface) hinzufügen.

Schreibgeschützte sFTP-Verbindungen werden _nicht_ unterstützt. Der sFTP-Zugriff wird standardmäßig mit der Berechtigung _write_ versehen.

Verwenden Sie beim Konfigurieren von sFTP die Informationen aus Ihrem SSH-Zugriffsumgebungsbefehl: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Benutzername**: Alle Inhalte vor dem `@` in Ihrem SSH-Zugriffsziel.
- **Kennwort**: Sie benötigen kein Kennwort für sFTP. Der FTP-Zugriff verwendet die SSH-Schlüsselauthentifizierung.
- **Host**: Alle Inhalte nach dem `@` in Ihrem SSH-Zugriff.
- **Port**: 22, der standardmäßige SSH-Port.
- **SSH** Privater Schlüssel: Geben Sie bei Bedarf den Speicherort Ihres privaten Schlüssels für den sFTP-Client an. Standardmäßig werden private Schlüssel im Verzeichnis `~/.ssh` gespeichert.

Je nach Client sind möglicherweise zusätzliche Optionen erforderlich, um die SSH-Authentifizierung für sFTP abzuschließen. Überprüfen Sie die Dokumentation für Ihren ausgewählten Client.

Bei **Starterumgebungen und Pro-Integrationsumgebungen** sollten Sie auch erwägen, [eine `mount`](../application/properties.md#mounts) für den Zugriff auf einen bestimmten Ordner hinzuzufügen. Sie würden das -Reittier zu Ihrer `.magento.app.yaml`-Datei hinzufügen. Eine Liste der beschreibbaren Ordner finden Sie unter [Projektstruktur](../project/file-structure.md). Dieser Bereitstellungspunkt funktioniert nur in diesen Umgebungen.

Wenn Sie für **Pro Staging- und Produktionsumgebungen** keinen SSH-Zugriff auf die Umgebung haben, müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um den SFTP-Zugriff und einen Bereitstellungspunkt für den Zugriff auf den jeweiligen Ordner anzufordern, z. B. `pub/media`.

>[!NOTE]
>Wenn die sFTP-Verbindung für Pro-Staging- und -Produktions-Benutzer _generic_ ist und **nicht** [ zum Cloud-Projekt hinzugefügt werden muss, müssen Sie [ ein Adobe Commerce-Supportticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), an das der Schlüssel **public** angehängt ist. ](../project/user-access.md) **Geben Sie Ihren privaten SSH-Schlüssel nie an.**

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

Um einen Tunnel zu erstellen, müssen Sie den [Anwendungsnamen](../application/properties.md#name) kennen. Sie können den Anwendungsnamen mithilfe der CLI überprüfen:

```bash
magento-cloud apps
```

### Einrichten des SSH-Tunnels

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Um beispielsweise einen Tunnel zum Zweig `sprint5` in einem Projekt mit einer App namens `mymagento` zu öffnen, geben Sie

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Beispielantwort:

```
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
