---
title: Pro Architektur
description: Erfahren Sie mehr über die Umgebungen, die von der Pro-Architektur unterstützt werden.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: eccf69d792f5f8bbd32fb24ac731fffa1eeb91ba
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---

# Pro Architektur

Ihre Adobe Commerce on Cloud Infrastructure Pro-Architektur unterstützt mehrere Umgebungen, mit denen Sie Ihren Store entwickeln, testen und starten können.

- **Master**: Stellt eine `master` -Verzweigung bereit, die in Platform as a service (PageS)-Containern bereitgestellt wird.
- **Integration**: Stellt einen einzelnen `integration` -Zweig zur Entwicklung bereit, Sie können jedoch einen weiteren Zweig erstellen. Dies ermöglicht bis zu zwei _aktive_ Zweige, die in Platform as a service (PageS)-Containern bereitgestellt werden.
- **Staging**: Stellt einen einzelnen `staging`-Zweig bereit, der in dedizierten Infrastructure as a service (IAAs)-Containern bereitgestellt wird.
- **Produktion**: Stellt eine einzelne `production` -Verzweigung bereit, die in dedizierten Infrastructure as a service (IAAs)-Containern bereitgestellt wird.

Die folgende Tabelle fasst die Unterschiede zwischen Umgebungen zusammen:

|                                        | INTEGRATION | STAGING | PRODUKTION |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| Unterstützt die Einstellungsverwaltung im [!DNL Cloud Console] | Ja | Begrenzt | Begrenzt |
| Unterstützt mehrere Zweige | Ja | Nein (nur Staging) | Nein (nur Produktion) |
| Verwendet YAML-Dateien für die Konfiguration | Ja | Nein | Nein |
| Wird auf dedizierter IAAs-Hardware ausgeführt | Nein | Ja | Ja |
| Enthält Fastly-CDN | Nein | Ja | Ja |
| Enthält New Relic-Dienst | Nein | APM | APM + NRI |
| Automatische Backups | Nein | Ja | Ja |

>[!NOTE]
>
>Adobe stellt das Cloud Docker-Tool für Commerce für die Bereitstellung in einer lokalen Cloud Docker-Umgebung bereit, damit Sie Adobe Commerce-Projekte entwickeln und testen können. Siehe [Docker-Entwicklung](../dev-tools/cloud-docker.md).

## Umgebungsarchitektur

Ihr Projekt ist ein einzelnes Git-Repository mit drei Hauptumgebungsverzweigungen: `integration`, `staging` und `production`. Das folgende Diagramm zeigt die hierarchische Beziehung von Pro-Umgebungen:

![Allgemeine Ansicht der Pro-Umgebung-Architektur](../../assets/pro-branch-architecture.png)

### Master-Umgebung

Bei Pro-Projekten stellt die Verzweigung `master` eine aktive PaaS-Umgebung für Ihre Produktionsumgebung bereit. Pushen Sie stets eine Kopie des Produktionscodes an die Umgebung `master` , damit Sie die Produktionsumgebung debuggen können, ohne die Dienste zu unterbrechen.

**Einschränkungen:**

- Erstellen Sie **nicht** einen Zweig, der auf dem Zweig `master` basiert. Verwenden Sie die Integrationsumgebung, um aktive Verzweigungen für die Entwicklung zu erstellen.

- Verwenden Sie nicht die `master` -Umgebung für Entwicklungs-, UAT- oder Leistungstests.

### Integrationsumgebung

Die Integrationsumgebung wird in einem Linux-Container (LXC) auf einem als &quot;PaaS&quot;bekannten Serverraster ausgeführt. Jede Umgebung enthält einen Webserver und eine Datenbank zum Testen Ihrer Site. Eine Liste der AWS- und Azure-IP-Adressen finden Sie unter [Regionale IP-Adressen](../project/regional-ip-addresses.md) .

**Empfohlene Anwendungsfälle:**

