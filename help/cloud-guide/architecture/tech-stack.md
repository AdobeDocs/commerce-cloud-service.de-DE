---
title: Technologiestapel
description: Erfahren Sie mehr über den Technologiestapel, der die Commerce-Infrastruktur in Cloud bildet.
feature: Cloud, Iaas, Paas
exl-id: e456db25-c44b-4053-b96d-517d3d1606d0
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Technologiestapel

Stellen Sie sich die Adobe Commerce in der Cloud-Infrastruktur als fünf funktionale Ebenen vor, wie unten dargestellt:

![Cloud Stack](../../assets/CloudStack.svg)

1. [**Cloud-Infrastruktur**](pro-architecture.md): Wählen Sie entweder Amazon Web Services (AWS) oder Microsoft Azure als Grundlage für Ihre Infrastruktur-as-a-Service-Projekte (IAAs) für Ihre Adobe Commerce in Cloud-Infrastruktur Pro-Projekte.

   Adobe analysiert routinemäßig die Nutzung Ihrer Virtual Compute-Ressource (vCPU) und weist automatisch Ressourcen zu, um Ihre langfristige Nutzung zu optimieren und das Risiko einer Überschreitung der maximalen jährlichen vCPU-Tagesmenge zu verringern. Wenn Sie für bestimmte Zeiträume einen erhöhten Site-Traffic erwarten, müssen Sie weiterhin ein Support-Ticket für [temporäre Größe anfordern](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html).

1. [**Plattform als Dienst**](cloud-architecture.md): Jedes Adobe Commerce-Projekt zur Cloud-Infrastruktur bietet eine Plattform-as-a-Service-Integrationsumgebung (Platform as a Service, PAs) für die Entwicklung, Prüfung und Integration von Diensten.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce on Cloud Infrastructure bietet eine vorkonfigurierte Infrastruktur, die PHP, MySQL (MariaDB), Redis, [!DNL RabbitMQ]und unterstützte Suchmaschinentechnologien.
1. [**Leistungs-Tools**](../monitor/new-relic-service.md): Mit den New Relic-Leistungstools können Sie Ihre Anwendungen und Infrastrukturen debuggen, überwachen und verwalten, indem Sie Daten aus Ihrer Adobe Commerce zu Cloud-Infrastrukturprojekten erfassen, analysieren und anzeigen.
1. [**Content Delivery Network (CDN), Web Application Firewall ([!DNL WAF]) und Bildoptimierung (IO)**](../cdn/fastly.md):

   * [Fastly CDN](../cdn/fastly.md#ddos-protection)—Bietet sichere CDN-Dienste mit integriertem Schutz vor Denial-of-Service-Angriffen (Distributed Denial of Service, DDoS) wie [!DNL Ping of Death], [!DNL Smurf] Angriffe und andere auf dem Internet Control Message Protocol (ICMP) basierende Hochwasserangriffe.
   * [Web Application Firewall (WAF)](../cdn/fastly-waf-service.md)—WAF-Dienste gewährleisten PCI-Compliance für Adobe Commerce-Storefronts in Produktionsumgebungen und WAF-Richtlinien, die Ihre Adobe Commerce-Webanwendungen vor Injection-Angriffen, böswilligen Eingaben, Cross-Site-Scripting, Datenexfiltration, HTTP-Protokollverletzungen und anderen [[!DNL OWASP] Die zehn wichtigsten Sicherheitsbedrohungen](https://owasp.org/www-project-top-ten/).
   * [Bildoptimierung (IO)](../cdn/fastly-image-optimization.md)—Bietet Echtzeit-Bildbearbeitung und -optimierung, um die Bildbereitstellung zu beschleunigen und die Verwaltung von Bildquellen-Sets für responsive Webanwendungen zu vereinfachen. Schnelles IO-Abladen der Bildverarbeitung und Größenanpassung der Auslastung, wodurch Server effizient für die Verarbeitung von Bestellungen und Konversionen genutzt werden können.

Monolithische Anwendungen sind ressourcenintensiv und schwer zu skalieren und schnell zu bedienen. Mit der Cloud-Infrastruktur erhalten Commerce-Kunden beispiellosen Zugriff auf SaaS-basierte Microservices, die reich, intelligent und leistungsfähig sind. Siehe [Unterstützte Software und Dienste](cloud-architecture.md#supported-software-and-services).

Verwenden Sie die [Erste Schritte mit Commerce](../../get-started/overview.md) , um Ihr neues Cloud-Programm einzurichten und mit der Verwaltung Ihrer [!DNL Commerce] in einer Cloud-nativen Umgebung.
