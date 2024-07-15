---
title: Entwicklungsübersicht
description: Bereiten Sie sich auf die lokale Entwicklung mit einem Adobe Commerce-Projekt zur Cloud-Infrastruktur vor.
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

Adobe Commerce in Cloud-Infrastruktur-Remote-Umgebungen sind **schreibgeschützt**, einschließlich aller Starterumgebungen und aller Pro-Integration-, Staging- und Produktionsumgebungen. In einer lokalen Entwicklungsumgebung können Sie Code schreiben und testen, bevor Sie ihn in eine Integrationsumgebung senden, um weitere Tests und Implementierungen in Staging und Produktion durchzuführen.

Stellen Sie vor der Vorbereitung Ihres lokalen Arbeitsbereichs sicher, dass Sie über Ihre [Anmeldedaten](../../get-started/prepare-workspace.md) verfügen. Für die lokale Entwicklung ist die Installation von PHP und Composer erforderlich, es sei denn, Sie entscheiden sich für die Verwendung von [Cloud Docker für Commerce](#docker-environment).

## Erforderliche Pakete

Adobe Commerce on Cloud Infrastructure verwendet Composer zum Verwalten der Abhängigkeiten und Upgrades für Projekte. Für die lokale Entwicklung müssen Sie die PHP- und Composer-Versionen installieren, die mit Ihrem Cloud-Projekt kompatibel sind. Wenn Sie beispielsweise die Cloud-Vorlage [!DNL Commerce] 2.4.7 verwenden, können Sie sehen, dass die Konfigurationsdatei [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) **PHP 8.3** und **Composer 2.7.2** verwendet.

Der Composer installiert die erforderlichen Bibliotheken und Abhängigkeiten für Ihr Projekt im Verzeichnis &quot;`vendor`&quot;. Die folgenden erforderlichen Composer-Dateien befinden sich im Projektstammordner:

- `composer.json` - Verwenden Sie die `composer.json`-Datei, um Produktinstallationen und -aktualisierungen zu verwalten.
- `composer.lock`—Die Datei `composer.lock` speichert eine Reihe exakter Versionsabhängigkeiten, die die Versionsbegrenzungen jeder Anforderung für jedes Paket in der Abhängigkeitsstruktur des Projekts erfüllen.

**Allgemeine Befehle:**

| Befehl | Beschreibung |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Aktualisierungen der neuesten Versionen der Abhängigkeiten, die in der Datei `composer.json` angezeigt werden. Dadurch wird die `composer.lock` -Datei aktualisiert. |
| `composer install` | Liest die Datei `composer.lock` , um Abhängigkeiten herunterzuladen. Es empfiehlt sich, eine aktuelle Kopie von `composer.lock` in Ihrem Projekt-Repository aufzubewahren. |

{style="table-layout:auto"}

Nachdem Sie den aktualisierten Code hinzugefügt, übertragen und gepusht haben, wird während der [Build-Phase](../deploy/process.md#build-phase-build-phase) automatisch der Befehl `composer install` ausgeführt.

### Cloud-Metapaket

Adobe Commerce in der Cloud-Infrastruktur verwendet ein Metapaket, das `magento/product-enterprise-edition` erfordert. Verwenden Sie die folgende Einschränkungssyntax, um die neuesten Updates für die neueste Version von Commerce zu erhalten:

```text
>=current_version <next_version
```

Um beispielsweise die neueste Adobe Commerce-Version 2.4.7 zu verwenden, setzen Sie `2.4.7` als &quot;aktuelle&quot;Version und `2.4.8` als &quot;nächste&quot;Version in der Datei `composer.json`:

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Die Hauptpakete dieses Metapakets sind:

- **Anbieter/Magento/ece-tools**: Das `ece-tools` -Paket ist mit Adobe Commerce-Version 2.1.4 und höher kompatibel, um eine Vielzahl von Funktionen bereitzustellen, mit denen Sie Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur verwalten können. Es enthält Skripte und Adobe Commerce zu Cloud-Infrastrukturbefehlen, die Sie bei der Verwaltung Ihres Codes und der automatischen Erstellung und Bereitstellung Ihrer Projekte unterstützen. Siehe [`ece-tools` Paketübersicht](../dev-tools/package-overview.md).
- **Anbieter/Magento/Produkt-Enterprise-Edition**: Für dieses Metapaket sind Anwendungskomponenten erforderlich, darunter Module, Frameworks, Designs und mehr.
- **vendor/fastly2/magento2** - Dieses Modul verwaltet das Fastly-CDN und die Services für die Produktions- und Staging-Umgebungen von Pro. Siehe [Schnelldienste](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **Anbieter/Magento/module-paypal-on-boarding** - Dieses Modul bietet PayPal-Zahlungseingang zum Checkout, indem es eine Verbindung zu Ihrem PayPal-Handelskonto herstellt. Siehe [PayPal On-Boarding-Tool](../store/paypal.md).

>[!TIP]
>
>Eine Liste der Abhängigkeiten und Drittanbieterlizenzen finden Sie unter [Cloud-Pakete für Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) in den _Commerce-Versionshinweisen_ .

## Docker-Umgebung

Mit dem Cloud Docker für Commerce-Tool können Sie die Adobe Commerce in den Produktions- und Entwicklungsumgebungen der Cloud-Infrastruktur für die lokale Entwicklung emulieren. Cloud Docker für Commerce erfordert keine lokale Installation von PHP und Composer.

- [Lokale Entwicklung mit Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) auf der Adobe Developer-Site
- [Docker-Architektur und allgemeine Befehle](../dev-tools/cloud-docker.md)
- [Cloud Docker - Versionshinweise](../release-notes/cloud-docker.md)

>[!TIP]
>
>Informationen zur Verwendung von Git-basierten Hosting-Diensten mit Adobe Commerce in der Cloud-Infrastruktur finden Sie unter [Integrationen](../integrations/overview.md).