Integrationsumgebungen sind für begrenzte Tests und Entwicklung ausgelegt, bevor Änderungen in Staging- und Produktionsumgebungen verschoben werden. Beispielsweise können Sie die Integrationsumgebung verwenden, um die folgenden Aufgaben auszuführen:

- Sicherstellen, dass Änderungen an CI-Prozessen (Continuous Integration) Cloud-kompatibel sind

- Testen Sie kritische Workflows auf wichtigen Seiten wie Startseite, Kategorie, Produktdetailseite (PDP), Checkout und Admin

Befolgen Sie die folgenden Best Practices, um eine optimale Leistung in der Integrationsumgebung zu erzielen:

- Schränken Sie die Kataloggröße ein - Die Beispieldaten enthalten beispielsweise etwa 2.048 Produkte. Versuchen Sie, Ihre Kataloggröße auf etwa 4.000-5.000 Produkte zu reduzieren.

- Verringerung der Anzahl der Kundengruppen - Eine zu große Anzahl von Kundengruppen kann sich auf die Indizierungsleistung und die Gesamtleistung auswirken.

- Beschränkung der Verwendung auf einen oder zwei gleichzeitige Benutzer

- Deaktivieren Sie Cron-Aufträge und führen Sie sie nach Bedarf manuell aus.

**Einschränkungen:**

- Schnellere CDN- und New Relic-Dienste sind in einer Integrationsumgebung nicht verfügbar

- Die Architektur der Integrationsumgebung entspricht nicht der Staging- und Produktionsarchitektur

- Verwenden Sie nicht die `integration` -Umgebung für Entwicklungstests, Leistungstests oder Benutzerakzeptanztests.

- Verwenden Sie nicht die Umgebung &quot;`integration`&quot;, um B2B für Adobe Commerce-Funktionen zu testen.

- Sie können die Datenbank in der Integrationsumgebung nicht aus der Datenbankproduktion oder -staging wiederherstellen

{{enhanced-integration-envs}}

### Staging-Umgebung

Die Staging-Umgebung bietet eine nahezu produktionsorientierte Umgebung zum Testen Ihrer Site. Diese Umgebung, die auf dedizierter IaaS-Hardware gehostet wird, umfasst alle Dienste wie Fastly CDN, New Relic APM und Search.

**Empfohlene Anwendungsfälle:**

Die Umgebung entspricht der Produktionsarchitektur und wurde für UAT, Content Staging und endgültige Überprüfung entwickelt, bevor Funktionen in die `production` -Umgebung gepusht werden. Sie können beispielsweise die Umgebung `staging` verwenden, um die folgenden Aufgaben auszuführen:

- Regressionstests mit Produktionsdaten

- Leistungstests mit aktivierter Fastly-Caching-Funktion

- Testen neuer Builds anstelle von Patches in der Produktion

- UAT-Tests für neue Builds

- B2B-Test für Adobe Commerce

- Anpassen der Cron-Konfiguration und Testen von Cron-Aufträgen

