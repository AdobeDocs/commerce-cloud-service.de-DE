---
title: Web Application Firewall (WAF)
description: Erfahren Sie, wie der Fastly WAF-Dienst bösartigen Anforderungs-Traffic erkennt, protokolliert und blockiert, bevor er das Adobe Commerce-Netzwerk oder die-Sites beschädigen kann.
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Web Application Firewall (WAF)

Mit dem WAP-Dienst (Web Application Firewall, WAF) für Adobe Commerce in der Cloud-Infrastruktur erkennt, protokolliert und blockiert böswilligen Anforderungs-Traffic, bevor er Ihre Sites oder Ihr Netzwerk beschädigen kann. Der WAF-Dienst ist nur in Produktionsumgebungen verfügbar.

Der WAF-Dienst bietet die folgenden Vorteile:

- **PCI compliance** - Die WAF-Aktivierung stellt sicher, dass Adobe Commerce-Storefronts in Produktionsumgebungen die PCI DSS 6.6-Sicherheitsanforderungen erfüllen.
- **Standard-WAF-Richtlinie**: Die standardmäßige WAF-Richtlinie, die von Fastly konfiguriert und gepflegt wird, bietet eine Sammlung von Sicherheitsregeln, die auf Ihre Adobe Commerce-Webanwendungen zugeschnitten sind, um sie vor einer Vielzahl von Angriffen zu schützen, einschließlich Injection-Angriffen, schädlichen Eingaben, Site-übergreifendem Scripting, Datenexfiltration, HTTP-Protokollverletzungen und anderen Sicherheitsbedrohungen vom Typ [OWASP Top Ten](https://owasp.org/www-project-top-ten/).
- **WAF-Onboarding und -Aktivieren** - Adobe stellt die standardmäßige WAF-Richtlinie in Ihrer Produktionsumgebung innerhalb von 2 bis 3 Wochen nach der endgültigen Bereitstellung bereit und aktiviert sie.
- **Betriebs- und Wartungsunterstützung**—
   - Adobe und Schnelles Einrichten und Verwalten Ihrer Protokolle und Warnhinweise für den WAF-Dienst.
   - Adobe testet Kunden-Support-Tickets zu WAF-Service-Problemen, die den legalen Traffic als Priorität 1-Probleme blockieren.
   - Automatisierte Upgrades auf die WAF-Dienstversion sorgen für eine sofortige Abdeckung neuer oder sich entwickelnder Exploits. Siehe [WAF-Wartung und -Upgrades](#waf-maintenance-and-updates).

>[!TIP]
>
>Weitere Informationen zur Aufrechterhaltung der PCI-Compliance für Ihre Adobe Commerce in Cloud-Infrastrukturspeichern finden Sie unter [PCI compliance](https://business.adobe.com/products/magento/pci-compliance.html).

## Aktivieren der WAF

Adobe ermöglicht den WAF-Dienst für neue Konten innerhalb von 2 bis 3 Wochen nach der endgültigen Bereitstellung. Die WAF wird über den Fastly CDN-Dienst implementiert. Sie müssen keine Hardware oder Software installieren oder warten.

>[!NOTE]
>
>Bevor Sie den WAF-Dienst verwenden können, müssen Sie den gesamten externen Traffic zu Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur über den Fastly-Dienst leiten. Siehe [Schnelles Einrichten](fastly-configuration.md).

## Funktionsweise

Der WAF-Dienst lässt sich mit Fastly integrieren und verwendet die Cache-Logik innerhalb des Fastly CDN-Dienstes, um den Traffic auf den schnell globalen Knoten zu filtern. Wir aktivieren den WAF-Dienst in Ihrer Produktionsumgebung mit einer standardmäßigen WAF-Richtlinie, die auf den [ModSecurity Rules von Trustwave SpiderLabs](https://github.com/owasp-modsecurity/ModSecurity) und den OWASP Top Ten-Sicherheitsbedrohungen basiert.

Der WAF-Dienst filtert HTTP- und HTTPS-Traffic (GET- und POST-Anfragen) gegen den WAF-Regelsatz und blockiert Traffic, der bösartig ist oder bestimmten Regeln nicht entspricht. Der Dienst filtert nur ursprungsgebundenen Traffic, der versucht, den Cache zu aktualisieren. Infolgedessen stoppen wir die meisten Angriffe auf Traffic im Fastly-Cache und schützen Ihren Ursprungs-Traffic vor bösartigen Angriffen. Durch die Verarbeitung des Ursprungs-Traffics behält der WAF-Dienst die Cache-Leistung bei und führt für jede nicht zwischengespeicherte Anforderung nur eine geschätzte Latenz von 1,5 bis 20 Millisekunden ein.

## Fehlerbehebung bei blockierten Anfragen

Wenn der WAF-Dienst aktiviert ist, filtert er den gesamten Web- und Admin-Traffic gegen die WAF-Regeln und blockiert jede Webanfrage, die Trigger einer Regel macht. Wenn eine Anforderung blockiert wird, wird dem Anfragenden eine standardmäßige Fehlerseite mit dem Fehler `403 Forbidden` angezeigt, die eine Referenz-ID für das Blockierungsereignis enthält.

![WAF-Fehlerseite](../../assets/cdn/fastly-waf-403-error.png)

Sie können diese Fehlerantwortseite vom Administrator anpassen. Siehe [Anpassen der WAF-Antwortseite](fastly-custom-response.md#customize-the-waf-error-page).

Wenn Ihre Adobe Commerce-Admin-Seite oder -Storefront als Antwort auf eine legitime URL-Anfrage eine Fehlerseite vom Typ `403 Forbidden` zurückgibt, senden Sie ein [Adobe Commerce-Supportticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Kopieren Sie die Referenz-ID von der Fehlerantwortseite und fügen Sie sie in die Ticketbeschreibung ein.

## Wartung und Aktualisierung der WAF

Pflege und Aktualisierung des WAF-Regelsatzes auf der Grundlage von Regelaktualisierungen kommerzieller Dritter, Fastly Research und Open Sources. Aktualisiert die veröffentlichten Regeln bei Bedarf oder wenn Änderungen an den Regeln aus den entsprechenden Quellen verfügbar sind, schnell in eine Richtlinie. Außerdem kann Fastly Regeln, die mit den veröffentlichten Regelklassen übereinstimmen, zur WAF-Instanz eines beliebigen Dienstes hinzufügen, nachdem der WAF-Dienst aktiviert wurde. Diese Updates gewährleisten eine sofortige Abdeckung neuer oder sich entwickelnder Exploits.

Adobe und verwalten Sie den Aktualisierungsprozess schnell, um sicherzustellen, dass neue oder geänderte WAF-Regeln in Ihrer Produktionsumgebung effektiv funktionieren, bevor die Aktualisierungen im Blockierungsmodus bereitgestellt werden.

## Einschränkungen

Der Standard-WAF-Dienst, der von Fastly unterstützt wird, unterstützt die folgenden Funktionen nicht:

- Schutz vor Malware oder Bot-Abschwächung - Erwägen Sie die Verwendung von [Zugriffssteuerungslisten](./fastly-vcl-allowlist.md) oder eines Drittanbieterdienstes.
- Ratenbegrenzung - Siehe [Ratenbegrenzung](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) in der Schnelldokumentation oder finden Sie unter [Ratenbegrenzung](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) im Sicherheitsabschnitt der _Commerce Web API_ .
- Konfigurieren eines Protokollierungsendpunkts für Kunden (siehe alternativ den [PrivateLink-Dienst](../development/privatelink-service.md) ).

Obwohl der WAF-Dienst es Ihnen nicht gestattet, den Traffic auf der Grundlage von IP-Adressen zu blockieren oder zuzulassen, können Sie Ihrem Fastly-Service Zugriffssteuerungslisten (ACL) und benutzerdefinierte VCL-Snippets hinzufügen, um die IP-Adressen und die VCL-Logik zum Blockieren oder Zulassen von Traffic anzugeben. Siehe [Benutzerdefinierte schnelle VCL-Snippets](fastly-vcl-custom-snippets.md).

Das Filtern nach TCP-, UDP- oder ICMP-Anforderungen wird vom WAF-Dienst nicht unterstützt. Diese Funktion wird jedoch durch den integrierten DDoS-Schutz bereitgestellt, der im Fastly CDN-Dienst enthalten ist. Siehe [DDoS-Schutz](fastly.md#ddos-protection).
