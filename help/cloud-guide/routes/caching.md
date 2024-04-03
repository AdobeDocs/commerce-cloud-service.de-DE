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

Aktivieren Sie die Zwischenspeicherung für Ihre Anwendung, indem Sie die Cache-Regeln im Abschnitt `.magento/routes.yaml` Datei wie folgt:

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

Und die folgenden Routen sind **not** zwischengespeichert:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>Reguläre Ausdrücke in Routen sind **not** unterstützt.

## Aufbewahrungsfrist im Cache

Die Aufbewahrungsfrist im Cache wird durch die Variable `Cache-Control` Antwortheader-Wert. Wenn nicht `Cache-Control` -Kopfzeile in der Antwort enthalten ist, wird die `default_ttl` verwendet wird.

## Cache-Schlüssel

Um zu entscheiden, wie eine Antwort zwischengespeichert werden soll, erstellt Adobe Commerce einen Cache-Schlüssel, der von mehreren Faktoren abhängt, und speichert die mit diesem Schlüssel verknüpfte Antwort. Wenn eine Anforderung denselben Cache-Schlüssel enthält, wird die Antwort wiederverwendet. Ihr Zweck ähnelt dem HTTP [`Vary` header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Die Parameter `headers` und `cookies` -Schlüssel ermöglichen es Ihnen, diesen Cache-Schlüssel zu ändern.

Der Standardwert für diese Schlüssel lautet:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cache-Attribute

### `enabled`

Wenn festgelegt auf `true`aktivieren Sie den Cache für diese Route. Wenn festgelegt auf `false`, deaktivieren Sie den Cache für diese Route.

### `headers`

Definiert, von welchen Werten der Cache-Schlüssel abhängen muss.

Wenn beispielsweise die Variable `headers` Schlüssel ist:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Anschließend speichert Adobe Commerce für jeden Wert der Variablen `Accept` HTTP-Header.

### `cookies`

Die `cookies` -Schlüssel definiert, von welchen Werten der Cache-Schlüssel abhängen muss.

Beispiel:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

Der Cache-Schlüssel hängt vom Wert der `value` -Cookie in der -Anfrage.

Wenn die Variable `cookies` -Schlüssel hat die `["*"]` -Wert. Dieser Wert bedeutet, dass jede Anforderung mit einem Cookie den Cache umgeht. Dies ist der Standardwert.

>[!NOTE]
>
>Sie können keine Platzhalter im Cookie-Namen verwenden. Verwenden Sie entweder einen präzisen Cookie-Namen oder gleichen Sie alle Cookies mit einem Sternchen (`*`). Beispiel: `SESS*` oder `~SESS` derzeit **not** gültige Werte.

Cookies haben die folgenden Einschränkungen:

- Sie können die maximale Anzahl von **50 Cookies** im System. Andernfalls gibt die Anwendung eine `Unable to send the cookie. Maximum number of cookies would be exceeded` Ausnahmefehler.
- Die maximale Cookie-Größe beträgt **4096 Byte**. Andernfalls gibt die Anwendung eine `Unable to send the cookie. Size of '%name' is %size bytes` Ausnahmefehler.

### `default_ttl`

Wenn die Antwort keine `Cache-Control` -Kopfzeile, die `default_ttl` -Schlüssel wird verwendet, um die Aufbewahrungsfrist im Cache in Sekunden zu definieren. Der Standardwert ist `0`, was bedeutet, dass nichts zwischengespeichert wird.
