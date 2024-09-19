---
title: Verwalten des Benutzerzugriffs
description: Erfahren Sie, wie Sie den Benutzerzugriff auf Adobe Commerce in Cloud-Infrastrukturprojekten und -Umgebungen verwalten.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: 5e4be034a392716ea55e2878d336cb9ecac1e052
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---

# Verwalten des Benutzerzugriffs

Adobe Commerce-Projekte zur Cloud-Infrastruktur nutzen rollenbasierten Zugriff. Auf Projektebene stehen zwei Rollen zur Verfügung:

- **Projektadministrator**: Schreiben Sie Zugriff auf alle Projektumgebungen und können Benutzer verwalten, Code pushen und Projekteinstellungen aktualisieren. (Zuvor als **Super Admin** bezeichnet)
- **Projekt-Viewer**: Schreibgeschützter Zugriff auf alle Projektumgebungen.

Projekt-Viewer können in keiner Umgebung Aufgaben ausführen. Sie können jedoch Projekt-Viewern Schreibzugriff auf einen bestimmten Umgebungstyp gewähren.

Der Zugriff auf Umgebungsebene basiert auf dem Umgebungstyp: Produktion, Staging und Entwicklung. Wenn einem Benutzer _Viewer_ Berechtigungen für _Entwicklungsumgebungen_ gewährt werden, können alle **5} Entwicklungsumgebungen im Projekt angezeigt werden.** In der folgenden Tabelle werden die den einzelnen Berechtigungsebenen zugewiesenen Fähigkeiten erläutert:

| Berechtigungsebene | Zugriff | SSH-Zugriff |
| ------------------ | ----------- | :----------: |
| **Admin** | Ausführen von Administratoraufgaben, wie z. B. Einstellungen ändern, Push-Code, Ausführen von Aufgaben und Verzweigungsverwaltung, einschließlich der Zusammenführung mit der übergeordneten Umgebung | Ja |
| **Contributor** | Push-Code und Verzweigung der Umgebung; kann Einstellungen nicht ändern oder Aktionen ausführen | Ja |
| **Betrachter** | Schreibgeschützter Zugriff auf den Umgebungstyp | Nein |
| **Kein Zugriff** | Kein Zugriff auf den Umgebungstyp | Nein |

{style="table-layout:auto"}

Sie können Benutzer hinzufügen und Rollen mithilfe der CLI `magento-cloud` oder der [!DNL Cloud Console] zuweisen.

>[!BEGINSHADEBOX]

**Voraussetzungen:**

