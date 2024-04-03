---
title: ECE-Tools - Versionshinweise
description: Siehe eine Liste der neuesten Verbesserungen des ECE-Tools-Pakets.
recommendations: noDisplay, catalog
last-substantial-update: 2024-01-16T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: f2aa4aa183298d829d27c4641f21acef1514d312
workflow-type: tm+mt
source-wordcount: '2887'
ht-degree: 0%

---

# ECE-Tools - Versionshinweise

Die [ece-tools](https://github.com/magento/ece-tools) -Paket ist ein Satz von Skripten und Tools zur Verwaltung und Bereitstellung von Cloud-Projekten. Diese Versionshinweise beschreiben die neuesten Verbesserungen an diesem Paket, das Teil der [Cloud Tools Suite für Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Siehe [ECE-Tools aktualisieren](../dev-tools/update-package.md) für Informationen zur Aktualisierung auf die neueste Version des `ece-tools` Paket.

Die `ece-tools` -Paket verwendet die folgende Versionsversionierungssequenz: `200<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![Neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v2002.1.17 {#latest}

Veröffentlichungsdatum: 16. Januar 2024

- ![Fixsymbol](../../assets/fix.svg) **Validator für Elasticsearch und OpenSearch**—Korrektur des Validators, der eine irreführende Meldung zur Installation eines Suchdienstes erzeugt hat, wenn LiveSearch aktiviert ist.<!-- MCLOUD-10167 -->
- ![Fixsymbol](../../assets/fix.svg) **Bereitstellungswarnung**—Es wurde ein Problem behoben, das zu Bereitstellungswarnungen zu nicht leeren Ordnern führte.<!-- MCLOUD-8958 -->

## v2002.1.16

Veröffentlichungsdatum: 16. Oktober 2023

- ![Neues Symbol](../../assets/new.svg) **Globale Umgebungsvariable ENABLE_WEBHOOKS**—Die [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) globale Variable zur Verwendung mit Commerce-Webhooks, um eine Verbindung zu einem externen Endpunkt herzustellen, z. B. App Builder-Laufzeitaktion oder ein Inventarverwaltungssystem von Drittanbietern.

## v2002.1.15

Veröffentlichungsdatum: 31. Juli 2023

- ![Fixsymbol](../../assets/fix.svg) **Fehler-Codes**—Aktualisiertes Fehlercode-Schema und -Dokumentgenerator für Fehler-Codes.
- ![Fixsymbol](../../assets/fix.svg) **Validator für benutzerdefiniertes Redis-Modell**-Der Validator für benutzerdefinierte Redis-Backend-Modelle wurde aktualisiert. [Siehe Beispiel für die Cache-Konfiguration](../environment/variables-deploy.md#cache_configuration).
- ![Fixsymbol](../../assets/fix.svg) **Validator für RabbitMQ**-Hinzugefügte Unterstützung für RabbitMQ 3.11
- ![Fixsymbol](../../assets/fix.svg) **Der falsche Link wurde korrigiert**-Korrektur des falschen Links zur Onboarding-Dokumentation in der Begrüßungs-E-Mail-Vorlage.

## v2002.1.14

Veröffentlichungsdatum: 10. März 2023

- ![Neues Symbol](../../assets/new.svg) **PHP**—Unterstützung für PHP 8.2 hinzugefügt.
- ![Neues Symbol](../../assets/new.svg) **Validatoren für Dienste**—Aktualisierte Validatoren für Commerce 2.4.6 erforderte Dienste: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x und RabbitMQ 3.9.
- ![Fixsymbol](../../assets/fix.svg) **ece-tools db-dump**—Korrektur eines Problems, das dazu führte, dass das `db-dump` vorzeitig anhalten.

## v2002.1.13

Veröffentlichungsdatum: 27. Oktober 2022

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für Adobe I/O-Ereignisse für Adobe Commerce hinzugefügt**. Erweiterungsentwickler können jetzt die [Adobe I/O-Ereignisse](https://developer.adobe.com/events/docs/) Framework zum Senden von Commerce-Ereignisinformationen von Cloud-Instanzen an ihre Anwendungen, die für geschrieben wurden [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Adobe I/O-Ereignisse für Adobe Commerce befinden sich in der Partnervorschau.<!-- CEXT-932 -->
- ![Neues Symbol](../../assets/new.svg) **Validator für die OPcache-Konfiguration**—Es wurde ein Validator hinzugefügt, um die OPcache-Konfiguration auf ausgeschlossene Pfade zu überprüfen.<!-- MCLOUD-9485 -->
- ![Fixsymbol](../../assets/fix.svg) **Problem mit der GraphQL-Cache-Konfiguration behoben**—Jetzt bewahren die ECE-Tools die GraphQL auf `id_salt` Wert in `cache` Konfiguration in der `app/etc/env.php` -Datei.<!-- MCLOUD-9486 -->

## v2002.1.12

Veröffentlichungsdatum: 13. September 2022

- ![Neues Symbol](../../assets/new.svg) **Aktivieren`synchronous_replication`**—ECE-Tools-Sets `synchronous_replication=>true` im `app/etc/env.php` Datei beim `MYSQL_USE_SLAVE_CONNECTION` aktiviert ist. Diese Konfiguration betrifft nur Commerce 2.4.6+. Siehe `MYSQL_USE_SLAVE_CONNECTION` Variablenbeschreibung in [Bereitstellen von Variablen](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![Neues Symbol](../../assets/new.svg) **OpenSearch**—Zusätzliche Funktionen zum Konfigurieren und Festlegen der `opensearch` Engine für die nächste Adobe Commerce-Version 2.4.6. Siehe [Einrichten des OpenSearch-Dienstes](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.1

Veröffentlichungsdatum: 4. August 2022

- ![Fixsymbol](../../assets/fix.svg) **ElasticSuite Validator und OpenSearch**—Korrektur des Validierungsproblems bei der ElasticSuite-Integritätsprüfung bei der Installation von OpenSearch.<!-- MCLOUD-8767 -->
- ![Fixsymbol](../../assets/fix.svg) **Rückgabetypen für Bereitstellungsbefehle**—Feste Rückgabetypen für Bereitstellungsbefehle.<!-- AC-3208 -->
- ![Fixsymbol](../../assets/fix.svg) **[!DNL RabbitMQ]Problem mit der neuen Commerce 2.4.5-Installation**—Fixed [!DNL RabbitMQ] Absturzproblem bei der neuen Commerce 2.4.5-Installation.<!-- MCLOUD-9059 -->

## v2002.1.10

Veröffentlichungsdatum: 31. März 2022

- ![Fixsymbol](../../assets/fix.svg) **Elasticsearch 7.10**—Validatoren wurden aktualisiert, um die Version 7.10 von Elasticsearch zu unterstützen.<!-- MCLOUD-8548 -->

## v2002.1.9

Veröffentlichungsdatum: 10. März 2022

- ![Neues Symbol](../../assets/new.svg) **OpenSearch**—Unterstützung für OpenSearch für Adobe Commerce-Versionen 2.4.4, 2.4.3-p2 und 2.3.7-p3 hinzugefügt.<!-- MCLOUD-8296 -->
- ![Neues Symbol](../../assets/new.svg) **PHP**—Hinzugefügte Unterstützung für PHP 8.1.
- ![Fixsymbol](../../assets/fix.svg) **symfony/process**—Die Kompatibilität mit symfony/process ^5.3 wurde hinzugefügt.<!-- MCLOUD-8283 -->

- ![Neues Symbol](../../assets/new.svg) **Mehrere Prozesse für Verbraucher**—Hinzufügung einer `multiple_processes` -Option, damit Sie die Anzahl der Prozesse festlegen können, die für jeden Verbraucher erzeugt werden sollen. Siehe `CRON_CONSUMERS_RUNNER` Variablenbeschreibung in [Bereitstellen von Variablen](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![Neues Symbol](../../assets/new.svg) **OpenSearch-Schema und vollständiger Host-Pfad**—Es wurde die Möglichkeit hinzugefügt, ein Elasticsearch-Schema und den vollständigen Host-Pfad zu konfigurieren.
- ![Fixsymbol](../../assets/fix.svg) **AWS S3**—Die Methode zur Aktivierung von AWS S3 wurde geändert.
- ![Fixsymbol](../../assets/fix.svg) **Reader &quot;driver_options&quot; reparieren**—Die Konfiguration für das Lesen der driver_options für die DB-Verbindung aus dem `env.php` Datei nach `ece-tools` für Validatoren.<!-- MCLOUD-8420 -->

## v2002.1.8

Veröffentlichungsdatum: 25. Oktober 2021

- ![Neues Symbol](../../assets/new.svg) **Alternative Abbildposition**—Die `--dump-directory` -Option, damit Sie einen Zielordner für einen DB-Dump auswählen können. Jetzt `/app/var/dump-main` ist der Standardzielordner für einen DB-Dump. Siehe [Backup-Management: Dump Ihrer Datenbank](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![Fixsymbol](../../assets/fix.svg) **Monolog aktualisieren**—Die für die `monolog` Paket zu `^2.3`.<!-- ACMP-1263 -->
- ![Fixsymbol](../../assets/fix.svg) **Symfony aktualisieren**—Aktualisierung der Symfony-Abhängigkeiten auf die Kompatibilität mit Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![Fixsymbol](../../assets/fix.svg) **Automatische Aktualisierung von Funktionen/Auflösung**—Es wurde ein Problem bei der Bereitstellung in einer Integrationsumgebung und beim Anzeigen der Variablen `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` Fehler.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Veröffentlichungsdatum: 29. Juli 2021

**Konfigurationsaktualisierungen**—

- ![Neues Symbol](../../assets/new.svg) Unterstützung für Composer 2.0 hinzugefügt.<!--MCLOUD-8003-->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte Composer-Anforderungen für`symphony/console`**—Aktualisierung der ECE-Tools `composer.json` Versionsanforderungen für `symphony/console` -Paket, um ein Problem zu beheben, das die `di:compile` -Befehle zum Fehlschlagen mit dem folgenden Fehler: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![Fixsymbol](../../assets/fix.svg) Aktualisierung der Softwareprüfungen zum Ende der Produktlebensdauer (`eol.yaml`), um Elasticsearch 7.9.x einzuschließen.<!--MCLOUD-7938-->

## v2002.1.6

Veröffentlichungsdatum: 20. April 2021

- ![Neues Symbol](../../assets/new.svg) **Redis-Authentifizierungsberechtigungen**—Es wurde die Möglichkeit hinzugefügt, Redis-Autorisierungsberechtigungen aus der `relationships` -Eigenschaft während der Bereitstellungsphase fest.<!--MCLOUD-7694-->

- ![Neues Symbol](../../assets/new.svg) **Anmeldeinformationen für die Elasticsearch-Autorisierung**—Es wurde die Möglichkeit hinzugefügt, Elasticsearch-Autorisierungsberechtigungen aus der `relationships` -Eigenschaft während der Bereitstellungsphase fest.<!--MCLOUD-7695-->

- ![Neues Symbol](../../assets/new.svg) **Dedizierter Sitzungsspeicherdienst**—Hinzugefügt `redis-session` als zweite Option für die Sitzungsspeicherung. Sie können die `redis-session` Dienst zum Speichern von Sitzungsinformationen und Verwenden der `redis` -Dienst für den Cache, um eine bessere Leistung zu erzielen.<!--MCLOUD-7698-->

- ![Neues Symbol](../../assets/new.svg) **Veraltete SPLIT_DB-Meldungen**—Es wurden Validator-Warnungen und kritische Meldungen für veraltete Benutzer hinzugefügt. `SPLIT_DB` Option für Adobe Commerce 2.4.2 und dessen Entfernung in Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![Fixsymbol](../../assets/fix.svg) **Elasticsearch-Version aus Beziehungen**—Fester Service-Validator zum Abrufen der richtigen Version des Elasticsearchs aus der `relationships` Eigenschaften in Cloud Docker- und Integrationsumgebungen.<!--MCLOUD-7572-->

- ![Fixsymbol](../../assets/fix.svg) **Flexible Überprüfung von Redis-Ports**—Redis kann jetzt den Port in einer benutzerdefinierten Cache-Verbindung von der `server` URL. Sie können beispielsweise Ihre Portnummer wie folgt zu Ihrer Server-URL hinzufügen: `server: 'tcp://rfs-store-simple-page-cache:26379'`. Dies hilft bei der Vermeidung von Validierungsfehlern, bei denen die Variable `port` fehlt oder ist falsch.<!--MCLOUD-7722-->

- ![Fixsymbol](../../assets/fix.svg) **Upgrade auf Adobe Commerce 2.4.2**—Es wurde ein Problem behoben, bei dem Benutzer manuell ausführen mussten. `bin/magento setup:upgrade` , damit ihre Standorte nach der Aktualisierung auf Adobe Commerce 2.4.2 betriebsbereit sind.<!--MCLOUD-7776-->

## v2002.1.5

Veröffentlichungsdatum: 1. Februar 2021

- ![Neues Symbol](../../assets/new.svg) **Remote-Speicher**—Die `REMOTE_STORAGE` Umgebungsvariable, um Cloud-Projekte für die Remote-Speicherung von Mediendateien zu aktivieren, die einen Speicherdienst wie AWS S3 verwenden. Diese Konfigurationsoption ist Teil des ECE-Tools-Pakets, wird jedoch in Adobe Commerce in der Cloud-Infrastruktur nicht unterstützt.<!--MCLOUD-7153-->

- ![Neues Symbol](../../assets/new.svg) **Neu `cloud:config:validate` command**—Hinzugefügt, Befehl `php vendor/bin/ece-tools cloud:config:validate` validieren Sie die `.magento.env.yaml` Konfiguration vor dem Übertragen von Änderungen in die Remote-Cloud-Umgebung.<!--MCLOUD-7120-->

- ![Neues Symbol](../../assets/new.svg) **Leeren des Cache**—Unterstützung für die `opcache.enable_cli` PHP-Option, um den OPcache zu leeren, bevor der Bereitstellungshaken ausgeführt wird. Durch diese Konfiguration wird die Cachekonfiguration zurückgesetzt, um sicherzustellen, dass die aktuellen Konfigurationseinstellungen bei jeder Bereitstellung angewendet werden.<!--MCLOUD-7015-->

- ![Neues Symbol](../../assets/new.svg) **Validierung der Aurora DB**—Die Validierung des Datenbankdienstes wurde aktualisiert, sodass sie mit der Aurora-Datenbank kompatibel ist.<!--MCLOUD-7269-->

- ![Neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable SCD_NO_PARENT**—Die `SCD_NO_PARENT` Umgebungsvariable (für Adobe Commerce >=2.4.2) verwenden, um die Generierung statischer Inhalte für übergeordnete Designs zu verwalten.<!--MCLOUD-7284-->

- ![Fixsymbol](../../assets/fix.svg) **Speicherbeschränkungen und Befehle**—Es wurde ein Problem behoben, bei dem `php vendor/bin/ece-tools` -Befehle funktionieren nicht, wenn die Größe der `cloud.log` -Datei die PHP-Speicherbegrenzung überschritten hat. Anstatt das gesamte `cloud.log` -Datei in den Speicher geschrieben haben, lesen wir jetzt nur noch eine kleinere Teilmenge der Daten aus der Protokolldatei.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![Fixsymbol](../../assets/fix.svg) **Benutzerdefinierte Datenbankverbindungen**—Korrektur einer `.magento.env.yaml` Konfigurationsproblem, bei dem benutzerdefinierte Datenbankverbindungen für `DATABASE_CONFIGURATION` wurden nicht verwendet. Die Verbindungsparameter wurden nicht zu `app/etc/env.php`.<!--MCLOUD-7426-->

- ![Fixsymbol](../../assets/fix.svg) **Leere Fehlerprotokolle**—Korrektur eines Problems, das dazu führte, dass Bereitstellungen fehlschlugen, wenn die Variable `cloud.error.log` war leer.<!--MCLOUD-7296-->

- ![Fixsymbol](../../assets/fix.svg) **MariaDB 10.3-Validierung**—Die Validierung von MariaDB 10.3 für Adobe Commerce 2.3.6-p1 wurde korrigiert.<!--MCLOUD-7416-->

- ![Fixsymbol](../../assets/fix.svg) **Cache:Flush-Protokollierung**—Verbesserte Protokolleinträge, um den Start und die Fertigstellung der `cache:flush` Schritt.<!--MCLOUD-7503-->

## v2002.1.4

Veröffentlichungsdatum: 19. November 2020

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das zu einem Bereitstellungsfehler führte, wenn die in der Variablen `SEARCH_CONFIGURATION` Umgebungsvariable ist ein anderer Wert als `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Veröffentlichungsdatum: 9. November 2020

**Aktualisierungen der Infrastruktur**—

- ![Neues Symbol](../../assets/new.svg) Unterstützung von ECE-Tools für schreibgeschützt hinzugefügt `pub/static` -Ordner, wenn der statische Inhalt auf die Bereitstellung im Build-Schritt eingestellt ist.<!--MC-37699-->

- ![Neues Symbol](../../assets/new.svg) Unterstützung für Elasticsearch 7.9 und Redis 6 zur Kompatibilität mit kommenden Adobe Commerce-Versionen hinzugefügt.<!--MCLOUD-7191-->

- ![Fixsymbol](../../assets/fix.svg) Aktualisierung der ECE-Tools `composer.json` , um eine erforderliche Abhängigkeit für das Tool &quot;Qualitätsmuster&quot;hinzuzufügen. Dadurch wird eine zirkuläre Abhängigkeit behoben, die zwischen den ECE-Tools- und Magento-Cloud-Patches-Paketen bestand.<!--MCLOUD-6910-->

**Validierungs- und Protokollverbesserungen**—

- ![Neues Symbol](../../assets/new.svg) Suchmaschinenvalidierung hinzugefügt, um sicherzustellen, dass `elasticsearch` für Adobe Commerce auf Cloud-Infrastruktur 2.4 und höher festgelegt ist. Wenn die Validierung fehlschlägt, wird die Bereitstellung mit einer kritischen Fehlermeldung angehalten, die Fehlerbehebungen für das Problem vorschlägt. Siehe [Kritische Fehler, Bereitstellung](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![Neues Symbol](../../assets/new.svg) Es wurde eine Elasticsearch-Validierung hinzugefügt, um die Kompatibilität zwischen der Elasticsearch-Dienstversion und der Adobe Commerce-Version zu überprüfen.<!--MCLOUD-7193-->

- ![Neues Symbol](../../assets/new.svg) Die Fehlermeldung zur Elasticsearch-Kompatibilität wurde aktualisiert und zeigt jetzt die Versionen von Elasticsearch an, die mit dem Adobe Commerce-Elasticsearch-Modul kompatibel sind. Die Fehlermeldung enthält jetzt die spezifischen Elasticsearch-Versionen, die in Ihrer Cloud-Infrastruktur installiert werden sollen, damit sie mit dem von Ihrer Adobe Commerce-Elasticsearch-Version verwendeten -Modul kompatibel sind. Siehe [Warnungsfehler, Bereitstellung](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![Neues Symbol](../../assets/new.svg) Hinzugefügte Warnfehler `2026` und `2027` für ungültig `MAGE_MODE` Umgebungsvariableneinstellung. Der einzige gültige Wert ist `production`. Vor dieser Korrektur `MAGE_MODE` kann auf `developer` ohne Bereitstellungsfehler, um später nur Fehler zu verursachen, wenn versucht wird, in schreibgeschützte Dateien zu schreiben. Siehe [Warnfehler](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![Fixsymbol](../../assets/fix.svg) Die Validierung für Redis-, RabbitMQ- und MySQL-Dienste wurde korrigiert, um sicherzustellen, dass diese Versionen mit der Adobe Commerce-Version kompatibel sind. Gültige Versionen dieser Dienste werden jetzt in die `cloud.log`.<!--MCLOUD-7098-->

- ![Fixsymbol](../../assets/fix.svg) Die `cloud.log` , um das Limit für gleichzeitige Anfragen zum Senden von Anfragen während der Cache-Aufwärmung einzuschließen. Dieser Wert wird im [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) Variable nach der Bereitstellung.<!--MCLOUD-5563-->

**CLI-Befehlsaktualisierungen**—

- ![Neues Symbol](../../assets/new.svg) CLI-Befehle hinzugefügt (`cloud:config:create` und `cloud:config:update`), um die `.magento.env.yaml` -Datei mit einer Konfiguration, die eine oder mehrere Build-, Bereitstellungs- und Nachbereitungsvariablen enthalten kann. Siehe [Konfigurationsdatei über CLI erstellen](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Aktualisierungen der Umgebungsvariablen**—

- ![Neues Symbol](../../assets/new.svg) Der [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) Build-Variable. Festlegen der Variablen auf `true` verhindert, dass die Anwendung die `composer dump-autoload` -Befehl während einer Cloud Docker für Commerce-Installation. Die -Variable ist nur für Cloud Docker für Commerce-Container mit beschreibbaren Dateisystemen relevant (erstellt für Tests und Entwicklung mit `./vendor/bin/ece-docker build:compose --with-test`). Bei solchen Installationen überspringen Sie die `composer dump-autoload` -Befehl verhindert Fehler bei der Ausführung anderer Befehle, die versuchen, auf Dateien aus einem gelöschten `generated` Verzeichnis.<!--MCLOUD-6939-->

## v2002.1.2

Releasedatum: 5. August 2020

**Validierungs- und Protokollverbesserungen**—

- ![Neues Symbol](../../assets/new.svg) Der `schema.error.yaml` -Datei, die alle Fehler- und Warnbenachrichtigungen enthält, die während des Build-, Bereitstellungs- und Nachbereitungsprozesses auftreten können, sowie Vorschläge zur Behebung der Fehler. Die Informationen in dieser Datei sind auch im Abschnitt _Cloud-Handbuch für Commerce_. Siehe [Fehlermeldungsreferenz für Eece-Tools](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![Neues Symbol](../../assets/new.svg) Das Cloud-Fehlerprotokoll wurde geändert (`/var/log/cloud.error.log`) Einträge in das JSON-Format hinzu, um die programmgesteuerte Analyse des Protokolls zu erleichtern.<!--MCLOUD-5879-->

- ![Neues Symbol](../../assets/new.svg) Es wurden zusätzliche Fehlerprüfungen zum Erstellen, Bereitstellen und Bereitstellen der Verarbeitung nach der Bereitstellung sowie verbesserte vorhandene Prüfungen hinzugefügt:

   - Fehler-Code 2026 - Während der Build-Phase erzeugte Daten konnten nicht in den bereitgestellten Ordnern wiederhergestellt werden

   - Fehler-Code 3004 - Sicherungsdateien können nicht erstellt werden

   - Fehler-Code 102 - Zusätzliche Prüfungen für Probleme, die auftreten, wenn die `env.php` Datei nicht schreibbar <!--MCLOUD-6221-->

- ![Neues Symbol](../../assets/new.svg) Der **QUALITY_PATCH** Umgebungsvariable zum Angeben eines oder mehrerer Qualitäts-Patches, die während des Bereitstellungsprozesses angewendet werden sollen. Siehe [Erstellen von Variablen](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Veröffentlichungsdatum: 25. Juni 2020

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Infrastruktur**—

   - ![Neues Symbol](../../assets/new.svg) **Verbesserungen bei der Protokollierung**—Verbesserte Log-Tracking-Funktion durch Zuweisung von Ausstiegscodes zu kritischen Bereitstellungsfehlern und Offenlegung der Ausstiegscodes in Fehlernachrichten- und Protokollereignissen. Siehe [Fehlermeldungsreferenz für Eece-Tools](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![Neues Symbol](../../assets/new.svg) Der Prozess für Datenbank-Dumps wurde verbessert (`vendor/bin/ece-tools db-dump`) und aktualisierte Protokollmeldungen, um klarzustellen, dass der Datenbankabbildvorgang die Anwendung in den Wartungsmodus wechselt, Prozesse in der Verbraucherwarteschlange stoppt und Cron-Aufträge deaktiviert, bevor der Abbildmodus gestartet wird.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, um sicherzustellen, dass die Projekt-URL bei der Bereitstellung in Staging- und Produktionsumgebungen korrekt aktualisiert wird. Jetzt `ece-tools` verwendet die URL für die Route mit der `primary:true` -Attribut in der Routenkonfiguration des Projekts festgelegt. Siehe [Bereitstellen von Variablen](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![Fixsymbol](../../assets/fix.svg) Die `generate.xml` Build-Szenario-Workflow zum Anwenden von Patches. Patches müssen früher angewendet werden, um Adobe Commerce zu aktualisieren und alle Probleme zu beheben, die die `di:compile` und `module:refresh` Schritte zum Fehlschlagen.<!--MCLOUD-5941-->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem im Installationsprozess behoben, durch das fälschlicherweise die `Crypt key missing` Fehler. Die `crypt/key` -Wert wird während der Installation automatisch generiert.<!--MCLOUD-6120-->

- ![Neues Symbol](../../assets/new.svg) **Dienstaktualisierungen**—

   - ![Neues Symbol](../../assets/new.svg) Unterstützung für PHP 7.4 und MariaDB 10.4 hinzugefügt.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![Neues Symbol](../../assets/new.svg) Der **SCD_USE_BALER** -Variable, um das Baler-Modul für das JavaScript-Bundling während des Build-Prozesses der Cloud-Infrastruktur in Adobe Commerce zu aktivieren. Siehe Variablenbeschreibung im Abschnitt [Build-Variablen](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![Neues Symbol](../../assets/new.svg) Der **REDIS_BACKEND** Umgebungsvariable zum Konfigurieren des Redis-Backend-Modells für Redis-Cache für Adobe Commerce 2.3.5 oder höher. Siehe Variablenbeschreibung im Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![Neues Symbol](../../assets/new.svg) **CLI-Befehlsaktualisierungen**—

   - ![Neues Symbol](../../assets/new.svg) Die folgenden CLI-Befehle wurden mit einer Option für eine detailliertere Protokollierung aktualisiert:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Die Protokollierungsstufe für jeden Aufruf wird durch die Konfiguration der [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) in der `.magento.env.yaml` -Datei.<!--MCLOUD-3503-->

- ![Neues Symbol](../../assets/new.svg) **Verbesserungen bei der Validierung**—

   - ![Neues Symbol](../../assets/new.svg) **Kompatibilitätsprüfungen mit Elasticsearch 7.x**—Aktualisierung der Elasticsearch-Validierung für Elasticsearch 7.x-Softwarekompatibilitätsprüfungen.<!--MCLOUD-5542-->

   - ![Neues Symbol](../../assets/new.svg) **Aktualisierte Dienstversion- und EOL-Validierungsprüfungen**—Validierung aktualisiert, um installierte Dienstversionen anhand der Anforderungen von Adobe Commerce 2.4 zu überprüfen.<!--MCLOUD-6144-->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Validierungsproblem behoben, sodass die folgende Warnung nach der Bereitstellung nur angezeigt wird, wenn die `post-deploy` Die Hook-Konfiguration fehlt in der `.magento.app.yaml` Datei:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![Neues Symbol](../../assets/new.svg) **Validierung für Zend Framework-Abhängigkeiten hinzugefügt**—Die Komponentenabhängigkeit wurde für das Zend Framework überprüft, das zum Laminas-Projekt migriert wurde. Wenn die erforderlichen Abhängigkeiten fehlen, wird während des Build-Prozesses die folgende Fehlermeldung angezeigt.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Siehe [Überprüfen von Zend-Framework-Abhängigkeiten](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![Neues Symbol](../../assets/new.svg) **Validierung hinzugefügt für `env.php` Datei und Daten**—Es wurden Prüfungen für die `env.php` Datei und Daten während des Installations- und Aktualisierungsprozesses.<!--MCLOUD-5991-->

      - Wenn die Variable `env.php` -Datei fehlt in der Installation und die `crypt/key` Wert wird nicht im `.magento.app.yaml` -Datei, schlägt die Bereitstellung mit der folgenden Benachrichtigung fehl:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Wenn die Installation die Variable `env.php` oder die Konfiguration nur einen Cache-Typ enthält, die `cron:enable` Befehl wird während des Aktualisierungsprozesses ausgeführt, um die Datei mit allen `cache_types`. Die folgende Benachrichtigung wird dem Protokoll hinzugefügt:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Veröffentlichungsdatum: 6. Februar 2020

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Infrastruktur**—

   - ![Neues Symbol](../../assets/new.svg) **Separates Paket für Cloud Docker für Commerce hinzugefügt**—Entpacken Sie das Docker-Paket aus dem `ece-tools` -Paket, um die Codequalität zu erhalten und unabhängige Versionen bereitzustellen. Aktualisierungen und Fehlerbehebungen im Zusammenhang mit `ece-tools` werden über die [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub-Repository.<!--MAGECLOUD-2927-->

   - ![Neues Symbol](../../assets/new.svg) **Aktualisierte Patchfunktionen**—Die Patch-Funktion wurde vom ECE-Tools-Paket in ein separates Paket verschoben. [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) Paket. Während der Bereitstellung `ece-tools` verwendet das neue Paket, um Patches anzuwenden. Siehe [Versionshinweise zu Cloud-Patches](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![Neues Symbol](../../assets/new.svg) **Aktualisierte Composer-Abhängigkeiten**—Die `composer.json` -Datei für Adobe Commerce in Cloud-Infrastruktur mit einer Abhängigkeit für die `magento/magento-cloud-docker` Paket. Jetzt `ece-tools` enthält Abhängigkeiten für alle Pakete in der [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Diese Pakete werden bei der Installation oder Aktualisierung automatisch installiert und aktualisiert `ece-tools`.

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für szenario-basierte Bereitstellungen**—<!--MAGECLOUD-4101-->

   - ![Neues Symbol](../../assets/new.svg) Jetzt können Sie den Build, die Bereitstellung und die Nachbereitstellung von Prozessen mithilfe von XML-Konfigurationsdateien anpassen, um die Standardkonfiguration zu überschreiben oder anzupassen.

   - ![Neues Symbol](../../assets/new.svg) **Die `hooks` Konfiguration in`.magento.app.yaml`**—Wir haben die `hooks` Konfigurationsformat zur Unterstützung von szenariobasierten Bereitstellungen. Das alte Format aus früheren ECE-Tools-Versionen 2002.0.x wird weiterhin unterstützt. Sie müssen jedoch auf das neue Format aktualisieren, um die szenario-basierte Bereitstellungsfunktion zu verwenden. Siehe [Szenario-basierte Bereitstellungen](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Bevor Sie auf die ECE-Tools-Version 2002.1.0 aktualisieren, lesen Sie die [Abwärtskompatible Änderungen](backward-incompatible-changes.md) , um mehr über Änderungen zu erfahren, bei denen Sie möglicherweise Adobe Commerce bei der Konfiguration oder den Prozessen von Cloud-Infrastrukturprojekten aktualisieren müssen.

- ![Neues Symbol](../../assets/new.svg) **Dienstaktualisierungen**—

   - ![Neues Symbol](../../assets/new.svg) Unterstützung für PHP 7.3 hinzugefügt.<!--MAGECLOUD-4022-->

   - ![Neues Symbol](../../assets/new.svg) RabbitMQ 3.8 wird nun unterstützt.<!--MAGECLOUD-4674-->

   - ![Neues Symbol](../../assets/new.svg) Es wurde eine Validierung hinzugefügt, um installierte Dienstversionen mit dem Datum der Einstellung für die Einstellung der Unterstützung für jeden Dienst zu vergleichen. Jetzt erhalten Kunden eine Benachrichtigung, wenn eine Dienstversion innerhalb von drei Monaten nach dem Datum der Einstellung der Unterstützung verfügbar ist, und eine Warnung, wenn das Datum der Abschaffung in der Vergangenheit liegt.<!--MAGECLOUD-4076-->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem bei der Konfiguration von Elasticsearch behoben, um sicherzustellen, dass die richtigen Elasticsearch-Einstellungen in allen Umgebungen konfiguriert sind.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Siehe [Dienstversionen](../services/services-yaml.md#service-versions) für eine Liste der in Adobe Commerce in der Cloud-Infrastruktur verwendeten Dienste und deren Versionskompatibilität mit der Cloud-Vorlage.

- ![Neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![Neues Symbol](../../assets/new.svg) Erweiterung der Funktionalität der `WARM_UP_PAGES` Umgebungsvariable, um das Vorausfüllen des Caches für bestimmte Produktseiten zu unterstützen. Siehe erweiterte Definition in der [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages) Thema.<!--MAGECLOUD-4444-->

   - ![Neues Symbol](../../assets/new.svg) Der `ERROR_REPORT_DIR_NESTING_LEVEL` Umgebungsvariable zur Vereinfachung der Datenverwaltung in den Fehlerberichten `<magento_root>/var/report/` Verzeichnis. Siehe Variablenbeschreibung im Abschnitt [Build-Variablen](../environment/variables-build.md#error_report_dir_nesting_level) Thema.

   - ![Fixsymbol](../../assets/fix.svg) Entfernt die `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`, und `STATIC_CONTENT_SYMLINK` Umgebungsvariablen. Siehe [Abwärtskompatible Änderungen](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem im Elastic Suite-Konfigurationsprozess behoben, sodass die Standardkonfiguration bei der Konfiguration der `ELASTICSUITE_CONFIGURATION` Bereitstellungsvariable ohne die `_merge` -Option.<!--MAGECLOUD-4388-->

- ![Neues Symbol](../../assets/new.svg) **CLI-Befehlsaktualisierungen**—

   - ![Neues Symbol](../../assets/new.svg) **Neuer Cron-Befehl**- Sie können die Cron-Verarbeitung in Ihrer Adobe Commerce in der Cloud-Infrastruktur-Umgebung jetzt manuell verwalten, indem Sie `cron:disable` und `cron:enable` Befehle. Verwenden Sie den Befehl disable , um alle aktiven Cron-Prozesse anzuhalten und alle Cron-Aufträge zu deaktivieren. Verwenden Sie den Befehl &quot;Aktivieren&quot;, um Cron-Aufträge erneut zu aktivieren, wenn Sie bereit sind. Siehe [Deaktivieren von Cron-Aufträgen](../application/crons-property.md#disable-cron-jobs).

   - ![Neues Symbol](../../assets/new.svg) **Verbesserte Fehlerberichterstellung**—Es wurde eine bessere Protokollierung für CLI-Befehlsfehler hinzugefügt, die während der Verarbeitung der ECE-Tools auftreten.<!--MAGECLOUD-4849-->

   - ![Neues Symbol](../../assets/new.svg) **Entfernen veralteter Build-Befehle**— Die folgenden Build-Befehle wurden entfernt: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`und umbenannt `ece-tools docker` Befehle zu `ece-docker`. Siehe [Abwärtskompatible Änderungen](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![Neues Symbol](../../assets/new.svg) Entfernt veraltete `build_options.ini` und eine Validierung hinzugefügt, um den Build fehlschlagen zu lassen, wenn die Datei vorhanden ist. Verwenden Sie die [.magento.env.yaml](../environment/configure-env-yaml.md) -Datei, um Build-Optionen zu konfigurieren.

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass der Build-Prozess fehlschlug, wenn die Variable `config.php` ist leer.<!--MAGECLOUD-4127-->

## 2002.0.23

Veröffentlichungsdatum: 27. Februar 2020

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Kompatibilitätsproblem mit `ece-tools` Versionen von 2002.0.x, die verhinderten, dass die On-Demand-Erstellung von statischen Inhalten im Produktionsmodus erfolgreich abgeschlossen wurde.

## Ältere Versionen

Siehe [Versionshinweise-Archiv](cloud-release-archive.md) für Version 2002.0.22 und früher.
