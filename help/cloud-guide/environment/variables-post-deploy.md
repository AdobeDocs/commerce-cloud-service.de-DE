---
title: Variablen nach der Bereitstellung
description: Siehe die Liste der Umgebungsvariablen, die Aktionen in der Adobe Commerce in der Cloud-Infrastruktur nach der Bereitstellung steuern.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: 8b02757591c4e8f607e936de4eda74d76953d9b7
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variablen nach der Bereitstellung

Die folgenden _nach der Bereitstellung_ Variablen steuern Aktionen in der Phase nach der Bereitstellung und können Werte von der [Globale Variablen](variables-global.md). Fügen Sie diese Variablen in die `post-deploy` der `.magento.env.yaml` Datei:

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

Weitere Informationen zum Anpassen des Build- und Bereitstellungsprozesses finden Sie unter

- [Bereitstellungskonfiguration](configure-env-yaml.md)
- [Bereitstellungsprozess](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **Standard**— `[]` (ein leeres Array)
- **Version**—Adobe Commerce 2.1.4 und höher

Konfigurieren _Zeit bis zum ersten Byte_ (TTFB) Tests auf bestimmte Seiten, um die Leistung Ihrer Site zu testen. Geben Sie für jede Seite, für die der Test erforderlich ist, einen absoluten Pfadverweis oder eine URL mit Protokoll und Host an.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

Nachdem Sie die Seiten angegeben haben, die getestet und übertragen werden sollen, wird die _Zeit bis zum ersten Byte_ Der Test wird in der Phase nach der Bereitstellung ausgeführt und die Ergebnisse für jeden Pfad zum Cloud-Protokoll werden veröffentlicht:

```terminal
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

Bei umgeleiteten Pfaden zeigt das Protokoll den Pfad des Umleitungsziels anstelle des in der Umgebungsvariablen konfigurierten an. Wenn Sie einen ungültigen Pfad angeben, wird im Protokoll eine Warnmeldung angezeigt.

## `WARM_UP_CONCURRENCY`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Geben Sie die Begrenzung für gleichzeitige Anfragen an, die während der Cache-Warmup-Vorgänge gesendet werden sollen, um die Serverlast zu reduzieren. Dieser Wert begrenzt die Anzahl der parallelen Verbindungen und ist für Umgebungskonfigurationen nützlich, in denen die Variable `WARM_UP_PAGES` Variable nach der Bereitstellung gibt mehrere Seiten für das Vorausfüllen des Caches an.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Standard**— `index.php`
- **Version**—Adobe Commerce 2.1.4 und höher

Anpassen der Liste der Seiten, die zum Vorausfüllen des Cache im `post_deploy` Bühne. Sie müssen den Hook nach der Bereitstellung konfigurieren. Siehe [Hooks-Abschnitt](../application/hooks-property.md) des `.magento.app.yaml` -Datei.

- **Einzelseiten**—Geben Sie eine einzelne Seite an, die dem Cache hinzugefügt werden soll. Sie müssen nicht die Standard-Basis-URL angeben. Im folgenden Beispiel wird die `BASE_URL/index.php` Seite:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **mehrere Domänen**—Mehrere URLs auflisten. Im folgenden Beispiel werden Seiten aus zwei Domänen zwischengespeichert:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **mehrere Seiten**—Verwenden Sie das folgende Format, um mehrere Seiten gemäß einem bestimmten Muster für reguläre Ausdrücke zwischenzuspeichern:

  ```terminal
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: Mögliche Varianten `category`, `cms-page`, `product`, `store-page`
   - `pattern|url|product_sku`: Verwenden Sie eine `regexp` Muster oder exakte Übereinstimmung `url` , um die URLs zu filtern, oder verwenden Sie ein Sternchen (\*) für alle Seiten. Verwenden Sie die Produkt-SKU für die `product` Entitätstyp
   - `store_id|store_code`: Verwenden Sie die ID oder den Code des Stores oder ein Sternchen (\*) für alle Stores. Sie können mehrere Store-IDs oder Codes übergeben, die durch `|`

  Im folgenden Beispiel wird für `category` und `cms-page` Entitätstypen basierend auf diesen Kriterien:
   - alle Kategorieseiten mit ID speichern `1`
   - alle Kategorieseiten für Stores mit Code `store1` und `store2`
   - Kategorieseite `cars` zum Speichern mit Code `store_en`
   - cms-Seite `contact` für alle Geschäfte
   - cms-Seite `contact` für Stores mit ID `1` und `2`
   - jede Kategorieseite, die `car_` und endet mit `html` für Speicher mit ID 2
   - jede Kategorieseite, die `tires_` zum Speichern mit Code `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  Im folgenden Beispiel werden für die `product` Entitätstyp basierend auf diesen Kriterien:
   - alle Produkte für alle Stores (programmgesteuert auf 100 pro Store beschränkt, um Leistungsprobleme zu vermeiden)
   - alle Produkte für den Store `store1`
   - Produkte mit `sku1` für alle Geschäfte
   - Produkte mit `sku1` für Stores mit Code `store1` und `store2`
   - Produkte mit `sku1`, `sku2` und `sku3` für Stores mit Code `store1` und `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  Im folgenden Beispiel werden für die `store-page` Entitätstyp basierend auf diesen Kriterien:
   - page `/contact-us` für alle Geschäfte
   - page `/contact-us` für Store mit ID `1`
   - page `/contact-us` für Stores mit Code `code1` und `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
