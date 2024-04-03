---
title: Entwicklungsübersicht
description: Bereiten Sie sich auf die lokale Entwicklung mit einem Adobe Commerce-Projekt zur Cloud-Infrastruktur vor.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Entwicklungsübersicht

Adobe Commerce in Remote-Umgebungen der Cloud-Infrastruktur **Schreibgeschützt**, einschließlich aller Starter-Umgebungen und aller Pro-Integration-, Staging- und Produktionsumgebungen. In einer lokalen Entwicklungsumgebung können Sie Code schreiben und testen, bevor Sie ihn in eine Integrationsumgebung senden, um weitere Tests und Implementierungen in Staging und Produktion durchzuführen.

Stellen Sie vor der Vorbereitung Ihres lokalen Arbeitsbereichs sicher, dass Sie über [Anmeldeinformationen](../../get-started/prepare-workspace.md). Die lokale Entwicklung erfordert die Installation von PHP und Composer, es sei denn, Sie entscheiden sich für die Verwendung von [Cloud Docker für Commerce](#docker-environment).

## Erforderliche Pakete

Adobe Commerce on Cloud Infrastructure verwendet Composer zum Verwalten der Abhängigkeiten und Upgrades für Projekte. Für die lokale Entwicklung müssen Sie die PHP- und Composer-Versionen installieren, die mit Ihrem Cloud-Projekt kompatibel sind. Wenn Sie beispielsweise die [!DNL Commerce] 2.4.6 Cloud-Vorlage können Sie sehen, dass die [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.6/.magento.app.yaml) Konfigurationsdatei verwendet **PHP 8.2** und **Verfasser 2.2.21**.

Der Composer installiert die erforderlichen Bibliotheken und Abhängigkeiten für Ihr Projekt im `vendor` Verzeichnis. Die folgenden erforderlichen Composer-Dateien befinden sich im Projektstammordner:

- `composer.json`—Verwenden Sie die `composer.json` -Datei, um Produktaninstallationen und -aktualisierungen zu verwalten.
- `composer.lock`—Die `composer.lock` -Datei speichert eine Reihe exakter Versionsabhängigkeiten, die die Versionsbegrenzungen jeder Anforderung für jedes Paket in der Abhängigkeitsstruktur des Projekts erfüllen.

**Allgemeine Befehle:**

| Befehl | Beschreibung |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Aktualisierungen der neuesten Versionen der Abhängigkeiten, die in der `composer.json` -Datei. Dadurch wird die `composer.lock` -Datei. |
| `composer install` | Liest die `composer.lock` -Datei, um Abhängigkeiten herunterzuladen. Es empfiehlt sich, eine aktuelle Kopie von `composer.lock` in Ihrem Projekt-Repository. |

{style="table-layout:auto"}

Nachdem Sie den aktualisierten Code hinzugefügt, übertragen und gepusht haben, wird bei der Bereitstellung automatisch die `composer install` -Befehl während der [Build-Phase](../deploy/process.md#build-phase-build-phase).

### Cloud-Metapaket

Adobe Commerce in der Cloud-Infrastruktur verwendet ein Metapaket, das `magento/product-enterprise-edition`. Verwenden Sie die folgende Einschränkungssyntax, um die neuesten Updates für die neueste Version von Commerce zu erhalten:

```text
>=current_version <next_version
```

Wenn Sie beispielsweise die neueste Adobe Commerce-Version 2.4.5 verwenden möchten, legen Sie `2.4.5` als &quot;aktuelle&quot;Version und `2.4.6` als &quot;nächste&quot;Version in der `composer.json` Datei:

```text
"magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
```

Die Hauptpakete dieses Metapakets sind:

- **vendor/magento/ece-tools**—Die `ece-tools` Das -Paket ist mit Adobe Commerce-Version 2.1.4 und höher kompatibel, um eine Vielzahl von Funktionen bereitzustellen, mit denen Sie Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur verwalten können. Es enthält Skripte und Adobe Commerce zu Cloud-Infrastrukturbefehlen, die Sie bei der Verwaltung Ihres Codes und der automatischen Erstellung und Bereitstellung Ihrer Projekte unterstützen. Siehe [`ece-tools` Paketübersicht](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition**—Dieses Metapaket erfordert Anwendungskomponenten, einschließlich Modulen, Frameworks, Designs und mehr.
- **vendor/fastly2/magento2**—Dieses Modul verwaltet das Fastly CDN und die Services für die Produktions- und Produktionsumgebungen von Pro Staging und Starter. Siehe [Schnelldienste](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-paypal-on-boarding**—Dieses Modul bietet PayPal Payment Gateway Checkout, indem es mit Ihrem PayPal-Handelskonto verbunden wird. Siehe [PayPal-Onboarding-Tool](../store/paypal.md).

>[!TIP]
>
>Siehe [Cloud-Pakete für Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) im _Commerce-Versionshinweise_ für eine Liste von Abhängigkeiten und Drittanbieterlizenzen.

## Docker-Umgebung

Sie können das Cloud Docker für Commerce-Tool verwenden, um die Adobe Commerce in Cloud-Infrastruktur-Produktions- und Entwicklungsumgebungen für die lokale Entwicklung zu emulieren. Cloud Docker für Commerce erfordert keine lokale Installation von PHP und Composer.

- [Lokale Entwicklung mit Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) auf der Adobe Developer-Site
- [Docker-Architektur und allgemeine Befehle](../dev-tools/cloud-docker.md)
- [Cloud Docker - Versionshinweise](../release-notes/cloud-docker.md)

>[!TIP]
>
>Informationen zur Verwendung von Git-basierten Hosting-Diensten mit Adobe Commerce in der Cloud-Infrastruktur finden Sie unter [Integrationen](../integrations/overview.md).
