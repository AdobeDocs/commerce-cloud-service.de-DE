---
title: Staging- und Produktionstests
description: Erfahren Sie, wie Sie in Staging- und Produktionsumgebungen testen können.
exl-id: 5b762d59-04c5-4e89-a637-719141759158
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Staging- und Produktionstests

Verwenden Sie nach erfolgreicher Migration von Code, Dateien und Daten in Staging oder Produktion die Umgebungs-URLs, um Ihre Sites und Stores zu testen. Im Folgenden finden Sie Informationen zum Überprüfen von Protokollen, zum Testen von Fastly-Konfigurationen, zum Testen von Benutzerakzeptanztests (UAT) und mehr.

## Protokolldateien

Wenn bei der Bereitstellung Fehler auftreten oder andere Probleme beim Testen auftreten, überprüfen Sie die Protokolldateien. Protokolldateien befinden sich unter der `var/log` Verzeichnis.

Das Bereitstellungsprotokoll befindet sich in `/var/log/platform/<prodject-ID>/deploy.log`. Der Wert von `<project-ID>` hängt von der Projekt-ID ab und davon, ob es sich bei der Umgebung um Staging oder Produktion handelt. Beispielsweise mit einer Projekt-ID von `yw1unoukjcawe`, lautet der Staging-Benutzer `yw1unoukjcawe_stg` und der Produktionsbenutzer `yw1unoukjcawe`.

