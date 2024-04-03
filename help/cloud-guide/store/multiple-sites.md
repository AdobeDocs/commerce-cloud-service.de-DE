---
title: Einrichten mehrerer Websites oder Stores
description: Erfahren Sie, wie Sie mehrere Websites oder Stores für Adobe Commerce in der Cloud-Infrastruktur konfigurieren.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Einrichten mehrerer Websites oder Stores

Sie können Adobe Commerce so konfigurieren, dass es über mehrere Websites oder Stores verfügt, z. B. einen englischen Store, einen französischen Store und einen deutschen Store. Siehe [Grundlegendes zu Websites, Geschäften und Store-Ansichten](best-practices.md#store-views).

>[!WARNING]
>
>Die Katalogdaten werden mit der Erhöhung der Anzahl der Websites und Stores erweitert. Abhängig von Ihrer Projektarchitektur können die zusätzlichen Stores zu einem längeren Indizierungsprozess und langsameren Reaktionszeiten für nicht zwischengespeicherte Katalogseiten führen. Adobe empfiehlt, dass Sie die Site-Leistung genau überwachen.

Die Einrichtung mehrerer Stores hängt davon ab, ob Sie eindeutige oder freigegebene Domänen verwenden.

Mehrere Stores mit eindeutigen Domänen:

```terminal
https://first.store.com/
https://second.store.com/
```

Mehrere Stores mit derselben Domäne:

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Um der Site-Basis-URL eine Store-Ansicht hinzuzufügen, müssen Sie nicht mehrere Verzeichnisse erstellen. Siehe [Hinzufügen des Store-Codes zur Basis-URL](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) im _Konfigurationshandbuch_.

## Domänen hinzufügen

Benutzerdefinierte Domänen können zu Pro Staging- und beliebigen Produktionsumgebungen hinzugefügt werden. Sie können nicht zu Integrationsumgebungen hinzugefügt werden.

Der Prozess zum Hinzufügen einer Domäne hängt vom Typ des Cloud-Kontos ab:

- Für Pro Staging und Produktion

  Fügen Sie die neue Domäne zu Fastly hinzu, siehe [Domänen verwalten](../cdn/fastly-custom-cache-configuration.md#manage-domains)oder ein Support-Ticket öffnen, um Unterstützung anzufordern. Darüber hinaus müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um neue Domänen anzufordern, die einem Cluster hinzugefügt werden sollen.

- Nur für Starterproduktion

  Fügen Sie die neue Domäne zu Fastly hinzu, siehe [Domänen verwalten](../cdn/fastly-custom-cache-configuration.md#manage-domains)oder [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) um Hilfe zu ersuchen. Darüber hinaus müssen Sie die neue Domäne zum **Domänen** im [!DNL Cloud Console]: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Lokale Installation konfigurieren

Informationen zum Konfigurieren der lokalen Installation für die Verwendung mehrerer Stores finden Sie unter [Mehrere Websites oder Stores][config-multiweb] im _Konfigurationshandbuch_.

Nachdem Sie die lokale Installation erfolgreich erstellt und getestet haben, um mehrere Stores zu verwenden, müssen Sie Ihre Integrationsumgebung vorbereiten:

1. **Konfigurieren von Routen oder Orten**—spezifizieren, wie eingehende URLs von Adobe Commerce verarbeitet werden

   - [Routen für separate Domänen](#configure-routes-for-separate-domains)
   - [Speicherorte für freigegebene Domänen](#configure-locations-for-shared-domains)

1. **Einrichten von Websites, Geschäften und Speichern von Ansichten**—konfigurieren Sie die Adobe Commerce Admin-Benutzeroberfläche
1. **Variablen ändern**—geben Sie die Werte der `MAGE_RUN_TYPE` und `MAGE_RUN_CODE` Variablen in `magento-vars.php` file
1. **Bereitstellen und Testen von Umgebungen**—stellen und testen Sie die `integration` Verzweigung

>[!TIP]
>
>Sie können eine lokale Umgebung verwenden, um mehrere Websites oder Stores einzurichten. Siehe Cloud Docker-Anweisungen unter [Einrichten mehrerer Websites oder Stores](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Konfigurationsaktualisierungen für Pro-Umgebungen

{{pro-self-service-warning}}

### Routen für separate Domänen konfigurieren

Routen definieren, wie eingehende URLs verarbeitet werden. Bei mehreren Stores mit eindeutigen Domänen müssen Sie jede Domäne im `routes.yaml` -Datei. Wie Sie Routen konfigurieren, hängt davon ab, wie Ihre Site funktionieren soll.

**So konfigurieren Sie Routen in einer Integrationsumgebung**:

1. Öffnen Sie auf Ihrer lokalen Workstation die `.magento/routes.yaml` in einem Texteditor.

1. Definieren Sie die Domäne und Subdomänen. Die `mymagento` Upstream value ist derselbe Wert wie die name -Eigenschaft in `.magento.app.yaml` -Datei.

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Speichern Sie Ihre Änderungen in der `routes.yaml` -Datei.

1. Weiter zu [Einrichten von Websites, Geschäften und Speichern von Ansichten](#set-up-websites-stores-and-store-views).

### Orte für freigegebene Domänen konfigurieren

Wenn die Routenkonfiguration definiert, wie die URLs verarbeitet werden, wird die `web` -Eigenschaft in der `.magento.app.yaml` definiert, wie Ihre Anwendung im Internet verfügbar gemacht wird. Web _locations_ mehr Granularität für eingehende Anforderungen. Wenn Ihre Domäne beispielsweise `store.com`, können Sie `/first` (Standardsite) und `/second` für Anfragen an zwei verschiedene Stores, die eine Domäne teilen.

**So konfigurieren Sie einen neuen Webspeicherort**:

1. Erstellen Sie einen Alias für den Stamm (`/`). In diesem Beispiel lautet der Alias `&app` in Zeile 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Erstellen Sie einen Pass-Through für die Website (`/website`) und referenzieren Sie mithilfe des Alias aus dem vorherigen Schritt den Stamm.

   Der Alias ermöglicht Folgendes: `website` , um auf Werte vom Stammspeicherort zuzugreifen. In diesem Beispiel wird die Website `passthru` ist online 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**So konfigurieren Sie einen Speicherort mit einem anderen Ordner**:

1. Erstellen Sie einen Alias für den Stamm (`/`) und für das statische (`/static`).

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Erstellen Sie ein Unterverzeichnis für die Website unter der `pub` directory: `pub/<website>`

1. Kopieren Sie die `pub/index.php` in die `pub/<website>` und aktualisieren Sie das `bootstrap` path (`/../../app/bootstrap.php`).

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Erstellen Sie einen Pass-Through für die `index.php` -Datei.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Übernehmen und pushen Sie die geänderten Dateien.

   - `pub/<website>/index.php` (Wenn diese Datei in `.gitignore`, kann die Push-Benachrichtigung die Force-Option erfordern.)
   - `.magento.app.yaml`

### Einrichten von Websites, Geschäften und Speichern von Ansichten

Im _Admin-Benutzeroberfläche_, richten Sie Adobe Commerce ein. **Websites**, **Stores**, und **Store-Ansichten**. Siehe [Einrichten mehrerer Websites, Stores und Speichern von Ansichten im Admin](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) im _Konfigurationshandbuch_.

Es ist wichtig, bei der Einrichtung Ihrer lokalen Installation denselben Namen und Code Ihrer Websites, Stores und Ansichten von Ihrem Administrator zu verwenden. Sie benötigen diese Werte, wenn Sie die `magento-vars.php` -Datei.

### Variablen ändern

Übergeben Sie anstelle der Konfiguration eines virtuellen NGINX-Hosts die `MAGE_RUN_CODE` und `MAGE_RUN_TYPE` Variablen, die `magento-vars.php` -Datei in Ihrem Stammverzeichnis des Projekts.

**So übergeben Sie Variablen mithilfe der `magento-vars.php` file**:

1. Öffnen Sie die `magento-vars.php` in einem Texteditor.

   Die [default `magento-vars.php` file](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) sollte wie folgt aussehen:

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. Kommentar verschieben `if` blockieren, damit _after_ die `function` und nicht mehr kommentiert.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Ersetzen Sie die folgenden Werte in der `if (isHttpHost("example.com"))` block:
   - `example.com`—mit der Basis-URL Ihrer _website_
   - `default`—mit dem eindeutigen CODE für Ihre _website_ oder _Store-Ansicht_
   - `store`—mit einem der folgenden Werte:
      - `website`—laden Sie die _website_ in der Storefront
      - `store`—laden Sie eine _Store-Ansicht_ in der Storefront

   Für mehrere Sites mit eindeutigen Domänen:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   Bei mehreren Sites mit derselben Domäne müssen Sie die _Host_ und _URI_:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Speichern Sie Ihre Änderungen in der `magento-vars.php` -Datei.

### Bereitstellen und Testen auf dem Integrationsserver

Übertragen Sie Ihre Änderungen in die Adobe Commerce-Integrationsumgebung der Cloud-Infrastruktur und testen Sie Ihre Site.

1. Fügen Sie Änderungen am Remote-Zweig hinzu, übertragen Sie diese und fügen Sie sie per Push-Benachrichtigung hinzu.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Warten Sie, bis die Bereitstellung abgeschlossen ist.

1. Öffnen Sie nach der Bereitstellung Ihre Store-URL in einem Webbrowser.

   Verwenden Sie für eine eindeutige Domäne das folgende Format: `http://<magento-run-code>.<site-URL>`

   Beispiel: `http://french.master-name-projectID.us.magentosite.cloud/`

   Bei einer freigegebenen Domäne verwenden Sie folgendes Format: `http://<site-URL>/<magento-run-code>`

   Beispiel: `http://master-name-projectID.us.magentosite.cloud/french/`

1. Testen Sie Ihre Site gründlich und führen Sie den Code mit dem `integration` -Verzweigung für eine weitere Bereitstellung.

## Bereitstellen in Staging und Produktion

Befolgen Sie den Implementierungsprozess für [Bereitstellung in Staging und Produktion](../deploy/staging-production.md). Für Starter- und Pro-Umgebungen verwenden Sie die [!DNL Cloud Console] , um Code über Umgebungen hinweg zu pushen.

Adobe empfiehlt vollständige Tests in der Staging-Umgebung, bevor sie an die Produktionsumgebung gesendet wird. Nehmen Sie Code-Änderungen in der Integrationsumgebung vor und starten Sie den Prozess zur erneuten Bereitstellung in allen Umgebungen.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
