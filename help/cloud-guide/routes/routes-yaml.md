---
title: Routen konfigurieren
description: Erfahren Sie, wie Sie die Routen für eingehende HTTPS-Anforderungen für die Adobe Commerce in Cloud-Infrastruktur-Umgebungen definieren.
feature: Cloud, Configuration, Routes
exl-id: a33797e5-14cc-45eb-a048-96180b872a4a
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Routen konfigurieren

Die `routes.yaml` in der Datei `.magento/routes.yaml` definiert Routen für Ihre Adobe Commerce in Cloud-Infrastruktur-Integrations-, Staging- und Produktionsumgebungen. Routen bestimmen, wie die Anwendung eingehende HTTP- und HTTPS-Anforderungen verarbeitet.

Die Standardeinstellung `routes.yaml` -Datei gibt die Routenvorlagen für die Verarbeitung von HTTP-Anfragen als HTTPS für Projekte an, die eine einzelne Standarddomäne aufweisen, und für Projekte, die für mehrere Domänen konfiguriert sind:

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

Verwenden Sie die `magento-cloud` CLI zum Anzeigen einer Liste der konfigurierten Routen:

```bash
magento-cloud environment:routes

+-------------------+----------+---------------+
| Route             | Type     | To            |
+-------------------+----------+---------------+
| http://{default}/ | upstream | mymagento     |
+-------------------+----------+---------------+
```

## Konfigurationsaktualisierungen für Pro-Umgebungen

{{pro-self-service-warning}}

## Routenvorlagen

Die `routes.yaml` -Datei ist eine Liste von Vorlagenrouten und deren Konfigurationen. Sie können die folgenden Platzhalter in Routenvorlagen verwenden:

- Die `{default}` Platzhalter stellt den qualifizierten Domänennamen dar, der als Standard für das Projekt konfiguriert wurde.

  Beispiel: ein Projekt mit der Standarddomäne `example.com` und den folgenden Routenvorlagen:

  ```text
  https://www.{default}/
  https://{default}/blog
  ```

  Diese Vorlagen werden in einer Produktionsumgebung zu den folgenden URLs aufgelöst:

  ```text
  https://www.example.com/
  https://example.com/blog
  ```

- Die `{all}` Platzhalter stellt alle Domänennamen dar, die für das Projekt konfiguriert sind.

  Beispiel: ein Projekt mit `example.com` und `example1.com` Domänen mit den folgenden Routenvorlagen:

  ```text
  https://www.{all}/
  
  https://{all}/blog
  ```

  Diese Vorlagen werden für alle Domänen im Projekt in die folgenden Routen aufgelöst:

  ```text
  https://www.example.com/
  
  https://www.example1.com/
  
  https://example.com/blog
  
  https://example1.com/blog
  ```

  Die `{all}` Platzhalter ist für Projekte nützlich, die für mehrere Domänen konfiguriert sind. In einer Nicht-Produktionszweig `{all}` wird durch die Projekt-ID und die Umgebungs-ID für jede Domäne ersetzt.

  Wenn für ein Projekt keine Domänen konfiguriert sind, was bei der Entwicklung üblich ist, wird die Variable `{all}` Platzhalter verhält sich genauso wie der `{default}` Platzhalter.

Adobe Commerce generiert außerdem Routen für jede aktive Integrationsumgebung. In Integrationsumgebungen wird die `{default}` Platzhalter wird durch den folgenden Domänennamen ersetzt:

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

Beispiel: die `refactorcss` -Verzweigung für `mswy7hzcuhcjw` Projekt, das im `us` Der Cluster weist die folgende Domäne auf:

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>Wenn Ihr Cloud-Projekt mehrere Stores unterstützt, befolgen Sie die Routenkonfigurationsanweisungen für [mehrere Websites oder Stores](../store/multiple-sites.md).

### Schrägstrich

Routendefinitionen enthalten einen Schrägstrich, der einen Ordner oder Ordner angibt. Derselbe Inhalt kann jedoch mit oder ohne Schrägstrich bedient werden. Die folgenden URLs lösen die gleichen auf, können jedoch als _zwei verschiedene_ URLs:

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>Es empfiehlt sich, einen Schrägstrich für Verzeichnisse zu verwenden. Bei jeder beliebigen Methode ist es jedoch wichtig, **konsistent bleiben** um zu vermeiden, dass zwei Standorte generiert werden.

## Routenprotokolle

Alle Umgebungen unterstützen automatisch sowohl HTTP als auch HTTPS.

- Wenn in der Konfiguration nur die HTTP-Route angegeben wird, werden automatisch HTTPS-Routen erstellt, sodass die Site sowohl über HTTP als auch über HTTPS bereitgestellt werden kann, ohne dass Umleitungen erforderlich sind.

  Beispiel: ein Projekt mit der Standarddomäne `example.com` und der folgenden Routenvorlage:

  ```text
  http://{default}/
  ```

  Diese Vorlage wird zu den folgenden URLs aufgelöst:

  ```text
  http://example.com/
  
  https://example.com/
  ```

- Wenn die Konfiguration nur die HTTPS-Route angibt, werden alle HTTP-Anforderungen zu HTTPS umgeleitet.

  Beispiel: ein Projekt mit der Standarddomäne `example.com` mit der folgenden Routenvorlage:

  ```text
  https://{default}/
  ```

  Diese Vorlage wird in die folgende URL aufgelöst:

  ```text
  https://example.com/
  ```

  Außerdem wird die folgende Umleitung verarbeitet:

  `http://example.com/` ==> `https://example.com/`

