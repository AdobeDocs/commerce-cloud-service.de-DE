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

Im Folgenden wird gezeigt, wie Sie mithilfe der Konfigurationsdatei &quot;`routes.yaml`&quot;Umleitungsregeln in Ihrer Adobe Commerce für Cloud-Infrastrukturprojekte verwalten. Wenn die in diesem Thema behandelten Umleitungsmethoden für Sie nicht funktionieren, können Sie die Zwischenspeicherung von Kopfzeilen verwenden, um dasselbe zu tun.

{{route-placeholder}}

## Updates für Pro-Umgebungen

{{pro-self-service-warning}}

>[!WARNING]
>
>Bei Adobe Commerce in Cloud-Infrastrukturprojekten kann das Konfigurieren zahlreicher Nicht-Regex-Weiterleitungen und Rewrites in der Datei `routes.yaml` Leistungsprobleme verursachen. Wenn Ihre `routes.yaml` -Datei 32 KB oder größer ist, laden Sie Ihre Nicht-Regex-Umleitungen ab und schreiben Sie sie in Fastly um. Siehe [Nicht-Regex-Umleitungen zu Fastly anstatt Nginx (Routen) laden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) im _Adobe Commerce Help Center_.

## Umleitungen auf ganze Strecken

Mithilfe von Umleitungen über ganze Routen können Sie einfache Routen mithilfe der Datei `routes.yaml` definieren. Sie können beispielsweise wie folgt von einer Apex-Domäne zu einer `www` -Subdomäne umleiten:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Teilroute-Umleitungen

In der Datei `.magento/routes.yaml` können Sie basierend auf der Musterübereinstimmung partielle Umleitungsregeln zu bestehenden Routen hinzufügen:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Teilumleitungen funktionieren mit jeder Route, einschließlich Routen, die direkt von der Anwendung bedient werden.

Zwei Schlüssel sind unter `redirects` verfügbar:

- **expires** - Optional: Gibt die Zeit an, die zum Zwischenspeichern der Weiterleitung im Browser erforderlich ist. Beispiele für gültige Werte sind `3600s`, `1d`, `2w`, `3m`.

- **Pfade**: Ein oder mehrere Schlüssel-Wert-Paare, die die Konfiguration für Regeln für Umleitungen mit partieller Route angeben.

  Für jede Umleitungsregel ist der Schlüssel ein Ausdruck zum Filtern von Anfragepfaden für die Umleitung. Der Wert ist ein Objekt, das das Zielziel für die Umleitung und die Optionen für die Verarbeitung der Umleitung angibt.

  Das value -Objekt weist die folgenden Eigenschaften auf:

  | Eigenschaft | Beschreibung |
  | ---------- | ----------- |
  | `to` | Erforderlich: ein teilweiser absoluter Pfad, eine URL mit Protokoll und Host oder ein Muster, das das Ziel für die Umleitungsregel angibt. |
  | `regexp` | Optional, standardmäßig `false`. Gibt an, ob der Pfadschlüssel als regulärer PCRE-Ausdruck interpretiert werden soll. |
  | `prefix` | Gibt an, ob die Umleitung sowohl für den Pfad als auch für alle untergeordneten Elemente oder nur für den Pfad selbst gilt. Der Standardwert ist `true`. Dieser Wert wird nicht unterstützt, wenn `regexp` `true` ist. |
  | `append_suffix` | Bestimmt, ob das Suffix mit der Umleitung übernommen wird. Der Standardwert ist `true`. Dieser Wert wird nicht unterstützt, wenn der `regexp` -Schlüssel `true` oder* ist, wenn der `prefix` -Schlüssel `false` ist. |
  | `code` | Gibt den HTTP-Statuscode an. Gültige Statuscodes sind [`301` (Dauerhaft verschoben)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8) und [`308`](https://www.rfc-editor.org/rfc/rfc7238). Der Standardwert ist `302`. |
  | `expires` | Optional: Gibt die Zeit an, die die Weiterleitung im Browser zwischengespeichert werden soll. Der Standardwert ist der `expires` -Wert, der direkt unter dem `redirects` -Schlüssel definiert ist. Auf dieser Ebene können Sie jedoch den Cache-Ablauf für einzelne Teilumleitungen optimieren. |

## Beispiele für Umleitungen auf Teilstrecken

Die folgenden Beispiele zeigen, wie Sie mithilfe verschiedener `paths` -Konfigurationsoptionen Teilroute-Umleitungen in der Datei `routes.yaml` angeben.

### Abgleich von regulärem Ausdrucksmuster

Verwenden Sie das folgende Format, um Umleitungsanfragen basierend auf einem regulären Ausdruck zu konfigurieren.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Diese Konfiguration filtert Anfragepfade für einen regulären Ausdruck und leitet übereinstimmende Anforderungen an `https://example.com` um. Beispielsweise wird eine Anforderung an `https://example.com/regexp/a/b/c/match` an `https://example.com/a/b/c` umgeleitet.

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

- Leitet Anforderungen, die dem Muster `/from` entsprechen, an den Pfad `http://{default}/to` um.

- Leitet Anforderungen, die dem Muster `/from/another/path` entsprechen, auf `https://{default}/to/another/path` um.

- Wenn Sie die Eigenschaft `prefix` in `false` ändern, werden Anforderungen, die mit dem Muster-Trigger `/from` übereinstimmen, zwar umgeleitet, Anforderungen, die mit dem Muster `/from/another/path` übereinstimmen, jedoch nicht.

### Suffix-Musterabgleich

Verwenden Sie das folgende Format, um Umleitungsanfragen zu konfigurieren, die das Pfadsuffix aus der Anfrage an das Zielziel anhängen:

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Diese Konfiguration funktioniert wie folgt:

- Leitet Anforderungen, die dem Muster `/from/path/suffix` entsprechen, an den Pfad `https://{default}/to` um.

- Wenn Sie die Eigenschaft `append_suffix` in `true` ändern, werden Anforderungen, die mit `/from/path/suffix` übereinstimmen, zum Pfad `https://{default}/to/path/suffix` umgeleitet.

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

- Umleitungen aus dem ersten Pfad (`/from`) werden einen Tag lang zwischengespeichert.

- Umleitungen vom zweiten Pfad (`/here`) werden zwei Wochen lang zwischengespeichert.
