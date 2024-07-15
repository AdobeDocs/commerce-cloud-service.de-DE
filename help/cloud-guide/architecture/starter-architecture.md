---
title: Starterarchitektur
description: Erfahren Sie mehr über die von der Starter-Architektur unterstützten Umgebungen.
feature: Cloud, Paas
exl-id: 03365d32-4eb4-42d4-82a7-771df5e7b3da
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Starterarchitektur

Ihre Adobe Commerce on Cloud-Infrastruktur-Starter-Architektur unterstützt bis zu **4** Umgebungen, einschließlich einer `master` -Umgebung, die den anfänglichen Projektcode, die Staging-Umgebung und bis zu zwei Integrationsumgebungen enthält.

Alle Umgebungen befinden sich in PaaS-Containern (Platform as a Service). Diese Container werden in stark eingeschränkten Containern auf einem Serverraster bereitgestellt. Diese Umgebungen sind schreibgeschützt und akzeptieren bereitgestellte Codeänderungen aus Verzweigungen, die von Ihrem lokalen Arbeitsbereich aus gesendet werden. Jede Umgebung stellt eine Datenbank und einen Webserver bereit.

Sie können jede beliebige Entwicklungs- und Verzweigungsmethode verwenden. Wenn Sie anfänglichen Zugriff auf Ihr Projekt erhalten, erstellen Sie eine `staging` -Umgebung aus der `master` -Umgebung. Erstellen Sie dann die `integration` -Umgebung durch Verzweigung von `staging`.

## Architektur der Starterumgebung

Das folgende Diagramm zeigt die hierarchischen Beziehungen der Starter-Umgebungen.

![Ansicht des Starter-Projekts auf hoher Ebene](../../assets/starter/architecture.png)

## Produktionsumgebung

Die Produktionsumgebung stellt den Quellcode für die Bereitstellung von Adobe Commerce in der Cloud-Infrastruktur bereit, in der Ihre öffentlich zugänglichen Storefronts mit einzelnen und mehreren Sites ausgeführt werden. Die Produktionsumgebung verwendet Code aus der `master`-Verzweigung, um den Webserver, die Datenbank, die konfigurierten Dienste und Ihren Anwendungscode zu konfigurieren und zu aktivieren.

Da die `production` -Umgebung schreibgeschützt ist, verwenden Sie die `integration` -Umgebung, um Code-Änderungen vorzunehmen, stellen Sie sie in der gesamten Architektur von `integration` bis `staging` und schließlich in der `production` -Umgebung bereit. Siehe [Bereitstellen Ihres Stores](../deploy/staging-production.md) und [Website-Launch](../launch/overview.md).

Adobe empfiehlt, die `staging` -Verzweigung vollständig zu testen, bevor sie an die `master` -Verzweigung gepusht wird, die in der `production` -Umgebung bereitgestellt wird.

## Staging-Umgebung

Adobe empfiehlt die Erstellung einer Verzweigung mit dem Namen `staging` von `master`. Die `staging`-Verzweigung stellt Code in der Staging-Umgebung bereit, um eine Produktionsumgebung bereitzustellen, in der Code, Module und Erweiterungen, Zahlungskanäle, Versand, Produktdaten und vieles mehr getestet werden können. Diese Umgebung bietet die Konfiguration für alle Dienste, die mit der Produktionsumgebung übereinstimmen, einschließlich Fastly, New Relic APM und Suche.

Weitere Abschnitte in diesem Handbuch enthalten Anweisungen für endgültige Code-Bereitstellungen und zum Testen von Interaktionen auf Produktionsebene in einer sicheren Staging-Umgebung. Für optimale Leistung und Funktionstests replizieren Sie Ihre Datenbank in der Staging-Umgebung.

>[!WARNING]
>
>Adobe empfiehlt, alle Handels- und Kundeninteraktionen in der Staging-Umgebung vor der Bereitstellung in der Produktionsumgebung zu testen. Siehe [Bereitstellen Ihres Stores](../deploy/staging-production.md) und [Testen der Bereitstellung](../test/staging-and-production.md).

## Integrationsumgebung

Entwickler verwenden die `integration` -Umgebung, um Folgendes zu entwickeln, bereitzustellen und zu testen:

- Adobe Commerce-Anwendungscode

- Benutzerspezifischer Code

- Erweiterungen

- Dienste

**Empfohlene Anwendungsfälle:**

Integrationsumgebungen sind für begrenzte Tests und Entwicklung ausgelegt. Beispielsweise können Sie die Integrationsumgebung verwenden, um die folgenden Aufgaben auszuführen:

- Sicherstellen, dass Änderungen an CI-Prozessen (Continuous Integration) Cloud-kompatibel sind

- Testen Sie kritische Workflows auf wichtigen Seiten wie Startseite, Kategorie, Produktdetailseite (PDP), Checkout und Admin

Befolgen Sie die folgenden Best Practices, um eine optimale Leistung in der Integrationsumgebung zu erzielen:

- Eingrenzen der Kataloggröße

- Beschränkung der Verwendung auf einen oder zwei gleichzeitige Benutzer

- Deaktivieren Sie Cron-Aufträge und führen Sie sie nach Bedarf manuell aus.

