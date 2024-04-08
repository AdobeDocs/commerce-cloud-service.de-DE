---
title: Cloud-Komponenten für Commerce
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud-Komponenten-Pakets an.
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: c02dfd2709cdc63ac1630edaa8c89cad5f737ea1
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Cloud-Komponenten für Commerce

Die [Cloud-Komponenten](https://github.com/magento/magento-cloud-components) Das -Paket bietet erweiterte Adobe Commerce-Kernfunktionen für Sites, die in der Cloud-Infrastruktur bereitgestellt werden. Dieses Paket ist eine Abhängigkeit vom ECE-Tools-Paket. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben, das eine Komponente von [Cloud Tools Suite für Commerce](cloud-tools-suite.md).

Die `magento/magento-cloud-components` -Paket verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![Neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v1.0.14 {#latest}

Veröffentlichungsdatum: 8. April 2024

- ![Neues Symbol](../../assets/new.svg) **PHP** — Unterstützung für PHP 8.3 hinzugefügt.

## v1.0.13

Veröffentlichungsdatum: 10. März 2023

- ![Neues Symbol](../../assets/new.svg) **Erweiterte Unterstützung für PHP 8.2**—Es wurden Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen behoben, um Commerce 2.4.6 zu unterstützen.

## v1.0.12

Veröffentlichungsdatum: 13. September 2022

- ![Fixsymbol](../../assets/fix.svg) **Fehler bei der Aufwärmung**—Es wurde ein Problem behoben, durch das versucht wurde, [Wärme](../environment/variables-post-deploy.md#warm_up_pages) wenn die Seitenanzeige auf [**Individuell nicht sichtbar**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) im Admin, was zu `ERROR: Warming up failed: <link to page>` Fehler im Bereitstellungsprotokoll.<!-- MCLOUD-9134 -->

## v1.0.11

Veröffentlichungsdatum: 4. August 2022

- ![Fixsymbol](../../assets/fix.svg) **Unterstützung für Symfony 5.4-Kompatibilität hinzugefügt**—Fehlerbehebungen für die Kompatibilität mit Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Veröffentlichungsdatum: 10. März 2022

- ![Neues Symbol](../../assets/new.svg) **Unterstützung von PHP 8.1**—Unterstützung für PHP 8.1 hinzugefügt und Unterstützung für PHP 7.1 eingestellt.

## v1.0.9

Veröffentlichungsdatum: 25. Oktober 2021

- ![Fixsymbol](../../assets/fix.svg) **Monolog aktualisieren**—Die für die `monolog` Paket zu `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Veröffentlichungsdatum: 29. Juli 2021

- ![Fixsymbol](../../assets/fix.svg) **Nachfolgende Schrägstriche aus automatisch generierten URLs wurden entfernt**—Die nachfolgenden Schrägstriche aus Kategorieseiten-URLs, die beim Aufwärmen des Caches generiert wurden, wurden entfernt.<!--MCLOUD-7192-->

## v1.0.7

Veröffentlichungsdatum: 9. September 2020

- ![Neues Symbol](../../assets/new.svg) **Verbesserungen bei der Protokollierung**—Reduzieren Sie die Größe der `cache.log` -Datei, um die Leistung zu verbessern.<!--MCLOUD-6859-->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - In den Cache-Konfigurationswerten tritt kein Typfehler mehr auf, der die `php bin/magento cache:evict` CLI-Befehl schlägt fehl.

## v1.0.6

Releasedatum: 5. August 2020

- ![Neues Symbol](../../assets/new.svg) **Verbessern der Redis-Leistung**—Die `./bin/magento cache:evict` -Befehl zum Entfernen abgelaufener Redis-Schlüssel, wodurch die Redis-Speicherbelegung reduziert wird, um die Leistung zu verbessern.<!--MCLOUD-6023-->

- ![Fixsymbol](../../assets/fix.svg) Die Unterstützung für *New Relic-Protokolle im Kontext* , um ein Leistungsproblem zu beheben.<!--MCLOUD-6422-->

## v1.0.5

Veröffentlichungsdatum: 25. Juni 2020

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das in Version 1.0.4 von magento/magento-cloud-components eingeführt wurde und dazu führte, dass der Flush-Cache-Vorgang während der Bereitstellungsphase fehlschlug und den Bereitstellungsprozess unterbrach.

## v1.0.4

Veröffentlichungsdatum: 25. Juni 2020

- ![Neues Symbol](../../assets/new.svg) **Implementierte New Relic-Protokolle im Kontext**—Von Adobe Commerce generierte Anwendungsprotokolle werden jetzt in Traces in New Relic angezeigt, um die Fehlerbehebungsfunktionen zu verbessern.<!--MCLOUD-6029-->

- ![Neues Symbol](../../assets/new.svg) **Verbesserte Protokollierung**—Protokollierung hinzugefügt, um Cache-Invalidierung und vollständige Neuindizierungsereignisse zu verfolgen.<!--MCLOUD-6157-->

## v1.0.3

Veröffentlichungsdatum: 27. Februar 2020

- ![Fixsymbol](../../assets/fix.svg) Kompatibilitätsproblem behoben, um `ece-tools` 2002.0.x-Versionen, die ältere PHP-Versionen verwenden.

## v1.0.2

Veröffentlichungsdatum: 6. Februar 2020

- ![Neues Symbol](../../assets/new.svg) Erweiterung der Funktionalität der `WARM_UP_PAGES` Umgebungsvariable, um das Vorausfüllen des Caches für bestimmte Produktseiten zu unterstützen. Siehe [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages) Thema für eine detaillierte Funktionsbeschreibung.<!--MAGECLOUD-4444-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem eine ungültige Store-URL dazu führte, dass der Hook nach der Bereitstellung bei Verwendung der `WARM_UP_PAGES` -Funktion, um den Cache zu füllen. Dieses Problem trat nur auf, wenn URL-Neuschreibungen deaktiviert waren.<!-- MAGECLOUD-4094 -->

## v1.0.1

Veröffentlichungsdatum: 23. Juli 2019

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das Folgendes verursachte: [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) -Funktion, die eine standardmäßige Store-URL verwendet. Wenn die Variable `config:show:default-url` kann keine Basis-URL abrufen, wird die URL aus der Variablen MAGENTO_CLOUD_ROUTES verwendet.<!-- MAGECLOUD-3866 -->

## v1.0.0

Veröffentlichungsdatum: 12. Juni 2019

Dies ist die erste Version der [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) -Paket, das eine neue Abhängigkeit für `ece-tools` Paketversion 2002.0.20 und höher.

- ![Neues Symbol](../../assets/new.svg) Die Funktion zur Verwendung von Regex-Mustern zum Konfigurieren der **WARM_UP_PAGES** Umgebungsvariable zum Zwischenspeichern einzelner Seiten, mehrerer Domänen und mehrerer Seiten. Siehe [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
