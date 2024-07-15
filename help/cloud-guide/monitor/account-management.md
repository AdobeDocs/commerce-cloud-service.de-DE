---
title: New Relic-Kontoverwaltung
description: Erfahren Sie, wie Sie auf Ihr New Relic-Konto zugreifen und den Zugriff, Integrationen und die Verwendung von Tools für Ihre Adobe Commerce im Cloud-Infrastrukturprojekt verwalten können.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# New Relic-Kontoverwaltung

Wenn Adobe Ihr Cloud-Infrastrukturprojekt bereitstellt, erhält der Lizenzinhaber eine E-Mail von New Relic mit Anmeldeinformationen und Anweisungen zum Zugriff auf das New Relic-Konto. Wenn Sie die E-Mail nicht erhalten haben, verwenden Sie die E-Mail-Adresse des Lizenzinhabers, um das New Relic-Kennwort zurückzusetzen.

## Verwalten des Benutzerzugriffs

Einem New Relic-Konto kann nur eine Person die Eigentümerrolle zugewiesen werden. Wenn Sie den Kontoinhaber ändern müssen, weisen Sie die Administratorrolle dem aktuellen Eigentümer zu und weisen Sie dann die Eigentümerrolle einem anderen Benutzer zu. Anweisungen finden Sie unter [Aktualisieren des Kontoinhabers](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) in der Dokumentation zu _New Relic_ .

Richtlinien für die Verwaltung des New Relic-Zugriffs:

- Projekteigentümer und Admin-Benutzer können Benutzer zum New Relic-Konto hinzufügen und daraus entfernen.
- Erstellen Sie nicht mehr als fünf volle **Benutzer**.
- Gewähren Sie nur uneingeschränkten Zugriff für Benutzer, die Zugriff auf das vollständige Funktionssatz benötigen.
- Es gibt keine spezielle Anleitung für freie **Eingeschränkte** Benutzer.

>[!TIP]
>
>Bevor Sie einem Benutzer die Eigentümerrolle zuweisen, überprüfen Sie, ob der Benutzer im New Relic-Konto für Adobe Commerce in der Cloud-Infrastruktur vorhanden ist. Wenn Sie den Benutzer zu diesem Konto hinzufügen müssen und ein bestehender Kontoinhaber oder -administrator nicht helfen kann, kann jeder Benutzer mit Zugriff auf das [Adobe Partnereigentümerkonto](https://account.newrelic.com/accounts/1311131/users) für New Relic Benutzer im Namen des Kunden hinzufügen.

Fügen Sie Ihrem New Relic-Konto mindestens einen **Admin** -Benutzer hinzu, der alle Zugriffs-, Integrations- und Tool-Verwendungen verwalten kann.

**So greifen Sie auf die Benutzerverwaltung in New Relic zu:**

1. Melden Sie sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) an.

1. Wählen Sie Ihren Benutzernamen in der Navigation unten links aus.

1. Klicken Sie auf **[!UICONTROL Administration]** und wählen Sie aus der Liste eine der folgenden Optionen aus:

   - **[!UICONTROL User management]** , um einen Benutzer hinzuzufügen und aktive Benutzer und ausstehende Einladungen zu verwalten.

   - **[!UICONTROL Access management]** , um Benutzergruppen, Rollen und Konten zu verwalten.

Siehe [Benutzerverwaltung](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) in der Dokumentation zu _New Relic_ .

## Konfigurieren von New Relic für die Starterumgebung

>[!NOTE]
>
>**Pro-Umgebungen** sind für die Verwendung von New Relic-Diensten vorkonfiguriert und können Anweisungen zum Aktivieren und Verbinden überspringen. Wenn das New Relic-APM nicht in der Staging- und Produktionsumgebung installiert ist oder die New Relic-Infrastruktur in der Produktionsumgebung nicht verfügbar ist, senden [ein Adobe Commerce-Supportticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um eine Installation anzufordern.

Bei Starterumgebungen müssen Sie die Datei `.magento.app.yaml` überprüfen, um sicherzustellen, dass der Abschnitt `runtime` die New Relic-Erweiterung enthält. Wenn die Erweiterung nicht konfiguriert wurde, fügen Sie Folgendes hinzu:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Lizenzschlüssel anwenden

Um eine Cloud-Umgebung mit New Relic zu verbinden, fügen Sie den New Relic-Lizenzschlüssel zur Umgebung hinzu.

- Für **Pro projects** fügt Adobe während des Bereitstellungsprozesses den Lizenzschlüssel zu Ihren Produktions- und Staging-Umgebungen hinzu. Sie können sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) anmelden, um die Verbindung zwischen Ihrer Adobe Commerce auf der Cloud-Infrastruktur-Site und New Relic zu überprüfen.

