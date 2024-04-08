---
title: Cloud Docker-Paket
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud Docker-Pakets an.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: bc76cba0219f16fd055c20289811b51c35c9b026
workflow-type: tm+mt
source-wordcount: '3662'
ht-degree: 0%

---

# Cloud Docker-Paket

Die [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) bietet Funktionen und Docker-Bilder zum Bereitstellen von Adobe Commerce in einer lokalen Cloud-Umgebung. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben, das eine Komponente von [Cloud Tools Suite für Commerce](cloud-tools-suite.md).

Die `magento/magento-cloud-docker` -Paket verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![Neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v1.3.7 {#latest}

Veröffentlichungsdatum: 8. April 2024

- ![Neues Symbol](../../assets/new.svg) **PHP** — Zusätzliche Unterstützung für PHP 8.3- und PHP 8.3-Bilder.
- ![Neues Symbol](../../assets/new.svg) **Nginx** — Bild Nginx v. 1.24 hinzugefügt.
- ![Neues Symbol](../../assets/new.svg) **OpenSearch** - Bild OpenSearch v. 2.12, 1.3 hinzugefügt.
- ![Neues Symbol](../../assets/new.svg) **Verfasser** - Aktualisierung der Composer-Version auf 2.2.23.

## v1.3.6

Veröffentlichungsdatum: 31. Juli 2023

- ![Neues Symbol](../../assets/new.svg) **Neue Dienstversion hinzugefügt**—OpenSearch 2.5.
- ![Neues Symbol](../../assets/new.svg) **Composer-Cache aktivieren**—Jetzt können Sie die Docker-Konfiguration erweitern, um den leeren Cache-Speicher von Composer beim Starten des Docker-Containers zu aktivieren. Siehe [Erweitern der Docker-Konfiguration](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) im _Cloud Docker für Commerce_ Handbuch.

## v1.3.5

Veröffentlichungsdatum: 10. März 2023

- ![Neues Symbol](../../assets/new.svg) **ionCube**—Die ionCube-Erweiterung für das PHP 8.1-Bild wurde hinzugefügt.
- ![Neues Symbol](../../assets/new.svg) **Neue Dienstversionen hinzugefügt**—OpenSearch 2.3 und 2.4, PHP 8.2, Varnish 7.1.1.
- ![Neues Symbol](../../assets/new.svg) **Erweiterte Unterstützung für PHP 8.2**—Es wurden Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen behoben, um Commerce 2.4.6 zu unterstützen.
- ![Fixsymbol](../../assets/fix.svg) **Problem mit dem Verfasser**—Es wurden Probleme behoben, die nach der Aktualisierung der Composer-Version in den Docker-Containern auftraten.

## v1.3.4

Veröffentlichungsdatum: 27. Oktober 2022

- ![Neues Symbol](../../assets/new.svg) **Neue Varnish-Bilder hinzugefügt**—Es wurden Bilder für Varnish 6.5, 7.0 und 7.1 hinzugefügt.<!-- MCLOUD-7879 -->

## v1.3.3

Veröffentlichungsdatum: 13. September 2022

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für Apple M1 (ARM64)**—Es wurden Änderungen an Docker-Bildern hinzugefügt, um die Unterstützung für die Apple M1 (ARM64)-Architektur zu ermöglichen.<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![Fixsymbol](../../assets/fix.svg) **Mailhog**—Es wurde ein Problem behoben, bei dem der Mailhog-Dienst im Entwicklermodus keine E-Mails erfasste.<!-- MCLOUD-8643 -->
- ![Fixsymbol](../../assets/fix.svg) **init-docker.sh**—Der Validator für Dienstversionen im `init-docker.sh` Skript.<!-- MCLOUD-8765 -->

## v1.3.2

Veröffentlichungsdatum: 31. März 2022

- ![Neues Symbol](../../assets/new.svg) **Elasticsearch 7.10-Bild hinzugefügt**<!-- MCLOUD-8548 -->

## v1.3.1

Veröffentlichungsdatum: 10. März 2022

- ![Neues Symbol](../../assets/new.svg) **Unterstützung von PHP 8.1**—Hinzugefügte Unterstützung für PHP 8.1.
- ![Neues Symbol](../../assets/new.svg) **OpenSearch**—Bilder der OpenSearch-Versionen 1.1 und 1.2 hinzugefügt.
- ![Neues Symbol](../../assets/new.svg) **Verfasser 2.1**—Setzen Sie Composer 2.1.x standardmäßig in PHP 8.x-Bildern.
- ![Neues Symbol](../../assets/new.svg) **Verbesserungen bei PHP-Bildern**—

   - PHP 8.1-Bilder hinzugefügt
   - Aktualisierte xDebug-Version 3.1.2
   - Aktualisiertes xmlrpc 1.0.0RC3

- ![Fixsymbol](../../assets/fix.svg) **Verbesserungen bei Elasticsearch und OpenSearch**—Verbesserungen in Elasticsearch und OpenSearch Docker-Dateien; Elasticsearch 5.2 wurde entfernt.
- ![Fixsymbol](../../assets/fix.svg) **Natriumerweiterung**—Aktiviert die `sodium` -Erweiterung standardmäßig in allen PHP-Bildern.
- ![Fixsymbol](../../assets/fix.svg) **Composer-Cache-Volumen**—Pfad für Composer-Cache-Volumen behoben, um zwischengespeicherte Composer-Pakete zu erhalten.
- ![Fixsymbol](../../assets/fix.svg) **Speicherbegrenzung in nginx**—Speicherbegrenzung im NGINX-Bild korrigiert.

## v1.3.0

Veröffentlichungsdatum: 25. Oktober 2021

- ![Fixsymbol](../../assets/fix.svg) **Verbessern des Arbeitsablaufs im Entwicklermodus**—Zuvor mussten Sie den Modus in den Build- und Bereitstellungsschritten angeben. Nun, die `--mode` in der `build` bestimmt den Modus im späteren Schritt `deploy` Schritt. Es ist nicht mehr erforderlich, den Modus nach der Bereitstellung festzulegen. Siehe [Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![Fixsymbol](../../assets/fix.svg) **Verbesserungen für schreibgeschütztes Dateisystem**—<!-- ACMP-1106 -->
   - Fehlerkorrektur - Ein PHP-Container für die E-Mail-Konfiguration kann jetzt gestartet werden.
   - Kann Umgebungsvariablen in INI-Dateien verwenden.
   - Stellen Sie sicher, dass PHP-Einstiegspunkte keine Schreibberechtigung benötigen.
- ![Fixsymbol](../../assets/fix.svg) **Knoten aktualisieren**—Aktualisieren Sie die gebündelte Knotenversion. Bei der Installation von Node in PHP-CLI-Bildern wird nun die aktuelle LTS-Version verwendet.<!-- ACMP-1539 -->
- ![Fixsymbol](../../assets/fix.svg) **Symfony aktualisieren**—Aktualisierung der Symfony-Konfigurationsabhängigkeiten auf die Kompatibilität mit Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Veröffentlichungsdatum: 29. Juli 2021

- ![Neues Symbol](../../assets/new.svg) **Neu `Zookeeper` container**—Hinzufügung einer [Zookeeper-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) zum Verwalten der Konfiguration des Sperranbieters für Projekte, die nicht in der Cloud-Infrastruktur in Adobe Commerce bereitgestellt werden.<!--MCLOUD-8000-->

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für Composer 2.0 hinzugefügt.**—Composer-Version 2.0 wurde zur Konfigurationsdatei des Composers hinzugefügt, um Aktualisierungen von Composer 1.0 zu unterstützen, die kurz vor dem Ende des Lebenszyklus stehen.<!--MCLOUD-8003-->

## v1.2.3

Veröffentlichungsdatum: 14. Juni 2021

- ![Neues Symbol](../../assets/new.svg) **PHP 8.0 wurde hinzugefügt**—PHP wurde auf Version 8.0 aktualisiert, sodass Sie alle neuen Funktionen und Optimierungen nutzen können, die PHP 8.0 beinhaltet.<!--MCLOUD-7941-->
- ![Neues Symbol](../../assets/new.svg) **Aktualisiert auf Version 6.6 und Elasticsearch 7.11.2**—Die folgenden Links bieten Versionsinformationen zu [Varnish Cache 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) und Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![Neues Symbol](../../assets/new.svg) **hinzugefügt `ioncube` Erweiterung für PHP 7.4 image**—Die `ioncube` -Erweiterung wurde zum PHP 7.4-Image neu hinzugefügt, nachdem sie ursprünglich aus dem PHP 7.3 auf PHP 7.4 Upgrade ausgeschlossen worden war. *[Gesendet von mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![Neues Symbol](../../assets/new.svg) **Eine Dateisynchronisierungsoption wurde hinzugefügt:`manual-native`**—Die `manual-native` Die Dateisynchronisierungsoption bietet eine manuelle Kontrolle über die Synchronisierung, die die beste Leistung für macOS- und Windows-Umgebungen bietet. Erfahren Sie mehr über die Verwendung der `manual-native` -Option in [Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) und [Synchronisieren von Daten in einer Docker-Entwicklungsumgebung](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![Neues Symbol](../../assets/new.svg) **Entfernte Volumenlöschungen aus `up` und `down` commands**—Die `--volume` wurde aus der `bin/magento-docker up` und `bin/magento-docker down` durch die neuen `bin/magento-docker init` -Befehl mit einer Datenverlustwarnung. Durch diese Änderung wird ein versehentlicher Datenverlust verhindert. *[Gesendet von joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![Fixsymbol](../../assets/fix.svg) **Aktualisiert `CN` Wert für das generierte Zertifikat**—Die hartcodierte `CN` -Wert aus der Dockerfile. Mit diesem Wert wurde ein Zertifikatfehler (`NET::ERR_CERT_INVALID`), die die `--host` -Option für `ece-docker build:compose` zu ignorieren.<!--MCLOUD-7934-->

## v1.2.2

Veröffentlichungsdatum: 20. April 2021

- ![Neues Symbol](../../assets/new.svg) **Aktualisiert `host.docker.internal` plattformunabhängig**—Sie können jetzt denselben Docker erstellen Erstellen Sie Skripte für Ubuntu, Windows und macOS. Die Verwendung von Xdebug in Ubuntu erfordert keine separate Umgebungsvariable mehr. [Fehlerbehebung von Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![Neues Symbol](../../assets/new.svg) **init-docker.sh aktualisiert**—Die `mounts` -Objekt `MAGENTO_CLOUD_APPLICATION` Umgebungsvariable. [Fehlerbehebung von Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![Neues Symbol](../../assets/new.svg) **init-docker.sh aktualisiert**—Die `init-docker.sh` Skript mit PHP 7.4 und Cloud Docker 1.2.1 Versionen. [Fehlerbehebung von Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![Neues Symbol](../../assets/new.svg) **Standardmäßig aktiviertes Natrium**—Aktiviert die `sodium` PHP-Erweiterung standardmäßig in PHP Docker-Images.<!--MCLOUD-7548-->
- ![Neues Symbol](../../assets/new.svg) **`custom-registry`option**—Hinzufügung einer `--custom-registry` -Option `php ./vendor/bin/ece-docker build:compose` -Befehl zur Verwendung Ihrer eigenen Bildregistrierung.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![Neues Symbol](../../assets/new.svg) **Alte Elasticsearch-Versionen entfernt**—Die Elasticsearch-Versionen 1.7 und 2.4 wurden aus den Elasticsearch-Bildern entfernt.<!--MCLOUD-7504-->
- ![Neues Symbol](../../assets/new.svg) **Automatische Generierung von NGINX-Zertifikaten**—Die vorhandenen Zertifikate wurden aus dem NGINX-Bild entfernt. Die NGINX-Zertifikate werden jetzt mit jeder neuen Implementierung automatisch generiert, um die Sicherheit zu verbessern.<!--MCLOUD-7396-->
- ![Fixsymbol](../../assets/fix.svg) **Aktiviert`opcache.validate_timestamps`**—Aktiviert die `opcache.validate_timestamps` PHP-Einstellung standardmäßig im Entwicklermodus. Durch Aktivierung dieser Einstellung wurde das Problem behoben, dass Änderungen am Dateisystem in Docker nicht erkannt wurden.<!--MCLOUD-7466-->
- ![Fixsymbol](../../assets/fix.svg) **Fest`build:custom:compose`**—Korrektur der `build:custom:compose` -Befehl, um einen Fehler auszulösen, wenn Dateien während des Build-Prozesses nicht überschrieben werden können. Das Ausgeben eines Fehlers verhindert Situationen, in denen `docker-compose up` verwendet möglicherweise die falschen Dateien.<!--MCLOUD-7457-->
- ![Fixsymbol](../../assets/fix.svg) **Fest `--sync_engine="native"` option**—Es wurde ein Problem behoben, bei dem im Produktionsmodus (`--mode="production"`), die `--sync_engine="native"` -Option keine Einträge für lokale Ordner in der `docker.composer.yml` -Datei.<!--MCLOUD-7254-->
- ![Fixsymbol](../../assets/fix.svg) **Fehler bei der Überprüfung der Dienstversion behoben**—Dienstversionen für hinzugefügt [!DNL RabbitMQ], Elasticsearch und andere Dienste für die `type` -Eigenschaft in der `MAGENTO_CLOUD_RELATIONSHIP` -Variable. Hinzufügen dieser Versionen zum `relationships` Korrektur der Validierungsfehler, die während der Bereitstellungsphase aufgetreten sind.<!--MCLOUD-7572-->

## v1.2.1

Veröffentlichungsdatum: 21. Dezember 2020

- ![Neues Symbol](../../assets/new.svg) **NGINX-Befehlsoptionen**—Hinzufügung von Build-Befehlsoptionen zur Änderung der Anzahl von NGINX `worker_processes` und NGINX `worker_connections` für TLS und Webdienste. Die `worker_process` Der Parameter behält die Möglichkeit, den Wert auf `auto`. Beispiele: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![Neues Symbol](../../assets/new.svg) **TLS-Befehlsoption**—Es wurde eine Befehlsoption zum Erstellen einer Konfiguration ohne den TLS-Dienst hinzugefügt. Beispiel: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![Neues Symbol](../../assets/new.svg) **NGINX-Speicherverbrauch**—Verringerter Speicher, der vom NGINX-Prozess für TLS und Webdienste benötigt wird.<!--MCLOUD-7259-->

- ![Neues Symbol](../../assets/new.svg) **Blackfire**—Blackfire PHP-Erweiterung standardmäßig im Cloud Docker-Bild deaktiviert.

- ![Fixsymbol](../../assets/fix.svg) **PHP-FPM-Container**—Korrektur der Konsistenzprüfung des PHP-FPM-Containers durch Ändern der `WEB_PORT` von `80` nach `8080`.<!--MCLOUD-7232-->

- ![Fixsymbol](../../assets/fix.svg) **Ungültige Volumenbenennung**—Fehlerkorrektur - im Entwicklermodus tritt kein Fehler mehr mit ungültiger Volumenbenennung auf.<!--MCLOUD-7442-->

- ![Fixsymbol](../../assets/fix.svg) **NGINX Upstream Port**—Das Docker NGINX 1.19-Bild wurde aktualisiert, um Port 8080 zu verwenden, um eine Endlosschleife zu vermeiden. [Fehlerbehebung von Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Veröffentlichungsdatum: 9. November 2020

- ![Neues Symbol](../../assets/new.svg) **Container-Aktualisierungen -**

   - ![Neues Symbol](../../assets/new.svg) **PHP-FPM-Container**—Unterstützung für die GNupg PHP-Erweiterung hinzugefügt. [Fehlerbehebung von G Arvind von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![Fixsymbol](../../assets/fix.svg) **Datenbankcontainer**—Die Konsistenzprüfung des Datenbankcontainers wurde korrigiert, indem das erforderliche Datenbankkennwort zum Befehl zur Konsistenzprüfung hinzugefügt wurde.<!--MCLOUD-7122-->

   - ![Neues Symbol](../../assets/new.svg) **Elasticsearch-Container**

      - Unterstützung für Elasticsearch 7.9 zur Kompatibilität mit kommenden Adobe Commerce-Versionen hinzugefügt.<!--MCLOUD-7190-->

      - **Elasticsearch-Plug-in-Konfiguration**—Es wurde Unterstützung für die Verwendung der Konfigurationsinformationen des Elasticsearch-Plug-ins aus dem `services.yaml` -Datei, die erstellt werden soll `docker-compose.yaml` -Datei für eine Cloud Docker für Commerce-Umgebung. Siehe [Elasticsearch-Plugins](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Elasticsearch-Plug-in-Unterstützung**—Unterstützung für die folgenden Elasticsearch-Plug-ins hinzugefügt: `analysis-icu`, `analysis-phonetic`, `analysis-stempel`, und `analysis-nori`. Die `analysis-icu` und `analysis-phonetic` -Plug-ins sind standardmäßig installiert. Sie können die `analysis-stempel` und `analysis-nori` Plug-ins nach Bedarf.<!--MCLOUD-2789-->

   - ![Neues Symbol](../../assets/new.svg) **CLI-Container**

      - **Ausführen von Befehlen in Docker-PHP-Containern**—Jetzt können Sie die Cloud Docker-CLI verwenden, um Befehle in PHP-Containern in Ihrer Docker-Umgebung auszuführen, ohne PHP auf dem Host installieren zu müssen. Beispielsweise erstellt der folgende Befehl die Konfiguration:  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Siehe [Cloud Docker-CLI](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Fehlerbehebung von G Arvind von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - Der OpenSSH-Client wurde zu PHP CLI-Containern hinzugefügt. Jetzt können Sie die SSH-Agent-Weiterleitung für Composer verwenden, wenn die `composer.json` -Datei enthält private Git-Repositorys, für die ein SSH-Client Composer-Befehle verwenden muss.<!--MCLOUD-6008-->

   - ![Fixsymbol](../../assets/fix.svg) **TLS-Container**—Nun, die [TLS-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) basiert auf der `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Docker-Bild anstelle des CentOS-Bildes. Durch diese Änderung werden Probleme behoben, die beim Senden von HTTPS-Anforderungen zwischen Containern in der Cloud Docker-Umgebung zu Fehlern führten.<!--MCLOUD-6469-->

   - ![Neues Symbol](../../assets/new.svg) **Testcontainer**—Es wurde ein Testcontainer für Anwendungstests hinzugefügt und der `--with-test` Option zum Docker `build:compose` -Befehl, um den Container nur beim Testen in der Docker-Umgebung zu erstellen. Siehe [Anwendungstests](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![Neues Symbol](../../assets/new.svg) **FPM-XDEBUG-Container**

      - ![Neues Symbol](../../assets/new.svg) **Konfigurieren von Xdebug unter Linux**—Die `--set-docker-host` -Option `ece-docker build:compose` -Befehl zum Konfigurieren der `host.docker.internal` -Wert im Xdebug -Container. Diese Option ist erforderlich, um Xdebug auf Linux-Systemen zu verwenden. Siehe [Xdebug für Docker konfigurieren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![Fixsymbol](../../assets/fix.svg) Die Xdebug-Variablenkonfiguration für den Docker-ENTRYPOINT wurde korrigiert, um `uninitialized "with_xdebug" variable` Fehler in den Protokollen. [Fehlerbehebung von Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![Neues Symbol](../../assets/new.svg) **Docker-Konfigurationsänderungen**

   - **MailHog-Konfiguration**—Jetzt können Sie Folgendes verwenden: `ece-docker build:compose` Befehlsoptionen zum Deaktivieren von MailHog und Angeben von Ports: `--no-mailhog`, `--mailhog-http-port`, und `--mailhog-smtp-port`. Siehe [E-Mail einrichten](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Für Cloud Docker für Commerce 1.2.0 und höher stellt Adobe jetzt Docker-Bilder für jede Patch-Version bereit. Der Docker-Konfigurationsgenerator erstellt die Docker-Konfiguration mit einer angegebenen Patch-Version, anstatt die neueste Version zu verwenden. Zuvor erstellte der Docker-Konfigurationsgenerator die Konfiguration mit der neuesten Patch-Version, die Cloud Docker für Commerce-Umgebungen beschädigte, die mit einer früheren Version erstellt wurden.<!--MCLOUD-7093-->

   - **Festlegen benutzerdefinierter Bilder und Versionen in der benutzerdefinierten Cloud Docker-Konfiguration**—Die `build:custom:compose` -Befehl mit Optionen zum Angeben benutzerdefinierter Bilder und Versionen beim Generieren einer benutzerdefinierten Docker-Komprimierungskonfigurationsdatei (`docker-compose.yaml`). Siehe [Erstellen einer benutzerdefinierten Docker Composer-Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Aktualisierung der Docker-Host-Konfiguration, um Port 443 anzuzeigen und den Zugriff auf Adobe Commerce zu ermöglichen (`https://magento2.docker`) von allen CLI-Containern aus. Sie können den Standardanschluss ändern, indem Sie die `--tls-port` -Option, wenn Sie die Docker-Konfigurationsdatei generieren.<!--MCLOUD-6806-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass der Cloud Docker für Commerce-Build fehlschlug, wenn die Variable `app/etc/env.php` vorhanden ist.<!--MCLOUD-6732-->

- ![Fixsymbol](../../assets/fix.svg) Die Build-Konfiguration wurde aktualisiert, um benannte Volumes durch normale Volumes zu ersetzen, um Probleme bei der Bereitstellung von Cloud Docker für Commerce unter Linux oder Windows Subsystem für Linux (WSL2) zu vermeiden.<!--MCLOUD-6732-->

- ![Fixsymbol](../../assets/fix.svg) Die Funktionstests für Cloud Docker für Commerce wurden aktualisiert und unterstützen jetzt Composer 2.0.<!--MCLOUD-7183-->

## v1.1.2

Veröffentlichungsdatum: 9. September 2020

- ![Neues Symbol](../../assets/new.svg) Unterstützung für Elasticsearch 7.7 hinzugefügt<!--MCLOUD-6219-->

## v1.1.1

Releasedatum: 5. August 2020

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte E-Mail-Konfiguration**—Die standardmäßige Cloud Docker für Commerce-Konfiguration wurde aktualisiert, um den MailHog-Dienst anstelle von SendMail zu unterstützen. Siehe [E-Mail einrichten](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![Fixsymbol](../../assets/fix.svg) PS-Bibliothek in Cloud Docker-Umgebungskonfiguration wiederhergestellt, um sie zu beheben `ps:  command not found` Fehler.<!--MCLOUD-6621-->

- ![Fixsymbol](../../assets/fix.svg) Aktualisierung der standardmäßigen Cloud Docker für Commerce-Konfiguration, um die automatische Bereitstellung der Datenbankeinstiegspunkte und MariaDB-Volumes zu entfernen und `Cannot create container for service db` Fehler, die beim Starten Ihrer Cloud Docker-Umgebung auftreten können.

  Jetzt können Sie die Cloud Docker-Umgebung konfigurieren, um die Datenbankverzeichnisse bereitzustellen, indem Sie die folgenden Optionen zum `ece-docker build:compose` command: `--with-entry-point` und `with-mariadb-conf`. Siehe [Dienstkonfigurationsoptionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![Neues Symbol](../../assets/new.svg) **CLI-Befehlsaktualisierungen**

| Aktion | Befehl |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Fügen Sie einen Einstiegspunkt zum Datenbankcontainer hinzu, um die Datenbank aus der Sicherung wiederherzustellen. | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| MariaDB-Konfigurationsvolumen hinzufügen | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Veröffentlichungsdatum: 25. Juni 2020

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für die Lösung zur geteilten Datenbankleistung hinzugefügt**- Jetzt können Sie einen Store mithilfe der Lösung Split database performance in der Cloud Docker-Umgebung konfigurieren und bereitstellen.<!--MCLOUD-3740-->

- ![Neues Symbol](../../assets/new.svg) **Unterstützung für Adobe Commerce- und Magento Open Source-Bereitstellung**—Jetzt können Sie Cloud Docker für Commerce verwenden, um eine lokale Entwicklungsumgebung für Projekte bereitzustellen, die nicht in Adobe Commerce auf Cloud-Infrastruktur gehostet werden.<!--MCLOUD-5667-->

- ![Neues Symbol](../../assets/new.svg) **Blackfire.io-Unterstützung**—Unterstützung für die Verwendung der [Blackfire.io-Erweiterung](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) für automatisierte Leistungstests. [Fehlerbehebung von Adarsh Manickam von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![Neues Symbol](../../assets/new.svg) **Container-Aktualisierungen**

   - **Varnisch**—Jetzt ist &quot;Varnish&quot;der Standardcache, wenn Sie Adobe Commerce in einer Cloud Docker-Umgebung mit einer unterstützten Version der Cloud-Anwendungsvorlage bereitstellen. Siehe [Varkontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Der `--no-varnish` Option zum Überspringen der Varnish-Dienstinstallation beim Generieren der Cloud Docker-Konfigurationsdatei.<!--MCLOUD-2634-->

   - ![Neues Symbol](../../assets/new.svg) **Datenbank**

      - Unterstützung für die MySQL-Datenbank hinzugefügt. Jetzt können Sie die Cloud Docker-Umgebung mit MariaDB oder MySQL konfigurieren. Siehe [Dienstkonfigurationsoptionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Es wurde die Möglichkeit hinzugefügt, die Inkrement- und Offset-Einstellungen für die Datenbankreplikation festzulegen, wenn Sie die Docker-Komprimierungsdatei generieren. Siehe [Dienstcontainer](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![Neues Symbol](../../assets/new.svg) **PHP-FPM**

      - Unterstützung für PHP 7.4 hinzugefügt. [Fehlerbehebung von Mohanela Murugan von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Möglichkeit zum Kopieren einer `php.ini` im Stammverzeichnis des Projekts in die Cloud Docker-Umgebung und wenden benutzerdefinierte PHP-Einstellungen auf die PHP-FPM- und CLI-Container an. Siehe [PHP-Einstellungen anpassen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Es wurde eine Konsistenzprüfung für Container hinzugefügt. [Fehlerbehebung von Visanth Sampath von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![Fixsymbol](../../assets/fix.svg) **Node.js**—Aktualisierung der standardmäßigen Node.js-Version von Version 8 auf Version 10, um die Sicherheit zu verbessern. Node.js Version 8 ist veraltet und nicht mehr mit Fehlerbehebungen oder Sicherheits-Patches aktualisiert. [Fehlerbehebung von Mohan Elamurugan von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![Neues Symbol](../../assets/new.svg) **Elasticsearch**

      - Unterstützung für Elasticsearch 6.8, 7.2, 7.5 und 7.6 hinzugefügt.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Es wurde die Möglichkeit hinzugefügt, die [Konfiguration des Elasticsearch-Containers](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) wenn Sie die Docker-Komprimierungskonfigurationsdatei generieren.<!--MCLOUD-3059-->

      - Der `--no-es` -Option zu den Dienstkonfigurationsoptionen zum Generieren der Konfigurationsdatei Docker erstellen . Verwenden Sie diese Option, um die Installation des Elasticsearch-Containers zu überspringen und stattdessen die MySQL-Suche zu verwenden. Diese Option wird nur für Adobe Commerce-Versionen 2.3.5 und frühere Versionen unterstützt.<!--MCLOUD-3766-->

   - ![Neues Symbol](../../assets/new.svg) **FPM-XDEBUG-Container**—Es wurde eine Dienstkonfigurationsoption hinzugefügt, um Xdebug zum Debuggen von PHP in Ihrer Cloud Docker-Umgebung zu installieren und zu konfigurieren. Siehe [Xdebug konfigurieren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![Neues Symbol](../../assets/new.svg) **Docker-Konfigurationsänderungen**

   - Es wurden Konsistenzprüfungen für die Dienstcontainer PHP-FPM, Redis, Elasticsearch und MySQL Docker hinzugefügt.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Der standardmäßige Dateisynchronisierungsmodus wurde in `native` im Entwicklermodus.<!--MCLOUD-3890 -->

   - Versionsinformationen zum generischen Docker-Dienst-Container-Bild beim Generieren der `docker-compose.yml` -Datei.<!--MCLOUD-3878-->

   - Verbesserte Fähigkeit, große Antworten aus dem Upstream PHP-FPM Container zu verarbeiten, indem die `fastcgi_buffers` -Wert für den Nginx-Server.<!--MCLOUD-5980-->

   - Verbesserte Leistung bei der Synchronisierung von Mutagen-Dateien durch Hinzufügen einer zweiten Synchronisierungssitzung zur Synchronisierung von Dateien im `vendor` Verzeichnis. Diese Änderung verhindert, dass Mutagen während der Dateisynchronisierung feststecken bleibt. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![Neues Symbol](../../assets/new.svg) **CLI-Befehlsaktualisierungen**

| Aktion | Befehl |
| -------- | --------------- |
| Rediv-Cache löschen | `bin/magento-docker flush-redis` |
| Varnish-Cache löschen | `bin/magento-docker flush-varnish` |
| Überspringen der standardmäßigen Varnish-Installation | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Elasticsearch-Optionen anpassen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [Elasticsearch-Konfiguration entfernen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| Konfigurieren des DB-Containers mit MySQL-Version 5.6 oder 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Festlegen der benutzerdefinierten Basis-URL | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Container für die Xdebug-Konfiguration hinzufügen](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - Die Synchronisation von Mutagen-Dateien wird nun problemlos durchgeführt, um zu verhindern, dass Mutagen veraltete Sitzungen erstellt. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Konfigurationsproblem behoben, das beim Starten des PHP-FPM-Containers Syntaxfehler im Docker-Komprimierungsprotokoll verursachte. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![Fixsymbol](../../assets/fix.svg) Fehlerkorrektur - bei der Verwendung mehrerer Docker-Umgebungen treten keine Volumenkonfliktfehler mehr auf. [Fehlerbehebung von G Arvind von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/168).

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Fehler behoben, der dazu führte, dass `ece-docker build:compose` -Befehl fehlschlagen, wenn die Konfiguration Blackfire.io enthielt. [Fehlerbehebung von G Arvind von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![Fixsymbol](../../assets/fix.svg) Die PHP-CLI-Bildkonfiguration wurde aktualisiert, um speicherinterne Fehler zu vermeiden, die bei der Installation mehrerer Pakete mit Cloud Docker for Commerce aufgetreten sind. [Fehlerbehebung von Mohan Elamurugan von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![Fixsymbol](../../assets/fix.svg) Unterstützung für mehrere MySQL-Benutzer in der Cloud Docker-Umgebung hinzugefügt. In früheren Versionen wurde die `build:compose` -Vorgang fehlgeschlagen ist, wenn `magento.app.yaml` -Datei, die mehrere Datenbankbenutzer angegeben hat. [Fehlerbehebung von G Arvind von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![Fixsymbol](../../assets/fix.svg) Entfernt `rsyslog` aus dem Cloud Docker für Commerce-PHP-Container , um Kompatibilitätsprobleme zu beheben, die Warnhinweise während der Implementierung verursacht haben. Cloud Docker verwendet nicht das Dienstprogramm rsyslog .<!--MCLOUD-6173-->

## v1.0.0

Veröffentlichungsdatum: 5. Februar 2020

- ![Neues Symbol](../../assets/new.svg) **Erstellen eines separaten Pakets zur Bereitstellung`Cloud Docker for Commerce`**—Der Quellcode wurde verschoben, um Cloud Docker für Commerce aus der bereitzustellen. `ece-tools` Repository in [new `magento-cloud-docker` Repository](https://github.com/magento/magento-cloud-docker) um die Codequalität zu erhalten und unabhängige Versionen bereitzustellen. Das neue Paket ist eine Abhängigkeit von ECE-Tools v2002.1.0 und höher.

  Wenn Sie die Eece-Tools aktualisieren, aktualisieren Sie auch die `magento/magento-cloud-docker` auf Version 1.0.0. Wenn Sie Cloud Docker für Commerce mit einer früheren `ece-tools` -Version (2002.0.x), überprüfen Sie die [Abwärtskompatibilitäten](backward-incompatible-changes.md) und aktualisieren Sie Ihr Projekt nach Bedarf als Skripte, Befehle und Prozesse.

- ![Neues Symbol](../../assets/new.svg) **Neue Versionierung für die Docker-Bilder**- Sie müssen jetzt die `magento/magento-cloud-docker` -Paket, um die aktualisierten Bilder zu erhalten.<!--MAGECLOUD-4737-->

- ![Neues Symbol](../../assets/new.svg) **Container-Aktualisierungen**—

   - ![Neues Symbol](../../assets/new.svg) **PHP-FPM-Container**—

      - ![Neues Symbol](../../assets/new.svg) **Node.js-Unterstützung hinzugefügt**—Das PHP-FPM-Image wurde aktualisiert, um die Funktionen node, npm und grunt-cli im PHP-Container zu unterstützen.<!--MAGECLOUD-3953-->

      - ![Neues Symbol](../../assets/new.svg) **Hinzugefügte Unterstützung für [ionCube](https://www.ioncube.com/)**—Die standardmäßige Docker-Konfiguration wurde aktualisiert, um ionCube in der lokalen Docker-Entwicklungsumgebung zu unterstützen.<!--MAGECLOUD-4354-->

   - ![Neues Symbol](../../assets/new.svg) **Webcontainer**—

      - ![Neues Symbol](../../assets/new.svg) **Konfigurieren von NGINX**—Die Funktion zum Bereitstellen eines benutzerdefinierten `nginx.conf` in die Cloud Docker für Commerce-Umgebung. Siehe [Webcontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![Neues Symbol](../../assets/new.svg) **Automatisch generierte NGINX-Zertifikate**—Die Docker-Konfigurationsdatei enthält jetzt die Konfiguration zum automatischen Generieren von NGINX-Zertifikaten für den Webcontainer.<!--MAGECLOUD-4258-->

   - ![Neues Symbol](../../assets/new.svg) **Neuer Selenium-Container**—Hinzufügung einer [Selenium-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) , um Adobe Commerce-Anwendungstests mithilfe des Magento Functional Testing Framework (MFTF) zu unterstützen.<!--MAGECLOUD-4040-->

   - ![Neues Symbol](../../assets/new.svg) **[!DNL RabbitMQ]Versionsunterstützung**—Die [!DNL RabbitMQ] Container-Konfiguration zur Unterstützung [!DNL RabbitMQ] Version 3.8.<!--MAGECLOUD-4674-->

   - ![Fixsymbol](../../assets/fix.svg) **Persistenter Datenbankcontainer**—Die `magento-db: /var/lib/mysql` Das Datenbankvolumen bleibt jetzt erhalten, nachdem Sie die Docker-Konfiguration angehalten und entfernt haben, und wird beim Neustart der Docker-Konfiguration wiederhergestellt. Jetzt müssen Sie das Datenbankvolumen manuell löschen. Siehe [Datenbankcontainer].<!--MAGECLOUD-3978-->

   - ![Neues Symbol](../../assets/new.svg) **TLS-Container**—

      - ![Neues Symbol](../../assets/new.svg) **Aktualisierung des Basisbilds des Containers zur Verwendung des offiziellen Bildes**—Die [Cloud TLS-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) Das Bild basiert nun auf der offiziellen `debian:jessie` Docker-Bild.—<!--MAGECLOUD-4163-->

      - ![Neues Symbol](../../assets/new.svg) **Unterstützung für die [Pundierter TLS-Beenden-Proxy]**—Die [Pfund-Konfigurationsdatei](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) fügt die folgenden ENV-Variablen hinzu, um die Docker-Konfiguration für den TLS-Container anzupassen:

         - **`TimeOut`**—Legt den Wert für Time to First Byte (TTFB) timeout fest. Der Standardwert ist 300 Sekunden.

         - **`RewriteLocation`**—Bestimmt, ob der Proxy &quot;Pfund&quot;den Speicherort standardmäßig in die Anforderungs-URL umschreibt. Standardwert ist `0` um zu verhindern, dass das Umschreiben Umleitungen zu externen Websites wie einer externen SSO-Site unterbricht. [Fehlerbehebung von Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![Neues Symbol](../../assets/new.svg) Der Timeout-Wert in der TLS-Container-Konfiguration wurde von 15 auf 300 Sekunden erhöht. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![Neues Symbol](../../assets/new.svg) **Varkontainer**—

      - ![Neues Symbol](../../assets/new.svg) **Aktualisierung des Basisbilds des Containers zur Verwendung des offiziellen Bildes**—Die [Cloud Varnish-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) basiert nun auf dem offiziellen `centos` Docker-Bild.<!--MAGECLOUD-4163-->

      - ![Neues Symbol](../../assets/new.svg) **Verbesserte standardmäßige Timeout-Konfiguration**-Hinzugefügt `.first_byte_timeout` und `.between_bytes_timeout` Konfiguration in den Varnish-Container. Beide Timeout-Werte sind standardmäßig auf `300s` (5 Minuten). [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![Fixsymbol](../../assets/fix.svg) **Überspringen von Varnish während Xdebug-Sitzungen**—Aktualisierung der Konfiguration des Varnish-Containers, um `pass` bei Anfragen, die empfangen werden, wenn Xdebug aktiviert ist. In früheren Versionen konnten Sie Xdebug nicht verwenden, wenn die Docker-Umgebung Varnish enthielt. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![Neues Symbol](../../assets/new.svg) **Docker-Konfigurationsänderungen**—

   - ![Neues Symbol](../../assets/new.svg) **Verwalten von Bereitstellungen und Volumen für Ihr Projekt**—Es wurde die Möglichkeit hinzugefügt, beim Start einer Docker-Umgebung für die lokale Entwicklung Bereitstellungen und Volumen zu verwalten. Siehe [Projektdaten freigeben].<!--MAGECLOUD-3248-->

   - ![Neues Symbol](../../assets/new.svg) **Unterstützung für Netzwerkbrücke-Modus**—Unterstützung für Netzwerkbrücke-Modus hinzugefügt, um Verbindungen zwischen Docker-Containern über das lokale Netzwerk zu ermöglichen.<!--MAGECLOUD-4165-->

   - ![Neues Symbol](../../assets/new.svg) **Cron-Container standardmäßig deaktiviert**—Um die Leistung zu verbessern, ist der Cron-Container beim Erstellen der Docker-Umgebung nicht mehr standardmäßig konfiguriert. Sie können die `--with-cron` -Option auf dem Docker-Build-Befehl, um Ihrer Umgebung einen Cron-Container hinzuzufügen. Siehe [Verwalten von Cron-Aufträgen](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![Neues Symbol](../../assets/new.svg) **Anhalten der Synchronisierung großer Backup-Dateien**—DB-Dumps und Archivdateien (ZIP, SQL, GZ und BZ2) wurden zur Ausschlussliste in der `dist/docker-sync.yml` und `dist/mutagen.sh` -Dateien. Das Synchronisieren großer Dateien (> 1 GB) kann zu einer Inaktivität führen und Sicherungsdateien müssen normalerweise nicht synchronisiert werden, da Sie sie neu generieren können.<!--MAGECLOUD-3979-->

- ![Neues Symbol](../../assets/new.svg) **Befehlsänderungen**—

   - ![Fixsymbol](../../assets/fix.svg) Die `./bin/docker` Datei in `./bin/magento-docker` , um ein Problem zu beheben, das dazu führte, dass einige Docker-Umgebungen aufgrund der `./bin/docker` -Datei überschreibt vorhandene Docker-Binärdateien. Dies ist ein [Abwärtskompatible Änderung](backward-incompatible-changes.md) die Aktualisierungen an Ihren Skripten und Befehlen erfordert.<!-- MAGECLOUD-4038 -->

   - ![Neues Symbol](../../assets/new.svg) **Eine Dienstkonfigurationsoption wurde hinzugefügt, um den Datenbankanschluss für den Host verfügbar zu machen**—Verwenden Sie die `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` Option zur Anzeige des Datenbankanschlusses für den Host beim Erstellen der `docker-compose.yml` Datei: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![Neues Symbol](../../assets/new.svg) **Neuer Befehl nach der Bereitstellung**—Zuvor wurden die nach der Bereitstellung im `.magento.app.yaml` Datei automatisch ausgeführt, nachdem Sie Adobe Commerce in einem Cloud Docker-Container mit der `cloud-deploy` Befehl. Jetzt müssen Sie eine separate `cloud-post-deploy` -Befehl zum Ausführen der Hooks nach der Bereitstellung. Die aktualisierten Launch-Anweisungen finden Sie unter [Entwickler](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) und [production](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) -Modus.<!--MAGECLOUD-3996-->

   - ![Neues Symbol](../../assets/new.svg) Der `--rm` -Option `./bin/magento-docker` -Befehle für den Build- und Bereitstellungscontainer. Dadurch wird der Container nach Abschluss der Aufgabe entfernt.<!--MAGECLOUD-4205-->

   - ![Neues Symbol](../../assets/new.svg) **Aktualisierungen für `build:compose` command**—

      - ![Neues Symbol](../../assets/new.svg) Der `--sync-engine="native"` -Option `docker-build` -Befehl, um die Dateisynchronisierung zu deaktivieren, wenn Sie die Docker-Konfigurationsdatei im Entwicklermodus erstellen. Verwenden Sie diese Option bei der Entwicklung auf Linux-Systemen, die keine Dateisynchronisierung für die lokale Docker-Entwicklung erfordern. Siehe [Synchronisieren von Daten in der Docker-Umgebung](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![Neues Symbol](../../assets/new.svg) Die Standardeinstellung für die Dateisynchronisierung wurde geändert von `docker-sync` nach `native`. [Fehlerbehebung von Mathew Beane von Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![Neues Symbol](../../assets/new.svg) **Verbesserungen bei der Validierung**—

   - ![Neues Symbol](../../assets/new.svg) Es wurde eine Validierung zum Bereitstellungsprozess für lokale Docker-Entwicklungsumgebungen hinzugefügt, um zu überprüfen, ob die Cloud-Umgebungskonfiguration den zum Entschlüsseln der Datenbank erforderlichen Verschlüsselungsschlüssel enthält. Jetzt erhalten Sie eine Fehlermeldung im Protokoll, wenn die Umgebungskonfiguration keinen Wert für den Verschlüsselungsschlüssel angibt.<!--MAGECLOUD-4423-->

   - ![Neues Symbol](../../assets/new.svg) Es wurde eine Container-Konsistenzprüfung zum Elasticsearch-Dienst hinzugefügt, um sicherzustellen, dass der Dienst bereit ist, bevor die Build- und Bereitstellungsverarbeitung fortgesetzt wird. Wenn die Konsistenzprüfung einen Fehler zurückgibt, wird der Container automatisch neu gestartet.<!--MAGECLOUD-4456-->
