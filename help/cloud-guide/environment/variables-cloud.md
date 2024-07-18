---
title: Cloud-spezifische Variablen
description: Sehen Sie sich eine Liste der für Adobe Commerce spezifischen Umgebungsvariablen in der Cloud-Infrastruktur an.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Cloud-spezifische Variablen

Umgebungsvariablen, die für Adobe Commerce in der Cloud-Infrastruktur spezifisch sind, verwenden das Präfix `MAGENTO_CLOUD_*`:

| Variable | Beschreibung |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Der absolute Pfad zum Anwendungsverzeichnis. |
| `MAGENTO_CLOUD_APPLICATION` | Ein base64-kodiertes JSON-Objekt, das die Anwendung beschreibt. Er wird dem Inhalt der Datei `.magento.app.yaml` zugeordnet und enthält Unterschlüssel. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | Der Name der in der Datei `.magento.app.yaml` konfigurierten Anwendung. |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Der absolute Pfad zum Webdokumentstamm, falls zutreffend. |
| `MAGENTO_CLOUD_ENVIRONMENT` | Der Name der Umgebungsverzweigung. |
| `MAGENTO_CLOUD_PROJECT` | Die Projekt-ID. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Ein base64-kodiertes JSON-Objekt, das die Endpunktdefinition für Schlüssel (Beziehungsname) und Wert (Arrays von Beziehungspaaren) darstellt. Jede Definition eines Beziehungs-Endpunkts ist eine dekomprimierte Form einer URL. Er hat einen `scheme`, einen `host`, einen `port` und _optional_ einen `username`, `password`, `path` und einige zusätzliche Informationen in `query`. |
| `MAGENTO_CLOUD_ROUTES` | Beschreiben Sie die in der Umgebungsdatei &quot;`.magento/routes.yaml`&quot; definierten Routen. |
| `MAGENTO_CLOUD_TREE_ID` | Die Baum-ID für die Anwendung, die der SHA des Baums in Git entspricht. |
| `MAGENTO_CLOUD_VARIABLES` | Ein base64-kodiertes JSON-Objekt mit Schlüssel-Wert-Paaren, z. B. `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | Stellt den Pfad zum Bereitstellungspunkt für den Sperranbieter in der Cloud-Infrastruktur bereit. Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. |

>[!WARNING]
>
>Um Umgebungsvariablen zu [Override configuration settings](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) mithilfe von [[!DNL Cloud Console]](../project/overview.md) hinzuzufügen, müssen Sie dem Variablennamen &quot;`env:`&quot;voranstellen, wie im folgenden Beispiel gezeigt:
>
>![Beispiel für Umgebungsvariable](../../assets/set-env-variable-ui.png)

Da sich Werte im Laufe der Zeit ändern können, ist es am besten, die Variable zur Laufzeit zu überprüfen und sie zur Konfiguration Ihrer Anwendung zu verwenden. Verwenden Sie beispielsweise die Variable `MAGENTO_CLOUD_RELATIONSHIPS` , um umgebungsbezogene Beziehungen wie folgt abzurufen:

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

Sie können den Befehl `env:config:show` aus [dem `ece-tools` -Paket](../dev-tools/package-overview.md) verwenden, um eine Liste der Variablen für die aktuelle Umgebung anzuzeigen.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Beispielausgabe für die Option `variables` :

```
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
