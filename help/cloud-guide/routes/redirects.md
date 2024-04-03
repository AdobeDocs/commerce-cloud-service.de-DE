---
title: Umleitungen
description: Erfahren Sie, wie Sie Umleitungsregeln für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur verwalten.
feature: Cloud, Routes
exl-id: 7089a790-6341-4443-990a-df42091f0680
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Umleitungen

Die Verwaltung von Weiterleitungsregeln ist eine gängige Voraussetzung für Webanwendungen, insbesondere in Fällen, in denen Sie eingehende Links, die sich im Laufe der Zeit geändert oder entfernt haben, nicht verlieren möchten.

Im Folgenden wird gezeigt, wie Sie Umleitungsregeln für Ihre Adobe Commerce in Cloud-Infrastrukturprojekten mit dem `routes.yaml` Konfigurationsdatei. Wenn die in diesem Thema behandelten Umleitungsmethoden für Sie nicht funktionieren, können Sie die Zwischenspeicherung von Kopfzeilen verwenden, um dasselbe zu tun.

{{route-placeholder}}

## Updates für Pro-Umgebungen

{{pro-self-service-warning}}

>[!WARNING]
>
>Konfigurieren Sie für Adobe Commerce in Cloud-Infrastrukturprojekten zahlreiche Nicht-Regex-Umleitungen und Umschreibungen in der `routes.yaml` -Datei Leistungsprobleme verursachen. Wenn `routes.yaml` -Datei 32 KB oder größer ist, laden Sie Ihre Nicht-Regex-Umleitungen ab und schreiben Sie sie auf Fastly um. Siehe [Nicht-Regex-Umleitungen werden nach Fastly anstatt nach Nginx (Routen) abgeladen.](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) im _Adobe Commerce Help Center_.

## Umleitungen auf ganze Strecken

Mithilfe von Umleitungen über ganze Routen können Sie einfache Routen mithilfe der `routes.yaml` -Datei. Sie können beispielsweise von einer Apex-Domäne zu einer `www` Subdomain wie folgt:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Teilroute-Umleitungen

Im `.magento/routes.yaml` -Datei können Sie basierend auf der Musterübereinstimmung partielle Umleitungsregeln zu vorhandenen Routen hinzufügen:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Teilumleitungen funktionieren mit jeder Route, einschließlich Routen, die direkt von der Anwendung bedient werden.

Zwei Schlüssel sind unter verfügbar `redirects`:

- **expires**—Optional, gibt die Zeit an, die die Weiterleitung im Browser zwischengespeichert werden soll. Beispiele für gültige Werte sind `3600s`, `1d`, `2w`, `3m`.

- **paths**—Ein oder mehrere Schlüssel-Wert-Paare, die die Konfiguration für Umleitungsregeln für Teilstrecken angeben.

  Für jede Umleitungsregel ist der Schlüssel ein Ausdruck zum Filtern von Anfragepfaden für die Umleitung. Der Wert ist ein Objekt, das das Zielziel für die Umleitung und die Optionen für die Verarbeitung der Umleitung angibt.

  Das value -Objekt weist die folgenden Eigenschaften auf:

  | Eigenschaft | Beschreibung |
  | ---------- | ----------- |
  | `to` | Erforderlich: ein teilweiser absoluter Pfad, eine URL mit Protokoll und Host oder ein Muster, das das Ziel für die Umleitungsregel angibt. |
  | `regexp` | Optional, standardmäßig `false`. Gibt an, ob der Pfadschlüssel als regulärer PCRE-Ausdruck interpretiert werden soll. |
  | `prefix` | Gibt an, ob die Umleitung sowohl für den Pfad als auch für alle untergeordneten Elemente oder nur für den Pfad selbst gilt. Standardwert ist `true`. Dieser Wert wird nicht unterstützt, wenn `regexp` is `true`. |
  | `append_suffix` | Bestimmt, ob das Suffix mit der Umleitung übernommen wird. Standardwert ist `true`. Dieser Wert wird nicht unterstützt, wenn die `regexp` Schlüssel ist `true` oder* wenn die `prefix` Schlüssel ist `false`. |
  | `code` | Gibt den HTTP-Statuscode an. Gültige Statuscodes sind [`301` (Dauerhaft verschoben)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8), und [`308`](https://www.rfc-editor.org/rfc/rfc7238). Standardwert ist `302`. |
  | `expires` | Optional: Gibt die Zeit an, die die Weiterleitung im Browser zwischengespeichert werden soll. Die Standardeinstellung ist `expires` Wert, der direkt unter dem `redirects` auf, aber auf dieser Ebene können Sie den Cache-Ablauf für einzelne partielle Weiterleitungen optimieren. |

## Beispiele für Umleitungen auf Teilstrecken

Die folgenden Beispiele zeigen, wie Sie Teilroute-Umleitungen im `routes.yaml` Datei mit verschiedenen `paths` Konfigurationsoptionen.

### Abgleich von regulärem Ausdrucksmuster

Verwenden Sie das folgende Format, um Umleitungsanfragen basierend auf einem regulären Ausdruck zu konfigurieren.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Diese Konfiguration filtert Anfragepfade für einen regulären Ausdruck und leitet übereinstimmende Anforderungen an `https://example.com`. Beispielsweise eine Anfrage an `https://example.com/regexp/a/b/c/match` umleitet auf `https://example.com/a/b/c`.

### Präfixmuster-Übereinstimmung

Verwenden Sie das folgende Format, um Umleitungsanfragen für Pfade zu konfigurieren, die mit einem angegebenen Präfixmuster beginnen.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Diese Konfiguration funktioniert wie folgt:

- Umleitungsanfragen, die dem Muster entsprechen `/from` zum Pfad `http://{default}/to`.

- Umleitungsanfragen, die dem Muster entsprechen `/from/another/path` nach `https://{default}/to/another/path`.

- Wenn Sie die `prefix` Eigenschaft auf `false`, Anforderungen, die mit dem `/from` Muster Trigger einer Umleitung, aber Anforderungen, die mit dem `/from/another/path` Muster nicht verwenden.

### Suffix-Musterabgleich

Verwenden Sie das folgende Format, um Umleitungsanfragen zu konfigurieren, die das Pfadsuffix aus der Anfrage an das Zielziel anhängen:

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Diese Konfiguration funktioniert wie folgt:

- Umleitungsanfragen, die dem Muster entsprechen `/from/path/suffix` zum Pfad `https://{default}/to`.

- Wenn Sie die `append_suffix` Eigenschaft auf `true`, dann Anforderungen, die übereinstimmen `/from/path/suffix`  zum Pfad umleiten `https://{default}/to/path/suffix`.

### Pfadspezifische Cache-Konfiguration

Verwenden Sie das folgende Format, um die Zeit zum Zwischenspeichern einer Weiterleitung von einem bestimmten Pfad anzupassen:

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
    paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Diese Konfiguration funktioniert wie folgt:

- Umleitungen vom ersten Pfad (`/from`) werden einen Tag lang zwischengespeichert.

- Umleitungen vom zweiten Pfad (`/here`) werden zwei Wochen lang zwischengespeichert.
