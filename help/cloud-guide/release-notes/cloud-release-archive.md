---
title: Versionshinweise-Archiv für Eece-Tools
description: Erfahren Sie mehr über archivierte Verbesserungen für Eece-Tools.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Versionshinweise-Archiv für Eece-Tools

>[!NOTE]
>
>Diese Versionshinweise enthalten Informationen und Aktualisierungen für `ece-tools` v2002.0.22 und höher. Siehe [Versionshinweise für Cloud Tools Suite](cloud-tools-suite.md) , um die neuesten Updates für `ece-tools` und anderen Cloud-Packages.

## v2002.0.22

Die `ece-tools` Version 2002.0.22 ändert die Struktur der `ece-tools` Paket zum Entkoppeln der Veröffentlichung von `Adobe Commerce on cloud infrastructure` Patches aus der ECE-Tools-Version. Ab dieser Version werden Patches und wichtige Fehlerbehebungen mithilfe der Variablen [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) -Paket, das eine neue Abhängigkeit für die `ece-tools` Paket. Wir haben diese Änderungen vorgenommen, um die Komplexität bei der Planung von Release-Updates und der Arbeit mit Community-Beiträgen zu reduzieren.

- ![Neues Symbol](../../assets/new.svg) **Änderungen am ECE-Tools-Paket**

   - ![Neues Symbol](../../assets/new.svg) Die Adobe Commerce-Patches wurden aus der `ece-tools` -Paket in ein neues [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) Komponentenpaket.

   - ![Neues Symbol](../../assets/new.svg) Die `composer.json` -Datei für `ece-tools` -Paket, um eine Abhängigkeit für die `magento/magento-cloud-patches` v1.0.0-Paket.

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass `ece-tools` Patchprozess, der beim Anwenden von Patch-Sets zusätzlich zu reinen Sicherheitsversionen beschädigt wird, beginnend mit Version 2.3.2-p2 und höher. Dieses Problem wurde durch das neue Versionierungssystem eingeführt, das für [Sicherheits-Patches](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![Fixsymbol](../../assets/fix.svg) **Patches und wichtige Fehlerbehebungen**-Aktualisieren Sie Ihre Cloud-Umgebungen mit `ece-tools` Version 2002.0.22 verwenden, um die folgenden Patches und kritischen Korrekturen anzuwenden. Diese Patches sind im `magento/magento-cloud-patches` v1.0.0-Paket.

   - ![Fixsymbol](../../assets/fix.svg) **Sicherheits-Patches für Page Builder für die Versionen 2.3.1.x und 2.3.2.x**-Behebung eines Fehlers in der Seitenaufbau-Vorschau, der es nicht authentifizierten Benutzern ermöglicht, auf einige Vorlagenmethoden zuzugreifen, die zum Trigger der Ausführung beliebigen Codes über das Netzwerk (RCE) verwendet werden können, was zu globalen Informationslecks führt. Dieses Problem kann auftreten, wenn nicht unterstützte Versionen von Page Builder mit Adobe Commerce-Versionen 2.3.1 und 2.3.2 verwendet werden.<!--MAGECLOUD-4649-->

   - ![Fixsymbol](../../assets/fix.svg) **MSI-Patches**-Behebt Probleme, die bei der Verwendung von Standardeinstellungen für die Lagerverwaltung zu Indizierungsfehlern und Leistungsproblemen führten.<!--MAGECLOUD-4428-->

   - ![Fixsymbol](../../assets/fix.svg) **Abwärtskompatibilität neuer E-Mail-Schnittstellen**-behebt ein Abwärtskompatibilitätsproblem, das durch die `Magento\Framework\Mail\EmailMessageInterface` Die PHP-Schnittstelle wurde in Adobe Commerce v2.3.3 eingeführt. Im Rahmen dieses Patches wird die neue `EmailMessageInterface` erbt von der alten `MessageInterface`und die Adobe Commerce-Kernmodule wieder auf Abhängigkeiten `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![Fixsymbol](../../assets/fix.svg) **Katalogpaginierung funktioniert nicht auf Elasticsearch 6.x**-Behebung eines kritischen Problems mit der Seitennummerierung von Suchergebnissen, das Kunden betrifft, die Elasticsearch 6.x als Katalogsuchmaschine verwenden.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![Neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - ![Neues Symbol](../../assets/new.svg) **Neue Docker-Bilder**—Unterstützt von Versionen 2.3.3 und höher<!-- MAGECLOUD-3345 -->

      - PHP Version 7.3.<!-- MAGECLOUD-4017 -->

      - Varnish Cache 6.2.0<!-- MAGECLOUD-4017 -->

   - ![Neues Symbol](../../assets/new.svg) Unterstützung für die Anwendung der benutzerdefinierten Hook-Konfiguration hinzugefügt in `.magento.app.yaml` in der Docker-Umgebung. Zuvor unterstützte die Docker-Umgebung nur die standardmäßige Hook-Konfiguration.<!-- MAGECLOUD-3505-->

   - ![Neues Symbol](../../assets/new.svg) Docker-ENV-Dateien werden nicht mehr während des Docker-Builds generiert und die `docker:config:convert` nicht mehr unterstützt. Die entsprechenden Daten werden jetzt im `docker-compose.yml` -Datei.<!-- MAGECLOUD-3816-->

   - ![Neues Symbol](../../assets/new.svg) **Aktualisiertes PHP-Bild**-Node.js wurde zum PHP Docker-Image hinzugefügt, um die Funktionen node, npm und grunt-cli zu unterstützen.<!-- MAGECLOUD-3953 -->

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**-

   - ![Neues Symbol](../../assets/new.svg) Der **LOCK_PROVIDER** deploy -Variable zum Konfigurieren des Sperranbieters, der den Start doppelter Cron-Aufträge und Cron-Gruppen verhindert. Siehe Variablenbeschreibung im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#lock_provider) Thema.<!-- MAGECLOUD-4052 -->

   - ![Neues Symbol](../../assets/new.svg) Der **CONSUMERS_WAIT_FOR_MAX_MESSAGES** Umgebungsvariable zum Konfigurieren, wie Verbraucher bei Verwendung der Variablen `CRON_CONSUMERS_RUNNER` Umgebungsvariable zum Verwalten von Cron-Aufträgen. Siehe Variablenbeschreibung im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#consumers_wait_for_max_messages) Thema.<!-- MAGECLOUD-4071 -->

   - ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Datenbankblockierfehler können jetzt auch dann auftreten, wenn die Variable `consumers_runner` Der Cron-Auftrag startet mehrere Instanzen desselben Verbrauchers auf verschiedenen Knoten. Wenn Sie jetzt die [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) -Variablen in Ihrer Umgebung bereitstellen, wird die `consumers_runner` Der Auftrag verwendet die `single-thread` -Option, um eine Instanz jedes Verbrauchers auf nur einem Knoten zu starten.<!-- MAGECLOUD-3913 -->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das Folgendes verursachte: [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) -Funktion, die eine standardmäßige Store-URL verwendet. Wenn die Variable `config:show:default-url` kann keine Basis-URL abrufen, wird die URL aus der Variablen MAGENTO_CLOUD_ROUTES verwendet.<!-- MAGECLOUD-3866 -->

- ![Neues Symbol](../../assets/new.svg) Die von der `module:refresh` Befehl. Jetzt können Sie eine detaillierte Liste der aktivierten Module im `cloud.log` -Datei.<!-- MAGECLOUD-2514 -->

- ![Neues Symbol](../../assets/new.svg) Verbesserte Validierung der Versionskompatibilität und Warnhinweise für Kompatibilitätsprobleme zwischen der Adobe Commerce-Version und installierten Diensten, z. B. Elasticsearch, [!DNL RabbitMQ], Redis und DB.<!-- MAGECLOUD-3535 -->

- ![Neues Symbol](../../assets/new.svg) Unterstützung für RabitMQ Version 3.8 hinzugefügt.<!-- MAGECLOUD-4674-->

- ![Neues Symbol](../../assets/new.svg) Die interaktiven Validierungen für die Dienstkompatibilität wurden aktualisiert, um die unterstützten Versionen für die neuen Adobe Commerce-Versionen 2.3.3 und 2.2.10 widerzuspiegeln. Siehe [Systemanforderungen](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) im _Installationshandbuch_ für empfohlene Versionen.<!-- MAGECLOUD-4018 -->

- ![Fixsymbol](../../assets/fix.svg) Die Protokollmeldung, die zurückgegeben wird, wenn der Cron-Auftragsverwaltungsprozess in der Bereitstellungsphase versucht, einen bereits abgeschlossenen Cron-Auftrag zu stoppen, wurde verbessert, um zu klären, dass dieses Problem kein Fehler ist. Die Protokollebene wurde geändert von `INFO` nach `DEBUG`.<!-- MAGECLOUD-3653-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das bei der Ausführung des `setup:upgrade` -Befehl, der den Bereitstellungsprozess nicht unterbrochen hat, wenn während der `app:config:import` Aufgabe.<!-- MAGECLOUD-3806 -->

- ![Neues Symbol](../../assets/new.svg) Die standardmäßige Protokollebene für den Datei-Handler wurde in `debug` um die Detailmenge im Protokoll zu reduzieren, das im [!DNL Cloud Console], während Sie weiterhin detaillierte Informationen zum Debugging bereitstellen.<!-- MAGECLOUD-3871 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das bei der Bereitstellung statischer Inhalte während des Builds einen Fehler verursachte. Nach der Installation und `ece-tools` config dump, ein Fehler, wenn kein Gebietsschema für den Administrator im `config.php` -Datei. Jetzt gibt es ein standardmäßiges Gebietsschema für den Admin-Benutzer im `config.php` -Datei.<!-- MAGECLOUD-3957 -->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines `Undefined index error` das auftritt, wenn `magento-cloud` Der CLI-Befehl schlägt in einer Umgebung fehl, die nicht mit einer sicheren URL (https) konfiguriert ist. Das ECE-Tools-Paket verwendet jetzt die Basis-URL (http), wenn die sichere URL nicht verfügbar ist.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![Neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - ![Neues Symbol](../../assets/new.svg) Sie können jetzt Funktionstests mit dem `ece-tools` in der Docker-Umgebung. Siehe [Anwendungstests](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![Neues Symbol](../../assets/new.svg) Unterstützung für die Konfiguration von PHP-Modulen mithilfe der `.magento.app.yaml` -Datei. Alle [In der Variablen `.magento.app.yaml` file](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) in den Docker PHP-Containern verfügbar sein.<!-- MAGECLOUD-3357 -->

   - ![Neues Symbol](../../assets/new.svg) Es stehen neue Befehle zur Verbesserung des Docker-Befehlszeilenerlebnisses zur Verfügung. Siehe [`bin/magento-docker` Abschnitt der Docker-Referenz](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![Neues Symbol](../../assets/new.svg) Es wurde die Möglichkeit hinzugefügt, Mutagen.io zu verwenden, um Dateien während der Entwicklung zwischen dem lokalen Host und Docker zu synchronisieren.<!-- MAGECLOUD-3559 -->

   - ![Fixsymbol](../../assets/fix.svg) Der Standardpfad bei Verwendung der Docker-Umgebung wurde korrigiert. Wenn Sie sich jetzt mit SSH beim Docker-Container anmelden, befinden Sie sich im Projektstamm im `/app` Verzeichnis.<!-- MAGECLOUD-3582 -->

   - ![Fixsymbol](../../assets/fix.svg) Die Sodium-Bibliothek wurde von Version 1.0.11 auf Version 1.0.18 aktualisiert und die Sodium-PHP-Erweiterung aktualisiert.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Adobe Commerce für Cloud-Infrastrukturkunden [Senden eines Adobe Commerce-Support-Tickets](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) , um das libNatrium-Paket in Pro Production- und Staging-Umgebungen vor der Aktualisierung auf Adobe Commerce 2.3.2 zu aktualisieren. Derzeit können Sie keine Starter-Umgebungen auf Adobe Commerce 2.3.2 aktualisieren.

   - ![Fixsymbol](../../assets/fix.svg) Der `analysis-icu` und `analysis-phonetic` Elasticsearch-Plugins für alle Docker-Bilder.<!-- MAGECLOUD-3446 -->

   - ![Fixsymbol](../../assets/fix.svg) Verbesserte Validierungen: Bei Verwendung von Optionen für `docker:build` -Befehl verwenden, müssen Sie bei der Verwendung einer Option einen Wert angeben. Außerdem wurde eine Validierung für die Knotenversion bei Verwendung der `docker:build run` Befehl.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![Neues Symbol](../../assets/new.svg) Unterstützung für Datenbanktabellenpräfixe mit der [Umgebungsvariable DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![Neues Symbol](../../assets/new.svg) Der **FORCE_UPDATE_URLS** -Variablen bereitstellen, um bei der Bereitstellung in Produktions- und Staging-Umgebungen von Pro und Starter die Basis-URLs zu aktualisieren. Siehe Definition im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#force_update_urls) Inhalt.<!-- MAGECLOUD-3602 -->

   - ![Neues Symbol](../../assets/new.svg) Der **TTFB_TESTED_PAGES** Zu konfigurierende Variable nach der Bereitstellung _Time to First Byte_ Seitentests, um die Anwendungsleistung auf Sites zu überprüfen, die in der Cloud-Infrastruktur bereitgestellt werden. Siehe Variablenbeschreibung in [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit Multi-Thread-SCD behoben, das zu zufälligen Fehlern bei der Bereitstellung statischer Inhalte führte. Die Problemumgehung beinhaltet die Festlegung der **SCD_THREADS** zu `1`. Sie können jetzt die Anzahl nach Bedarf erhöhen. Siehe Definitionen im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_threads) und [Build-Variablen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![Fixsymbol](../../assets/fix.svg) Sie können die **WARM_UP_PAGES** Umgebungsvariable zum Zwischenspeichern einzelner Seiten, mehrerer Domänen und mehrerer Seiten. Siehe erweiterte Definition in der [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages) Inhalt.<!-- MAGECLOUD-3258 -->

- ![Fixsymbol](../../assets/fix.svg) Der `pub/static/.htaccess` in die Ausschlussliste. [Fehlerbehebung eingereicht von Björn Kraus von PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der auftrat, wenn alle Validierungsmeldungen als `Critical` wenn mindestens ein Validator für kritische Ebenen einen Fehler zurückgegeben hat.<!-- MAGECLOUD-3178 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das zu einem Bereitstellungsfehler führte, wenn die Basis-URL nicht in der Datenbank vorhanden war.<!-- MAGECLOUD-3075 -->

- ![Neues Symbol](../../assets/new.svg) Es wurde ein neuer **`env:config:show`command** der `ece-tools` -Paket, das Umgebungsdienste, Routen oder Variablen anzeigt. Siehe [Dienste, Routen und Variablen](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Von Vladimir Kerkhoff vorgelegte Funktion](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der beim Versuch, Adobe Commerce 2.2.6 oder früher zu installieren, einen kritischen Fehler verursachte. `ece-tools` nach der Umgestaltung der Shell entwickeln.<!-- MAGECLOUD-3665 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass Installationen von Adobe Commerce 2.1.x und 2.2.x fehlschlugen und eine Warnung angezeigt wurde, dass eine veraltete Version von Carbon verwendet wurde.<!-- MAGECLOUD-3704 -->

- ![Fixsymbol](../../assets/fix.svg) Verringert die `cloud.log` Protokollebene für die Shell-Ausgabe von `info` nach `debug`.<!-- MAGECLOUD-3277 -->

- ![Fixsymbol](../../assets/fix.svg) Der `--remove-definers (-d)` -Option `ece-tools db-dump` -Befehl zum Entfernen von Definitoren aus der Dump-Datei.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, durch das die `env.php` -Datei während einer Bereitstellung zu einem Verlust von benutzerdefinierten Konfigurationen führen. Diese Aktualisierung stellt sicher, dass Adobe Commerce in der Cloud-Infrastruktur die `env.php` -Datei bei jeder Bereitstellung und unter Beibehaltung benutzerdefinierter Konfigurationen.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![Neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - ![Neues Symbol](../../assets/new.svg) Die Docker-Umgebung unterstützt jetzt die Cron-Konfiguration, die in der [crons-Eigenschaft der Datei .magento.app.yaml](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![Neues Symbol](../../assets/new.svg) **Neuer Docker-Container**—Hinzufügung einer [TLS-Terminierungsproxy-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) zur Erleichterung der Varnish-SSL-Beendigung über HTTPS.<!-- MAGECLOUD-2890 -->

   - ![Neues Symbol](../../assets/new.svg) **Neues Docker-Bild**—Es wurde ein Node.js-Bild hinzugefügt, um Gulp und andere Funktionen wie Jasmine JS Unit Testing zu unterstützen.<!-- MAGECLOUD-3345 -->

   - ![Neues Symbol](../../assets/new.svg) **Docker-Build-Modi**—Jetzt können Sie die Docker-Umgebung in starten. [Produktionsmodus oder Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). Der Entwicklermodus unterstützt die aktive Entwicklung mit vollständigen, beschreibbaren Dateisystemberechtigungen.<!-- MAGECLOUD-3152/3511 -->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass die Docker-Bereitstellung mit einer `Name or service not known` Fehler, wenn der Cache für einen Dienst konfiguriert ist, der nicht verfügbar ist. Jetzt können Sie einen Dienst aus der [`.magento/services.yaml` file](https://devdocs.magento.com/cloud/project/services.html). Der Docker-Konfigurationsgenerator aktualisiert den Dienst im `docker/config.php.dist` automatisch.<!-- MAGECLOUD-3369 -->

   - ![Neues Symbol](../../assets/new.svg) Interaktive Validierungen zur Dienstkompatibilität hinzugefügt. Wenn ein angeforderter Dienst jetzt mit der Adobe Commerce-Version oder anderen Diensten inkompatibel ist, wird die _interaktiver Modus_ fordert den Benutzer mit einer Meldung und einer Auswahl auf, fortzufahren. Siehe [Dienstversionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) für Docker verfügbar. Verwenden Sie die `-n` Option zum Überspringen der Interaktivität für CICD-Zwecke.<!-- MAGECLOUD-3251 -->

   - ![Fixsymbol](../../assets/fix.svg) Problem mit der Docker-Komposition behoben `db-dump` -Befehl, der vorhandene Dumps gelöscht hat.<!-- MAGECLOUD-3366 -->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, durch das Redis zugewiesen wurde `session`, `default`, und `page_cache` Cache-Speicher auf dieselbe Datenbank-ID übertragen.<!-- MAGECLOUD-3172 -->

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![Neues Symbol](../../assets/new.svg) Die neue **ELASTICSUITE\_CONFIGURATION** Die Umgebungsvariable behält Ihre benutzerdefinierten Diensteinstellungen zwischen den Implementierungen bei. Siehe Definition im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#elasticsuite_configuration) Inhalt.<!-- MAGECLOUD-3205 -->

   - ![Neues Symbol](../../assets/new.svg) Der **SCD_MAX_EXECUTION_TIMEOUT** Umgebungsvariable, damit Sie die Zeit für den Abschluss der Bereitstellung statischer Inhalte über die `.magento.env.yaml` -Datei. Siehe Definition im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_max_execution_time), die [Build-Variablen](../environment/variables-build.md#scd_max_execution_time)und die [globale Variablen](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![Neues Symbol](../../assets/new.svg) Der **MAGENTO_CLOUD_LOCKS_DIR** Umgebungsvariable zum Konfigurieren des Pfads zum Bereitstellungspunkt für den Sperranbieter in der Cloud-Infrastruktur. Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. Diese Variable wird von Adobe Commerce-Version 2.2.5 und höher unterstützt und automatisch konfiguriert. Siehe Definition unter [Cloud-Variablen](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![Fixsymbol](../../assets/fix.svg) Die **SCD_THREADS** Umgebungsvariable Standardwerte, um den optimalen Wert basierend auf der erkannten CPU-Thread-Anzahl automatisch zu bestimmen. Siehe aktualisierte Definitionen in der [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_threads) und [Build-Variablen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Es wurde ein Problem mit einem Patch für den DB Isolation Mechanism behoben, das beim Aktualisieren auf Adobe Commerce in der Cloud-Infrastruktur-Version 2002.0.16 einen Fehler verursachte.<!-- MAGECLOUD-3383 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Patch hinzugefügt, der _Google-Bilddiagramme_ mit _Grafiken_. Siehe den Artikel DevBlog . [Google Image Charts - veraltete und aktualisierte Version für M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![Fixsymbol](../../assets/fix.svg) Validierung für die [Variable &quot;SEARCH_CONFIGURATION&quot;](../environment/variables-deploy.md#search_configuration). Die Bereitstellung schlägt fehl, wenn die Option &quot;Engine&quot;nicht festgelegt ist und `_merge` ist nicht erforderlich.<!-- MAGECLOUD-3470 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - sensible Daten werden jetzt nicht mehr angezeigt, wenn eine Ausnahme auftritt. Jetzt werden die sensiblen Informationen entsprechend maskiert.<!-- MAGECLOUD-3525 -->

- ![Fixsymbol](../../assets/fix.svg) Die Fehlertoleranzeinstellungen des Magento Open Source-Packages wurden verbessert. Wenn Adobe Commerce keine Daten aus den Redizes lesen kann `slave` -Instanz wird aus den Redis gelesen. `master` -Instanz. Siehe [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>Die `ece-tools` Version 2002.0.17 enthält einen wichtigen Sicherheits-Patch. Siehe [Technische Ressourcen: Magento Open Source Patches](https://magento.com/tech-resources/download#download2288).

- ![Neues Symbol](../../assets/new.svg) **Dienstaktualisierungen**—Unterstützt von den folgenden Adobe Commerce-Versionen: 2.2.8 und höher 2.2.x, 2.3.1 und höher 2.3.x

   - Elasticsearch-Version 6.x wird nun unterstützt.<!-- MAGECLOUD-3196 -->

   - Unterstützung für Redis Version 5.0 hinzugefügt.

- ![Neues Symbol](../../assets/new.svg) **Neue Docker-Bilder**—Die folgenden Dienste wurden zum Docker-Build hinzugefügt:

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![Neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable**—Zuvor gab es einen hartcodierten Timeout für die SCD-Komprimierung. Jetzt können Sie das SCD-Komprimierungs-Timeout mithilfe der **SCD_COMPRESSION_TIMEOUT** Umgebungsvariable. Siehe Definitionen im Abschnitt [Build-Variablen](../environment/variables-build.md#scd_compression_timeout) und [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_compression_timeout) Inhalt.<!-- MAGECLOUD-2870 -->

- ![Fixsymbol](../../assets/fix.svg) Der `--use-rewrites` -Option zum Installationsbefehl, sodass Webserver-Neuschreibungen für generierte Links in der Storefront und Administratorzugriff verwendet werden, um die Sicherheit und das Kundenerlebnis zu verbessern.<!-- MAGECLOUD-3246 -->

- ![Fixsymbol](../../assets/fix.svg) Zeitstempel zum `var/log/install_upgrade.log` -Datei, damit sie die Daten für Installations- und Aktualisierungsereignisse anzeigt.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![Neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - Die in der Docker-Umgebung generierte Standarddienstkonfiguration entspricht nun der Standardkonfiguration in der Cloud-Vorlage.<!-- MAGECLOUD-3025 -->

   - Sie können E-Mails aus Ihrer Docker-Umgebung mit dem `sendmail` -Dienst.<!-- MAGECLOUD-2907 -->

   - Die Möglichkeit wurde hinzugefügt, [Xdebug konfigurieren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) zum Debugging in der Cloud Docker-Umgebung.<!-- MAGECLOUD-2891 -->

   - Es wurde ein Problem mit Webdienstberechtigungen behoben, das beim Generieren der `docker-compose.yml` -Datei.<!-- MAGECLOUD-2883 -->

- ![Neues Symbol](../../assets/new.svg) **Upgrade-Verbesserung**—Es wurde eine Validierung hinzugefügt, um zu bestätigen, dass die `autoload` -Eigenschaft in der `composer.json` enthält die erforderlichen Konfigurationsänderungen vor der Aktualisierung auf Adobe Commerce v2.3. Siehe [Upgrade der Version](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![Neues Symbol](../../assets/new.svg) Der Komprimierungsprozess bei der Bereitstellung statischer Inhalte umfasst jetzt alle - nativ generierten oder angepassten - Assets und tritt während der Build-Phase zu Beginn der [`build:transfer` Abschnitt](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Zuvor trat der Komprimierungsprozess auf, bevor eine benutzerdefinierte Minimierung und Bündelung von statischen Assets angewendet wurde. [Fehlerbehebung von Rafael Garcia Lepper von Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Es wurde ein Fehler bei der Datenbankverbindung behoben, der während der Bereitstellung unmittelbar nach dem Konfigurieren einer zusätzlichen Datenbank- und Dienstbeziehung auftrat. Außerdem wurde ein Problem behoben, das während der Konfiguration von Commerce Reporting für Starter auftrat. Für Starter ist dieses Upgrade ein &quot;Muss vorhanden&quot;für die Verwendung von Commerce-Berichten.<!-- MAGECLOUD-3035 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Validierungsproblem mit der Datenbankkonfiguration behoben, das dazu führte, dass der Bereitstellungsprozess fehlschlug.<!-- MAGECLOUD-3003 -->

- ![Fixsymbol](../../assets/fix.svg) Die Einschränkung wurde mit der entsprechenden Version der `symfony/yaml` Paket, das mit [PHP-Konstanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). Die konstante Analyse funktioniert nicht bei Verwendung einer `symfony/yaml` Paketversion vor 3.2. [Fehlerbehebung von Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![Neues Symbol](../../assets/new.svg) **Prüfung der Umgebungskonfiguration**—Es wurde eine Validierung hinzugefügt, um die PHP-Version zu überprüfen und Benutzer zu warnen, wenn sie nicht die neueste empfohlene Version verwenden.<!--MAGECLOUD-2903-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem bei der Verarbeitung von falsch formatierten JSON-Variablen behoben. Wenn jetzt eine JSON-Variable einen Syntaxfehler verursacht, erscheint eine Warnung in der `cloud.log` -Datei und -Bereitstellung wird weiterhin mit der Standardvariablen verwendet.<!-- MAGECLOUD-2851 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Es wurde ein Verbindungsfehler behoben, der während der Bereitstellung unmittelbar nach der Deaktivierung des Redis-Dienstes auftrat.<!-- MAGECLOUD-2747 -->

- ![Neues Symbol](../../assets/new.svg) **Änderungen protokollieren**—Die [Protokollebene](../environment/log-handlers.md#log-levels) von `Info` nach `Notice` für die folgenden Build- und Bereitstellungs-Prozessereignisse:<!--MAGECLOUD-2925-->

   - Starten und beenden Sie den Prozess zur Abstimmung installierter Module in `composer.json` mit freigegebenen Konfigurationseinstellungen in `app/etc/config.php` file

   - Beginn und Ende des Konfigurationsvalidierungsprozesses

   - Anfang und Ende der `setup:di:compile` Prozess zum Generieren von Klassen

- ![Neues Symbol](../../assets/new.svg) **Neue Umgebungsvariablen**—

   - **[Bereitstellungsvariable RESOURCE_CONFIGURATION](../environment/variables-deploy.md#resource_configuration)**—Verwenden Sie diese Variable, um einen Ressourcennamen einer Datenbankverbindung zuzuordnen.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[Globale Variable X_FRAME_CONFIGURATION](../environment/variables-global.md#x_frame_configuration)**—Verwenden Sie diese Variable, um die `X-Frame-Options` Kopfzeilenkonfiguration zum Rendern einer Adobe Commerce-Seite in einer `<frame>`, `<iframe>`oder `<object>`.<!-- MAGECLOUD-3048 -->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierungen der Umgebungsvariablen**—Die folgenden Umgebungsvariablen wurden geändert:

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**—Es wurde die Möglichkeit hinzugefügt, den Cache für bestimmte Seiten auf allen Domänen vorab zu laden, die für einen Adobe Commerce Store definiert sind. Wenn Ihre Site zuvor mit mehreren Domänen konfiguriert war, konnte der Prozess nach der Bereitstellung den Cache für die angegebenen Seiten auf nicht standardmäßigen Domänen nicht vorab laden und gab den folgenden Fehler im Protokoll nach der Bereitstellung zurück: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**—Die Dokumentation und das Beispiel wurden aktualisiert `.magento.env.yaml` -Datei mit den richtigen Standardwerten für die SCD-Komprimierungsstufe. Siehe Definitionen im Abschnitt [Build-Variablen](../environment/variables-build.md#scd_compression_level) und [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_compression_level) Inhalt.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES**—Diese Umgebungsvariable wird nicht mehr unterstützt. Verwenden Sie die [SCD_MATRIX](../environment/variables-build.md#scd_matrix) um die Designkonfiguration zu steuern.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX**—Korrektur des Validierungsprozesses, um ein Problem zu verhindern, das auftrat, wenn SCD_MATRIX einen Designwert ignorierte, der verschiedene Zeichenfälle enthielt. Siehe Definitionen im Abschnitt [Build-Variablen](../environment/variables-build.md#scd_matrix) und [Bereitstellungsvariablen](../environment/variables-deploy.md#scd_matrix) Inhalt.<!-- MAGECLOUD-2904 -->

   - **ADMIN-Variablen**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Verbesserte Sicherheit bei der Verwaltung von Anmeldeinformationen für den Admin-Benutzer mithilfe von Umgebungsvariablen. Sie können die Umgebungsvariablen ADMIN_EMAIL, ADMIN_USERNAME und ADMIN_PASSWORD nicht mehr verwenden, um Administratorberechtigungen bei Upgrades zu überschreiben. Wenn Sie nicht auf das Admin-Bedienfeld zugreifen können, verwenden Sie die _Kennwort vergessen_ oder `admin:user:create` CLI-Befehl zum Erstellen eines neuen Administratorbenutzers. Siehe [Zugriff auf Ihr Admin-Bedienfeld](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL ist beim Aktualisieren oder Anwenden von Patches nicht mehr erforderlich.

## v2002.0.15

- ![Neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - Jetzt verwendet der Docker-Generator die in der `.magento.app.yaml` und `.magento/services.yaml` Konfigurationsdateien beim [Erstellen einer Docker-Umgebung](https://devdocs.magento.com/cloud/docker/docker-config.html). Sie können mithilfe von Build-Parametern eine andere Dienstversion auswählen.<!-- MAGECLOUD-2888 -->

   - PHP 7.2-Image hinzugefügt - Unterstützung für PHP 7.2 in Cloud Docker hinzugefügt; Aktualisierung der [Launch-Docker-Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) , um `docker:build --php` -Option, um die PHP-Version anzugeben, die mit Ihrer Adobe Commerce-Version kompatibel ist.<!-- MAGECLOUD-2799 -->

   - Hinzufügung von [Cron-Container](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) basiert auf dem PHP-CLI-Image.<!-- MAGECLOUD-2565 -->

   - Die folgenden Dienste wurden zum Docker-Build hinzugefügt:

      - [!DNL RabbitMQ] 3.5 und 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 und 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 und 4.0<!-- MAGECLOUD-2886 -->

- ![Neues Symbol](../../assets/new.svg) **Konfigurieren mit PHP-Konstanten**—Unterstützung für [PHP-Konstanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) im `.magento.env.yaml` Konfigurationsdatei.<!-- MAGECLOUD- 2575 -->

- ![Neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable**—Standardmäßig sind nur die Google Analytics in der Produktionsumgebung aktiviert. Sie können Google Analytics in den Staging- und Integrationsumgebungen aktivieren, indem Sie die  [Umgebungsvariable ENABLE_GOOGLE_ANALYTICS](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, durch das benutzerdefinierte Cron-Konfigurationen aus dem `env.php` -Datei nach einer Neubereitstellung. Jetzt bleiben benutzerdefinierte Cron-Konfigurationen sicher im `env.php` -Datei.<!-- MAGECLOUD-2923 -->

- ![Fixsymbol](../../assets/fix.svg) Inkonsistenzen in den Nachrichten und [Protokollebenen](../environment/log-handlers.md#log-levels) für Build-, Bereitstellungs- und Post-Bereitstellungsphasen. Erhöhte Start- und End-Protokollierungsstufen von **Info** nach **Hinweis** für alle Phasen und Unterphasen. Es wurden gegebenenfalls Start- und Endprotokollmeldungen hinzugefügt.<!-- MAGECLOUD-2919 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Es wurde ein Problem mit Cron-Prozessen behoben, das den Start der Phase nach der Bereitstellung verhinderte, sofern konfiguriert. Wenn Sie jetzt den Hook für die Bereitstellung aktiviert haben, werden die Cron-Prozesse zu Beginn der Phase nach der Bereitstellung erneut aktiviert.<!-- MAGECLOUD-2862 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - jetzt kann Adobe Commerce bei der Angabe einer benutzerdefinierten Datenbankkonfiguration erfolgreich installiert werden. Zuvor verwendete der Installationsprozess die Datenbankkonfiguration aus dem [MAGENTO_CLOUD_RELATIONSHIP-Variable](../environment/variables-cloud.md) auch wenn Sie in der [Umgebungsvariable DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![Fixsymbol](../../assets/fix.svg) Die `config:dump` -Befehl, damit jedes Website-Gebietsschema in die `system` Abschnitt `config.php` -Datei.<!--MAGECLOUD-2740-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das zu _Warmup_ Fehler während der Phase nach der Bereitstellung durch Korrektur der Quell-URL-Referenz.<!--MAGECLOUD-2797-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, durch das Dateien während der `setup:di:compile` -Prozess, der sich auf das Amazon Pay-Modul auswirkte.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![Neues Symbol](../../assets/new.svg) **Überprüfen des richtigen Zustands**—Die `ideal-state` Der Assistent überprüft jetzt die aktuelle Konfiguration bei jeder Bereitstellung und enthält klare Anweisungen zum Aktualisieren der Konfiguration, um eine schnellere Bereitstellung ohne Ausfallzeiten zu erzielen.<!--MAGECLOUD-2372-->

- ![Fixsymbol](../../assets/fix.svg) **PCI-Compliance**—Die Nachrichtenprotokolle für Adobe Commerce in Cloud-Infrastruktur wurden aktualisiert und erfordern jetzt bei der Verbindung mit Drittanbieter-Messaging-Diensten die Transport Layer Security (TLS)-Version 1.2. Wenn Sie einen Nachrichtendienst verwenden, der TLS Version 1.2 nicht unterstützt, müssen Sie Ihren Dienst aktualisieren. Andernfalls wird die folgende Fehlermeldung angezeigt, wenn Ihre Adobe Commerce-Anwendung versucht, eine Verbindung zum Nachrichtenserver herzustellen, um eine E-Mail zu senden: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![Neues Symbol](../../assets/new.svg) **Implementierungsverbesserung**—Es wurde eine Validierung hinzugefügt, die Kunden warnt, wenn eine Staging- oder Produktionsumgebung `dev`, `debug`oder `debug_logging` -Optionen aktiviert sind, um Leistungsprobleme zu verhindern, die durch eine übermäßige Protokollierungsaktivität verursacht werden.<!--MAGECLOUD-2517-->

- ![Fixsymbol](../../assets/fix.svg) **Fehlerbehebungen bei der Bereitstellung**—

   - Der Wartungsmodus ist jetzt zu Beginn der Bereitstellungsphase aktiviert und am Ende deaktiviert. Wenn die Bereitstellung fehlschlägt, bleibt die Site im Wartungsmodus, bis die Bereitstellungsprobleme behoben sind. Zuvor kehrte die Site in den Produktionsmodus zurück, selbst wenn die Bereitstellung fehlschlug.<!--MAGECLOUD-2603-->

      - Die Validierungsprüfungen für die Bereitstellungsphase wurden überarbeitet, um die Fehlerstufe für die folgenden Bereitstellungsprobleme herabzustufen: `CRITICAL` nach `WARNING` , damit die Bereitstellung abgeschlossen ist. Zuvor führten diese Probleme dazu, dass die Bereitstellung fehlschlug.

      - Die Umgebungskonfiguration enthält falsche Werte für Bereitstellungen oder Cloud-Variablen.

   - Die Elasticsearch-Version in der Cloud-Infrastruktur ist nicht mit der von Adobe Commerce in der Cloud-Infrastruktur unterstützten Version des Elasticsearch-/Elasticsearch-Moduls kompatibel. Siehe [Artikel zur Fehlerbehebung bei Elasticsearch](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in der Wissensdatenbank zur Adobe Commerce-Unterstützung.<!--MAGECLOUD-2600-->

   - Es wurde ein Problem mit den freigegebenen Konfigurationseinstellungen im `app/etc/config.php` -Datei `recursion detected` Fehler während der Bereitstellung.<!--MAGECLOUD-2173-->

- ![Fixsymbol](../../assets/fix.svg) **Kronbezogene Fehlerbehebungen**—

   - Fehlerkorrektur - Die Ausführung von Aufträgen ist jetzt möglich, wenn Sie eine andere Cron-Häufigkeit als die Standardfrequenz (1 Minute) angeben.<!--MAGECLOUD-2602-->

   - Fehlerkorrektur - Es wurde ein Problem in der Bereitstellungsphase behoben, durch das die Ausführung von Cron-Aufträgen während der Bereitstellung fortgesetzt werden konnte. Dies kann zu Datenbanksperren und anderen kritischen Problemen führen. Jetzt werden alle Cron-Aufträge beendet, bevor die Bereitstellungsphase beginnt und nach Abschluss der Bereitstellung neu gestartet wird.&lt;!—MAGECLOUD—2537—>

   - Fehlerkorrektur - Der Cron-Auftrags-Workflow in den Versionen 2.2.x wird jetzt nicht mehr so aktiviert, dass gefrorene Cron-Aufträge vor der Implementierung angehalten werden können. Zuvor führte ein eingefrorener Cron-Auftrag dazu, dass die Bereitstellung angehalten wurde.<!--MAGECLOUD-2501-->

- ![Fixsymbol](../../assets/fix.svg) Das Format der `config.php` -Datei, die von der `vendor/bin/ece-tools config:dump` -Befehl zur Verwendung der kurzen Array-Syntax und des 4-Raum-Einzugs, um den Adobe Commerce-Kodierungsstandards zu entsprechen.<!--MAGECLOUD-2527-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Bereitstellungsfehler behoben, der auftrat, wenn die Variable `.magento.env.yaml` contains `{{ base_url }}` und `{{ unsecure_base_url }}` Platzhalter für Webkonfigurationen anstelle der standardmäßigen URL-Konfiguration für ein Adobe Commerce-Projekt in der Cloud-Infrastruktur./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![Neues Symbol](../../assets/new.svg) **Bereitstellung ohne Ausfallzeiten aktivieren**—Adobe Commerce in der Cloud-Infrastruktur stellt jetzt Anforderungen mit erforderlichen Datenbankänderungen während der Bereitstellung in die Warteschlange und wendet die Änderungen an, sobald die Bereitstellung abgeschlossen ist. Anfragen können bis zu 5 Minuten lang aufbewahrt werden, um sicherzustellen, dass keine Sitzungen verloren gehen. Siehe [Bereitstellungsoptionen für statische Inhalte zur Reduzierung der Bereitstellungsunterbrechung in Cloud](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![Neues Symbol](../../assets/new.svg) **Docker Compose für Cloud**—Die folgenden Verbesserungen wurden am [Docker-Setup und -Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) Prozess:

   - Ein Befehl wurde hinzugefügt —`docker:config:convert` um PHP-Konfigurationsdateien in das Docker ENV-Format zu konvertieren, um die Konfiguration der Umgebung zu vereinfachen. Jetzt kopieren Sie die PHP-Konfigurationsdateien in das Docker-Verzeichnis und konvertieren sie in Docker ENV-Dateien. Siehe [Launch-Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Der Installationsprozess von Adobe Commerce on Cloud-Infrastruktur unterstützt jetzt die Bereitstellung sowohl auf schreibgeschützten als auch auf Lese- und Schreibdateisystemen, um das Cloud-Dateisystem genauer zu emulieren. Siehe [Docker konfigurieren](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Unterstützung des Redis-Dienstes**—Es wurde ein Redis-Bild hinzugefügt, das in einem Docker-Container bereitgestellt und automatisch für die Verwendung mit Ihrer Docker-Installation konfiguriert wird.&lt;!—MAGECLOUD—2442—>

   - Jetzt verfügen Sie über die DB-Dump-Funktion bei der Verwendung des Cloud Docker [Datenbankcontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Außerdem können Sie [Freigeben von Dateien](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) zwischen einem Hostcomputer und einem Container, der `docker/mnt` Verzeichnis.<!-- MAGECLOUD-2577 -->

   - **Support für Varkonsole**— Es wurde ein Varnish-Bild hinzugefügt, das automatisch in einem Docker-Container bereitgestellt wird. Nach der Bereitstellung können Sie Varnish anhand der Best Practices von Adobe Commerce manuell konfigurieren. Siehe [Konfigurieren und Verwenden von Varnish](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Sicherer Site-Zugriff: SSL-Unterstützung für den Zugriff auf Ihren Adobe Commerce Store und das Admin-Bedienfeld hinzugefügt.&lt;!—MAGECLOUD—2360—>

- ![Fixsymbol](../../assets/fix.svg) **Verbesserte Unterstützung von Adobe Commerce für Cloud-Infrastrukturerweiterungen**—Herabstufung der Mindestanforderungen an die Version des &quot;guzzlehttp/guzzle&quot;-Pakets in der Adobe Commerce-Cloud-Infrastruktur [Datei &quot;composer.json&quot;](https://devdocs.magento.com/cloud/reference/cloud-composer.html) auf Version 6.2, sodass die Variable `ece-tools` -Paket ist mit mehr Erweiterungen kompatibel.<!--MAGECLOUD-2205-->

- ![Neues Symbol](../../assets/new.svg) **Anwenden benutzerdefinierter Änderungen auf Ihre Adobe Commerce-Anwendung während der Build-Phase**—Wir teilen die Build-Phase in zwei separate Prozesse auf, damit Sie mithilfe von Erweiterungspunkten benutzerdefinierte Änderungen an den generierten statischen Inhalten vornehmen können, bevor Sie die Anwendung für die Implementierung verpacken. Die _build:generate_ -Prozess generiert Code, wendet Patches an und generiert statische Inhalte. Die _build:transfer_ -Prozess überträgt den generierten Code und statischen Inhalt an das endgültige Ziel. Siehe [Anwendungshooks](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![Fixsymbol](../../assets/fix.svg) **Prüfung der Umgebungskonfiguration**—Verbesserte Validierung der Umgebungskonfiguration, um Kunden vor der Erstellung und Bereitstellung von Adobe Commerce in der Cloud-Infrastruktur vor Versionsinkompatibilitäten und Konfigurationsfehlern zu warnen.

   - Versionsspezifische Validierung hinzugefügt, um nicht unterstützte oder veraltete Umgebungsvariablen und -werte zu identifizieren.<!--MAGECLOUD-2183-->

   - Es wurde eine Elasticsearch-Kompatibilitätsprüfung hinzugefügt, um Benutzer vor Problemen mit der Elasticsearch-Konfiguration zu warnen. Jetzt schlägt die Bereitstellung fehl, wenn die Elasticsearch-Dienstversion auf dem Server mit Adobe Commerce inkompatibel ist. Zuvor war die Bereitstellung auch dann erfolgreich, wenn die Elasticsearch-Version inkompatibel war, was nach der Site-Bereitstellung zu Problemen mit dem Produktkatalog führte.<!--MAGECLOUD-2389-->

     Sie können die Inkompatibilität durch [Senden eines Support-Tickets](https://devdocs.magento.com/cloud/trouble/trouble.html) , um Elasticsearch auf eine kompatible Version zu aktualisieren, oder ändern Sie die Adobe Commerce-Konfiguration, um eine kompatible Version des Elasticsearch-PHP-Clients anzugeben.

      - Aktualisieren Sie für Adobe Commerce-Version 2.1.x auf Version 2.2.2 Elasticsearch auf Version 2.4.

      - Aktualisieren Sie Elasticsearch für Adobe Commerce-Version 2.2.3 und höher auf Version 5.2.

      - Wenn Sie Elasticsearch 1.x oder 2.x haben und nicht aktualisieren möchten, aktualisieren Sie die Adobe Commerce Elasticsearch PHP-Clientversionserfordernis in Composer.json auf `"elasticsearch/elasticsearch": "~2.0"`.

   - Die Validierung von Umgebungsvariablen zur Identifizierung von Konfigurationseinstellungen, die während der Build-, Bereitstellungs- und Post-Bereitstellungsphasen Konflikte verursachen können, wurde verbessert. Beispielsweise wird während des Installations- und Aktualisierungsprozesses eine Warnmeldung angezeigt, wenn die globale Einstellung für die Bereitstellung statischer Inhalte mit den Einstellungen für die Build- oder Bereitstellungsphase in Konflikt gerät.<!--MAGECLOUD-2156-->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierungen der Umgebungsvariablen**—Die folgenden Umgebungsvariablen wurden geändert:

   - **[Globale Variable SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification)**—Der Standardwert wurde geändert in `true` zur Aktivierung der On-Demand-HTML-Inhaltsminimierung, wodurch Ausfallzeiten bei der Bereitstellung in Staging- und Produktionsumgebungen minimiert werden. Diese Konfiguration ist für Bereitstellungen ohne Ausfallzeiten erforderlich.<!--MAGECLOUD-2435-->

   - **[Variable &quot;CLEAN_STATIC_FILES&quot;bereitstellen](../environment/variables-deploy.md#clean_static_files)**—Es wurde die Möglichkeit hinzugefügt, die Verarbeitung sauberer statischer Dateien für statischen Inhalt zu verwalten, der während der Build-Phase basierend auf der Umgebungsvariableneinstellung CLEAN_STATIC_FILES generiert wurde. Zuvor wurden statische Inhaltsdateien, die während der Build-Phase generiert wurden, immer bereinigt.<!--MAGECLOUD-1506-->

- ![Fixsymbol](../../assets/fix.svg) **Protokollierung**—Die folgenden Änderungen wurden vorgenommen, um Protokollmeldungen zu verbessern und die Protokollgröße zu reduzieren:

   - In den Protokolleinträgen zu Implementierungsfehlern ist jetzt die Befehlsausgabe aus den Vorgängen enthalten, die zu Fehlern führen, selbst wenn in Ihrer Umgebungskonfiguration keine Protokollierung auf der Debug-Ebene festgelegt ist. Siehe [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Es wurde eine Protokollierung für Bereitstellungsfehler hinzugefügt, die auftreten, wenn von einigen Erweiterungen benötigte generierte Fabriken nicht korrekt generiert werden können, da das Dateisystem schreibgeschützt ist.<!--MAGECLOUD-2209-->

   - Die Bereitstellungsprotokollgröße wurde reduziert und es wurden Formatierungsprobleme behoben, die durch Setup-Befehle verursacht wurden, die die interaktive Fortschrittsleiste verwenden.<!--MAGECLOUD-2402-->

   - Die unnötige Ausführlichkeit wurde beseitigt und die Prioritätsstufen für einige Protokollanweisungen aktualisiert.<!--MAGECLOUD-2227-->

- ![Fixsymbol](../../assets/fix.svg) **Cron-spezifische Fehlerbehebungen**—

   - Die standardmäßigen Einstellungen für die Cron-Auftragskonfiguration für die Verlaufslebensdauer wurden von 3d (4320 min) auf 1h (60 min) geändert, um Leistungsprobleme und Bereitstellungsfehler zu verhindern, die auftreten können, wenn die Cron-Warteschlange zu schnell gefüllt wird.<!--MAGECLOUD-2427-->

   - Der Cron-Auftragsverwaltungsprozess während der Bereitstellungsphase wurde verbessert, um Datenbanksperren und andere kritische Probleme zu verhindern. Jetzt werden alle Cron-Aufträge während der Bereitstellungsphase beendet und nach Abschluss der Bereitstellung neu gestartet.<!--MAGECLOUD-2445-->

   - Fehlerkorrektur - Es wurde ein Problem mit dem Sperrmechanismus für die Planung von Verbrauchern behoben, die von Cron-Aufträgen in Adobe Commerce-Versionen 2.2.0 und höher gestartet wurden, um zu verhindern, dass Cron-Aufträge doppelte Verbraucher starten.<!--MAGECLOUD-2464-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit der [Prozess der statischen Inhaltskomprimierung](../environment/variables-intro.md) (`gzip`), die `not overwritten` und `no such file or directory` Fehler beim Referenzieren der komprimierten Datei während des Bereitstellungsprozesses.<!-- MAGECLOUD-2182-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, durch das die `php ./vendor/bin/ece-tools config:dump` -Befehl zum Entfernen redundanter Abschnitte aus dem `config.php` -Datei während des Dump-Prozesses, wenn das Speichergebietsschema nicht angegeben ist. Jetzt können Sie Ihre Konfigurationsdateien einfach zwischen Umgebungen verschieben. Nach der Aktualisierung auf `ece-tools` v2002.0.13, ältere Version neu generieren `config.php` -Dateien mit verbesserter `config:dump` Befehl. Siehe [Konfigurationsverwaltung für Speichereinstellungen](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das während der Bereitstellungsphase einen Fehler verursachte, wenn die Routenkonfiguration in der `.magento/routes.yaml` Dateiumleitungen aus einer [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) einer Domäne `www` Domäne.<!--MAGECLOUD-2556-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit der `_merge` -Option für [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) -Variable, die falsche Zusammenführungsergebnisse verursacht hat, wenn Sie die Variable `engine` -Parameter in der aktualisierten `.magento.env.yaml` Konfigurationsdatei. Jetzt überschreibt der Zusammenführungsvorgang korrekt nur die Werte, die Sie in der aktualisierten `.magento.env.yaml` ohne dass Sie die `engine` -Parameter.<!--MAGECLOUD-2520-->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Die Sitzungssperrung für Adobe Commerce in Cloud-Infrastrukturversionen 2.2.1 und höher wird jetzt nicht mehr fälschlicherweise aktiviert. Dies kann zu Leistungseinbußen und Zeitüberschreitungen führen. Jetzt ist die Sitzungssperrung standardmäßig deaktiviert. Das Problem wurde durch eine Änderung des Standardverhaltens der `disable_locking` -Parameter, der in Version 1.3.4 des Redis-Sitzungs-Handler-Pakets eingeführt wurde. Siehe [colinmollenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![Neues Symbol](../../assets/new.svg) **Docker Compose für Cloud**—Hinzufügung eines Befehls—`docker:build`—um eine [Docker Compose](https://devdocs.magento.com/cloud/docker/docker-config.html) Konfiguration aus der Cloud `ece-tools` Repository.<!-- MAGECLOUD-2250 -->

- ![Neues Symbol](../../assets/new.svg) **Gebietsschemata ändern**—Jetzt können Sie das Gebietsschema des Stores ändern, ohne den Konfigurationsprozess exportieren und importieren zu müssen. Während sich die Anwendung in der Produktion befindet und SCD_ON_DEMAND aktiviert ist, sind die Gebietsschemaoptionen &quot;Store&quot;und &quot;Admin&quot;verfügbar.<!-- MAGECLOUD-2019 -->

- ![Neues Symbol](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Sitemap und Roboter**—Erstellen Sie eine [Workflow](../store/robots-sitemap.md) , um `robots.txt` und generieren Sie eine `sitemap.xml` -Datei für eine einzelne Domain-Konfiguration erstellen, ohne dass die Infrastruktur geändert werden muss.

- ![Neues Symbol](../../assets/new.svg) **Assistenten**—Zwei hinzugefügt [Assistenten](../deploy/smart-wizards.md) um Sie bei der Cloud-Konfiguration zu unterstützen:<!-- MAGECLOUD-1910 -->

   - `ideal-state`—Konfigurieren Sie den idealen Status für minimale Bereitstellungsausfälle.

   - `master-slave`—Konfigurieren des Lastenausgleichs für Datenbank und Versionen

- ![Neues Symbol](../../assets/new.svg) **Modulaktualisierung**—Cloud-Befehl hinzugefügt —`module:refresh`—um Module zu aktivieren, die deaktiviert wurden oder nicht explizit aktiviert wurden, ähnlich wie bei einem Build automatisch.<!-- MAGECLOUD-1521 -->

- ![Neues Symbol](../../assets/new.svg) Die Möglichkeit zum Zusammenführen oder Überschreiben der Konfiguration für Dienste mit der `_merge` -Option in [CACHE](../environment/variables-deploy.md#cache_configuration), [SITZ](../environment/variables-deploy.md#session_configuration), [QUEUE](../environment/variables-deploy.md#queue_configuration), und [SUCHEN](../environment/variables-deploy.md#search_configuration) -Konfigurationen.<!-- MAGECLOUD-2105 -->

- ![Neues Symbol](../../assets/new.svg) **Beispieldatei für die Umgebungskonfiguration**—Wir haben eine `.magento.env.yaml` Beispieldatei zum ECE-Tools-Paket mit einer detaillierten Beschreibung und möglichen Werten für jede Umgebungsvariable.<!-- MAGECLOUD-1908 -->

   - Wir haben außerdem eine tiefe Validierung für die `.magento.env.yaml` Konfiguration, die Fehler im Bereitstellungsprozess verhindert, die durch unerwartete Werte verursacht werden. Wenn ein Fehler auftritt, erhalten Sie jetzt eine detaillierte Fehlermeldung, die mit Folgendem beginnt: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![Neues Symbol](../../assets/new.svg) Folgendes wurde hinzugefügt: [**Umgebungsvariablen**](../environment/variables-intro.md):

   - Jetzt können Sie mehrere Gebietsschemata für jedes Thema mit dem neuen [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) -Umgebungsvariable, die die Anzahl der bereitzustellenden Designdateien verringert.<!-- MAGECLOUD-1501 -->

   - Der [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) Umgebungsvariable, um Ihre Datenbankverbindungen für die Bereitstellung anzupassen.<!-- MAGECLOUD-2047 -->

   - Die neue [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) überschreibt die minimale Protokollierungsstufe für alle Ausgabestreams, ohne Änderungen am Code vorzunehmen.<!-- MAGECLOUD-2129 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der zwischen der Bereitstellungs- und der Postbereitstellungsphase zu Ausfallzeiten führte. Jetzt beginnt die Phase nach der Bereitstellung _sofort_ nach Ende der Bereitstellungsphase.

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem die erfolgreichen Cron-Aufträge, die mit `status = success`aus dem Zeitplan.<!-- MAGECLOUD-2268 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit der `post_deploy` -Erweiterungspunkt, der den Cache in der Bereitstellungsphase statt in der Phase nach der Bereitstellung des Projekts gelöscht hat.<!-- MAGECLOUD-2113 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Bei der Verwendung von SCD mit mehreren Gebietsschemas tritt jetzt kein Fehler mehr auf, der die gleiche `js-translation.json` -Datei für jedes Gebietsschema.<!-- MAGECLOUD-2034 -->

- ![Fixsymbol](../../assets/fix.svg) Optimiert die `db:dump` im `ece-tools` -Paket zu vermeiden, Tabellen zu sperren und die Geschwindigkeit zu erhöhen.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>Die ECE-Tools-Version 2002.0.11 ist für die Kompatibilität mit 2.2.4 erforderlich.

- ![Neues Symbol](../../assets/new.svg) **Konfigurieren schreibgeschützter Verbindungen zu Nicht-Master-Knoten**—Diese Version bietet die Möglichkeit, eine schreibgeschützte Verbindung zu einem Nicht-Master-Knoten zu konfigurieren, um schreibgeschützten Traffic zu erhalten (für  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) und <!--MAGECLOUD-143 -->

- ![Neues Symbol](../../assets/new.svg) **Konfigurationsassistent**—Es wurde ein Assistent hinzugefügt, mit dem Sie Ihre Konfiguration für die Bereitstellung statischer Inhalte überprüfen können. Siehe [Smart-Assistenten](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für Symfony Console**—Unterstützung für Symfony Console 4 mit Adobe Commerce 2.3 hinzugefügt.<!-- MAGECLOUD-1966 -->

- ![Fixsymbol](../../assets/fix.svg) **Optimierungen der Cron-Planung**—Verbesserte Warteschlangenverwaltung und verbesserte Protokollierung, um das Debugging von Cron-bezogenen Problemen zu unterstützen.<!-- MAGECLOUD-1607 -->

- ![Fixsymbol](../../assets/fix.svg) Die Freigabevalidierung schlägt bei einem `ADMIN_EMAIL` oder `ADMIN_USERNAME` ist mit einem vorhandenen Administratorkonto identisch.<!-- MAGECLOUD-1221 -->

- ![Fixsymbol](../../assets/fix.svg) SOLR-Unterstützung für 2.2.x-Versionen wurde entfernt. 2.1.x-Versionen behalten die Möglichkeit, SOLR zu aktivieren.<!-- MAGECLOUD-1282 -->

- ![Fixsymbol](../../assets/fix.svg) Die erste Installation der Staging- und Produktionsumgebungen eines PRO-Projekts enthält jetzt verschiedene Indexpräfixe zum Elasticsearch, um mögliche Konflikte bei der Identifizierung von Datensätzen zu vermeiden, die zu den einzelnen Umgebungen gehören.<!-- MAGECLOUD-1489 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Die Build-Phase für die alte Architektur wird jetzt bei der Bereitstellung statischer Inhalte unterbrochen.<!-- MAGECLOUD-2021 -->

- ![Fixsymbol](../../assets/fix.svg) **Cron-spezifische Verbesserungen**—Die Cron-Implementierung wurde überarbeitet:<!-- MAGECLOUD-1607 -->

   - Es wurde ein Fehler behoben, der dazu führte, dass die Cron-Warteschlange schnell gefüllt wurde. Jetzt werden die veralteten Cron-Jobs verlässlicher gelöscht.

   - Die Sequenz von Cron-Aufträgen wurde neu organisiert, sodass alle Aufträge in separaten Threads vor der allgemeinen Gruppe gestartet werden.

   - Verbesserte Protokollierung, um das Debugging von Cron-Problemen zu verbessern.

   - **NOTE**—Diese Version behandelt viele Cron-bezogene Probleme. Wenn Sie derzeit einige Cron-bezogene Patches in _m2-hotfixes_, entfernen Sie sie.

- ![Fixsymbol](../../assets/fix.svg) **SCD-spezifische Verbesserungen**—

   - Sie können die `VERBOSE_COMMANDS` und `SCD_COMPRESSION_LEVEL` Umgebungsvariablen während _build_ und de_ploy-Phasen.<!-- MAGECLOUD-1819 -->

   - Fehlerkorrektur - Die Bereitstellung schlägt jetzt nicht mehr mit einem zufälligen Fehler fehl, wenn ein unerwarteter Wert für die `SCD_COMPRESSION_LEVEL` Umgebungsvariable. Die Konfigurationsvalidierung wurde verbessert, um aussagekräftige Benachrichtigungen bereitzustellen. Siehe [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) für annehmbare Werte.<!-- MAGECLOUD-2043 -->

   - Das Verhalten der `SCD_COMPRESSION_LEVEL` Konfigurationsfluss der Umgebungsvariablen, damit die Außerkraftsetzungen erwartungsgemäß funktionieren.<!-- MAGECLOUD-2044 -->

   - Fehlerkorrektur - Die Konfiguration der `SCD_THREADS` Umgebungsvariable in `.magento.env.yaml` file _deploy_ Bühne.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![Neues Symbol](../../assets/new.svg) **Statische Inhaltsbereitstellung (SCD)**—Es gibt einen neuen, alternativen Bereitstellungsprozess zum Generieren statischer Inhalte bei Bedarf (On-Demand). Dadurch werden Ausfallzeiten reduziert und die Cache-Handhabung verbessert, indem die wichtigsten Assets generiert werden.<!-- MAGECLOUD-1285 -->

   - **Neue Umgebungsvariable**—Die `SCD_ON_DEMAND` globale Umgebungsvariable, um bei Bedarf statischen Inhalt zu generieren.<!-- MAGECLOUD-1738 -->

   - **Hook nach der Bereitstellung**—Hinzufügung einer `post_deploy` Hook für `.magento.app.yaml` Datei, die den Cache löscht und den Cache vorlädt (wärmt). _after_ der Container beginnt, Verbindungen zu akzeptieren. Sie ist nur für Pro-Projekte verfügbar, die Staging- und Produktionsumgebungen in der [!DNL Cloud Console] und für Starter-Projekte. Obwohl dies nicht erforderlich ist, funktioniert dies zusammen mit dem `SCD_ON_DEMAND` Umgebungsvariable.<!-- MAGECLOUD-1788 -->

- ![Neues Symbol](../../assets/new.svg) **Optimierung**—Optimiertes Verschieben oder Kopieren von Dateien während der Bereitstellung, um die Bereitstellungsgeschwindigkeit zu verbessern und die Auslastung des Dateisystems zu verringern.<!-- MAGECLOUD-1842 -->

- ![Neues Symbol](../../assets/new.svg) **Implementierungs-Protokollierung**—Es wurde die Möglichkeit hinzugefügt, während des Bereitstellungsprozesses Syslog- und Graylog Extended Log Format (GELF)-Handler für die Ausgabe von Protokollen zu aktivieren. Siehe [Protokollierungshandler](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![Neues Symbol](../../assets/new.svg) Folgendes wurde hinzugefügt: [**Umgebungsvariablen**](../environment/variables-intro.md):

   - `CRYPT_KEY`—Stellen Sie beim Verschieben einer Datenbank einen kryptografischen Schlüssel für eine andere Umgebung bereit.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Global_ Umgebungsvariable, die das Kopieren der statischen Ansichtsdateien in die `var/view_preprocessed` und generiert bei Bedarf minimierte HTML.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Global_ Umgebungsvariable, um bei Bedarf statischen Inhalt zu generieren.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES`- Sie können die Seiten auflisten, die zum Vorausfüllen des Cache verwendet werden sollen. Verfügbar in der neuen [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md).

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Es wurde ein Problem behoben, bei dem ein lokal angewendeter Patch die Bereitstellung auf einer Instanz beschädigte. Jetzt können ECE-Tools erkennen, dass ein Patch angewendet wurde.<!-- MAGECLOUD-982 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Konflikt zwischen JavaScript-Bundling und GZIP-Funktionalität behoben. Jetzt funktionieren diese Funktionen richtig zusammen.<!-- MAGECLOUD-1735 -->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Jetzt tritt kein Fehler mehr auf, wenn frühere PHP 7.0.x-Versionen verwendet werden, weil die CLI-Befehle der ECE-Tools fehlschlagen.<!-- MAGECLOUD-1744 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das die Bereitstellung statischer Inhalte mit der kompakten Strategie in mehreren Threads verhinderte.<!-- MAGECLOUD-1822 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit der Sitzungssperrung für Redis behoben, das eine Admin-Anmeldungsverzögerung verursachte. Außerdem ist die Fehlerbehebung für 2.1.x verfügbar.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Sie müssen [Aktualisierung des Adobe Commerce-Metapakets zur Cloud-Infrastruktur](../dev-tools/install-package.md#update-the-metapackage) um diese und alle zukünftigen Updates zu erhalten.

- ![Neues Symbol](../../assets/new.svg) **ece-tools**—Die `ece-tools` unterstützt jetzt Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![Neues Symbol](../../assets/new.svg) **Redis-Konfiguration**—Sie können jetzt [Redis konfigurieren](../environment/variables-deploy.md#cache_configuration) Seite und standardmäßiger Cache- und Redis-Sitzungsspeicher mithilfe einer Umgebungsvariablen.<!-- MAGECLOUD-1552 -->

- ![Neues Symbol](../../assets/new.svg) **Verbesserungen beim Such-, AMQP- und Redis-Dienst**—Wir haben den Konfigurationsfluss für den Dienst so vereinheitlicht, dass er nun für alle Dienste auf die gleiche Weise funktioniert. Manuelles Bearbeiten des `env.php` -Datei zum Konfigurieren von Diensten wird nicht mehr unterstützt. Sie müssen Umgebungsvariablen oder die `.magento.env.yaml` -Datei.<!-- MAGECLOUD-1437 -->

- ![Fixsymbol](../../assets/fix.svg) **Umgebungsvariablen**—

   - Die Verwendung von `env:STATIC_CONTENT_THREADS` nicht mehr unterstützt wurde und in einer zukünftigen Version entfernt wird. Verwenden Sie die [SCD_THREADS](../environment/variables-deploy.md#scd_threads) anstatt.<!-- MAGECLOUD-1507 -->

   - Die `STATIC_CONTENT_EXCLUDE_THEMES` -Umgebungsvariable nicht mehr unterstützt. Sie müssen die `SCD_EXCLUDE_THEMES` Umgebungsvariable.<!-- MAGECLOUD-1640 -->

- ![Fixsymbol](../../assets/fix.svg) **Protokollierung**—Wir haben die Protokollierung von integrierten Patchvorgängen vereinfacht.<!-- MAGECLOUD-1674 -->

- ![Fixsymbol](../../assets/fix.svg) Wir entfernt `developer` Unterstützung des Modus und `APPLICATION_MODE` -Umgebungsvariable, da sie unerwartetes Verhalten verursacht haben.<!-- MAGECLOUD-1615 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das zu Fehlern bei der Bereitstellung statischer Inhalte im Zusammenhang mit Redis führte. Jetzt wird die Bereitstellung statischer Inhalte mit mehreren Threads wie geplant ausgeführt.<!-- MAGECLOUD-1630 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das Benutzer daran hinderte, Änderungen an Konfigurationsfeldern in Admin zu speichern, die nach dem Ausführen der `app:config:dump` Befehl.<!-- MAGECLOUD-1175 -->

- ![Fixsymbol](../../assets/fix.svg) Wir haben Unterstützung für eine frühere Version von `symfony/yaml` um Konflikte mit einigen Paketen zu beheben, die noch nicht mit der neuesten Version kompatibel sind.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>Wir fusionierten `vendor/magento/ece-patches` mit `vendor/magento/ece-tools` in dieser Version. Sie müssen die `vendor/magento/ece-patches` Paket getrennt.

**Neue Funktionen:**

- **Verbesserte Protokollierung**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Die Protokollnachrichten wurden verbessert, um bessere Erklärungen zu liefern, wenn der Build- oder Bereitstellungsprozess eine Umgebungsvariable außer Kraft setzt.
   - Sie können nun den Installations- und Aktualisierungsfortschritt in Echtzeit anzeigen. Verfolgen Sie die `install_update.log` -Datei, um den Fortschritt anzuzeigen. Beispiel:

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Neuer Cron-Befehl**—Sie können jetzt bestimmte hängende Cron-Aufträge entsperren, anstatt sie mit dem [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) Befehl. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1367 -->

- **Einheitliche Konfigurationsdatei**—Sie können jetzt Build- und Bereitstellungsschritte mithilfe eines [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) -Datei.<!-- MAGECLOUD-1369 -->

- **Backup-Konfigurationsdateien**—Der Bereitstellungsprozess erstellt jetzt automatisch eine Sicherung der `app/etc/env.php` und `app/etc/config.php` Konfigurationsdateien nach der Bereitstellung. Wir haben auch eine [neue CLI, Befehl](https://support.magento.com/hc/en-us/articles/360033182871) , um diese Konfigurationsdateien aus einem Backup wiederherzustellen.<!-- MAGECLOUD-1372 -->

- **Fehlerbehebung bei Validierungsfehlern**—Wir haben den Befehl geändert, den Sie verwenden müssen, um Validierungsfehler zu beheben, wenn `config.php` enthält nicht genügend Daten für die Bereitstellung statischer Inhalte. Zuvor wurden Sie von der Fehlermeldung angewiesen, `bin/magento app:config:dump`. Jetzt müssen Sie `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Neue Umgebungsvariablen**- Sie können jetzt Umgebungsvariablen verwenden, um eine benutzerdefinierte Verbindung herzustellen. [suchen](../environment/variables-deploy.md#search_configuration) und [AMQP-basiert](../environment/variables-deploy.md#queue_configuration) Dienste zu Ihrer Site hinzufügen.<!-- MAGECLOUD-1410 -->

- Wir haben smartes Patchen implementiert. Jetzt wendet das Paket Patches an, die nicht auf der Cloud-Infrastrukturversion von Adobe Commerce basieren, sondern auf der gepatchten Paketversion.<!--MAGECLOUD-1090-->

**Gelöste Probleme:**

- Es wurde ein Protokollierungsproblem behoben, das Build-Fehler verursachte.<!-- MAGECLOUD-1162 -->

- Es wurde ein Problem behoben, das beim Ausführen von Bereitstellungen im interaktiven Modus Timeout-Ausnahmen verursachte.<!-- MAGECLOUD-1389 -->

- Es wurde ein Problem behoben, das bei der Verwendung der kompakten Strategie für die statische Inhaltserstellung Fehler verursachte. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Es wurde ein Problem behoben, durch das das Bereitstellungsskript die Staging- und Produktionsumgebungen nicht ordnungsgemäß identifizieren konnte.<!-- MAGECLOUD-1493 -->

- Es wurde ein Problem behoben, das dazu führte, dass Netzwerkprobleme Datenbankverbindungen störten und während der Installation und Aktualisierung Fehler verursachten.<!-- MAGECLOUD-1520 -->

- Es wurde ein Fehler behoben, der Sie daran hinderte, die Konfigurationsdateien mit `app:config:dump` mehr als einmal. Nicht verfügbar in 2.1.<!--  MAGECLOUD-1567  -->

- Wir haben eine Redis-Sitzung repariert _sperren_ -Problem verursacht _Admin_ Login Delay. Nicht verfügbar in 2.1.<!--  MAGECLOUD-1582  -->

- Es wurde ein Implementierungsproblem im Zusammenhang mit der Versionierung behoben, das zu einem Konflikt mit anderen Composer-basierten Patchmodulen führte.<!-- MAGECLOUD-1450 -->

- Es wurde ein Problem behoben, das während des Imports Probleme mit dem PHP-Speicher verursachte.<!-- MAGECLOUD-1310 -->

- Patch entfernt; Fehler beheben in `colinmollenhour/credis` v1.6, um die Unterstützung für Adobe Commerce in der Cloud-Infrastruktur 2.2.1 zu aktivieren. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Gelöste Probleme:**

- Wir entfernt `var/view_preprocessed` symlinks zur Behebung eines Problems, das zu JavaScript-Minimierungskonflikten führte.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Gelöste Probleme:**

- Wir haben ein Problem behoben, das `gzip` Fehler, wenn ein Datei- oder Verzeichnisname Leerzeichen enthält.<!-- MAGECLOUD-1413 -->

- Es wurde ein Fehler behoben, der verhinderte, dass Bereitstellungsskripte Modulabhängigkeiten ordnungsgemäß erkennen und aktivieren.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Neue Funktionen:**

- **Konfigurieren eines Cron-Verbrauchers mit einer Umgebungsvariablen**- Sie können jetzt Cron-Verbraucher mithilfe des neuen `CRON_CONSUMERS_RUNNER` Umgebungsvariable.

- **Konfigurationsscan**—Wir suchen jetzt während des Build-/Bereitstellungsprozesses nach kritischen Komponenten und stoppen den Prozess, wenn die Prüfung fehlschlägt, was unnötige Ausfallzeiten aufgrund des Wartungsmodus der Site verhindert.

- **Benachrichtigungen erstellen/bereitstellen**—Wir haben eine Konfigurationsdatei hinzugefügt, die Sie für [Einrichten von Slack- und/oder E-Mail-Benachrichtigungen](../environment/set-up-notifications.md) für Build-/Bereitstellungsaktionen in allen Ihren Umgebungen.

- **Statische Inhaltskomprimierung**—Wir komprimieren jetzt statische Inhalte mit [gzip](https://www.gnu.org/software/gzip/) während der Build- und Bereitstellungsphasen. Diese Komprimierung in Verbindung mit der schnellen Komprimierung trägt dazu bei, die Größe Ihres Stores zu reduzieren und die Bereitstellungsgeschwindigkeit zu erhöhen. Bei Bedarf können Sie die Komprimierung mithilfe einer [Build-Option](../environment/variables-build.md) oder [Bereitstellungsvariable](../environment/variables-deploy.md). Weitere Informationen finden Sie in den folgenden Themen:

   - [Umgebungsvariablen der Anwendung](../application/variables-property.md)

   - [Leistung bei der Bereitstellung statischer Inhalte](../deploy/static-content.md)

   - [Bereitstellungsprozess](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Konfigurationsverwaltung**—Wir generieren jetzt automatisch eine `app/etc/config.php` -Datei in Ihrem Git-Repository während der Build-Phase, falls sie noch nicht vorhanden ist. Die automatisch generierte Datei enthält nur eine Liste von Modulen und Erweiterungen. Wenn die Datei bereits vorhanden ist, wird die Build-Phase normal fortgesetzt. Wenn Sie [Konfigurationsverwaltung](../store/store-settings.md) zu einem späteren Zeitpunkt aktualisieren die Befehle die Datei, ohne dass zusätzliche Schritte erforderlich sind. Siehe Abschnitt [Bereitstellungsprozess](https://devdocs.magento.com/cloud/reference/discover-deploy.html) für weitere Informationen.

- **Datenbank-Dumps**—Wir haben eine `magento/ece-tools` CLI-Befehl zum Erstellen von Datenbank-Dumps in allen Umgebungen. Bei Pro-Plan-Produktionsumgebungen wird dieser Befehl nur von einem von drei Hochverfügbarkeitsknoten abgelegt. Daher können Produktionsdaten, die während des Dump auf einen anderen Knoten geschrieben wurden, nicht kopiert werden. Es wird empfohlen, die Anwendung in den Wartungsmodus zu versetzen, bevor ein Datenbank-Dump in Produktionsumgebungen durchgeführt wird. Siehe [Backup-Management](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) für weitere Informationen.

- **Einschränkungen bei Cron-Intervallen aufgehoben**—Das standardmäßige Cron-Intervall für alle in den Regionen us-3, eu-3 und ap-3 bereitgestellten Umgebungen beträgt 1 Minute. Das standardmäßige Cron-Intervall in allen anderen Regionen beträgt 5 Minuten für Pro Integration-Umgebungen und 1 Minute für Pro Staging- und Produktionsumgebungen. Um Ihre vorhandenen Cron-Aufträge zu ändern, bearbeiten Sie Ihre Einstellungen in `.magento.app.yaml` oder erstellen Sie ein Support-Ticket für Produktions-/Staging-Umgebungen. Siehe Abschnitt [Einrichten von Cron-Aufträgen](../application/crons-property.md#set-up-cron-jobs) für weitere Informationen.

**Gelöste Probleme:**

- Es wurde ein Problem behoben, das aufgrund des Bereitstellungsprozesses, der die `cache-clean` -Vorgang vor der Bereitstellung statischer Inhalte.<!-- MAGECLOUD-1327 -->

- Es wurde ein Problem behoben, das während des Schritts zur Erstellung statischer Inhalte bei der Implementierung in Produktionsumgebungen Fehler verursachte.<!-- MAGECLOUD-1322 -->

- Wir haben ein Problem behoben, das einige `magento/ece-tools` Befehle zur Protokollierungsausgabe in `stderr`.<!-- MAGECLOUD-1264 -->

- Es wurde ein Fehler behoben, der dazu führte, dass Basis-URL-Werte in `env.php` in abgespalteten Zweigen aktualisiert werden.<!-- MAGECLOUD-1242 -->

- Es wurde ein Problem behoben, das die `magento setup:install` -Befehl zum Hinzufügen eines unsicheren Präfixes (`http://`), um Basis-URLs zu sichern.<!-- MAGECLOUD-1171 -->

- Es wurde ein Problem behoben, das verhinderte, dass Patch-Fehler zu Implementierungsfehlern führten.<!-- MAGECLOUD-1170 -->

- Es wurde ein Problem behoben, das `ece-tools` die Ausführung stoppen und eine Ausnahme auslösen, wenn keine Patches angewendet werden können.<!-- MAGECLOUD-1152 -->

- Es wurde ein Problem behoben, das beim Laden der Storefront nach der Aktivierung der HTML-Minimierung in der Admin-Konsole Fehler verursachte.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Gelöste Probleme:**

- Sie können jetzt [Zurücksetzen von Cron-Aufträgen manuell zurücksetzen](https://support.magento.com/hc/en-us/articles/360033099451) Verwendung eines CLI-Befehls in allen Umgebungen über SSH-Zugriff. Der Bereitstellungsprozess setzt Cron-Aufträge automatisch zurück.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Gelöste Probleme:**

- Es wurde ein Problem behoben, das dazu führte, dass Seiten eine Zeitüberschreitung verursachten, da Redis zu lange zum Lesen/Schreiben brauchte. Sie können jetzt die `disable_locking` in Redis-Konfigurationen fest, um dieses Problem zu vermeiden.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Gelöste Probleme:**

- Die [!DNL RabbitMQ] Der Konfigurationsprozess ruft nun alle erforderlichen Parameter automatisch ab.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Neue Funktionen:**

- Adobe Commerce in der Cloud-Infrastruktur unterstützt jetzt Bereiche und [Bereitstellungsstrategien für statische Inhalte](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). Wir haben `–s` -Parameter mit der Standardeinstellung `quick` für die Bereitstellungsstrategie für statische Inhalte. Sie können die Umgebungsvariable verwenden [SCD_STRATEGY](../environment/variables-deploy.md) , um diese Strategien mit Ihren Build- und Bereitstellungsaktionen anzupassen und zu verwenden. Diese Variable unterstützt die Optionen `standard`, `quick`oder `compact`. Wenn Sie `compact`, überschreiben wir die `STATIC_CONTENT_THREADS` Wert mit `1`, was insbesondere in Produktionsumgebungen die Bereitstellung verlangsamen kann. Nicht verfügbar in 2.1.<!--- MAGECLOUD-1057 -->

- Wir haben eine Protokolldatei für Umgebungen erstellt, um Build- und Bereitstellungsaktionen zu erfassen und zu kompilieren. Die `var/log/cloud.log` -Datei im Stammverzeichnis der Anwendung gespeichert.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Gelöste Probleme:**

- Die `ece-tools` -Paket, um die Kompatibilität mit Adobe Commerce auf Cloud-Infrastruktur 2.2.0 und höher herzustellen.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Wir haben ein Problem behoben, das verhinderte, dass `ece-tools` die Ausführung stoppen und eine Ausnahme auslösen, wenn keine Patches angewendet werden können.<!-- MAGECLOUD-1186 -->

- Es wurde ein Problem behoben, bei dem Ausnahmen ausgelöst wurden, wenn die Kompilierung der Abhängigkeitseinfügung (Di) während der Builds übersprungen wurde.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Es wurde ein Problem behoben, durch das der Bereitstellungsprozess benutzerdefinierte Redis-Konfigurationen in der `env.php` -Datei.<!-- MAGECLOUD-1019 -->

- Es wurde ein Problem behoben, das zu Umleitungs-Schleifen führte, da diese standardmäßig durch einen sicheren Administrator deaktiviert waren.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Dieses Paket ist nicht mehr mit anderen Versionen von Adobe Commerce in der Cloud-Infrastruktur kompatibel und **nicht** verwendet werden.

### Erste Version

Erstmalige Veröffentlichung von `ece-tools` für Adobe Commerce auf Cloud-Infrastruktur 2.2.0.
