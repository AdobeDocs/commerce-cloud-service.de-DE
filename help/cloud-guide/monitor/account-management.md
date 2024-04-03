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

Einem New Relic-Konto kann nur eine Person die Eigentümerrolle zugewiesen werden. Wenn Sie den Kontoinhaber ändern müssen, weisen Sie die Administratorrolle dem aktuellen Eigentümer zu und weisen Sie dann die Eigentümerrolle einem anderen Benutzer zu. Siehe [Kontoinhaber aktualisieren](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) im _New Relic-Dokumentation_ für Anweisungen.

Richtlinien für die Verwaltung des New Relic-Zugriffs:

- Projekteigentümer und Admin-Benutzer können Benutzer zum New Relic-Konto hinzufügen und daraus entfernen.
- Erstellen Sie nicht mehr als fünf volle Zugriffsberechtigungen **Benutzer**.
- Gewähren Sie nur uneingeschränkten Zugriff für Benutzer, die Zugriff auf das vollständige Funktionssatz benötigen.
- Es gibt keine spezifischen Leitlinien zu kostenlosen **Beschränkt** Benutzer.

>[!TIP]
>
>Bevor Sie einem Benutzer die Eigentümerrolle zuweisen, überprüfen Sie, ob der Benutzer im New Relic-Konto für Adobe Commerce in der Cloud-Infrastruktur vorhanden ist. Wenn Sie den Benutzer zu diesem Konto hinzufügen müssen und ein bestehender Kontoinhaber oder -administrator nicht helfen kann, kann jeder Benutzer mit Zugriff auf die [Adobe Partnerschafts-Eigentümerkonto](https://account.newrelic.com/accounts/1311131/users) für New Relic können Benutzer im Namen des Kunden hinzufügen.

Mindestens 1 hinzufügen **Admin** -Benutzer auf Ihr New Relic-Konto zu, das alle Zugriffs-, Integrations- und Tool-Verwendungsmöglichkeiten verwalten kann.

**So greifen Sie auf die Benutzerverwaltung in New Relic zu**:

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login).

1. Wählen Sie Ihren Benutzernamen in der Navigation unten links aus.

1. Klicks **[!UICONTROL Administration]** und wählen Sie eine der folgenden Optionen aus der Liste aus:

   - **[!UICONTROL User management]** , um einen Benutzer hinzuzufügen und aktive Benutzer und ausstehende Einladungen zu verwalten.

   - **[!UICONTROL Access management]** um Benutzergruppen, Rollen und Konten zu verwalten.

Siehe [Benutzerverwaltung](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) im _New Relic_ Dokumentation.

## Konfigurieren von New Relic für die Starterumgebung

>[!NOTE]
>
>**Pro Umgebung** sind für die Verwendung von New Relic-Diensten vorkonfiguriert und können Anweisungen zum Aktivieren und Verbinden überspringen. Wenn New Relic APM nicht in der Staging- und Produktionsumgebung installiert ist oder die New Relic-Infrastruktur in der Produktionsumgebung nicht verfügbar ist, [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Installation anzufordern.

Bei Starterumgebungen müssen Sie die `.magento.app.yaml` -Datei, um zu überprüfen, ob die `runtime` enthält die New Relic-Erweiterung. Wenn die Erweiterung nicht konfiguriert wurde, fügen Sie Folgendes hinzu:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Lizenzschlüssel anwenden

Um eine Cloud-Umgebung mit New Relic zu verbinden, fügen Sie den New Relic-Lizenzschlüssel zur Umgebung hinzu.

- Für **Pro Projekte** fügt Adobe den Lizenzschlüssel während des Bereitstellungsprozesses Ihren Produktions- und Staging-Umgebungen hinzu. Sie können sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) , um die Verbindung zwischen Ihrer Adobe Commerce auf der Cloud-Infrastruktur-Site und New Relic zu überprüfen.

- Für **Starterprojekte**, verfügen Sie über einen New Relic-Lizenzschlüssel, der bis zu _three_ Umgebungen. Sie müssen den Schlüssel manuell zu Ihren Umgebungskonfigurationen hinzufügen. Starterumgebungen sind nicht für die Verwendung des New Relic-Dienstes vorkonfiguriert.

Aktivieren Sie bei Starterumgebungen die New Relic-Integration, indem Sie den New Relic-Lizenzschlüssel zur Umgebungskonfiguration hinzufügen. Fügen Sie den Schlüssel zu den Staging- und Produktionsumgebungen und einer anderen Umgebung Ihrer Wahl hinzu. Für die Konfiguration ist nur der New Relic-Lizenzschlüssel erforderlich. Weitere Informationen zu zusätzlichen Konfigurationsoptionen finden Sie im Abschnitt [New Relic Reporting](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) Thema im _Adobe Commerce-Benutzerhandbuch_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Anmeldedaten für die Adobe Commerce-Kontoseite oder für die mit Ihrem Projekt verknüpfte New Relic-Lizenz
>- [Zugriff auf Administratorebene](../project/user-access.md) in die Starterumgebungen zur Konfiguration
>- Anmeldedaten für den Zugriff auf [Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) Umwelt

**So konfigurieren Sie New Relic für Starterumgebungen**:

1. Suchen Sie Ihren New Relic-Lizenzschlüssel über [!DNL Cloud Console] oder die Cloud-CLI.

   **[!DNL Cloud Console]method**:

   - Cloud-Projekt öffnen [Kontoseite](https://accounts.magento.cloud/user).

   - Im _Projekte_ Registerkarte, suchen Sie Ihr Projekt.

   - Klicks **Details anzeigen** für Informationen zur Projektinfrastruktur.

   - Erweitern Sie die **New Relic-Dienst** -Abschnitt, um den Lizenzschlüssel anzuzeigen.

   - Kopieren Sie den Lizenzschlüssel.

   **Cloud-CLI-Methode**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Fügen Sie den New Relic-Lizenzschlüssel mithilfe der `magento-cloud` CLI.

   - Ändern Sie die Umgebung, die den Lizenzschlüssel benötigt.
   - Aktualisieren Sie den Variablenwert wie folgt `magento-cloud` CLI-Befehl:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Optional können Sie sie über das [Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login) , um zu überprüfen, ob Sie Daten aus der Adobe Commerce-Umgebung anzeigen können. Siehe [Leistung untersuchen](investigate-performance.md).

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
   >Wenn Sie den Lizenzschlüssel als _Projekt_ müssen Sie diese Variable auf Projektebene entfernen. Eine Projektvariable fügt die Lizenz zu _each_ erstellte Umgebungsverzweigung, die die Lizenzbeschränkung verbrauchen oder überschreiten kann. So listen Sie Projektvariablen auf: `magento-cloud variable:list --level project`

1. Löschen Sie die Lizenzvariable.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
