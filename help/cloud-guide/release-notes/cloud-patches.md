---
title: Cloud-Patches für Commerce
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud Patches-Pakets an.
recommendations: noDisplay, catalog
last-substantial-update: 2024-10-07T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 196efa316b9998c1980412ad96577d7ce42d4aec
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 0%

---

# Cloud-Patches für Commerce

Das Paket [Cloud Patches](https://github.com/magento/magento-cloud-patches) enthält eine Reihe erforderlicher Patches, die die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen verbessern und die schnelle Bereitstellung kritischer Fehlerbehebungen unterstützen.

Das Paket Cloud Patches für Commerce ist eine Abhängigkeit vom Paket ECE-Tools und wird installiert und aktualisiert, wenn Sie das Paket ECE-Tools installieren oder aktualisieren. Sie können Cloud Patches für Commerce auch als eigenständiges Paket verwenden und verwalten, um Patches auf ein Adobe Commerce-Projekt anzuwenden, das sich nicht auf der Cloud-Plattform befindet. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben.

>[!TIP]
>
>Um sicherzustellen, dass Ihr Projekt über alle erforderlichen Patches verfügt, aktualisieren Sie auf die [neueste Version der ece-tools](../dev-tools/update-package.md).

>[!NOTE]
>
>Anweisungen zum Anwenden von Patches auf Ihre Projekte finden Sie unter [Anwenden von Patches](../development/apply-patches.md) .

Das Paket `magento/magento-cloud-patches` verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.1.0 {#latest}

Veröffentlichungsdatum: 7. Oktober 2024

- ![Fixsymbol](../../assets/fix.svg) **Refaktorierter Code**—Die Unterstützung alter PHP-Versionen (7.4, 7.3, 7.2) und verwandter Bibliotheken wurde entfernt.<!-- MCLOUD-9278 - -->
- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte Monolog-Version** - Unterstützung für Monolog 3.6 wurde hinzugefügt.<!-- MCLOUD-12855 - -->
- ![Fixsymbol](../../assets/fix.svg) **Patch for Application Server**: Löst ein bekanntes Problem mit dem GraphQL-Anwendungsserver auf. Genauer gesagt enthielt der `CatalogGraphQl\\Model\\Config\\AttributeReader` in Version 2.4.7 einen Fehler, der dazu führen konnte, dass GraphQL-Anforderungen Antworten basierend auf veralteter Attributkonfiguration abrufen.<!-- ACPT-1876 -->

## v1.0.27

Veröffentlichungsdatum: 21. Mai 2024

- **Unterstützung für PHP 8.3** - Dieser Patch löst Kompatibilitätsfehler zwischen PHP 8.3 und der Composer-Paketversion auf.

## v1.0.26

Veröffentlichungsdatum: 8. April 2024

- ![neues Symbol](../../assets/new.svg) **PHP** — Unterstützung für PHP 8.3 hinzugefügt.

## v1.0.25

Veröffentlichungsdatum: 16. Januar 2024

- **Cache-Verbesserungen** - Dieser Patch verbessert die Effizienz des Layout-Caches und reduziert die Speicherbelegung für Adobe Commerce-Versionen 2.4.4 und höher erheblich.<!-- MCLOUD-11514 -->
- **Verbesserungen bei CRON-Aufträgen** - Dieser Patch behebt das Problem, dass verpasste Aufträge unnötigerweise auf Cron-Auftragssperren für Adobe Commerce-Versionen 2.4.4 und höher warten.<!-- MCLOUD-11329 -->

## v1.0.24

Veröffentlichungsdatum: 15. September 2023

- **Leistungsverbesserung** - Dieser Patch behebt ein Problem, das die Leistung beeinträchtigt, indem die Anzahl der Ladevorgänge derselben Implementierungskonfigurationen für Adobe Commerce 2.4.6 auf 2.4.6-p1<!-- MCLOUD-10604 --> reduziert wird.

## v1.0.23

Veröffentlichungsdatum: 31. Juli 2023

- **Entfernen Sie den Patch MCLOUD-10604** - Dieser Patch wurde in QPT verschoben.<!-- MCLOUD-10736 -->

## v1.0.22

Veröffentlichungsdatum: 19. Juni 2023

- **Verbesserter QPT-CLI-Assistent/-Ausgabe**: Es wurde eine Warnung zum QPT-CLI-Assistenten/-Output hinzugefügt, die Sie daran erinnert, Patch-Details und -Anforderungen zu überprüfen, wenn Abhängigkeiten vorliegen.<!-- ACP2E-1963 -->
- **Patches für Commerce 2.4.6 hinzugefügt:**
   - Korrektur der `regexp cache tag`-Validierung.<!-- MCLOUD-10226 -->
   - Die Leistung wurde verbessert, indem die Anzahl der Ladevorgänge derselben Implementierungskonfigurationen verringert wurde.<!-- MCLOUD-10604 -->
- **Patches für Commerce 2.3.7 zu 2.4.6** hinzugefügt - Es wurde ein Problem behoben, das dazu führte, dass für die `catalog_product_entity_*` -Tabellen eine Inkrementierung um einen zufälligen Wert statt einer Inkrementierung um 1 vorgenommen wurde.<!-- MCLOUD-10032 -->
- **Es wurden Patches für Commerce 2.4.0 zu 2.4.6** hinzugefügt - Es wurde ein Fehler mit `The file can't be deleted. Warning!unlink: No such file or directory` behoben, der beim Löschen des JS-/CSS-Cache vom Admin auftrat.<!-- MCLOUD-10279 -->

## v1.0.21

Veröffentlichungsdatum: 10. März 2023

- **Verbesserte Unterstützung für PHP 8.2** - Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen wurden behoben, um Commerce 2.4.6 zu unterstützen.

## v1.0.20

Veröffentlichungsdatum: 27. Oktober 2022

- **Verbesserter L2-Cache-Patch** - Dieser Patch behebt ein Problem beim Leeren des lokalen L2-Cache für Commerce-Versionen 2.4.0 und 2.4.1.<!-- MCLOUD-7845 -->

## v1.0.19

Veröffentlichungsdatum: 13. September 2022

- **Verbesserte Unterstützung für PHP 8.1** - Kompatibilitätsprobleme mit bestimmten PHP 8.1.x-Versionen wurden behoben.

## v1.0.18

Veröffentlichungsdatum: 11. August 2022

Kritischer Patch für Adobe Commerce 2.4.5:

- **Problem mit Bestellungen, die Braintree-Zahlungen verwenden** - Dieser Patch behebt ein kritisches Problem, das Administratoren daran hindert, neue Bestellungen oder Bestellungen zu tätigen.<!-- MCLOUD-9137 -->

Siehe [Admin kann keine Bestellung/Neuanordnung erstellen, wenn die Braintree-Zahlung aktiviert ist](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Veröffentlichungsdatum: 24. Mai 2022

Es wurden Einschränkungen für Sicherheits-Patches in der Datei `patches.json` behoben.

## v1.0.16

Veröffentlichungsdatum: 31. März 2022

Kritischer Patch für Adobe Commerce 2.3.3-p1 und neuere Versionen:

Es wurden Patches aktualisiert, um eine **kritische** Schwachstelle zu beheben, die zu einer nicht authentifizierten Ausführung von Remote-Code führte.<!-- MCLOUD-8479 -->

Siehe [Adobe-Sicherheitsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Veröffentlichungsdatum: 10. März 2022

- **Unterstützung von PHP 8.1**: Unterstützung für PHP 8.1 hinzugefügt und Unterstützung für PHP 7.0 und 7.1 eingestellt.
- **Patch für Adobe Commerce 2.3.3** hinzugefügt - Die auf der Produktseite angezeigte Währung wurde korrigiert.

## v1.0.14

Veröffentlichungsdatum: 13. Februar 2022

Kritischer Patch für Adobe Commerce 2.3.3-p1 und neuere Versionen:

Es wurde ein Patch hinzugefügt, um eine **kritische** -Schwachstelle zu beheben, die zu einer nicht authentifizierten Ausführung des Remote-Codes führte.<!-- MCLOUD-8461 -->

Siehe [Adobe-Sicherheitsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Veröffentlichungsdatum: 25. Oktober 2021

- **Monolog aktualisieren**: Die für das `monolog`-Paket erforderliche Mindestversion wurde auf `^2.3` aktualisiert.<!-- ACMP-1263 -->
- **Inkompatible PHP-Methode**—Korrektur inkompatibler PHP-Methoden für Adobe Commerce-Versionen 2.4.3 und 2.3.7-p1.<!-- AC-384 -->
- **PHP-Fehler** - Korrektur eines `PHP error 'Undefined variable: errorMessage' ...` Fehlers, der beim Versuch auftrat, einen Patch anzuwenden.<!-- ACP2E-138 -->

## v1.0.12

Veröffentlichungsdatum: 12. August 2021

Kritisches Patch für Adobe Commerce 2.4.3 und 2.3.7-p1:

- **Problem mit API-Ratenbegrenzung** - Dieser Patch behebt ein standardmäßiges Ratenlimit, das verhindert, dass Web-APIs Anforderungen mit mehr als 20 Elementen in einem Array verarbeiten. Dieser Patch erhöht den Standardwert des Ratenlimits. Siehe Adobe Commerce-Versionshinweise [2.4.3 ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/adobe-commerce/2-4-3#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Veröffentlichungsdatum: 29. Juli 2021

- **Korrektur eines Problems, das durch das Anwenden des Navigations-Patches für B2B-Ebenen verursacht wurde** - Für Kunden, die den Navigationspfeil für B2B-Ebenen angewendet haben, löst diese Korrektur einen `Undefined offset` -Fehler auf der Suchseite nach dem Wechseln der Store-Ansicht auf.<!--MCLOUD-5287-->

- **Paypal Checkout Patch** - Behebt ein Adobe Commerce 2.3.7-Problem mit PayPal Express, bei dem der zuvor platzierte Bestellpreis angezeigt wird.<!--MC-42674-->

- **Unterstützung der Patch-Kategorie**: Zusätzliche Unterstützung für die Verarbeitung von Patch-Kategorien und Ursprungsquellen, die Qualitätspatches zugewiesen sind. Mit den Kategorien können Kunden Filter und Sortierung verwenden, um bei der Verwendung des [Qualitäts-Patches-Tools](https://github.com/magento/quality-patches) und des Site-weiten Analyse-Tools (SWAT) schneller nach Patches zu suchen. <!--MC-38577-->

## v1.0.10

Veröffentlichungsdatum: 10. Mai 2021

- **Kompatibilität mit Adobe Commerce 2.3.7**—Behobene Komponentenabhängigkeitskonflikte bei der Installation auf Adobe Commerce 2.3.7.<!--MC-42131-->
- **Korrektur eines Problems, das durch mehrmals Anwendung eines gebündelten Patches** auftrat. Das mehrmalige Anwenden eines gebündelten Patches (eines Patches, der andere veraltete Patches enthält) führte dazu, dass die eingeschlossenen veralteten Pakete zurückgesetzt werden konnten. Alle Patches werden jetzt nur einmal angewendet. Wenn Sie versuchen, dasselbe Paket erneut anzuwenden, wird eine Meldung angezeigt, dass der Patch bereits angewendet wurde.<!--MC-41912-->
- **B2B-Navigations-Patch für Ebenen**: Es wurde ein weiteres Problem behoben, das die Anzeige aller Produktoptionen in der mehrschichtigen Navigation verhinderte, wenn der Benutzer den freigegebenen B2B-Katalog aktiviert.<!--MCLOUD-7742-->

## v1.0.9

Veröffentlichungsdatum: 1. Februar 2021

- **B2B-Navigations-Patch für Ebenen** - Es wurde ein Problem behoben, das die Anzeige aller Produktoptionen in der mehrschichtigen Navigation verhinderte, wenn der freigegebene B2B-Katalog aktiviert war.<!--MCLOUD-6923-->
- **Kompatibilität mit PHP 7.4** - Es wurde ein Kompatibilitätsproblem mit Cloud-Patches mit PHP 7.4 behoben.<!--MCLOUD-7367-->
- **Veraltete Patches werden sichtbar** - Es wurde ein Cloud-Patches-Problem behoben, bei dem veraltete Patches in der Patchtabelle sichtbar wurden, nachdem ein Ersatzpatch angewendet wurde, der den gesamten Inhalt des veralteten Patches enthielt. Dies könnte passieren, wenn Sie einen Patch angewendet haben, der mehrere andere Patches kombiniert hat.<!--MC-40626-->
- **Stillschweigende Fehler beim Anwenden von Patches** - Es wurde ein Cloud-Patches-Problem behoben, bei dem der Befehl `git apply` in einigen Umgebungen still keine Patches angewendet hat.<!--MC-40529-->

## v1.0.8

Veröffentlichungsdatum: 14. Oktober 2020

- **Kompatibilitätsaktualisierungen für Magento/magento-cloud-patches** - Die Versionsbegrenzungen von `symfony` und `semver` in der Datei `composer.json` wurden aktualisiert, um die Kompatibilität mit Adobe Commerce 2.4.1 und höheren Versionen sicherzustellen.<!--MCLOUD-7111-->

## v1.0.7

Veröffentlichungsdatum: 14. Oktober 2020

- **Redis-Patches für Adobe Commerce 2.3.0 auf 2.3.5, 2.4.0** - Redis-Patches wurden aktualisiert, um beim Implementieren eines Level 2-Caches das Hinzufügen von Produkten zu einer Kategorie zu unterstützen. <!--MCLOUD-6659-->

- **Braintree VBE Patch**: Behebung eines Fehlers, der zu einem Fehler führte, wenn ein Administrator versuchte, einen Braintree-Settlement-Bericht anzuzeigen. <!--MCLOUD-6684-->

- Jetzt verwendet der Befehl `ece-patches apply` den Unix `patch`-Befehl, um Patches anzuwenden, wenn Git nicht im Hostsystem verfügbar ist. <!--MCLOUD-7069-->

## v1.0.6

Veröffentlichungsdatum:

- **Redist-Patches für Adobe Commerce 2.3.0 - 2.3.4** - Optimieren Sie die Kommunikation und verbessern Sie die Leistung.
   - Reduzierung der Netzwerkübertragungen zwischen Redis und Adobe Commerce
   - Beheben von Race-Bedingungen bei Lade- und Schreibvorgängen für Redis
   - Neuschreiben des Basis-Cache-Adapters zur Fehlerbehebung beim Speichern
   - Verringern Sie den CPU-Verbrauch von Redis<!--MCLOUD-6139-->

- **Redis patches for Adobe Commerce 2.3.0 - 2.3.5** - Verbessert die Leistung und behebt Fehler
   - Beheben Sie die Implementierung der Cache-Sperre, um unendliche Sperren zu verhindern.
   - Verbessern des aktuellen Sperrmechanismus
   - Implementieren signierter Sperren, um die Entsperrung von parallelen Anforderungen zu verhindern
   - Beheben Sie den folgenden Fehler, der beim Schreibvorgang &quot;Redis&quot;auftritt: `OOM command not allowed when used memory > maxmemory`
   - Fehlerbehebung für die Verarbeitung des sauberen Caches durch das `cat_p`-Tag, das während der Produktaktualisierungen ausgeführt wird<!--MCLOUD-6110-->

- Es wurde ein Fehler behoben, der beim Anwenden des erforderlichen `amzn/amazon-pay-module`-Patches auf Adobe Commerce bei Cloud-Infrastrukturprojekten mit Adobe Commerce v2.2.6 oder 2.3.5, die dieses Modul nicht enthalten, einen Fehler verursachte. Jetzt überspringt der Patch-Prozess den `amzn/amazon-pay-module`-Patch, wenn das Modul nicht installiert ist.<!--MCLOUD-6588-->

## v1.0.5

Veröffentlichungsdatum: 26. Juni 2020

- **Ändert Leistungsverbesserungen**: Fügt Redis-Optimierungsfunktionen zu den Adobe Commerce-Versionen 2.3.3 und 2.3.4 hinzu. Diese Fehlerbehebungen wurden in der Adobe Commerce-Version 2.3.5 vorgenommen.<!--MCLOUD-5771-->

- **New Relic log enricher**: Fügt die Monolog ProcessorInterface hinzu, die zur Unterstützung der in Cloud-Komponenten der Commerce-Version 1.0.4 eingeführten New Relic-Protokollierungsfunktionen erforderlich ist. Dieser Patch ist für die Bereitstellung von Adobe Commerce 2.1.x erforderlich. Wenn der Patch nicht angewendet wird, schlägt der Build während des `di:compile`-Prozesses fehl.<!--MCLOUD-6029-->

## v1.0.4

Veröffentlichungsdatum: 12. Mai 2020

- **Amazon Pay Checkout** - Behebung eines Problems mit dem Amazon Pay Payment Widget, das Kunden daran hinderte, die Zahlungsmethode im Schritt _Überprüfen und Zahlungen_ während des Checkout-Prozesses zu ändern.<!--MCLOUD-5930-->

- **Produktanzeige auf Kategorieseite** - Behebung eines Fehlers, der verhindert hat, dass Produkte auf der Kategorieseite in der Ansicht _Alle Seiten anzeigen_ angezeigt wurden.<!--MCLOUD-5684-->

- **Seiten-Builder-Bild-Upload** - Behebt ein Problem mit der Seitenaufbau-Oberfläche, das manchmal den folgenden Fehler beim Hochladen von Bildern in die Bildergalerie verursachte: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Vermeiden unnötiger Warnungen bei der Sitemap-Generierung** - Fügt einen Wiederholungsversuch hinzu, wenn während der Sitemap-Generierung Fehler auftreten, und überspringt die E-Mail-Benachrichtigung von Kunden, wenn Fehler automatisch abgerufen werden können.<!--MCLOUD-3025-->

- **Verbesserung der Site-Leistung**: Behebt ein Leistungsproblem mit der Funktion `Magento\Framework\App\DeploymentConfig\Reader::load`, die regelmäßig lange Ladezeiten erlebt hat, die die Site-Leistung beeinträchtigten. <!--MCLOUD-5650-->

- Die Patch-Zuweisung für Zahlungsmethode-Patches wurde aktualisiert, um die Zahlungsmodule anstelle des Magento-Basispakets (magento/magento2-base) zu verwenden, sodass die Zahlungspatches nur angewendet werden, wenn die Zahlungsmodule vorhanden sind.<!--MCLOUD-5666-->

- Aktualisierte Patches zur Kompatibilität mit Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Veröffentlichungsdatum: 28. April 2020

- Es wurde eine Fehlerbehebung für den Patch &quot;FPC wird während der Bereitstellung deaktiviert&quot;hinzugefügt, um Adobe Commerce 2.3.5 zu unterstützen.

## v1.0.2

Veröffentlichungsdatum: 27. Februar 2020

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Kompatibilitätsaktualisierungen für Magento/magento-cloud-patches**

   - Die Versionsbegrenzungen `symfony` und `semver` in der Datei `composer.json` wurden aktualisiert, um die Kompatibilität mit Adobe Commerce 2.4 und höheren Versionen sicherzustellen.<!--MAGECLOUD-5127-->

   - Die Einschränkungen in `composer.json` wurden für die Kompatibilität mit `ece-tools` 2002.0.22 und späteren Versionen 2002.0.x aktualisiert.

- **PayPal Express Checkout**: Dieser Patch wurde am 12. Februar 2020 veröffentlicht und behebt ein Problem, das bei PayPal Express Checkout platzierte Bestellungen betrifft, bei dem die Versandadresse für die Bestellung eine Länderregion angibt, die manuell in das Textfeld eingegeben wurde, anstatt über das Dropdown-Menü auf der Versandseite ausgewählt zu werden. Weitere Informationen finden Sie in der vollständigen Patch-Beschreibung auf der Patch-Download-Seite.

- **Fehlerbehebung bei der Anwendungsbereitstellung**: Es wurde ein Patch hinzugefügt, mit dem ein Problem behoben wird, das den vollständigen Seiten-Cache während des Bereitstellungsprozesses deaktiviert hat. Dieser Patch gilt für Adobe Commerce 2.3.2 und neuere Versionen.

- **Perimeter-Parameter für die Async/Bulk-API**: Dieser Patch wurde aktualisiert, um einen Syntaxfehler in der Datei `composer.json` zu beheben. Dieses Pflaster gilt für die Magento Open Sourcen 2.3.1 und 2.3.2. Weitere Informationen finden Sie in der vollständigen Patch-Beschreibung auf der Patch-Download-Seite.

## v1.0.1

Veröffentlichungsdatum: 6. Februar 2020

Wir haben alle Patches der Magento Open Source 2.x von der Software-Downloadseite in der Magento/magento-cloud-patches Version 1.0.1 integriert. Wenn Sie Patches bereits in Ihr Projekt kopiert haben, entfernen Sie sie, um Konflikte zu vermeiden.

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Korrigieren Sie Cron-Deadlocks und verbessern Sie die CRON-Sperre**—

   - Behebung eines Problems, bei dem einige Cron-Aufträge aufgrund eines falschen Statuswerts in der Tabelle `cron_schedule` nicht ausgeführt wurden. Jetzt verwenden wir das Adobe Commerce-Sperrframework, um den Cron-Auftragsstatus zu überprüfen und zu aktualisieren, anstatt die `cron_schedule` -Tabelle zu verwenden. Cron-Aufträge, die mit einem Fehlerstatus beendet wurden, werden während der nächsten Cron-Ausführung erneut versucht, anstatt 24 Stunden zu warten.

   - Fügt einen _Wiederholungsversuch_ -Vorgang hinzu, um zu verhindern, dass bei Aktualisierungen der Daten in der `cron_schedule` -Tabelle ein Deadlock auftritt.

- **`magento/magento-cloud-patches` wurde aktualisiert, um alle verfügbaren Patches für Magento Open Source 2.x einzuschließen.** - Das Package magento/magento-cloud-patches wurde aktualisiert und enthält nun alle Patches der Magento Open Source 2.x, die auf der Seite &quot;Softwaredownloads&quot;verfügbar sind. Wenn Sie bereits früher Magento Open Source-Patches in Ihr Adobe Commerce-Cloud-Infrastrukturprojekt kopiert haben, entfernen Sie sie, um Konflikte zu vermeiden.<!--MAGECLOUD-4606-->

- **Korrektur der Seitennummerierung im Elasticsearch-Katalog** - Ersetzt den Paginierungs-Patch für den Elasticsearch-Katalog, der in Magento/magento-cloud-patches v1.0 bereitgestellt wurde, durch eine wirksamere Korrektur.<!--MAGECLOUD-4847-->

- **Page Builder-Patches** - In Cloud Patches für Commerce 1.0.0 haben wir Page Builder-Patches gebündelt, um eine bekannte RCE-Schwachstelle (Remote Code Execution) von Page Builder zu beheben, wobei die Erstkorrektur auf Adobe Commerce 2.3.3 basiert. Wir haben diese Patches mit einer stabileren Implementierung auf Grundlage von Adobe Commerce 2.3.4 aktualisiert, die mehrere Optimierungen zur Behebung des Problems enthält.<!--MAGECLOUD-4884-->

  Wenn Sie über das Package magento/magento-cloud-patches 1.0.0 verfügen, sind Sie dennoch vor den RCE-Schwachstellen des Seitenaufbaus geschützt. Wenn Sie auf 1.0.1 oder höher aktualisieren, haben Sie eine bessere Implementierung derselben Korrektur.

## v1.0.0

Veröffentlichungsdatum: 14. November 2019

Dies ist die erste Version des [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) -Pakets, das eine neue Abhängigkeit für die `ece-tools` -Paketversion 2002.0.22 oder höher darstellt.

Diese Version umfasst die folgenden Patches und wichtigen Fehlerbehebungen:

- **Page Builder-Sicherheits-Patches für die Versionen 2.3.1.x und 2.3.2.x** - Behebt ein Problem in der Page Builder-Vorschau, das es nicht authentifizierten Benutzern ermöglicht, auf einige Vorlagenmethoden zuzugreifen, die zum Trigger der beliebigen Code-Ausführung über das Netzwerk (RCE) verwendet werden können, was zu globalen Informationslecks führt. Dieses Problem kann auftreten, wenn nicht unterstützte Versionen von Page Builder mit den Adobe Commerce-Versionen 2.3.1 und 2.3.2 verwendet werden.<!--MAGECLOUD-4649-->

- **MSI-Patches** - Behebt Probleme, die bei der Verwendung der standardmäßigen Inventareinstellungen für die Verwaltung von Lagern zu Indizierungsfehlern und Leistungsproblemen geführt haben.<!--MAGECLOUD-4428-->

- **Abwärtskompatibilität der neuen E-Mail-Schnittstellen**-behebt ein Abwärtskompatibilitätsproblem, das durch die in Adobe Commerce v2.3.3 eingeführte `Magento\Framework\Mail\EmailMessageInterface` PHP-Schnittstelle verursacht wurde. Im Rahmen dieses Patches erbt das neue `EmailMessageInterface` die alten `MessageInterface`, und die Kernmodule von Adobe Commerce werden wieder auf `MessageInterface` angewiesen.<!--MAGECLOUD-4422-->

- **Die Katalogpaginierung funktioniert nicht in Elasticsearch 6.x** - behebt ein kritisches Problem mit der Seitennummerierung der Suchergebnisse, das Kunden betrifft, die Elasticsearch 6.x als Katalogsuchmaschine verwenden.<!--MAGECLOUD-4448-->
