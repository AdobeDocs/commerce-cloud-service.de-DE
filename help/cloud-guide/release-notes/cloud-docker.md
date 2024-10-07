---
title: Cloud Docker-Paket
description: Sehen Sie sich eine Liste der neuesten Verbesserungen des Cloud Docker-Pakets an.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-10-07T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: fdb596430fbc532bed4a6b251872f44c5321d375
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 0%

---

# Cloud Docker-Paket

Das Paket [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) bietet Funktionen und Docker-Bilder zum Bereitstellen von Adobe Commerce in einer lokalen Cloud-Umgebung. In diesen Versionshinweisen werden die neuesten Verbesserungen an diesem Paket beschrieben, das Bestandteil der [Cloud Tools Suite für Commerce](cloud-tools-suite.md) ist.

Das Paket `magento/magento-cloud-docker` verwendet die folgende Versionssequenz: `<major>.<minor>.<patch>`

Die Versionshinweise beinhalten:

- ![neues Symbol](../../assets/new.svg) Neue Funktionen
- ![Fixsymbol](../../assets/fix.svg) Fehlerbehebungen und Verbesserungen

<!--Add release notes below-->

## v1.4.0 {#latest}

Veröffentlichungsdatum: 7. Oktober 2024

- ![Fixsymbol](../../assets/fix.svg) **Refaktorierter Code**: Die Unterstützung alter PHP-Versionen (7.4, 7.3, 7.2) und verwandter Bibliotheken und Bilder wurde entfernt.

## v1.3.7

Veröffentlichungsdatum: 8. April 2024

- ![neues Symbol](../../assets/new.svg) **PHP** — Unterstützung für PHP 8.3- und PHP 8.3-Bilder hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Nginx** - Bild Nginx v. 1.24 wurde hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **OpenSearch** - Bild OpenSearch v. 2.12, 1.3 hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Composer** - Die Composer-Version wurde auf 2.2.23 aktualisiert.

## v1.3.6

Veröffentlichungsdatum: 31. Juli 2023

- ![neues Symbol](../../assets/new.svg) **Neue Dienstversion** - OpenSearch 2.5 wurde hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Composer-Cache aktivieren** - Jetzt können Sie die Docker-Konfiguration erweitern, um den Cache zum Löschen durch Composer beim Starten des Docker-Containers zu aktivieren. Siehe [Erweitern der Docker-Konfiguration](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) im Handbuch _Cloud Docker für Commerce_ .

## v1.3.5

Veröffentlichungsdatum: 10. März 2023

- ![new icon](../../assets/new.svg) **ionCube**—Es wurde die ionCube-Erweiterung für das PHP 8.1-Bild hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Es wurden neue Dienstversionen hinzugefügt**—OpenSearch 2.3 und 2.4, PHP 8.2, Varnish 7.1.1.
- ![neues Symbol](../../assets/new.svg) **Verbesserte Unterstützung für PHP 8.2** - Kompatibilitätsprobleme mit bestimmten PHP 8.2.x-Versionen wurden behoben, um Commerce 2.4.6 zu unterstützen.
- ![Fixsymbol](../../assets/fix.svg) **Composer-Problem** - Es wurden Probleme behoben, die nach der Aktualisierung der Composer-Version in den Docker-Containern auftraten.

## v1.3.4

Veröffentlichungsdatum: 27. Oktober 2022

- ![neues Symbol](../../assets/new.svg) **Neue irische Bilder hinzugefügt**—Es wurden Bilder für Varnish 6.5, 7.0 und 7.1 hinzugefügt.<!-- MCLOUD-7879 -->

## v1.3.3

Veröffentlichungsdatum: 13. September 2022

- ![neues Symbol](../../assets/new.svg) **Apple M1 (ARM64) unterstützt** - Es wurden Änderungen an Docker-Bildern hinzugefügt, um die Unterstützung für die Apple M1-Architektur (ARM64) zu ermöglichen.<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![Fixsymbol](../../assets/fix.svg) **Mailhog** - Es wurde ein Problem behoben, bei dem der Mailhog-Dienst im Entwicklermodus keine E-Mails erfasste.<!-- MCLOUD-8643 -->
- ![Fixsymbol](../../assets/fix.svg) **init-docker.sh** - Korrektur des Validators für Dienstversionen im `init-docker.sh`-Skript.<!-- MCLOUD-8765 -->

## v1.3.2

Veröffentlichungsdatum: 31. März 2022

- ![neues Symbol](../../assets/new.svg) **Elasticsearch 7.10 image hinzugefügt**<!-- MCLOUD-8548 -->

## v1.3.1

Veröffentlichungsdatum: 10. März 2022

- ![new icon](../../assets/new.svg) **support PHP 8.1**—Es wurde Unterstützung für PHP 8.1 hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **OpenSearch**: Es wurden Bilder von OpenSearch-Versionen 1.1 und 1.2 hinzugefügt.
- ![neues Symbol](../../assets/new.svg) **Composer 2.1** - Legt Composer 2.1.x standardmäßig in PHP 8.x-Bildern fest.
- ![neues Symbol](../../assets/new.svg) **Verbesserungen bei PHP-Bildern**—

   - PHP 8.1-Bilder hinzugefügt
   - Aktualisierte xDebug-Version 3.1.2
   - Aktualisiertes xmlrpc 1.0.0RC3

