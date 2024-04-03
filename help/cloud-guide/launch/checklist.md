---
title: Checkliste für Launch
description: Überprüfen Sie die Elemente der Checkliste für den Site-Start.
exl-id: 4525742e-18c5-40d1-975d-00ba3f3a51a0
source-git-commit: 5b0a691a4355f5eda31d42cd3da9925439dfb510
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Checkliste für Launch

Laden Sie vor der Bereitstellung in der Produktionsumgebung die [Checkliste für Launch](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf)und verwenden Sie es mit diesen Anweisungen, um zu bestätigen, dass Sie alle erforderlichen Konfigurationen und Tests abgeschlossen haben. Einen Überblick über den vollständigen Bereitstellungsprozess für Starter und Pro finden Sie unter [Bereitstellen Ihres Stores](../deploy/staging-production.md).

## Vollständiger Test in der Produktion

Siehe [Testen der Bereitstellung](../test/staging-and-production.md) zum Testen aller Aspekte Ihrer Sites, Stores und Umgebungen. Zu diesen Tests gehören die schnelle Überprüfung, Benutzerakzeptanztests (User Acceptance Tests, UAT) und Leistungstests.

## TLS und Fastly

Adobe stellt ein &quot;Let&#39;s Encrypt SSL/TLS&quot;-Zertifikat für jede Umgebung bereit. Dieses Zertifikat ist erforderlich, damit Fastly sicheren Traffic über HTTPS bereitstellen kann.

Um dieses Zertifikat zu verwenden, müssen Sie Ihre DNS-Konfiguration aktualisieren, damit Adobe die Domänenvalidierung abschließen und das Zertifikat auf Ihre Umgebung anwenden kann. Jede Umgebung verfügt über ein eindeutiges Zertifikat, das die Domänen für die Adobe Commerce auf in dieser Umgebung bereitgestellten Cloud-Infrastruktur-Sites abdeckt. Es wird empfohlen, die Konfigurationsaktualisierungen während der [Schnelles Einrichten](../cdn/fastly-configuration.md).

## DNS-Konfiguration mit Produktionseinstellungen aktualisieren

Wenn Sie bereit sind, Ihre Site zu starten, müssen Sie die DNS-Konfiguration aktualisieren, um den Traffic von Ihrer Produktionsumgebung über den Fastly-Dienst zu leiten.

**Voraussetzungen:**

