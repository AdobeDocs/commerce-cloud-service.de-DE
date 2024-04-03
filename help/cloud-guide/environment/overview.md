---
title: Übersicht über Konfigurationsdateien
description: Erfahren Sie mehr über die Konfiguration der Cloud-Infrastruktur-Umgebung zur Unterstützung der Bereitstellung und Verwaltung Ihres benutzerdefinierten Adobe Commerce-Stores.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: f469a0ec-e459-413f-9725-66a0fbf34f01
source-git-commit: 47b66d0d2bbff14e76ce49182a68d5e6c9fb13a7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Übersicht über Konfigurationsdateien

Zu den Umgebungen in Adobe Commerce auf Cloud-Infrastruktur gehören Container mit Anwendungen, Diensten und einer Datenbank, um ein komplettes System für Ihre Adobe Commerce-Anwendungs-Codebasis und -Dateien bereitzustellen.

Sie können Anwendungseinstellungen, Routen, Aktionen erstellen und bereitstellen und Benachrichtigungen zur Unterstützung Ihrer Projektumgebungen mithilfe der folgenden Konfigurationsdateien konfigurieren:

| Konfiguration | Dateiname | Beschreibung |
| ------------- | -------- | ----------- |
| [Anwendung](../application/configure-app-yaml.md) | `.magento.app.yaml` | Definiert, wie Adobe Commerce erstellt und bereitgestellt wird, einschließlich Diensten, Hooks und Cron-Aufträgen. |
| [Umgebung](configure-env-yaml.md) | `.magento.env.yaml` | Zentralisiert die Verwaltung von Build- und Bereitstellungsaktionen in allen Umgebungen, einschließlich Pro Staging und Produktion, mithilfe von Umgebungsvariablen. |
| [Routen](../routes/routes-yaml.md) | `.magento/routes.yaml` | Konfigurieren Sie Zwischenspeicherung, Umleitungen und serverseitige Includes. |
| [Dienst](../services/services-yaml.md) | `.magento/services.yaml` | Definiert die Dienste, die Adobe Commerce nach Name und Version verwendet. Diese Datei kann beispielsweise Versionen von MariaDB, PHP-Erweiterungen, Redis, RabbitMQ und Elasticsearch oder OpenSearch enthalten. Sie müssen ein Support-Ticket öffnen, um diese Änderungen an die Staging- und Produktionsumgebungen von Pro Plan zu übertragen. |
| [PHP-Einstellungen](../application/php-settings.md#configure-php) | `php.ini` | Eine optionale Datei, die zum Projekt hinzugefügt werden kann. Die in dieser Datei enthaltenen Einstellungen werden an die Einstellungen angehängt, die von der Cloud-Infrastruktur verwaltet werden. |

{style="table-layout:auto"}

## Konfigurationsaktualisierungen für Pro-Umgebungen

Für Adobe Commerce in den Staging- und Produktionsumgebungen der Cloud-Infrastruktur können Sie viele Konfigurationsoptionen in Ihrer lokalen Entwicklungsumgebung aktualisieren und die Änderungen übernehmen, um sie auf diese Umgebungen anzuwenden. Sie müssen jedoch [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) um die folgenden Konfigurationsoptionen zu aktualisieren:

- Installieren oder aktualisieren Sie Dienste in der `.magento/services.yaml` -Datei.
- Ändern Sie die Konfiguration für die `mounts` und `disk` -Eigenschaften in `.magento.app.yaml` -Datei.

{{pro-self-service-warning}}
