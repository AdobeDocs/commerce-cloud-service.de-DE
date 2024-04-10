---
title: Entwicklungsübersicht
description: Bereiten Sie sich mit einem Adobe Commerce on Cloud-Infrastrukturprojekt auf die lokale Entwicklung vor.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Entwicklungsübersicht

Remote-Umgebungen von Adobe Commerce auf Cloud-Infrastrukturen sind **Schreibgeschützt**, einschließlich aller Starter-Umgebungen und aller Pro-Integrations-, Staging- und Produktionsumgebungen. In einer lokalen Entwicklungsumgebung können Sie Code schreiben und testen, bevor Sie ihn in eine Integrationsumgebung pushen, um weitere Tests durchzuführen und ihn in der Staging- und Produktionsumgebung bereitzustellen.

Stellen Sie vor der Vorbereitung Ihres lokalen Arbeitsbereichs sicher, dass Sie über Folgendes verfügen [Anmeldedaten](../../get-started/prepare-workspace.md). Lokale Entwicklung erfordert die Installation von PHP und Composer, es sei denn, Sie entscheiden sich für die Verwendung [Cloud Docker für Commerce](#docker-environment).

## Erforderliche Pakete

Adobe Commerce in der Cloud-Infrastruktur verwendet Composer, um die Abhängigkeiten und Upgrades für Projekte zu verwalten. Für die lokale Entwicklung müssen Sie die PHP- und Composer-Versionen installieren, die mit Ihrem Cloud-Projekt kompatibel sind. Wenn Sie beispielsweise den [!DNL Commerce] 2.4.7 Cloud-Vorlage ist zu sehen, dass die [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) Konfigurationsdatei verwendet **PHP 8.3** und **Composer 2.7.2**.

Composer installiert die erforderlichen Bibliotheken und Abhängigkeiten für Ihr Projekt im `vendor` Verzeichnis. Die folgenden erforderlichen Composer-Dateien befinden sich im Stammverzeichnis des Projekts:

- `composer.json`—Verwenden Sie die `composer.json` Datei zum Verwalten von Produktinstallationen und Upgrades.
- `composer.lock`—the `composer.lock` speichert einen Satz exakter Versionsabhängigkeiten, die den Versionsbeschränkungen jeder Anforderung für jedes Paket in der Abhängigkeitsstruktur des Projekts entsprechen.

**Allgemeine Befehle:**

| Befehl | Beschreibung |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Aktualisierungen der neuesten Versionen der Abhängigkeiten, die in der `composer.json` -Datei. Dadurch wird der `composer.lock` -Datei. |
| `composer install` | Liest die `composer.lock` Datei zum Herunterladen von Abhängigkeiten. Es empfiehlt sich, eine Kopie von auf dem neuesten Stand zu halten `composer.lock` im Projekt-Repository. |

{style="table-layout:auto"}

Nachdem Sie den aktualisierten Code hinzugefügt, übertragen und per Push übertragen haben, wird der Bereitstellungsprozess automatisch ausgeführt `composer install` Befehl während der [Build-Phase](../deploy/process.md#build-phase-build-phase).

### Cloud-Metapaket

Adobe Commerce in Cloud-Infrastrukturen verwendet ein Metapaket, für das Folgendes erforderlich ist `magento/product-enterprise-edition`. Verwenden Sie die folgende Einschränkungssyntax, um die neuesten Aktualisierungen für die neueste Version von Commerce zu erhalten:

```text
>=current_version <next_version
```

Um beispielsweise die neueste Adobe Commerce-Version 2.4.7 zu verwenden, setzen Sie `2.4.7` als „aktuelle“ Version und `2.4.8` als „nächste“ Version im `composer.json` Datei:

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Die Hauptpakete dieses Metapakets sind die folgenden:

- **Anbieter/Magento/ECE-Tools**—the `ece-tools` Das -Paket ist mit Adobe Commerce Version 2.1.4 und höher kompatibel und bietet eine Vielzahl von Funktionen, mit denen Sie Ihr Adobe Commerce on Cloud Infrastructure-Projekt verwalten können. Es enthält Skripte und Adobe Commerce-Befehle für die Cloud-Infrastruktur, die Ihnen bei der Code-Verwaltung helfen und die automatische Erstellung und Bereitstellung Ihrer Projekte ermöglichen. Siehe [`ece-tools` Paketübersicht](../dev-tools/package-overview.md).
- **Vendor/Magento/Product-Enterprise-Edition**- Dieses Metapaket erfordert Anwendungskomponenten, einschließlich Module, Frameworks, Designs und mehr.
- **Anbieter/Fastly2/Magento2**- Dieses Modul verwaltet das Fastly CDN und die Services für die Pro Staging- und Produktions- und Starter Production-Umgebungen. Siehe [Fastly Services](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **Vendor/Magento/module-PayPal-on-boarding**- Dieses Modul ermöglicht den PayPal Payment Gateway Checkout, indem es sich mit Ihrem PayPal-Händlerkonto verbindet. Siehe [PayPal-Onboarding-Tool](../store/paypal.md).

>[!TIP]
>
>Siehe [Cloud-Pakete für Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) in der _Versionshinweise zu Commerce_ für eine Liste der Abhängigkeiten und Drittanbieterlizenzen.

## Docker-Umgebung

Sie können das Tool Cloud Docker for Commerce verwenden, um die Adobe Commerce in Cloud-Infrastruktur-Produktions- und Entwicklungsumgebungen für die lokale Entwicklung zu emulieren. Cloud Docker für Commerce erfordert keine lokale Installation von PHP und Composer.

- [Lokale Entwicklung mit Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) Auf der Adobe Developer-Site
- [Docker-Architektur und allgemeine Befehle](../dev-tools/cloud-docker.md)
- [Versionshinweise zu Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Informationen zur Verwendung von Git-basierten Hosting-Services mit Adobe Commerce in der Cloud-Infrastruktur finden Sie unter [Integrationen](../integrations/overview.md).
