---
title: Bereitstellen von Variablen
description: Siehe die Liste der Umgebungsvariablen, die Aktionen in der Adobe Commerce-Bereitstellungsphase der Cloud-Infrastruktur steuern.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Bereitstellen von Variablen

Die folgenden _deploy_ -Variablen steuern Aktionen in der Bereitstellungsphase und können Werte von den [globalen Variablen](variables-global.md) übernehmen und überschreiben. Fügen Sie diese Variablen in die `deploy` -Phase der `.magento.env.yaml`-Datei ein:

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

Konfigurieren Sie die Seite &quot;Redis&quot;und die standardmäßige Zwischenspeicherung. Beim Festlegen des Parameters `cm_cache_backend_redis` müssen Sie die Optionen `server`, `port` und `database` angeben.

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

Im folgenden Beispiel wird die Funktion [Redis preload Feature](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) verwendet, wie im _Konfigurationshandbuch_ definiert:

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

Um ein benutzerdefiniertes [REDIS_BACKEND](#redis_backend) -Modell (nicht nur aus der Zulassungsliste) zu verwenden, setzen Sie die `_custom_redis_backend` -Option auf `true` , um die korrekte Validierung zu aktivieren, wie im folgenden Beispiel gezeigt:

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

Aktiviert bzw. deaktiviert das Löschen von [statischen Inhaltsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html), die während der Build- oder Bereitstellungsphase generiert wurden. Verwenden Sie den Standardwert _true_ in der Entwicklung als Best Practice.

- **`true`**: Entfernt alle vorhandenen statischen Inhalte, bevor der aktualisierte statische Inhalt bereitgestellt wird.
- **`false`** - Die Bereitstellung überschreibt nur vorhandene statische Inhaltsdateien, wenn der generierte Inhalt eine neuere Version enthält.

Wenn Sie statischen Inhalt in einem separaten Prozess ändern, setzen Sie den Wert auf _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Wenn statische Ansichtsdateien vor der Bereitstellung nicht bereinigt werden, kann dies zu Problemen führen, wenn Sie Aktualisierungen für vorhandene Dateien bereitstellen, ohne die vorherigen Versionen zu entfernen. Aufgrund von [statischen Dateiausweichregeln](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) können Fallback-Vorgänge die falsche Datei anzeigen, wenn das Verzeichnis mehrere Versionen derselben Datei enthält.

## `CRON_CONSUMERS_RUNNER`

- **Default**—`cron_run = false`, `max_messages = 1000`
- **Version**—Adobe Commerce 2.2.0 und höher

Verwenden Sie diese Umgebungsvariable, um sicherzustellen, dass Nachrichtenwarteschlangen nach einer Bereitstellung ausgeführt werden.

- `cron_run`—Ein boolescher Wert, der den `consumers_runner` Cron-Auftrag aktiviert oder deaktiviert (Standard = `false`).
- `max_messages` - Eine Zahl, die die maximale Anzahl von Nachrichten angibt, die jeder Verbraucher vor dem Beenden verarbeiten muss (Standard = `1000`). Sie können den Wert auf `0` setzen, um zu verhindern, dass der Verbraucher beendet wird.
- `consumers` - Ein Array von Zeichenfolgen, die angeben, welche Verbraucher ausgeführt werden sollen. Ein leeres Array führt _alle_ -Verbraucher aus.

- `multiple_processes`-Eine Zahl, die die Anzahl der Prozesse angibt, die für jeden Verbraucher erzeugt werden sollen. Unterstützt in Commerce **2.4.4** oder höher.

>[!NOTE]
>
>Um eine Liste der Nachrichtenwarteschlange `consumers` zurückzugeben, führen Sie den Befehl `./bin/magento queue:consumers:list` in der Remote-Umgebung aus.

Beispiel-Array, das bestimmte `consumers` und die `multiple_processes` ausführt, die für jeden Verbraucher erzeugt werden sollen:

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

Beispiel für ein leeres Array, das alle `consumers` -Werte ausführt:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Standardmäßig überschreibt der Bereitstellungsprozess alle Einstellungen in der Datei &quot;`env.php`&quot;. Siehe [Verwalten von Nachrichtenwarteschlangen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) im _Commerce Configuration Guide_ für lokale Adobe Commerce.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.2.0 und höher

Konfigurieren Sie, wie `consumers` Nachrichten aus der Nachrichtenwarteschlange verarbeitet, indem Sie eine der folgenden Optionen auswählen:

- `false`—`Consumers` verarbeitet verfügbare Nachrichten in der Warteschlange, schließt die TCP-Verbindung und beendet sie. `Consumers` nicht warten, bis zusätzliche Nachrichten in die Warteschlange gelangen, selbst wenn die Anzahl der verarbeiteten Nachrichten kleiner ist als der in der Implementierungsvariable `CRON_CONSUMERS_RUNNER` angegebene Wert `max_messages` .

- `true`—`Consumers` verarbeitet weiterhin Nachrichten aus der Nachrichtenwarteschlange, bis die in der Bereitstellungsvariable `CRON_CONSUMERS_RUNNER` angegebene maximale Anzahl von Nachrichten (`max_messages`) erreicht ist, bevor die TCP-Verbindung geschlossen und der Verbraucherprozess beendet wird. Wenn die Warteschlange vor Erreichen von `max_messages` leer ist, wartet der Verbraucher, bis weitere Nachrichten eintreffen.

>[!WARNING]
>
>Wenn Sie Sekundäre zum Ausführen von `consumers` anstelle eines Cron-Auftrags verwenden, setzen Sie diese Variable auf &quot;true&quot;.

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
>Legen Sie den Wert `CRYPT_KEY` über die Datei [!DNL Cloud Console] anstelle der Datei `.magento.env.yaml` fest, um zu vermeiden, dass der Schlüssel im Quellcode-Repository für Ihre Umgebung verfügbar gemacht wird. Siehe [Festlegen von Umgebungs- und Projektvariablen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

Wenn Sie die Datenbank ohne Installationsprozess von einer Umgebung in eine andere verschieben, benötigen Sie die entsprechenden kryptografischen Informationen. Adobe Commerce verwendet den in [!DNL Cloud Console] festgelegten Verschlüsselungsschlüsselwert als den Wert `crypt/key` in der Datei `env.php`.

## `DATABASE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Wenn Sie eine Datenbank in der [Eigenschaft &quot;Relations&quot;](../application/properties.md#relationships) der `.magento.app.yaml`-Datei definiert haben, können Sie Ihre Datenbankverbindungen für die Bereitstellung anpassen.

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

Im folgenden Beispiel wird das Tabellenpräfix `ece_` mit den Standardverbindungseinstellungen verwendet, anstatt die Option `_merge` zu verwenden:

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

```
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

Behält angepasste [!DNL Elastic Suite] Diensteinstellungen zwischen Bereitstellungen bei und verwendet sie im Abschnitt &quot;system/default/smile_elasticsuite_core_base_settings&quot;der Hauptkonfiguration [!DNL Elastic Suite]. Wenn das Paket [!DNL Elastic Suite] Composer installiert ist, wird es automatisch konfiguriert.

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

- Wenn Sie die Suchmaschine auf einen anderen Typ als `elasticsuite` ändern, tritt ein Bereitstellungsfehler auf, dem ein entsprechender Validierungsfehler beigefügt ist.
- Das Entfernen des Elasticsearch-Dienstes führt zu einem Bereitstellungsfehler zusammen mit einem entsprechenden Validierungsfehler

>[!NOTE]
>
>Weitere Informationen zur Verwendung des Plug-ins [!DNL Elastic Suite] oder zur Fehlerbehebung mit Adobe Commerce finden Sie in der [[!DNL Elastic Suite] Dokumentation](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 und höher

Aktiviert und deaktiviert Google Analytics bei der Bereitstellung in Staging- und Integrationsumgebungen. Standardmäßig gilt Google Analytics nur für die Produktionsumgebung. Setzen Sie diesen Wert auf `true` , um Google Analytics in den Staging- und Integrationsumgebungen zu aktivieren.

- **`true`** - Aktiviert Google Analytics in Staging- und Integrationsumgebungen.
- **`false`** - Deaktiviert Google Analytics in Staging- und Integrationsumgebungen.

Fügen Sie die Umgebungsvariable `ENABLE_GOOGLE_ANALYTICS` in der `.magento.env.yaml` -Datei der `deploy`-Phase hinzu:

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

Bei der Bereitstellung in der Pro- oder Starter-Staging- und Produktionsumgebung ersetzt diese Variable die Basis-URLs der Adobe Commerce-Datenbank durch die in der Variable [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) angegebenen Projekt-URLs. Verwenden Sie diese Einstellung, um das Standardverhalten der Bereitstellungsvariable [UPDATE_URLS](#update_urls) zu überschreiben, die bei der Bereitstellung in Staging- oder Produktionsumgebungen ignoriert wird.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Standard**—`file`
- **Version**—Adobe Commerce 2.2.5 und höher

Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. Verwenden Sie den Sperranbieter `file` in der Produktionsumgebung. Starterumgebungen und die Pro-Integrationsumgebung verwenden nicht die Variable [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) . Daher wendet `ece-tools` den Sperranbieter `db` automatisch an.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Siehe [Konfigurieren der Sperre](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) im _Installationshandbuch_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 und höher

>[!TIP]
>
>Die Variable &quot;`MYSQL_USE_SLAVE_CONNECTION`&quot; wird nur in Adobe Commerce in Cloud-Infrastruktur-Staging- und Produktions-Pro-Cluster-Umgebungen unterstützt und nicht in Starter-Projekten.

Adobe Commerce kann mehrere Datenbanken asynchron lesen. Auf `true` setzen, um automatisch eine _schreibgeschützte_ Verbindung zur Datenbank zu verwenden, um schreibgeschützten Traffic auf einem Nicht-Master-Knoten zu empfangen. Diese Verbindung verbessert die Leistung durch Lastenausgleich, da nur ein Knoten Lese- und Schreibvorgänge-Traffic verarbeitet. Auf `false` setzen, um ein vorhandenes schreibgeschütztes Verbindungs-Array aus der `env.php`-Datei zu entfernen.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Wenn die Variable `MYSQL_USE_SLAVE_CONNECTION` auf `true` gesetzt ist, wird der Parameter `synchronous_replication` in der Datei `env.php` in den Pro Staging- und Produktionsumgebungen standardmäßig auf `true` gesetzt. Wenn `MYSQL_USE_SLAVE_CONNECTION` auf `false` gesetzt ist, wird der Parameter `synchronous_replication` nicht konfiguriert.

## `QUEUE_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Verwenden Sie diese Umgebungsvariable, um zwischen Bereitstellungen benutzerdefinierte AMQP-Diensteinstellungen beizubehalten. Wenn Sie beispielsweise einen vorhandenen Nachrichtenwarteschlangendienst verwenden möchten, anstatt ihn von der Cloud-Infrastruktur zu erstellen, verwenden Sie die Umgebungsvariable `QUEUE_CONFIGURATION` , um ihn mit Ihrer Site zu verbinden:

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

Das Beispiel zum Festlegen von `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Wenn Sie `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` als Redis-Backend-Modell angeben, um den [L2-Cache](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html) zu aktivieren, generiert `ece-tools` die Cache-Konfiguration automatisch. Eine Beispiel-Konfigurationsdatei [finden Sie im _Adobe Commerce-Konfigurationshandbuch_. ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) Um die generierte Cache-Konfiguration zu überschreiben, verwenden Sie die Bereitstellungsvariable [CACHE_CONFIGURATION](#cache_configuration) .

## `REDIS_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.16 und höher

>[!WARNING]
>
>Aktivieren Sie diese Variable _nicht_ in einem [skalierten Architektur](../architecture/scaled-architecture.md) -Projekt. Dies führt zu Redis-Verbindungsfehlern. Redis Slaves sind noch aktiv, werden aber nicht für Redis-Lesevorgänge verwendet. Alternativ empfiehlt Adobe die Verwendung von Adobe Commerce 2.3.5 oder höher, eine neue Redis-Backend-Konfiguration zu implementieren und die L2-Zwischenspeicherung für Redis zu implementieren.

>[!TIP]
>
>Die Variable &quot;`REDIS_USE_SLAVE_CONNECTION`&quot; wird nur in Adobe Commerce in Cloud-Infrastruktur-Staging- und Produktions-Pro-Cluster-Umgebungen unterstützt und nicht in Starter-Projekten.

Adobe Commerce kann mehrere Redis-Instanzen asynchron lesen. Auf `true` setzen, um automatisch eine schreibgeschützte _Verbindung_ zu einer Redis-Instanz zu verwenden, um schreibgeschützten Traffic auf einem Nicht-Master-Knoten zu empfangen. Diese Verbindung verbessert die Leistung durch Lastenausgleich, da nur ein Knoten Lese- und Schreibvorgänge-Traffic verarbeitet. Auf `false` setzen, um ein vorhandenes schreibgeschütztes Verbindungs-Array aus der `env.php`-Datei zu entfernen.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Sie müssen einen Redis-Dienst in der Datei `.magento.app.yaml` und in der Datei `services.yaml` konfiguriert haben.

[ECE-Tools Version 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) und höher verwendet fehlertolerantere Einstellungen. Wenn Adobe Commerce keine Daten aus der Redis _slave_ -Instanz lesen kann, werden Daten aus der Redis _master_ -Instanz gelesen.

Die schreibgeschützte Verbindung kann nicht in der Integrationsumgebung verwendet werden oder wenn Sie die Variable [`CACHE_CONFIGURATION` ](#cache_configuration) verwenden.

## `RESOURCE_CONFIGURATION`

- **Standard**—Nicht festgelegt
- **Version**—Adobe Commerce 2.1.4 und höher

Ordnet einen Ressourcennamen einer Datenbankverbindung zu. Diese Konfiguration entspricht dem Abschnitt `resource` der Datei `env.php` .

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

Gibt an, welche [gzip](https://www.gnu.org/software/gzip)-Komprimierungsstufe (`0` bis `9`) beim Komprimieren statischen Inhalts verwendet werden soll. `0` deaktiviert die Komprimierung.

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

Sie können mehrere Gebietsschemata pro Design konfigurieren. Diese Anpassung beschleunigt den Implementierungsprozess, indem die Anzahl unnötiger Designdateien verringert wird. Sie können beispielsweise das Design _magento/backend_ auf Englisch und ein benutzerdefiniertes Design in anderen Sprachen bereitstellen.

Im folgenden Beispiel wird das `Magento/backend` -Design mit drei Gebietsschemas bereitgestellt:

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

Außerdem können Sie festlegen, dass _nicht_ ein Design bereitstellt:

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

Legen Sie in der Bereitstellungsphase den Wert &quot;`SCD_NO_PARENT: true`&quot;fest, damit statische Inhalte für übergeordnete Designs nicht während der Bereitstellungsphase generiert werden. Diese Einstellung minimiert die Bereitstellungszeit und verhindert Site-Ausfallzeiten, die auftreten können, wenn der statische Inhaltserstellung während der Bereitstellung fehlschlägt. Siehe [Bereitstellung statischer Inhalte](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Standard**—`quick`
- **Version**—Adobe Commerce 2.2.0 und höher

Ermöglicht die Anpassung der [Implementierungsstrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) für statischen Inhalt. Siehe [Bereitstellen von statischen Ansichtsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Verwenden Sie diese Optionen _nur_ , wenn Sie mehr als ein Gebietsschema haben:

- `standard` - stellt alle statischen Ansichtsdateien für alle Pakete bereit.
- `quick`—(_default_) minimiert die Bereitstellungszeit.
- `compact` - Speichert Speicherplatz auf dem Server. In Adobe Commerce Version 2.2.4 und früher überschreibt diese Einstellung den Wert für `scd_threads` mit dem Wert `1`.

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

Um die Bereitstellungszeit weiter zu verkürzen, verwenden Sie [Konfigurationsverwaltung](../store/store-settings.md) mit dem Befehl `scd-dump` , um die statische Bereitstellung in die Build-Phase zu verschieben.

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

Konfigurieren des Sitzungsspeichers für Redis. Erfordert die Optionen `save`, `redis`, `host`, `port` und `database` für die Sitzungsspeichervariable. Beispiel:

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

Setzen Sie dies auf &quot;`true`&quot;, um die Bereitstellung statischer Inhalte während der Bereitstellungsphase zu überspringen.

Legen Sie in der Bereitstellungsphase `SKIP_SCD: true` fest, damit der statische Inhaltserstellung nicht während der Bereitstellungsphase erfolgt. Diese Einstellung minimiert die Bereitstellungszeit und verhindert Site-Ausfallzeiten, die auftreten können, wenn der statische Inhaltserstellung während der Bereitstellung fehlschlägt. Siehe [Bereitstellung statischer Inhalte](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 und höher

Ersetzen Sie bei der Bereitstellung die Adobe Commerce-Basis-URLs in der Datenbank durch die Projekt-URLs, die durch die Variable [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) angegeben wurden. Diese Konfiguration ist für die lokale Entwicklung nützlich, bei der Basis-URLs für Ihre lokale Umgebung eingerichtet werden. Wenn Sie eine Bereitstellung in einer Cloud-Umgebung durchführen, werden die URLs aktualisiert, damit Sie über die Projekt-URLs auf Ihre Storefront und Ihren Administrator zugreifen können.

Wenn Sie URLs bei der Bereitstellung in Pro- oder Starter Staging- und Produktionsumgebungen aktualisieren müssen, verwenden Sie die Variable &quot;[`FORCE_UPDATE_URLS`](#force_update_urls)&quot;.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivieren oder deaktivieren Sie die Debugging-Ausführlichkeitsstufe für `bin/magento` CLI-Befehle, die während der Bereitstellungsphase ausgeführt werden.[](https://symfony.com/doc/current/console/verbosity.html)

>[!NOTE]
>
>Um die VERBOSE_COMMANDS-Einstellung zu verwenden, um die Details in der Befehlsausgabe für erfolgreiche und fehlgeschlagene `bin/magento` CLI-Befehle zu steuern, müssen Sie [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug` festlegen.

Wählen Sie den Detailgrad aus, der in den Protokollen angegeben wird:

- `-v` = normale Ausgabe
- `-vv`= ausführlichere Ausgabe
- `-vvv` = ausführliche Ausgabe, ideal für das Debugging

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
