---
title: Einrichten des OpenSearch-Dienstes
description: Erfahren Sie, wie Sie den OpenSearch-Dienst für Adobe Commerce in der Cloud-Infrastruktur aktivieren.
feature: Cloud, Search, Services
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Einrichten des OpenSearch-Dienstes

Der Dienst [OpenSearch](https://www.opensearch.org) ist eine Open-Source-Abspaltung von Elasticsearch 7.10.2, die den Lizenzänderungen für Elasticsearch folgt. Siehe das [OpenSource-Projekt](https://github.com/opensearch-project) in GitHub.

{{elasticsearch-support}}

Mit OpenSearch können Sie Daten aus beliebigen Quellen und beliebigen Formaten aufnehmen und in Echtzeit suchen und visualisieren.

- Schnelle und erweiterte Suchen nach Produkten im Produktkatalog
- OpenSearch-Analyzer unterstützen mehrere Sprachen
- Unterstützt Stoppwörter und Synonyme
- Die Indizierung hat keine Auswirkungen auf Kunden, bis der Neuindizierungsvorgang abgeschlossen ist

{{service-instruction}}

>[!TIP]
>
>Adobe empfiehlt, OpenSearch immer für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur einzurichten, selbst wenn Sie ein Tool für die Drittanbietersuche für Ihre Adobe Commerce-Anwendung konfigurieren möchten. Das Einrichten von OpenSearch bietet eine Ausweichoption, wenn das Suchwerkzeug eines Drittanbieters fehlschlägt.

**So aktivieren Sie OpenSearch**:

1. Bei Integrationsumgebungen von Starter und Pro fügen Sie den Dienst `opensearch` der Datei `.magento/services.yaml` mit der entsprechenden Version und dem zugewiesenen Speicherplatz in MB hinzu. In diesem Fall ist Version 2 angemessen. Die Nebenversion ist nicht erforderlich, da die Cloud-Infrastruktur die neueste Version von OpenSearch verwendet.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   Für Pro-Projekte müssen Sie [ein Adobe Commerce-Supportticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die OpenSearch-Version in den Staging- und Produktionsumgebungen zu ändern.

1. Legen Sie die Eigenschaft `relationships` in der Datei `.magento.app.yaml` fest oder überprüfen Sie sie.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   Informationen dazu, wie sich diese Änderungen auf Ihre Umgebungen auswirken, finden Sie unter [Konfigurieren von Diensten](services-yaml.md).

1. Nachdem der Bereitstellungsprozess abgeschlossen ist, melden Sie sich mit SSH bei der Remote-Umgebung an.

   ```bash
   magento-cloud ssh
   ```

1. Indizieren Sie den Index der Katalogsuche neu.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Bereinigen Sie den Cache.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## OpenSearch-Softwarekompatibilität

Wenn Sie Adobe Commerce in einem Cloud-Infrastrukturprojekt installieren oder aktualisieren, prüfen Sie immer, ob die OpenSearch-Dienstversion mit dem [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php)-Client für Adobe Commerce kompatibel ist.

- **Erstmaliges Setup** - Vergewissern Sie sich, dass die in der Datei `services.yaml` angegebene OpenSearch-Version mit dem für Adobe Commerce konfigurierten OpenSearch-PHP-Client kompatibel ist.

- **Projekt-Upgrade**-Überprüfen Sie, ob der OpenSearch-PHP-Client in der neuen Anwendungsversion mit der in der Cloud-Infrastruktur installierten OpenSearch-Dienstversion kompatibel ist.

Die Unterstützung von Dienstversionen und Kompatibilität wird durch Versionen bestimmt, die in der Cloud-Infrastruktur getestet und bereitgestellt werden. Manchmal unterscheidet sich die Unterstützung von Versionen, die von lokalen Adobe Commerce-Implementierungen unterstützt werden. Eine Liste der unterstützten Versionen finden Sie unter [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im _Installationshandbuch_ .

**Überprüfen der Kompatibilität der OpenSearch-Software**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Zeigen Sie die OpenSearch-Details für die aktive Umgebung an.

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. Alternativ können Sie SSH verwenden, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Rufen Sie die Verbindungsdetails des OpenSearch-Dienstes ab.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   Suchen Sie in der Antwort die IP-Adresse und den Port für den Endpunkt des OpenSearch-Dienstes:

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. Rufen Sie den installierten OpenSearch-Dienst `version:number` vom Dienstendpunkt ab.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## Starten Sie den OpenSearch-Dienst neu

Wenn Sie den OpenSearch-Dienst neu starten müssen, müssen Sie sich an den Adobe Commerce-Support wenden.

## Zusätzliche Suchkonfiguration

- Standardmäßig wird die Suchkonfiguration für Cloud-Umgebungen bei jeder Bereitstellung neu generiert. Sie können die Variable &quot;`SEARCH_CONFIGURATION` deploy&quot;verwenden, um benutzerdefinierte Sucheinstellungen zwischen Implementierungen beizubehalten. Siehe [Bereitstellen von Variablen](../environment/variables-deploy.md#search_configuration).

- Nachdem Sie den OpenSearch-Dienst für Ihr Projekt eingerichtet haben, verwenden Sie die Admin-Benutzeroberfläche, um die OpenSearch-Verbindung zu testen und die OpenSearch-Einstellungen für Adobe Commerce anzupassen.

### Hinzufügen von Plug-ins für OpenSearch

Optional können Sie Plugins für OpenSearch hinzufügen, indem Sie den Abschnitt `configuration:plugins` zum OpenSearch-Dienst in der Datei `.magento/services.yaml` hinzufügen. Beispielsweise ermöglicht der folgende Code die Plug-ins für die ICU-Analyse und die Phonetic-Analyse.

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Weitere Informationen zu Plug-ins finden Sie im [OpenSearch-Projekt](https://github.com/opensearch-project) .

### Entfernen von Plug-ins für OpenSearch

Wenn Sie die Plug-in-Einträge aus dem Abschnitt `opensearch:` der Datei `.magento/services.yaml` entfernen, wird der Dienst **nicht** deinstalliert oder deaktiviert. Um den Dienst vollständig zu deaktivieren, müssen Sie Ihre OpenSearch-Daten neu indizieren, nachdem Sie die Plug-ins aus Ihrer `.magento/services.yaml` -Datei entfernt haben. Dieses Design verhindert den möglichen Verlust oder die Beschädigung von Daten, die von diesen Plug-ins abhängig sind.

**So entfernen Sie OpenSearch-Plug-ins**:

1. Entfernen Sie die OpenSearch-Plug-in-Einträge aus Ihrer `.magento/services.yaml` -Datei.
1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Binden Sie die `.magento/services.yaml`-Änderungen in Ihr Cloud-Repository ein.
1. Indizieren Sie den Index der Katalogsuche neu.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Bereinigen Sie den Cache.

   ```bash
   bin/magento cache:clean
   ```