Verwenden Sie beim Zugriff auf Protokolle in Produktions- oder Staging-Umgebungen SSH, um sich bei jedem der drei Knoten anzumelden, um die Protokolle zu finden. Oder Sie können [Protokollverwaltung von New Relic](../monitor/log-management.md) um aggregierte Protokolldaten aller Knoten anzuzeigen und abzufragen. Siehe [Protokolle anzeigen](log-locations.md#application-logs).

## Überprüfen der Codebasis

Stellen Sie sicher, dass Ihre Codebasis ordnungsgemäß in Staging- und Produktionsumgebungen bereitgestellt wird. Die Umgebungen sollten über identische Codegrundlagen verfügen.

## Konfigurationseinstellungen überprüfen

Überprüfen Sie die Konfigurationseinstellungen über das Admin-Bedienfeld, einschließlich Basis-URL, Basis-Admin-URL, Einstellungen für mehrere Sites und mehr. Wenn Sie weitere Änderungen vornehmen müssen, nehmen Sie die Änderungen in Ihrer lokalen Git-Verzweigung vor und pushen Sie zum `master` -Verzweigung in Integration, Staging und Produktion.

## Schnelles Zwischenspeichern überprüfen

[Schnelles Konfigurieren](../cdn/fastly-configuration.md) Sorgfältige Detailgenauigkeit erfordert: Verwendung der richtigen Fastly Service ID und der Fastly API Token-Anmeldeinformationen, Hochladen des Fastly VCL-Codes, Aktualisierung der DNS-Konfiguration und Anwendung der SSL/TLS-Zertifikate auf Ihre Umgebungen. Nach Abschluss dieser Einrichtungsaufgaben können Sie die schnelle Zwischenspeicherung in Staging- und Produktionsumgebungen überprüfen.

**Überprüfen der Konfiguration des Fastly-Dienstes**:

1. Melden Sie sich bei Admin für Staging und Produktion über die URL mit `/admin`oder die [aktualisierte Admin-URL](../environment/variables-admin.md#admin-url).

1. Navigieren Sie zu **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**. Scrollen und klicken **Vollständiger Seiten-Cache**.

1. Stellen Sie sicher, dass **Caching-Anwendung** Wert auf _Fastly CDN_ .

1. Testen Sie die Fastly-Anmeldeinformationen.

   - Klicks **Schnelle Konfiguration**.

   - Überprüfen Sie, ob die Werte für die Anmeldedaten für die Fastly Service ID und den Fastly API-Token vorhanden sind. Siehe [Schnelles Abrufen von Anmeldedaten](/help/cloud-guide/cdn/fastly-configuration.md#get-fastly-credentials).

   - Klicks **Testen von Anmeldeinformationen**.

   >[!WARNING]
   >
   >Vergewissern Sie sich, dass Sie in Ihren Staging- und Produktionsumgebungen die richtige Fastly Service-ID und das richtige API-Token eingegeben haben. Schnelle Anmeldeinformationen werden pro Dienstumgebung erstellt und zugeordnet. Wenn Sie in Ihrer Produktionsumgebung Staging-Anmeldeinformationen eingeben, können Sie Ihre VCL-Snippets nicht hochladen. Das Caching funktioniert nicht ordnungsgemäß und Ihre Caching-Konfiguration verweist auf den falschen Server und die falschen Stores.

**So überprüfen Sie das Verhalten beim schnellen Zwischenspeichern**:

1. Suchen Sie mithilfe der `dig` Befehlszeilen-Dienstprogramm, um Informationen zur Site-Konfiguration zu erhalten.

   Sie können jede beliebige URL mit der `dig` Befehl. Die folgenden Beispiele verwenden Pro-URLs:

   - Staging: `dig https://mcstaging.<your-domain>.com`
   - Produktion: `dig https://mcprod.<your-domain>.com`

   Für zusätzliche `dig` Tests, siehe Fastly&#39;s [Tests vor DNS-Änderung](https://docs.fastly.com/en/guides/working-with-domains).

1. Verwendung `cURL` , um die Informationen des Antwortheaders zu überprüfen.

   ```bash
   curl https://mcstaging.<your-domain>.com -H "host: mcstaging.<your-domain.com>" -k -vo /dev/null -H Fastly-Debug:1
   ```

   Siehe [Überprüfen von Antwortheadern](../cdn/fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) für Details zum Überprüfen der Kopfzeilen.

1. Wenn Sie live sind, verwenden Sie `cURL` , um Ihre Live-Site zu überprüfen.

   ```bash
   curl https://<your-domain> -k -vo /dev/null -H Fastly-Debug:1
   ```

## Vollständige UAT-Tests

Führen Sie Benutzerakzeptanztests (UAT) für Staging und Produktion durch. Die folgenden Tests sind eine kurze Liste möglicher Aufgaben und Bereiche, die als Händler und Kunde getestet werden können. Ihre Liste kann länger sein und zusätzliche Tests für benutzerdefinierte Module, Erweiterungen und Drittanbieterintegrationen enthalten. Verwenden Sie beim Testen Desktops, Laptops und Mobilgeräte.

Wenn Probleme auftreten, speichern Sie Ihre Reproduktionsschritte, Fehlermeldungen, seltsame Bildschirmaufzeichnungen und Links. Verwenden Sie diese Informationen, um Probleme im Code und Konfigurationen der Integrationsumgebung oder in den Umgebungseinstellungen zu untersuchen und zu beheben.

<table>
<tr>
<td style="width:150px">Benutzerverwaltung</td>
<td>
<ul>
<li>Kundenkonten erstellen und bearbeiten, E-Mails überprüfen</li>
<li>Erstellen von Administratorrollen für Händler</li>
<li>Erstellen von Handelskonten mit bestimmten Rollen</li>
<li>Testen des Händlerkontozugriffs pro Rolle</li>
</ul>
</td>
</tr>
<tr>
<td>Kataloge und Produkte</td>
<td>
<ul>
<li>Erstellen eines Katalogs mit zugehörigen Produkten</li>
<li>Erstellen Sie Produkte für Ihre Storefront, einschließlich aller Produkttypen: einfach, konfigurierbar, gebündelt</li>
<li>Hinzufügen von Produktbildern, Farbfeldern, Videos und anderen Medienoptionen</li>
<li>Preis, Rabatte, Preisregeln konfigurieren </li>
<li>Konfigurieren Sie erweiterte Funktionen wie Preisspannen, vorgestellte Produkte und Verfügbarkeitsdaten.</li>
<li>Inventar ändern und die korrekten Werte anzeigen und ändern pro Erhöhung und abgeschlossenem Kauf</li>
</ul>
</td>
</tr>
<tr>
<td>Warenkorb und Checkout</td>
<td>
<ul>
<li>Nach Produkten suchen und Filteroptionen auswählen</li>
<li>Produkte aus Suchergebnissen, Kategorieseiten und Produktseiten zum Warenkorb hinzufügen</li>
<li>Alle Produkttypen testen</li>
<li>Anzeigen des Warenkorbs und Ändern des Inhalts durch Entfernen oder Ändern von Beträgen </li>
<li>Checkout, um die Bestellmengen mit den Warenkorb- und Produktinformationen zu überprüfen</li>
<li>Überprüfen, ob die Steuer für den Warenkorb korrekt berechnet wird</li>
<li>Führen Sie einen Kauf mit verschiedenen Optionen durch: Fügen Sie einen Gutschein hinzu, wählen Sie Versand aus, geben Sie Versand- und Rechnungsinformationen sowie Zahlungsinformationen ein.</li>
<li>Überprüfen der Zahlungskanäle und -optionen beim Checkout</li>
<li>Überprüfen Sie auf On-Screen-Benachrichtigungen, im Kundenkonto aufgelistete Bestellungen und E-Mail-Benachrichtigungen.</li>
<li>Test des Gastes und des Kunden-Checkouts</li>
</ul>
</td>
</tr>
<tr>
<td>Auftragsverwaltung</td>
<td>
<ul>
<li>Erstellen einer Bestellung für einen Kunden</li>
<li>Suchen und Anzeigen von Bestellungen</li>
<li>Ändern einer Bestellung durch Hinzufügen und Entfernen von Produkten, Ändern von Beträgen, Ändern von Versand- und Rechnungsinformationen</li>
<li>Umgang mit Erstattungen</li>
<li>Abbrechen einer Bestellung</li>
<li>Couponcodes und Rabatte anwenden</li>
</ul>
</td>
</tr>
<tr>
<td>Site-Content</td>
<td>
<ul>
<li>Überprüfen Sie, ob alle Designs und Assets ordnungsgemäß geladen werden.</li>
<li>Überprüfen der korrekten Anzeige von CSS, einschließlich responsiver Mediengrößen</li>
<li>Überprüfen Sie die Geschäftsbedingungen, die Erstattungsrichtlinien und andere Informationen zu den Richtlinien.</li>
<li>Kontaktinformationen, Links und mehr zu Ihrem Unternehmen</li>
<li>Suchen Sie nach Produkten und Inhalten, überprüfen Sie die Filterung der Ergebnisse.</li>
<li>Fußzeilenblock und oberste Navigationsbausteine überprüfen</li>
<li>404- und Wartungsseiten testen</li>
</ul>
</td>
</tr>
<tr>
<td>Erweiterungen</td>
<td>
<ul>
<li>Überprüfen Sie alle Erweiterungseinstellungen, insbesondere für Steuer-, Versand- und Zahlungsmodule (z. B. an Lager- und Finanzverwaltungssystem gesendete Bestellung).</li>
<li>Testen aller benutzerdefinierten Module und installierten Erweiterungsinteraktionen</li>
<li>Überprüfen Sie die Daten auf alle Interaktionen, die abgeschlossen werden sollen (Zahlungen, Bestellungen, E-Mail-Benachrichtigungen).</li>
<li>Überprüfen der Konfigurationen pro Umgebung für Ihre Erweiterungen</li>
<li>Überprüfen der Abhängigkeiten zwischen Modulen und Erweiterungen funktioniert</li>
<li>Alle Aktionen als Händler und Kunde überprüfen</li>
</ul>
</td>
</tr>
<tr>
<td>Drittanbieterintegrationen</td>
<td>
<ul>
<li>Stellen Sie sicher, dass die Daten in Adobe Commerce korrekt gespeichert werden und exportiert, gepusht oder für den Drittanbieterdienst zugänglich sind (Beispiel: Bestellungen werden im Auftragsverwaltungssystem eines Drittanbieters angezeigt).</li>
<li>Konfigurationen und Interaktionen pro Integration überprüfen</li>
<li>Durchführen von Roundtrip-Tests mit Ursprung in Adobe Commerce und Ihrem Drittanbieter-Service</li>
<li>Überprüfen, ob die Authentifizierung abgeschlossen ist</li>
<li>Prüfen Sie, ob protokollierte Probleme auftreten, um Code-Integrationen oder Fehlermeldungen in den Control Panels zu aktualisieren.</li>
</ul>
</td>
</tr>
<tr>
<td>Backend-Tests</td>
<td>
<ul>
<li>Cache testen und löschen </li>
<li>Neuindizierungen durchführen und Ergebnisse überprüfen</li>
<li>Überprüfen Sie die Cron-Aufträge auf etwaige cron_schedule-Fehler.</li>
<li>Überprüfen und Überprüfen von Shell-Skriptproblemen</li>
<li>Prüfen Sie, ob protokollierte Probleme vorliegen: Anwendungsprotokolle, PHP-Protokolle, MySQL-Protokolle, E-Mail-Protokolle</li>
</ul>
</td>
</tr>
</table>

## Belastungs- und Belastungstests

Vor dem Start sollten Sie in Ihren Staging- und Produktionsumgebungen umfangreiche Traffic- und Leistungstests durchführen. Prüfen Sie die Leistung Ihrer Frontend- und Backend-Prozesse.

Bevor Sie mit dem Testen beginnen, geben Sie ein Ticket mit Support ein, das die getesteten Umgebungen, die verwendeten Tools und den Zeitrahmen berät. Aktualisieren Sie das Ticket mit Ergebnissen und Informationen, um die Leistung zu verfolgen. Fügen Sie nach Abschluss des Tests Ihre aktualisierten Ergebnisse hinzu und beachten Sie, dass der Tickettest mit einem Datums- und Zeitstempel abgeschlossen ist.

Überprüfen Sie die [Leistungs-Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) Optionen im Rahmen Ihres Vorab-Starts-Bereitstellungsprozesses.

Verwenden Sie die folgenden Tools, um die bestmöglichen Ergebnisse zu erzielen:

- [Leistungstest der Anwendung](../environment/variables-post-deploy.md#ttfb_tested_pages)—Testen Sie die Leistung der Anwendung, indem Sie die `TTFB_TESTED_PAGES` Umgebungsvariable zum Testen der Antwortzeit der Site.
- [Belagung](https://www.joedog.org/siege-home/)—Software für die Traffic-Formgebung und -Tests, um Ihr Geschäft an die Grenzen zu bringen. Treffer auf Ihrer Site mit einer konfigurierbaren Anzahl simulierter Clients. Belagerung unterstützt grundlegende Authentifizierungs-, Cookies-, HTTP-, HTTPS- und FTP-Protokolle.
- [Jmeter](https://jmeter.apache.org)—Ausgezeichnete Belastungstests zur Messung der Leistung bei erhöhtem Traffic, z. B. bei Flash-Verkäufen. Erstellen Sie benutzerdefinierte Tests, die für Ihre Site ausgeführt werden.
- [New Relic](../monitor/new-relic-service.md) (bereitgestellt) - Hilft bei der Suche nach Prozessen und Bereichen der Site, die eine langsame Leistung mit der pro Aktion aufgezeichneten Zeit verursachen, wie das Senden von Daten, Abfragen, Redis und mehr.
- [WebPageTest](https://www.webpagetest.org) und [Pingdom](https://www.pingdom.com)—Echtzeitanalyse der Seiten Ihrer Site Ladezeit mit verschiedenen Ausgangspunkten. Pingdom kann eine Gebühr verlangen. WebPageTest ist ein kostenloses Tool.

## Funktionstests

Sie können das Magento Functional Testing Framework (MFTF) verwenden, um Funktionstests für Adobe Commerce aus der Cloud Docker-Umgebung abzuschließen. Siehe [Anwendungstests](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) im _Handbuch zu Cloud Docker für Commerce_.

## Einrichten des Sicherheitsscan-Tools

Es gibt ein kostenloses Sicherheits-Scan-Tool für Ihre Sites. Informationen zum Hinzufügen Ihrer Sites und Ausführen des Tools finden Sie unter [Sicherheitsscan-Tool](../launch/overview.md#set-up-the-security-scan-tool).
