---
title: Cloud-Architektur für Commerce
description: Erfahren Sie, wie Starter- und Pro-Projektarchitekturen sich in Bezug auf Commerce in Cloud-Infrastruktur unterscheiden.
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
exl-id: 37cd6733-c10a-4d06-b784-171da576f9fc
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Cloud-Architektur für Commerce

Adobe Commerce on Cloud Infrastructure hat einen Starter- und einen Pro-Plan. Jeder Plan verfügt über eine eigene Architektur, um den Entwicklungs- und Bereitstellungsprozess für Adobe Commerce voranzubringen. Sowohl der Starter-Plan als auch die Pro-Plan-Architektur stellen Datenbanken, Webserver und Caching-Server in mehreren Umgebungen für End-to-End-Tests bereit und unterstützen gleichzeitig die kontinuierliche Integration.

Zum Vergleich umfasst jeder Plan die folgenden Infrastrukturfunktionen und unterstützten Produkte.

|          | Starter | Pro |
| -------- | --------------------| ------------------ |
| Kernfunktionen | <ul><li>[Alle Adobe Commerce-Funktionen](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal Onboarding-Tool</li><li>[Commerce-Berichterstellung](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li></ul> | <ul><li>[Alle Adobe Commerce-Funktionen](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>PayPal Onboarding-Tool</li><li>[Commerce-Berichterstellung](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li><li>[B2B-Modul](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| Infrastruktur und Bereitstellung | <ul><li>Tools zur kontinuierlichen Cloud-Integration mit unbegrenzten Benutzern</li><li>Fastly Content Delivery Network (CDN), Image Optimization (IO) und zusätzliche Sicherheit mit großzügigen Bandbreitenzertifikaten. Der Web Application Firewall (WAF)-Dienst ist nur in Produktionsumgebungen verfügbar.</li><li>[New Relic](../monitor/new-relic-service.md) APM (Performance Monitoring) für 3 Zweige: `master` und 2 Ihrer Wahl<br>Produktions-, Staging- und Entwicklungsumgebungen für Platform as a Service (PaaS) (4 aktive Umgebungen insgesamt), die für Adobe Commerce optimiert sind</li><li>Ausgehend-Filter (ausgehende Firewall)</li></ul> | <ul><li>Tools zur kontinuierlichen Cloud-Integration mit unbegrenzten Benutzern</li><li>Fastly Content Delivery Network (CDN), Image Optimization (IO) und zusätzliche Sicherheit mit großzügigen Bandbreitenzertifikaten. Der Web Application Firewall (WAF)-Dienst ist nur in Produktionsumgebungen verfügbar.</li><li>[New Relic](../monitor/new-relic-service.md) Infrastruktur für Produktion und APM (Performance Monitoring) für Staging und Produktion. Die [Richtlinie für verwaltete Warnhinweise](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) für Adobe Commerce-Richtlinien implementiert die Überwachung von Best Practices, um Sie proaktiv über Anwendungs- und Infrastrukturprobleme zu informieren, die sich auf die Site-Leistung auswirken.</li><li>Platform as a Service (PaaS)-basiert [Integrationsentwicklung](pro-architecture.md#integration-environment) Umgebungen (2 aktive Umgebungen insgesamt) für Adobe Commerce optimiert</li><li>Infrastructure as a service (IAAS) - dedizierte virtuelle Infrastruktur für Staging- und Produktionsumgebungen</li></ul> |
| Hochverfügbare Infrastruktur | | [Architektur mit hoher Verfügbarkeit](pro-architecture.md#redundant-hardware) mit einer Einrichtung von drei Servern in der zugrunde liegenden Infrastruktur as a service (IAAs) zur Bereitstellung von Zuverlässigkeit und Verfügbarkeit auf Unternehmensebene |
| Dedizierte Hardware | | Isolierte und dedizierte Hardware in der zugrunde liegenden Infrastruktur as a service (IAAs), um eine noch höhere Zuverlässigkeit und Verfügbarkeit zu gewährleisten |
| E-Mail-Unterstützung rund um die Uhr | 24x7-Monitoring und E-Mail-Unterstützung für die Kernanwendung und die Cloud-Infrastruktur | 24x7-Monitoring und E-Mail-Unterstützung für die Kernanwendung und die Cloud-Infrastruktur |
| Ein spezieller technischer Kundenberater (CTA) | | Dedizierte technische Kontoverwaltung für den ersten Startzeitraum, beginnend mit Ihrem Abonnement bis zum Start Ihrer ersten Site |
| Add-ons\* | <ul><li>[B2B-Modul](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _Gegen eine zusätzliche Gebühr verfügbar_

## Starterprojekte

Die [Starter-Plan-Architektur](starter-architecture.md) verfügt über vier Umgebungen:

- **Integration**- Die Integrationsumgebung bietet zwei testbare Umgebungen. Jede Umgebung enthält eine aktive Git-Verzweigung, Datenbank, Webserver, Zwischenspeicherung, einige Dienste, Umgebungsvariablen und Konfigurationen.

- **Staging**—Wenn Code und Erweiterungen Ihre Tests bestehen, können Sie Ihre `integration` in die Staging-Umgebung verzweigen, die zu Ihrer Testumgebung vor der Produktion wird. Er enthält die `staging` aktive Verzweigung, Datenbank, Webserver, Zwischenspeicherung, Dienste von Drittanbietern, Umgebungsvariablen, Konfigurationen und Dienste wie Fastly und New Relic.

- **Produktion**—Wenn der Code fertig ist und getestet wird, führt der gesamte Code zu `master` für die Bereitstellung auf der Produktions-Live-Site. Diese Umgebung umfasst Ihre aktiven `master` Verzweigung, Datenbank, Webserver, Zwischenspeicherung, Dienste von Drittanbietern, Umgebungsvariablen und Konfigurationen.

- **Inaaktiv**—Sie haben eine unbegrenzte Anzahl von inaktiven Verzweigungen.

## Pro Projekte

Die [Pro Plan Architektur](pro-architecture.md) hat eine globale `master` mit drei Umgebungen:

- **Integration**—Die Integrationsumgebung bietet eine testbare Umgebung mit einer Datenbank, einem Webserver, einer Zwischenspeicherung, einigen Diensten, Umgebungsvariablen und Konfigurationen. Sie können Ihren Code entwickeln, bereitstellen und testen, bevor Sie ihn zur Staging-Umgebung zusammenführen.

   - _Inaaktiv_—Sie können eine unbegrenzte Anzahl von inaktiven Verzweigungen auf Grundlage der Variablen `integration` Umgebung, aber nur eine aktive Verzweigung (ausgenommen `integration` ).

- **Staging**—Die Staging-Umgebung dient zum Testen vor der Produktion und umfasst eine Datenbank, einen Webserver, Caching, Dienste von Drittanbietern, Umgebungsvariablen, Konfigurationen und Dienste wie Fastly.

- **Produktion**—Die Produktionsumgebung umfasst eine dreistellige Hochverfügbarkeitsarchitektur für Ihre Daten, Dienste, Zwischenspeicherung und Speicherung. Die Produktion ist Ihre Live- und öffentliche Store-Umgebung mit Umgebungsvariablen, Konfigurationen und Drittanbieterdiensten.

## Unterstützte Software und Dienste

Adobe Commerce in der Cloud-Infrastruktur verwendet:

- Betriebssystem: Debian GNU/Linux
- Webserver: Nginx
- Datenbank: MySQL (MariaDB)
- Content Delivery Network (CDN): Fastly CDN

Sie können die folgenden Dienste konfigurieren:

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>Siehe [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im _Installationshandbuch_ für empfohlene Versionen.

Das Fastly CDN-Modul wird für CDN- und Caching-Dienste in Staging- und Produktionsumgebungen verwendet. Siehe [Fastly Services konfigurieren](../cdn/fastly.md).

Informationen zum Konfigurieren der in Ihrer Implementierung zu verwendenden Softwareversionen finden Sie in den folgenden Adobe Commerce zu Konfigurationsdateien für die Cloud-Infrastruktur:

- [Anwendungskonfiguration (.magento.app.yaml)](../application/configure-app-yaml.md)
- [Umgebungskonfiguration (.magento.env.yaml)](../environment/configure-env-yaml.md)
- [Routenkonfiguration (routes.yaml)](../routes/routes-yaml.md)
- [Dienstkonfiguration (services.yaml)](../services/services-yaml.md)