Sie können über bis zu **zwei** aktive Integrationsumgebungen verfügen. Sie erstellen eine Integrationsumgebung, indem Sie eine Verzweigung aus der Verzweigung `staging` erstellen. Wenn Sie eine Integrationsumgebung erstellen, entspricht der Umgebungsname dem Zweignamen. Eine Integrationsumgebung umfasst einen Webserver und eine Datenbank. Sie umfasst nicht alle Dienste, z. B. Fastly CDN und New Relic sind nicht verfügbar.

Sie können eine unbegrenzte Anzahl von inaktiven Verzweigungen für die Codespeicherung haben. Um auf einen inaktiven Zweig zuzugreifen, ihn anzuzeigen und zu testen, müssen Sie ihn aktivieren

{{enhanced-integration-envs}}

## Staging- und Produktions- und Staging-Technologie-Stack

Die Produktions- und Staging-Umgebungen umfassen die folgenden Technologien. Sie können diese Technologien über die Datei [`.magento.app.yaml`](../application/configure-app-yaml.md) ändern und konfigurieren.

- Schnelles HTTP-Caching und CDN
- Nginx-Webserver, der mit PHP-FPM spricht, eine Instanz mit mehreren Arbeitern
- Redis-Server
- Elasticsearch für die Katalogsuche für Adobe Commerce 2.2 bis 2.4.3-p2
- OpenSearch für die Katalogsuche nach Adobe Commerce 2.3.7-p3, 2.4.3-p2 und 2.4.4 und höher
- Ausgehend-Filter (ausgehende Firewall)

### Dienste

Adobe Commerce on Cloud Infrastructure unterstützt derzeit die folgenden Dienste: PHP, MySQL (MariaDB), Elasticsearch (Adobe Commerce 2.2 bis 2.4.3-p2), OpenSearch (2.3.7-p3, 2.4.3-p2, 2.4.4 und höher), Redis und [!DNL RabbitMQ].

Jeder Dienst wird in einem separaten, sicheren Container ausgeführt. Container werden im Projekt gemeinsam verwaltet. Einige Dienste sind Standard, z. B.:

- HTTP-Router (Verarbeitung eingehender Anfragen, aber auch Zwischenspeicherung und Umleitungen)

- PHP-Anwendungsserver

- Git

- Secure Shell (SSH)

### Softwareversionen

Adobe Commerce auf Cloud-Infrastruktur verwendet das Debian GNU/Linux-Betriebssystem und den NGINX-Webserver. Sie können diese Software nicht aktualisieren, Sie können jedoch Versionen für Folgendes konfigurieren:

- [PHP](../application/php-settings.md)

- [MySQL](../services/mysql.md)

- [Redis](../services/redis.md)

- [RabbitMQ](../services/rabbitmq.md)

- [Elasticsearch](../services/elasticsearch.md)

- [OpenSearch](../services/opensearch.md)

In den Staging- und Produktionsumgebungen verwenden Sie Fastly für CDN und Caching. Die neueste Version der Fastly CDN-Erweiterung wird während der ersten Bereitstellung Ihres Projekts installiert. Sie können die Erweiterung aktualisieren, um die neuesten Fehlerbehebungen und Verbesserungen zu erhalten. Siehe [Schnelles CDN-Modul für Magento 2](https://github.com/fastly/fastly-magento2). Außerdem haben Sie Zugriff auf [New Relic](../monitor/account-management.md) zur Leistungsüberwachung.

Verwenden Sie die folgenden Dateien, um die Softwareversionen zu konfigurieren, die Sie in Ihrer Implementierung verwenden möchten.

- [`.magento.app.yaml`](../application/configure-app-yaml.md)

- [&quot;routes.yaml&quot;](../routes/routes-yaml.md)

- [&quot;services.yaml&quot;](../services/services-yaml.md)

### Sicherung und Wiederherstellung nach Katastrophen

Sie können eine Sicherung Ihrer Datenbank und Ihres Dateisystems mithilfe von [!DNL Cloud Console] oder der CLI erstellen. Siehe [Backup management](../storage/snapshots.md).

## Vorbereitungen für die Entwicklung

Der folgende Workflow fasst den Prozess zur Verzweigung Ihres Codes, Entwicklung und Bereitstellung Ihres Stores zusammen:

1. Lokale Umgebung einrichten

1. Klonen Sie den Zweig `master` in Ihre lokale Umgebung

1. Erstellen eines `staging`-Zweigs aus `master`

1. Erstellen von Verzweigungen für die Entwicklung aus `staging`

1. Push-Code an Git, der erstellt und in einer Umgebung zum Testen bereitgestellt wird

In den folgenden Abschnitten finden Sie ausführliche Anweisungen und schrittweise Anleitungen zum Entwickeln, Testen und Bereitstellen Ihres Stores:

- [Workflow für die Entwicklung und Bereitstellung von Startern](starter-develop-deploy-workflow.md)

- [Docker-Entwicklung](../dev-tools/cloud-docker.md) (lokale Entwicklungsumgebung aktiviert durch Cloud Docker für Commerce)

- [Verzweigungen verwalten](../project/console-branches.md)

- [Bereitstellen Ihres Stores](../deploy/staging-production.md)

- [Site-Launch](../launch/overview.md)
