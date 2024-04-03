---
title: Anwendungsbereitstellung konfigurieren
description: Erfahren Sie, wie Sie die Eigenschaften in der Anwendungskonfigurationsdatei konfigurieren, die steuern, wie die [!DNL Commerce] -Anwendung erstellt und stellt sie in der Cloud-Umgebung bereit.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Anwendungsbereitstellung konfigurieren

Die `.magento.app.yaml` -Datei steuert, wie Ihre Anwendung erstellt und bereitgestellt wird. Obwohl Adobe Commerce on Cloud Infrastructure mehrere Anwendungen pro Projekt unterstützt, verfügt ein Projekt in der Regel über eine einzige Anwendung mit der `.magento.app.yaml` -Datei im Stammverzeichnis des Repositorys.

Die `.magento.app.yaml` hat viele Standardwerte, siehe [Beispiel `.magento.app.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Überprüfen Sie immer die `.magento.app.yaml` für Ihre installierte Version. Diese Datei kann in Adobe Commerce in Cloud-Infrastrukturversionen unterschiedlich sein.

Verwenden Sie die `.magento.app.yaml` -Datei, um die folgenden Konfigurationswerte zu definieren:

- [Eigenschaften](properties.md)—Definieren Sie Eigenschaftswerte für die Anwendungsinstanz.
- [Variableneigenschaft](variables-property.md)—Überprüfen Sie die für die [!DNL Commerce] Anwendungsversion.
- [PHP-Einstellungen](php-settings.md)—Konfigurieren von Runtime-PHP-Optionen.
- [Festlegen des Cache für statische Dateien](set-cache.md)—Legen Sie die TTL-Zwischenspeicher für Ihre Medien- und statischen Dateien fest.
