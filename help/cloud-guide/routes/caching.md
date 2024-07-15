---
title: Zwischenspeicherung
description: Erfahren Sie, wie Sie die Zwischenspeicherung für Ihre Adobe Commerce in Cloud-Infrastrukturumgebungen aktivieren.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Zwischenspeicherung

Sie können die Zwischenspeicherung in Ihrer Cloud-Infrastruktur-Projektumgebung aktivieren. Wenn Sie die Zwischenspeicherung deaktivieren, stellt Adobe Commerce die Dateien direkt bereit.

{{route-placeholder}}

## Zwischenspeicherung einrichten

Aktivieren Sie das Caching für Ihre Anwendung, indem Sie die Cache-Regeln in der Datei `.magento/routes.yaml` wie folgt konfigurieren:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Routenbasiertes Caching

Aktivieren Sie die differenzierte Zwischenspeicherung, indem Sie die Zwischenspeicherung für mehrere Routen separat einrichten, wie im folgenden Beispiel gezeigt wird:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

Im obigen Beispiel werden die folgenden Routen zwischengespeichert:

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

Die folgenden Routen werden im Cache **nicht** zwischengespeichert:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>Reguläre Ausdrücke in Routen werden **nicht** unterstützt.

## Aufbewahrungsfrist im Cache

Die Aufbewahrungsfrist im Cache wird durch den Wert des Antwortheaders `Cache-Control` bestimmt. Wenn keine `Cache-Control` -Kopfzeile in der Antwort enthalten ist, wird der `default_ttl` -Schlüssel verwendet.

## Cache-Schlüssel

Um zu entscheiden, wie eine Antwort zwischengespeichert werden soll, erstellt Adobe Commerce einen Cache-Schlüssel, der von mehreren Faktoren abhängt, und speichert die mit diesem Schlüssel verknüpfte Antwort. Wenn eine Anforderung denselben Cache-Schlüssel enthält, wird die Antwort wiederverwendet. Ihr Zweck ähnelt dem HTTP-Header [`Vary`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Die Parameter `headers` und `cookies` ermöglichen es Ihnen, diesen Cache-Schlüssel zu ändern.

Der Standardwert für diese Schlüssel lautet:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cache-Attribute

### `enabled`

Wenn auf `true` gesetzt, aktivieren Sie den Cache für diese Route. Wenn auf `false` gesetzt, deaktivieren Sie den Cache für diese Route.

### `headers`

Definiert, von welchen Werten der Cache-Schlüssel abhängen muss.

Wenn beispielsweise der Schlüssel `headers` wie folgt lautet:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Anschließend speichert Adobe Commerce für jeden Wert des HTTP-Headers `Accept` eine andere Antwort zwischen.

### `cookies`

Der Schlüssel `cookies` definiert, von welchen Werten der Cache-Schlüssel abhängen muss.

Beispiel:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

Der Cache-Schlüssel hängt vom Wert des `value` -Cookies in der Anforderung ab.

Es gibt einen Sonderfall, wenn der Schlüssel `cookies` den Wert `["*"]` aufweist. Dieser Wert bedeutet, dass jede Anforderung mit einem Cookie den Cache umgeht. Dies ist der Standardwert.

>[!NOTE]
>
>Sie können keine Platzhalter im Cookie-Namen verwenden. Verwenden Sie entweder einen genauen Cookie-Namen oder gleichen Sie alle Cookies mit einem Sternchen (`*`) ab. Beispielsweise sind `SESS*` oder `~SESS` derzeit gültige Werte vom Typ **nicht**.

Cookies haben die folgenden Einschränkungen:

- Sie können maximal **50 Cookies** im System festlegen. Andernfalls gibt die Anwendung die Ausnahme `Unable to send the cookie. Maximum number of cookies would be exceeded` aus.
- Die maximale Cookie-Größe beträgt **4096 Byte**. Andernfalls gibt die Anwendung die Ausnahme `Unable to send the cookie. Size of '%name' is %size bytes` aus.

### `default_ttl`

Wenn die Antwort keinen `Cache-Control` -Header aufweist, wird der `default_ttl` -Schlüssel verwendet, um die Aufbewahrungsfrist im Cache in Sekunden zu definieren. Der Standardwert ist `0`, was bedeutet, dass nichts zwischengespeichert wird.
