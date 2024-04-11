---
title: Verwalten des Benutzerzugriffs
description: Erfahren Sie, wie Sie den Benutzerzugriff auf Adobe Commerce in Cloud-Infrastrukturprojekten und -Umgebungen verwalten.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: b85a163ff62f8a63430dff7c96b5cf391cf38d79
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Verwalten des Benutzerzugriffs

Adobe Commerce-Projekte zur Cloud-Infrastruktur nutzen rollenbasierten Zugriff. Auf Projektebene stehen zwei Rollen zur Verfügung:

- **Projektadministrator**—Schreiben Sie Zugriff auf alle Projektumgebungen und können Benutzer verwalten, Push-Code bereitstellen und Projekteinstellungen aktualisieren.
- **Projekt-Viewer**—Schreibgeschützter Zugriff auf alle Projektumgebungen.

Projekt-Viewer können in keiner Umgebung Aufgaben ausführen. Sie können jedoch Projekt-Viewern Schreibzugriff auf einen bestimmten Umgebungstyp gewähren.

Der Zugriff auf Umgebungsebene basiert auf dem Umgebungstyp: Produktion, Staging und Entwicklung. Gewähren eines Benutzers _Viewer_ Berechtigung zu _development_ Umgebungen bedeutet, dass sie **all** Entwicklungsumgebungen im Projekt. In der folgenden Tabelle werden die den einzelnen Berechtigungsebenen zugewiesenen Fähigkeiten erläutert:

| Berechtigungsebene | Zugriff | SSH-Zugriff |
| ------------------ | ----------- | :----------: |
| **Admin** | Ausführen von Administratoraufgaben, wie z. B. Einstellungen ändern, Push-Code, Ausführen von Aufgaben und Verzweigungsverwaltung, einschließlich der Zusammenführung mit der übergeordneten Umgebung | Ja |
| **Mitarbeiter** | Push-Code und Verzweigung der Umgebung; kann Einstellungen nicht ändern oder Aktionen ausführen | Ja |
| **Viewer** | Schreibgeschützter Zugriff auf den Umgebungstyp | Nein |
| **Kein Zugriff** | Kein Zugriff auf den Umgebungstyp | Nein |

{style="table-layout:auto"}

Sie können Benutzer hinzufügen und Rollen zuweisen mithilfe der `magento-cloud` CLI oder [!DNL Cloud Console].

>[!BEGINSHADEBOX]

**Voraussetzungen:**

