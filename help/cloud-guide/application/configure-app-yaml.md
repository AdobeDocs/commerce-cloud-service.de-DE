---
title: Anwendungsbereitstellung konfigurieren
description: Erfahren Sie, wie Sie die Eigenschaften in der Anwendungskonfigurationsdatei konfigurieren, die steuern, wie die [!DNL Commerce] Anwendung erstellt und in der Cloud-Umgebung bereitgestellt wird.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: c9339137d957840a9ae33ed45950c613eea93660
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Anwendungsbereitstellung konfigurieren

Die Datei &quot;`.magento.app.yaml`&quot; steuert, wie Ihre Anwendung erstellt und bereitgestellt wird. Obwohl Adobe Commerce in der Cloud-Infrastruktur mehrere Anwendungen pro Projekt unterstützt, verfügt ein Projekt in der Regel über eine einzige Anwendung mit der Datei &quot;`.magento.app.yaml`&quot;im Stammverzeichnis des Repositorys.

Die `.magento.app.yaml` hat viele Standardwerte, siehe [eine Beispieldatei `.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Überprüfen Sie immer die `.magento.app.yaml` für Ihre installierte Version. Diese Datei kann in Adobe Commerce in Cloud-Infrastrukturversionen unterschiedlich sein.

Verwenden Sie die Datei `.magento.app.yaml` , um die folgenden Konfigurationswerte zu definieren:

- [Eigenschaften](properties.md) - Definieren Sie Eigenschaftswerte für die Anwendungsinstanz.
- [Variables property](variables-property.md) - Überprüfen Sie die Umgebungsvariablen, die für die [!DNL Commerce] -Anwendungsversion erforderlich sind.
- [PHP-Einstellungen](php-settings.md) - Konfigurieren Sie die PHP-Laufzeitoptionen.
- [Cache für statische Dateien festlegen](set-cache.md) - Legen Sie die TTL-Zwischenspeicher für Ihre Medien- und statischen Dateien fest.

>[!NOTE]
>
>Die Datei &quot;`.magento.app.yaml`&quot; wird lokal oder im Git-Repository verwaltet. Die Konfiguration wird nur zum Zweck der Bereitstellung und des Build-Prozesses gelesen und nach Abschluss der Bereitstellung entfernt, sodass Sie sie nicht auf dem Server finden.
