---
title: Überblick über Speicheroptionen und Konfigurationsverwaltung
description: Passen Sie Ihren Adobe Commerce Store in der Cloud-Infrastruktur an.
feature: Cloud, Configuration, Services
exl-id: 06d477e4-02de-4742-8495-541458400e93
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Überblick über Speicheroptionen und Konfigurationsverwaltung

Es gibt viele Möglichkeiten, Ihren Store anzupassen, z. B. das Hinzufügen eines benutzerdefinierten Designs, das Installieren einer Erweiterung oder das Erzwingen einer bestimmten Konfiguration in Cloud-Infrastrukturumgebungen. Sie können Einstellungen für bestimmte Dienste direkt in Staging- und Produktionsumgebungen konfigurieren. Sie können mehrere Websites und Stores einrichten. Die Speicherkonfiguration hilft Ihnen dabei, diese Optionen in Ihrer lokalen Workstation zu konfigurieren und bestimmte Einstellungen in allen Umgebungen bereitzustellen.

Um auf Ihre Storefront zuzugreifen, verwenden Sie die `magento-cloud url` und antworten Sie auf die Eingabeaufforderungen. Oder Sie finden die URL im [!DNL Cloud Console] under **Auf Website zugreifen**.

## Store-Optionen konfigurieren

Zu den Speicheroptionen gehören:

* [B2B (Business-to-Business-Modul)](b2b-module.md)
* [Benutzerdefinierte Designs](custom-theme.md)
* [Erweiterungen](extensions.md)
* [Mehrere Sites](multiple-sites.md)
* [Zahlungsdienste](paypal.md)

## Dienste und Integrationen konfigurieren

Es gibt bestimmte [Konfigurationsdateien](../environment/overview.md) die bestimmte Bereitstellungsverhaltensweisen in Remote-Umgebungen verwalten. Sie können diese Themen separat prüfen:

* [Anwendungsimplementierung](../application/configure-app-yaml.md)
* [Aktionen zum Erstellen und Bereitstellen von Umgebungen](../environment/configure-env-yaml.md)
* [Eingehende Anfragerouten](../routes/routes-yaml.md)
* [Unterstützte Dienste](../services/services-yaml.md)

## Konfigurationsverwaltung

Verwenden Sie nach dem Konfigurieren der Speicheroptionen, Dienste und Integrationen das Konfigurationsmanagement, um diese Konfigurationen konsistent und mit minimalen Ausfallzeiten in allen Umgebungen bereitzustellen. Siehe [Konfigurationsverwaltung](store-settings.md).