- Ein registrierter Benutzer bei einem Adobe ID. Ein Benutzer muss [sich für ein Adobe-Konto registrieren](https://account.adobe.com) und dann [Initialisieren ihres Cloud-Kontos](https://console.adobecommerce.com) , bevor Sie sie zu einem Cloud-Projekt hinzufügen können.
- Ein Benutzer hat **Admin** -Rolle kann Benutzer mit `magento-cloud` CLI. Nur Benutzer, denen die **Kontoinhaber** -Rolle können Benutzer verwalten.

>[!ENDSHADEBOX]

## Benutzer mit der CLI verwalten

Verwenden Sie die `magento-cloud` CLI zur Verwaltung von Benutzern und Integration in automatisierte Systeme:

- `magento-cloud user:add`-einen Benutzer zum Projekt hinzufügen
- `magento-cloud user:delete`-Löschen eines Benutzers
- `magento-cloud user:list [users]`-Liste der Projektbenutzer
- `magento-cloud user:role`-Ansicht oder Änderung der Benutzerrolle
- `magento-cloud user:update`-Aktualisieren der Benutzerrolle in einem Projekt

Die folgenden Beispiele verwenden die `magento-cloud` CLI zum Hinzufügen eines Benutzers, Konfigurieren von Rollen, Ändern von Projektzuweisungen und Zuweisen von Benutzerrollen.

**So fügen Sie einen Benutzer hinzu und weisen Rollen zu**:

1. Verwenden Sie die `magento-cloud` CLI zum Hinzufügen des Benutzers.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >Der Benutzer muss über eine Adobe ID verfügen; siehe [Voraussetzungen](#add-users-and-manage-access).

1. Befolgen Sie die Anweisungen: Geben Sie die E-Mail-Adresse des Benutzers an, legen Sie die Rollen &quot;Projekt&quot;und &quot;Umgebung&quot;fest und fügen Sie den Benutzer hinzu.

   > Beispielaufforderungen

   ```terminal
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   Nachdem Sie den Benutzer hinzugefügt haben, sendet Adobe eine E-Mail mit Anweisungen zum Zugriff auf Adobe Commerce im Cloud-Infrastrukturprojekt an die angegebene Adresse.

### Anzeigen der Projektrolle eines Benutzers

```bash
magento-cloud user:get alice@example.com
```

>Beispielantwort:

```terminal
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Benutzer zu mehreren Umgebungen hinzufügen

So fügen Sie einen Benutzer als `viewer` auf `Production` und als `contributor` auf `Integration` Umgebung:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Berechtigungen der Benutzerumgebung aktualisieren

So aktualisieren Sie die Berechtigungen der Benutzerumgebung auf `admin` auf `Production` Umgebung:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Verwalten Sie Benutzer über die [!DNL Cloud Console]

Sie können die [[!DNL Cloud Console]](../../get-started/cloud-console.md) um Berechtigungen hinzuzufügen und die _Bearbeiten_ , um die Berechtigungen für einen vorhandenen Benutzer zu ändern.

>[!IMPORTANT]
>
>Der Benutzer muss über eine Adobe ID verfügen; siehe [Voraussetzungen](#add-users-and-manage-access).

### Einen Benutzer zum Projekt hinzufügen

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com/).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Klicken Sie im Projekt-Dashboard auf das Konfigurationssymbol oben rechts.

1. under _Projekteinstellungen_ klicken **[!UICONTROL Access]**.

1. Im _Zugriff_ Ansicht, klicken Sie **[!UICONTROL Add]**.

1. Führen Sie die _[!UICONTROL Add User]_form:

   - Geben Sie die E-Mail-Adresse des Benutzers ein.

   - **[!UICONTROL Project admin]**—gewähren Sie Administratorrechte für alle Einstellungen und Umgebungstypen.

   - **[!UICONTROL Environment types and permissions]**—Gewähren von Zugriff und spezifischen Berechtigungen für bestimmte Umgebungstypen. _Kein Zugriff_, _Admin_ (Einstellungen ändern, Aktion ausführen, Zusammenführungscode), _Mitarbeiter_ (Push-Code) oder _Viewer_ (nur Ansicht).

   >[!TIP]
   >
   >Nur ein **Projektadministrator** Benutzer können in jeder Umgebung verwaltet werden. So gewähren Sie Benutzern Zugriff auf die **Zugriff** Registerkarte, eine andere **Projektadministrator** oder **Kontoinhaber** muss diesem Benutzer die **Projektadministrator** Rolle.

1. Klicks **[!UICONTROL Add User]**.

   >[!IMPORTANT]
   >
   >Beim Hinzufügen eines Benutzers wird eine Bereitstellung nicht automatisch Trigger.

1. Stellen Sie nach dem Hinzufügen von Benutzern alle Umgebungen erneut bereit, um die Änderungen anzuwenden. Beim Hinzufügen eines Benutzers wird eine Bereitstellung nicht automatisch Trigger. Die Neubereitstellung ist ein wichtiger Schritt, um sicherzustellen, dass der Benutzer über SSH auf eine Umgebung zugreifen oder Administratoraufgaben ausführen kann.

Nachdem Sie den Benutzer hinzugefügt haben, sendet Adobe eine E-Mail mit Anweisungen zum Zugriff auf Adobe Commerce im Cloud-Infrastrukturprojekt an die angegebene Adresse.

## Authentifizierungspflichten für Benutzer

Für zusätzliche Sicherheit bietet Adobe eine Durchsetzung der Multi-Factor-Authentifizierung (MFA) auf Projektebene, sodass eine Zweifaktorauthentifizierung (TFA) für den SSH-Zugriff auf Adobe Commerce über den Quellcode und die Umgebungen von Cloud-Infrastruktur-Projekten erforderlich ist. Siehe [MFA für SSH aktivieren](multi-factor-authentication.md).

Wenn die MFA-Durchsetzung in einem Adobe Commerce-Projekt zur Cloud-Infrastruktur aktiviert ist, müssen alle Benutzer mit SSH-Zugriff auf eine Umgebung in diesem Projekt TFA in ihrem Adobe Commerce-Konto für die Cloud-Infrastruktur aktivieren. Für automatisierte Prozesse können Sie einen Maschinenbenutzer und ein API-Token erstellen, die über die Befehlszeile authentifiziert werden.

Nachdem Sie einen Benutzer zu einem Cloud-Projekt hinzugefügt haben, bitten Sie den Benutzer, seine Kontosicherheitseinstellungen zu überprüfen und die folgenden Sicherheitskonfigurationen nach Bedarf hinzuzufügen:

- **Aktivieren von TFA**—Erfüllen Sie die Sicherheits- und Compliance-Standards durch Konfiguration der Authentifizierung mit zwei Faktoren. Mit [MFH-Durchsetzung](multi-factor-authentication.md) TFA für Konten benötigen, die SSH verwenden, um auf die Projekte zuzugreifen.

- **SSH-Schlüssel aktivieren**—Benutzer, die Zugriff auf Adobe Commerce in Quell-Code-Repositorys für Cloud-Infrastruktur benötigen, müssen SSH-Schlüssel in ihrem Konto aktivieren. Siehe [Sichere Verbindungen](../development/secure-connections.md).

- **API-Token erstellen**—Benutzer müssen ein API-Token generieren, das für den SSH-Zugriff auf eine Umgebung verwendet wird. Sie benötigen das Token, um Authentifizierungs-Workflows für automatisierte Prozesse zu aktivieren.

  Bei Projekten mit aktivierter MFA-Durchsetzung müssen Sie das API-Token verwenden, um SSH-Zugriffsanfragen von automatisierten Konten zu authentifizieren. Das Token ermöglicht automatisierte Prozesse, um Authentifizierungs-Workflows zu umgehen, die TFA erfordern.

### Aktivieren von TFA für Cloud-Konten

Adobe Commerce on Cloud Infrastructure unterstützt TFA mit einer der folgenden Anwendungen:

- [Google Authenticator (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Authy (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [GAuth Authenticator (Firefox OS, Desktop, andere)](https://github.com/gbraad-apps/gauth)

Anweisungen zum Installieren der Authentifizierungsanwendung und Aktivieren von TFA finden Sie im Abschnitt _Kontoeinstellungen_ in der [!DNL Cloud Console].

**Aktivieren von TFA in Ihrem Benutzerkonto**:

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com).

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Im _Sicherheit_ Registerkarte, klicken **[!UICONTROL Set up application]**.

1. Wenn Sie auf Ihrem Mobilgerät keine genehmigte Authentifizierungsanwendung haben, installieren Sie eine mit den verknüpften Anweisungen.

1. Fügen Sie Ihr Adobe Commerce on Cloud-Infrastrukturkonto zur Authentifizierungsanwendung hinzu.

   - Öffnen Sie auf Ihrem Mobilgerät die Authentifizierungsanwendung. Fügen Sie dann den Einrichtungscode zur Anwendung hinzu.

   - Im [!UICONTROL **[!UICONTROL TFA set up - Application]**] Seite, geben Sie den TFA-Code von Ihrem Mobilgerät in die **[!UICONTROL Application verification code]** -Feld.

   - Klicks **[!UICONTROL Verify and save]**.

     Wenn der Code gültig ist, sendet Adobe eine Benachrichtigung an die E-Mail-Adresse des Kontos, die bestätigt, dass das Konto jetzt über TFA verfügt.

1. Optional. Aktivieren _Vertrauenswürdiger Browser_ -Einstellungen, um den Authentifizierungscode im Browser 30 Tage lang zwischenzuspeichern.

   Diese Konfiguration reduziert die Anzahl der Authentifizierungsprobleme während der Projektanmeldung.

1. Klicks **Speichern** oder **Überspringen**.

1. Speichern Sie die Wiederherstellungscodes.

   - Im _TFA-Einrichtung - Wiederherstellung_ Codes hinzufügen, kopieren und speichern Sie die Wiederherstellungscodes, damit Sie sich bei Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur anmelden können, wenn Sie nicht auf Ihr Mobilgerät oder Ihre Authentifizierungsanwendung zugreifen können.

   - Kopieren Sie die Wiederherstellungscodes an einen anderen Speicherort oder schreiben Sie sie auf, falls Sie den Zugriff auf Ihr Gerät oder Ihre Authentifizierungsanwendung verlieren.

   - Klicks **Speichern** um die Codes in Ihrem Konto zu speichern, damit Sie sie in Ihren Kontosicherheitseinstellungen anzeigen und verwalten können.

     >[!WARNING]
     >
     >Wenn Sie den Zugriff auf ein Konto mit TFA verlieren und nicht über die Liste der Wiederherstellungscodes verfügen, müssen Sie sich an Ihren Projektadministrator wenden oder [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die TFA-Anwendung zurückzusetzen.

1. Klicken Sie nach Abschluss des TFA-Setups auf **Speichern** , um Ihr Konto zu aktualisieren.

1. Authentifizieren Sie Ihre aktuelle Sitzung mit TFA.

   - Melden Sie sich von Ihrem Konto ab.
   - Melden Sie sich mit Ihrem Benutzernamen und Kennwort an.
   - Geben Sie bei Aufforderung den TFA-Code für die `accounts.magento.cloud` Eintrag aus der Authentifizierungsanwendung auf Ihrem Mobilgerät.

### Verwalten von TFA-Konfigurations- und Wiederherstellungscodes

Sie können die TFA-Konfiguration für ein Adobe Commerce-Konto für die Cloud-Infrastruktur über das _Sicherheit_ im Abschnitt _Mein Profil_ Seite.

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com).

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Im _Mein Profil_ klicken Sie auf die **[!UICONTROL Security]** Registerkarte.

1. Verwenden Sie die verfügbaren Links, um die TFA-Einstellungen für Ihr Adobe Commerce-Konto für die Cloud-Infrastruktur zu aktualisieren:

   - TFA deaktivieren
   - Zurücksetzen der Authentifizierungsanwendung
   - Hinzufügen oder Entfernen von vertrauenswürdigen Browsern
   - Anzeigen oder Aktualisieren von TFA-Wiederherstellungscodes in Ihrem Konto

### API-Token erstellen

Ein API-Token kann gegen ein OAuth 2-Zugriffstoken ausgetauscht werden, das dann zum Authentifizieren von Anfragen verwendet werden kann.

Bei Projekten mit aktivierter MFA-Durchsetzung müssen Sie über ein API-Token verfügen, um den SSH-Zugriff für Maschinenbenutzer und automatisierte Prozesse zu ermöglichen.

>[!IMPORTANT]
>
>Protect-API-Token-Werte für Ihr Konto. Stellen Sie den Wert nicht in Codebeispielen, Bildschirmaufzeichnungen oder unsicherer Client-Server-Kommunikation bereit. Stellen Sie außerdem den Wert nicht im Quellcode bereit, der in öffentlichen Repositorys gespeichert ist.

**So erstellen Sie ein API-Token**:

1. Anmelden bei [Ihr Konto](https://console.adobecommerce.com).

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Im _Mein Profil_ klicken Sie auf die **[!UICONTROL API tokens]** Registerkarte.

1. Klicks **[!UICONTROL Create API token]** und geben Sie einen Namen ein, beispielsweise einen Namen, der mit dem maschinellen Benutzer oder automatisierten Prozess übereinstimmt, der das API-Token verwendet.

   ![API-Token](../../assets/api-token-name.png)

1. Klicks **[!UICONTROL Create API token]**.
