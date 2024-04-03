---
title: Übersicht über Fastly Services
description: Erfahren Sie, wie Sie mit den in der Cloud-Infrastruktur von Adobe Commerce enthaltenen Fastly-Diensten die Bereitstellung von Inhalten für Ihre Adobe Commerce-Sites optimieren und sichern können.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: dc4500bf-f037-47f0-b7ec-5cd1291f73a1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Übersicht über Fastly Services

>[!WARNING]
>
>Um die PCI-Kompatibilität für Adobe Commerce-Sites zu gewährleisten, die auf der Cloud-Plattform bereitgestellt werden, richten Sie in Ihrer Starter-Hauptverzweigung, Pro Production- und Pro Staging-Umgebung schnell ein. Wenn Sie Adobe Commerce in einer Headless-Implementierung verwenden, wird dringend empfohlen, die GraphQL-Antworten schnell zwischenzuspeichern. Siehe [Caching mit Fastly](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) im *GraphQL-Entwicklerhandbuch*.

bietet die folgenden Dienste zur Optimierung und Sicherung der Inhaltsbereitstellung für Adobe Commerce in Cloud-Infrastrukturprojekten. Diese Dienste sind in Adobe Commerce in der Cloud-Infrastruktur ohne zusätzliche Kosten enthalten.

- **Content Delivery Network (CDN)**—Verschiedener Service, der Ihre Site-Seiten, Assets, CSS und mehr in von Ihnen eingerichteten Backend-Rechenzentren zwischenspeichert. Wenn Kunden auf Ihre Site und Ihre Stores zugreifen, drücken Sie schnell die Anforderungen, um zwischengespeicherte Seiten schneller zu laden. Der CDN-Dienst bietet die folgenden Funktionen:

