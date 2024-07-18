---
title: Routen konfigurieren
description: Erfahren Sie, wie Sie die Routen für eingehende HTTPS-Anforderungen für die Adobe Commerce in Cloud-Infrastruktur-Umgebungen definieren.
feature: Cloud, Configuration, Routes
exl-id: a33797e5-14cc-45eb-a048-96180b872a4a
source-git-commit: c39332d352f6dcb6f92c312a6ef1b74319d37aa3
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Routen konfigurieren

Die Datei &quot;`routes.yaml`&quot;im Ordner &quot;`.magento/routes.yaml`&quot;definiert Routen für Ihre Adobe Commerce in Cloud-Infrastruktur-Integrations-, Staging- und Produktionsumgebungen. Routen bestimmen, wie die Anwendung eingehende HTTP- und HTTPS-Anforderungen verarbeitet.

Die standardmäßige `routes.yaml` -Datei gibt die Routenvorlagen für die Verarbeitung von HTTP-Anfragen als HTTPS für Projekte an, die eine einzige Standarddomäne haben, und für Projekte, die für mehrere Domänen konfiguriert sind:

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

Verwenden Sie die CLI `magento-cloud` , um eine Liste der konfigurierten Routen anzuzeigen:

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

Die Datei &quot;`routes.yaml`&quot; ist eine Liste mit Vorlagenrouten und ihren Konfigurationen. Sie können die folgenden Platzhalter in Routenvorlagen verwenden:

- Der Platzhalter `{default}` stellt den qualifizierten Domänennamen dar, der als Standard für das Projekt konfiguriert wurde.

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

- Der Platzhalter `{all}` stellt alle für das Projekt konfigurierten Domänennamen dar.

  Beispiel: ein Projekt mit den Domänen `example.com` und `example1.com` mit den folgenden Routenvorlagen:

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

  Der Platzhalter `{all}` ist für Projekte nützlich, die für mehrere Domänen konfiguriert sind. In einer Nicht-Produktions-Verzweigung wird `{all}` durch die Projekt-ID und die Umgebungs-ID für jede Domäne ersetzt.

  Wenn für ein Projekt keine Domänen konfiguriert sind, was bei der Entwicklung üblich ist, verhält sich der Platzhalter `{all}` genauso wie der Platzhalter `{default}` .

Adobe Commerce generiert außerdem Routen für jede aktive Integrationsumgebung. In Integrationsumgebungen wird der Platzhalter `{default}` durch den folgenden Domänennamen ersetzt:

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

Die Verzweigung `refactorcss` für das im `us`-Cluster gehostete `mswy7hzcuhcjw`-Projekt weist beispielsweise die folgende Domäne auf:

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>Wenn Ihr Cloud-Projekt mehrere Stores unterstützt, befolgen Sie die Routenkonfigurationsanweisungen für [mehrere Websites oder Stores](../store/multiple-sites.md).

### Schrägstrich

Routendefinitionen enthalten einen Schrägstrich, der einen Ordner oder Ordner angibt. Derselbe Inhalt kann jedoch mit oder ohne Schrägstrich bedient werden. Die folgenden URLs lösen die gleichen auf, können jedoch als _zwei verschiedene_ URLs interpretiert werden:

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>Es empfiehlt sich, einen Schrägstrich für Verzeichnisse zu verwenden. Bei jeder beliebigen Methode ist es jedoch wichtig, **konsistent zu bleiben**, um zu verhindern, dass zwei Speicherorte generiert werden.

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

- Ändern Sie das Protokoll in der Datei `routes.yaml` in HTTPS.

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- Aktivieren Sie für Staging- und Produktionsumgebungen die Option [TLS auf Schnell erzwingen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html) in der Admin-Benutzeroberfläche. Wenn Sie diese Option verwenden, verarbeitet die Umleitung schnell zu HTTPS, sodass Sie die `routes.yaml` -Konfiguration nicht aktualisieren müssen.

## Routenoptionen

Konfigurieren Sie die einzelnen Routen separat mit den folgenden Eigenschaften:

| Eigenschaft | Beschreibung |
| ---------------- | ----------- |
| `type: upstream` | Stellt eine Anwendung bereit. Außerdem verfügt es über eine Eigenschaft `upstream` , die den Namen der Anwendung (wie in `.magento.app.yaml` definiert) gefolgt vom Endpunkt `:http` angibt. |
| `type: redirect` | Leitet zu einer anderen Route um. Anschließend folgt die Eigenschaft `to` , bei der es sich um eine HTTP-Weiterleitung zu einer anderen durch die Vorlage identifizierten Route handelt. |
| `cache:` | Steuert die [Zwischenspeicherung für die Route](caching.md). |
| `redirects:` | Steuert [Umleitungsregeln](redirects.md). |
| `ssi:` | Steuerelemente zum Aktivieren von [Server Side Includes](server-side-includes.md). |

## Einfache Routen

In den folgenden Beispielen leitet die Routenkonfiguration die Apex-Domäne und die `www`-Subdomäne an die `mymagento`-Anwendung weiter. Diese Route leitet keine HTTPS-Anforderungen weiter.

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

- Der Server gibt für Anfragen mit dem folgenden URL-Muster eine Umleitung _301_ aus:

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

Sie können über einen Punkt (`.`) zu einem System weiterleiten, das keiner Domäne zugeordnet ist, um die Subdomain zu trennen.

**Beispiel:**

Ein Projekt mit dem Zweig `add-theme` leitet zu der folgenden URL weiter:

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

Sie können das Routenmuster für nicht zugeordnete Domänen anzeigen, indem Sie eine SSH-Verbindung zur Umgebung herstellen und die Routen mithilfe der CLI `magento-cloud` auflisten:

```bash
vendor/bin/ece-tools env:config:show routes

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

Wie ausführlicher unter [Umleitungen](redirects.md) erläutert, können Sie komplexe Umleitungsregeln verwalten, wie z. B. _partielle Umleitungen_, und Regeln für die routen basierten [Caching](caching.md) festlegen:

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
