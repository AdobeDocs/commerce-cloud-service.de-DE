---
title: Versionshinweise für Cloud Tools Suite
description: Erfahren Sie mehr über die neuesten Verbesserungen der Cloud Tools-Suite für Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: e04a9de8f0e31098f0cc2e47112f206c11a0e23b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Versionshinweise für Commerce Cloud Tools Suite

Diese Versionsinformationen enthalten die neuesten Verbesserungen der Cloud Tools Suite für Commerce-Pakete, die zur Bereitstellung und Verwaltung von Adobe Commerce-Installationen und -Upgrades auf der Cloud-Plattform entwickelt wurden.

| Versionshinweise | Version | Beschreibung | Quelle |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package](ece-tools-package.md) | 2002.1.19 | Eine Reihe von Skripten und Tools zum Verwalten und Bereitstellen von Cloud-Projekten | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Cloud-Patches für Commerce](cloud-patches.md) | 1,0,27 | Eine Reihe von Patches, die die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen verbessern. Dieses Paket enthält Adobe Commerce-Patches und verfügbare Hotfixes, die angewendet werden, wenn Sie `ece-tools` bereitstellen | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker für Commerce](cloud-docker.md) | 1,3,7 | Funktionen und Konfigurationsdateien für Docker-Bilder zum Bereitstellen von Adobe Commerce in einer lokalen Cloud-Umgebung | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Cloud-Komponenten von Commerce](cloud-components.md) | 1,0,14 | Erweiterte Adobe Commerce-Kernfunktionen für Sites, die in der Cloud-Infrastruktur bereitgestellt werden | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

Wenn Sie ein Update auf ECE-Tools 2002.1.0 oder höher durchführen, aktualisieren Sie automatisch auf die neuesten Versionen der anderen Pakete, die Abhängigkeiten für die `ece-tools` Paket. Siehe [Cloud-Metapaket](../development/overview.md#cloud-metapackage) für eine Liste von Abhängigkeiten.