Servieren Sie alle Seiten über TLS. Für diese Konfiguration müssen Sie Umleitungen für alle unverschlüsselten Anforderungen mit einer der folgenden Methoden an die TLS-Entsprechung konfigurieren:

- Ändern Sie das Protokoll in HTTPS im `routes.yaml` -Datei.

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- Aktivieren Sie für Staging- und Produktionsumgebungen die [TLS schnell erzwingen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html) in der Admin-Benutzeroberfläche. Wenn Sie diese Option verwenden, wird die Umleitung zu HTTPS schnell verarbeitet, sodass Sie die `routes.yaml` Konfiguration.

## Routenoptionen

Konfigurieren Sie die einzelnen Routen separat mit den folgenden Eigenschaften:

| Eigenschaft | Beschreibung |
| ---------------- | ----------- |
| `type: upstream` | Stellt eine Anwendung bereit. Außerdem verfügt es über eine `upstream` -Eigenschaft, die den Namen der Anwendung angibt (wie in `.magento.app.yaml`), gefolgt von `:http` -Endpunkt. |
| `type: redirect` | Leitet zu einer anderen Route um. Danach folgt die `to` -Eigenschaft, bei der es sich um eine HTTP-Weiterleitung zu einer anderen Route handelt, die durch ihre Vorlage identifiziert wird. |
| `cache:` | Steuerelemente [Zwischenspeicherung für die Route](caching.md). |
| `redirects:` | Steuerelemente [Umleitungsregeln](redirects.md). |
| `ssi:` | Steuerelemente zur Aktivierung von [Serverseitige Includes](server-side-includes.md). |

## Einfache Routen

In den folgenden Beispielen routet die Routenkonfiguration die Apex-Domäne und die `www` Subdomäne an `mymagento` Anwendung. Diese Route leitet keine HTTPS-Anforderungen weiter.

**Beispiel 1:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: redirect
    to: "http://{default}/"
```

In diesem Beispiel folgt das Anfrage-Routing den folgenden Regeln:

- Der Server antwortet direkt auf Anfragen mit dem folgenden URL-Muster:

  ```text
  http://example.com/path
  ```

- Der Server gibt eine _301-Umleitung_ für Anforderungen mit dem folgenden URL-Muster:

  ```text
  http://www.example.com/mypath
  ```

  Diese Anfragen werden an die Apex-Domäne weitergeleitet, z. B.:

  ```text
  http://example.com/mypath
  ```

Im folgenden Beispiel leitet die Routenkonfiguration keine URLs von der Domäne www zur Apex-Domäne weiter. Stattdessen werden Anforderungen sowohl von der www- als auch von der apex-Domäne bereitgestellt.

**Beispiel 2:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: upstream
    upstream: "mymagento:http"
```

## Platzhalterrouten

Adobe Commerce in der Cloud-Infrastruktur unterstützt Platzhalterrouten, sodass Sie mehrere Subdomänen derselben Anwendung zuordnen können. Dies funktioniert bei Umleitungs- und Upstream-Routen. Der Route wird ein Sternchen (\*) vorangestellt. Beispielsweise werden die folgenden Routen zu derselben Anwendung geleitet:

- `*.example.com`
- `www.example.com`
- `blog.example.com`
- `us.example.com`

Dies dient als Sammeldomäne in einer Live-Umgebung.

### Routing einer nicht zugeordneten Domäne

Mit einem Punkt (`.`), um die Subdomain zu trennen.

**Beispiel:**

Ein Projekt mit `add-theme` -Zweig leitet zu der folgenden URL weiter:

```text
http://add-theme-projectID.us.magento.com/
```

Wenn Sie die folgende Routenvorlage definieren:

```text
http://www.{default}/
```

Die Route wird zu der folgenden URL aufgelöst:

```text
http://www.add-theme-projectID.us.magento.com/
```

Sie können jede Subdomäne einfügen, bevor der Punkt und die Route aufgelöst werden.

**Beispiel:**

Definieren Sie die folgende Routenvorlage:

```text
http://*.{default}/
```

Diese Vorlage löst beide der folgenden URLs auf:

```text
http://foo.add-theme-projectID.us.magentosite.cloud/
http://bar.add-theme-projectID.us.magentosite.cloud/
```

Sie können das Routenmuster für nicht zugeordnete Domänen anzeigen, indem Sie eine SSH-Verbindung zur Umgebung herstellen und die `magento-cloud` CLI zum Auflisten der Routen:

```terminal
web@mymagento.0:~$ vendor/bin/ece-tools env:config:show routes

Magento Cloud Routes:
+------------------------------------------+--------------------------------------------------------------+
| Route configuration                      | Value                                                        |
+------------------------------------------+--------------------------------------------------------------+
| http://www.add-theme-projectID.us.magento.com/:                                                         |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https:/{default}/                                            |
+------------------------------------------+--------------------------------------------------------------+
| https://*.add-theme-projectID.us.magentosite.cloud/:                                                    |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https://*.{default}/                                         |
+------------------------------------------+--------------------------------------------------------------+
```

## Umleitungen und Caching

Weitere Informationen finden Sie unter [Umleitungen](redirects.md)können Sie komplexe Umleitungsregeln verwalten, z. B. _partielle Umleitungen_ und Regeln für streckenbasierte [Zwischenspeicherung](caching.md):

```yaml
https://www.{default}/:
    type: redirect
    to: https://{default}/
https://{default}/:
    cache:
        cookies: [""]
        default_ttl: 0
        enabled: true
        headers:
            - Accept
            - Accept-Language
    ssi:
        enabled: false
    type: upstream
    upstream: mymagento:http
```
