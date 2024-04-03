---
title: Implementierungen verfolgen
description: Erfahren Sie, wie Sie New Relic so konfigurieren, dass Bereitstellungen in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt verfolgt und Leistungsänderungen analysiert werden.
feature: Cloud, Deploy, Observability
topic: Performance
last-substantial-update: 2023-10-12T00:00:00Z
exl-id: 3d477a4b-ae5a-4c82-b71b-33ff24827b93
source-git-commit: cd9b541bd5b2fa342b76c992ab85a5115368313b
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Implementierungen verfolgen

Sie können die New Relic aktivieren _Änderungen verfolgen_ zur Überwachung von Implementierungsereignissen in Ihrem Commerce-Projekt in der Cloud-Infrastruktur.

Die Datenerfassung für Bereitstellungen hilft bei der Analyse der Auswirkungen von Implementierungsänderungen auf die Gesamtleistung, wie CPU, Speicher, Antwortzeit und mehr. Siehe [Verfolgen von Änderungen mit NerdGraph](https://docs.newrelic.com/docs/change-tracking/change-tracking-graphql/) im _New Relic-Dokumentation_.

>[!PREREQUISITES]
>
>- `NR_API_URL`: New Relic-API-Endpunkt, in diesem Fall NerdGraph-API-URL `https://api.newrelic.com/graphql`
>- `NR_API_KEY`: Erstellen Sie einen Benutzerschlüssel, siehe [New Relic-API-Schlüssel](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys) im _New Relic_ Dokumentation.
>- `NR_APP_GUID`: Eine Entität, die Daten an New Relic meldet, verfügt über eine eindeutige ID (GUID). Um beispielsweise in einer Staging-Umgebung zu aktivieren, passen Sie die Staging-Umgebung an `NR_APP_GUID` Cloud-Variable mit _Staging-Entität GUID_ aus New Relic. Siehe [Informationen zu New Relic-Entitäten](https://docs.newrelic.com/docs/new-relic-solutions/new-relic-one/core-concepts/what-entity-new-relic/) und [NerdGraph-Tutorial: Anzeigen von Entitätsdaten](https://docs.newrelic.com/docs/apis/nerdgraph/examples/nerdgraph-entities-api-tutorial/) im _New Relic_ Dokumentation.

## Implementierungen verfolgen aktivieren

Verfolgen Sie die Implementierungsereignisse Ihrer Commerce-Projekte in New Relic, indem Sie eine _script_ Integration.

**So aktivieren Sie die Tracking-Implementierungen**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Erstellen Sie eine `action-integration.js` -Datei. Kopieren Sie den folgenden Code und fügen Sie ihn in den `action-integration.js` Datei speichern:

   ```javascript
   function trackDeployments() {
     const envName = activity.payload.environment.name;
     let variables;
     activity.payload.deployment.variables.forEach(function(variable) {
       if (variable.name === "env:NR_CONFIG") {
         variables = variable.value;
       }
     });
     const config = JSON.parse(variables.replace(/'/g, '"'));
     const commitSha = activity.payload.commits ? activity.payload.commits[0].sha : activity.payload.environment.head_commit;
     const deploymentType = activity.type;
   
     if (!(envName in config)) {
       throw new Error('There is no configuration for ' + envName);
     }
   
     const configEnv = config[envName];
   
     if (!configEnv.NR_APP_GUID || !configEnv.NR_API_KEY || !configEnv.NR_API_URL) {
       throw new Error('You must define the next configuation in the env variable NR_CONFIG: NR_APP_GUID, NR_API_KEY and NR_API_URL');
     }
   
     const query = `mutation {
       changeTrackingCreateDeployment(
       deployment: {
           version: "${commitSha}",
           entityGuid: "${configEnv.NR_APP_GUID}",
           commit: "${commitSha}",
           changelog: "${deploymentType}"
       }
       ) {
         deploymentId
         entityGuid
       }
     }`;
   
     var resp = fetch(configEnv.NR_API_URL, {
       method: 'POST',
       headers: {
           'Content-Type': 'application/json',
           'API-Key': configEnv.NR_API_KEY
       },
       body: JSON.stringify({
           query
       })
     });
   
     if (!resp.ok) {
       console.log('Sending new relic change tracking failed: ' + resp.text());
     } else {
       console.log(resp.text());
     }
   }
   
   trackDeployments();
   ```

1. Erstellen Sie eine _script_ Integration mithilfe der `magento-cloud` CLI-Befehl und -Verweis `action-integration.js` -Datei.

   ```bash
   magento-cloud integration:add --type script --events='environment.restore, environment.push, environment.branch, environment.activate, environment.synchronize, environment.initialize, environment.merge, environment.redeploy, environment.variable.create, environment.variable.delete, environment.variable.update' --file ./action-integration.js --project=<YOUR_PROJECT_ID> --environments=<YOUR_ENVIRONMENT_ID>
   ```

   Beispielantwort:

   ```terminal
   Created integration 767u4hathojjw (type: script)
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Property              | Value                                                                                                                                   |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | 767u4hathojjw                                                                                                                           |
   | type                  | script                                                                                                                                  |
   | role                  |                                                                                                                                         |
   | events                | - environment.restore                                                                                                                   |
   |                       | - environment.push                                                                                                                      |
   |                       | - environment.branch                                                                                                                    |
   |                       | - environment.activate                                                                                                                  |
   |                       | - environment.synchronize                                                                                                               |
   |                       | - environment.initialize                                                                                                                |
   |                       | - environment.merge                                                                                                                     |
   |                       | - environment.redeploy                                                                                                                  |
   |                       | - environment.variable.create                                                                                                           |
   |                       | - environment.variable.delete                                                                                                           |
   |                       | - environment.variable.update                                                                                                           |
   | environments          | - staging                                                                                                                               |
   |                       | - production                                                                                                                            |
   | excluded_environments | {  }                                                                                                                                    |
   | states                | - complete                                                                                                                              |
   | result                | *                                                                                                                                       |
   | script                | function variables() {                                                                                                                  |
   |                       |     var vars = {};                                                                                                                      |
   |                       |     activity.payload.deployment.variables.forEach(function(variable) {                                                                  |
   |                       |         vars[variable.name] = variable.value;                                                                                           |
   |                       |     });                                                                                                                                 |
   |                       |     return vars;                                                                                                                        |
   |                       | }                                                                                                                                       |
   |                       |                                                                                                                                         |
   |                       | function trackDeployments() {                                                                                                           |
   |                       |     const envName = activity.payload.environment.name;                                                                                  |
   |                       |                                                                                                                                         |
   |                       |     const config = JSON.parse(variables()['env:NR_CONFIG'].replace(/'/g, '"'));                                                         |
   |                       |     const commitSha = activity.payload.commits ? activity.payload.commits[0].sha : activity.payload.environment.head_commit;            |
   |                       |     const deploymentType = activity.type;                                                                                               |
   |                       |                                                                                                                                         |
   |                       |     if (!(envName in config)) {                                                                                                         |
   |                       |         throw new Error('There is no configuration for ' + envName);                                                                    |
   |                       |     }                                                                                                                                   |
   |                       |                                                                                                                                         |
   |                       |     const configEnv = config[envName];                                                                                                  |
   |                       |                                                                                                                                         |
   |                       |     if (!configEnv.NR_APP_GUID || !configEnv.NR_API_KEY || !configEnv.NR_API_URL) {                                                     |
   |                       |         throw new Error('You must define the next configuation in the env variable NR_CONFIG: NR_APP_GUID, NR_API_KEY and NR_API_URL'); |
   |                       |     }                                                                                                                                   |
   |                       |                                                                                                                                         |
   |                       |     const query = `mutation {                                                                                                           |
   |                       |         changeTrackingCreateDeployment(                                                                                                 |
   |                       |           deployment: {                                                                                                                 |
   |                       |             version: "${commitSha}",                                                                                                    |
   |                       |             entityGuid: "${configEnv.NR_APP_GUID}",                                                                                     |
   |                       |             commit: "${commitSha}",                                                                                                     |
   |                       |             changelog: "${deploymentType}"                                                                                              |
   |                       |           }                                                                                                                             |
   |                       |         ) {                                                                                                                             |
   |                       |           deploymentId                                                                                                                  |
   |                       |           entityGuid                                                                                                                    |
   |                       |         }                                                                                                                               |
   |                       |     }`;                                                                                                                                 |
   |                       |                                                                                                                                         |
   |                       |     var resp = fetch(configEnv.NR_API_URL, {                                                                                            |
   |                       |         method: 'POST',                                                                                                                 |
   |                       |         headers: {                                                                                                                      |
   |                       |             'Content-Type': 'application/json',                                                                                         |
   |                       |             'API-Key': configEnv.NR_API_KEY                                                                                             |
   |                       |         },                                                                                                                              |
   |                       |         body: JSON.stringify({                                                                                                          |
   |                       |             query                                                                                                                       |
   |                       |         })                                                                                                                              |
   |                       |     });                                                                                                                                 |
   |                       |                                                                                                                                         |
   |                       |     if (!resp.ok) {                                                                                                                     |
   |                       |         console.log('Sending new relic change tracking failed: ' + resp.text());                                                        |
   |                       |     } else {                                                                                                                            |
   |                       |         console.log(resp.text());                                                                                                       |
   |                       |     }                                                                                                                                   |
   |                       | }                                                                                                                                       |
   |                       |                                                                                                                                         |
   |                       | trackDeployments();                                                                                                                     |
   |                       |                                                                                                                                         |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   ```

1. Notieren Sie sich die Integrations-ID zur späteren Verwendung. In diesem Beispiel lautet die ID:

   ```terminal
   Created integration 767u4hathojjw (type: script)
   ```

   Optional können Sie die Integration überprüfen und die Integrations-ID wie folgt feststellen: `magento-cloud integration:list`

1. Erstellen Sie die Umgebungsvariable unter Verwendung der Voraussetzungen.

   ```bash
   magento-cloud variable:create --level project --name=env:NR_CONFIG --value='{"<YOUR_ENVIRONMENT_ID>":{"NR_API_KEY": "<YOUR_API_KEY>", "NR_API_URL": "https://api.newrelic.com/graphql", "NR_APP_GUID":"<YOUR_APP_GUID>"}}'  -p <YOUR_PROJECT_ID>
   ```

1. Überprüfen Sie das letzte Aktivitätsprotokoll.

   ```bash
   magento-cloud integration:activity:log <INTEGRATION_ID> -p <YOUR_PROJECT_ID> -e <YOUR_ENVIRONMENT_ID>
   ```

   Antwort:

   ```terminal
   Integration ID: 767u4hathojjw
   Activity ID: poxqidsfajkmg
   Type: integration.script
   Description: Running activity script
   Created: 2023-08-28T20:32:02+00:00
   State: complete
   Log:
   HTTP request
   HTTP response
   {"data":{"changeTrackingCreateDeployment":{"deploymentId":"some-deployment-id","entityGuid":"SomeGUIDhere"}}}
   ```

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login).

1. Klicken Sie im Explorer-Navigationsmenü auf **[!UICONTROL APM & Services]**. Umgebung auswählen [!UICONTROL Name] und [!UICONTROL Account].

1. under _Veranstaltungen_ klicken **[!UICONTROL Change tracking]**.

   ![Bereitstellungen](../../assets/new-relic/deployments.png)
