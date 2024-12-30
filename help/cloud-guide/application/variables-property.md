---
title: Variablen-Eigenschaft
description: Verwenden Sie die Variableneigenschaft, um Speicherkonfigurationsoptionen für die Anwendung  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 5cd92fbb-8bff-48b1-9658-500140591344
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Variablen-Eigenschaft

Sie können anwendungsbasierte Umgebungsvariablen verwenden, um Store-Konfigurationen anzupassen. Diese Variablen verwenden eine bestimmte Syntax. Siehe [Konfigurationseinstellungen überschreiben](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) im _Konfigurationshandbuch_.

Die folgenden in der `.magento.app.yaml`-Datei enthaltenen Umgebungsvariablen sind für bestimmte Versionen des [!DNL Commerce]-Programms erforderlich.

Erforderlich für Adobe Commerce 2.2.x bis 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Legen Sie für Adobe Commerce 2.4.x die folgenden Variablen fest:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