- Ein registrierter Benutzer bei einem Adobe ID. Benutzer müssen [sich für ein Adobe-Konto registrieren](https://account.adobe.com) und dann [ihr Cloud-Konto initialisieren](https://console.adobecommerce.com), bevor sie einem Cloud-Projekt hinzugefügt werden können.
- Benutzer mit der Rolle **Admin** können Benutzer mit der CLI `magento-cloud` nicht verwalten. Benutzer, denen die Rolle **Kontoinhaber** zugewiesen wurde, können diese verwalten.

>[!ENDSHADEBOX]

## Benutzer mit der CLI verwalten

Verwenden Sie die `magento-cloud`-CLI, um Benutzer zu verwalten und in automatisierte Systeme zu integrieren:

- `magento-cloud user:add` - Hinzufügen eines Benutzers zum Projekt
- `magento-cloud user:delete` - Löschen eines Benutzers
- `magento-cloud user:list [users]` list-Projektbenutzer
- `magento-cloud user:role` - Anzeigen oder Ändern der Benutzerrolle
- `magento-cloud user:update` Benutzerrolle in einem Projekt aktualisieren

In den folgenden Beispielen wird die CLI `magento-cloud` verwendet, um einen Benutzer hinzuzufügen, Rollen zu konfigurieren, Projektzuweisungen zu ändern und Benutzerrollen zuzuweisen.

**So fügen Sie einen Benutzer hinzu und weisen die Rollen zu**:

1. Verwenden Sie die CLI `magento-cloud` , um den Benutzer hinzuzufügen.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >Der Benutzer muss über eine Adobe ID verfügen; siehe die [Voraussetzungen](#add-users-and-manage-access).

1. Befolgen Sie die Anweisungen: Geben Sie die E-Mail-Adresse des Benutzers an, legen Sie die Rollen &quot;Projekt&quot;und &quot;Umgebung&quot;fest und fügen Sie den Benutzer hinzu.

   > Beispielaufforderungen

   ```
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

```
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Benutzer zu mehreren Umgebungen hinzufügen

So fügen Sie einen Benutzer als `viewer` in einer `Production` -Umgebung und als `contributor` in einer `Integration` -Umgebung hinzu:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Berechtigungen der Benutzerumgebung aktualisieren

Aktualisieren der Benutzerumgebungsberechtigungen auf `admin` in der `Production`-Umgebung:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Verwalten von Benutzern über die [!DNL Cloud Console]

Sie können die [[!DNL Cloud Console]](../../get-started/cloud-console.md) verwenden, um Berechtigungen hinzuzufügen, und die Funktion _Bearbeiten_ verwenden, um Berechtigungen für einen vorhandenen Benutzer zu ändern.

>[!IMPORTANT]
>
>Der Benutzer muss über eine Adobe ID verfügen; siehe die [Voraussetzungen](#add-users-and-manage-access).

### Einen Benutzer zum Projekt hinzufügen

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com/) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Klicken Sie im Projekt-Dashboard auf das Konfigurationssymbol oben rechts.

1. Klicken Sie unter &quot;_Projekteinstellungen_&quot;auf &quot;**[!UICONTROL Access]**&quot;.

1. Klicken Sie in der Ansicht _Zugriff_ auf **[!UICONTROL Add]**.

1. Füllen Sie das Formular _[!UICONTROL Add User]_aus:

   - Geben Sie die E-Mail-Adresse des Benutzers ein.

   - **[!UICONTROL Project admin]** - Erteilen Sie Administratorrechte für alle Einstellungen und Umgebungstypen.

   - **[!UICONTROL Environment types and permissions]** - Gewähren Sie bestimmten Umgebungstypen Zugriff und spezifische Berechtigungsstufen. _Kein Zugriff_, _Admin_ (Einstellungen ändern, Aktion ausführen, Zusammenführungscode), _Mitarbeiter_ (Push-Code) oder _Betrachter_ (nur Ansicht).

   >[!TIP]
   >
   >Nur ein **Projektadministrator** kann Benutzer in jeder Umgebung verwalten. Um einem Benutzer Zugriff auf die Registerkarte **Zugriff** zu gewähren, muss diesem Benutzer ein anderer **Projektadministrator** oder der **Kontoinhaber** die Rolle **Projektadministrator** zuweisen.

1. Klicken Sie auf **[!UICONTROL Add User]**.

   >[!IMPORTANT]
   >
   >Beim Hinzufügen eines Benutzers wird eine Bereitstellung nicht automatisch Trigger.

1. Stellen Sie nach dem Hinzufügen von Benutzern alle Umgebungen erneut bereit, um die Änderungen anzuwenden. Beim Hinzufügen eines Benutzers wird eine Bereitstellung nicht automatisch Trigger. Die Neubereitstellung ist ein wichtiger Schritt, um sicherzustellen, dass der Benutzer über SSH auf eine Umgebung zugreifen oder Administratoraufgaben ausführen kann.

Nachdem Sie den Benutzer hinzugefügt haben, sendet Adobe eine E-Mail mit Anweisungen zum Zugriff auf Adobe Commerce im Cloud-Infrastrukturprojekt an die angegebene Adresse.

## Authentifizierungspflichten für Benutzer

Für zusätzliche Sicherheit bietet Adobe eine Durchsetzung der Multi-Factor-Authentifizierung (MFA) auf Projektebene, sodass eine Zweifaktorauthentifizierung (TFA) für den SSH-Zugriff auf Adobe Commerce über den Quellcode und die Umgebungen von Cloud-Infrastruktur-Projekten erforderlich ist. Siehe [MFA für SSH aktivieren](multi-factor-authentication.md).

Wenn die MFA-Durchsetzung in einem Adobe Commerce-Projekt zur Cloud-Infrastruktur aktiviert ist, müssen alle Benutzer mit SSH-Zugriff auf eine Umgebung in diesem Projekt TFA in ihrem Adobe Commerce-Konto für die Cloud-Infrastruktur aktivieren. Für automatisierte Prozesse können Sie einen Maschinenbenutzer und ein API-Token erstellen, die über die Befehlszeile authentifiziert werden.

Nachdem Sie einen Benutzer zu einem Cloud-Projekt hinzugefügt haben, bitten Sie den Benutzer, seine Kontosicherheitseinstellungen zu überprüfen und die folgenden Sicherheitskonfigurationen nach Bedarf hinzuzufügen:

- **Aktivieren Sie TFA**: Erfüllen Sie die Sicherheits- und Compliance-Standards durch Konfiguration der Authentifizierung mit zwei Faktoren. Für Projekte, die mit der [MFA-Durchsetzung](multi-factor-authentication.md) konfiguriert wurden, ist TFA für Konten erforderlich, die SSH verwenden, um auf die Projekte zuzugreifen.

- **SSH-Schlüssel aktivieren** - Benutzer, die Zugriff auf Adobe Commerce in Cloud-Infrastruktur-Quellcode-Repositorys benötigen, müssen SSH-Schlüssel in ihrem Konto aktivieren. Siehe [Sichere Verbindungen](../development/secure-connections.md).

- **API-Token erstellen**: Benutzer müssen ein API-Token generieren, das für den SSH-Zugriff auf eine Umgebung verwendet wird. Sie benötigen das Token, um Authentifizierungs-Workflows für automatisierte Prozesse zu aktivieren.

  Bei Projekten mit aktivierter MFA-Durchsetzung müssen Sie das API-Token verwenden, um SSH-Zugriffsanfragen von automatisierten Konten zu authentifizieren. Das Token ermöglicht automatisierte Prozesse, um Authentifizierungs-Workflows zu umgehen, die TFA erfordern.

### Aktivieren von TFA für Cloud-Konten

Adobe Commerce on Cloud Infrastructure unterstützt TFA mit einer der folgenden Anwendungen:

- [Google Authenticator (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Authy (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [GAuth Authenticator (Firefox OS, Desktop, andere)](https://github.com/gbraad-apps/gauth)

Anweisungen zum Installieren der Authentifizierungsanwendung und Aktivieren von TFA finden Sie auf der Seite _Kontoeinstellungen_ im Abschnitt [!DNL Cloud Console].

**Aktivieren von TFA für Ihr Benutzerkonto**:

1. Melden Sie sich bei [Ihrem Konto](https://console.adobecommerce.com) an.

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Klicken Sie auf der Registerkarte _Sicherheit_ auf **[!UICONTROL Set up application]**.

1. Wenn Sie auf Ihrem Mobilgerät keine genehmigte Authentifizierungsanwendung haben, installieren Sie eine mit den verknüpften Anweisungen.

1. Fügen Sie Ihr Adobe Commerce on Cloud-Infrastrukturkonto zur Authentifizierungsanwendung hinzu.

   - Öffnen Sie auf Ihrem Mobilgerät die Authentifizierungsanwendung. Fügen Sie dann den Einrichtungscode zur Anwendung hinzu.

   - Geben Sie auf der Seite [!UICONTROL **[!UICONTROL TFA set up - Application]**] den TFA-Code von Ihrem Mobilgerät in das Feld **[!UICONTROL Application verification code]** ein.

   - Klicken Sie auf **[!UICONTROL Verify and save]**.

     Wenn der Code gültig ist, sendet Adobe eine Benachrichtigung an die E-Mail-Adresse des Kontos, die bestätigt, dass das Konto jetzt über TFA verfügt.

1. Optional. Aktivieren Sie die Einstellungen für _vertrauenswürdigen Browser_ , um den Authentifizierungscode 30 Tage lang im Browser zwischenzuspeichern.

   Diese Konfiguration reduziert die Anzahl der Authentifizierungsprobleme während der Projektanmeldung.

1. Klicken Sie auf **Speichern** oder **Überspringen**.

1. Speichern Sie die Wiederherstellungscodes.

   - Kopieren Sie auf der Seite &quot;_TFA-Setup - Recovery_ -Codes&quot;die Wiederherstellungscodes und speichern Sie sie, damit Sie sich bei Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur anmelden können, wenn Sie nicht auf Ihr Mobilgerät oder Ihre Authentifizierungsanwendung zugreifen können.

   - Kopieren Sie die Wiederherstellungscodes an einen anderen Speicherort oder schreiben Sie sie auf, falls Sie den Zugriff auf Ihr Gerät oder Ihre Authentifizierungsanwendung verlieren.

   - Klicken Sie auf **Speichern** , um die Codes in Ihrem Konto zu speichern, damit Sie sie in Ihren Kontosicherheitseinstellungen anzeigen und verwalten können.

     >[!WARNING]
     >
     >Wenn Sie den Zugriff auf ein Konto mit TFA verlieren und nicht über die Liste der Wiederherstellungscodes verfügen, müssen Sie sich an Ihren Projektadministrator wenden oder [Senden Sie ein Adobe Commerce-Supportticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die TFA-Anwendung zurückzusetzen.

1. Klicken Sie nach Abschluss des TFA-Setups auf **Speichern** , um Ihr Konto zu aktualisieren.

1. Authentifizieren Sie Ihre aktuelle Sitzung mit TFA.

   - Melden Sie sich von Ihrem Konto ab.
   - Melden Sie sich mit Ihrem Benutzernamen und Kennwort an.
   - Geben Sie bei Aufforderung den TFA-Code für den Eintrag `accounts.magento.cloud` aus der Authentifizierungsanwendung auf Ihrem Mobilgerät ein.

### Verwalten von TFA-Konfigurations- und Wiederherstellungscodes

Sie können die TFA-Konfiguration für ein Adobe Commerce-Konto für Cloud-Infrastruktur im Abschnitt _Sicherheit_ auf der Seite _Mein Profil_ verwalten.

1. Melden Sie sich bei [Ihrem Konto](https://console.adobecommerce.com) an.

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Klicken Sie auf der Seite _Mein Profil_ auf die Registerkarte **[!UICONTROL Security]** .

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

1. Melden Sie sich bei [Ihrem Konto](https://console.adobecommerce.com) an.

1. Klicken Sie oben rechts im Kontomenü auf **[!UICONTROL My Profile]**.

1. Klicken Sie auf der Seite _Mein Profil_ auf die Registerkarte **[!UICONTROL API tokens]** .

1. Klicken Sie auf **[!UICONTROL Create API token]** und geben Sie einen Namen ein, z. B. einen Namen, der dem maschinellen Benutzer oder automatisierten Prozess entspricht, der das API-Token verwendet.

   ![API-Token](../../assets/api-token-name.png)

1. Klicken Sie auf **[!UICONTROL Create API token]**.