Siehe [Freigabe-Workflow](pro-develop-deploy-workflow.md#deployment-workflow) und [Testen der Bereitstellung](../test/staging-and-production.md).

**Einschränkungen:**

- Verwenden Sie nach dem Start der Produktions-Site die Staging-Umgebung in erster Linie, um Patches auf produktionskritische Fehlerbehebungen zu testen.

- Sie können keine Verzweigung aus der Verzweigung `staging` erstellen. Stattdessen übernehmen Sie die Übertragung von Code-Änderungen vom Zweig `integration` in den Zweig `staging` .

### Produktionsumgebung

In der Produktionsumgebung werden Ihre öffentlichen Storefronts mit einzelnen und mehreren Sites ausgeführt. Diese Umgebung wird auf dedizierter iOS-Hardware mit redundanten Hochverfügbarkeitsknoten ausgeführt, die einen kontinuierlichen Zugriff und Failover-Schutz für Ihre Kunden ermöglichen. Die Produktionsumgebung umfasst alle Dienste in der Staging-Umgebung sowie den Dienst [New Relic Infrastructure (NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) , der automatisch eine Verbindung zu den Anwendungsdaten und Leistungsanalysen herstellt, um eine dynamische Serverüberwachung zu ermöglichen.

**Caveat:**

Sie können keine Verzweigung aus der Verzweigung `production` erstellen. Stattdessen übernehmen Sie die Übertragung von Code-Änderungen vom Zweig `staging` in den Zweig `production` .

### Produktionstechnologie-Stapel

Die Produktionsumgebung verfügt über drei virtuelle Maschinen (VMs) hinter einem Elastic Load Balancer, der von einem HAProxy pro VM verwaltet wird. Jede VM umfasst die folgenden Technologien:

- **Fastly CDN**—HTTP-Caching und CDN

- **NGINX**—Webserver mit PHP-FPM, einer Instanz mit mehreren Arbeitern

- **GlusterFS** - Dateiserver für die Verwaltung aller statischen Dateibereitstellungen und für die Synchronisierung mit vier Ordnerbereitstellungen:

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis** - ein Server pro VM mit nur einem aktiven Server und die beiden anderen als Replikate

- **Elasticsearch**—Suche nach Adobe Commerce in der Cloud-Infrastruktur 2.2 bis 2.4.3-p2

- **OpenSearch** - Suchen Sie in der Cloud-Infrastruktur 2.3.7-p3, 2.4.3-p2, 2.4.4 und höher nach Adobe Commerce.

- **Galera**—Datenbankcluster mit einer MariaDB MySQL-Datenbank pro Knoten mit einer automatischen Inkrementierungseinstellung von drei für eindeutige IDs in jeder Datenbank

Die folgende Abbildung zeigt die in der Produktionsumgebung verwendeten Technologien:

![Produktionstechnologiestapel](../../assets/az-stack-diagram.png)

## Redundante Hardware

Anstatt eine herkömmliche, aktive/passive `master`- oder eine primär-sekundäre Einrichtung auszuführen, führt Adobe Commerce in der Cloud-Infrastruktur eine _redundante Architektur_ aus, in der alle drei Instanzen Lese- und Schreibvorgänge akzeptieren. Diese Architektur bietet keine Ausfallzeiten bei der Skalierung und garantiert Transaktionsintegrität.

Aufgrund der einzigartigen, redundanten Hardware kann Adobe drei Gateway-Server bereitstellen. Die meisten externen Dienste ermöglichen es Ihnen, mehrere IP-Adressen zu einer Zulassungsliste hinzuzufügen, sodass es kein Problem darstellt, mehr als eine feste IP-Adresse zu haben. Die drei Gateways ordnen die drei Server im Cluster der Produktionsumgebung zu und behalten statische IP-Adressen bei. Sie ist vollständig redundant und auf allen Ebenen verfügbar:

- DNS
- Content Delivery Network (CDN)
- Elastic load balancer (ELB)
- Cluster mit drei Servern, das alle Adobe Commerce-Dienste einschließlich Datenbank und Webserver umfasst

## Sicherung und Wiederherstellung nach Katastrophen

Adobe Commerce on Cloud Infrastructure verwendet eine Hochverfügbarkeitsarchitektur, die jedes Pro-Projekt in drei separaten AWS- oder Azure-Verfügbarkeitszonen repliziert, wobei jede Zone über ein eigenes Rechenzentrum verfügt. Zusätzlich zu dieser Redundanz erhalten die Pro-Staging- und Produktionsumgebungen regelmäßige Live-Backups, die für die Verwendung bei _katastrophalen Fehlern_ entwickelt wurden.

**Automatische Sicherungen** enthalten persistente Daten von allen laufenden Diensten, wie z. B. der MySQL-Datenbank und Dateien, die auf den bereitgestellten Volumes gespeichert sind. Die Sicherungen werden in verschlüsselter Elastic Block Storage (EBS) in derselben Region wie die Produktionsumgebung gespeichert. Die automatischen Sicherungen sind nicht öffentlich zugänglich, da sie in einem separaten System gespeichert sind.

{{pro-backups}}

Sie können mithilfe von CLI-Befehlen eine **manuelle Sicherung** der Datenbank für Ihre Staging- und Produktionsumgebungen erstellen. Siehe [Sichern der Datenbank](../storage/database-dump.md). Für `integration` -Umgebungen empfiehlt Adobe, ein Backup als ersten Schritt nach dem Zugriff auf Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur zu erstellen, bevor Sie größere Änderungen vornehmen. Siehe [Backup management](../storage/snapshots.md).

### Ziel des Rückgewinnungspunkts

RPO ist eine maximale Zeitdauer von sechs Stunden bis zum letzten Backup (z. B. um 06:00 Uhr, dann um 12:00 Uhr, dann um 18:00 Uhr). Die Häufigkeit der Backups hängt vom Backup-Zeitplan Ihres Plans und dem Volumen der Änderungen ab, die in den Speicherdienst geschrieben werden sollen.

### Bindungsrichtlinie

Adobe behält automatische Sicherungen gemäß der folgenden Datenaufbewahrungsrichtlinie bei:

| Zeitraum | Richtlinie zur Sicherung der Datenaufbewahrung |
| ------------------ | ----------------------- |
| Tag 1 bis 3 | Ein Backup pro Stunde |
| Tage 4 bis 7 | Ein Backup pro Tag |
| Wochen 2 bis 6 | Ein Backup pro Woche |
| Wochen 8 bis 12 | Ein zweiwöchiges Backup |
| Monat 3 bis 5 | Ein Backup pro Monat |

Diese Richtlinie kann je nach Ihrem Cloud-Infrastrukturplan variieren.

### Recovery Time Objective

RTO hängt von der Speichergröße ab. Die Wiederherstellung großer EBS-Volumina nimmt mehr Zeit in Anspruch. Die Wiederherstellungszeiten variieren je nach Größe Ihrer Datenbank:

- Eine große Datenbank (200+ GB) kann 5 Stunden dauern
- Eine mittlere Datenbank (150 GB) kann 2 1/2 Stunden dauern
- Eine kleine Datenbank (60 GB) kann eine Stunde dauern

## Pro Cluster-Skalierung

Die Konfigurationen für die Größe des Pro-Clusters und _compute_ variieren je nach gewähltem Cloud-Anbieter (AWS, Azure), Region und Service-Abhängigkeiten. Adobe Cloud-Infrastruktur kann Pro-Cluster skalieren, um Verkehrserwartungen und Service-Anforderungen bei sich ändernden Anforderungen gerecht zu werden.

Die redundante Architektur ermöglicht das Hochskalieren der Adobe-Cloud-Infrastruktur ohne Ausfallzeiten. Beim Hochskalieren rotiert jede der drei Instanzen auf die Upgrade-Kapazität, ohne dass sich dies auf den Betrieb des Standorts auswirkt. Beispielsweise können Sie einem vorhandenen Cluster zusätzliche Webserver hinzufügen, wenn die Beschränkung auf PHP-Ebene und nicht auf Datenbankebene erfolgt. Dies ermöglicht die _horizontale Skalierung_, um die vertikale Skalierung zu ergänzen, die von zusätzlichen CPUs auf Datenbankebene bereitgestellt wird. Siehe [Skalierte Architektur](scaled-architecture.md).

Wenn Sie aus einem Ereignis oder aus anderen Gründen einen signifikanten Anstieg des Traffics erwarten, können Sie eine vorübergehende Erhöhung der Kapazität anfordern. Siehe [Anfordern einer temporären Upsize-Datei](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) im _Commerce Help Center_.
