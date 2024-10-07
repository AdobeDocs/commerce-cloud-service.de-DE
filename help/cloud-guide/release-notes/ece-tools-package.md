---
title: ECE-Tools - Versionshinweise
description: Siehe eine Liste der neuesten Verbesserungen des ECE-Tools-Pakets.
recommendations: noDisplay, catalog
last-substantial-update: 2024-10-07T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: 30eafa856aaa57bb2fd2ce26e3be2a69aee726e2
workflow-type: tm+mt
source-wordcount: '2990'
ht-degree: 0%

---

# ECE-Tools - Versionshinweise

Das Paket [ece-tools](https://github.com/magento/ece-tools) enthält Skripte und Tools zur Verwaltung und Bereitstellung von Cloud-Projekten. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben, das Teil der [Cloud Tools Suite für Commerce](cloud-tools-suite.md) ist.

>[!NOTE]
>
>Informationen zum Aktualisieren auf die neueste Version des `ece-tools`-Pakets finden Sie unter [ECE-Tools aktualisieren](../dev-tools/update-package.md) .

Das Paket `ece-tools` verwendet die folgende Versionsversionierungssequenz: `200<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v2002.2.0 {#latest}

Veröffentlichungsdatum: 7. Oktober 2024

- ![neues Symbol](../../assets/new.svg) **MariaDB 11.4**-Hinzugefügte Unterstützung von MariaDB 11.4.
- ![Fixsymbol](../../assets/fix.svg) **Umgestalteter Code**-Die Unterstützung alter PHP-Versionen 7.4, 7.3, 7.2 und verwandter Bibliotheken wurde entfernt.<!-- MCLOUD-9278 -->
- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte Monolog-Version** - Unterstützung für Monolog 3.6 wurde hinzugefügt.<!-- MCLOUD-12855 -->
- ![Fixsymbol](../../assets/fix.svg) **Validator für RabbitMQ, MariaDB und PHP**-Korrektur des Validators, der eine irreführende Meldung zur falschen Dienstversion erzeugt hat.

## v2002.1.19

Veröffentlichungsdatum: 21. Mai 2024

- ![neues Symbol](../../assets/new.svg) **Lua**—Die Option useLua für CACHE_CONFIGURATION wurde hinzugefügt.
- ![Fixsymbol](../../assets/fix.svg) **Validator** - Aktualisierte Validatoren für neue Versionen von Redis und RabbitMQ.

## v2002.1.18

Veröffentlichungsdatum: 8. April 2024

- ![neues Symbol](../../assets/new.svg) **PHP** — Unterstützung für PHP 8.3 hinzugefügt.
- ![Fixsymbol](../../assets/fix.svg) **Validator** - Aktualisierter EOL-Validator.

## v2002.1.17

Veröffentlichungsdatum: 16. Januar 2024

- ![Fixsymbol](../../assets/fix.svg) **Validator für Elasticsearch und OpenSearch** - Korrektur des Validators, der eine irreführende Meldung zur Installation eines Suchdienstes erzeugt hat, wenn LiveSearch aktiviert ist.<!-- MCLOUD-10167 -->
- ![Fixsymbol](../../assets/fix.svg) **Bereitstellungswarnung** - Es wurde ein Problem behoben, das zu Bereitstellungswarnungen zu nicht leeren Ordnern führte.<!-- MCLOUD-8958 -->

## v2002.1.16

Veröffentlichungsdatum: 16. Oktober 2023

- ![neues Symbol](../../assets/new.svg) **Globale Umgebungsvariable ENABLE_WEBHOOKS**: Es wurde die globale Variable [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) hinzugefügt, die mit Commerce-Webhooks verwendet werden kann, um eine Verbindung zu einem externen Endpunkt herzustellen, z. B. einer App Builder-Laufzeitaktion oder einem Lagerbestandsverwaltungssystem eines Drittanbieters.

## v2002.1.15

Veröffentlichungsdatum: 31. Juli 2023

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Fehlercodes** - Das Fehlercode-Schema und der Generator für Fehlercodes wurden aktualisiert.
- ![Fixsymbol](../../assets/fix.svg) **Validator für benutzerdefiniertes Redis-Modell** - Der Validator für benutzerdefinierte Redis-Backend-Modelle wurde aktualisiert. [Siehe Beispiel für die Cache-Konfiguration](../environment/variables-deploy.md#cache_configuration).
- ![Fixsymbol](../../assets/fix.svg) **Validator für RabbitMQ** - Unterstützung für RabbitMQ 3.11 hinzugefügt
- ![Fixsymbol](../../assets/fix.svg) **Korrektur des falschen Links**-Korrektur des falschen Links zur Onboarding-Dokumentation in der Begrüßungs-E-Mail-Vorlage.

## v2002.1.14

Veröffentlichungsdatum: 10. März 2023

- ![neues Symbol](../../assets/new.svg) **PHP**—Es wurde Unterstützung für PHP 8.2 hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Validators for Services** - Aktualisierte Validatoren für Commerce 2.4.6 erforderte Dienste: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x und RabbitMQ 3.9.
- ![Fixsymbol](../../assets/fix.svg) **ece-tools db-dump** - Es wurde ein Problem behoben, das dazu führte, dass der `db-dump` -Vorgang vorzeitig angehalten wurde.

## v2002.1.13

Veröffentlichungsdatum: 27. Oktober 2022

- ![neues Symbol](../../assets/new.svg) **Adobe I/O-Ereignisse für Adobe Commerce wurden unterstützt**. Erweiterungsentwickler können jetzt das Framework [Adobe I/O Events](https://developer.adobe.com/events/docs/) verwenden, um Commerce-Ereignisinformationen von Cloud-Instanzen an ihre Anwendungen zu senden, die für [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/) geschrieben wurden. Adobe I/O-Ereignisse für Adobe Commerce befinden sich in der Partnervorschau.<!-- CEXT-932 -->
- ![neues Symbol](../../assets/new.svg) **Validator für die OPcache-Konfiguration**: Es wurde ein Validator hinzugefügt, um die OPcache-Konfiguration auf ausgeschlossene Pfade zu überprüfen.<!-- MCLOUD-9485 -->
- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Es wurde ein Problem mit der GraphQL-Cache-Konfiguration behoben** - Jetzt behält ECE-Tools den GraphQL `id_salt` -Wert in der `cache` -Konfiguration in der `app/etc/env.php`-Datei bei.<!-- MCLOUD-9486 -->

## v2002.1.12

Veröffentlichungsdatum: 13. September 2022

- ![neues Symbol](../../assets/new.svg) **Aktivieren`synchronous_replication`**—ECE-Tools setzt `synchronous_replication=>true` in der Datei `app/etc/env.php`, wenn `MYSQL_USE_SLAVE_CONNECTION` aktiviert ist. Diese Konfiguration betrifft nur Commerce 2.4.6+. Siehe Beschreibung der `MYSQL_USE_SLAVE_CONNECTION`-Variablen in den [Variablen bereitstellen](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![neues Symbol](../../assets/new.svg) **OpenSearch**: Es wurde eine Funktion zum Konfigurieren und Festlegen der `opensearch`-Engine für die nächste Adobe Commerce-Version 2.4.6 hinzugefügt. Siehe [Einrichten des OpenSearch-Dienstes](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.1

Veröffentlichungsdatum: 4. August 2022

- ![Fixsymbol](../../assets/fix.svg) **ElasticSuite Validator and OpenSearch** - Korrektur des Überprüfungsproblems bei der ElasticSuite-Integritätsprüfung bei der Installation von OpenSearch.<!-- MCLOUD-8767 -->
- ![Fixsymbol](../../assets/fix.svg) **Rückgabetypen für Bereitstellungsbefehle** - Rückgabetypen für Bereitstellungsbefehle wurden korrigiert.<!-- AC-3208 -->
- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **[!DNL RabbitMQ]Problem bei der neuen Installation von Commerce 2.4.5**—Es wurde ein [!DNL RabbitMQ] Absturzproblem bei der neuen Installation von Commerce 2.4.5 behoben.<!-- MCLOUD-9059 -->

## v2002.1.10

Veröffentlichungsdatum: 31. März 2022

- ![Fixsymbol](../../assets/fix.svg) **Elasticsearch 7.10**—Aktualisierte Validatoren zur Unterstützung der Version 7.10 von Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Veröffentlichungsdatum: 10. März 2022

- ![neues Symbol](../../assets/new.svg) **OpenSearch**: Unterstützung für OpenSearch für Adobe Commerce-Versionen 2.4.4, 2.4.3-p2 und 2.3.7-p3 hinzugefügt.<!-- MCLOUD-8296 -->
- ![neues Symbol](../../assets/new.svg) **PHP**—Es wurde Unterstützung für PHP 8.1 hinzugefügt.
- ![Fixsymbol](../../assets/fix.svg) **symfony/process**—Die Kompatibilität mit symfony/process ^5.3 wurde hinzugefügt.<!-- MCLOUD-8283 -->

- ![neues Symbol](../../assets/new.svg) **Mehrere Prozesse unterhalten** - Es wurde eine `multiple_processes` -Option hinzugefügt, mit der Sie die Anzahl der Prozesse festlegen können, die für jeden Verbraucher erzeugt werden sollen. Siehe Beschreibung der `CRON_CONSUMERS_RUNNER`-Variablen in den [Variablen bereitstellen](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![neues Symbol](../../assets/new.svg) **OpenSearch-Schema und vollständiger Host-Pfad**: Es wurde die Möglichkeit hinzugefügt, ein Elasticsearch-Schema und den vollständigen Host-Pfad zu konfigurieren.
- ![Fixsymbol](../../assets/fix.svg) **AWS S3**: Die Methode zur Aktivierung von AWS S3 wurde geändert.
- ![Fixsymbol](../../assets/fix.svg) **Fixieren Sie driver_options reader**—Es wurde die Konfiguration zum Lesen der driver_options für die DB-Verbindung aus der Datei `env.php` von `ece-tools` für Validatoren hinzugefügt.<!-- MCLOUD-8420 -->

## v2002.1.8

Veröffentlichungsdatum: 25. Oktober 2021

- ![neues Symbol](../../assets/new.svg) **Alternativer Abbildspeicherort**: Die Option `--dump-directory` wurde hinzugefügt, sodass Sie einen Zielordner für einen DB-Abbild auswählen können. Jetzt ist `/app/var/dump-main` der standardmäßige Zielordner für einen DB-Dump. Siehe [Backup management: Dump your database](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![Fixsymbol](../../assets/fix.svg) **Monolog aktualisieren**: Die für das `monolog`-Paket erforderliche Mindestversion wurde auf `^2.3` aktualisiert.<!-- ACMP-1263 -->
- ![Fixsymbol](../../assets/fix.svg) **Symfony aktualisieren**: Die Symfony-Abhängigkeiten wurden aktualisiert und sind nun mit Adobe Commerce 2.4.4 kompatibel.<!-- ACMP-1533 -->
- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Feature/resolve Autoload** - Es wurde ein Problem bei der Bereitstellung in einer Integrationsumgebung und der Anzeige des `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.`-Fehlers behoben.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Veröffentlichungsdatum: 29. Juli 2021

**Konfigurationsaktualisierungen**—

- ![neues Symbol](../../assets/new.svg) Unterstützung für Composer 2.0 hinzugefügt.<!--MCLOUD-8003-->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte Composer-Anforderungen für`symphony/console`**—Die ECE-Tools `composer.json`-Versionsanforderungen für das `symphony/console`-Paket wurden aktualisiert, um ein Problem zu beheben, das dazu führte, dass die `di:compile`-Befehle mit dem folgenden Fehler fehlschlugen: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![ Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die Prüfungen für das Ende der Lebensdauer der Software (`eol.yaml`) wurden aktualisiert und enthalten nun Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Veröffentlichungsdatum: 20. April 2021

- ![neues Symbol](../../assets/new.svg) **Redis authentication credentials** - Es wurde die Möglichkeit hinzugefügt, während der Bereitstellungsphase Redis-Autorisierungsberechtigungen aus der `relationships` -Eigenschaft zu lesen.<!--MCLOUD-7694-->

- ![neues Symbol](../../assets/new.svg) **Anmeldedaten für die Elasticsearch-Autorisierung**: Es wurde die Möglichkeit hinzugefügt, während der Bereitstellungsphase Anmeldeinformationen für die Elasticsearch-Autorisierung aus der Eigenschaft `relationships` zu lesen.<!--MCLOUD-7695-->

- ![neues Symbol](../../assets/new.svg) **Dedizierter Sitzungsspeicherdienst**—`redis-session` wurde als zweite Option für die Sitzungsspeicherung hinzugefügt. Sie können den `redis-session`-Dienst verwenden, um Sitzungsinformationen zu speichern und den `redis`-Dienst für den Cache zu verwenden, um eine bessere Leistung zu erzielen.<!--MCLOUD-7698-->

- ![neues Symbol](../../assets/new.svg) **Veraltete SPLIT_DB-Meldungen** - Es wurden Validator-Warnungen und kritische Meldungen für die veraltete `SPLIT_DB` -Option für Adobe Commerce 2.4.2 und deren Entfernung in Adobe Commerce 2.5.0 hinzugefügt.<!--MCLOUD-7806-->

- ![Fixsymbol](../../assets/fix.svg) **Elasticsearch-Version aus Beziehungen** - Der Service-Validator wurde behoben, um die richtige Version des Elasticsearchs aus den `relationships` -Eigenschaften in Cloud Docker- und Integrationsumgebungen abzurufen.<!--MCLOUD-7572-->

- ![Fixsymbol](../../assets/fix.svg) **Flexible Überprüfung der Anschlussvalidierung** - Redis kann jetzt den Port in einer benutzerdefinierten Cache-Verbindung über die `server`-URL validieren. Sie können beispielsweise Ihre Portnummer wie folgt zu Ihrer Server-URL hinzufügen: `server: 'tcp://rfs-store-simple-page-cache:26379'`. Dadurch wird verhindert, dass Überprüfungsfehler auftreten, wenn die Option `port` fehlt oder falsch ist.<!--MCLOUD-7722-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Aktualisierung auf Adobe Commerce 2.4.2** - Es wurde ein Problem behoben, bei dem Benutzer nach der Aktualisierung auf Adobe Commerce 2.4.2 <!--MCLOUD-7776--> manuell `bin/magento setup:upgrade` ausführen mussten, damit ihre Sites betriebsbereit waren.

## v2002.1.5

Veröffentlichungsdatum: 1. Februar 2021

- ![neues Symbol](../../assets/new.svg) **Remote-Speicher**: Die Umgebungsvariable `REMOTE_STORAGE` wurde hinzugefügt, um Cloud-Projekte für die Remote-Speicherung von Mediendateien mithilfe eines Speicherdienstes wie AWS S3 zu aktivieren. Diese Konfigurationsoption ist Teil des ECE-Tools-Pakets, wird aber in Adobe Commerce nicht in der Cloud-Infrastruktur unterstützt.<!--MCLOUD-7153-->

- ![neues Symbol](../../assets/new.svg) **Neuer `cloud:config:validate` Befehl**—Der Befehl `php vendor/bin/ece-tools cloud:config:validate` wurde hinzugefügt, um die `.magento.env.yaml` -Konfiguration zu validieren, bevor Änderungen an die Remote-Cloud-Umgebung gepusht werden.<!--MCLOUD-7120-->

- ![neues Symbol](../../assets/new.svg) **Leeren des opcache**—Es wurde Unterstützung für die PHP-Option `opcache.enable_cli` hinzugefügt, um den OPcache zu leeren, bevor der Bereitstellungs-Hook ausgeführt wird. Durch diese Konfiguration wird die Cache-Konfiguration zurückgesetzt, um sicherzustellen, dass die aktuellen Konfigurationseinstellungen auf jede Bereitstellung angewendet werden.<!--MCLOUD-7015-->

- ![neues Symbol](../../assets/new.svg) **Validierung von Aurora DB**: Die Validierung des Datenbankdienstes wurde aktualisiert, sodass er mit der Aurora-Datenbank kompatibel ist.<!--MCLOUD-7269-->

- ![neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable SCD_NO_PARENT**—Es wurde die Umgebungsvariable `SCD_NO_PARENT` hinzugefügt (für Adobe Commerce >=2.4.2), um die Erstellung von statischen Inhalten für übergeordnete Designs zu verwalten.<!--MCLOUD-7284-->

- ![Fixsymbol](../../assets/fix.svg) **Speicherbeschränkungen und -befehle** - Es wurde ein Problem behoben, bei dem `php vendor/bin/ece-tools`-Befehle nicht funktionierten, wenn die Größe der `cloud.log`-Datei das PHP-Speicherlimit überschritt. Anstatt die gesamte `cloud.log` -Datei in den Speicher zu lesen, lesen wir jetzt nur eine kleinere Teilmenge der Daten aus der Protokolldatei.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![Fixsymbol](../../assets/fix.svg) **Benutzerdefinierte Datenbankverbindungen** - Es wurde ein `.magento.env.yaml` Konfigurationsproblem behoben, bei dem benutzerdefinierte Datenbankverbindungen, die für `DATABASE_CONFIGURATION` definiert wurden, nicht verwendet wurden. Die Verbindungseinstellungen wurden nicht zu `app/etc/env.php`<!--MCLOUD-7426--> hinzugefügt.

- ![Fixsymbol](../../assets/fix.svg) **Leere Fehlerprotokolle** - Es wurde ein Problem behoben, das dazu führte, dass Bereitstellungen fehlschlugen, wenn der `cloud.error.log` leer war.<!--MCLOUD-7296-->

- ![Fixsymbol](../../assets/fix.svg) **Validierung von MariaDB 10.3**—Korrektur der Validierung von MariaDB 10.3 für Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![Fixsymbol](../../assets/fix.svg) **Cache:flush logging**—Verbesserte Protokolleinträge, um den Start und das Ende des `cache:flush` Schritts anzuzeigen.<!--MCLOUD-7503-->

## v2002.1.4

Veröffentlichungsdatum: 19. November 2020

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das zu einem Bereitstellungsfehler führte, wenn die in der Umgebungsvariable `SEARCH_CONFIGURATION` angegebene Suchmaschine ein anderer Wert als `elasticsearch` war.<!--MCLOUD-7283-->

## v2002.1.3

Veröffentlichungsdatum: 9. November 2020

**Aktualisierungen der Infrastruktur**—

- ![neues Symbol](../../assets/new.svg) ECE-Tools-Unterstützung für das schreibgeschützte Verzeichnis `pub/static` hinzugefügt, wenn der statische Inhalt auf die Bereitstellung im Build-Schritt eingestellt ist.<!--MC-37699-->

- ![neues Symbol](../../assets/new.svg) Unterstützung für Elasticsearch 7.9 und Redis 6 zur Kompatibilität mit kommenden Adobe Commerce-Versionen hinzugefügt.<!--MCLOUD-7191-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die ECE-Tools `composer.json` wurden aktualisiert, um eine erforderliche Abhängigkeit für das Tool &quot;Qualitätsmuster&quot;hinzuzufügen. Dadurch wird eine zirkuläre Abhängigkeit behoben, die zwischen den ECE-Tools- und Magento-cloud-patches-Paketen bestand.<!--MCLOUD-6910-->

**Validierungs- und Protokollverbesserungen**—

- ![neues Symbol](../../assets/new.svg) Suchmaschinenvalidierung hinzugefügt, um sicherzustellen, dass `elasticsearch` für Adobe Commerce in der Cloud-Infrastruktur 2.4 und höher festgelegt ist. Wenn die Validierung fehlschlägt, wird die Bereitstellung mit einer kritischen Fehlermeldung angehalten, die Fehlerbehebungen für das Problem vorschlägt. Siehe [Kritische Fehler, Bereitstellen von Schritt](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![neues Symbol](../../assets/new.svg) Elasticsearch-Überprüfung hinzugefügt, um die Kompatibilität zwischen der Elasticsearch-Dienstversion und der Adobe Commerce-Version zu überprüfen.<!--MCLOUD-7193-->

- ![neues Symbol](../../assets/new.svg) Die Fehlermeldung zur Elasticsearch-Kompatibilität wurde aktualisiert, um die Versionen von Elasticsearch anzuzeigen, die mit dem Adobe Commerce-Elasticsearch-Modul kompatibel sind. Die Fehlermeldung enthält jetzt die spezifischen Elasticsearch-Versionen, die in Ihrer Cloud-Infrastruktur installiert werden sollen, damit sie mit dem von Ihrer Adobe Commerce-Elasticsearch-Version verwendeten -Modul kompatibel sind. Siehe [Warnfehler, Schritt bereitstellen](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![neues Symbol](../../assets/new.svg) Hinzugefügte Warnmeldungen `2026` und `2027` für ungültige Umgebungsvariableneinstellung `MAGE_MODE`. Der einzige gültige Wert ist `production`. Vor dieser Fehlerbehebung konnte `MAGE_MODE` ohne Bereitstellungsfehler auf `developer` gesetzt werden, um später beim Versuch, in schreibgeschützte Dateien zu schreiben, nur Fehler zu verursachen. Siehe [Warnfehler](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![Fixsymbol](../../assets/fix.svg) Die Validierung für Redis-, RabbitMQ- und MySQL-Dienste wurde korrigiert, um sicherzustellen, dass diese Versionen mit der Adobe Commerce-Version kompatibel sind. Gültige Versionen dieser Dienste werden jetzt in die `cloud.log` geschrieben.<!--MCLOUD-7098-->

- ![Fixsymbol](../../assets/fix.svg) Das `cloud.log` wurde aktualisiert, um die Begrenzung für gleichzeitige Anforderungen beim Senden von Anforderungen während der Cache-Aufwärmung einzuschließen. Dieser Wert wird in der Variablen [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) post-deploy<!--MCLOUD-5563--> konfiguriert.

**Aktualisierungen des CLI-Befehls**—

- ![neues Symbol](../../assets/new.svg) CLI-Befehle (`cloud:config:create` und `cloud:config:update`) wurden hinzugefügt, um die `.magento.env.yaml` -Datei zu erstellen und mit einer Konfiguration zu aktualisieren, die mindestens eine Build-, Bereitstellungs- und Post-Deploy-Variablen enthalten kann. Siehe [Konfigurationsdatei aus CLI erstellen](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Aktualisierungen der Umgebungsvariablen**—

- ![neues Symbol](../../assets/new.svg) Die Build-Variable [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) wurde hinzugefügt. Wenn Sie die Variable auf &quot;`true`&quot; setzen, wird die Anwendung während einer Cloud Docker-Installation für Commerce daran gehindert, den Befehl &quot;`composer dump-autoload`&quot;auszuführen. Die -Variable ist nur für Cloud Docker für Commerce-Container mit beschreibbaren Dateisystemen relevant (erstellt zum Testen und Entwickeln mit `./vendor/bin/ece-docker build:compose --with-test`). Bei solchen Installationen verhindert das Überspringen des Befehls `composer dump-autoload` Fehler, wenn andere Befehle ausgeführt werden, die versuchen, auf Dateien aus einem gelöschten Verzeichnis `generated` zuzugreifen.<!--MCLOUD-6939-->

## v2002.1.2

Releasedatum: 5. August 2020

**Validierungs- und Protokollverbesserungen**—

- ![neues Symbol](../../assets/new.svg) Die Datei &quot;`schema.error.yaml`&quot;wurde hinzugefügt, die alle Fehler- und Warnbenachrichtigungen enthält, die während des Build-, Bereitstellungs- und Post-Bereitstellungsprozesses auftreten können, sowie Vorschläge zur Behebung der Fehler. Die Informationen in dieser Datei sind auch im _Cloud-Handbuch für Commerce_ verfügbar. Siehe [Fehlermeldungsreferenz für ece-tools](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![neues Symbol](../../assets/new.svg) Die Einträge im Cloud-Fehlerprotokoll (`/var/log/cloud.error.log`) wurden in das JSON-Format geändert, um die programmgesteuerte Analyse des Protokolls zu vereinfachen.<!--MCLOUD-5879-->

- ![neues Symbol](../../assets/new.svg) Zusätzliche Fehlerprüfungen zum Erstellen, Bereitstellen und Bereitstellen der Verarbeitung nach der Bereitstellung sowie verbesserte vorhandene Prüfungen wurden hinzugefügt:

   - Fehler-Code 2026 - Während der Build-Phase erzeugte Daten konnten nicht in den bereitgestellten Ordnern wiederhergestellt werden

   - Fehler-Code 3004 - Sicherungsdateien können nicht erstellt werden

   - Fehler-Code 102 - Zusätzliche Prüfungen für Probleme wurden hinzugefügt, die auftreten, wenn die `env.php`-Datei nicht schreibbar ist <!--MCLOUD-6221-->

- ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable **QUALITY_PATCH** wurde hinzugefügt, um einen oder mehrere Qualitäts-Patches anzugeben, die während des Bereitstellungsprozesses angewendet werden sollen. Siehe [Variablen erstellen](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Veröffentlichungsdatum: 25. Juni 2020

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Infrastruktur**—

   - ![neues Symbol](../../assets/new.svg) **Verbesserungen bei der Protokollierung**: Die Log-Tracking-Funktion wurde verbessert, indem Ausstiegscodes kritischen Bereitstellungsfehlern zugewiesen und Ausstiegscodes in Fehlerbenachrichtigungen und Protokollereignissen angezeigt wurden. Siehe [Fehlermeldungsreferenz für ece-tools](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![neues Symbol](../../assets/new.svg) Der Prozess für Datenbank-Dumps (`vendor/bin/ece-tools db-dump`) und aktualisierte Protokollmeldungen wurden verbessert, um klarzustellen, dass der Datenbankabbildvorgang die Anwendung in den Wartungsmodus wechselt, die Verarbeitung von Verbraucherwarteschlangen stoppt und Cron-Aufträge deaktiviert, bevor der Abbildmodus gestartet wird.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, um sicherzustellen, dass die Projekt-URL bei der Bereitstellung in Staging- und Produktionsumgebungen korrekt aktualisiert wird. Jetzt verwendet `ece-tools` die URL für die Route, wobei das Attribut `primary:true` in der Konfiguration der Projektroute festgelegt ist. Siehe [Variablen bereitstellen](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Der Workflow für das Build-Szenario `generate.xml` zum Anwenden von Patches wurde aktualisiert. Patches müssen zuvor angewendet werden, um Adobe Commerce zu aktualisieren und alle Probleme zu beheben, die dazu führen können, dass die Schritte `di:compile` und `module:refresh` fehlschlagen.<!--MCLOUD-5941-->

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem im Installationsprozess behoben, durch das fälschlicherweise der Fehler `Crypt key missing` zurückgegeben wurde. Der `crypt/key` -Wert wird während der Installation automatisch generiert.<!--MCLOUD-6120-->

- ![neues Symbol](../../assets/new.svg) **Dienstaktualisierungen**—

   - ![neues Symbol](../../assets/new.svg) Unterstützung für PHP 7.4 und MariaDB 10.4 hinzugefügt.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![neues Symbol](../../assets/new.svg) Die Variable **SCD_USE_BALER** wurde hinzugefügt, um das Baler-Modul für das JavaScript-Bundling während des Build-Prozesses der Cloud-Infrastruktur in Adobe Commerce zu aktivieren. Siehe die Variablenbeschreibung in den [Build-Variablen](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable **REDIS_BACKEND** wurde hinzugefügt, um das Redis-Backend-Modell für den Redis-Cache für Adobe Commerce 2.3.5 oder höher zu konfigurieren. Siehe die Variablenbeschreibung in den [Bereitstellungsvariablen](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![neues Symbol](../../assets/new.svg) **CLI-Befehl aktualisiert**—

   - ![neues Symbol](../../assets/new.svg) Die folgenden CLI-Befehle wurden mit einer Option für eine detailliertere Protokollierung aktualisiert:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Die Protokollierungsstufe für jeden Aufruf wird durch die Konfiguration der Variable [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) in der Datei `.magento.env.yaml` bestimmt.<!--MCLOUD-3503-->

- ![neues Symbol](../../assets/new.svg) **Verbesserungen bei der Validierung**—

   - ![neues Symbol](../../assets/new.svg) **Kompatibilitätsprüfungen für Elasticsearch 7.x**—Die Überprüfung des Elasticsearchs für Kompatibilitätsprüfungen mit Elasticsearch 7.x wurde aktualisiert.<!--MCLOUD-5542-->

   - ![neues Symbol](../../assets/new.svg) **Aktualisierte Dienstversion und EOL-Validierungsprüfungen**—Aktualisierung der Validierung, um installierte Dienstversionen anhand der Anforderungen von Adobe Commerce 2.4 zu überprüfen.<!--MCLOUD-6144-->

   - ![Fixsymbol](../../assets/fix.svg) Korrektur eines Validierungsproblems, sodass die folgende Warnmeldung nach der Bereitstellung nur angezeigt wird, wenn die `post-deploy` -Hook-Konfiguration in der `.magento.app.yaml`-Datei fehlt:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![neues Symbol](../../assets/new.svg) **Validierung für Zend Framework-Abhängigkeiten hinzugefügt**—Hinzufügung der Komponentenabhängigkeit für das Zend Framework, das zum Laminas-Projekt migriert wurde. Wenn die erforderlichen Abhängigkeiten fehlen, wird während des Build-Prozesses die folgende Fehlermeldung angezeigt.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Siehe [Überprüfen der Zend-Framework-Abhängigkeiten](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![neues Symbol](../../assets/new.svg) **Validierung für `env.php` Datei und Daten hinzugefügt** - Es wurden Prüfungen für die `env.php`-Datei und -Daten während des Installations- und Aktualisierungsprozesses hinzugefügt.<!--MCLOUD-5991-->

      - Wenn die Datei `env.php` in der Installation fehlt und der Wert `crypt/key` nicht in der Datei `.magento.app.yaml` angegeben ist, schlägt die Bereitstellung mit der folgenden Benachrichtigung fehl:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Wenn die Installation nicht die Datei `env.php` enthält oder die Konfiguration nur einen Cache-Typ enthält, wird während des Aktualisierungsprozesses der Befehl `cron:enable` ausgeführt, um die Datei mit allen `cache_types` wiederherzustellen. Die folgende Benachrichtigung wird dem Protokoll hinzugefügt:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Veröffentlichungsdatum: 6. Februar 2020

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Infrastruktur**—

   - ![neues Symbol](../../assets/new.svg) **Das separate Paket für Cloud Docker für Commerce wurde hinzugefügt** - Das Docker-Paket wurde aus dem `ece-tools`-Paket entpackt, um die Codequalität zu wahren und unabhängige Versionen bereitzustellen. Aktualisierungen und Fehlerbehebungen im Zusammenhang mit `ece-tools` werden vom GitHub-Repository [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) verwaltet.<!--MAGECLOUD-2927-->

   - ![neues Symbol](../../assets/new.svg) **Aktualisierte Patchfunktionen** - Die Patchfunktion wurde vom ECE-Tools-Paket in ein separates Paket [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) verschoben. Während der Bereitstellung verwendet `ece-tools` das neue Paket, um Patches anzuwenden. Siehe [Versionshinweise zu Cloud-Patches](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![neues Symbol](../../assets/new.svg) **Aktualisierte Composer-Abhängigkeiten** - Die `composer.json` -Datei für Adobe Commerce für die Cloud-Infrastruktur mit einer Abhängigkeit für das Paket `magento/magento-cloud-docker` wurde aktualisiert. Jetzt enthält `ece-tools` Abhängigkeiten für alle Pakete im [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Diese Pakete werden automatisch installiert und aktualisiert, wenn Sie `ece-tools` installieren oder aktualisieren.

- ![neues Symbol](../../assets/new.svg) **Unterstützung für szenario-basierte Bereitstellungen**—<!--MAGECLOUD-4101-->

   - ![neues Symbol](../../assets/new.svg) Sie können jetzt den Build, die Bereitstellung und die Nachbereitstellung von Prozessen mithilfe von XML-Konfigurationsdateien anpassen, um die Standardkonfiguration zu überschreiben oder anzupassen.

   - ![neues Symbol](../../assets/new.svg) **Änderung der `hooks` -Konfiguration in`.magento.app.yaml`** - Wir haben das `hooks` -Konfigurationsformat aktualisiert, um szenario-basierte Bereitstellungen zu unterstützen. Das alte Format aus früheren ECE-Tools-Versionen 2002.0.x wird weiterhin unterstützt. Sie müssen jedoch auf das neue Format aktualisieren, um die szenario-basierte Bereitstellungsfunktion zu verwenden. Siehe [Szenario-basierte Bereitstellungen](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Bevor Sie auf die ECE-Tools-Version 2002.1.0 aktualisieren, überprüfen Sie die [rückwärts   inkompatible Änderungen](backward-incompatible-changes.md) , um mehr über Änderungen zu erfahren, für die Sie möglicherweise   Aktualisieren Sie Adobe Commerce in der Konfiguration oder den Prozessen von Cloud-Infrastrukturprojekten.

- ![neues Symbol](../../assets/new.svg) **Dienstaktualisierungen**—

   - ![neues Symbol](../../assets/new.svg) Unterstützung für PHP 7.3 wurde hinzugefügt.<!--MAGECLOUD-4022-->

   - ![neues Symbol](../../assets/new.svg) Unterstützung für RabbitMQ 3.8 hinzugefügt.<!--MAGECLOUD-4674-->

   - ![neues Symbol](../../assets/new.svg) Es wurde eine Validierung hinzugefügt, um die installierten Dienstversionen mit dem Datum der Einstellung für die Abschaffung für jeden Dienst zu vergleichen. Jetzt erhalten Kunden eine Benachrichtigung, wenn eine Dienstversion innerhalb von drei Monaten nach dem Datum der Einstellung der Unterstützung verfügbar ist, und eine Warnung, wenn das Datum der Abschaffung in der Vergangenheit liegt.<!--MAGECLOUD-4076-->

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem bei der Konfiguration von Elasticsearch behoben, um sicherzustellen, dass die richtigen Elasticsearch-Einstellungen in allen Umgebungen konfiguriert sind.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Unter [Dienstversionen](../services/services-yaml.md#service-versions) finden Sie eine Liste der in Adobe Commerce in der Cloud-Infrastruktur verwendeten Dienste und deren Versionskompatibilität mit der Cloud-Vorlage.

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![neues Symbol](../../assets/new.svg) Die Funktionalität der Umgebungsvariablen `WARM_UP_PAGES` wurde erweitert, um das Vorausfüllen des Caches für bestimmte Produktseiten zu unterstützen. Siehe die erweiterte Definition im Thema [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages) .<!--MAGECLOUD-4444-->

   - ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable `ERROR_REPORT_DIR_NESTING_LEVEL` wurde hinzugefügt, um die Verwaltung von Fehlerberichtsdaten im Verzeichnis `<magento_root>/var/report/` zu vereinfachen. Weitere Informationen finden Sie in der Variablenbeschreibung im Thema [Build-Variablen](../environment/variables-build.md#error_report_dir_nesting_level) .

   - ![Fixsymbol](../../assets/fix.svg) Die Umgebungsvariablen `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`, `DO_DEPLOY_STATIC_CONTENT` und `STATIC_CONTENT_SYMLINK` wurden entfernt. Siehe [Abwärtskompatible Änderungen](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![Fixsymbol](../../assets/fix.svg) Korrektur eines Problems im Elastic Suite-Konfigurationsprozess, sodass die Standardkonfiguration wie erwartet überschrieben wird, wenn Sie die `ELASTICSUITE_CONFIGURATION` -Bereitstellungsvariable ohne die `_merge` -Option konfigurieren.<!--MAGECLOUD-4388-->

- ![neues Symbol](../../assets/new.svg) **CLI-Befehl aktualisiert**—

   - ![neues Symbol](../../assets/new.svg) **Neuer Cron-Befehl**: Sie können jetzt die Cron-Verarbeitung in Ihrer Adobe Commerce-Umgebung in der Cloud-Infrastruktur mithilfe der Befehle `cron:disable` und `cron:enable` manuell verwalten. Verwenden Sie den Befehl disable , um alle aktiven Cron-Prozesse anzuhalten und alle Cron-Aufträge zu deaktivieren. Verwenden Sie den Befehl &quot;Aktivieren&quot;, um Cron-Aufträge erneut zu aktivieren, wenn Sie bereit sind. Siehe [Deaktivieren von Cron-Aufträgen](../application/crons-property.md#disable-cron-jobs).

   - ![neues Symbol](../../assets/new.svg) **Verbesserte Fehlerberichterstellung** - Es wurde eine bessere Protokollierung für CLI-Befehlsfehler hinzugefügt, die während der Verarbeitung der ECE-Tools auftreten.<!--MAGECLOUD-4849-->

   - ![neues Symbol](../../assets/new.svg) **Entfernt veraltete Build-Befehle**— Die folgenden Build-Befehle wurden entfernt: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump` und `ece-tools docker` wurden in `ece-docker` umbenannt. Siehe [Abwärtskompatible Änderungen](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![neues Symbol](../../assets/new.svg) Entfernte die veraltete `build_options.ini`-Datei und fügte eine Validierung hinzu, um den Build bei vorhandener Datei fehlschlagen zu lassen. Verwenden Sie die Datei [.magento.env.yaml](../environment/configure-env-yaml.md) , um Build-Optionen zu konfigurieren.

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das dazu führte, dass der Build-Prozess fehlschlug, wenn die `config.php` -Datei leer war.<!--MAGECLOUD-4127-->

## 2002.0.23

Veröffentlichungsdatum: 27. Februar 2020

- ![Symbol zur Fehlerbehebung](../../assets/fix.svg) Es wurde ein Kompatibilitätsproblem mit den Versionen `ece-tools` 2002.0.x behoben, das verhinderte, dass die On-Demand-Erstellung von statischen Inhalten im Produktionsmodus erfolgreich abgeschlossen wurde.

## Ältere Versionen

Siehe Archiv mit den [Versionshinweisen](cloud-release-archive.md) für Version 2002.0.22 und früher.
