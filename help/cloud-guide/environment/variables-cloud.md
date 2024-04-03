---
title: Cloud-spezifische Variablen
description: Sehen Sie sich eine Liste der für Adobe Commerce spezifischen Umgebungsvariablen in der Cloud-Infrastruktur an.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Cloud-spezifische Variablen

Umgebungsvariablen, die für Adobe Commerce in der Cloud-Infrastruktur spezifisch sind, verwenden die `MAGENTO_CLOUD_*` prefix:

| Variable | Beschreibung |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Der absolute Pfad zum Anwendungsverzeichnis. |
| `MAGENTO_CLOUD_APPLICATION` | Ein base64-kodiertes JSON-Objekt, das die Anwendung beschreibt. Er wird dem `.magento.app.yaml` Dateiinhalt und enthält Unterschlüssel. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | Der Name der Anwendung, der im `.magento.app.yaml` -Datei. |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Der absolute Pfad zum Webdokumentstamm, falls zutreffend. |
| `MAGENTO_CLOUD_ENVIRONMENT` | Der Name der Umgebungsverzweigung. |
| `MAGENTO_CLOUD_PROJECT` | Die Projekt-ID. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Ein base64-kodiertes JSON-Objekt, das die Endpunktdefinition für Schlüssel (Beziehungsname) und Wert (Arrays von Beziehungspaaren) darstellt. Jede Definition eines Beziehungs-Endpunkts ist eine dekomprimierte Form einer URL. Es hat eine `scheme`, a `host`, a `port`, und _optional_ a `username`, `password`, `path`sowie einige zusätzliche Informationen in `query`. |
| `MAGENTO_CLOUD_ROUTES` | Beschreiben der in der Umgebung definierten Routen `.magento/routes.yaml` -Datei. |
| `MAGENTO_CLOUD_TREE_ID` | Die Baum-ID für die Anwendung, die der SHA des Baums in Git entspricht. |
| `MAGENTO_CLOUD_VARIABLES` | Ein base64-kodiertes JSON-Objekt mit Schlüssel-Wert-Paaren, z. B. `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | Stellt den Pfad zum Bereitstellungspunkt für den Sperranbieter in der Cloud-Infrastruktur bereit. Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. |

>[!WARNING]
>
>Hinzufügen von Umgebungsvariablen zu [Konfigurationseinstellungen überschreiben](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) mithilfe der [[!DNL Cloud Console]](../project/overview.md), müssen Sie dem Variablennamen `env:` wie im folgenden Beispiel:
>
>![Beispiel für Umgebungsvariable](../../assets/set-env-variable-ui.png)

Da sich Werte im Laufe der Zeit ändern können, ist es am besten, die Variable zur Laufzeit zu überprüfen und sie zur Konfiguration Ihrer Anwendung zu verwenden. Verwenden Sie beispielsweise die `MAGENTO_CLOUD_RELATIONSHIPS` zum Abrufen von umgebungsbezogenen Beziehungen wie folgt:

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## Anzeigen von Umgebungsvariablen

Sie können die `env:config:show` Befehl von [die `ece-tools` package](../dev-tools/package-overview.md) um eine Liste der Variablen für die aktuelle Umgebung anzuzeigen.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Beispielausgabe für die `variables` Option:

```terminal
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
