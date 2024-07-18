---
title: Variablen nach der Bereitstellung
description: Siehe die Liste der Umgebungsvariablen, die Aktionen in der Adobe Commerce in der Cloud-Infrastruktur nach der Bereitstellung steuern.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variablen nach der Bereitstellung

Die folgenden _Variablen nach der Bereitstellung_ steuern Aktionen in der Phase nach der Bereitstellung und können Werte von den [globalen Variablen](variables-global.md) übernehmen und überschreiben. Fügen Sie diese Variablen in die `post-deploy` -Phase der `.magento.env.yaml`-Datei ein:

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

Konfigurieren Sie den Test _Time to First Byte_ (TTFB) für bestimmte Seiten, um die Leistung Ihrer Site zu testen. Geben Sie für jede Seite, für die der Test erforderlich ist, einen absoluten Pfadverweis oder eine URL mit Protokoll und Host an.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

Nachdem Sie die Seiten angegeben haben, auf denen Ihre Änderungen getestet und übertragen werden sollen, wird der Test _Zeit bis Erstbyte_ in der Phase nach der Bereitstellung ausgeführt und die Ergebnisse für jeden Pfad zum Cloud-Protokoll werden veröffentlicht:

```
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

Bei umgeleiteten Pfaden zeigt das Protokoll den Pfad des Umleitungsziels anstelle des in der Umgebungsvariablen konfigurierten an. Wenn Sie einen ungültigen Pfad angeben, wird im Protokoll eine Warnmeldung angezeigt.

## `WARM_UP_CONCURRENCY`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Geben Sie die Begrenzung für gleichzeitige Anfragen an, die während der Cache-Warmup-Vorgänge gesendet werden sollen, um die Serverlast zu reduzieren. Dieser Wert begrenzt die Anzahl der parallelen Verbindungen und ist nützlich für Umgebungskonfigurationen, in denen die Variable `WARM_UP_PAGES` nach der Bereitstellung mehrere Seiten zum Vorausfüllen des Caches angibt.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Default**— `index.php`
- **Version**—Adobe Commerce 2.1.4 und höher

Passen Sie die Liste der Seiten an, die zum Vorausfüllen des Caches in der Phase &quot;`post_deploy`&quot;verwendet werden. Sie müssen den Hook nach der Bereitstellung konfigurieren. Siehe Abschnitt [Hooks](../application/hooks-property.md) der Datei `.magento.app.yaml` .

- **einzelne Seiten**: Geben Sie eine einzelne Seite an, die dem Cache hinzugefügt werden soll. Sie müssen nicht die Standard-Basis-URL angeben. Im folgenden Beispiel wird die Seite `BASE_URL/index.php` zwischengespeichert:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **multiple domains** - Auflisten mehrerer URLs. Im folgenden Beispiel werden Seiten aus zwei Domänen zwischengespeichert:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **multiple pages** - Verwenden Sie das folgende Format, um mehrere Seiten gemäß einem bestimmten Muster für reguläre Ausdrücke zwischenzuspeichern:

  ```
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: Mögliche Varianten `category`, `cms-page`, `product`, `store-page`
   - `pattern|url|product_sku`: Verwenden Sie ein `regexp` -Muster oder eine exakte Übereinstimmung `url`, um die URLs zu filtern, oder verwenden Sie ein Sternchen (\*) für alle Seiten. Verwenden der Produkt-SKU für den Entitätstyp `product`
   - `store_id|store_code`: Verwenden Sie die ID oder den Code des Stores oder ein Sternchen (\*) für alle Stores. Sie können mehrere Store-IDs oder Codes, getrennt durch `|`, übergeben.

  Im folgenden Beispiel werden basierend auf diesen Kriterien für die Entitätstypen `category` und `cms-page` zwischengespeichert:
   - alle Kategorieseiten für Speicher mit ID `1`
   - alle Kategorieseiten für Stores mit Code `store1` und `store2`
   - Kategorieseite `cars` für Speicher mit Code `store_en`
   - cms page `contact` für alle Stores
   - cms page `contact` für Stores mit ID `1` und `2`
   - Jede Kategorieseite, die `car_` enthält und bei Speicher mit ID 2 mit `html` endet
   - jede Kategorieseite, die `tires_` für den Store mit Code `store_gb` enthält

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

  Im folgenden Beispiel werden basierend auf diesen Kriterien für den Entitätstyp `product` zwischengespeichert:
   - alle Produkte für alle Stores (programmgesteuert auf 100 pro Store beschränkt, um Leistungsprobleme zu vermeiden)
   - alle Produkte für den Store `store1`
   - Produkte mit `sku1` für alle Geschäfte
   - Produkte mit `sku1` für Geschäfte mit Code `store1` und `store2`
   - Produkte mit `sku1`, `sku2` und `sku3` für Geschäfte mit Code `store1` und `store2`

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

  Im folgenden Beispiel werden basierend auf diesen Kriterien für den Entitätstyp `store-page` zwischengespeichert:
   - Seite `/contact-us` für alle Stores
   - Seite `/contact-us` für Speicher mit ID `1`
   - Seite `/contact-us` für Stores mit Code `code1` und `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
