---
title: Aktivieren der Authentifizierung mit mehreren Faktoren für den SSH-Zugriff
description: Erfahren Sie, wie Sie Authentifizierungsanforderungen für den SSH-Zugriff auf Adobe Commerce in Cloud-Infrastrukturumgebungen verwalten.
feature: Cloud, Security
topic: Security
exl-id: 754b2c22-f197-49be-a699-fb3bedf053fc
source-git-commit: ec1e59c3aafae6452ad1590fdb9de37c68b94ed9
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Aktivieren der Authentifizierung mit mehreren Faktoren für den SSH-Zugriff

Für zusätzliche Sicherheit bietet Adobe Commerce on Cloud-Infrastruktur die Durchsetzung der Authentifizierung mit mehreren Faktoren (MFA), um Authentifizierungsanforderungen für den SSH-Zugriff auf Cloud-Umgebungen zu verwalten.

Wenn die MFA für ein Projekt aktiviert ist, benötigen alle Benutzerkonten mit SSH-Zugriff entweder einen TFA-Code (mit zwei Faktoren) oder ein API-Token und SSH-Zertifikat, um auf die Umgebung zuzugreifen.

>[!NOTE]
>
>MFA ist in Cloud-Projekten standardmäßig nicht aktiviert. Der Kontoinhaber für Adobe Commerce im Cloud-Infrastrukturprojekt muss [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um sie zu aktivieren. Wenn die MFA aktiviert ist, müssen alle Benutzer in ihrem Adobe Commerce über das Cloud-Infrastrukturkonto eine Zwei-Faktor-Authentifizierung (TFA) aktivieren, damit SSH-Zugriff auf die Projektumgebungen erhalten kann.

## Zertifikate für SSH-Zugriff

MFA ermöglicht Benutzern den Austausch eines OAUTH-Zugriffstokens mit einem kurzlebigen SSH-Zertifikat, das von der Adobe Cloud Certifier-API generiert wurde. Wenn der Benutzer über die Admin- oder Beitragsrolle, einen gültigen SSH-Schlüssel und einen gültigen TFA-Code oder API-Token verfügt, verwendet Adobe Commerce in der Cloud-Infrastruktur diese Anmeldeinformationen, um das temporäre SSH-Zertifikat zu generieren. Der Zertifikatablauf ist auf eine Stunde festgelegt, wird jedoch während der aktuellen Sitzung automatisch aktualisiert.

Nach der Anmeldung bei einem Projekt mit MFA müssen Benutzer die `magento-cloud` CLI zum Generieren des SSH-Zertifikats:

```bash
magento-cloud ssh-cert:load
```

Die `ssh-cert:load` generiert das SSH-Zertifikat und installiert es im SSH-Agenten des lokalen Benutzers.

### Zertifikat automatisch bei Anmeldung generieren

Sie können Ihre lokale Umgebung so konfigurieren, dass das SSH-Zertifikat automatisch generiert wird, wenn Sie sich beim `magento-cloud` CLI.

**So fügen Sie Ihrer `magento-cloud` CLI-Konfiguration**:

1. Erstellen Sie auf Ihrer lokalen Workstation eine Datei mit dem Namen `config.yaml` im `.magento-cloud` in Ihrem Basisverzeichnis, falls noch nicht vorhanden.

   ```bash
   touch ~/.magento-cloud/config.yaml
   ```

1. Fügen Sie die folgende Konfiguration zum `config.yaml` -Datei.

   ```yaml
   api:
      auto_load_ssh_cert: true
   ```

1. Verwenden Sie die `magento-cloud` CLI zur erneuten Authentifizierung:

   >Abmelden:

   ```bash
   magento-cloud logout
   ```

   >Anmelden:

   ```bash
   magento-cloud login
   ```

   >Befolgen Sie die Antwort:

   ```terminal
   Please open the following URL in a browser and log in:
   http://127.0.0.1:5000
   
   Help:
     Leave this command running during login.
     If you need to quit, use Ctrl+C.
   
     To log in using an API token, run: magento-cloud auth:api-token-login
   
   Login information received. Verifying...
   You are logged in.
   
   Generating SSH certificate...
   A new SSH certificate has been generated.
   It will be automatically refreshed when necessary.
   The certificate is included in your SSH configuration: /Users/<user-name>/.ssh/config
   ```

## Verbindung zu einer Umgebung mit SSH mit TFA herstellen

Wenn die MFA für ein Projekt aktiviert ist, muss TFA für Ihr Konto aktiviert sein, damit Sie über eine SSH eine Verbindung zu einer Remote-Umgebung herstellen können. Siehe [Aktivieren von TFA](user-access.md#enable-tfa-for-cloud-accounts).

>[!BEGINSHADEBOX]

**Voraussetzungen:**

Für Projekte, die mit der MFA-Durchsetzung aktiviert sind, erfordert der SSH-Zugriff die folgenden Berechtigungen und Kontoeinstellungen:

- [Admin- oder Beitragszugriff auf die Umgebung](user-access.md)
- [SSH-Zugriffsschlüssel, der für das Konto konfiguriert ist](../development/secure-connections.md#add-an-ssh-public-key-to-your-account)
- [TFA-Aktivierung auf Konto](user-access.md#enable-tfa-for-cloud-accounts)

>[!ENDSHADEBOX]

**So verbinden Sie sich mit SSH mit den Anmeldedaten für das TFA-Benutzerkonto**:

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com).

1. Verwenden Sie auf Ihrer lokalen Workstation die `magento-cloud` CLI zum Generieren des SSH-Zertifikats.

   ```bash
   magento-cloud ssh-cert:load
   ```

   > Beispielantwort:

   ```terminal
   Generating SSH certificate...
     Expires at: 2020-07-13T15:28:13-04:00
     Multi-factor authentication: verified
     Mode: interactive
   The certificate will be automatically refreshed when necessary.
   Checking SSH configuration file: /Users/<user-name>/.ssh/config
   Do you want to update the file automatically? [Y/n] Y
   Configuration file updated successfully: /Users/<user-name>/.ssh/config
   ```

1. Verwenden Sie eine SSH, um eine Verbindung zur Remote-Umgebung herzustellen.

   ```bash
   ssh abcdef7uyxabce-master-7rqtwti--mymagento@ssh.us-5.magento.cloud
   ```

   ```terminal
    __  __                   _          ___ _             _
   |  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
   | |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
   |_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
               |___/
   
    Welcome to Magento Cloud.
   
    This is environment master-7rqtwti
    of project abcdef7uyxabce.
   
   web@mymagento.0:~$
   ```

## Verwalten des Quellcodes mit SSH mit TFA

Beim Verwalten des Quellcodes für Adobe Commerce in Cloud-Infrastrukturprojekten verwenden Sie SSH, um sich beim Git-Repository für das Projekt zu authentifizieren. Wenn für Ihr Projekt die MFA-Durchsetzung aktiviert ist, müssen Sie ein SSH-Zertifikat generieren, bevor Sie Befehlszeilenvorgänge mit dem Git-Repository durchführen können.

**So verbinden Sie sich mit SSH mit den Anmeldedaten für das TFA-Benutzerkonto**:

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com) und mit TFA authentifizieren.

   >[!NOTE]
   >
   >Wenn TFA in Ihrem Konto nicht aktiviert ist, müssen Sie es aktivieren. Siehe [Aktivieren von TFA für Cloud-Konten](user-access.md#enable-tfa-for-cloud-accounts).

1. Verwenden Sie auf Ihrer lokalen Workstation die `magento-cloud` CLI zum Generieren des SSH-Zertifikats.

   ```bash
   magento-cloud ssh-cert:load
   ```

   > Beispielantwort:

   ```terminal
   Generating SSH certificate...
     Expires at: 2020-07-13T15:28:13-04:00
     Multi-factor authentication: verified
     Mode: interactive
   The certificate will be automatically refreshed when necessary.
   Checking SSH configuration file: /Users/<user-name>/.ssh/config
   Do you want to update the file automatically? [Y/n] Y
   Configuration file updated successfully: /Users/<user-name>/.ssh/config
   ```

1. Klonen Sie das Git-Repository für Ihre Projektumgebung:

   ```bash
   git clone --branch integration abcdef7uyxabce@git.us-3.magento.cloud:abcdef7uyxabce.git myproject
   ```

   > Beispielantwort:

   ```terminal
   Cloning into 'myproject'...
   Connection to git.us-3.magento.cloud port 22 [tcp/ssh] succeeded!
   remote: counting objects: 22, done.
   Receiving objects: 100% (22/22), 82.42 KiB | 16.48 MiB/s, done.
   ```

## Verbindung zu einer Umgebung mit SSH mit einem API-Token herstellen

Wenn MFA für ein Projekt aktiviert ist, erfordern automatisierte Prozesse, für die SSH-Zugriff auf eine Cloud-Umgebung erforderlich ist, ein API-Token. Sie können das Token aus einem Adobe Commerce-Konto für Cloud-Infrastruktur mit Admin- oder Contributor-Zugriff auf das Projekt generieren.

Für die Authentifizierung mit einem API-Token muss weiterhin ein SSH-Zertifikat generiert werden. Automatisierte Prozesse müssen auch die Erstellung eines SSH-Zertifikats automatisieren.

>[!BEGINSHADEBOX]

**Voraussetzungen:**

- [Admin- oder Contributor-Zugriff auf Adobe Commerce in der Cloud-Infrastruktur-Umgebung](user-access.md)
- [Gültiges API-Token für Konto verfügbar](user-access.md#create-an-api-token)

>[!ENDSHADEBOX]

**So stellen Sie eine Verbindung mit SSH mit einer API-Token-Berechtigung her**:

1. Melden Sie sich mit der API-Schlüsselauthentifizierung beim Cloud-Projekt an.

   ```bash
   magento-cloud auth:api-token
   ```

1. Geben Sie an der Eingabeaufforderung den Wert für ein gültiges API-Token ein.

   ```terminal
   Please enter an API token:
   >
   
   The API token is valid.
   You are logged in.
   ```

### Beispiel: automatisiertes SSH-Skript

Es gibt zwei Optionen zum Speichern des API-Tokens.

>[!NOTE]
>
>Wenn ein API-Token gespeichert wird, wird die `magento-cloud` Die CLI authentifiziert sich automatisch und es ist nicht erforderlich, die `magento-cloud login` Befehl.

**Option 1**: Erstellen Sie eine Umgebungsvariable zum Speichern des API-Tokens.

Schreiben Sie das Token in Ihr bash_profile

```bash
echo "export MAGENTO_CLOUD_CLI_TOKEN=<your api token>" >> ~/.bash_profile
```

**Option 2**: Fügen Sie das Token zum `config.yaml` file

1. Erstellen Sie auf Ihrer lokalen Workstation eine Datei mit dem Namen `config.yaml` im `.magento-cloud` in Ihrem Basisverzeichnis, falls noch nicht vorhanden.

   ```bash
   touch ~/.magento-cloud/config.yaml
   ```

1. Fügen Sie die folgende Konfiguration zum `config.yaml` -Datei.

   ```yaml
   api:
      token: <your api token>
   ```

>Beispiel-Bash-Skript

```shell
#!/bin/bash
magento-cloud ssh-cert:load
ssh abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud "tail -n 10 ~/var/log/cloud.log"
```

## Fehlerbehebung

Verwenden Sie die folgenden Informationen, um SSH-Verbindungsanforderungsfehler aufgrund von Authentifizierungsfehlern wie `access requires MFA` oder `permission denied`.

### Ihre Anfrage stellt kein gültiges Zertifikat bereit

Wenn Ihre Anforderung kein gültiges Zertifikat enthält, wird eine Meldung ähnlich der folgenden angezeigt:

```terminal
to Hello user-test (UUID: abaacca12-5cd1-4b123-9096-411add578998), you successfully
authenticated, but could not connect to service abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud:>
(reason: access requires MFA)
```

Versuchen Sie die folgenden Schritte zur Fehlerbehebung, um das Verbindungsproblem zu beheben:

- Überprüfen der TFA-Kontokonfiguration
- Erneutes Authentifizieren und dann das Zertifikat erneut laden

**Überprüfen der TFA-Konfiguration und -Authentifizierung**:

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com).

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Im _Mein Profil_ klicken Sie auf die **[!UICONTROL Security]** Registerkarte.

   Wenn TFA aktiviert ist, bietet der Abschnitt Sicherheit Optionen zum Verwalten der TFA-Konfiguration.

1. Wenn TFA nicht eingerichtet ist, klicken Sie auf **[!UICONTROL Set up application]** und folgen Sie den Anweisungen, um sie zu aktivieren. Siehe [Aktivieren von TFA](user-access.md#enable-tfa-for-cloud-accounts).

1. Wenn TFA konfiguriert ist, versuchen Sie erneut, sich zu authentifizieren.

**So authentifizieren Sie das SSH-Zertifikat und laden es neu**:

1. Verwenden Sie die `magento-cloud` CLI zur erneuten Authentifizierung:

   ```bash
   magento-cloud logout
   ```

   ```bash
   magento-cloud login
   ```

1. Laden Sie das SSH-Zertifikat neu:

   ```bash
   magento-cloud ssh-cert:load
   ```

### Erlaubnis verweigert

Wenn der SSH-Schlüssel fehlt oder ungültig ist, gibt die SSH-Verbindungsanforderung eine `Permission denied (publickey)` Fehler.

```terminal
Hello user-test (UUID: abaacca12-5cd1-4b123-9096-411add578998), you successfully authenticated, but could not connect to service oh2wi6klp5ytk-mc-35985-integration-nnulm4a--mymagento (reason: service doesn't exist or you do not have access to it)
oh2wi6klp5ytk-mc-35985-integration-nnulm4a--mymagento@ssh.eu-3.magento.cloud: Permission denied (publickey).
```

Um das Problem zu beheben, fügen Sie den SSH-Schlüssel zu Ihrer aktuellen Sitzung hinzu oder aktualisieren Sie die SSH-Konfigurationsdatei, um Ihre SSH-Schlüssel automatisch zu laden. Siehe [Öffentlichen SSH-Schlüssel hinzufügen](../development/secure-connections.md#add-an-ssh-public-key-to-your-account).

### Zugriff auf Projekte ohne MFA nicht möglich

Wenn Sie sich bei einem Projekt authentifizieren, für das die Multifaktorauthentifizierung (MFA) aktiviert ist, erhalten Sie beim Herstellen einer Verbindung zu anderen Projekten, für die keine MFA erforderlich ist, möglicherweise den folgenden Fehler:

```bash
ssh abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud
```

Beispielantwort:

```terminal
abcdef7uyxabce-master-7rqtabc--mymagento@ssh.us-3.magento.cloud: Permission denied (publickey).
```

Während der Erstellung des SSH-Zertifikats muss die `magento-cloud` CLI fügt einen zusätzlichen SSH-Schlüssel zu Ihrer lokalen Umgebung hinzu. Dieser Schlüssel wird standardmäßig verwendet, wenn Ihre lokale SSH-Konfiguration den SSH-Schlüssel für den Projektzugriff nicht enthält.

**Hinzufügen des SSH-Schlüssels zur lokalen Konfiguration**:

1. Erstellen Sie die `config` Datei, wenn sie nicht vorhanden ist.

   ```bash
   touch ~/.ssh/config
   ```

1. Hinzufügen einer `IdentityFile` Konfiguration.

   ```yaml
   Host *
     IdentityFile ~/.ssh/id_rsa
   ```

>[!NOTE]
>
>Sie können mehrere SSH-Schlüssel angeben, indem Sie mehrere `IdentityFile` -Einträge in Ihrer Konfiguration.