- Für **Starterprojekte** verfügen Sie über einen New Relic-Lizenzschlüssel, der bis zu _drei_ -Umgebungen unterstützt. Sie müssen den Schlüssel manuell zu Ihren Umgebungskonfigurationen hinzufügen. Starterumgebungen sind nicht für die Verwendung des New Relic-Dienstes vorkonfiguriert.

Aktivieren Sie bei Starterumgebungen die New Relic-Integration, indem Sie den New Relic-Lizenzschlüssel zur Umgebungskonfiguration hinzufügen. Fügen Sie den Schlüssel zu den Staging- und Produktionsumgebungen und einer anderen Umgebung Ihrer Wahl hinzu. Für die Konfiguration ist nur der New Relic-Lizenzschlüssel erforderlich. Informationen zu zusätzlichen Konfigurationsoptionen finden Sie im Thema [New Relic Reporting](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) im _Adobe Commerce-Benutzerhandbuch_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Anmeldedaten für die Adobe Commerce-Kontoseite oder für die mit Ihrem Projekt verknüpfte New Relic-Lizenz
>- [Zugriff auf Starterumgebungen auf Administratorebene](../project/user-access.md) zum Konfigurieren
>- Anmeldedaten für den Zugriff auf [Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) für die Umgebung

**So konfigurieren Sie New Relic für Starterumgebungen**:

1. Suchen Sie Ihren New Relic-Lizenzschlüssel über die Cloud-CLI (0) oder die Cloud-CLI.[!DNL Cloud Console]

   **[!DNL Cloud Console]method**:

   - Öffnen Sie die Cloud-Projekt-[Kontoseite](https://accounts.magento.cloud/user).

   - Suchen Sie auf der Registerkarte _Projekte_ Ihr Projekt.

   - Klicken Sie auf **Details anzeigen** , um Informationen zur Projektinfrastruktur zu erhalten.

   - Erweitern Sie den Abschnitt **New Relic-Dienst** , um den Lizenzschlüssel anzuzeigen.

   - Kopieren Sie den Lizenzschlüssel.

   **Cloud-CLI-Methode**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Fügen Sie den New Relic-Lizenzschlüssel mithilfe der CLI `magento-cloud` einer Umgebung hinzu.

   - Ändern Sie die Umgebung, die den Lizenzschlüssel benötigt.
   - Aktualisieren Sie den Variablenwert mit dem folgenden `magento-cloud` CLI-Befehl:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Optional können Sie sie über den [Commerce-Administrator](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store) hinzufügen.

1. Melden Sie sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) an, um zu überprüfen, ob Sie Daten aus der Adobe Commerce-Umgebung anzeigen können. Siehe [Leistung untersuchen](investigate-performance.md).

### Lizenzschlüssel löschen

Sie können Ihren New Relic-Lizenzschlüssel nur in drei aktiven Umgebungen verwenden. Wenn der Schlüssel in drei Umgebungen verwendet wird, müssen Sie den Schlüssel aus einer Umgebung entfernen, bevor Sie ihn einer anderen Umgebung hinzufügen können.

**So entfernen Sie einen Lizenzschlüssel aus einer Umgebung**:

1. Umgebungsvariablen auflisten.

   ```bash
   magento-cloud variable:list
   ```

   Beispielantwort:

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Wenn Sie den Lizenzschlüssel als _Projekt_-Variable hinzugefügt haben, müssen Sie diese Variable auf Projektebene entfernen. Eine Projektvariable fügt die Lizenz _jedem erstellten_ -Umgebungszweig hinzu, der die Lizenzbeschränkung verbrauchen oder überschreiten kann. So listen Sie Projektvariablen auf: `magento-cloud variable:list --level project`

1. Löschen Sie die Lizenzvariable.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
