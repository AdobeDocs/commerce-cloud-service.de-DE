---
title: Serverseitige Includes
description: Erfahren Sie, wie Sie serverseitige Includes mit Adobe Commerce in der Cloud-Infrastruktur verwenden.
feature: Cloud, Routes
exl-id: 34a38cb5-5f0e-49ac-9dba-bb581a06aeed
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Serverseitige Includes

[Serverseitige Includes](https://nginx.org/en/docs/http/ngx_http_ssi_module.html) (SSI) sind Anweisungen auf HTML-Seiten, die auf dem Server ausgewertet werden, während die Seiten gerendert werden. Mit SSI können Sie dynamisch generierte Inhalte zu einer bestehenden HTML hinzufügen, ohne die gesamte Seite zu bedienen.

Sie können SSI pro Route in Ihrer `.magento/routes.yaml`; zum Beispiel:

```yaml
    "http://{default}/":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: false
            ssi:
                enabled: true
    "http://{default}/time.php":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: true
```

Mit SSI können Sie in Ihre HTML-Response-Direktiven einschließen, die dazu führen, dass der Server Teile des HTML ausfüllt, wobei alle vorhandenen berücksichtigt werden [Caching-Konfiguration](caching.md).

Das folgende Beispiel zeigt, wie Sie ein dynamisches Datumssteuerelement am Anfang einer Seite einfügen und ein weiteres Datumssteuerelement am unteren Rand, das alle 600 Sekunden aktualisiert wird:

Fügen Sie jeder Seite Folgendes hinzu, beispielsweise `/index.php`:

```php?start_inline=1
echo date(DATE_RFC2822);
<!--#include virtual="time.php" -->
```

Fügen Sie Folgendes hinzu: `time.php`:

```php?start_inline=1
header("Cache-Control: max-age=600");
echo date(DATE_RFC2822);
```

Navigieren Sie zu der Seite, auf der Sie das Steuerelement hinzugefügt haben. Aktualisieren Sie die Seite mehrmals und beachten Sie, dass sich die Zeit oben auf der Seite ändert, die Zeit am unteren Rand jedoch nur alle 600 Sekunden geändert wird.
