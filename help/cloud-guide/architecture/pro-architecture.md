---
title: Pro Architektur
description: Erfahren Sie mehr über die Umgebungen, die von der Pro-Architektur unterstützt werden.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: 95b033ba430cb5dc74fa654b9d519dfcd5b6d319
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Pro Architektur

Ihre Adobe Commerce on Cloud Infrastructure Pro-Architektur unterstützt mehrere Umgebungen, mit denen Sie Ihren Store entwickeln, testen und starten können.

- **Master**—Stellt eine `master` -Verzweigung, die in Platform as a Service (PageS)-Containern bereitgestellt wird.
- **Integration**—Stellt eine einzelne `integration` -Verzweigung zur Entwicklung, Sie können jedoch eine weitere Verzweigung erstellen. Dies ermöglicht bis zu zwei _active_ Verzweigungen, die in Platform as a Service (PageS)-Containern bereitgestellt werden.
- **Staging**—Stellt eine einzelne `staging` in dedizierten Infrastructure as a service (IAAS)-Containern bereitgestellt.
- **Produktion**—Stellt eine einzelne `production` in dedizierten Infrastructure as a service (IAAS)-Containern bereitgestellt.

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

Ihr Projekt ist ein einzelnes Git-Repository mit drei Hauptumgebungszweigen: `integration`, `staging`, und `production`. Das folgende Diagramm zeigt die hierarchische Beziehung von Pro-Umgebungen:

![Allgemeine Ansicht der Pro-Umgebungs-Architektur](../../assets/pro-branch-architecture.png)

### Master-Umgebung

Bei Pro-Projekten wird die `master` -Verzweigung bietet eine aktive PaaS-Umgebung für Ihre Produktionsumgebung. Pushen Sie stets eine Kopie des Produktionscodes an die `master` -Umgebung, sodass Sie die Produktionsumgebung debuggen können, ohne die Dienste zu unterbrechen.

**Einschränkungen:**

- Do **not** Erstellen Sie eine Verzweigung basierend auf der `master` -Verzweigung. Verwenden Sie die Integrationsumgebung, um aktive Verzweigungen für die Entwicklung zu erstellen.

- Verwenden Sie nicht das `master` Umgebung für Entwicklungs-, UAT- oder Leistungstests

### Integrationsumgebung

Die Integrationsumgebung wird in einem Linux-Container (LXC) auf einem als &quot;PaaS&quot;bekannten Serverraster ausgeführt. Jede Umgebung enthält einen Webserver und eine Datenbank zum Testen Ihrer Site. Siehe [Regionale IP-Adressen](../project/regional-ip-addresses.md) für eine Liste von AWS- und Azure-IP-Adressen.

**Empfohlene Anwendungsfälle:**

Integrationsumgebungen sind für begrenzte Tests und Entwicklung ausgelegt, bevor Änderungen in Staging- und Produktionsumgebungen verschoben werden. Beispielsweise können Sie die Integrationsumgebung verwenden, um die folgenden Aufgaben auszuführen:

- Sicherstellen, dass Änderungen an CI-Prozessen (Continuous Integration) Cloud-kompatibel sind

- Testen Sie kritische Workflows auf wichtigen Seiten wie Startseite, Kategorie, Produktdetailseite (PDP), Checkout und Admin

Befolgen Sie die folgenden Best Practices, um eine optimale Leistung in der Integrationsumgebung zu erzielen:

- Eingrenzen der Kataloggröße

- Beschränkung der Verwendung auf einen oder zwei gleichzeitige Benutzer

- Deaktivieren Sie Cron-Aufträge und führen Sie sie nach Bedarf manuell aus.

**Einschränkungen:**

- Schnellere CDN- und New Relic-Dienste sind in einer Integrationsumgebung nicht verfügbar

- Die Architektur der Integrationsumgebung entspricht nicht der Staging- und Produktionsarchitektur

- Verwenden Sie nicht das `integration` Umgebung für Entwicklungstests, Leistungstests oder Benutzerakzeptanztests (UAT)

