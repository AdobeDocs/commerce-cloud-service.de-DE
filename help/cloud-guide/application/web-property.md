---
title: Webeigenschaft
description: Beispiele zum Konfigurieren der Webeigenschaft finden Sie im Abschnitt [!DNL Commerce] Anwendungskonfigurationsdatei.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Webeigenschaft

Die `web` -Eigenschaft definiert, wie Ihre Anwendung dem Web bereitgestellt wird (in HTTP), bestimmt, wie die Webanwendung Inhalte bereitstellt, und steuert, wie der Anwendungscontainer auf eingehende Anforderungen reagiert, indem Regeln an jedem Ort festgelegt werden. _block_. Ein Block stellt einen absoluten Pfad dar, der mit einem Schrägstrich (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

Sie können Ihre `locations` Konfiguration mit den folgenden Schlüsselwerten für jede `locations` block:

| Attribut | Beschreibung |
| :--- | :--- |
| `allow` | Bereitstellen von Dateien, die nicht mit den &quot;Regeln&quot;übereinstimmen. Standardwert = `true` |
| `expires` | Legen Sie die Anzahl der Sekunden fest, um Inhalte im Browser zwischenzuspeichern. Dieser Schlüssel ermöglicht die `cache-control` und `expires` Kopfzeilen für statischen Inhalt. Wenn dieser Wert nicht festgelegt ist, wird die `expires` -Direktive und die resultierenden Kopfzeilen sind bei der Bereitstellung statischer Inhaltsdateien nicht enthalten. Negativ 1 (`-1`) führt zu keiner Zwischenspeicherung und ist der Standardwert. Sie können den Zeitwert mit den folgenden Einheiten ausdrücken:  `ms` (Millisekunden), `s` (Sekunden), `m` (Minuten), `h` (Stunden) `d` (Tage) `w` (Wochen) `M` (Monate, 30d) oder `y` (Jahre, 365d) |
| `headers` | Festlegen benutzerdefinierter Kopfzeilen, z. B. `X-Frame-Options`, für statischen Inhalt, der von diesem Speicherort bereitgestellt wird. |
| `index` | Auflisten der statischen Dateien, die für Ihre Anwendung bereitgestellt werden sollen, z. B. die `index.html` -Datei. Dieser Schlüssel erwartet eine Sammlung. Dies funktioniert nur, wenn der Zugriff auf die Datei(en) durch die `allow` oder `rules` Schlüssel für diesen Speicherort. |
| `rules` | Legen Sie Überschreibungen für einen Ort fest. Verwenden Sie einen regulären Ausdruck, um eine Anforderung abzugleichen. Wenn eine eingehende Anfrage mit der Regel übereinstimmt, wird die regelmäßige Verarbeitung der Anfrage durch die in der Regel verwendeten Schlüssel überschrieben. |
| `passthru` | Legen Sie die URL fest, die verwendet wird, falls keine statische Datei oder PHP-Datei gefunden werden kann. Normalerweise ist diese URL der erste Controller für Ihre Anwendungen, z. B. `/index.php` oder `/app.php`. |
| `root` | Legen Sie den Pfad relativ zum Stammverzeichnis der Anwendung fest, die im Internet verfügbar gemacht wird. Das öffentliche Verzeichnis (Speicherort &quot;/&quot;) für ein Cloud-Projekt ist standardmäßig auf &quot;pub&quot;festgelegt. |
| `scripts` | Laden von Skripten an diesem Speicherort zulassen. Setzen Sie den Wert auf `true` , um Skripte zuzulassen. |

Die Standardkonfiguration ermöglicht Folgendes:

- Aus dem Stammverzeichnis (`/`), nur auf Web und Medien zugreifen können.
- Aus dem `~/pub/static` und `~/pub/media` Pfade, auf jede Datei kann zugegriffen werden

Das folgende Beispiel zeigt die Standardkonfiguration im `.magento.app.yaml` -Datei für eine Reihe von Web-zugänglichen Speicherorten, die mit einem Eintrag in der  [`mounts` property](properties.md#mounts):

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
>Dieses Beispiel zeigt die standardmäßige Webkonfiguration für ein Cloud-Projekt, das für die Unterstützung einer einzelnen Domäne konfiguriert ist. Für ein Projekt, für das die Unterstützung mehrerer Websites oder Stores erforderlich ist, muss die Variable `web` muss so eingerichtet sein, dass freigegebene Domänen unterstützt werden. Siehe [Orte für freigegebene Domänen konfigurieren](../store/multiple-sites.md#configure-locations-for-shared-domains).