- [Schnelles Einrichten und Testen in Ihrer Entwicklungsumgebung](../cdn/fastly-configuration.md#)

- Die Konfiguration der Produktionsumgebung wurde mit allen erforderlichen Domänen aktualisiert.

  In der Regel können Sie mit Ihrem technischen Kundenberater zusammenarbeiten, um alle Domänen und Subdomänen auf oberster Ebene hinzuzufügen, die für Ihre Geschäfte erforderlich sind. So können Sie die Domänen für Ihre Produktionsumgebung hinzufügen oder ändern: [Senden eines Adobe Commerce-Support-Tickets](https://support.magento.com/hc/en-us/articles/360019088251). Warten Sie auf die Bestätigung, dass Ihre Projektkonfiguration aktualisiert wurde.

  Bei Starter-Projekten müssen Sie die Domänen zu Ihrem Projekt hinzufügen. Siehe [Domänen verwalten](../cdn/fastly-custom-cache-configuration.md#manage-domains).

- SSL-/TLS-Zertifikat, das für Ihre Produktionsumgebungen bereitgestellt wurde.

  Wenn Sie die ACME-Anforderungsdatensätze für Ihre Produktionsdomänen während des Schnellsetup-Prozesses hinzugefügt haben, lädt Adobe das SSL-/TLS-Zertifikat automatisch in Ihre Produktionsumgebung hoch, wenn Sie die DNS-Konfiguration aktualisieren, um den Traffic an den Fastly-Dienst weiterzuleiten. Wenn Sie das Zertifikat nicht vorab bereitgestellt haben oder Ihre Domänen aktualisiert haben, muss Adobe die Domänenvalidierung abschließen und das Zertifikat bereitstellen, was bis zu 12 Stunden dauern kann.

### So aktualisieren Sie die DNS-Konfiguration für den Site-Start:

1. Aktualisieren Sie die folgende DNS-Konfiguration für Ihre Produktions-Site:

   - Legen Sie alle erforderlichen Umleitungen fest, insbesondere wenn Sie von einer vorhandenen Site migrieren.

   - Setzen Sie den Root-Ressourcendatensatz der Zone auf den Hostnamen.

   - Verringern Sie den Wert für &quot;Time-to-Live&quot;(TTL), um DNS-Informationen zu aktualisieren und Kunden auf den richtigen Produktionsspeicher zu verweisen.

     Wir empfehlen beim Wechsel des DNS-Eintrags einen deutlich niedrigeren TTL-Wert. Dieser Wert gibt dem DNS an, wie lange der DNS-Eintrag zwischengespeichert werden soll. Wenn der DNS verkürzt wird, wird er schneller aktualisiert. Beispielsweise können Sie den TTL-Wert beim Aktualisieren Ihrer Site von drei Tagen auf 10 Minuten ändern. Beachten Sie, dass eine Verkürzung des TTL-Werts die DNS-Infrastruktur zusätzlich belastet. Stellen Sie den vorherigen, höheren Wert nach dem Site-Start wieder her.


1. Fügen Sie CNAME-Einträge hinzu, um die Subdomains für Ihre Produktionsumgebung auf den Schnelldienst zu verweisen. `prod.magentocloud.map.fastly.net`, zum Beispiel:

   | Domäne oder Subdomäne | CNAME |
   | ----------------------- | -------------------------------- |
   | `www.<domain-name>.com` | prod.magentocloud.map.fastly.net |
   | `mystore.<domain-name>.com` | prod.magentocloud.map.fastly.net |

1. Fügen Sie bei Bedarf A-Datensätze hinzu, um die Apex-Domäne (`<domain-name>.com`) an die folgenden Fastly-IP-Adressen:

   | Apex-Domäne | ANAME |
   | --------------- | ----------------- |
   | `<domain-name>.com` | `151.101.1.124` |
   | `<domain-name>.com` | `151.101.65.124` |
   | `<domain-name>.com` | `151.101.129.124` |
   | `<domain-name>.com` | `151.101.193.124` |

>[!IMPORTANT]
>
>DNS-Anweisungen in [RFC 1034](https://www.rfc-editor.org/rfc/rfc1912) (**Abschnitt 2.4**) angeben, dass:
>_Ein CNAME-Eintrag darf nicht zusammen mit anderen Daten vorhanden sein. Anders ausgedrückt: Wenn suzy.podunk.xx ein Alias für use.podunk.xx ist, können Sie keinen MX-Eintrag für suzy.podunk.edu, keinen A-Datensatz oder sogar einen TXT-Eintrag haben._
>
>Aus diesem Grund sollten DNS-Einträge vom Typ `CNAME` für Subdomains und Typ `A` für Apex-Domänen (Stammdomänen). Das Verwerfen dieser Regel kann zu Störungen Ihres E-Mail-Dienstes oder der DNS-Verbreitung führen, da Sie die Möglichkeit verlieren, andere Datensätze wie MX oder NS hinzuzufügen. Einige DNS-Anbieter können dies durch interne Anpassungen umgehen, aber die Einhaltung des Standards gewährleistet Stabilität und Flexibilität (wie z. B. Änderung des DNS-Providers).

1. Aktualisieren Sie die Basis-URL.

   - Verwenden Sie SSH, um sich bei der Produktionsumgebung anzumelden.

     ```bash
     magento-cloud ssh -e production
     ```

   - Verwenden Sie die CLI, um die Basis-URL für Ihren Store zu ändern.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://www.<domain-name>.com/"
     ```

   **NOTE**: Sie können die Basis-URL auch über den Admin aktualisieren. Siehe [Store-URLs](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html) im _Adobe Commerce Stores and Purchase Experience Guide_.

1. Warten Sie einige Minuten, bis die Site aktualisiert wurde.

1. Testen Sie Ihre Site.

## Produktionskonfiguration überprüfen

Führen Sie einen endgültigen Durchlauf durch, um die Produktionskonfiguration für einen oder mehrere Stores zu validieren. Sie können die Konfiguration in der Produktionsumgebung aktualisieren. Wenn die Einstellungen schreibgeschützt sind, müssen Sie möglicherweise eine SSH-Verbindung öffnen und CLI-Befehle verwenden, um die Konfiguration zu ändern, oder Konfigurationsänderungen in Ihrer lokalen Umgebung vornehmen. Nach Abschluss der Aktualisierungen können Sie die Änderungen in den Staging- und Produktionsumgebungen bereitstellen.

Es werden folgende Änderungen und Prüfungen empfohlen:

- [Abgeschlossene ausgehende E-Mail-Tests](../project/outgoing-emails.md)

- [Sichere Konfiguration für Administratorberechtigungen und Basis-Admin-URL](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Alle Bilder für das Web optimieren](../cdn/fastly-image-optimization.md)

- [Überprüfen der Minimierungseinstellungen für HTML, JavaScript und CSS](../deploy/static-content.md)

## Schnelles Zwischenspeichern überprüfen

- Testen und überprüfen Sie, ob die schnelle Zwischenspeicherung auf der Produktions-Site ordnungsgemäß funktioniert. Detaillierte Tests und Prüfungen finden Sie unter [Schnelle Tests](../test/staging-and-production.md#check-fastly-caching).

- [Stellen Sie sicher, dass die neueste Version des Fastly CDN Module for Commerce in Ihrer Produktionsumgebung installiert ist.](../cdn/fastly-configuration.md#upgrade-the-fastly-module)

- [Stellen Sie sicher, dass die neueste Version des Fastly VCL-Codes hochgeladen wurde.](../cdn/fastly-configuration.md#upload-vcl-to-fastly)

## Leistungstests

Wir empfehlen Ihnen, die [Leistungs-Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) Optionen im Rahmen Ihres Vorab-Starts-Bereitstellungsprozesses.

Sie können auch mit den folgenden Drittanbieteroptionen testen:

- [Belagung](https://www.joedog.org/siege-home/): Software für Traffic-Formate und Tests, mit der Ihr Geschäft an die Grenzen gedrängt wird. Treffer auf Ihrer Site mit einer konfigurierbaren Anzahl simulierter Clients. Belagerung unterstützt grundlegende Authentifizierungs-, Cookies-, HTTP-, HTTPS- und FTP-Protokolle.

- [Jmeter](https://jmeter.apache.org/): Ausgezeichnete Belastungstests, mit denen die Leistung bei erhöhtem Traffic, wie z. B. bei Flash-Verkäufen, gemessen werden kann. Erstellen Sie benutzerdefinierte Tests, die für Ihre Site ausgeführt werden.

- [New Relic](https://support.newrelic.com/s/) (bereitgestellt): Hilft bei der Suche nach Prozessen und Bereichen der Site, die eine langsame Leistung mit der pro Aktion aufgezeichneten Zeit verursachen, wie das Senden von Daten, Abfragen, Redis und mehr.

- [WebPageTest](https://www.webpagetest.org/) und [Pingdom](https://www.pingdom.com/): Die Echtzeit-Analyse der Seiten Ihrer Site lädt die Zeit mit verschiedenen Ausgangspunkten. Pingdom könnte eine Gebühr kosten. WebPageTest ist ein kostenloses Tool.

## Sicherheitskonfiguration

- [Sicherheitsüberprüfung einrichten](overview.md#set-up-the-security-scan-tool)

- [Sichere Konfiguration für Admin-Benutzer](https://docs.magento.com/user-guide/stores/security-admin.html)

- [Sichere Konfiguration für Admin-URL](https://docs.magento.com/user-guide/stores/store-urls-custom-admin.html)

- [Entfernen Sie alle Benutzer, die nicht mehr in Adobe Commerce im Cloud-Infrastrukturprojekt verwendet werden](../project/user-access.md)

- [Zwei-Faktor-Authentifizierung konfigurieren](https://devdocs.magento.com/guides/v2.4/security/two-factor-authentication.html)

## Leistungsüberwachung

Sie können New Relic-Dienste für die Leistungsüberwachung in Pro- und Starter-Umgebungen verwenden. Auf Pro-Plan-Konten stellen wir die Warnhinweispolitik für verwaltete Warnhinweise für Adobe Commerce bereit, um die Anwendungs- und Infrastrukturleistung mit New Relic APM- und Infrastrukturagenten zu überwachen. Weitere Informationen zur Verwendung dieser Dienste finden Sie unter [Überwachen der Leistung mit verwalteten Warnhinweisen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

### Nächster Schritt

[Launch-Schritte](steps.md)
