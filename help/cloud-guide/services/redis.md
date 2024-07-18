---
title: Redis-Dienst einrichten
description: Erfahren Sie, wie Sie Redis als Backend-Cache-Lösung für Adobe Commerce in der Cloud-Infrastruktur einrichten und optimieren.
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: c39332d352f6dcb6f92c312a6ef1b74319d37aa3
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Redis-Dienst einrichten

[Redis](https://redis.io) ist eine optionale Backend-Cache-Lösung, die das Zend Framework Zend_Cache_Backend_File ersetzt, das Adobe Commerce standardmäßig verwendet.

Siehe [Konfigurieren von Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) im _Konfigurationshandbuch_.

{{service-instruction}}

**So aktivieren Sie Redis**:

1. Fügen Sie den erforderlichen Namen und Typ zur Datei `.magento/services.yaml` hinzu.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Um Ihre eigene Redis-Konfiguration bereitzustellen, fügen Sie einen `core_config` -Schlüssel in Ihre `.magento/services.yaml` -Datei ein:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Konfigurieren Sie die Beziehungen in der Datei &quot;`.magento.app.yaml`&quot;.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Überprüfen Sie die Dienstbeziehungen](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verwenden der Redis-CLI

Wenn Ihre Redis-Beziehung den Namen `redis` hat, können Sie mit dem Tool `redis-cli` darauf zugreifen.

1. Verwenden Sie SSH, um eine Verbindung zur Integrationsumgebung mit installierten und konfigurierten Redis herzustellen.

1. Öffnen Sie einen SSH-Tunnel zu einem Host.

   ```bash
   redis-cli -h redis.internal
   ```

## Installieren der Rediv-Version

Verwenden Sie den folgenden Befehl, um die Redis-Version in einer Integrationsumgebung zu installieren:

```bash
redis-cli -h redis.internal info | grep version
```

Beispielantwort:

```
redis_version:7.0.5
gcc_version:8.3.0
```

### Rediv zu Pro Staging und Produktion

Um die Redis-Version in einer Staging- oder Produktionsumgebung zu installieren, verwenden Sie den Befehl `redis-server`:

```bash
redis-server -v
```

```
Redis server v=7.0.5 ...
```

Verwenden Sie den folgenden Befehl, um die Redis-Konfiguration in einer Pro Staging- oder Produktionsumgebung zu installieren:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Beispielantwort:

```json
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Fehlerbehebung bei Redizes

In den folgenden Adobe Commerce-Supportartikeln finden Sie Hilfe zur Fehlerbehebung bei Problemen mit Redis:

- [Redis issue Delay Admin Login or Checkout](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Extended Redis Cache-Implementierung Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [MDVA-30102: Redis-Cache wird voll ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/v1-0-6/mdva-30102-magento-patch-redis-cache-getting-full.html)
- [Verwaltete Warnhinweise für Adobe Commerce: Warnhinweis bezüglich Speicherbereinigung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Verwaltete Warnhinweise für Adobe Commerce: Warnhinweis zur Speicherbedingung erneut anzeigen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
- [Redis troubleshooting](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