- **Cacheverwaltung**- Zwischenspeichern Sie Ihre Siteseiten, Assets, CSS und mehr in Back-End-Rechenzentren, die Sie einrichten, um die Bandbreitenlast und -kosten zu reduzieren.

   - Verwendung [Schnell benutzerdefinierte VCL-Snippets](fastly-vcl-custom-snippets.md) (Kompatibel mit Version 2.1) zum Ändern der Reaktion der Zwischenspeicherung auf Anforderungen

   - Einrichten [GeoIP-Service-Unterstützung](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Erzwingen unverschlüsselter Anfragen an TLS](fastly-custom-cache-configuration.md#force-tls)

   - [Schnelles Timeout anpassen](fastly-custom-cache-configuration.md#extend-fastly-timeout) Einstellungen zum Verhindern von 503-Antworten auf Anfragen für Massenvorgänge

   - Erstellen [Benutzerdefinierte Fehlerantwortseiten](fastly-custom-response.md)

- **Sicherheit**—Nachdem Sie die Fastly-Dienste für Adobe Commerce-Sites aktiviert haben, stehen zusätzliche Sicherheitsfunktionen zum Schutz Ihrer Sites und Ihres Netzwerks zur Verfügung:

   - [Web-Anwendungs-Firewall](fastly-waf-service.md) (WAF) - Verwalteter Firewall-Dienst für Webanwendungen, der PCI-konformen Schutz bietet, um schädlichen Traffic zu blockieren, bevor er Ihre Adobe Commerce-Produktion auf Cloud-Infrastruktur-Sites und im Netzwerk schädigen kann. Der WAF-Dienst ist nur in Pro- und Starter Production-Umgebungen verfügbar.

   - [Schutz durch verteilte Denial of Service (DDoS)](#ddos-protection)—Integrierter DDoS-Schutz gegen häufige Angriffe wie Ping of Death, Smurf-Angriffe und andere ICMP-basierte Hochwasserangriffe.

   - [SSL-/TLS-Zertifikate](fastly-configuration.md#provision-ssltls-certificates)—Der Fastly-Dienst benötigt ein SSL-/TLS-Zertifikat, um sicheren Traffic über HTTPS bereitzustellen.

     Adobe Commerce bietet ein domänenvalidiertes Let&#39;s Encrypt SSL/TLS-Zertifikat für jede Staging- und Produktionsumgebung. Adobe Commerce schließt die Domänenvalidierung und die Zertifikatbereitstellung während der schnellen Einrichtung ab.

- **Origin-Maskierung**—Verhindert, dass der Traffic die Fastly WAF umgeht, und blendet die IP-Adressen Ihrer Herkunftsserver aus, um sie vor direktem Zugriff und DoS-Angriffen zu schützen.

  Die Ursprungsbearbeitung ist in Adobe Commerce in Cloud Infrastructure Pro Production-Projekten standardmäßig aktiviert. Um das Ursprungs-Cloaking in Adobe Commerce in Cloud-Infrastruktur-Starter-Produktionsprojekten zu aktivieren, müssen Sie eine [Support-Ticket für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Wenn Sie Traffic haben, der nicht zwischengespeichert werden muss, können Sie die Konfiguration des Fastly-Dienstes anpassen, um Anforderungen zu ermöglichen, [Umgehen des Fastly-Cache](fastly-vcl-bypass-to-origin.md).

- **[Bildoptimierung](fastly-image-optimization.md)**—Lädt die Bildverarbeitung und Größenanpassung an den Fastly-Dienst aus, damit Server Bestellungen und Konversionen effizienter verarbeiten können.

- **[Schnelles CDN- und WAF-Protokoll](../monitor/new-relic-service.md#new-relic-log-management)**—Für Adobe Commerce on Cloud Infrastructure Pro-Projekte können Sie den New Relic Logs-Dienst verwenden, um CDN- und WAF-Protokolldaten schnell zu überprüfen und zu analysieren.

## Fastly CDN-Modul für Magento 2

Schnelle Dienste für Adobe Commerce in Cloud-Infrastrukturen verwenden die [Fastly CDN-Modul für Magento 2] installiert in den folgenden Umgebungen: Pro Staging and Production, Starter Production (`master` -Verzweigung).

Bei der ersten Bereitstellung oder Aktualisierung Ihres Adobe Commerce-Projekts installiert Adobe die neueste Version des Fastly CDN-Moduls in Ihren Staging- und Produktionsumgebungen. Wenn das Modul Fastly veröffentlicht wird, erhalten Sie im Admin Benachrichtigungen für Ihre Umgebungen. Adobe empfiehlt, dass Sie Ihre Umgebungen aktualisieren, um die neueste Version zu verwenden. Siehe [Schnelles Upgrade](fastly-configuration.md#upgrade-the-fastly-module).

## Schnelles Service-Konto und -Anmeldedaten

Adobe Commerces für Cloud-Infrastrukturprojekte erfordern kein spezielles Fastly-Konto oder keinen Kontoinhaber. Stattdessen verfügt jede Staging- und Produktionsumgebung über eindeutige Fastly-Anmeldeinformationen (API-Token und Service-ID) zum Konfigurieren und Verwalten von Fastly-Diensten über den Admin. Außerdem benötigen Sie die Anmeldeinformationen, um schnelle API-Anfragen zu senden.

Bei der Projektbereitstellung fügt Adobe Ihr Projekt zum Fastly-Dienstkonto für Adobe Commerce in der Cloud-Infrastruktur hinzu und fügt die Fastly-Anmeldeinformationen zur Konfiguration für die Staging- und Produktionsumgebungen hinzu. Siehe [Schnelles Abrufen von Anmeldedaten](fastly-configuration.md#get-fastly-credentials).

### Fastly-API-Token ändern

Senden Sie ein Adobe Commerce-Support-Ticket, um die Anmeldedaten für das schnelle API-Token zu ändern. Wenn Sie das neue Token erhalten, aktualisieren Sie Ihre Staging- oder Produktionsumgebung, um das neue Token zu verwenden.

**So ändern Sie die Anmeldedaten für das schnelle API-Token**:

1. [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) neue Fastly API-Anmeldeinformationen anzufordern.

   Schließen Sie Ihre Adobe Commerce in die Cloud-Infrastruktur-Projekt-ID und die Umgebungen ein, für die eine neue Berechtigung erforderlich ist.

1. Nachdem Sie das neue API-Token erhalten haben, aktualisieren Sie den API-Token-Wert im [Schnelle Konfiguration von Anmeldedaten](fastly-configuration.md#test-the-fastly-credentials) im Admin oder aus dem [[!DNL Cloud Console] Umgebungsvariablen](../project/overview.md#configure-environment).

1. [Testen der neuen Berechtigung](fastly-configuration.md#test-the-fastly-credentials).

1. Nachdem Sie die Berechtigung aktualisiert haben, senden Sie ein Adobe Commerce Support-Ticket, um das alte API-Token zu löschen.

### Mehrere schnelle Konten und zugewiesene Domänen

Fastly ermöglicht es Ihnen nur, eine Apex-Domäne und zugehörige Subdomains einem Fastly-Dienst und -Konto zuzuweisen. Wenn Sie über ein vorhandenes Fastly-Konto verfügen, das denselben Apex und dieselben Subdomänen verknüpft, die für Ihre Adobe Commerce-Site verwendet werden, haben Sie die folgenden Optionen:

- Entfernen Sie die Apex- und Subdomänen aus dem vorhandenen Konto, bevor Sie die Fastly-Service-Anmeldeinformationen für Ihre Adobe Commerce in Cloud-Infrastruktur-Projektumgebungen anfordern. Siehe [Arbeiten mit Domänen] in der Fastly-Dokumentation.

  Verwenden Sie diese Option, um die Apex-Domäne und alle Subdomänen mit dem Fastly-Dienstkonto für Adobe Commerce in der Cloud-Infrastruktur zu verknüpfen.

- Senden Sie ein Adobe Commerce-Support-Ticket, um eine Domain-Zuweisung anzufordern, damit Apex und Subdomains mit verschiedenen Konten verknüpft werden können.

  Verwenden Sie diese Option, wenn Sie über eine Apex-Domäne verfügen, die über mehrere Subdomänen für Adobe Commerce- und Nicht-Adobe Commerce-Sites verfügt und Sie diese Subdomänen mit verschiedenen Fastly-Konten verknüpfen möchten.

#### Domain-Zuweisung anfordern

*Szenario 1:*

Die Apex-Domäne (`testweb.com` und `www.testweb.com`) mit einem vorhandenen Fastly-Konto verknüpft ist. Sie haben ein Adobe Commerce on Cloud-Infrastrukturprojekt mit den folgenden Subdomains konfiguriert: `mcstaging.testweb.com` und `mcprod.testweb.com`. Sie möchten die Apex-Domäne nicht in das Fastly-Dienstkonto für Adobe Commerce in der Cloud-Infrastruktur verschieben.

Senden einer [Schnelles Support-Ticket] fordert, dass die Subdomains vom vorhandenen Fastly-Konto an das Fastly-Konto für Adobe Commerce in der Cloud-Infrastruktur delegiert werden. Fügen Sie Ihre Adobe Commerce-Projekt-ID in das Ticket ein.

Nachdem die Zuweisung abgeschlossen ist, können Ihre Projekt-Subdomains zum Fastly-Dienstkonto für Adobe Commerce in der Cloud-Infrastruktur hinzugefügt werden. Siehe [Schnelles Abrufen von Anmeldedaten](fastly-configuration.md#get-fastly-credentials).

*Szenario 2:*

Die Apex-Domäne (`testweb.com` und `www.testweb.com`) mit dem Adobe Commerce-Konto für Cloud-Infrastruktur Fastly-Service verknüpft ist. Sie möchten die Fastly-Dienste für die `service.testweb.com` und `product-updates.testweb.com` Subdomains von einem anderen Schnellkonto aus.

Senden Sie ein Adobe Commerce Support-Ticket, in dem Sie darum bitten, die Subdomains von der Adobe Commerce über das Cloud Infrastructure Fastly-Dienstkonto an das Fastly-Konto zu delegieren. Fügen Sie die Dienst-ID für das Fastly-Konto in das Ticket ein.

## DDoS-Schutz

Der DDOS-Schutz ist in den Fastly CDN-Dienst integriert. Sobald Sie die Fastly-Dienste für Ihre Adobe Commerce-Sites aktiviert haben, filtert Fastly den gesamten Web- und Admin-Traffic, um potenzielle Angriffe zu erkennen und zu blockieren.

- Bei Angriffen, die auf Ebene 3 oder 4 abzielen, filtert der Fastly-Dienst Traffic basierend auf Port und Protokoll heraus und prüft nur HTTP- oder HTTPS-Anforderungen. ICMP-, UDP- und andere netzwerkinitiierte Angriffe werden an unserem Netzwerkrand abgelegt. Dazu gehören Reflektions- und Verstärkungs-Angriffe, die UDP-Dienste wie SSDP oder NTP verwenden. Indem wir dieses Schutzniveau bieten, blockieren wir effektiv mehrere häufige Angriffe wie Ping of Death, Smurf-Angriffe und andere Überschwemmungen auf ICMP-Basis.

  Verwaltet schnell TCP-Level-Angriffe auf der Cache-Ebene. Diese Strategie bietet für jeden Client die notwendige Skala und den erforderlichen Kontext, um mit einem SYN-Hochwasserangriff und seinen vielen Varianten umzugehen, einschließlich TCP-Stack, Ressourcenangriffe und TLS-Angriffe in Fastly-Systemen.

- Fastly bietet auch Schutz vor Layer 7-Angriffen. Wenn bei Ihrem Store Leistungsprobleme auftreten und Sie einen Layer 7-DDoS-Angriff vermuten, senden Sie ein Adobe Commerce Support-Ticket. Adobe kann benutzerdefinierte Regeln erstellen und auf den Fastly-Dienst anwenden, um böswillige Anforderungen basierend auf Header, Payload oder einer Kombination von Attributen, die den Angriffs-Traffic identifizieren, zu untersuchen und herauszufiltern. Siehe [Überprüfen auf DoS-Angriffe] und [Blockieren von böswilligem Traffic] im *Adobe Commerce Help Center*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Überprüfen auf DoS-Angriffe]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Fastly CDN-Modul für Magento 2]: https://github.com/fastly/fastly-magento2

[Schnelles Support-Ticket]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[Blockieren von böswilligem Traffic]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Arbeiten mit Domänen]: https://docs.fastly.com/en/guides/working-with-domains