- Verwenden Sie nicht das `integration` Umgebung zum Testen von B2B für Adobe Commerce-Funktionen

- Sie können die Datenbank in der Integrationsumgebung nicht aus der Datenbankproduktion oder -staging wiederherstellen

{{enhanced-integration-envs}}

### Staging-Umgebung

Die Staging-Umgebung bietet eine nahezu produktionsorientierte Umgebung zum Testen Ihrer Site. Diese Umgebung, die auf dedizierter IaaS-Hardware gehostet wird, umfasst alle Dienste wie Fastly CDN, New Relic APM und Search.

**Empfohlene Anwendungsfälle:**

Die Umgebung entspricht der Produktionsarchitektur und ist für UAT, Content Staging und endgültige Überprüfung konzipiert, bevor Funktionen an die `production` Umgebung. Sie können beispielsweise die `staging` Umgebung, um die folgenden Aufgaben auszuführen:

- Regressionstests mit Produktionsdaten

- Leistungstests mit aktivierter Fastly-Caching-Funktion

- Testen neuer Builds anstelle von Patches in der Produktion

- UAT-Tests für neue Builds

- B2B-Test für Adobe Commerce

- Anpassen der Cron-Konfiguration und Testen von Cron-Aufträgen

Siehe [Bereitstellungsarbeitsablauf](pro-develop-deploy-workflow.md#deployment-workflow) und [Testen der Bereitstellung](../test/staging-and-production.md).

**Einschränkungen:**

- Verwenden Sie nach dem Start der Produktions-Site die Staging-Umgebung in erster Linie, um Patches auf produktionskritische Fehlerbehebungen zu testen.

- Sie können eine Verzweigung nicht über die `staging` -Verzweigung. Stattdessen können Sie Codeänderungen über die `integration` -Verzweigung `staging` -Verzweigung.

### Produktionsumgebung

In der Produktionsumgebung werden Ihre öffentlichen Storefronts mit einzelnen und mehreren Sites ausgeführt. Diese Umgebung wird auf dedizierter iOS-Hardware mit redundanten Hochverfügbarkeitsknoten ausgeführt, die einen kontinuierlichen Zugriff und Failover-Schutz für Ihre Kunden ermöglichen. Die Produktionsumgebung umfasst alle Dienste in der Staging-Umgebung sowie die [New Relic Infrastructure (NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) -Dienst, der automatisch eine Verbindung zu den Anwendungsdaten und Leistungsanalysen herstellt, um eine dynamische Server-Überwachung zu ermöglichen.

**Warnung:**

Sie können eine Verzweigung nicht über die `production` -Verzweigung. Stattdessen können Sie Codeänderungen über die `staging` -Verzweigung `production` -Verzweigung.

### Produktionstechnologie-Stapel

Die Produktionsumgebung verfügt über drei virtuelle Maschinen (VMs) hinter einem Elastic Load Balancer, der von einem HAProxy pro VM verwaltet wird. Jede VM umfasst die folgenden Technologien:

- **Fastly CDN**—HTTP-Caching und CDN

- **NGINX**—Webserver mit PHP-FPM, einer Instanz mit mehreren Arbeitern

- **GlusterFS**—Dateiserver für die Verwaltung aller statischen Dateibereitstellungen und Synchronisation mit vier Ordnerbereitstellungen:

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis**—ein Server pro VM mit nur einem aktiven Server und die beiden anderen als Replikate

- **Elasticsearch**—Suche nach Adobe Commerce in der Cloud-Infrastruktur 2.2 bis 2.4.3-p2

- **OpenSearch**—Suche nach Adobe Commerce in der Cloud-Infrastruktur 2.3.7-p3, 2.4.3-p2, 2.4.4 und höher

- **Galera**—Datenbankcluster mit einer MySQL-Datenbank von MariaDB pro Knoten mit einer automatischen Inkrementierungseinstellung von drei für eindeutige IDs in jeder Datenbank

Die folgende Abbildung zeigt die in der Produktionsumgebung verwendeten Technologien:

![Produktionstechnologie-Stapel](../../assets/az-stack-diagram.png)

## Redundante Hardware

Anstatt ein traditionelles, aktives Passiv zu betreiben `master` oder bei einem primären sekundären Setup führt Adobe Commerce in der Cloud-Infrastruktur einen _redundante Architektur_ wobei alle drei Instanzen Lese- und Schreibvorgänge akzeptieren. Diese Architektur bietet keine Ausfallzeiten bei der Skalierung und garantiert Transaktionsintegrität.

Aufgrund der einzigartigen, redundanten Hardware kann Adobe drei Gateway-Server bereitstellen. Die meisten externen Dienste ermöglichen es Ihnen, mehrere IP-Adressen zu einer Zulassungsliste hinzuzufügen, sodass es kein Problem darstellt, mehr als eine feste IP-Adresse zu haben. Die drei Gateways ordnen die drei Server im Cluster der Produktionsumgebung zu und behalten statische IP-Adressen bei. Sie ist vollständig redundant und auf allen Ebenen verfügbar:

- DNS
- Content Delivery Network (CDN)
- Elastic load balancer (ELB)
- Cluster mit drei Servern, das alle Adobe Commerce-Dienste einschließlich Datenbank und Webserver umfasst

## Sicherung und Wiederherstellung nach Katastrophen

Adobe Commerce on Cloud Infrastructure verwendet eine Hochverfügbarkeitsarchitektur, die jedes Pro-Projekt in drei separaten AWS- oder Azure-Verfügbarkeitszonen repliziert, wobei jede Zone über ein eigenes Rechenzentrum verfügt. Zusätzlich zu dieser Redundanz erhalten die Staging- und Produktionsumgebungen von Pro regelmäßige Live-Backups, die für die Verwendung in Fällen von _Katastrophenversagen_.

**Automatische Backups** enthalten persistente Daten aus allen laufenden Diensten, wie z. B. der MySQL-Datenbank und Dateien, die auf den bereitgestellten Volumes gespeichert sind. Die Sicherungen werden in verschlüsselter Elastic Block Storage (EBS) in derselben Region wie die Produktionsumgebung gespeichert. Die automatischen Sicherungen sind nicht öffentlich zugänglich, da sie in einem separaten System gespeichert sind.

{{pro-backups}}

Sie können eine **manuelles Backup** der Datenbank für Ihre Staging- und Produktionsumgebungen mithilfe von CLI-Befehlen. Siehe [Datenbank sichern](../storage/database-dump.md). Für `integration` -Umgebungen, empfiehlt Adobe die Erstellung eines Backups als ersten Schritt nach dem Zugriff auf Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur und vor der Anwendung größerer Änderungen. Siehe [Backup-Management](../storage/snapshots.md).

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

Die Clustergröße von Pro und _berechnen_ -Konfigurationen variieren je nach gewähltem Cloud-Anbieter (AWS, Azure), Region und Service-Abhängigkeiten. Adobe Cloud-Infrastruktur kann Pro-Cluster skalieren, um Verkehrserwartungen und Service-Anforderungen bei sich ändernden Anforderungen gerecht zu werden.

Die redundante Architektur ermöglicht das Hochskalieren der Adobe-Cloud-Infrastruktur ohne Ausfallzeiten. Beim Hochskalieren rotiert jede der drei Instanzen auf die Upgrade-Kapazität, ohne dass sich dies auf den Betrieb des Standorts auswirkt. Beispielsweise können Sie einem vorhandenen Cluster zusätzliche Webserver hinzufügen, wenn die Beschränkung auf PHP-Ebene und nicht auf Datenbankebene erfolgt. Diese _horizontale Skalierung_ um die vertikale Skalierung zu ergänzen, die von zusätzlichen CPUs auf Datenbankebene bereitgestellt wird. Siehe [Skalierte Architektur](scaled-architecture.md).

Wenn Sie aus einem Ereignis oder aus anderen Gründen einen signifikanten Anstieg des Traffics erwarten, können Sie eine vorübergehende Erhöhung der Kapazität anfordern. Siehe [Anfordern einer temporären Größe](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) im _Commerce Help Center_.
