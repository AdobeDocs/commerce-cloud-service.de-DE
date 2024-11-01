---
title: Cloud-Komponenten für Commerce
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud-Komponenten-Pakets an.
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: 196efa316b9998c1980412ad96577d7ce42d4aec
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Cloud-Komponenten für Commerce

Das Paket [Cloud-Komponenten](https://github.com/magento/magento-cloud-components) bietet erweiterte Adobe Commerce-Kernfunktionen für Sites, die in der Cloud-Infrastruktur bereitgestellt werden. Dieses Paket ist eine Abhängigkeit vom ECE-Tools-Paket. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben, das Bestandteil der [Cloud Tools Suite für Commerce](cloud-tools-suite.md) ist.

Das Paket `magento/magento-cloud-components` verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v1.1.0 {#latest}

Veröffentlichungsdatum: 7. Oktober 2024

- ![Fixsymbol](../../assets/fix.svg) **Refaktorierter Code**—Die Unterstützung alter PHP-Versionen 7.4, 7.3, 7.2 und zugehöriger Bibliotheken wurde entfernt.<!-- MCLOUD-9278 - -->
- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte Monolog-Version** - Unterstützung für Monolog 3.6 wurde hinzugefügt.<!-- MCLOUD-12855 - -->

## v1.0.14

Veröffentlichungsdatum: 8. April 2024

- ![neues Symbol](../../assets/new.svg) **PHP**—Es wurde Unterstützung für PHP 8.3 hinzugefügt.

## v1.0.13

Veröffentlichungsdatum: 10. März 2023

- ![neues Symbol](../../assets/new.svg) **Verbesserte Unterstützung für PHP 8.2** - Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen wurden behoben, um Commerce 2.4.6 zu unterstützen.

## v1.0.12

Veröffentlichungsdatum: 13. September 2022

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Fehler bei Aufwärmen** - Es wurde ein Problem behoben, bei dem versucht wurde, [Aufwärmen](../environment/variables-post-deploy.md#warm_up_pages) durchzuführen, wenn die Seitenanzeige im Admin auf [**Nicht sichtbar**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-attributes-product#simple-product-csv-file-structure) festgelegt ist. Dies führte zu `ERROR: Warming up failed: <link to page>` -Fehlern im Bereitstellungsprotokoll.<!-- MCLOUD-9134 -->

## v1.0.11

Veröffentlichungsdatum: 4. August 2022

- ![Fixsymbol](../../assets/fix.svg) **Hinzugefügte Unterstützung für Kompatibilität mit Symfony 5.4** - Korrekturen für die Kompatibilität mit Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Veröffentlichungsdatum: 10. März 2022

- ![new icon](../../assets/new.svg) **support PHP 8.1**—Es wurde Unterstützung für PHP 8.1 hinzugefügt und die Unterstützung für PHP 7.1 wurde eingestellt.

## v1.0.9

Veröffentlichungsdatum: 25. Oktober 2021

- ![Fixsymbol](../../assets/fix.svg) **Monolog aktualisieren**: Die für das `monolog`-Paket erforderliche Mindestversion wurde auf `^2.3` aktualisiert.<!-- ACMP-1263 -->

## v1.0.8

Veröffentlichungsdatum: 29. Juli 2021

- ![Fixsymbol](../../assets/fix.svg) **Nachfolgende Schrägstriche aus automatisch generierten URLs entfernt** - Die nachfolgenden Schrägstriche aus Kategorieseiten-URLs, die beim Aufwärmen des Caches generiert wurden, wurden entfernt.<!--MCLOUD-7192-->

## v1.0.7

Veröffentlichungsdatum: 9. September 2020

- ![neues Symbol](../../assets/new.svg) **Verbesserungen bei der Protokollierung** - Reduzieren Sie die Größe der `cache.log`-Datei, um die Leistung zu verbessern.<!--MCLOUD-6859-->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Typfehlers in den Cache-Konfigurationswerten, der dazu führte, dass der `php bin/magento cache:evict` CLI-Befehl fehlschlug.

## v1.0.6

Releasedatum: 5. August 2020

- ![neues Symbol](../../assets/new.svg) **Verbessern der Redis-Leistung**: Der Befehl `./bin/magento cache:evict` wurde hinzugefügt, um abgelaufene Redis-Schlüssel zu entfernen. Dadurch wird die Redis-Speicherbelegung reduziert, um die Leistung zu verbessern.<!--MCLOUD-6023-->

- ![Fixsymbol](../../assets/fix.svg) Die Unterstützung für *New Relic-Protokolle im Kontext* wurde entfernt, um ein Leistungsproblem zu beheben.<!--MCLOUD-6422-->

## v1.0.5

Veröffentlichungsdatum: 25. Juni 2020

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das in Version 1.0.4 von magento/magento-cloud-components eingeführt wurde und dazu führte, dass der Cache-Löschvorgang während der Bereitstellungsphase fehlschlug und den Bereitstellungsprozess unterbrach.

## v1.0.4

Veröffentlichungsdatum: 25. Juni 2020

- ![neues Symbol](../../assets/new.svg) **Implementierte New Relic-Protokolle im Kontext** - Von Adobe Commerce generierte Anwendungsprotokolle werden jetzt in Traces in New Relic angezeigt, um die Fehlerbehebungsfunktionen zu verbessern.<!--MCLOUD-6029-->

- ![neues Symbol](../../assets/new.svg) **Verbesserte Protokollierung** - Es wurde eine Protokollierung hinzugefügt, um Cache-Invalidierung und vollständige Neuindizierungsereignisse zu verfolgen.<!--MCLOUD-6157-->

## v1.0.3

Veröffentlichungsdatum: 27. Februar 2020

- ![Symbol zur Fehlerbehebung](../../assets/fix.svg) Es wurde ein Kompatibilitätsproblem behoben, um `ece-tools` 2002.0.x-Versionen zu unterstützen, die ältere PHP-Versionen verwenden.

## v1.0.2

Veröffentlichungsdatum: 6. Februar 2020

- ![neues Symbol](../../assets/new.svg) Die Funktionalität der Umgebungsvariablen `WARM_UP_PAGES` wurde erweitert, um das Vorausfüllen des Caches für bestimmte Produktseiten zu unterstützen. Eine detaillierte Funktionsbeschreibung finden Sie im Thema [ Variablen nach der Bereitstellung ](../environment/variables-post-deploy.md#warm_up_pages) .<!--MAGECLOUD-4444-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem eine ungültige Store-URL dazu führt, dass der Hook nach der Bereitstellung fehlschlägt, wenn die `WARM_UP_PAGES` -Funktion zum Ausfüllen des Caches verwendet wird. Dieses Problem trat nur auf, wenn URL-Neuschreibungen deaktiviert waren.<!-- MAGECLOUD-4094 -->

## v1.0.1

Veröffentlichungsdatum: 23. Juli 2019

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das sich auf die Funktionalität von [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) auswirkte und eine standardmäßige Store-URL verwendete. Wenn der Befehl `config:show:default-url` jetzt keine Basis-URL abrufen kann, wird die URL aus der Variablen MAGENTO_CLOUD_ROUTES verwendet.<!-- MAGECLOUD-3866 -->

## v1.0.0

Veröffentlichungsdatum: 12. Juni 2019

Dies ist die erste Version des [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) -Pakets, das eine neue Abhängigkeit für die `ece-tools` -Paketversion 2002.0.20 und höher darstellt.

- ![neues Symbol](../../assets/new.svg) Die Funktion zum Verwenden von Regex-Mustern wurde hinzugefügt, um die Umgebungsvariable **WARM_UP_PAGES** so zu konfigurieren, dass einzelne Seiten, mehrere Domänen und mehrere Seiten zwischengespeichert werden. Siehe [Variablen nach der Bereitstellung ](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
