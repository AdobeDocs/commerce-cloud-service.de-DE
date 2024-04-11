---
title: Bereitstellen von Variablen
description: Siehe die Liste der Umgebungsvariablen, die Aktionen in der Adobe Commerce-Bereitstellungsphase der Cloud-Infrastruktur steuern.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: b7307faf046884c13cba852df69d4fa9977e9a17
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Bereitstellen von Variablen

Die folgenden _deploy_ -Variablen steuern -Aktionen in der Bereitstellungsphase und können Werte von der [Globale Variablen](variables-global.md). Fügen Sie diese Variablen in die `deploy` der `.magento.env.yaml` Datei:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Weitere Informationen zum Anpassen des Build- und Bereitstellungsprozesses finden Sie unter

- [Bereitstellungskonfiguration](configure-env-yaml.md)
- [Bereitstellungsprozess](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Konfigurieren Sie die Seite &quot;Redis&quot;und die standardmäßige Zwischenspeicherung. Wenn Sie `cm_cache_backend_redis` -Parameter angeben, müssen Sie die `server`, `port`, und `database` Optionen.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

Im folgenden Beispiel werden neue Werte zu einer vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

Im folgenden Beispiel wird die [Funktion zum Vorausfüllen umkehren](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) wie in _Konfigurationshandbuch_:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

So verwenden Sie eine benutzerdefinierte [REDIS_BACKEND](#redis_backend) -Modell (nicht nur aus der Zulassungsliste) festlegen, legen Sie die `_custom_redis_backend` -Option `true` um die korrekte Validierung zu aktivieren, wie im folgenden Beispiel gezeigt:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivierung oder Deaktivierung der Reinigung [statische Inhaltsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) während der Build- oder Bereitstellungsphase generiert wurde. Standardwert verwenden _true_ in der Entwicklung als Best Practice.

- **`true`**—Entfernt alle vorhandenen statischen Inhalte vor der Bereitstellung des aktualisierten statischen Inhalts.
- **`false`**—Die Bereitstellung überschreibt nur vorhandene statische Inhaltsdateien, wenn der generierte Inhalt eine neuere Version enthält.

Wenn Sie statischen Inhalt über einen separaten Prozess ändern, setzen Sie den Wert auf _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Wenn statische Ansichtsdateien vor der Bereitstellung nicht bereinigt werden, kann dies zu Problemen führen, wenn Sie Aktualisierungen für vorhandene Dateien bereitstellen, ohne die vorherigen Versionen zu entfernen. Aufgrund von [Fallback statischer Dateien](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) Regeln verwenden, können Fallback-Vorgänge die falsche Datei anzeigen, wenn das Verzeichnis mehrere Versionen derselben Datei enthält.

## `CRON_CONSUMERS_RUNNER`

- **Standard**—`cron_run = false`, `max_messages = 1000`
- **Version**—Adobe Commerce 2.2.0 und höher

Verwenden Sie diese Umgebungsvariable, um sicherzustellen, dass Nachrichtenwarteschlangen nach einer Bereitstellung ausgeführt werden.

- `cron_run`—Ein boolean -Wert, der die `consumers_runner` Cron-Auftrag (Standard = `false`).
- `max_messages`—Eine Zahl, die die maximale Anzahl von Nachrichten angibt, die jeder Verbraucher vor dem Beenden verarbeiten muss (Standard = `1000`). Sie können den Wert auf `0` , um zu verhindern, dass der Verbraucher kündigt.
- `consumers`—Ein Array von Zeichenfolgen, die angeben, welche Verbraucher ausgeführt werden sollen. Ein leeres Array wird ausgeführt _all_ Verbraucher.

- `multiple_processes`-Eine Zahl, die die Anzahl der Prozesse angibt, die für jeden Verbraucher erzeugt werden sollen. In Commerce unterstützt **2,4,4** oder höher.

>[!NOTE]
>
>So geben Sie eine Liste der Nachrichtenwarteschlangen zurück `consumers`, führen Sie die `./bin/magento queue:consumers:list` in der Remote-Umgebung.

Beispiel für ein Array, das spezifisch ausgeführt wird `consumers` und `multiple_processes` für jeden Verbraucher zu laichen:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Beispiel für ein leeres Array, das alle `consumers`:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Standardmäßig überschreibt der Bereitstellungsprozess alle Einstellungen im `env.php` -Datei. Siehe [Verwalten von Nachrichtenwarteschlangen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) im _Commerce-Konfigurationshandbuch_ für Adobe Commerce vor Ort.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.2.0 und höher

Konfigurieren der `consumers` Verarbeiten Sie Nachrichten aus der Nachrichtenwarteschlange, indem Sie eine der folgenden Optionen auswählen:

- `false`—`Consumers` verarbeitet verfügbare Nachrichten in der Warteschlange, schließt die TCP-Verbindung und beendet sie. `Consumers` nicht warten, bis zusätzliche Nachrichten in die Warteschlange gelangen, selbst wenn die Anzahl der verarbeiteten Nachrichten kleiner ist als die Anzahl der `max_messages` Wert, der in der Variablen `CRON_CONSUMERS_RUNNER` Bereitstellungsvariable.

- `true`—`Consumers` weiterhin Nachrichten aus der Nachrichtenwarteschlange verarbeiten, bis die maximale Nachrichtenanzahl erreicht ist (`max_messages`), die in der Variablen `CRON_CONSUMERS_RUNNER` -Variable bereitstellen, bevor die TCP-Verbindung geschlossen und der Verbraucherprozess beendet wird. Wenn die Warteschlange vor dem Erreichen geleert wird `max_messages`, wartet der Verbraucher auf das Eintreffen weiterer Nachrichten.

>[!WARNING]
>
>Wenn Sie Sekundäre zum Ausführen verwenden `consumers` Setzen Sie diese Variable auf &quot;true&quot;, anstatt einen Cron-Auftrag zu verwenden.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

>[!WARNING]
>
>Legen Sie die `CRYPT_KEY` Wert durch [!DNL Cloud Console] anstelle der `.magento.env.yaml` -Datei, um zu vermeiden, dass der Schlüssel im Quellcode-Repository für Ihre Umgebung verfügbar wird. Siehe [Festlegen von Umgebungs- und Projektvariablen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

Wenn Sie die Datenbank ohne Installationsprozess von einer Umgebung in eine andere verschieben, benötigen Sie die entsprechenden kryptografischen Informationen. Adobe Commerce verwendet den in der Variablen [!DNL Cloud Console] als `crypt/key` Wert in `env.php` -Datei.

## `DATABASE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Wenn Sie eine Datenbank im [Beziehungseigenschaft](../application/properties.md#relationships) des `.magento.app.yaml` -Datei, können Sie Ihre Datenbankverbindungen für die Bereitstellung anpassen.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

Im folgenden Beispiel werden neue Werte zu einer vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

Außerdem können Sie ein Tabellenpräfix konfigurieren.

>[!WARNING]
>
>Wenn Sie die Zusammenführungsoption nicht mit dem Tabellenpräfix verwenden, müssen Sie die standardmäßigen Verbindungseinstellungen angeben oder die Bereitstellung schlägt bei der Validierung fehl.

Im folgenden Beispiel wird die `ece_` Tabellenpräfix mit Standardverbindungseinstellungen anstelle der Verwendung von `_merge` Option:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Beispielausgabe:

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.2.0 und höher

Behebt benutzerspezifische Inhalte bei [!DNL Elastic Suite] Diensteinstellungen zwischen -Implementierungen und verwendet sie im Abschnitt &quot;system/default/smile_elasticsuite_core_base_settings&quot;des Hauptteils [!DNL Elastic Suite] Konfiguration. Wenn die Variable [!DNL Elastic Suite] Das Composer-Paket wird installiert und automatisch konfiguriert.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

Im folgenden Beispiel wird ein neuer Wert mit der vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Bekannte Einschränkungen**:

- Ändern der Suchmaschine in einen anderen Typ als `elasticsuite` verursacht einen Bereitstellungsfehler, dem ein entsprechender Validierungsfehler beigefügt ist
- Das Entfernen des Elasticsearch-Dienstes führt zu einem Bereitstellungsfehler zusammen mit einem entsprechenden Validierungsfehler

>[!NOTE]
>
>Weitere Informationen zur Verwendung von oder Fehlerbehebung bei der [!DNL Elastic Suite] Plug-in mit Adobe Commerce, siehe [[!DNL Elastic Suite] Dokumentation](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 und höher

Aktiviert und deaktiviert Google Analytics bei der Bereitstellung in Staging- und Integrationsumgebungen. Standardmäßig gilt Google Analytics nur für die Produktionsumgebung. Setzen Sie diesen Wert auf `true` , um Google Analytics in den Staging- und Integrationsumgebungen zu aktivieren.

- **`true`**—Aktiviert Google Analytics in Staging- und Integrationsumgebungen.
- **`false`**—Deaktiviert Google Analytics in Staging- und Integrationsumgebungen.

Fügen Sie die `ENABLE_GOOGLE_ANALYTICS` Umgebungsvariable auf `deploy` im Abschnitt `.magento.env.yaml` Datei:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Der Bereitstellungsprozess aktiviert immer Google Analytics in Produktionsumgebungen.

## `FORCE_UPDATE_URLS`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 und höher

Bei der Bereitstellung in der Pro- oder Starter-Staging- und Produktionsumgebung ersetzt diese Variable die Adobe Commerce-Basis-URLs in der Datenbank durch die Projekt-URLs, die von der [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) -Variable. Verwenden Sie diese Einstellung, um das Standardverhalten der [UPDATE_URLS](#update_urls) Bereitstellungsvariable, die bei der Bereitstellung in Staging- oder Produktionsumgebungen ignoriert wird.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Standard**—`file`
- **Version**—Adobe Commerce 2.2.5 und höher

Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. Verwenden Sie die `file` Anbieter in der Produktionsumgebung sperren. Starterumgebungen und die Pro-Integrationsumgebung verwenden nicht die [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) -Variable, also `ece-tools` wendet die `db` Anbieter automatisch sperren.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Siehe [Schloss konfigurieren](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) im _Installationshandbuch_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 und höher

>[!TIP]
>
>Die `MYSQL_USE_SLAVE_CONNECTION` wird nur in Adobe Commerce in Cloud-Infrastruktur-Staging- und Produktions-Pro-Cluster-Umgebungen unterstützt und nicht in Starter-Projekten.

Adobe Commerce kann mehrere Datenbanken asynchron lesen. Legen Sie `true` zur automatischen Verwendung von _schreibgeschützt_ Verbindung zur Datenbank, um schreibgeschützten Traffic auf einem Nicht-Master-Knoten zu empfangen. Diese Verbindung verbessert die Leistung durch Lastenausgleich, da nur ein Knoten Lese- und Schreibvorgänge-Traffic verarbeitet. Legen Sie `false` , um ein vorhandenes schreibgeschütztes Verbindungs-Array aus dem `env.php` -Datei.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Wenn die Variable `MYSQL_USE_SLAVE_CONNECTION` festgelegt ist auf `true`, die `synchronous_replication` -Parameter auf `true` standardmäßig im `env.php` -Datei in Pro Staging- und Produktionsumgebungen. Wenn die Variable `MYSQL_USE_SLAVE_CONNECTION` auf `false`, die `synchronous_replication` -Parameter nicht konfiguriert ist.

## `QUEUE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Verwenden Sie diese Umgebungsvariable, um zwischen Bereitstellungen benutzerdefinierte AMQP-Diensteinstellungen beizubehalten. Wenn Sie beispielsweise einen vorhandenen Nachrichtenwarteschlangendienst verwenden möchten, anstatt die Cloud-Infrastruktur für Sie zu verwenden, verwenden Sie die `QUEUE_CONFIGURATION` Umgebungsvariable, um sie mit Ihrer Site zu verbinden:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

Im folgenden Beispiel werden neue Werte zu einer vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Standard**—`Cm_Cache_Backend_Redis`
- **Version**—Adobe Commerce 2.3.0 und höher

Gibt die Backend-Modellkonfiguration für den Redis-Cache an.

Adobe Commerce Version 2.3.0 und höher umfasst die folgenden Backend-Modelle:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

Das Beispiel für das Festlegen von `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Wenn Sie `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` als Redis-Backend-Modell zur Aktivierung von [L2-Cache](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html), `ece-tools` generiert automatisch die Cachekonfiguration. Beispiel anzeigen [Konfigurationsdatei](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) im _Adobe Commerce-Konfigurationshandbuch_. Um die generierte Cache-Konfiguration zu überschreiben, verwenden Sie die [CACHE_CONFIGURATION](#cache_configuration) Bereitstellungsvariable.

## `REDIS_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.16 und höher

>[!WARNING]
>
>Do _not_ Aktivieren Sie diese Variable auf einer [skalierte Architektur](../architecture/scaled-architecture.md) Projekt. Dies führt zu Redis-Verbindungsfehlern. Redis Slaves sind noch aktiv, werden aber nicht für Redis-Lesevorgänge verwendet. Alternativ empfiehlt Adobe die Verwendung von Adobe Commerce 2.3.5 oder höher, eine neue Redis-Backend-Konfiguration zu implementieren und die L2-Zwischenspeicherung für Redis zu implementieren.

>[!TIP]
>
>Die `REDIS_USE_SLAVE_CONNECTION` wird nur in Adobe Commerce in Cloud-Infrastruktur-Staging- und Produktions-Pro-Cluster-Umgebungen unterstützt und nicht in Starter-Projekten.

Adobe Commerce kann mehrere Redis-Instanzen asynchron lesen. Legen Sie `true` zur automatischen Verwendung von _schreibgeschützt_ Verbindung zu einer Redis-Instanz, um schreibgeschützten Traffic auf einem Nicht-Master-Knoten zu empfangen. Diese Verbindung verbessert die Leistung durch Lastenausgleich, da nur ein Knoten Lese- und Schreibvorgänge-Traffic verarbeitet. Legen Sie `false` , um ein vorhandenes schreibgeschütztes Verbindungs-Array aus dem `env.php` -Datei.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Sie müssen den Redis-Dienst im `.magento.app.yaml` und in der `services.yaml` -Datei.

[ECE-Tools, Version 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) und verwendet später fehlertolerantere Einstellungen. Wenn Adobe Commerce keine Daten aus den Redizes lesen kann _Slave_ -Instanz dann liest sie Daten aus den Redis _master_ -Instanz.

Die schreibgeschützte Verbindung kann nicht in der Integrationsumgebung verwendet werden oder wenn Sie die [`CACHE_CONFIGURATION` Variable](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **Standard**—Nicht festgelegt
- **Version**—Adobe Commerce 2.1.4 und höher

Ordnet einen Ressourcennamen einer Datenbankverbindung zu. Diese Konfiguration entspricht dem `resource` Abschnitt `env.php` -Datei.

{{merge-options}}

Im folgenden Beispiel werden neue Werte zu einer vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Standard**—`4`
- **Version**—Adobe Commerce 2.1.4 und höher

Gibt an, [gzip](https://www.gnu.org/software/gzip) Komprimierungsstufe (`0` nach `9`) für die Komprimierung von statischem Inhalt; `0` Deaktiviert die Komprimierung.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standard**—`600`
- **Version**—Adobe Commerce 2.1.4 und höher

Wenn die zum Komprimieren der statischen Assets benötigte Zeit das Zeitlimit für die Komprimierung überschreitet, wird der Bereitstellungsprozess unterbrochen. Legen Sie die maximale Ausführungszeit in Sekunden für den Befehl zur statischen Inhaltskomprimierung fest.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Sie können mehrere Gebietsschemata pro Design konfigurieren. Diese Anpassung beschleunigt den Implementierungsprozess, indem die Anzahl unnötiger Designdateien verringert wird. Beispielsweise können Sie die _Magento/Backend_ Thema auf Englisch und ein benutzerdefiniertes Thema in anderen Sprachen.

Im folgenden Beispiel wird die `Magento/backend` Design mit drei Gebietsschemata:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Außerdem können Sie _not_ Bereitstellen eines Designs:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.2.0 und höher

Ermöglicht Ihnen, die maximale erwartete Ausführungszeit für die Bereitstellung statischer Inhalte zu erhöhen.

Standardmäßig wird von Adobe Commerce die maximal erwartete Ausführung auf 900 Sekunden festgelegt. In einigen Szenarien benötigen Sie jedoch möglicherweise mehr Zeit, um die Bereitstellung statischer Inhalte für ein Cloud-Projekt abzuschließen.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.4.2 und höher

Legen Sie in der Bereitstellungsphase `SCD_NO_PARENT: true` damit statische Inhalte für übergeordnete Designs nicht während der Bereitstellungsphase generiert werden. Diese Einstellung minimiert die Bereitstellungszeit und verhindert Site-Ausfallzeiten, die auftreten können, wenn der statische Inhaltserstellung während der Bereitstellung fehlschlägt. Siehe [Statische Inhaltsbereitstellung](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Standard**—`quick`
- **Version**—Adobe Commerce 2.2.0 und höher

Ermöglicht Ihnen die Anpassung der [Implementierungsstrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) für statischen Inhalt. Siehe [Bereitstellen von statischen Ansichtsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Verwenden Sie diese Optionen _only_ wenn Sie mehr als ein Gebietsschema haben:

- `standard`—stellt alle statischen Ansichtsdateien für alle Pakete bereit.
- `quick`—(_default_) minimiert die Bereitstellungszeit.
- `compact`—speichert Speicherplatz auf dem Server. In Adobe Commerce Version 2.2.4 und früher überschreibt diese Einstellung den Wert für `scd_threads` mit dem Wert `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standard**—Automatisch
- **Version**—Adobe Commerce 2.1.4 und höher

Legt die Anzahl der Threads für die Bereitstellung statischer Inhalte fest. Der Standardwert wird basierend auf der erkannten CPU-Thread-Anzahl festgelegt und überschreitet nicht den Wert 4. Durch die Erhöhung der Thread-Anzahl wird die Bereitstellung statischer Inhalte beschleunigt, und die Verringerung der Thread-Anzahl verlangsamt die Bereitstellung. Sie können den Thread-Wert festlegen, beispielsweise:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Verwenden Sie zur weiteren Verkürzung der Bereitstellungszeit [Konfigurationsverwaltung](../store/store-settings.md) mit dem `scd-dump` -Befehl, um die statische Bereitstellung in die Build-Phase zu verschieben.

## `SEARCH_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Verwenden Sie diese Umgebungsvariable, um benutzerdefinierte Suchdiensteinstellungen zwischen -Implementierungen beizubehalten. Beispiel:

Elasticsearch-Konfiguration:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_hostname: http://elasticsearch.internal
      elasticsearch_server_port: '9200'
      elasticsearch_index_prefix: magento2
      elasticsearch_server_timeout: '15'
```

OpenSearch-Konfiguration (für Commerce 2.4.6 und höher):

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: opensearch
      opensearch_server_hostname: 'http://opensearch.internal'
      opensearch_server_port: '9200'
      opensearch_index_prefix: 'magento2'
      opensearch_server_timeout: '15'
```

{{merge-options}}

Im folgenden Beispiel wird ein neuer Wert mit der vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Konfigurieren des Sitzungsspeichers für Redis. Erfordert die `save`, `redis`, `host`, `port`, und `database` Optionen für die Sitzungsspeichervariable. Beispiel:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

Im folgenden Beispiel wird ein neuer Wert mit der vorhandenen Konfiguration zusammengeführt:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Standard**— _Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Legen Sie `true` Überspringen der Bereitstellung statischer Inhalte während der Bereitstellungsphase.

Legen Sie in der Bereitstellungsphase `SKIP_SCD: true` damit der statische Inhaltserstellung während der Bereitstellungsphase nicht erfolgt. Diese Einstellung minimiert die Bereitstellungszeit und verhindert Site-Ausfallzeiten, die auftreten können, wenn der statische Inhaltserstellung während der Bereitstellung fehlschlägt. Siehe [Statische Inhaltsbereitstellung](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 und höher

Ersetzen Sie bei der Bereitstellung die Adobe Commerce-Basis-URLs in der Datenbank durch die von der [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) -Variable. Diese Konfiguration ist für die lokale Entwicklung nützlich, bei der Basis-URLs für Ihre lokale Umgebung eingerichtet werden. Wenn Sie eine Bereitstellung in einer Cloud-Umgebung durchführen, werden die URLs aktualisiert, damit Sie über die Projekt-URLs auf Ihre Storefront und Ihren Administrator zugreifen können.

Wenn Sie URLs bei der Bereitstellung in Pro- oder Starter Staging- und Produktionsumgebungen aktualisieren müssen, verwenden Sie die [`FORCE_UPDATE_URLS`](#force_update_urls) -Variable.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivieren oder deaktivieren Sie die [Symfony](https://symfony.com/doc/current/console/verbosity.html) Debug-Ausführlichkeitsstufe für `bin/magento` CLI-Befehle, die während der Bereitstellungsphase ausgeführt werden.

>[!NOTE]
>
>So verwenden Sie die Einstellung VERBOSE_COMMANDS , um die Details in der Befehlsausgabe für erfolgreich und fehlgeschlagen zu steuern `bin/magento` CLI-Befehle, müssen Sie festlegen [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Wählen Sie den Detailgrad aus, der in den Protokollen angegeben wird:

- `-v`= normale Ausgabe
- `-vv`= ausführlichere Ausgabe
- `-vvv` = ausführliche Ausgabe, ideal für das Debugging

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
