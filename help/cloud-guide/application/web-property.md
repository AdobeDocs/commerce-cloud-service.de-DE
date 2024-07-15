---
title: Webeigenschaft
description: Siehe Beispiele zum Konfigurieren der Webeigenschaft in der Konfigurationsdatei der [!DNL Commerce] Anwendung.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Webeigenschaft

Die `web` -Eigenschaft definiert, wie Ihre Anwendung dem Web bereitgestellt wird (in HTTP), bestimmt, wie die Webanwendung Inhalte bereitstellt, und steuert, wie der Anwendungscontainer auf eingehende Anforderungen reagiert, indem Regeln an jedem Ort festgelegt werden _block_. Ein Block stellt einen absoluten Pfad dar, der mit einem Schrägstrich (`/`) führt.

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

Sie können Ihre `locations` -Konfiguration mithilfe der folgenden Schlüsselwerte für jeden `locations` -Block anpassen:

| Attribut | Beschreibung |
| :--- | :--- |
| `allow` | Bereitstellen von Dateien, die nicht mit den &quot;Regeln&quot;übereinstimmen. Standardwert = `true` |
| `expires` | Legen Sie die Anzahl der Sekunden fest, um Inhalte im Browser zwischenzuspeichern. Dieser Schlüssel aktiviert die Header `cache-control` und `expires` für statischen Inhalt. Wenn dieser Wert nicht festgelegt ist, werden die Anweisung `expires` und die resultierenden Kopfzeilen bei der Bereitstellung statischer Inhaltsdateien nicht einbezogen. Ein negativer 1-Wert (`-1`) führt zu keiner Zwischenspeicherung und ist der Standardwert. Sie können den Zeitwert mit den folgenden Einheiten ausdrücken: `ms` (Millisekunden), `s` (Sekunden), `m` (Minuten), `h` (Stunden), `d` (Tage), `w` (Wochen), `M` (Monate, 30d) oder `y` (Jahre, 365d) |
| `headers` | Legen Sie benutzerdefinierte Header wie `X-Frame-Options` für statischen Inhalt fest, der von diesem Speicherort bereitgestellt wird. |
| `index` | Geben Sie die statischen Dateien an, die für Ihre Anwendung bereitgestellt werden sollen, z. B. die Datei &quot;`index.html`&quot;. Dieser Schlüssel erwartet eine Sammlung. Dies funktioniert nur, wenn der Zugriff auf die Datei(en) durch den Schlüssel `allow` oder `rules` für diesen Speicherort &quot;erlaubt&quot;ist. |
| `rules` | Legen Sie Überschreibungen für einen Ort fest. Verwenden Sie einen regulären Ausdruck, um eine Anforderung abzugleichen. Wenn eine eingehende Anfrage mit der Regel übereinstimmt, wird die regelmäßige Verarbeitung der Anfrage durch die in der Regel verwendeten Schlüssel überschrieben. |
| `passthru` | Legen Sie die URL fest, die verwendet wird, falls keine statische Datei oder PHP-Datei gefunden werden kann. In der Regel ist diese URL der erste Controller für Ihre Anwendungen, z. B. `/index.php` oder `/app.php`. |
| `root` | Legen Sie den Pfad relativ zum Stammverzeichnis der Anwendung fest, die im Internet verfügbar gemacht wird. Das öffentliche Verzeichnis (Speicherort &quot;/&quot;) für ein Cloud-Projekt ist standardmäßig auf &quot;pub&quot;festgelegt. |
| `scripts` | Laden von Skripten an diesem Speicherort zulassen. Setzen Sie den Wert auf `true` , um Skripte zuzulassen. |

Die Standardkonfiguration ermöglicht Folgendes:

- Vom Stammpfad (`/`) aus kann nur auf Web und Medien zugegriffen werden
- Über die Pfade `~/pub/static` und `~/pub/media` kann auf jede Datei zugegriffen werden

Das folgende Beispiel zeigt die Standardkonfiguration in der Datei `.magento.app.yaml` für eine Reihe von Web-zugänglichen Speicherorten, die mit einem Eintrag in der Eigenschaft [`mounts` ](properties.md#mounts) verknüpft sind:

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>Dieses Beispiel zeigt die standardmäßige Webkonfiguration für ein Cloud-Projekt, das für die Unterstützung einer einzelnen Domäne konfiguriert ist. Für ein Projekt, das Unterstützung für mehrere Websites oder Stores erfordert, muss die Konfiguration `web` so eingerichtet sein, dass freigegebene Domänen unterstützt werden. Siehe [Speicherorte für freigegebene Domänen konfigurieren](../store/multiple-sites.md#configure-locations-for-shared-domains).
