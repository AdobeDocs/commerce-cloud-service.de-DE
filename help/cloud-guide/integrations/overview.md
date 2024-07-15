---
title: Integrationen - Übersicht
description: Erfahren Sie mehr über Integrationsoptionen von Drittanbietern für Ihre Adobe Commerce im Cloud-Infrastrukturprojekt.
role: Developer
feature: Cloud, Integration
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: 2dddba73-5b88-4b5d-a0e1-2f1c1f52354c
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Integrationen - Übersicht

Integrationen sind nützlich für die Verwendung externer Dienste wie Git-Hosting oder Slack-Bots und die Wartung Ihrer aktuellen Entwicklungsprozesse, z. B. die Verwendung der Pull-Anforderungsfunktion für die Codeüberprüfung in GitHub. Sie können die folgenden Integrationen zu Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur hinzufügen:

![Integrationen](/help/assets/integrations.png)

>[!BEGINTABS]

>[!TAB CLI]

**Hinzufügen einer Integration mithilfe der Cloud CLI**:

Der folgende Befehl startet interaktive Aufforderungen zur Auswahl des Typs und der Optionen für die neue Integration.

```bash
magento-cloud integration:add
```

**So listen Sie die für Ihr Projekt konfigurierten Integrationen auf**:

```bash
magento-cloud integration:list
```

Beispielantwort:

```terminal
+----------+--------------+---------------------------------------------------------------------------+
| ID       | Type         | Summary                                                                   |
+----------+--------------+---------------------------------------------------------------------------+
| <int-id> | bitbucket    | Repository: user/magento-int                                              |
|          |              | Hook URL:                                                                 |
|          |              | https://magento-url.cloud/api/projects/projectID/integrations/int-ID/hook |
| <int-id> | health.email | From: you@example.com                                                     |
|          |              | To: them@example.com                                                      |
+----------+--------------+---------------------------------------------------------------------------+
```

>[!TAB Konsole]

**Hinzufügen einer Integration mithilfe des[!DNL Cloud Console]**:

1. Klicken Sie in _Projekteinstellungen_ auf **[!UICONTROL Integrations]**.

1. Klicken Sie auf einen Integrationstyp oder auf **[!UICONTROL Add integration]**.

1. Führen Sie die Schritte zur Auswahl und Konfiguration des Integrationstyps durch.

1. Nach dem Hinzufügen der Integration wird sie in der Liste in der Ansicht &quot;Integrationen&quot;angezeigt.

>[!ENDTABS]

## Commerce-Webhooks

