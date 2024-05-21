---
title: Cloud-Patches für Commerce
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud Patches-Pakets an.
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 61c42a1bd1d5a28f90b8756032ee6f45be4565b2
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 0%

---

# Cloud-Patches für Commerce

Die [Cloud-Patches](https://github.com/magento/magento-cloud-patches) Das -Paket bietet eine Reihe erforderlicher Patches, die die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen verbessern und die schnelle Bereitstellung kritischer Fehlerbehebungen unterstützen.

Das Paket Cloud Patches für Commerce ist eine Abhängigkeit vom Paket ECE-Tools und wird installiert und aktualisiert, wenn Sie das Paket ECE-Tools installieren oder aktualisieren. Sie können Cloud Patches für Commerce auch als eigenständiges Paket verwenden und verwalten, um Patches auf ein Adobe Commerce-Projekt anzuwenden, das sich nicht auf der Cloud-Plattform befindet. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben.

>[!TIP]
>
>Um sicherzustellen, dass Ihr Projekt alle erforderlichen Patches aufweist, aktualisieren Sie auf [neueste Version der Eece-Tools](../dev-tools/update-package.md).

>[!NOTE]
>
>Siehe [Anwenden von Patches](../development/apply-patches.md) für Anweisungen zum Anwenden von Patches auf Ihre Projekte.

Die `magento/magento-cloud-patches` -Paket verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.27 {#latest}

Veröffentlichungsdatum: 21. Mai 2024

- **Unterstützung für PHP 8.3**—Dieser Patch löst Kompatibilitätsfehler zwischen PHP 8.3 und der Composer-Paketversion.

## v1.0.26

Veröffentlichungsdatum: 8. April 2024

- ![Neues Symbol](../../assets/new.svg) **PHP** — Unterstützung für PHP 8.3 hinzugefügt.

## v1.0.25

Veröffentlichungsdatum: 16. Januar 2024

- **Cache-Verbesserungen**-Dieser Patch verbessert die Effizienz des Layout-Caches und reduziert die Speicherbelegung für Adobe Commerce-Versionen 2.4.4 und höher erheblich.<!-- MCLOUD-11514 -->
- **Verbesserungen bei CRON-Aufträgen**-Dieser Patch behebt das Problem, dass verpasste Aufträge unnötig auf Cron-Auftragssperren für Adobe Commerce-Versionen 2.4.4 und höher warten.<!-- MCLOUD-11329 -->

## v1.0.24

Veröffentlichungsdatum: 15. September 2023

- **Leistungsverbesserung**-Dieser Patch behebt ein Problem, das die Leistung beeinträchtigt, indem die Anzahl der Ladevorgänge derselben Implementierungskonfigurationen für Adobe Commerce 2.4.6 auf 2.4.6-p1 reduziert wird.<!-- MCLOUD-10604 -->

## v1.0.23

Veröffentlichungsdatum: 31. Juli 2023

- **Patch MCLOUD-10604 entfernt**-Dieser Patch wurde nach QPT verschoben.<!-- MCLOUD-10736 -->

## v1.0.22

Veröffentlichungsdatum: 19. Juni 2023

- **Verbesserter QPT-CLI-Assistent/-Ausgabe**—Es wurde eine Warnung zum QPT CLI-Assistenten/-Output hinzugefügt, die Sie daran erinnert, Patch-Details und -Anforderungen zu überprüfen, wenn Abhängigkeiten vorhanden sind.<!-- ACP2E-1963 -->
- **Es wurden Patches für Commerce 2.4.6 hinzugefügt:**
   - Die `regexp cache tag` Validierung.<!-- MCLOUD-10226 -->
   - Die Leistung wurde verbessert, indem die Anzahl der Ladevorgänge derselben Implementierungskonfigurationen verringert wird.<!-- MCLOUD-10604 -->
- **Patches für Commerce 2.3.7 zu 2.4.6 hinzugefügt**—Korrektur eines Problems, das dazu führte, dass für die `catalog_product_entity_*` -Tabellen.<!-- MCLOUD-10032 -->
- **Patches für Commerce 2.4.0 zu 2.4.6 hinzugefügt**—Fehlerkorrektur - kein Fehler mehr bei der Angabe von `The file can't be deleted. Warning!unlink: No such file or directory`, das beim Leeren des JS/CSS-Cache vom Admin auftrat.<!-- MCLOUD-10279 -->

## v1.0.21

Veröffentlichungsdatum: 10. März 2023

- **Erweiterte Unterstützung für PHP 8.2**—Es wurden Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen behoben, um Commerce 2.4.6 zu unterstützen.

## v1.0.20

Veröffentlichungsdatum: 27. Oktober 2022

- **Patch für Verbesserungen des L2-Cache hinzugefügt**—Dieser Patch behebt ein Problem beim Leeren des lokalen L2-Cache für Commerce-Versionen 2.4.0 und 2.4.1.<!-- MCLOUD-7845 -->

## v1.0.19

Veröffentlichungsdatum: 13. September 2022

- **Erweiterte Unterstützung für PHP 8.1**—Es wurden Kompatibilitätsprobleme mit bestimmten PHP 8.1.x-Versionen behoben.

## v1.0.18

Veröffentlichungsdatum: 11. August 2022

Kritischer Patch für Adobe Commerce 2.4.5:

- **Problem mit Bestellungen unter Verwendung von Braintree-Zahlungen**—Mit diesem Patch wird ein kritisches Problem behoben, das Administratoren daran hindert, neue Bestellungen oder Neubestellungen zu tätigen.<!-- MCLOUD-9137 -->

Siehe [Der Administrator kann keine Bestellung/Neuanordnung erstellen, wenn die Braintree-Zahlung aktiviert ist](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Veröffentlichungsdatum: 24. Mai 2022

Feste Einschränkungen für Sicherheits-Patches im `patches.json` -Datei.

## v1.0.16

Veröffentlichungsdatum: 31. März 2022

Kritischer Patch für Adobe Commerce 2.3.3-p1 und neuere Versionen:

Aktualisierte Patches zum Beheben eines **kritisch** Schwachstelle, die zu einer nicht authentifizierten Ausführung von Remote-Code führt.<!-- MCLOUD-8479 -->

Siehe [Adobe-Sicherheitsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Veröffentlichungsdatum: 10. März 2022

- **Unterstützung von PHP 8.1**—Unterstützung für PHP 8.1 hinzugefügt und Unterstützung für PHP 7.0 und 7.1 eingestellt.
- **Patch für Adobe Commerce 2.3.3 hinzugefügt**—Die auf der Produktseite angezeigte feste Währung.

## v1.0.14

Veröffentlichungsdatum: 13. Februar 2022

Kritischer Patch für Adobe Commerce 2.3.3-p1 und neuere Versionen:

Es wurde ein Patch hinzugefügt, um einen **kritisch** Schwachstelle, die zu einer nicht authentifizierten Ausführung von Remote-Code führt.<!-- MCLOUD-8461 -->

Siehe [Adobe-Sicherheitsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Veröffentlichungsdatum: 25. Oktober 2021

- **Monolog aktualisieren**—Die für die `monolog` Paket zu `^2.3`.<!-- ACMP-1263 -->
- **Inkompatible PHP-Methode**—Die inkompatible PHP-Methode für die Adobe Commerce-Versionen 2.4.3 und 2.3.7-p1 wurde behoben.<!-- AC-384 -->
- **PHP-Fehler**—Korrektur einer `PHP error 'Undefined variable: errorMessage' ...` Fehler, der beim Versuch auftrat, einen Patch anzuwenden.<!-- ACP2E-138 -->

## v1.0.12

Veröffentlichungsdatum: 12. August 2021

Kritisches Patch für Adobe Commerce 2.4.3 und 2.3.7-p1:

- **Problem mit API-Ratenbegrenzung**—Dieser Patch korrigiert ein standardmäßiges Ratenlimit, das verhindert, dass Web-APIs Anforderungen mit mehr als 20 Elementen in einem Array verarbeiten. Dieser Patch erhöht den Standardwert des Ratenlimits. Siehe Adobe Commerce [2.4.3 - Versionshinweise](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) und [2.3.7 - Versionshinweise](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Veröffentlichungsdatum: 29. Juli 2021

- **Es wurde ein Problem behoben, das durch das Anwenden des Navigations-Patches für die B2B-Ebene verursacht wurde**—Für Kunden, die den Navigations-Patch für die B2B-Ebene angewendet haben, löst diese Korrektur einen `Undefined offset` auf der Suchseite nach dem Wechsel zur Store-Ansicht angezeigt.<!--MCLOUD-5287-->

- **Paypal Checkout-Patch**—Behebung eines Problems mit Adobe Commerce 2.3.7 mit PayPal Express, bei dem der zuvor platzierte Bestellpreis angezeigt wurde.<!--MC-42674-->

- **Patch-Kategorieunterstützung**—Zusätzliche Unterstützung für die Verarbeitung von Patch-Kategorien und Herkunftsquellen, die Qualitätspatches zugewiesen sind. Mit den Kategorien können Kunden Filter und Sortierung verwenden, um bei Verwendung der [Werkzeug für Qualitätsmuster](https://github.com/magento/quality-patches) und dem Site-weiten Analyse-Tool (SWAT). <!--MC-38577-->

## v1.0.10

Veröffentlichungsdatum: 10. Mai 2021

- **Kompatibilität mit Adobe Commerce 2.3.7**—Behobene Komponentenabhängigkeitskonflikte bei der Installation auf Adobe Commerce 2.3.7.<!--MC-42131-->
- **Es wurde ein Problem behoben, das durch mehrmals Anwendung eines gebündelten Patches verursacht wurde**—Wenn Sie einen gebündelten Patch (einen Patch, der andere veraltete Patches enthält) mehr als einmal anwenden, können die eingeschlossenen veralteten Pakete zurückgesetzt werden. Alle Patches werden jetzt nur einmal angewendet. Wenn Sie versuchen, dasselbe Paket erneut anzuwenden, wird eine Meldung angezeigt, dass der Patch bereits angewendet wurde.<!--MC-41912-->
- **B2B Layoutnavigations-Patch**—Ein weiteres Problem wurde behoben, das verhindert hatte, dass in der Navigation mit Ebenen alle Produktoptionen angezeigt wurden, wenn der Benutzer den freigegebenen B2B-Katalog aktiviert hat.<!--MCLOUD-7742-->

## v1.0.9

Veröffentlichungsdatum: 1. Februar 2021

- **B2B Layoutnavigations-Patch**—Korrektur des Fehlers, der verhindert hat, dass in der Navigation mit Ebenen alle Produktoptionen angezeigt wurden, wenn der freigegebene B2B-Katalog aktiviert war.<!--MCLOUD-6923-->
- **Kompatibilität mit PHP 7.4**—Es wurde ein Kompatibilitätsproblem mit Cloud-Patches mit PHP 7.4 behoben.<!--MCLOUD-7367-->
- **Veraltete Patches werden sichtbar**—Es wurde ein Cloud-Patches-Problem behoben, bei dem veraltete Patches nach dem Anwenden eines Ersetzen-Patches, der den gesamten Inhalt des veralteten Patches enthält, in der Patchtabelle sichtbar wurden. Dies könnte passieren, wenn Sie einen Patch angewendet haben, der mehrere andere Patches kombiniert.<!--MC-40626-->
- **Stilles Versagen beim Anwenden von Patches**—Es wurde ein Cloud-Patch-Problem behoben, bei dem das `git apply` -Befehl hat in einigen Umgebungen still keine Patches angewendet.<!--MC-40529-->

## v1.0.8

Veröffentlichungsdatum: 14. Oktober 2020

- **Kompatibilitätsaktualisierungen für Magento/magento-cloud-patches**—Die `symfony` und `semver` Versionsbegrenzungen in `composer.json` -Datei für die Kompatibilität mit Adobe Commerce 2.4.1 und höheren Versionen.<!--MCLOUD-7111-->

## v1.0.7

Veröffentlichungsdatum: 14. Oktober 2020

- **Reditiert Patches für Adobe Commerce 2.3.0 auf 2.3.5, 2.4.0**—Aktualisierung der Redis-Patches, um beim Implementieren eines Level 2-Caches das Hinzufügen von Produkten zu einer Kategorie zu unterstützen. <!--MCLOUD-6659-->

- **Braintree VBE-Patch**—Behebung eines Fehlers, der zu einem Fehler führte, wenn ein Administrator versuchte, einen Braintree-Abrechnungsbericht anzuzeigen. <!--MCLOUD-6684-->

- Nun, die `ece-patches apply` -Befehl verwendet Unix `patch` -Befehl zum Anwenden von Patches, wenn Git nicht auf dem Host-System verfügbar ist. <!--MCLOUD-7069-->

## v1.0.6

Veröffentlichungsdatum:

- **Redis-Patches für Adobe Commerce 2.3.0 - 2.3.4**—Kommunikation optimieren und Leistung verbessern
   - Reduzierung der Netzwerkübertragungen zwischen Redis und Adobe Commerce
   - Beheben von Race-Bedingungen bei Lade- und Schreibvorgängen für Redis
   - Neuschreiben des Basis-Cache-Adapters zur Fehlerbehebung beim Speichern
   - Verringern Sie den CPU-Verbrauch von Redis<!--MCLOUD-6139-->

- **Redis-Patches für Adobe Commerce 2.3.0 - 2.3.5**—Verbessern der Leistung und Fehlerbehebung
   - Beheben Sie die Implementierung der Cache-Sperre, um unendliche Sperren zu verhindern.
   - Verbessern des aktuellen Sperrmechanismus
   - Implementieren signierter Sperren, um die Entsperrung von parallelen Anforderungen zu verhindern
   - Beheben Sie den folgenden Fehler, der beim Schreibvorgang für Redis auftritt: `OOM command not allowed when used memory > maxmemory`
   - Fehlerbehebung für die Verarbeitung von sauberem Cache durch `cat_p` Tag, das während der Produktaktualisierungen ausgeführt wird<!--MCLOUD-6110-->

- Es wurde ein Problem behoben, das einen Fehler beim Anwenden der erforderlichen `amzn/amazon-pay-module` Patch auf Adobe Commerce für Cloud-Infrastrukturprojekte mit Adobe Commerce v2.2.6 oder 2.3.5, die dieses Modul nicht enthalten. Der Patch-Prozess überspringt jetzt die `amzn/amazon-pay-module` Patch, wenn das Modul nicht installiert ist.<!--MCLOUD-6588-->

## v1.0.5

Veröffentlichungsdatum: 26. Juni 2020

- **Leistungsverbesserungen bei Rediv**—Fügt Redis-Optimierungsfunktionen zu den Adobe Commerce-Versionen 2.3.3 und 2.3.4 hinzu. Diese Fehlerbehebungen wurden in der Adobe Commerce-Version 2.3.5 vorgenommen. Siehe [Leistungssteigerungen](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) im _Versionshinweise zu Adobe Commerce 2.3.5_.<!--MCLOUD-5771-->

- **New Relic-Protokollanreicherung**—Fügt die Monolog ProcessorInterface hinzu, die zur Unterstützung von Verbesserungen der New Relic-Protokollierungsfunktionen erforderlich ist, die in Cloud-Komponenten der Commerce-Version 1.0.4 eingeführt wurden. Dieser Patch ist für die Bereitstellung von Adobe Commerce 2.1.x erforderlich. Wenn der Patch nicht angewendet wird, schlägt der Build während der `di:compile` -Prozess.<!--MCLOUD-6029-->

## v1.0.4

Veröffentlichungsdatum: 12. Mai 2020

- **Amazon Pay-out**—Behebung eines Problems mit dem Amazon Pay Payment Widget, das Kunden daran hinderte, die Zahlungsmethode auf der _Überprüfung und Zahlungen_ Schritt während des Checkout-Prozesses.<!--MCLOUD-5930-->

- **Produktanzeige auf Kategorieseite**—Behebung eines Problems, bei dem Produkte nicht auf der Kategorieseite in angezeigt wurden. _Alle Seiten anzeigen_ anzeigen.<!--MCLOUD-5684-->

- **Seiten-Builder-Bild-Upload**—Behebt ein Problem mit der Seitenaufbau-Oberfläche, das manchmal den folgenden Fehler beim Hochladen von Bildern in die Bildergalerie verursachte: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Unterdrücken unnötiger sitemap-Generierungswarnungen**—Fügt einen Wiederholungsversuch bei Fehlern während der Sitemap-Generierung hinzu und überspringt die E-Mail-Benachrichtigung von Kunden, wenn Fehler automatisch wiederhergestellt werden können.<!--MCLOUD-3025-->

- **Verbesserung der Site-Leistung**—Behebt ein Leistungsproblem mit dem `Magento\Framework\App\DeploymentConfig\Reader::load` -Funktion, die regelmäßig lange Ladezeiten erlebt hat, die sich auf die Site-Leistung auswirkten. <!--MCLOUD-5650-->

- Die Patch-Zuweisung für Zahlungsmethode-Patches wurde aktualisiert, um die Zahlungsmodule anstelle des Magento-Basispakets (magento/magento2-base) zu verwenden, sodass die Zahlungspatches nur angewendet werden, wenn die Zahlungsmodule vorhanden sind.<!--MCLOUD-5666-->

- Aktualisierte Patches zur Kompatibilität mit Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Veröffentlichungsdatum: 28. April 2020

- Es wurde eine Fehlerbehebung für den Patch &quot;FPC wird während der Bereitstellung deaktiviert&quot;hinzugefügt, um Adobe Commerce 2.3.5 zu unterstützen.

## v1.0.2

Veröffentlichungsdatum: 27. Februar 2020

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Kompatibilitätsaktualisierungen für Magento/magento-cloud-patches**

   - Die `symfony` und `semver` Versionsbegrenzungen in `composer.json` -Datei für die Kompatibilität mit Adobe Commerce 2.4 und höheren Versionen.<!--MAGECLOUD-5127-->

   - Aktualisierte Einschränkungen in `composer.json` für Kompatibilität mit `ece-tools` Versionen 2002.0.22 und höher 2002.0.x.

- **PayPal Express Checkout**—Dieser Patch wurde am 12. Februar 2020 veröffentlicht und behebt ein Problem bei Bestellungen, die mit PayPal Express Checkout aufgegeben wurden. Dabei gibt die Lieferadresse für die Bestellung eine Länderregion an, die manuell in das Textfeld eingegeben wurde, anstatt über das Dropdown-Menü auf der Versandseite ausgewählt zu werden. Weitere Informationen finden Sie in der vollständigen Patch-Beschreibung auf der Patch-Download-Seite.

- **Fehlerbehebung bei der Anwendungsbereitstellung**—Es wurde ein Patch hinzugefügt, um ein Problem zu beheben, durch das der vollständige Seiten-Cache während des Bereitstellungsprozesses deaktiviert wurde. Dieser Patch gilt für Adobe Commerce 2.3.2 und neuere Versionen.

- **Perimeter-Parameter für die Async/Bulk-API**—Dieser Patch wurde aktualisiert, um einen Syntaxfehler im `composer.json` -Datei. Dieses Pflaster gilt für die Magento Open Sourcen 2.3.1 und 2.3.2. Weitere Informationen finden Sie in der vollständigen Patch-Beschreibung auf der Patch-Download-Seite.

## v1.0.1

Veröffentlichungsdatum: 6. Februar 2020

Wir haben alle Patches der Magento Open Source 2.x von der Software-Downloadseite in der Magento/magento-cloud-patches Version 1.0.1 integriert. Wenn Sie Patches bereits in Ihr Projekt kopiert haben, entfernen Sie sie, um Konflikte zu vermeiden.

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Korrigieren Sie Cron-Deadlocks und verbessern Sie die Cron-Sperre.**—

   - Behebung eines Problems, bei dem einige Cron-Aufträge aufgrund eines falschen Statuswerts im `cron_schedule` Tabelle. Jetzt verwenden wir das Adobe Commerce-Sperrframework, um den Cron-Auftragsstatus zu überprüfen und zu aktualisieren, anstatt die `cron_schedule` Tabelle. Cron-Aufträge, die mit einem Fehlerstatus beendet wurden, werden während der nächsten Cron-Ausführung erneut versucht, anstatt 24 Stunden zu warten.

   - Fügt eine _Wiederholen_ -Vorgang, um Deadlock bei Aktualisierungen der Daten im `cron_schedule` Tabelle.

- **Aktualisiert `magento/magento-cloud-patches` , um alle verfügbaren Patches für Magento Open Source 2.x einzuschließen.**—Das Package magento/magento-cloud-patches wurde aktualisiert und enthält nun alle Magento Open Source 2.x-Patches, die auf der Seite Softwaredownloads verfügbar sind. Wenn Sie zuvor Magento Open Source-Patches in Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur kopiert haben, entfernen Sie sie, um Konflikte zu vermeiden.<!--MAGECLOUD-4606-->

- **Korrektur der Elasticsearch-Katalogpaginierung** —Der in Magento/magento-cloud-patches v1.0 bereitgestellte Patch für die Seitennummerierung des Elasticsearch-Katalogs wurde durch eine wirksamere Korrektur ersetzt.<!--MAGECLOUD-4847-->

- **Page Builder-Patches**—In Cloud Patches für Commerce 1.0.0 haben wir Page Builder-Patches gebündelt, um eine bekannte RCE-Schwachstelle (Remote Code Execution) von Page Builder zu beheben, wobei die erste Korrektur auf Adobe Commerce 2.3.3 basiert. Wir haben diese Patches mit einer stabileren Implementierung aktualisiert, die auf Adobe Commerce 2.3.4 basiert und mehrere Optimierungen zur Behebung des Problems enthält.<!--MAGECLOUD-4884-->

  Wenn Sie über das Package magento/magento-cloud-patches 1.0.0 verfügen, sind Sie dennoch vor den RCE-Schwachstellen des Seitenaufbaus geschützt. Wenn Sie auf 1.0.1 oder höher aktualisieren, haben Sie eine bessere Implementierung derselben Korrektur.

## v1.0.0

Veröffentlichungsdatum: 14. November 2019

Dies ist die erste Version der [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) -Paket, das eine neue Abhängigkeit für die `ece-tools` Paketversion 2002.0.22 oder höher.

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Sicherheits-Patches für Page Builder für die Versionen 2.3.1.x und 2.3.2.x**—Behebung eines Fehlers in der Seitenaufbau-Vorschau, der es nicht authentifizierten Benutzern ermöglicht, auf einige Vorlagenmethoden zuzugreifen, die zum Trigger der Ausführung beliebigen Codes über das Netzwerk (RCE) verwendet werden können, was zu globalen Informationslecks führt. Dieses Problem kann auftreten, wenn nicht unterstützte Versionen von Page Builder mit Adobe Commerce-Versionen 2.3.1 und 2.3.2 verwendet werden.<!--MAGECLOUD-4649-->

- **MSI-Patches**—Behebt Probleme, die bei der Verwendung der standardmäßigen Lagerbestandseinstellungen für die Bestandsverwaltung zu Indizierungsfehlern und Leistungsproblemen führten.<!--MAGECLOUD-4428-->

- **Abwärtskompatibilität neuer E-Mail-Schnittstellen**-behebt ein Abwärtskompatibilitätsproblem, das durch die `Magento\Framework\Mail\EmailMessageInterface` Die PHP-Schnittstelle wurde in Adobe Commerce v2.3.3 eingeführt. Im Rahmen dieses Patches wird die neue `EmailMessageInterface` erbt von der alten `MessageInterface`und die Adobe Commerce-Kernmodule wieder auf Abhängigkeiten `MessageInterface`.<!--MAGECLOUD-4422-->

- **Katalogpaginierung funktioniert nicht auf Elasticsearch 6.x**—Behebung eines kritischen Problems mit der Paginierung von Suchergebnissen, das Kunden betrifft, die Elasticsearch 6.x als Katalogsuchmaschine verwenden.<!--MAGECLOUD-4448-->