- ![Fixsymbol](../../assets/fix.svg) **Verbesserungen bei Elasticsearch und OpenSearch**—Verbesserungen bei Elasticsearch und OpenSearch-Docker-Dateien; Elasticsearch 5.2 wurde entfernt.
- ![Fixsymbol](../../assets/fix.svg) **Sodium-Erweiterung**: Die `sodium` -Erweiterung wurde standardmäßig in allen PHP-Bildern aktiviert.
- ![Fixsymbol](../../assets/fix.svg) **Cache-Volumen des Composers**—Es wurde ein Pfad für das Cache-Volumen des Composers behoben, der zwischengespeicherte Composer-Pakete enthielt.
- ![Fixsymbol](../../assets/fix.svg) **Speicherbegrenzung in nginx** - Speicherbegrenzung im NGINX-Bild wurde korrigiert.

## v1.3.0

Veröffentlichungsdatum: 25. Oktober 2021

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Arbeitsablauf für den Entwicklermodus verbessern** - Zuvor mussten Sie den Modus in den Schritten zum Erstellen und Bereitstellen angeben. Jetzt bestimmt die Option `--mode` im Schritt `build` den Modus im späteren Schritt `deploy` . Es ist nicht mehr erforderlich, den Modus nach der Bereitstellung festzulegen. Siehe [Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![Fixsymbol](../../assets/fix.svg) **Verbesserungen für schreibgeschütztes Dateisystem**—<!-- ACMP-1106 -->
   - Fehlerkorrektur - Ein PHP-Container für die E-Mail-Konfiguration kann jetzt gestartet werden.
   - Kann Umgebungsvariablen in INI-Dateien verwenden.
   - Stellen Sie sicher, dass PHP-Einstiegspunkte keine Schreibberechtigung benötigen.
- ![Fixsymbol](../../assets/fix.svg) **Aktualisierungsknoten** - Aktualisieren Sie die gebündelte Knotenversion. Bei der Installation von Knoten in PHP-CLI-Bildern wird jetzt die aktuelle LTS-Version verwendet.<!-- ACMP-1539 -->
- ![Fixsymbol](../../assets/fix.svg) **Symfony aktualisieren**: Die Symfony-Konfigurationsabhängigkeiten wurden aktualisiert und sind nun mit Adobe Commerce 2.4.4 kompatibel.<!-- ACMP-1533 -->

## v1.2.4

Veröffentlichungsdatum: 29. Juli 2021

- ![neues Symbol](../../assets/new.svg) **Neuer `Zookeeper` Container**: Es wurde ein [Zookeeper-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) hinzugefügt, um die Konfiguration des Sperranbieters für Projekte zu verwalten, die nicht in der Cloud-Infrastruktur in Adobe Commerce bereitgestellt werden.<!--MCLOUD-8000-->

- ![neues Symbol](../../assets/new.svg) **Unterstützung für Composer 2.0 hinzugefügt.**: Composer-Version 2.0 wurde zur Konfigurationsdatei des Composers hinzugefügt, um Aktualisierungen von Composer 1.0 zu unterstützen, die kurz vor dem Ende des Lebenszyklus stehen.<!--MCLOUD-8003-->

## v1.2.3

Veröffentlichungsdatum: 14. Juni 2021

- ![neues Symbol](../../assets/new.svg) **PHP 8.0** hinzugefügt—PHP wurde auf Version 8.0 aktualisiert, sodass Sie alle neuen Funktionen und Optimierungen nutzen können, die PHP 8.0 enthält.<!--MCLOUD-7941-->
- ![neues Symbol](../../assets/new.svg) **Aktualisiert auf Varnish 6.6 und Elasticsearch 7.11.2** - Die folgenden Links enthalten Versionsinformationen zu [Varnish Cache 6.6.5} und Elasticsearch 7.11.2.<!--MCLOUD-7921-->](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0)
- ![neues Symbol](../../assets/new.svg) **Die Erweiterung `ioncube` für PHP 7.4 image** wurde hinzugefügt - Die Erweiterung `ioncube` wurde dem PHP 7.4-Bild erneut hinzugefügt, nachdem sie ursprünglich vom PHP 7.3 auf PHP 7.4-Upgrade ausgeschlossen wurde. *[Gesendet von mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![neues Symbol](../../assets/new.svg) **Eine Option zur Dateisynchronisierung wurde hinzugefügt:`manual-native`** - Die Option zur Dateisynchronisierung `manual-native` bietet manuelle Kontrolle über die Synchronisierung, was die beste Leistung für macOS- und Windows-Umgebungen bietet. Erfahren Sie mehr über die Verwendung der Option `manual-native` im [Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) und im [Synchronisieren von Daten in einer Docker-Entwicklerumgebung](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![neues Symbol](../../assets/new.svg) **Entfernte Lautstärke aus `up` und `down` Befehlen** entfernt - Die Option `--volume` wurde aus den Befehlen `bin/magento-docker up` und `bin/magento-docker down` entfernt und durch den neuen Befehl `bin/magento-docker init` mit einer Warnung wegen Datenverlust ersetzt. Durch diese Änderung wird ein versehentlicher Datenverlust verhindert. *[Gesendet von joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![Fixsymbol](../../assets/fix.svg) **Aktualisierter `CN` -Wert für das generierte Zertifikat** - Der hartcodierte `CN` -Wert wurde aus der Dockerdatei entfernt. Mit diesem Wert wurde ein Zertifikatfehler (`NET::ERR_CERT_INVALID`) erstellt, der dazu führte, dass die `--host` -Option für den `ece-docker build:compose` -Befehl ignoriert wurde.<!--MCLOUD-7934-->

## v1.2.2

Veröffentlichungsdatum: 20. April 2021

- ![neues Symbol](../../assets/new.svg) **`host.docker.internal` wurde aktualisiert, um plattformunabhängig zu sein** - Sie können jetzt dieselben Docker Compose-Skripte für Ubuntu, Windows und macOS erstellen. Die Verwendung von Xdebug in Ubuntu erfordert keine separate Umgebungsvariable mehr. [Fehlerbehebung, eingereicht von Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![neues Symbol](../../assets/new.svg) **Aktualisierung init-docker.sh** - Das Objekt `mounts` wurde zur Umgebungsvariablen `MAGENTO_CLOUD_APPLICATION` hinzugefügt. [Fehlerbehebung, eingereicht von Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![neues Symbol](../../assets/new.svg) **init-docker.sh** - Aktualisierung des `init-docker.sh` Skripts mit PHP 7.4 und Cloud Docker 1.2.1-Versionen. [Fehlerbehebung gesendet von Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![neues Symbol](../../assets/new.svg) **Natrium standardmäßig aktiviert** - Aktiviert die `sodium` PHP-Erweiterung standardmäßig in PHP Docker-Bildern.<!--MCLOUD-7548-->
- ![neues Symbol](../../assets/new.svg) **`custom-registry`Option**—Dem Befehl `php ./vendor/bin/ece-docker build:compose` wurde eine `--custom-registry` Option für die Verwendung der eigenen Bildregistrierung hinzugefügt.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![neues Symbol](../../assets/new.svg) **Alte Elasticsearch-Versionen entfernt** - Elasticsearch-Versionen 1.7 und 2.4 wurden aus den Elasticsearch-Bildern entfernt.<!--MCLOUD-7504-->
- ![neues Symbol](../../assets/new.svg) **Automatische Generierung von NGINX-Zertifikaten**: Die vorhandenen Zertifikate wurden aus dem NGINX-Bild entfernt. Die NGINX-Zertifikate werden jetzt bei jeder neuen Bereitstellung automatisch generiert, um die Sicherheit zu verbessern.<!--MCLOUD-7396-->
- ![Fixsymbol](../../assets/fix.svg) **Aktiviert`opcache.validate_timestamps`** - Aktiviert die PHP-Einstellung `opcache.validate_timestamps` standardmäßig im Entwicklermodus. Durch Aktivierung dieser Einstellung wurde das Problem behoben, dass Änderungen am Dateisystem in Docker nicht erkannt wurden.<!--MCLOUD-7466-->
- ![Fixsymbol](../../assets/fix.svg) **Fest`build:custom:compose`** - Korrektur des Befehls `build:custom:compose`, um einen Fehler auszulösen, wenn Dateien während des Build-Prozesses nicht überschrieben werden können. Die Ausgabe eines Fehlers verhindert Situationen, in denen `docker-compose up` die falschen Dateien verwenden könnte.<!--MCLOUD-7457-->
- ![Fixsymbol](../../assets/fix.svg) **Korrektur der `--sync_engine="native"` Option** - Korrektur des Problems, bei dem im Produktionsmodus (`--mode="production"`) die Option `--sync_engine="native"` keine Einträge für lokale Ordner in der Datei `docker.composer.yml` erstellte.<!--MCLOUD-7254-->
- ![Fixsymbol](../../assets/fix.svg) **Fehler bei der Überprüfung der Dienstversion behoben**—Dienstversionen für [!DNL RabbitMQ], Elasticsearch und andere Dienste wurden zur Eigenschaft `type` in der Variable `MAGENTO_CLOUD_RELATIONSHIP` hinzugefügt. Durch Hinzufügen dieser Versionen zur Variable `relationships` wurden die Validierungsfehler behoben, die während der Bereitstellungsphase aufgetreten sind.<!--MCLOUD-7572-->

## v1.2.1

Veröffentlichungsdatum: 21. Dezember 2020

- ![neues Symbol](../../assets/new.svg) **NGINX-Befehlsoptionen**—Es wurden Build-Befehlsoptionen hinzugefügt, mit denen die Anzahl der NGINX `worker_processes` und NGINX `worker_connections` für TLS und Webdienste geändert werden kann. Der Parameter `worker_process` behält die Möglichkeit, den Wert auf `auto` festzulegen. Beispiele: <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![neues Symbol](../../assets/new.svg) **TLS-Befehlsoption**—Es wurde eine Build-Befehlsoption hinzugefügt, mit der eine Konfiguration ohne den TLS-Dienst erstellt werden kann. Beispiel: <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![neues Symbol](../../assets/new.svg) **NGINX-Speicherverbrauch** - Verringerte den Speicher, der vom NGINX-Prozess für TLS und Webdienste benötigt wird.<!--MCLOUD-7259-->

- ![neues Symbol](../../assets/new.svg) **Blackfire** - Die Blackfire PHP-Erweiterung wurde standardmäßig im Cloud Docker-Bild deaktiviert.

- ![Fixsymbol](../../assets/fix.svg) **PHP-FPM-Container**—Korrektur der Konsistenzprüfung des PHP-FPM-Containers, indem der `WEB_PORT` von `80` in `8080` geändert wurde.<!--MCLOUD-7232-->

- ![Fixsymbol](../../assets/fix.svg) **Ungültige Volumenbenennung** - Es wurde ein Fehler mit ungültiger Volumenbenennung im Entwicklermodus behoben.<!--MCLOUD-7442-->

- ![Fixsymbol](../../assets/fix.svg) **NGINX Upstream Port** - Das Docker NGINX 1.19-Bild wurde aktualisiert und verwendet nun Port 8080, um eine Endlosschleife zu vermeiden. [Fehlerbehebung gesendet von Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Veröffentlichungsdatum: 9. November 2020

- ![neues Symbol](../../assets/new.svg) **Container-Aktualisierungen—**

   - ![new icon](../../assets/new.svg) **PHP-FPM container**—Es wurde Unterstützung für die gnupg PHP-Erweiterung hinzugefügt. [Fehlerbehebung, die von G Arvind von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![Fixsymbol](../../assets/fix.svg) **Datenbank-Container** - Die Konsistenzprüfung des Datenbankcontainers wurde korrigiert, indem das erforderliche Datenbankkennwort zum Konsistenzprüfungsbefehl hinzugefügt wurde.<!--MCLOUD-7122-->

   - ![neues Symbol](../../assets/new.svg) **Elasticsearch-Container**

      - Unterstützung für Elasticsearch 7.9 zur Kompatibilität mit kommenden Adobe Commerce-Versionen hinzugefügt.<!--MCLOUD-7190-->

      - **Elasticsearch-Plug-in-Konfiguration**: Es wurde Unterstützung für die Verwendung der Elasticsearch-Plug-in-Konfigurationsinformationen aus der `services.yaml` -Datei hinzugefügt, um die `docker-compose.yaml` -Datei für eine Cloud Docker für Commerce-Umgebung zu generieren. Siehe [Elasticsearch plugins](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Elasticsearch-Plug-in-Unterstützung** - Unterstützung für die folgenden Elasticsearch-Plug-ins hinzugefügt: `analysis-icu`, `analysis-phonetic`, `analysis-stempel` und `analysis-nori`. Die Plug-ins `analysis-icu` und `analysis-phonetic` sind standardmäßig installiert. Sie können die Plug-ins `analysis-stempel` und `analysis-nori` nach Bedarf hinzufügen oder entfernen.<!--MCLOUD-2789-->

   - ![neues Symbol](../../assets/new.svg) **CLI-Container**

      - **Ausführen von Befehlen in Docker PHP Containern** - Jetzt können Sie die Cloud Docker-CLI verwenden, um Befehle in PHP-Containern in Ihrer Docker-Umgebung auszuführen, ohne PHP auf dem Host installieren zu müssen. Beispielsweise erstellt der folgende Befehl die Konfiguration: `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Siehe [Cloud Docker-CLI](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Fehlerbehebung, die von G Arvind von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - Der OpenSSH-Client wurde zu PHP CLI-Containern hinzugefügt. Jetzt können Sie die ssh-agent-Weiterleitung für Composer verwenden, wenn die `composer.json` -Datei private Git-Repositorys enthält, für die ein SSH-Client Composer-Befehle verwenden muss.<!--MCLOUD-6008-->

   - ![Fixsymbol](../../assets/fix.svg) **TLS-Container** - Jetzt basiert der [TLS-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) auf dem `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Docker-Bild anstelle des CentOS-Bildes. Diese Änderung behebt Probleme, die beim Senden von HTTPS-Anforderungen zwischen Containern in der Cloud Docker-Umgebung zu Fehlern führten.<!--MCLOUD-6469-->

   - ![neues Symbol](../../assets/new.svg) **Testcontainer**: Es wurde ein Testcontainer für Anwendungstests hinzugefügt und die Option `--with-test` wurde zum Befehl Docker `build:compose` hinzugefügt, damit der Container nur beim Testen in der Docker-Umgebung erstellt wird. Siehe [Anwendungstests](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![neues Symbol](../../assets/new.svg) **FPM-XDEBUG-Container**

      - ![neues Symbol](../../assets/new.svg) **Xdebug unter Linux konfigurieren**: Die Option `--set-docker-host` wurde zum Befehl `ece-docker build:compose` hinzugefügt, um den Wert `host.docker.internal` im Xdebug-Container zu konfigurieren. Diese Option ist erforderlich, um Xdebug auf Linux-Systemen zu verwenden. Siehe [Xdebug für Docker konfigurieren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![Fixsymbol](../../assets/fix.svg) Korrektur der Xdebug-Variablenkonfiguration für den Docker ENTRYPOINT, um `uninitialized "with_xdebug" variable` Fehler in den Protokollen zu beheben. [Fehlerbehebung, eingereicht von Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![neues Symbol](../../assets/new.svg) **Änderungen der Docker-Konfiguration**

   - **MailHog-Konfiguration** - Jetzt können Sie die folgenden `ece-docker build:compose` -Befehlsoptionen verwenden, um MailHog zu deaktivieren und die Ports anzugeben: `--no-mailhog`, `--mailhog-http-port` und `--mailhog-smtp-port`. Siehe [E-Mail einrichten](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Für Cloud Docker für Commerce 1.2.0 und höher stellt Adobe jetzt Docker-Bilder für jede Patch-Version bereit. Der Docker-Konfigurationsgenerator erstellt die Docker-Konfiguration mit einer angegebenen Patch-Version, anstatt die neueste Version zu verwenden. Zuvor erstellte der Docker-Konfigurationsgenerator die Konfiguration mit der neuesten Patch-Version, die Cloud Docker für Commerce-Umgebungen beschädigte, die mit einer früheren Version erstellt wurden.<!--MCLOUD-7093-->

   - **Festlegen benutzerdefinierter Bilder und Versionen in der benutzerdefinierten Cloud Docker-Konfiguration** - Der Befehl `build:custom:compose` wurde mit Optionen zum Angeben benutzerdefinierter Bilder und Versionen beim Generieren einer benutzerdefinierten Docker-Komprimierungskonfigurationsdatei (`docker-compose.yaml`) aktualisiert. Siehe [Erstellen einer benutzerdefinierten Docker Compose-Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Aktualisierung der Docker-Host-Konfiguration, um Port 443 anzuzeigen und den Zugriff auf Adobe Commerce (`https://magento2.docker`) von allen CLI-Containern zu ermöglichen. Sie können den Standardanschluss ändern, indem Sie beim Generieren der Docker-Konfigurationsdatei die Option `--tls-port` hinzufügen.<!--MCLOUD-6806-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das dazu führte, dass der Cloud-Docker für den Commerce-Build fehlschlug, wenn die `app/etc/env.php` -Datei vorhanden war.<!--MCLOUD-6732-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die Build-Konfiguration wurde aktualisiert, um benannte Volumes durch normale Volumes zu ersetzen, um Probleme bei der Bereitstellung von Cloud Docker für Commerce unter Linux oder Windows Subsystem für Linux (WSL2) zu vermeiden.<!--MCLOUD-6732-->

- ![Fixsymbol](../../assets/fix.svg) Cloud Docker für Commerce-Funktionstests wurde aktualisiert, um Composer 2.0 zu unterstützen.<!--MCLOUD-7183-->

## v1.1.2

Veröffentlichungsdatum: 9. September 2020

- ![neues Symbol](../../assets/new.svg) Unterstützung für Elasticsearch 7.7<!--MCLOUD-6219--> hinzugefügt

## v1.1.1

Releasedatum: 5. August 2020

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierte E-Mail-Konfiguration**: Die standardmäßige Cloud Docker-Konfiguration für Commerce wurde aktualisiert, um den MailHog-Dienst anstelle von SendMail zu unterstützen. Siehe [E-Mail einrichten](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die PS-Bibliothek wurde in der Cloud Docker-Umgebungskonfiguration wiederhergestellt, um `ps:  command not found` Fehler zu beheben.<!--MCLOUD-6621-->

- ![Fixsymbol](../../assets/fix.svg) Aktualisierung des standardmäßigen Cloud Docker für die Commerce-Konfiguration, um die automatische Bereitstellung des Einstiegspunkts für die Datenbank und der MariaDB-Volumes zu entfernen und `Cannot create container for service db` Fehler zu beheben, die beim Starten Ihrer Cloud Docker-Umgebung auftreten können.

  Jetzt können Sie die Cloud Docker-Umgebung konfigurieren, um die Datenbankverzeichnisse bereitzustellen, indem Sie die folgenden Optionen zum Befehl `ece-docker build:compose` hinzufügen: `--with-entry-point` und `with-mariadb-conf`. Siehe [Dienstkonfigurationsoptionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![neues Symbol](../../assets/new.svg) **CLI-Befehl aktualisiert**

| Aktion | Befehl |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Fügen Sie einen Einstiegspunkt zum Datenbankcontainer hinzu, um die Datenbank aus der Sicherung wiederherzustellen. | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| MariaDB-Konfigurationsvolumen hinzufügen | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Veröffentlichungsdatum: 25. Juni 2020

- ![neues Symbol](../../assets/new.svg) **Unterstützung für die Lösung zur geteilten Datenbankleistung hinzugefügt** - Jetzt können Sie einen Store mithilfe der Aufspaltungs-Datenbankleistungslösung in der Cloud-Docker-Umgebung konfigurieren und bereitstellen.<!--MCLOUD-3740-->

- ![neues Symbol](../../assets/new.svg) **Unterstützung für Adobe Commerce- und Magento Open Source-Bereitstellung** - Jetzt können Sie Cloud Docker für Commerce verwenden, um eine lokale Entwicklungsumgebung für Projekte bereitzustellen, die nicht in Adobe Commerce in der Cloud-Infrastruktur gehostet werden.<!--MCLOUD-5667-->

- ![neues Symbol](../../assets/new.svg) **Blackfire.io-Unterstützung**—Es wurde Unterstützung für die Verwendung der [Blackfire.io-Erweiterung](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) für automatisierte Leistungstests hinzugefügt. [Fehlerbehebung, die von Adarsh Manickam von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![neues Symbol](../../assets/new.svg) **Container-Updates**

   - **Varnish**: &quot;Jetzt Varnish&quot;ist der Standardcache, wenn Sie Adobe Commerce in einer Cloud Docker-Umgebung mit einer unterstützten Version der Cloud-Anwendungsvorlage bereitstellen. Siehe [Varnish-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Die Option `--no-varnish` wurde hinzugefügt, um die Installation des Varnish-Dienstes zu überspringen, wenn Sie die Cloud Docker-Konfigurationsdatei generieren.<!--MCLOUD-2634-->

   - ![neues Symbol](../../assets/new.svg) **Datenbank**

      - Unterstützung für die MySQL-Datenbank hinzugefügt. Jetzt können Sie die Cloud Docker-Umgebung mit MariaDB oder MySQL konfigurieren. Siehe [Dienstkonfigurationsoptionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Es wurde die Möglichkeit hinzugefügt, die Inkrement- und Offset-Einstellungen für die Datenbankreplikation festzulegen, wenn Sie die Docker-Komprimierungsdatei generieren. Siehe [Dienstcontainer](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![neues Symbol](../../assets/new.svg) **PHP-FPM**

      - Unterstützung für PHP 7.4 hinzugefügt. [Fehlerbehebung, die von Mohanela Murugan von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Es wurde die Möglichkeit hinzugefügt, eine `php.ini` -Datei im Stammprojektverzeichnis in die Cloud Docker-Umgebung zu kopieren und benutzerdefinierte PHP-Einstellungen auf die PHP-FPM- und CLI-Container anzuwenden. Siehe [Anpassen von PHP-Einstellungen](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Es wurde eine Konsistenzprüfung für Container hinzugefügt. [Fehlerbehebung, die von Visanth Sampath von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![Fixsymbol](../../assets/fix.svg) **Node.js**: Die standardmäßige Node.js-Version von Version 8 wurde auf Version 10 aktualisiert, um die Sicherheit zu verbessern. Node.js Version 8 ist veraltet und nicht mehr mit Fehlerbehebungen oder Sicherheits-Patches aktualisiert. [Fehlerbehebung, die von Mohan Elamurugan von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![neues Symbol](../../assets/new.svg) **Elasticsearch**

      - Unterstützung für Elasticsearch 6.8, 7.2, 7.5 und 7.6 hinzugefügt.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Es wurde die Möglichkeit hinzugefügt, die [Konfiguration des Elasticsearch-Containers](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) anzupassen, wenn Sie die Konfigurationsdatei für die Docker-Komposition generieren.<!--MCLOUD-3059-->

      - Die Option `--no-es` wurde zu den Dienstkonfigurationsoptionen zum Generieren der Konfigurationsdatei Docker erstellen hinzugefügt. Verwenden Sie diese Option, um die Installation des Elasticsearch-Containers zu überspringen und stattdessen die MySQL-Suche zu verwenden. Diese Option wird nur für Adobe Commerce-Versionen 2.3.5 und älter unterstützt.<!--MCLOUD-3766-->

   - ![neues Symbol](../../assets/new.svg) **FPM-XDEBUG-Container**: Es wurde eine Dienstkonfigurationsoption zur Installation und Konfiguration von Xdebug zum Debugging von PHP in Ihrer Cloud Docker-Umgebung hinzugefügt. Siehe [Xdebug konfigurieren](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![neues Symbol](../../assets/new.svg) **Änderungen der Docker-Konfiguration**

   - Es wurden Konsistenzprüfungen für die Dienstcontainer PHP-FPM, Redis, Elasticsearch und MySQL Docker hinzugefügt.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Der standardmäßige Dateisynchronisierungsmodus wurde im Entwicklermodus zu `native` geändert.<!--MCLOUD-3890 -->

   - Es wurden Versionsinformationen zum generischen Docker-Dienst-Container-Bild beim Generieren der `docker-compose.yml`-Datei hinzugefügt.<!--MCLOUD-3878-->

   - Verbesserte Fähigkeit, große Antworten aus dem vorgelagerten PHP-FPM-Container zu verarbeiten, indem der `fastcgi_buffers` -Wert für den Nginx-Server erhöht wird.<!--MCLOUD-5980-->

   - Verbesserte Leistung bei der Synchronisierung von Mutagen-Dateien durch Hinzufügen einer zweiten Synchronisierungssitzung zum Synchronisieren von Dateien im Ordner &quot;`vendor`&quot;. Diese Änderung verhindert, dass Mutagen während der Dateisynchronisierung feststecken bleibt. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![neues Symbol](../../assets/new.svg) **CLI-Befehl aktualisiert**

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

- ![Fixsymbol](../../assets/fix.svg) Die Konfiguration der Mutagendatei-Synchronisation wurde korrigiert, um zu verhindern, dass Mutagen veraltete Sitzungen erstellt. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Konfigurationsproblems, das beim Starten des PHP-FPM-Containers Syntaxfehler im Docker-Komprimierungsprotokoll verursachte. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Behebung von Volumenkonfliktfehlern, die manchmal bei der Verwendung mehrerer Docker-Umgebungen aufgetreten sind. [Fehlerbehebung, die von G Arvind von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/168).

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem der Befehl `ece-docker build:compose` fehlschlug, wenn die Konfiguration Blackfire.io enthielt. [Fehlerbehebung, die von G Arvind von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die PHP-CLI-Bildkonfiguration wurde aktualisiert, um Fehler wegen zu wenig Arbeitsspeicher zu vermeiden, die bei der Installation mehrerer Pakete mit Cloud Docker für Commerce aufgetreten sind. [Fehlerbehebung, die von Mohan Elamurugan von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![Fixsymbol](../../assets/fix.svg) Unterstützung für mehrere MySQL-Benutzer in der Cloud Docker-Umgebung hinzugefügt. In früheren Versionen schlug der Vorgang `build:compose` fehl, wenn in der Datei `magento.app.yaml` mehrere Datenbankbenutzer angegeben waren. [Fehlerbehebung, die von G Arvind von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) `rsyslog` wurde aus dem Cloud-Docker für Commerce-PHP-Container entfernt, um Kompatibilitätsprobleme zu beheben, die Warnhinweise während der Bereitstellung verursachten. Cloud Docker verwendet nicht das Dienstprogramm rsyslog.<!--MCLOUD-6173-->

## v1.0.0

Veröffentlichungsdatum: 5. Februar 2020

- ![neues Symbol](../../assets/new.svg) **Erstellt ein separates Paket zur Bereitstellung von`Cloud Docker for Commerce`** - Der Quellcode wurde verschoben, um Cloud Docker für Commerce aus dem `ece-tools` -Repository in das [neue `magento-cloud-docker`-Repository bereitzustellen](https://github.com/magento/magento-cloud-docker), um die Codequalität zu wahren und unabhängige Versionen bereitzustellen. Das neue Paket ist eine Abhängigkeit von ECE-Tools v2002.1.0 und höher.

  Wenn Sie die ece-tools aktualisieren, aktualisieren Sie auch das `magento/magento-cloud-docker` -Paket auf Version 1.0.0. Wenn Sie Cloud Docker für Commerce mit einer früheren Version von `ece-tools` (2002.0.x) verwendet haben, überprüfen Sie die [Abwärtskompatibilitäten](backward-incompatible-changes.md) und aktualisieren Sie Ihr Projekt als Skripte, Befehle und Prozesse nach Bedarf.

- ![neues Symbol](../../assets/new.svg) **Versionierung zu den Docker-Bildern hinzugefügt** - Sie müssen jetzt das Paket `magento/magento-cloud-docker` aktualisieren, um die aktualisierten Bilder zu erhalten.<!--MAGECLOUD-4737-->

- ![neues Symbol](../../assets/new.svg) **Container-Updates**—

   - ![neues Symbol](../../assets/new.svg) **PHP-FPM-Container**—

      - ![neues Symbol](../../assets/new.svg) **Node.js-Unterstützung hinzugefügt**—Das PHP-FPM-Bild wurde aktualisiert, um die Funktionen node, npm und granunt-cli im PHP-Container zu unterstützen.<!--MAGECLOUD-3953-->

      - ![neues Symbol](../../assets/new.svg) **Unterstützung für [ionCube](https://www.ioncube.com/)** hinzugefügt - Die standardmäßige Docker-Konfiguration wurde aktualisiert, um ionCube in der lokalen Docker-Entwicklungsumgebung zu unterstützen.<!--MAGECLOUD-4354-->

   - ![neues Symbol](../../assets/new.svg) **Webcontainer**—

      - ![neues Symbol](../../assets/new.svg) **NGINX-Konfiguration anpassen**: Es wurde die Möglichkeit hinzugefügt, eine benutzerdefinierte `nginx.conf` -Datei für die Cloud-Docker-Umgebung für Commerce bereitzustellen. Siehe [Webcontainer](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![neues Symbol](../../assets/new.svg) **Automatisch generierte NGINX-Zertifikate** - Die Docker-Konfigurationsdatei enthält jetzt die Konfiguration zum automatischen Generieren von NGINX-Zertifikaten für den Webcontainer.<!--MAGECLOUD-4258-->

   - ![neues Symbol](../../assets/new.svg) **Neuer Selenium-Container**: Es wurde ein [Selenium-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) hinzugefügt, um Adobe Commerce-Anwendungstests mithilfe des Magento Functional Testing Framework (MFTF) zu unterstützen.<!--MAGECLOUD-4040-->

   - ![neues Symbol](../../assets/new.svg) **[!DNL RabbitMQ]Versionsunterstützung** - Die [!DNL RabbitMQ] -Containerkonfiguration wurde aktualisiert, um [!DNL RabbitMQ] Version 3.8 zu unterstützen.<!--MAGECLOUD-4674-->

   - ![Fixsymbol](../../assets/fix.svg) **Persistenter Datenbank-Container** - Das `magento-db: /var/lib/mysql` Datenbankvolumen bleibt jetzt erhalten, nachdem Sie die Docker-Konfiguration angehalten und entfernt haben. Das Datenbankvolumen wird dann beim Neustart der Docker-Konfiguration wiederhergestellt. Jetzt müssen Sie das Datenbankvolumen manuell löschen. Siehe [Datenbankcontainer].<!--MAGECLOUD-3978-->

   - ![neues Symbol](../../assets/new.svg) **TLS-Container**—

      - ![neues Symbol](../../assets/new.svg) **Das Basisbild des Containers wurde aktualisiert, um das offizielle Bild zu verwenden** - Das Bild für den [Cloud TLS-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) basiert jetzt auf dem offiziellen `debian:jessie` Docker-Bild.—<!--MAGECLOUD-4163-->

      - ![neues Symbol](../../assets/new.svg) **Unterstützung für den [Pund TLS Termination Proxy]** hinzugefügt - Die [Pund-Konfigurationsdatei](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) fügt die folgenden ENV-Variablen hinzu, um die Docker-Konfiguration für den TLS-Container anzupassen:

         - **`TimeOut`** - Legt den Wert Time to First Byte (TTFB) timeout fest. Der Standardwert ist 300 Sekunden.

         - **`RewriteLocation`** - Bestimmt, ob der Proxy &quot;Pfund&quot;den Speicherort standardmäßig in die Anforderungs-URL umschreibt. Die Standardeinstellung ist `0` , um zu verhindern, dass Umleitungen zu externen Websites wie einer externen SSO-Site umbrochen werden. [Von Sorin Sugar eingereichte Fehlerbehebung](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![neues Symbol](../../assets/new.svg) Der Timeout-Wert in der TLS-Container-Konfiguration wurde von 15 auf 300 Sekunden erhöht. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![new icon](../../assets/new.svg) **varnish container**—

      - ![neues Symbol](../../assets/new.svg) **Das Basisbild des Containers wurde aktualisiert, um das offizielle Bild zu verwenden** - Der [Cloud Varnish-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) basiert jetzt auf dem offiziellen `centos` Docker-Bild.<!--MAGECLOUD-4163-->

      - ![neues Symbol](../../assets/new.svg) **Verbesserte standardmäßige Timeout-Konfiguration**-Hinzufügung der Konfigurationen `.first_byte_timeout` und `.between_bytes_timeout` zum Varnish-Container. Beide Timeout-Werte sind standardmäßig auf `300s` (5 Minuten) eingestellt. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![Fixsymbol](../../assets/fix.svg) **Varianten während Xdebug-Sitzungen überspringen** - Die Konfiguration des varnish-Containers wurde aktualisiert und gibt `pass` für Anforderungen zurück, die bei aktiviertem Xdebug empfangen wurden. In früheren Versionen konnten Sie Xdebug nicht verwenden, wenn die Docker-Umgebung Varnish enthielt. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![neues Symbol](../../assets/new.svg) **Änderungen der Docker-Konfiguration**—

   - ![neues Symbol](../../assets/new.svg) **Verwalten von Bereitstellungen und Volumina für Ihr Projekt**: Es wurde die Möglichkeit hinzugefügt, Bereitstellungen und Volumina beim Start einer Docker-Umgebung für die lokale Entwicklung zu verwalten. Siehe [ Projektdaten freigeben].<!--MAGECLOUD-3248-->

   - ![neues Symbol](../../assets/new.svg) **Unterstützung für Netzwerkbrücke-Modus** - Unterstützung für Netzwerkbrücke-Modus hinzugefügt, um Verbindungen zwischen Docker-Containern über das lokale Netzwerk zu aktivieren.<!--MAGECLOUD-4165-->

   - ![neues Symbol](../../assets/new.svg) **Cron-Container standardmäßig deaktiviert** - Zur Leistungsverbesserung wird der Cron-Container beim Erstellen der Docker-Umgebung nicht mehr standardmäßig konfiguriert. Sie können die Option `--with-cron` im Docker-Build-Befehl verwenden, um Ihrer Umgebung einen Cron-Container hinzuzufügen. Siehe [Verwalten von Cron-Aufträgen](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![neues Symbol](../../assets/new.svg) **Beenden Sie die Synchronisation großer Sicherungsdateien**: DB-Dumps und Archivdateien - ZIP, SQL, GZ und BZ2 - wurden zur Ausschlussliste in den Dateien `dist/docker-sync.yml` und `dist/mutagen.sh` hinzugefügt. Die Synchronisation großer Dateien (> 1 GB) kann zu einer Inaktivität führen, und Sicherungsdateien erfordern normalerweise keine Synchronisation, da Sie sie neu generieren können.<!--MAGECLOUD-3979-->

- ![neues Symbol](../../assets/new.svg) **Befehlsänderungen**—

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die `./bin/docker` -Datei wurde in `./bin/magento-docker` umbenannt, um ein Problem zu beheben, das dazu führte, dass einige Docker-Umgebungen beschädigt wurden, da die `./bin/docker` -Datei vorhandene Docker-Binärdateien überschreibt. Dies ist eine [abwärtskompatible Änderung](backward-incompatible-changes.md), die Aktualisierungen Ihrer Skripte und Befehle erfordert.<!-- MAGECLOUD-4038 -->

   - ![neues Symbol](../../assets/new.svg) **Es wurde eine Dienstkonfigurationsoption hinzugefügt, um den Datenbankanschluss für den Host verfügbar zu machen** - Verwenden Sie die `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>`-Option, um den Datenbankanschluss für den Host verfügbar zu machen, wenn Sie die `docker-compose.yml`-Datei erstellen: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![neues Symbol](../../assets/new.svg) **Neuer Befehl nach der Bereitstellung** - Zuvor wurden die in der Datei `.magento.app.yaml` definierten Hooks nach der Bereitstellung automatisch ausgeführt, nachdem Sie Adobe Commerce mithilfe des Befehls `cloud-deploy` in einem Cloud-Docker-Container bereitgestellt haben. Jetzt müssen Sie einen separaten `cloud-post-deploy` -Befehl ausgeben, um die Hooks nach der Bereitstellung auszuführen. Siehe aktualisierte Launch-Anweisungen für den Modus [Entwickler](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) und [Produktion](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) .<!--MAGECLOUD-3996-->

   - ![neues Symbol](../../assets/new.svg) Die Option `--rm` wurde zu den Befehlen `./bin/magento-docker` für den Build- und Bereitstellungscontainer hinzugefügt. Dadurch wird der Container entfernt, nachdem die Aufgabe abgeschlossen ist.<!--MAGECLOUD-4205-->

   - ![neues Symbol](../../assets/new.svg) **Aktualisierungen an `build:compose` Befehl**—

      - ![neues Symbol](../../assets/new.svg) Die Option `--sync-engine="native"` wurde zum Befehl `docker-build` hinzugefügt, um die Dateisynchronisierung zu deaktivieren, wenn Sie die Konfigurationsdatei Docker erstellen im Entwicklermodus generieren. Verwenden Sie diese Option bei der Entwicklung auf Linux-Systemen, die keine Dateisynchronisierung für die lokale Docker-Entwicklung erfordern. Siehe [Daten in der Docker-Umgebung synchronisieren](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![neues Symbol](../../assets/new.svg) Die Standardeinstellung für die Dateisynchronisierung wurde von `docker-sync` in `native` geändert. [Fehlerbehebung, die von Mathew Beane von Zilker Technology eingereicht wurde](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![neues Symbol](../../assets/new.svg) **Verbesserungen bei der Validierung**—

   - ![neues Symbol](../../assets/new.svg) Dem Bereitstellungsprozess für lokale Docker-Entwicklungsumgebungen wurde eine Validierung hinzugefügt, um sicherzustellen, dass die Cloud-Umgebungskonfiguration den zum Entschlüsseln der Datenbank erforderlichen Verschlüsselungsschlüssel enthält. Jetzt erhalten Sie eine Fehlermeldung im Protokoll, wenn die Umgebungskonfiguration keinen Wert für den Verschlüsselungsschlüssel angibt.<!--MAGECLOUD-4423-->

   - ![neues Symbol](../../assets/new.svg) Dem Elasticsearch-Dienst wurde eine Konsistenzprüfung des Containers hinzugefügt, um sicherzustellen, dass der Dienst bereit ist, bevor die Build- und Bereitstellungsverarbeitung fortgesetzt wird. Wenn die Konsistenzprüfung einen Fehler zurückgibt, wird der Container automatisch neu gestartet.<!--MAGECLOUD-4456-->