Sie können Commerce-Webhooks in Ihrem Cloud-Projekt mit der globalen Variable [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) konfigurieren. Commerce-Webhooks senden Anfragen als Reaktion auf von Commerce generierte Ereignisse an einen externen Server. Im [_Webhooks-Handbuch_](https://developer.adobe.com/commerce/extensibility/webhooks) wird diese Funktion ausführlich beschrieben.

## Allgemeine Webhooks

Sie können Cloud-Infrastruktur- und Repository-Ereignisse mithilfe einer benutzerdefinierten Webhook-Integration in `POST` JSON-Nachrichten mit einer _webhook_ -URL erfassen und in Berichte aufnehmen.

**Verwenden Sie die folgende Syntax, um eine Webhook-URL hinzuzufügen**:

```bash
magento-cloud integration:add --type=webhook --url=https://hook-url.example.com
```

- `type` - Geben Sie den Integrationstyp `webhook` an.
- `url` - Geben Sie die Webhook-URL an, die JSON-Nachrichten empfangen kann.

Die Beispielantwort zeigt eine Reihe von Aufforderungen, die eine Möglichkeit bieten, die Integration anzupassen. Bei Verwendung der standardmäßigen (leeren) Antwort werden Meldungen zu allen Ereignissen in allen Umgebungen eines Projekts gesendet.

Sie können die Integration so anpassen, dass bestimmte [Ereignisse](#events-to-report) gemeldet werden, z. B. das Pushen von Code in eine Verzweigung. Sie können beispielsweise das `environment.push` -Ereignis angeben, um eine Nachricht zu senden, wenn ein Benutzer Code an eine Verzweigung sendet:

```terminal
Events to report (--events)
A list of events to report, e.g. environment.push
Default: *
Enter comma-separated values (or leave this blank)
>
```

Sie können Ereignisse in einem Status `pending`, `in_progress` oder `complete` melden:

```terminal
States to report (--states)
A list of states to report, e.g. pending, in_progress, complete
Default: complete
Enter comma-separated values (or leave this blank)
>
```

Außerdem können Sie __ - oder __ -Meldungen für bestimmte Umgebungen ausschließen:

```terminal
Included environments (--environments)
The environment IDs to include
Default: *
Enter comma-separated values (or leave this blank)
>

Excluded environments (--excluded-environments)
The environment IDs to exclude
Enter comma-separated values (or leave this blank)
>
```

Nach Abschluss der Integration erhalten Sie eine Zusammenfassung der Werte:

```terminal
Created integration integration-ID (type: webhook)
+-----------------------+------------------------------+
| Property              | Value                        |
+-----------------------+------------------------------+
| id                    | integration-ID               |
| type                  | webhook                      |
| events                | - '*'                        |
| environments          | - '*'                        |
| excluded_environments | {  }                         |
| states                | - complete                   |
| url                   | https://hook-url.example.com |
+-----------------------+------------------------------+
```

### Vorhandene Integration aktualisieren

Sie können eine vorhandene Integration aktualisieren. Ändern Sie beispielsweise die Status von `complete` in `pending`, indem Sie Folgendes verwenden:

```bash
magento-cloud integration:update --states=pending <int-id>
```

Beispielantwort:

```terminal
Integration integration-ID (webhook) updated
+-----------------------+------------------------------+
| Property              | Value                        |
+-----------------------+------------------------------+
| id                    | integration-ID               |
| type                  | webhook                      |
| events                | - '*'                        |
| environments          | - '*'                        |
| excluded_environments | {  }                         |
| states                | - pending                    |
| url                   | https://hook-url.example.com |
+-----------------------+------------------------------+
```

### Zu meldende Ereignisse

| Ereignis | Beschreibung |
| ----- | :-----------|
| `environment.access.add` | Benutzern wurde Zugriff auf die Umgebung gewährt |
| `environment.access.remove` | Ein Benutzer wurde aus der Umgebung entfernt |
| `environment.activate` | Eine Verzweigung wurde mit einer Umgebung &quot;aktiviert&quot; |
| `environment.backup` | Ein Benutzer hat einen Schnappschuss ausgelöst |
| `environment.branch` | Eine Verzweigung wurde mithilfe der Verwaltungskonsole erstellt |
| `environment.deactivate` | Eine Verzweigung wurde &quot;deaktiviert&quot;. Der Code ist noch vorhanden, aber die Umgebung wurde zerstört |
| `environment.delete` | Eine Verzweigung wurde gelöscht |
| `environment.initialize` | Die `master`-Verzweigung des Projekts, das mit einem ersten Commit initialisiert wurde |
| `environment.merge` | Eine aktive Verzweigung wurde mithilfe der Verwaltungskonsole oder API zusammengeführt. |
| `environment.push` | Ein Benutzer hat Code an eine Verzweigung gesendet |
| `environment.restore` | Ein Benutzer hat eine Momentaufnahme wiederhergestellt |
| `environment.route.create` | Eine Route wurde mithilfe der Verwaltungskonsole erstellt |
| `environment.route.delete` | Eine Route wurde mithilfe der Verwaltungskonsole gelöscht |
| `environment.route.update` | Eine Route wurde mithilfe der Verwaltungskonsole geändert |
| `environment.subscription.update` | Die Größe der Umgebung &quot;`master`&quot; wurde geändert, da sich das Abonnement geändert hat, es jedoch keine Inhaltsänderungen gibt. |
| `environment.synchronize` | In einer Umgebung wurden Daten oder Code aus der übergeordneten Umgebung erneut kopiert |
| `environment.update.http_access` | HTTP-Zugriffsregeln für eine Umgebung wurden geändert |
| `environment.update.restrict_robots` | Die Funktion &quot;Alle Roboter blockieren&quot;wurde aktiviert oder deaktiviert |
| `environment.update.smtp` | Der Versand von E-Mails wurde für eine Umgebung aktiviert oder deaktiviert. |
| `environment.variable.create` | Eine Variable wurde erstellt |
| `environment.variable.delete` | Eine Variable wurde gelöscht |
| `environment.variable.update` | Eine Variable wurde geändert |
| `project.domain.create` | Eine Domäne wurde erstellt und zum Projekt hinzugefügt |
| `project.domain.delete` | Eine dem Projekt zugeordnete Domäne wurde entfernt |
| `project.domain.update` | Eine dem Projekt zugeordnete Domäne wurde aktualisiert. |
