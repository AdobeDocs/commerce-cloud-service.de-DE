---
title: Elasticsearch-Dienst einrichten
description: Erfahren Sie, wie Sie den Elasticsearch-Dienst für Adobe Commerce in der Cloud-Infrastruktur aktivieren.
feature: Cloud, Search, Services
exl-id: ac559cbb-342a-4756-ade5-49eba4827965
source-git-commit: 8147b43b26370d9305c3c7dc47865ddcbae1904d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Elasticsearch-Dienst einrichten

[Elasticsearch](https://www.elastic.co) ist ein Open-Source-Produkt, mit dem Sie Daten aus beliebigen Quellen aufnehmen, in beliebigen Formaten suchen und in Echtzeit visualisieren können.

{{elasticsearch-support}}

Informationen zur Adobe Commerce-Version 2.4.4 und höher finden Sie unter [Einrichten des OpenSearch-Dienstes](opensearch.md).

- Elasticsearch führt schnelle und erweiterte Suchen nach Produkten im Produktkatalog durch
- Elasticsearch Analytics unterstützt mehrere Sprachen
- Unterstützt Stoppwörter und Synonyme
- Die Indizierung hat keine Auswirkungen auf Kunden, bis der Neuindizierungsvorgang abgeschlossen ist

>[!TIP]
>
>Adobe empfiehlt, immer Elasticsearch für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur einzurichten, selbst wenn Sie ein Tool für die Drittanbietersuche für Ihre Adobe Commerce-Anwendung konfigurieren möchten. Das Einrichten von Elasticsearch bietet eine Ausweichoption für den Fall, dass das Suchwerkzeug eines Drittanbieters fehlschlägt.

{{service-instruction}}

**So aktivieren Sie Elasticsearch**:

1. Fügen Sie bei Starterprojekten den Dienst `elasticsearch` zur Datei `.magento/services.yaml` hinzu, wobei die Elasticsearch-Version und der zugewiesene Speicherplatz in MB vorhanden sind.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   Für Pro-Projekte müssen Sie ein Adobe Commerce-Supportticket senden, um die Elasticsearch-Version in den Staging- und Produktionsumgebungen zu ändern.

1. Legen Sie die Eigenschaft `relationships` in der Datei `.magento.app.yaml` fest.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   Informationen dazu, wie sich diese Änderungen auf Ihre Umgebungen auswirken, finden Sie unter [Dienste](services-yaml.md).

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

## Elasticsearch-Softwarekompatibilität

Wenn Sie Adobe Commerce in einem Cloud-Infrastrukturprojekt installieren oder aktualisieren, prüfen Sie immer, ob die Elasticsearch-Dienstversion mit dem [Elasticsearch PHP](https://github.com/elastic/elasticsearch-php)-Client für Adobe Commerce kompatibel ist.

- **Erstmaliges Setup** - Vergewissern Sie sich, dass die in der Datei `services.yaml` angegebene Elasticsearch-Version mit dem für Adobe Commerce konfigurierten Elasticsearch-PHP-Client kompatibel ist.

- **Projektaktualisierung** - Überprüfen Sie, ob der Elasticsearch-PHP-Client in der neuen Anwendungsversion mit der in der Cloud-Infrastruktur installierten Elasticsearch-Dienstversion kompatibel ist.

Die Unterstützung von Dienstversionen und Kompatibilität für Adobe Commerce in der Cloud-Infrastruktur wird durch Versionen bestimmt, die in der Cloud-Infrastruktur bereitgestellt werden. Manchmal unterscheidet sich die Unterstützung von Versionen, die von lokalen Adobe Commerce-Implementierungen unterstützt werden. Siehe [Dienstversionen](services-yaml.md#service-versions).

**Überprüfen der Kompatibilität der Elasticsearch-Software**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Zeigen Sie die Details des Elasticsearchs für die aktive Umgebung an.

   ```bash
   magento-cloud relationships --property=elasticsearch
   ```

1. Alternativ können Sie SSH verwenden, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Überprüfen Sie die Composer-Paketversion auf `elasticsearch/elasticsearch`.

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   Überprüfen Sie in der Antwort die installierte Version in der Eigenschaft `versions` .

   ```terminal
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v7.17.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org/licenses/Apache-2.0.html#licenseText
   license  : GNU Lesser General Public License v2.1 only (LGPL-2.1-only) (OSI approved) https://spdx.org/licenses/LGPL-2.1-only.html#licenseText
   homepage :
   source   : [git] git@github.com:elastic/elasticsearch-php.git f1b8918f411b837ce5f6325e829a73518fd50367
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/f1b8918f411b837ce5f6325e829a73518fd50367 f1b8918f411b837ce5f6325e829a73518fd50367
   path     : ~/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   Außerdem finden Sie die Elasticsearch-PHP-Clientversion in der Datei `composer.lock` im Stammverzeichnis der Umgebung.

1. Rufen Sie in der Befehlszeile die Verbindungsdetails des Elasticsearch-Diensts ab.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   Suchen Sie in der Antwort die IP-Adresse für den Elasticsearch-Dienst-Endpunkt:

   ```terminal
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. Rufen Sie den installierten Elasticsearch-Dienst `version:number` vom Dienstendpunkt ab.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```terminal
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Überprüfen Sie die Versionskompatibilität zwischen dem Elasticsearch-Dienst und dem PHP-Client.

   Wenn die Versionen inkompatibel sind, nehmen Sie eine der folgenden Aktualisierungen an Ihrer Umgebungskonfiguration vor:

   - Ändern Sie den Elasticsearch-PHP-Client in eine Version, die mit der Elasticsearch-Dienstversion kompatibel ist.

     ```bash
     composer require "elasticsearch/elasticsearch:~<version>"
     ```

   - Ändern Sie die Version des Elasticsearch-Diensts in der Datei `services.yaml` in eine Version, die mit dem Elasticsearch-PHP-Client kompatibel ist.

     {{pro-update-service}}

## Elasticsearch-Dienst neu starten

Wenn Sie den Dienst [Elasticsearch](https://www.elastic.co) neu starten müssen, müssen Sie sich an den Adobe Commerce-Support wenden.

## Zusätzliche Suchkonfiguration

- Standardmäßig wird die Suchkonfiguration für Cloud-Umgebungen bei jeder Bereitstellung neu generiert. Sie können die Variable &quot;`SEARCH_CONFIGURATION` deploy&quot;verwenden, um benutzerdefinierte Sucheinstellungen zwischen Implementierungen beizubehalten. Siehe [Bereitstellen von Variablen](../environment/variables-deploy.md#search_configuration).

- Nachdem Sie den Projektdienst für Ihr Elasticsearch eingerichtet haben, verwenden Sie die Administrator-Benutzeroberfläche, um die Elasticsearch-Verbindung zu testen und die Elasticsearch-Einstellungen für Adobe Commerce anzupassen.

### Hinzufügen von Plug-ins für Elasticsearch

Optional können Sie Plugins für Elasticsearch hinzufügen, indem Sie den Abschnitt `configuration:plugins` zum Elasticsearch-Dienst in der Datei `.magento/services.yaml` hinzufügen. Beispielsweise ermöglicht der folgende Code die Plug-ins für die ICU-Analyse und die Phonetic-Analyse.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Wenn Sie das Drittanbieter-Plug-in der Elastic Suite verwenden, müssen Sie [das `ece-tools` -Paket](../dev-tools/update-package.md) auf Version 2002.0.19 oder höher aktualisieren.
Fügen Sie beim Einrichten der Elastic Suite die Konfigurationseinstellungen zur Variablen &quot;`ELASTICSUITE_CONFIGURATION` deploy&quot;hinzu. Mit dieser Konfiguration werden die Einstellungen über verschiedene Bereitstellungen hinweg gespeichert.

### Entfernen von Plug-ins für Elasticsearch

Wenn Sie die Plug-in-Einträge aus `elasticsearch:` in `.magento/services.yaml` entfernen, werden sie nicht wie erwartet deinstalliert oder deaktiviert. Sie müssen Ihre Elasticsearch-Daten neu indizieren. Dieses Verhalten soll verhindern, dass Daten, die von diesen Plug-ins abhängen, verloren gehen oder beschädigt werden.

**So entfernen Sie Elasticsearch-Plug-ins**:

1. Entfernen Sie die Elasticsearch-Plug-in-Einträge aus Ihrer `.magento/services.yaml` -Datei.
1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Vergeben Sie die Änderungen an `.magento/services.yaml` in Ihr Cloud-Repository.
1. Indizieren Sie den Index der Katalogsuche neu.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Bereinigen Sie den Cache.

   ```bash
   bin/magento cache:clean
   ```

>[!TIP]
>
>Weitere Informationen zur Verwendung oder Fehlerbehebung des Elastic Suite-Plug-ins mit Adobe Commerce finden Sie in der [Dokumentation zur Elastic Suite](https://github.com/Smile-SA/elasticsuite).

## Fehlerbehebung

In den folgenden Adobe Commerce-Supportartikeln finden Sie Hilfe zur Fehlerbehebung bei Problemen mit Elasticsearch:

- [Elasticsearch 5 ist konfiguriert, die Suchseite wird jedoch nicht mit dem Fehler &quot;Felddaten sind deaktiviert...&quot;geladen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html).
- [Die Katalogpaginierung funktioniert nicht, wenn Elasticsearch 6.x verwendet wird](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/catalog-pagination-doesn-t-work-when-elasticsearch-6.x-is-used.html)
- [Elasticsearch in Adobe Commerce-Fehlerbehebung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-in-magento-troubleshooter.html)
- [Elasticsearch-Indexstatus ist `yellow` oder `red`](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-index-status-is-yellow-or-red.html)
