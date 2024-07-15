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
>Diese Versionshinweise enthalten Informationen und Aktualisierungen für `ece-tools` v2002.0.22 und höher. Unter [Versionshinweise für Cloud Tools Suite](cloud-tools-suite.md) finden Sie die neuesten Updates für `ece-tools` und andere Cloud-Pakete.

## v2002.0.22

Die Version `ece-tools` 2002.0.22 ändert die Struktur des `ece-tools` -Pakets, um die Freigabe von `Adobe Commerce on cloud infrastructure` -Patches aus der ECE-Tools-Version zu entkoppeln. Ab dieser Version werden Patches und wichtige Fehlerbehebungen mit dem Paket [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) bereitgestellt, das eine neue Abhängigkeit für das Paket `ece-tools` darstellt. Wir haben diese Änderungen vorgenommen, um die Komplexität bei der Planung von Release-Updates und der Arbeit mit Community-Beiträgen zu reduzieren.

- ![neues Symbol](../../assets/new.svg) **Änderungen am ECE-Tools-Paket**

   - ![neues Symbol](../../assets/new.svg) Die Adobe Commerce-Patches wurden aus dem `ece-tools` -Paket in ein neues [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) Composer-Paket verschoben.

   - ![neues Symbol](../../assets/new.svg) Die Datei `composer.json` für das Paket `ece-tools` wurde aktualisiert, um eine Abhängigkeit für das Paket `magento/magento-cloud-patches` v1.0.0 hinzuzufügen.

   - ![Fixsymbol](../../assets/fix.svg) Korrektur eines Fehlers, der dazu führte, dass der `ece-tools`-Patchprozess beim Anwenden von Patch-Sets auf reinen Sicherheitsversionen, beginnend mit Version 2.3.2-p2 und höher, fehlschlug. Dieses Problem wurde durch das neue Versionierungssystem eingeführt, das für [Nur-Sicherheit-Patches](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches) eingeführt wurde.<!--MAGECLOUD-4661-->

- ![ Symbol Fehlerbehebung](../../assets/fix.svg) **Patches und wichtige Fehlerbehebungen** - Aktualisieren Sie Ihre Cloud-Umgebungen mit der Version 2002.0.22 von `ece-tools` , um die folgenden Patches und wichtigen Fehlerbehebungen anzuwenden. Diese Patches sind im Paket `magento/magento-cloud-patches` v1.0.0 enthalten.

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Seiten-Builder-Sicherheits-Patches für die Versionen 2.3.1.x und 2.3.2.x**-behebt ein Problem in der Seitenaufbau-Vorschau, das es nicht authentifizierten Benutzern ermöglicht, auf einige Vorlagenmethoden zuzugreifen, die zum Trigger beliebiger Code-Ausführung über das Netzwerk (RCE) verwendet werden können, was zu globalen Informationslecks führt. Dieses Problem kann auftreten, wenn nicht unterstützte Versionen von Page Builder mit den Adobe Commerce-Versionen 2.3.1 und 2.3.2 verwendet werden.<!--MAGECLOUD-4649-->

   - ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) **MSI-Patches** - Behebt Probleme, die bei der Verwendung der standardmäßigen Lagerbestandseinstellungen für die Verwaltung von Lagern zu Indizierungsfehlern und Leistungsproblemen führten.<!--MAGECLOUD-4428-->

   - ![Fixsymbol](../../assets/fix.svg) **Abwärtskompatibilität der neuen E-Mail-Schnittstellen**-behebt ein Abwärtskompatibilitätsproblem, das durch die in Adobe Commerce v2.3.3 eingeführte `Magento\Framework\Mail\EmailMessageInterface` PHP-Schnittstelle verursacht wurde. Im Rahmen dieses Patches erbt der neue `EmailMessageInterface` die alten `MessageInterface`, und die Kernmodule von Adobe Commerce werden wieder von `MessageInterface` abhängig gemacht.<!--MAGECLOUD-4422-->

   - ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) **Die Katalogpaginierung funktioniert nicht in Elasticsearch 6.x** - behebt ein kritisches Problem mit der Seitennummerierung der Suchergebnisse, das Kunden betrifft, die Elasticsearch 6.x als Katalogsuchmaschine verwenden.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - ![neues Symbol](../../assets/new.svg) **Neue Docker-Bilder** - Unterstützt von Versionen 2.3.3 und höher<!-- MAGECLOUD-3345 -->

      - PHP-Version 7.3.<!-- MAGECLOUD-4017 -->

      - Varnish Cache 6.2.0<!-- MAGECLOUD-4017 -->

   - ![neues Symbol](../../assets/new.svg) Unterstützung zum Anwenden der in `.magento.app.yaml` der Docker-Umgebung angegebenen benutzerdefinierten Hook-Konfiguration hinzugefügt. Zuvor unterstützte die Docker-Umgebung nur die standardmäßige Hook-Konfiguration.<!-- MAGECLOUD-3505-->

   - ![neues Symbol](../../assets/new.svg) Docker-ENV-Dateien werden während des Docker-Builds nicht mehr generiert und der Befehl `docker:config:convert` wird nicht mehr unterstützt. Die entsprechenden Daten werden jetzt in der Datei `docker-compose.yml` gespeichert.<!-- MAGECLOUD-3816-->

   - ![neues Symbol](../../assets/new.svg) **Aktualisiertes PHP-Bild** -Node.js wurde zum PHP-Docker-Bild hinzugefügt, um die Funktionen node, npm und grunt-cli zu unterstützen.<!-- MAGECLOUD-3953 -->

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**-

   - ![neues Symbol](../../assets/new.svg) Die Bereitstellungsvariable **LOCK_PROVIDER** wurde hinzugefügt, um den Sperranbieter zu konfigurieren, der den Start doppelter Cron-Aufträge und Cron-Gruppen verhindert. Weitere Informationen finden Sie in der Variablenbeschreibung im Thema [Bereitstellungsvariablen](../environment/variables-deploy.md#lock_provider).<!-- MAGECLOUD-4052 -->

   - ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable **CONSUMERS_WAIT_FOR_MAX_MESSAGES** wurde hinzugefügt, um zu konfigurieren, wie Verbraucher Meldungen aus der Nachrichtenwarteschlange verarbeiten, wenn sie die Umgebungsvariable `CRON_CONSUMERS_RUNNER` zur Verwaltung von Cron-Aufträgen verwenden. Weitere Informationen finden Sie in der Variablenbeschreibung im Thema [Bereitstellungsvariablen](../environment/variables-deploy.md#consumers_wait_for_max_messages).<!-- MAGECLOUD-4071 -->

   - ![Symbol zur Fehlerbehebung](../../assets/fix.svg) Es wurde ein Problem behoben, das zu Fehlern bei Datenbank-Deadlock führen konnte, wenn der `consumers_runner` Cron-Auftrag mehrere Instanzen desselben Verbrauchers auf verschiedenen Knoten startet. Wenn Sie jetzt die Bereitstellungsvariable [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) in Ihrer Umgebung aktiviert haben, verwendet der `consumers_runner` -Auftrag die Option `single-thread` , um eine Instanz jedes Verbrauchers auf nur einem Knoten zu starten.<!-- MAGECLOUD-3913 -->

   - ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das sich auf die Funktionalität von [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) auswirkte und eine standardmäßige Store-URL verwendete. Wenn der Befehl `config:show:default-url` jetzt keine Basis-URL abrufen kann, wird die URL aus der Variablen MAGENTO_CLOUD_ROUTES verwendet.<!-- MAGECLOUD-3866 -->

- ![neues Symbol](../../assets/new.svg) Die vom Befehl `module:refresh` zurückgegebenen Protokollierungsinformationen wurden aktualisiert. Jetzt können Sie eine detaillierte Liste der aktivierten Module in der Datei `cloud.log` sehen.<!-- MAGECLOUD-2514 -->

- ![neues Symbol](../../assets/new.svg) Verbesserte Validierung der Versionskompatibilität und Warnhinweise für Kompatibilitätsprobleme zwischen der Adobe Commerce-Version und installierten Diensten, z. B. Elasticsearch, [!DNL RabbitMQ], Redis und DB<!-- MAGECLOUD-3535 -->.

- ![neues Symbol](../../assets/new.svg) Unterstützung für RabitMQ Version 3.8 hinzugefügt.<!-- MAGECLOUD-4674-->

- ![neues Symbol](../../assets/new.svg) Aktualisierte interaktive Validierungen für die Dienstkompatibilität, um unterstützte Versionen für die neuen Adobe Commerce-Versionen 2.3.3 und 2.2.10 widerzuspiegeln. Empfohlene Versionen finden Sie unter [Systemanforderungen](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) im _Installationshandbuch_ .<!-- MAGECLOUD-4018 -->

- ![Fixsymbol](../../assets/fix.svg) Die Protokollmeldung, die zurückgegeben wird, wenn der Cron-Auftragsverwaltungsprozess in der Bereitstellungsphase versucht, einen bereits abgeschlossenen Cron-Auftrag zu stoppen, wurde verbessert, um zu klären, dass dieses Problem kein Fehler ist. Die Protokollebene wurde von `INFO` in `DEBUG` geändert.<!-- MAGECLOUD-3653-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem bei der Ausführung des Befehls `setup:upgrade` behoben, das den Bereitstellungsprozess nicht unterbrochen hat, wenn während der Aufgabe `app:config:import` ein Fehler aufgetreten ist.<!-- MAGECLOUD-3806 -->

- ![neues Symbol](../../assets/new.svg) Die standardmäßige Protokollebene für den Datei-Handler wurde zu `debug` geändert, um die Detailmenge im Protokoll zu reduzieren, das in der [!DNL Cloud Console] angezeigt wird, und trotzdem detaillierte Informationen für das Debugging bereitgestellt.<!-- MAGECLOUD-3871 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das bei der Bereitstellung statischer Inhalte während des Builds einen Fehler verursachte. Nach einer Installation und einem `ece-tools` Konfigurationsdump trat ein Fehler auf, wenn in der Datei `config.php` kein Gebietsschema für den Admin-Benutzer angegeben war. Jetzt gibt es ein standardmäßiges Gebietsschema für den Admin-Benutzer in der Datei `config.php`<!-- MAGECLOUD-3957 -->.

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines `Undefined index error` , der auftritt, wenn ein `magento-cloud` CLI-Befehl in einer Umgebung fehlschlägt, die nicht mit einer sicheren URL (https) konfiguriert ist. Das ECE-Tools-Paket verwendet jetzt die Basis-URL (http), wenn die sichere URL nicht verfügbar ist.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![neues Symbol](../../assets/new.svg) **Docker-Aktualisierungen**—

   - ![neues Symbol](../../assets/new.svg) Sie können jetzt Funktionstests mit dem Paket `ece-tools` in der Docker-Umgebung durchführen. Siehe [Anwendungstests](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![neues Symbol](../../assets/new.svg) Unterstützung für die Konfiguration von PHP-Modulen mithilfe der `.magento.app.yaml` -Datei hinzugefügt. Alle [PHP-Erweiterungen, die in der `.magento.app.yaml`-Datei](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) angegeben sind, stehen in den Docker-PHP-Containern zur Verfügung.<!-- MAGECLOUD-3357 -->

   - ![neues Symbol](../../assets/new.svg) Es stehen neue Befehle zur Verbesserung des Docker-Befehlszeilenerlebnisses zur Verfügung. Siehe Abschnitt [`bin/magento-docker` der Docker-Referenz](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![neues Symbol](../../assets/new.svg) Es wurde die Möglichkeit hinzugefügt, Mutagen.io zum Synchronisieren von Dateien während der Entwicklung zwischen dem lokalen Host und Docker zu verwenden.<!-- MAGECLOUD-3559 -->

   - ![Fixsymbol](../../assets/fix.svg) Korrektur des Standardpfads bei Verwendung der Docker-Umgebung. Wenn Sie sich jetzt mit SSH beim Docker-Container anmelden, befinden Sie sich wie erwartet im Projektstamm im Ordner &quot;`/app`&quot;.<!-- MAGECLOUD-3582 -->

   - ![Fixsymbol](../../assets/fix.svg) Die Natrium-Bibliothek wurde von Version 1.0.11 auf Version 1.0.18 aktualisiert und die Sodium-PHP-Erweiterung aktualisiert.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Kunden von Adobe Commerce in der Cloud-Infrastruktur müssen vor der Aktualisierung auf Adobe Commerce 2.3.2 ein Adobe Commerce-Support-Ticket senden ](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket), um das libNatrium-Paket in den Produktions- und Staging-Umgebungen zu aktualisieren. Derzeit können Sie keine Starter-Umgebungen auf Adobe Commerce 2.3.2 aktualisieren.[

   - ![Fixsymbol](../../assets/fix.svg) Das Elasticsearch-Plugin `analysis-icu` und das `analysis-phonetic` wurden zu allen Docker-Bildern hinzugefügt.<!-- MAGECLOUD-3446 -->

   - ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Verbesserte Validierungen: Wenn Sie Optionen für den Befehl `docker:build` verwenden, müssen Sie bei Verwendung einer Option einen Wert angeben. Außerdem wurde eine Validierung für die Knotenversion bei Verwendung des Befehls `docker:build run` hinzugefügt.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![neues Symbol](../../assets/new.svg) Unterstützung für Datenbanktabellenpräfixe mit der Umgebungsvariablen [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) hinzugefügt.<!-- MAGECLOUD-2901 -->

   - ![neues Symbol](../../assets/new.svg) Die Bereitstellungsvariable **FORCE_UPDATE_URLS** wurde hinzugefügt, um Basis-URLs bei der Bereitstellung in Produktions- und Staging-Umgebungen für Pro und Starter zu aktualisieren. Siehe Definition im Inhalt [Variablen bereitstellen](../environment/variables-deploy.md#force_update_urls).<!-- MAGECLOUD-3602 -->

   - ![neues Symbol](../../assets/new.svg) Die Variable **TTFB_TESTED_PAGES** nach der Bereitstellung wurde hinzugefügt, um die Seitentests _Time to First Byte_ zu konfigurieren und so die Anwendungsleistung auf in der Cloud-Infrastruktur bereitgestellten Sites zu überprüfen. Siehe Variablenbeschreibung in [Variablen nach der Bereitstellung ](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![Fixsymbol](../../assets/fix.svg) Korrektur eines Problems mit Multi-Thread-SCD, das zu zufälligen Fehlern bei der Bereitstellung statischer Inhalte führte. Um dieses Problem zu umgehen, musste die Variable **SCD_THREADS** auf `1` gesetzt werden. Sie können jetzt die Anzahl nach Bedarf erhöhen. Siehe Definitionen in den [Variablen bereitstellen](../environment/variables-deploy.md#scd_threads) und den [Build-Variablen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![Fixsymbol](../../assets/fix.svg) Sie können die Umgebungsvariable **WARM_UP_PAGES** so konfigurieren, dass einzelne Seiten, mehrere Domänen und mehrere Seiten zwischengespeichert werden. Siehe die erweiterte Definition im Inhalt [Variablen nach der Bereitstellung](../environment/variables-post-deploy.md#warm_up_pages).<!-- MAGECLOUD-3258 -->

- ![Fixsymbol](../../assets/fix.svg) Die Datei `pub/static/.htaccess` wurde zur Ausschlussliste hinzugefügt. [Fehlerbehebung, eingereicht von Björn Kraus von der PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Fehlers, der auftrat, wenn alle Validierungsmeldungen als `Critical` angezeigt wurden, wenn mindestens ein Validator auf kritischer Ebene einen Fehler zurückgab.<!-- MAGECLOUD-3178 -->

- ![Symbol zur Fehlerbehebung](../../assets/fix.svg) Es wurde ein Problem behoben, das zu einem Bereitstellungsfehler führte, wenn die Basis-URL nicht in der Datenbank vorhanden war.<!-- MAGECLOUD-3075 -->

- ![neues Symbol](../../assets/new.svg) Dem Paket `ece-tools` wurde ein neuer **`env:config:show`Befehl** hinzugefügt, der Umgebungsdienste, Routen oder Variablen anzeigt. Siehe [Dienste, Routen und Variablen](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Von Vladimir Kerkhoff gesendete Funktion](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das einen kritischen Fehler verursachte, wenn versucht wurde, Adobe Commerce 2.2.6 oder früher mit `ece-tools` zu installieren, nachdem die Shell-Umgestaltung abgeschlossen wurde.<!-- MAGECLOUD-3665 -->

- ![Symbol zur Fehlerbehebung](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem Installationen von Adobe Commerce 2.1.x und 2.2.x fehlschlugen und eine Warnung angezeigt wurde, dass eine veraltete Version von Carbon verwendet wurde.<!-- MAGECLOUD-3704 -->

- ![Fixsymbol](../../assets/fix.svg) Verringerte die `cloud.log` Protokollebene für die Shell-Ausgabe von `info` auf `debug`.<!-- MAGECLOUD-3277 -->

- ![Fixsymbol](../../assets/fix.svg) Die Option `--remove-definers (-d)` wurde zum Befehl `ece-tools db-dump` hinzugefügt, um Definer aus der Dump-Datei zu entfernen.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das die `env.php` -Datei während einer Bereitstellung überschrieben wurde, was zu einem Verlust benutzerdefinierter Konfigurationen führte. Durch diese Aktualisierung wird sichergestellt, dass Adobe Commerce in der Cloud-Infrastruktur die `env.php` -Datei bei jeder Bereitstellung aktualisiert und benutzerdefinierte Konfigurationen beibehalten.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![neues Symbol](../../assets/new.svg) **Docker-Aktualisierungen**—

   - ![neues Symbol](../../assets/new.svg) Die Docker-Umgebung unterstützt jetzt die Cron-Konfiguration, die in der Eigenschaft [crons der Datei .magento.app.yaml definiert ist](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![neues Symbol](../../assets/new.svg) **Neuer Docker-Container**: Es wurde ein [TLS-Terminierungsproxy-Container](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) hinzugefügt, um die unterschiedliche SSL-Beendigung über HTTPS zu erleichtern.<!-- MAGECLOUD-2890 -->

   - ![neues Symbol](../../assets/new.svg) **Neues Docker-Bild**: Es wurde ein Node.js-Bild hinzugefügt, um Gulp und andere Funktionen wie Jasmine JS Unit Testing zu unterstützen.<!-- MAGECLOUD-3345 -->

   - ![neues Symbol](../../assets/new.svg) **Docker-Build-Modi** - Jetzt können Sie die Docker-Umgebung im [Produktionsmodus oder Entwicklermodus](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode) starten. Der Entwicklermodus unterstützt die aktive Entwicklung mit vollständigen, beschreibbaren Dateisystemberechtigungen.<!-- MAGECLOUD-3152/3511 -->

   - ![Fixsymbol](../../assets/fix.svg) Korrektur des Fehlers, der dazu geführt hat, dass die Docker-Bereitstellung mit einem `Name or service not known` -Fehler fehlschlug, wenn der Cache für einen Dienst konfiguriert ist, der nicht verfügbar ist. Jetzt können Sie einen Dienst aus der [`.magento/services.yaml`-Datei](https://devdocs.magento.com/cloud/project/services.html) entfernen. Der Docker-Konfigurationsgenerator aktualisiert den Dienst in der Datei `docker/config.php.dist` automatisch.<!-- MAGECLOUD-3369 -->

   - ![neues Symbol](../../assets/new.svg) Interaktive Validierungen zur Dienstkompatibilität hinzugefügt. Wenn ein angeforderter Dienst nun mit der Adobe Commerce-Version oder anderen Diensten inkompatibel ist, wird der Benutzer im _interaktiven Modus_ aufgefordert, eine Meldung zu erhalten und die Wahl zu treffen, um fortzufahren. Siehe die für Docker verfügbaren [Dienstversionen](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers). Verwenden Sie die Option &quot;`-n`&quot;, um die Interaktivität für CICD-Zwecke zu überspringen.<!-- MAGECLOUD-3251 -->

   - ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit dem Befehl Docker compse `db-dump` behoben, durch den vorhandene Dumps gelöscht wurden.<!-- MAGECLOUD-3366 -->

   - ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem die Cache-Speicher für Redis `session`, `default` und `page_cache` derselben Datenbank-ID zugewiesen wurden.<!-- MAGECLOUD-3172 -->

- ![neues Symbol](../../assets/new.svg) **Aktualisierungen der Umgebungsvariablen**—

   - ![neues Symbol](../../assets/new.svg) Die neue Umgebungsvariable **ELASTICSUITE\_CONFIGURATION** behält Ihre angepassten Diensteinstellungen zwischen Bereitstellungen bei. Siehe Definition im Inhalt [Variablen bereitstellen](../environment/variables-deploy.md#elasticsuite_configuration).<!-- MAGECLOUD-3205 -->

   - ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable **SCD_MAX_EXECUTION_TIMEOUT** wurde hinzugefügt, sodass Sie die Zeit für den Abschluss der Bereitstellung statischer Inhalte aus der `.magento.env.yaml`-Datei erhöhen können. Siehe Definition in den [Variablen bereitstellen](../environment/variables-deploy.md#scd_max_execution_time), den [Build-Variablen](../environment/variables-build.md#scd_max_execution_time) und den [globalen Variablen](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![neues Symbol](../../assets/new.svg) Die Umgebungsvariable **MAGENTO_CLOUD_LOCKS_DIR** wurde hinzugefügt, um den Pfad zum Bereitstellungspunkt für den Sperranbieter in der Cloud-Infrastruktur zu konfigurieren. Der Sperranbieter verhindert den Start doppelter Cron-Aufträge und Cron-Gruppen. Diese Variable wird von Adobe Commerce-Version 2.2.5 und höher unterstützt und automatisch konfiguriert. Siehe Definition in [Cloud-Variablen](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![Fixsymbol](../../assets/fix.svg) Die Standardwerte der Umgebungsvariablen **SCD_THREADS** wurden geändert, um den optimalen Wert basierend auf der erkannten CPU-Thread-Anzahl automatisch zu bestimmen. Siehe aktualisierte Definitionen in den [Variablen bereitstellen](../environment/variables-deploy.md#scd_threads) und den [Build-Variablen](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem mit einem Patch für den DB-Isolationsmechanismus behoben, das beim Aktualisieren auf Adobe Commerce in der Cloud-Infrastruktur-Version 2002.0.16 einen Fehler verursachte.<!-- MAGECLOUD-3383 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Patch hinzugefügt, der _Google Image Charts_ durch _Image-Charts_ ersetzt. Weitere Informationen finden Sie im Artikel &quot;DevBlog&quot;[Google Image Charts - Einstellung und Aktualisierung für M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![Fixsymbol](../../assets/fix.svg) Validierung für die Variable [SEARCH_CONFIGURATION](../environment/variables-deploy.md#search_configuration) hinzugefügt. Die Bereitstellung schlägt fehl, wenn die Option &quot;Engine&quot;nicht festgelegt ist und `_merge` nicht erforderlich ist.<!-- MAGECLOUD-3470 -->

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das sensible Daten nach einem Ausnahmefehler angezeigt wurden. Jetzt werden die sensiblen Informationen entsprechend maskiert.<!-- MAGECLOUD-3525 -->

- ![Fixsymbol](../../assets/fix.svg) Die fehlertoleranten Einstellungen des Magento Open Source-Packages wurden verbessert. Falls Adobe Commerce keine Daten aus der Redis `slave` -Instanz lesen kann, wird eine Lektion aus der Redis `master` -Instanz durchgeführt. Siehe [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>Die `ece-tools` -Version 2002.0.17 enthält einen wichtigen Sicherheits-Patch. Siehe [Technische Ressourcen: Magento Open Source Patches](https://magento.com/tech-resources/download#download2288).

- ![neues Symbol](../../assets/new.svg) **Dienstaktualisierungen** - Unterstützt von den folgenden Adobe Commerce-Versionen: 2.2.8 und höher 2.2.x, 2.3.1 und höher 2.3.x

   - Elasticsearch-Version 6.x.<!-- MAGECLOUD-3196 --> wird nun unterstützt.

   - Unterstützung für Redis Version 5.0 hinzugefügt.

- ![neues Symbol](../../assets/new.svg) **Neue Docker-Bilder**: Der Docker-Build wurde um die folgenden Dienste erweitert:

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable** - Zuvor gab es eine hartcodierte Zeitüberschreitung für die SCD-Komprimierung. Jetzt können Sie das SCD-Komprimierungs-Timeout mithilfe der Umgebungsvariablen **SCD_COMPRESSION_TIMEOUT** konfigurieren. Siehe Definitionen in den [Build-Variablen](../environment/variables-build.md#scd_compression_timeout) und im Inhalt [deploy variables](../environment/variables-deploy.md#scd_compression_timeout) .<!-- MAGECLOUD-2870 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Die Option `--use-rewrites` wurde zum Installationsbefehl hinzugefügt, sodass Webserver-Neuschreibungen für generierte Links in der Storefront und Administratorzugriff verwendet werden, um die Sicherheit und das Kundenerlebnis zu verbessern.<!-- MAGECLOUD-3246 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Der Datei `var/log/install_upgrade.log` wurden Zeitstempel hinzugefügt, sodass sie Daten für Installations- und Aktualisierungsereignisse anzeigt.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - Die in der Docker-Umgebung generierte Standarddienstkonfiguration entspricht nun der Standardkonfiguration in der Cloud-Vorlage.<!-- MAGECLOUD-3025 -->

   - Sie können E-Mails aus Ihrer Docker-Umgebung mit dem Dienst `sendmail` senden.<!-- MAGECLOUD-2907 -->

   - Es wurde die Möglichkeit hinzugefügt, [Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) zum Debugging in der Cloud-Docker-Umgebung zu konfigurieren.<!-- MAGECLOUD-2891 -->

   - Fehlerkorrektur - Beim Generieren der `docker-compose.yml` -Datei tritt jetzt kein Fehler mehr mit den Webdienstberechtigungen auf.<!-- MAGECLOUD-2883 -->

- ![neues Symbol](../../assets/new.svg) **Verbesserung der Aktualisierung**: Es wurde eine Validierung hinzugefügt, um sicherzustellen, dass die Eigenschaft `autoload` in der Datei `composer.json` die erforderlichen Konfigurationsänderungen enthält, bevor auf Adobe Commerce v2.3 aktualisiert wird. Siehe [Upgrade der Version](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![neues Symbol](../../assets/new.svg) Der Komprimierungsprozess bei der Bereitstellung statischer Inhalte umfasst jetzt alle - nativ generierten oder angepassten - Assets und erfolgt während der Build-Phase zu Beginn des [`build:transfer` -Abschnitts](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Zuvor trat der Komprimierungsprozess auf, bevor eine benutzerdefinierte Minimierung und Bündelung von statischen Assets angewendet wurde. [Fehlerbehebung, eingereicht von Rafael Garcia Lepper von Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Fehlers bei der Datenbankverbindung, der während der Bereitstellung unmittelbar nach dem Konfigurieren einer zusätzlichen Datenbank- und Dienstbeziehung auftrat. Mit dieser Fehlerbehebung wird auch ein Problem behoben, das während des Konfigurationsprozesses von Commerce Reporting für Starter aufgetreten ist. Für Starter ist dieses Upgrade ein &quot;Muss vorhanden&quot;für die Verwendung der Commerce-Berichterstellung.<!-- MAGECLOUD-3035 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Korrektur eines Validierungsproblems mit der Datenbankkonfiguration, das dazu führte, dass der Bereitstellungsprozess fehlschlug.<!-- MAGECLOUD-3003 -->

- ![Fixsymbol](../../assets/fix.svg) Die Einschränkung wurde mit der entsprechenden Version des `symfony/yaml`-Pakets aktualisiert, um sie mit [PHP-Konstanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) zu verwenden. Das ständige Parsen funktioniert nicht, wenn eine `symfony/yaml` -Paketversion verwendet wird, die älter als 3.2 ist. [Fehlerbehebung, die von Vladimir Kerkhoff eingereicht wurde](https://github.com/magento/ece-tools/pull/404)<!-- MAGECLOUD-2956 -->

- ![neues Symbol](../../assets/new.svg) **Überprüfung der Umgebungskonfiguration**—Es wurde eine Validierung hinzugefügt, um die PHP-Version zu überprüfen und Benutzer zu warnen, wenn sie nicht die neueste empfohlene Version verwenden.<!--MAGECLOUD-2903-->

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem bei der Verarbeitung von falsch formatierten JSON-Variablen behoben. Wenn nun eine JSON-Variable einen Syntaxfehler verursacht, wird in der Datei `cloud.log` eine Warnung angezeigt und die Bereitstellung wird mit der Standardvariablen<!-- MAGECLOUD-2851 --> fortgesetzt.

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Verbindungsfehler behoben, der während der Bereitstellung unmittelbar nach der Deaktivierung des Redis-Dienstes auftrat.<!-- MAGECLOUD-2747 -->

- ![neues Symbol](../../assets/new.svg) **Änderungen protokollieren** - Die [Protokollebene](../environment/log-handlers.md#log-levels) wurde für die folgenden Build- und Bereitstellungs-Prozessereignisse von `Info` in `Notice` aktualisiert:<!--MAGECLOUD-2925-->

   - Starten und beenden Sie den Prozess zur Abstimmung der in `composer.json` installierten Module mit den freigegebenen Konfigurationseinstellungen in der Datei `app/etc/config.php`

   - Beginn und Ende des Konfigurationsvalidierungsprozesses

   - Starten und Ende des `setup:di:compile`-Prozesses zum Generieren von Klassen

- ![neues Symbol](../../assets/new.svg) **Neue Umgebungsvariablen**—

   - **[RESOURCE_CONFIGURATION deploy variable](../environment/variables-deploy.md#resource_configuration)** - Verwenden Sie diese Variable, um einen Ressourcennamen einer Datenbankverbindung zuzuordnen.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION global variable](../environment/variables-global.md#x_frame_configuration)**: Mit dieser Variablen können Sie die `X-Frame-Options` -Header-Konfiguration für das Rendern einer Adobe Commerce-Seite in einem `<frame>`, `<iframe>` oder `<object>` ändern.<!-- MAGECLOUD-3048 -->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierungen der Umgebungsvariablen** - Änderung der folgenden Umgebungsvariablen:

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**: Die Funktion zum Vorausfüllen des Caches für bestimmte Seiten auf allen Domänen, die für einen Adobe Commerce-Store definiert sind, wurde hinzugefügt. Wenn Ihre Site zuvor mit mehreren Domänen konfiguriert war, konnte der Prozess nach der Bereitstellung den Cache für die angegebenen Seiten auf nicht standardmäßigen Domänen nicht vorab laden und gab den folgenden Fehler im Protokoll nach der Bereitstellung zurück: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**: Die Dokumentation und die Beispieldatei `.magento.env.yaml` wurden mit den richtigen Standardwerten für die SCD-Komprimierungsstufe aktualisiert. Siehe Definitionen in den [Build-Variablen](../environment/variables-build.md#scd_compression_level) und im Inhalt [deploy variables](../environment/variables-deploy.md#scd_compression_level) .<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES** - Diese Umgebungsvariable wird nicht mehr unterstützt. Verwenden Sie [SCD_MATRIX](../environment/variables-build.md#scd_matrix), um die Designkonfiguration zu steuern.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX** - Der Validierungsprozess wurde korrigiert, um ein Problem zu verhindern, das auftrat, wenn SCD_MATRIX einen Designwert ignorierte, der unterschiedliche Zeichenfälle enthielt. Siehe Definitionen in den [Build-Variablen](../environment/variables-build.md#scd_matrix) und im Inhalt [deploy variables](../environment/variables-deploy.md#scd_matrix) .<!-- MAGECLOUD-2904 -->

   - **ADMIN-Variablen**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Verbesserte Sicherheit bei der Verwaltung von Anmeldeinformationen für den Admin-Benutzer mithilfe von Umgebungsvariablen. Sie können die Umgebungsvariablen ADMIN_EMAIL, ADMIN_USERNAME und ADMIN_PASSWORD nicht mehr verwenden, um Administratorberechtigungen bei Upgrades zu überschreiben. Wenn Sie nicht auf das Admin-Bedienfeld zugreifen können, verwenden Sie die Funktion &quot;_Kennwort vergessen_&quot;oder den CLI-Befehl &quot;`admin:user:create`&quot;, um einen neuen Admin-Benutzer zu erstellen. Siehe [Zugriff auf Ihr Admin-Bedienfeld](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL ist beim Aktualisieren oder Anwenden von Patches nicht mehr erforderlich.

## v2002.0.15

- ![neues Symbol](../../assets/new.svg) **Docker-Updates**—

   - Jetzt verwendet der Docker-Generator die in den Konfigurationsdateien `.magento.app.yaml` und `.magento/services.yaml` angegebenen Dienste, wenn [Ihre Docker-Umgebung erstellen](https://devdocs.magento.com/cloud/docker/docker-config.html). Sie können mithilfe von Build-Parametern eine andere Dienstversion auswählen.<!-- MAGECLOUD-2888 -->

   - PHP 7.2-Image hinzugefügt - Unterstützung für PHP 7.2 in Cloud Docker hinzugefügt; die [Launch Docker-Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) wurde aktualisiert und enthält nun die `docker:build --php` -Option, um die PHP-Version anzugeben, die mit Ihrer Adobe Commerce-Version kompatibel ist.<!-- MAGECLOUD-2799 -->

   - Es wurde ein [Cron-Container](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) hinzugefügt, der auf dem PHP-CLI-Bild basiert.<!-- MAGECLOUD-2565 -->

   - Die folgenden Dienste wurden zum Docker-Build hinzugefügt:

      - [!DNL RabbitMQ] 3,5 und 3,7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 und 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 und 4.0<!-- MAGECLOUD-2886 -->

- ![neues Symbol](../../assets/new.svg) **Mit PHP-Konstanten konfigurieren**—Es wurde Unterstützung für [PHP-Konstanten](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) in der Konfigurationsdatei `.magento.env.yaml` hinzugefügt.<!-- MAGECLOUD- 2575 -->

- ![neues Symbol](../../assets/new.svg) **Neue Umgebungsvariable** - Standardmäßig sind nur die Google Analytics in der Produktionsumgebung aktiviert. Sie können Google Analytics in den Staging- und Integrationsumgebungen mithilfe der Umgebungsvariablen [ENABLE_GOOGLE_ANALYTICS_1}<!--MAGECLOUD-2879--> aktivieren.](../environment/variables-deploy.md#enable_google_analytics)

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das benutzerdefinierte Cron-Konfigurationen nach einer Neubereitstellung aus der `env.php` -Datei entfernt wurden. Jetzt bleiben benutzerdefinierte Cron-Konfigurationen sicher in der Datei `env.php`.<!-- MAGECLOUD-2923 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurden Inkonsistenzen in den Nachrichten und [Protokollebenen](../environment/log-handlers.md#log-levels) in den Build-, Bereitstellungs- und Post-Bereitstellungsphasen behoben. Die Protokollierungsebenen für Anfang und Ende der Protokollmeldungen wurden für alle Phasen und Unterphasen von **info** auf **notice** erhöht. Logmeldungen für Anfang und Ende wurden hinzugefügt, sofern zutreffend.<!-- MAGECLOUD-2919 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem mit Cron-Prozessen behoben, das den Start der Phase nach der Bereitstellung, wenn konfiguriert, verhinderte. Wenn Sie jetzt den Hook für die Bereitstellung aktiviert haben, werden die Cron-Prozesse zu Beginn der Phase nach der Bereitstellung erneut aktiviert.<!-- MAGECLOUD-2862 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das eine erfolgreiche Installation von Adobe Commerce bei der Angabe einer benutzerdefinierten Datenbankkonfiguration verhinderte. Zuvor verwendete der Installationsprozess die Datenbankkonfiguration aus der Variable [MAGENTO_CLOUD_RELATIONSHIP Variable](../environment/variables-cloud.md), selbst wenn Sie in der Umgebungsvariablen [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) benutzerdefinierte Verbindungsinformationen angegeben haben.<!--MAGECLOUD-2736-->

- ![Fixsymbol](../../assets/fix.svg) Korrektur des Befehls `config:dump`, sodass jedes Website-Gebietsschema im Abschnitt `system` der `config.php`-Datei enthalten ist.<!--MAGECLOUD-2740-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das während der Phase nach der Bereitstellung zu Fehlern beim _Aufwärmen_ führte, indem die Quell-Basis-URL-Referenz korrigiert wurde.<!--MAGECLOUD-2797-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das Dateien während des `setup:di:compile`-Prozesses nicht korrekt generiert wurden, was sich auf das Amazon-Zahlungsmodul auswirkte.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![neues Symbol](../../assets/new.svg) **Ideal State verifizieren** - Der `ideal-state`-Assistent überprüft jetzt die aktuelle Konfiguration bei jeder Bereitstellung und enthält klare Anweisungen zum Aktualisieren der Konfiguration, um eine schnellere Bereitstellung ohne Ausfallzeiten zu erzielen.<!--MAGECLOUD-2372-->

- ![Fixsymbol](../../assets/fix.svg) **PCI Compliance**: Die Nachrichtenprotokolle für Adobe Commerce in der Cloud-Infrastruktur wurden aktualisiert und erfordern jetzt bei der Verbindung mit Drittanbieter-Messaging-Diensten die Transport Layer Security (TLS)-Version 1.2. Wenn Sie einen Nachrichtendienst verwenden, der TLS Version 1.2 nicht unterstützt, müssen Sie Ihren Dienst aktualisieren. Andernfalls wird die folgende Fehlermeldung angezeigt, wenn Ihre Adobe Commerce-Anwendung versucht, eine Verbindung zum Nachrichtenserver herzustellen, um eine E-Mail zu senden: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![neues Symbol](../../assets/new.svg) **Verbesserung der Implementierung**: Es wurde eine Validierung hinzugefügt, die Kunden warnt, wenn in einer Staging- oder Produktionsumgebung die Optionen `dev`, `debug` oder `debug_logging` aktiviert sind, um Leistungsprobleme zu vermeiden, die durch übermäßige Protokollierungsaktivitäten verursacht werden.<!--MAGECLOUD-2517-->

- ![Fixsymbol](../../assets/fix.svg) **Fehlerbehebungen bei der Bereitstellung**—

   - Der Wartungsmodus ist jetzt zu Beginn der Bereitstellungsphase aktiviert und am Ende deaktiviert. Wenn die Bereitstellung fehlschlägt, bleibt die Site im Wartungsmodus, bis die Bereitstellungsprobleme behoben sind. Zuvor kehrte die Site in den Produktionsmodus zurück, selbst wenn die Bereitstellung fehlschlug.<!--MAGECLOUD-2603-->

      - Die Validierungsprüfungen für die Bereitstellungsphase wurden überarbeitet, um die Fehlerstufe für die folgenden Bereitstellungsprobleme von `CRITICAL` auf `WARNING` herabzustufen, sodass die Bereitstellung abgeschlossen ist. Zuvor führten diese Probleme dazu, dass die Bereitstellung fehlschlug.

      - Die Umgebungskonfiguration enthält falsche Werte für Bereitstellungen oder Cloud-Variablen.

   - Die Elasticsearch-Version in der Cloud-Infrastruktur ist nicht mit der von Adobe Commerce in der Cloud-Infrastruktur unterstützten Version des Elasticsearch-/Elasticsearch-Moduls kompatibel. Weitere Informationen finden Sie im Artikel zur Fehlerbehebung bei Elasticsearch ](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in der Wissensdatenbank zum Adobe Commerce-Support.<!--MAGECLOUD-2600-->[

   - Es wurde ein Problem mit den freigegebenen Konfigurationseinstellungen in der Datei `app/etc/config.php` behoben, das während der Bereitstellung `recursion detected` Fehler verursachte.<!--MAGECLOUD-2173-->

- ![Fixsymbol](../../assets/fix.svg) **Cron-bezogene Fehlerbehebungen**—

   - Fehlerkorrektur - Die Ausführung von Aufträgen ist jetzt möglich, wenn Sie eine andere Cron-Häufigkeit als die Standardfrequenz (1 Minute) angeben.<!--MAGECLOUD-2602-->

   - Fehlerkorrektur - Es wurde ein Problem in der Bereitstellungsphase behoben, durch das die Ausführung von Cron-Aufträgen während der Bereitstellung fortgesetzt werden konnte. Dies kann zu Datenbanksperren und anderen kritischen Problemen führen. Jetzt werden alle Cron-Aufträge beendet, bevor die Bereitstellungsphase beginnt und nach Abschluss der Bereitstellung neu gestartet wird.&lt;!—MAGECLOUD—2537—>

   - Fehlerkorrektur - Der Cron-Auftrags-Workflow in den Versionen 2.2.x wird jetzt nicht mehr so aktiviert, dass gefrorene Cron-Aufträge vor der Implementierung angehalten werden können. Zuvor führte ein eingefrorener Cron-Auftrag dazu, dass die Bereitstellung angehalten wurde.<!--MAGECLOUD-2501-->

- ![Fixsymbol](../../assets/fix.svg) Das Format der vom `vendor/bin/ece-tools config:dump` -Befehl generierten `config.php`-Datei wurde geändert, um die kurze Array-Syntax und den Einzug von 4 Leerzeichen zu verwenden und die Adobe Commerce-Kodierungsstandards zu erfüllen.<!--MAGECLOUD-2527-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Bereitstellungsfehler behoben, der auftrat, wenn die `.magento.env.yaml` Platzhalter für `{{ base_url }}` und `{{ unsecure_base_url }}` für Webkonfigurationen anstelle der standardmäßigen URL-Konfiguration für ein Adobe Commerce-Projekt in der Cloud-Infrastruktur enthielt./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![neues Symbol](../../assets/new.svg) **Bereitstellung ohne Ausfallzeiten aktivieren** - Adobe Commerce in der Cloud-Infrastruktur stellt jetzt Anforderungen mit erforderlichen Datenbankänderungen während der Bereitstellung in die Warteschlange und wendet die Änderungen an, sobald die Bereitstellung abgeschlossen ist. Anfragen können bis zu 5 Minuten lang aufbewahrt werden, um sicherzustellen, dass keine Sitzungen verloren gehen. Siehe [Bereitstellungsoptionen für statische Inhalte, um Bereitstellungsausfälle in Cloud zu reduzieren](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![neues Symbol](../../assets/new.svg) **Docker-Compose für Cloud** - Es wurden die folgenden Verbesserungen am Prozess [Docker-Setup und -Konfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) vorgenommen:

   - Es wurde ein Befehl &quot;—`docker:config:convert`&quot; hinzugefügt, um PHP-Konfigurationsdateien in das Docker ENV-Format zu konvertieren, um die Umgebungskonfiguration zu vereinfachen. Jetzt kopieren Sie die PHP-Konfigurationsdateien in das Docker-Verzeichnis und konvertieren sie in Docker ENV-Dateien. Siehe [Docker starten](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Der Installationsprozess von Adobe Commerce on Cloud-Infrastruktur unterstützt jetzt die Bereitstellung sowohl auf schreibgeschützten als auch auf Lese- und Schreibdateisystemen, um das Cloud-Dateisystem genauer zu emulieren. Siehe [Docker konfigurieren](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Unterstützung des Redis-Dienstes**: Es wurde ein Redis-Bild hinzugefügt, das in einem Docker-Container bereitgestellt und automatisch für die Verwendung mit Ihrer Docker-Installation konfiguriert wird.&lt;!—MAGECLOUD—2442—>

   - Jetzt verfügen Sie über die DB-Dump-Funktion bei der Verwendung des Cloud Docker [Datenbankcontainers](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Außerdem können Sie [Dateien](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) mithilfe des Verzeichnisses `docker/mnt` zwischen einem Hostcomputer und einem Container freigeben.<!-- MAGECLOUD-2577 -->

   - **Unterstützung des Varnish-Dienstes**: Es wurde ein Varnish-Bild hinzugefügt, das automatisch in einem Docker-Container bereitgestellt wird. Nach der Bereitstellung können Sie Varnish anhand der Best Practices von Adobe Commerce manuell konfigurieren. Siehe [Konfigurieren und Verwenden von Varnish](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Sicherer Site-Zugriff: SSL-Unterstützung für den Zugriff auf Ihren Adobe Commerce Store und das Admin-Bedienfeld hinzugefügt.&lt;!—MAGECLOUD—2360—>

- ![Fixsymbol](../../assets/fix.svg) **Verbesserte Unterstützung der Adobe Commerce-Cloud-Infrastrukturerweiterung**—Die Mindestanforderung für die Version des &quot;guzzlehttp/guzzle&quot;-Pakets in der Adobe Commerce für die Cloud-Infrastruktur [composer.json-Datei](https://devdocs.magento.com/cloud/reference/cloud-composer.html) wurde auf Version 6.2 herabgestuft, sodass das `ece-tools`-Paket mit mehr Erweiterungen kompatibel ist.<!--MAGECLOUD-2205-->

- ![neues Symbol](../../assets/new.svg) **Wenden Sie während der Build-Phase benutzerdefinierte Änderungen an Ihrer Adobe Commerce-Anwendung an** - Wir teilen die Build-Phase in zwei separate Prozesse auf, sodass Sie mithilfe von Hooks benutzerdefinierte Änderungen an den generierten statischen Inhalt anwenden können, bevor Sie die Anwendung für die Bereitstellung verpacken. Der Prozess _build:generate_ generiert Code, wendet Patches an und generiert statische Inhalte. Der Prozess _build:transfer_ überträgt den generierten Code und statischen Inhalt an das endgültige Ziel. Siehe [Anwendungs-Hooks](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Überprüfung der Umgebungskonfiguration** - Verbesserte Validierung der Umgebungskonfiguration, um Kunden vor dem Erstellen und Bereitstellen von Adobe Commerce in der Cloud-Infrastruktur vor Versionsinkompatibilitäten und Konfigurationsfehlern zu warnen.

   - Versionsspezifische Validierung hinzugefügt, um nicht unterstützte oder veraltete Umgebungsvariablen und -werte zu identifizieren.<!--MAGECLOUD-2183-->

   - Es wurde eine Elasticsearch-Kompatibilitätsprüfung hinzugefügt, um Benutzer vor Problemen mit der Elasticsearch-Konfiguration zu warnen. Jetzt schlägt die Bereitstellung fehl, wenn die Elasticsearch-Dienstversion auf dem Server mit Adobe Commerce inkompatibel ist. Zuvor war die Bereitstellung auch dann erfolgreich, wenn die Elasticsearch-Version inkompatibel war, was nach der Site-Bereitstellung zu Problemen mit dem Produktkatalog führte.<!--MAGECLOUD-2389-->

     Sie können die Inkompatibilität beheben, indem Sie [ein Support-Ticket senden](https://devdocs.magento.com/cloud/trouble/trouble.html), um Elasticsearch auf eine kompatible Version zu aktualisieren, oder die Adobe Commerce-Konfiguration ändern, um eine kompatible Version des Elasticsearch-PHP-Clients anzugeben.

      - Aktualisieren Sie für Adobe Commerce-Version 2.1.x auf Version 2.2.2 Elasticsearch auf Version 2.4.

      - Aktualisieren Sie Elasticsearch für Adobe Commerce-Version 2.2.3 und höher auf Version 5.2.

      - Wenn Sie Elasticsearch 1.x oder 2.x haben und nicht aktualisieren möchten, aktualisieren Sie die Adobe Commerce Elasticsearch PHP-Clientversionserfordernis in Composer.json auf `"elasticsearch/elasticsearch": "~2.0"`.

   - Die Validierung von Umgebungsvariablen zur Identifizierung von Konfigurationseinstellungen, die während der Build-, Bereitstellungs- und Post-Bereitstellungsphasen Konflikte verursachen können, wurde verbessert. Beispielsweise wird während des Installations- und Aktualisierungsprozesses eine Warnmeldung angezeigt, wenn die globale Einstellung für die Bereitstellung statischer Inhalte mit den Einstellungen für die Build- oder Bereitstellungsphase in Konflikt gerät.<!--MAGECLOUD-2156-->

- ![Fixsymbol](../../assets/fix.svg) **Aktualisierungen der Umgebungsvariablen** - Änderung der folgenden Umgebungsvariablen:

   - **[SKIP_HTML_MINIFICATION global variable](../environment/variables-global.md#skip_html_minification)** - Der Standardwert wurde zu `true` geändert, um die Minimierung von On-Demand-HTML-Inhalten zu aktivieren, wodurch Ausfallzeiten bei der Bereitstellung in Staging- und Produktionsumgebungen minimiert werden. Diese Konfiguration ist für Bereitstellungen ohne Ausfallzeiten erforderlich.<!--MAGECLOUD-2435-->

   - **[CLEAN_STATIC_FILES-Bereitstellungsvariable](../environment/variables-deploy.md#clean_static_files)**: Die Funktion zum Verwalten der sauberen statischen Dateiverarbeitung für statischen Inhalt, der während der Build-Phase basierend auf der Umgebungsvariableneinstellung CLEAN_STATIC_FILES generiert wurde, wurde hinzugefügt. Zuvor wurden statische Inhaltsdateien, die während der Build-Phase generiert wurden, immer bereinigt.<!--MAGECLOUD-1506-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Protokollierung**: Es wurden die folgenden Änderungen vorgenommen, um Protokollmeldungen zu verbessern und die Protokollgröße zu reduzieren:

   - In den Protokolleinträgen zu Implementierungsfehlern ist jetzt die Befehlsausgabe aus den Vorgängen enthalten, die zu Fehlern führen, selbst wenn in Ihrer Umgebungskonfiguration keine Protokollierung auf der Debug-Ebene festgelegt ist. Siehe [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Es wurde eine Protokollierung für Bereitstellungsfehler hinzugefügt, die auftreten, wenn von einigen Erweiterungen benötigte generierte Fabriken nicht korrekt generiert werden können, da das Dateisystem schreibgeschützt ist.<!--MAGECLOUD-2209-->

   - Die Größe des Bereitstellungsprotokolls wurde reduziert und es wurden Formatierungsprobleme behoben, die durch Setup-Befehle verursacht wurden, die die interaktive Fortschrittsleiste verwenden.<!--MAGECLOUD-2402-->

   - Die unnötige Ausführlichkeit wurde beseitigt und die Prioritätsstufen für einige Protokolleinträge wurden aktualisiert.<!--MAGECLOUD-2227-->

- ![Fixsymbol](../../assets/fix.svg) **Cron-spezifische Korrekturen**—

   - Die standardmäßigen Einstellungen für die Cron-Auftragskonfiguration für die Verlaufslebensdauer wurden von 3d (4320 min) auf 1h (60 min) geändert, um Leistungsprobleme und Bereitstellungsfehler zu verhindern, die auftreten können, wenn die Cron-Warteschlange zu schnell gefüllt wird.<!--MAGECLOUD-2427-->

   - Der Cron-Auftragsverwaltungsprozess während der Bereitstellungsphase wurde verbessert, um Datenbanksperren und andere kritische Probleme zu verhindern. Jetzt werden alle Cron-Aufträge während der Bereitstellungsphase beendet und nach Abschluss der Bereitstellung neu gestartet.<!--MAGECLOUD-2445-->

   - Fehlerkorrektur - Der Sperrmechanismus für die Planung von Kunden, die von Cron-Aufträgen in Adobe Commerce-Versionen 2.2.0 und höher gestartet werden, funktioniert jetzt einwandfrei. Er verhindert, dass Cron-Aufträge doppelte Verbraucher starten.<!--MAGECLOUD-2464-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem beim [Prozess der statischen Inhaltskomprimierung](../environment/variables-intro.md) (`gzip`) behoben, das beim Verweisen auf die komprimierte Datei während des Bereitstellungsprozesses `not overwritten` - und `no such file or directory` -Fehler verursachte.<!-- MAGECLOUD-2182-->

- ![Symbol &quot;Beheben&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das verhindert hat, dass der Befehl `php ./vendor/bin/ece-tools config:dump` redundante Abschnitte während des Dump-Prozesses aus der Datei `config.php` entfernt, wenn das Gebietsschema &quot;Speichern&quot;nicht angegeben ist. Jetzt können Sie Ihre Konfigurationsdateien einfach zwischen Umgebungen verschieben. Nachdem Sie auf `ece-tools` v2002.0.13 aktualisiert haben, erstellen Sie ältere `config.php` -Dateien mit dem verbesserten Befehl `config:dump` neu. Siehe [Konfigurationsverwaltung für Speichereinstellungen](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Fehlers, der während der Bereitstellungsphase einen Fehler verursachte, wenn die Routenkonfiguration in der `.magento/routes.yaml` -Datei von einer [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) -Domäne zu einer `www` -Domäne umleitet.<!--MAGECLOUD-2556-->

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem mit der Option `_merge` für die Variable [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) behoben, das zu falschen Zusammenführungsergebnissen führte, wenn Sie den Parameter `engine` nicht in die aktualisierte Konfigurationsdatei `.magento.env.yaml` eingeschlossen haben. Der Zusammenführungsvorgang überschreibt jetzt korrekt nur die Werte, die Sie in der aktualisierten `.magento.env.yaml` angeben, ohne dass Sie den Parameter `engine` festlegen müssen.<!--MAGECLOUD-2520-->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem bei der Redis-Konfiguration behoben, durch das die Sitzungssperrung für Adobe Commerce in den Cloud-Infrastrukturversionen 2.2.1 und höher fälschlicherweise aktiviert wurde, was zu langsamer Leistung und Zeitüberschreitungen führen kann. Jetzt ist die Sitzungssperrung standardmäßig deaktiviert. Das Problem wurde durch eine Änderung des Standardverhaltens des Parameters `disable_locking` verursacht, der in Version 1.3.4 des Redis-Sitzungs-Handler-Pakets eingeführt wurde. Siehe [colinmollenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![neues Symbol](../../assets/new.svg) **Docker-Compose für Cloud** - Es wurde ein Befehl—`docker:build` hinzugefügt, um eine [Docker Compose](https://devdocs.magento.com/cloud/docker/docker-config.html) -Konfiguration aus dem Cloud `ece-tools`-Repository zu generieren.<!-- MAGECLOUD-2250 -->

- ![neues Symbol](../../assets/new.svg) **Gebietsschemata ändern** - Jetzt können Sie das Gebietsschema für den Speicher ändern, ohne den Konfigurationsvorgang für den Export und Import durchführen zu müssen. Während sich die Anwendung in der Produktion befindet und SCD_ON_DEMAND aktiviert ist, sind die Gebietsschemaoptionen &quot;Store&quot;und &quot;admin&quot;verfügbar.<!-- MAGECLOUD-2019 -->

- ![neues Symbol](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Sitemap und Robots**: Es wurde ein [Workflow](../store/robots-sitemap.md) erstellt, um eine `robots.txt` -Datei hinzuzufügen und eine `sitemap.xml` -Datei für eine einzelne Domänenkonfiguration zu generieren, ohne dass die Infrastruktur geändert werden muss.

- ![neues Symbol](../../assets/new.svg) **Assistenten**—Es wurden zwei [Assistenten](../deploy/smart-wizards.md) hinzugefügt, die Ihnen bei der Cloud-Konfiguration helfen:<!-- MAGECLOUD-1910 -->

   - `ideal-state` - Konfigurieren Sie den idealen Status für minimale Bereitstellungsausfälle

   - `master-slave` - Konfigurieren des Lastenausgleichs für Datenbank und Rediv

- ![neues Symbol](../../assets/new.svg) **Modulaktualisierung**: Es wurde ein Cloud-Befehl hinzugefügt -`module:refresh` - um Module zu aktivieren, die deaktiviert oder nicht explizit aktiviert wurden, ähnlich wie bei einem Build automatisch.<!-- MAGECLOUD-1521 -->

- ![neues Symbol](../../assets/new.svg) Es wurde die Möglichkeit hinzugefügt, die Konfiguration für Dienste mithilfe der Option `_merge` in den Konfigurationen [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSION](../environment/variables-deploy.md#session_configuration), [QUEUE](../environment/variables-deploy.md#queue_configuration) und [SEARCH](../environment/variables-deploy.md#search_configuration) zusammenzuführen oder zu überschreiben.<!-- MAGECLOUD-2105 -->

- ![neues Symbol](../../assets/new.svg) **Beispieldatei für die Umgebungskonfiguration** - Wir haben dem ECE-Tools-Paket eine Beispieldatei mit einer detaillierten Beschreibung und möglichen Werten für jede Umgebungsvariable hinzugefügt.<!-- MAGECLOUD-1908 -->`.magento.env.yaml`

   - Außerdem wurde eine tiefe Validierung für die `.magento.env.yaml` -Konfiguration hinzugefügt, die Fehler im Bereitstellungsprozess verhindert, die durch unerwartete Werte verursacht werden. Wenn ein Fehler auftritt, erhalten Sie jetzt eine detaillierte Fehlermeldung, die beginnt mit: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![neues Symbol](../../assets/new.svg) Die folgenden [**Umgebungsvariablen**](../environment/variables-intro.md) wurden hinzugefügt:

   - Jetzt können Sie mit der neuen Umgebungsvariablen [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) mehrere Gebietsschemas für jedes Design definieren, wodurch sich die Anzahl der bereitzustellenden Designdateien verringert.<!-- MAGECLOUD-1501 -->

   - Die Umgebungsvariable [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) wurde hinzugefügt, um Ihre Datenbankverbindungen für die Bereitstellung anzupassen.<!-- MAGECLOUD-2047 -->

   - Die neue Variable [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) überschreibt die minimale Protokollierungsstufe für alle Ausgabestreams, ohne Änderungen am Code vorzunehmen.<!-- MAGECLOUD-2129 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das zwischen der Bereitstellung und der Phase nach der Bereitstellung zu Ausfallzeiten führte. Nun beginnt die Phase nach der Bereitstellung _unmittelbar_ nach dem Ende der Bereitstellungsphase.

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das die erfolgreichen Cron-Aufträge, die mit `status = success` ausgestattet waren, nicht aus dem Zeitplan entfernt wurden.<!-- MAGECLOUD-2268 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem mit dem Erweiterungspunkt `post_deploy` behoben, durch das der Cache in der Bereitstellungsphase und nicht in der Phase nach der Bereitstellung des Projekts gelöscht wurde.<!-- MAGECLOUD-2113 -->

- ![Symbol &quot;Korrektur&quot;](../../assets/fix.svg) Es wurde ein Problem bei der Verwendung von SCD mit mehreren Gebietsschemas behoben, durch das dieselbe `js-translation.json` -Datei für jedes Gebietsschema generiert wurde.<!-- MAGECLOUD-2034 -->

- ![Fixsymbol](../../assets/fix.svg) Der Befehl `db:dump` im Paket `ece-tools` wurde optimiert, um zu verhindern, dass Tabellen gesperrt werden, und um die Geschwindigkeit zu erhöhen.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>Die ECE-Tools-Version 2002.0.11 ist für die Kompatibilität mit 2.2.4 erforderlich.

- ![neues Symbol](../../assets/new.svg) **Konfigurieren schreibgeschützter Verbindungen zu Nicht-Master-Knoten** - Diese Version bietet die Möglichkeit, eine schreibgeschützte Verbindung zu einem Nicht-Master-Knoten zu konfigurieren, um schreibgeschützten Traffic zu erhalten (für [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) und für <!--MAGECLOUD-143 -->

- ![neues Symbol](../../assets/new.svg) **Konfigurationsassistent**: Es wurde ein Assistent hinzugefügt, mit dem Sie Ihre Konfiguration für die Bereitstellung statischer Inhalte überprüfen können. Siehe [Smart-Assistenten](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![neues Symbol](../../assets/new.svg) **Unterstützung der Symfony-Konsole**—Unterstützung für Symfony Console 4 mit Adobe Commerce 2.3 wurde hinzugefügt.<!-- MAGECLOUD-1966 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) **Optimierungen für die Cron-Planung**: Die Warteschlangenverwaltung und die verbesserte Protokollierung wurden verbessert, um das Debugging von Cron-bezogenen Problemen zu erleichtern.<!-- MAGECLOUD-1607 -->

- ![ Symbol Fehlerbehebung](../../assets/fix.svg) Die Freigabe-Validierung schlägt fehl, wenn ein `ADMIN_EMAIL` - oder `ADMIN_USERNAME` -Wert mit einem vorhandenen Administratorkonto übereinstimmt.<!-- MAGECLOUD-1221 -->

- ![Fixsymbol](../../assets/fix.svg) SOLR-Unterstützung für 2.2.x-Versionen wurde entfernt. 2.1.x-Versionen behalten die Möglichkeit, SOLR zu aktivieren.<!-- MAGECLOUD-1282 -->

- ![Fixsymbol](../../assets/fix.svg) Die erste Installation der Staging- und Produktionsumgebungen eines PRO-Projekts enthält jetzt verschiedene Indexpräfixe zum Elasticsearch, um mögliche Konflikte bei der Identifizierung von Datensätzen zu vermeiden, die zu den einzelnen Umgebungen gehören.<!-- MAGECLOUD-1489 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, durch das die Build-Phase für die alte Architektur während der Bereitstellung statischer Inhalte unterbrochen wurde.<!-- MAGECLOUD-2021 -->

- ![Fixsymbol](../../assets/fix.svg) **Cron-spezifische Verbesserungen**—Die Cron-Implementierung wurde überarbeitet:<!-- MAGECLOUD-1607 -->

   - Es wurde ein Fehler behoben, der dazu führte, dass die Cron-Warteschlange schnell gefüllt wurde. Jetzt werden die veralteten Cron-Jobs verlässlicher gelöscht.

   - Die Sequenz von Cron-Aufträgen wurde neu organisiert, sodass alle Aufträge in separaten Threads vor der allgemeinen Gruppe gestartet werden.

   - Verbesserte Protokollierung, um das Debugging von Cron-Problemen zu verbessern.

   - **HINWEIS** - Diese Version behandelt viele Cron-bezogene Probleme. Wenn Sie derzeit einige Cron-bezogene Patches in _m2-hotfixes_ verwenden, entfernen Sie sie.

- ![Fixsymbol](../../assets/fix.svg) **SCD-spezifische Verbesserungen**—

   - Sie können die Umgebungsvariablen `VERBOSE_COMMANDS` und `SCD_COMPRESSION_LEVEL` sowohl während der _Build_- als auch der de_ploy-Phasen verwenden.<!-- MAGECLOUD-1819 -->

   - Es wurde ein Problem behoben, bei dem die Bereitstellung mit einem zufälligen Fehler fehlschlug, wenn ein unerwarteter Wert für die Umgebungsvariable `SCD_COMPRESSION_LEVEL` auftrat. Die Konfigurationsvalidierung wurde verbessert, um aussagekräftige Benachrichtigungen bereitzustellen. Unter [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) finden Sie akzeptable Werte.<!-- MAGECLOUD-2043 -->

   - Das Verhalten des Konfigurationsflusses der Umgebungsvariablen `SCD_COMPRESSION_LEVEL` wurde korrigiert, sodass die Außerkraftsetzungen erwartungsgemäß funktionieren.<!-- MAGECLOUD-2044 -->

   - Fehlerkorrektur - Die Konfiguration der Umgebungsvariablen `SCD_THREADS` in der Phase `.magento.env.yaml` file _deploy_ funktioniert jetzt einwandfrei.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![neues Symbol](../../assets/new.svg) **Statische Inhaltsbereitstellung (SCD)** - Es gibt einen neuen alternativen Bereitstellungsprozess zum Generieren von statischem Inhalt bei Anforderung (On-Demand). Dadurch werden Ausfallzeiten reduziert und die Cache-Handhabung verbessert, indem die wichtigsten Assets generiert werden.<!-- MAGECLOUD-1285 -->

   - **Neue Umgebungsvariable**: Die globale Umgebungsvariable `SCD_ON_DEMAND` wurde hinzugefügt, um bei Anforderung statischen Inhalt zu generieren.<!-- MAGECLOUD-1738 -->

   - **Post-deploy-Erweiterungspunkt**: Es wurde ein `post_deploy` -Erweiterungspunkt für die Datei `.magento.app.yaml` hinzugefügt, der den Cache löscht und den Cache vorlädt (wärmt), _nachdem_ der Container Verbindungen akzeptiert. Sie ist nur für Pro-Projekte verfügbar, die Staging- und Produktionsumgebungen in der [!DNL Cloud Console] enthalten, sowie für Starter-Projekte. Obwohl dies nicht erforderlich ist, funktioniert dies zusammen mit der Umgebungsvariablen `SCD_ON_DEMAND`.<!-- MAGECLOUD-1788 -->

- ![neues Symbol](../../assets/new.svg) **Optimierung**—Das Verschieben oder Kopieren von Dateien während der Bereitstellung wurde optimiert, um die Bereitstellungsgeschwindigkeit zu verbessern und die Auslastung des Dateisystems zu verringern.<!-- MAGECLOUD-1842 -->

- ![neues Symbol](../../assets/new.svg) **Freigabe-Protokollierung**: Es wurde die Möglichkeit hinzugefügt, die Globen-Handler (Syslog and Graylog Extended Log Format) für die Ausgabe von Protokollen während des Bereitstellungsprozesses zu aktivieren. Siehe [Protokollierungs-Handler](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![neues Symbol](../../assets/new.svg) Die folgenden [**Umgebungsvariablen**](../environment/variables-intro.md) wurden hinzugefügt:

   - `CRYPT_KEY`—Stellen Sie einen kryptografischen Schlüssel für eine andere Umgebung bereit, wenn Sie eine Datenbank verschieben.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Global_ -Umgebungsvariable, die das Kopieren der statischen Ansichtsdateien in den Ordner `var/view_preprocessed` überspringt und bei Anforderung minimierte HTML generiert.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Global_ Umgebungsvariable zum Generieren von statischem Inhalt bei Anforderung.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES` - Sie können die Seiten auflisten, die zum Vorausfüllen des Cache verwendet werden sollen. Verfügbar in den neuen [Post-Bereitstellungsvariablen](../environment/variables-post-deploy.md).

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, bei dem ein lokal angewendeter Patch die Bereitstellung auf einer Instanz verhinderte. Jetzt können die ECE-Tools erkennen, dass ein Patch angewendet wurde.<!-- MAGECLOUD-982 -->

- ![Fixsymbol](../../assets/fix.svg) Korrektur eines Konflikts zwischen JavaScript-Bundling und GZIP-Funktionalität. Jetzt funktionieren diese Funktionen richtig zusammen.<!-- MAGECLOUD-1735 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das dazu führte, dass die Befehle der ECE-Tools-CLI bei Verwendung früherer PHP 7.0.x-Versionen fehlschlugen.<!-- MAGECLOUD-1744 -->

- ![Fixsymbol](../../assets/fix.svg) Es wurde ein Problem behoben, das die Bereitstellung statischer Inhalte mit der kompakten Strategie in mehreren Threads verhinderte.<!-- MAGECLOUD-1822 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem mit der Sitzungssperrung für Redis behoben, das eine Admin-Anmeldungsverzögerung verursachte. Außerdem ist die Fehlerbehebung für 2.1.x verfügbar.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Sie müssen [das Adobe Commerce-Metapaket zur Cloud-Infrastruktur aktualisieren](../dev-tools/install-package.md#update-the-metapackage), um dieses und alle künftigen Aktualisierungen zu erhalten.

- ![neues Symbol](../../assets/new.svg) **ece-tools** - Das `ece-tools`-Paket unterstützt jetzt Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![neues Symbol](../../assets/new.svg) **Redis configuration** - Sie können jetzt die Seite &quot;Redis](../environment/variables-deploy.md#cache_configuration)&quot;und den standardmäßigen Cache- und Redis-Sitzungsspeicher mit einer Umgebungsvariablen konfigurieren.<!-- MAGECLOUD-1552 -->[

- ![neues Symbol](../../assets/new.svg) **Verbesserungen beim Such-, AMQP- und Redis-Dienst** - Wir haben den Dienstkonfigurationsfluss vereinheitlicht, sodass er sich jetzt für alle Dienste genauso verhält. Die manuelle Bearbeitung der `env.php` -Datei zum Konfigurieren von Diensten wird nicht mehr unterstützt. Sie müssen stattdessen Umgebungsvariablen oder die Datei `.magento.env.yaml` verwenden.<!-- MAGECLOUD-1437 -->

- ![Fixsymbol](../../assets/fix.svg) **Umgebungsvariablen**—

   - Die Verwendung von `env:STATIC_CONTENT_THREADS` wurde eingestellt und wird in einer zukünftigen Version entfernt. Verwenden Sie stattdessen [SCD_THREADS](../environment/variables-deploy.md#scd_threads).<!-- MAGECLOUD-1507 -->

   - Die Umgebungsvariable `STATIC_CONTENT_EXCLUDE_THEMES` wurde eingestellt. Sie müssen stattdessen die Umgebungsvariable `SCD_EXCLUDE_THEMES` verwenden.<!-- MAGECLOUD-1640 -->

- ![Fixsymbol](../../assets/fix.svg) **Protokollierung** - Wir haben die Protokollierung von integrierten Patchvorgängen vereinfacht.<!-- MAGECLOUD-1674 -->

- ![Fixsymbol](../../assets/fix.svg) Wir haben die `developer` -Modusunterstützung und die `APPLICATION_MODE` -Umgebungsvariable entfernt, da sie zu unerwartetem Verhalten führten.<!-- MAGECLOUD-1615 -->

- ![Symbol &quot;Fehlerbehebung&quot;](../../assets/fix.svg) Es wurde ein Problem behoben, das zu Fehlern bei der Bereitstellung statischer Inhalte im Zusammenhang mit Redis führte. Jetzt wird die Bereitstellung statischer Inhalte mit mehreren Threads wie geplant ausgeführt.<!-- MAGECLOUD-1630 -->

- ![Symbol Fehlerbehebung](../../assets/fix.svg) Es wurde ein Problem behoben, das Benutzer daran hinderte, Änderungen an Konfigurationsfeldern in Admin zu speichern, die nach Ausführung des Befehls `app:config:dump` als vertraulich markiert wurden.<!-- MAGECLOUD-1175 -->

- ![Fixsymbol](../../assets/fix.svg) Wir haben Unterstützung für eine frühere Version von `symfony/yaml` hinzugefügt, um Konflikte mit einigen Paketen zu beheben, die noch nicht mit der neuesten Version kompatibel sind.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>In dieser Version haben wir `vendor/magento/ece-patches` mit `vendor/magento/ece-tools` zusammengeführt. Sie müssen das `vendor/magento/ece-patches` -Paket nicht mehr separat aktualisieren.

**Neue Funktionen:**

- **Verbesserte Protokollierung**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Die Protokollnachrichten wurden verbessert, um bessere Erklärungen zu liefern, wenn der Build- oder Bereitstellungsprozess eine Umgebungsvariable außer Kraft setzt.
   - Sie können nun den Installations- und Aktualisierungsfortschritt in Echtzeit anzeigen. Prüfen Sie die Datei &quot;`install_update.log`&quot;, um den Fortschritt anzuzeigen. Beispiel:

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Neuer Cron-Befehl**: Sie können jetzt bestimmte angehaltene Cron-Aufträge entsperren, anstatt sie mit dem Befehl [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) zu stoppen und neu zu starten. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1367 -->

- **Einheitliche Konfigurationsdatei** - Sie können jetzt Build- und Bereitstellungsschritte mithilfe einer [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) -Datei konfigurieren.<!-- MAGECLOUD-1369 -->

- **Konfigurationsdateien sichern** - Der Bereitstellungsprozess erstellt jetzt nach der Bereitstellung automatisch eine Sicherung der Konfigurationsdateien `app/etc/env.php` und `app/etc/config.php`. Außerdem wurde ein [neuer CLI-Befehl](https://support.magento.com/hc/en-us/articles/360033182871) hinzugefügt, um diese Konfigurationsdateien aus einer Sicherung wiederherzustellen.<!-- MAGECLOUD-1372 -->

- **Fehlerbehebung bei Validierungsfehlern** - Der Befehl, den Sie verwenden müssen, um Validierungsfehler zu beheben, wurde geändert, wenn `config.php` nicht genügend Daten für die Bereitstellung statischer Inhalte enthält. Zuvor wurden Sie in der Fehlermeldung angewiesen, `bin/magento app:config:dump` auszuführen. Nun müssen Sie `php ./vendor/bin/ece-tools config:dump` ausführen.<!-- MAGECLOUD-1491 -->

- **Neue Umgebungsvariablen**: Sie können jetzt Umgebungsvariablen verwenden, um benutzerdefinierte [Suchdienste](../environment/variables-deploy.md#search_configuration) und [AMQP-basierte](../environment/variables-deploy.md#queue_configuration) Dienste mit Ihrer Site zu verbinden.<!-- MAGECLOUD-1410 -->

- Wir haben smartes Patchen implementiert. Jetzt wendet das Paket Patches an, die nicht auf der Cloud-Infrastrukturversion von Adobe Commerce basieren, sondern auf der gepatchten Paketversion.<!--MAGECLOUD-1090-->

**Gelöste Probleme:**

- Es wurde ein Protokollierungsproblem behoben, das Build-Fehler verursachte.<!-- MAGECLOUD-1162 -->

- Es wurde ein Problem behoben, das beim Ausführen von Bereitstellungen im interaktiven Modus Timeout-Ausnahmen verursachte.<!-- MAGECLOUD-1389 -->

- Es wurde ein Problem behoben, das bei der Verwendung der kompakten Strategie für die statische Inhaltserstellung Fehler verursachte. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Es wurde ein Problem behoben, durch das das Bereitstellungsskript die Staging- und Produktionsumgebungen nicht ordnungsgemäß identifizieren konnte.<!-- MAGECLOUD-1493 -->

- Es wurde ein Problem behoben, das dazu führte, dass Netzwerkprobleme Datenbankverbindungen störten und während der Installation und Aktualisierung Fehler verursachten.<!-- MAGECLOUD-1520 -->

- Es wurde ein Problem behoben, das Sie daran hinderte, die Konfigurationsdateien mit `app:config:dump` mehrmals zu exportieren. Nicht verfügbar in 2.1.<!--  MAGECLOUD-1567  -->

- Es wurde ein Fehler mit der Sitzungssperrung &quot;Redis&quot;_locking_ behoben, der eine Anmeldungsverzögerung für _Admin_ verursachte. Nicht verfügbar in 2.1.<!--  MAGECLOUD-1582  -->

- Es wurde ein Implementierungsproblem im Zusammenhang mit der Versionierung behoben, das einen Konflikt mit anderen Composer-basierten Patchmodulen verursachte.<!-- MAGECLOUD-1450 -->

- Es wurde ein Problem behoben, das während des Imports PHP-Speicherprobleme verursachte.<!-- MAGECLOUD-1310 -->

- Es wurde ein Patch entfernt. Es wurde ein Fehler in `colinmollenhour/credis` v1.6 behoben, durch den die Unterstützung für Adobe Commerce in der Cloud-Infrastruktur 2.2.1 aktiviert wurde. Nicht verfügbar in 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Gelöste Probleme:**

- Wir haben `var/view_preprocessed` symlinks entfernt, um ein Problem zu beheben, das zu JavaScript-Minimierungskonflikten führte.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Gelöste Probleme:**

- Es wurde ein Problem behoben, das `gzip` -Fehler verursachte, wenn ein Datei- oder Verzeichnisname Leerzeichen enthielt.<!-- MAGECLOUD-1413 -->

- Es wurde ein Fehler behoben, der verhinderte, dass Bereitstellungsskripte Modulabhängigkeiten ordnungsgemäß erkennen und aktivieren.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Neue Funktionen:**

- **Konfigurieren eines Cron-Verbrauchers mit einer Umgebungsvariablen** - Sie können jetzt Cron-Verbraucher mit der neuen Umgebungsvariablen `CRON_CONSUMERS_RUNNER` konfigurieren.

- **Konfigurationsprüfung**: Wir suchen jetzt während des Build-/Bereitstellungsprozesses nach kritischen Komponenten und stoppen den Prozess, wenn die Prüfung fehlschlägt. Dies verhindert unnötige Ausfallzeiten aufgrund des Wartungsmodus der Site.

- **Benachrichtigungen erstellen/bereitstellen** - Wir haben eine Konfigurationsdatei hinzugefügt, die Sie verwenden können, um [Slack- und/oder E-Mail-Benachrichtigungen einrichten](../environment/set-up-notifications.md) für Build-/Bereitstellungsaktionen in allen Ihren Umgebungen einzurichten.

- **Statische Inhaltskomprimierung** - Wir komprimieren jetzt statischen Inhalt mit [gzip](https://www.gnu.org/software/gzip/) während der Build- und Bereitstellungsphasen. Diese Komprimierung in Verbindung mit der schnellen Komprimierung trägt dazu bei, die Größe Ihres Stores zu reduzieren und die Bereitstellungsgeschwindigkeit zu erhöhen. Bei Bedarf können Sie die Komprimierung mit einer [Build-Option](../environment/variables-build.md) oder der [Bereitstellungsvariable](../environment/variables-deploy.md) deaktivieren. Weitere Informationen finden Sie in den folgenden Themen:

   - [Umgebungsvariablen der Anwendung](../application/variables-property.md)

   - [Leistung bei der Bereitstellung statischer Inhalte](../deploy/static-content.md)

   - [Bereitstellungsprozess](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Konfigurationsverwaltung**: Wir generieren jetzt während der Build-Phase automatisch eine `app/etc/config.php` -Datei in Ihrem Git-Repository, sofern sie noch nicht vorhanden ist. Die automatisch generierte Datei enthält nur eine Liste von Modulen und Erweiterungen. Wenn die Datei bereits vorhanden ist, wird die Build-Phase normal fortgesetzt. Wenn Sie zu einem späteren Zeitpunkt die [Konfigurationsverwaltung](../store/store-settings.md) befolgen, aktualisieren die Befehle die Datei, ohne dass zusätzliche Schritte erforderlich sind. Weitere Informationen finden Sie unter [Implementierungsprozess](https://devdocs.magento.com/cloud/reference/discover-deploy.html) .

- **Datenbank-Dumps**: Es wurde ein `magento/ece-tools` CLI-Befehl zum Erstellen von Datenbank-Dumps in allen Umgebungen hinzugefügt. Bei Pro-Plan-Produktionsumgebungen wird dieser Befehl nur von einem von drei Hochverfügbarkeitsknoten abgelegt. Daher können Produktionsdaten, die während des Dump auf einen anderen Knoten geschrieben wurden, nicht kopiert werden. Es wird empfohlen, die Anwendung in den Wartungsmodus zu versetzen, bevor ein Datenbank-Dump in Produktionsumgebungen durchgeführt wird. Weitere Informationen finden Sie unter [Backup Management](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) .

- **Einschränkungen des Cron-Intervalls aufgehoben** - Das standardmäßige Cron-Intervall für alle Umgebungen, die in den Regionen us-3, eu-3 und ap-3 bereitgestellt werden, beträgt 1 Minute. Das standardmäßige Cron-Intervall in allen anderen Regionen beträgt 5 Minuten für Pro Integration-Umgebungen und 1 Minute für Pro Staging- und Produktionsumgebungen. Um Ihre vorhandenen Cron-Aufträge zu ändern, bearbeiten Sie Ihre Einstellungen in `.magento.app.yaml` oder erstellen Sie ein Support-Ticket für Produktions-/Staging-Umgebungen. Weitere Informationen finden Sie unter [Einrichten von Cron-Aufträgen](../application/crons-property.md#set-up-cron-jobs) .

**Gelöste Probleme:**

- Es wurde ein Problem behoben, das zu langen Bereitstellungszeiten führte, da der Bereitstellungsprozess vor der Bereitstellung statischer Inhalte den `cache-clean` -Vorgang aufrief.<!-- MAGECLOUD-1327 -->

- Es wurde ein Problem behoben, das während des Schritts zur Erstellung statischer Inhalte bei der Bereitstellung in Produktionsumgebungen Fehler verursachte.<!-- MAGECLOUD-1322 -->

- Es wurde ein Fehler behoben, der verhinderte, dass einige `magento/ece-tools`-Befehle die Ausgabe auf `stderr` protokollieren konnten.<!-- MAGECLOUD-1264 -->

- Es wurde ein Fehler behoben, der verhinderte, dass Basis-URL-Werte in `env.php` in abgespalteten Verzweigungen aktualisiert wurden.<!-- MAGECLOUD-1242 -->

- Es wurde ein Fehler behoben, der dazu führte, dass der Befehl `magento setup:install` ein unsicheres Präfix (`http://`) hinzufügte, um Basis-URLs zu sichern.<!-- MAGECLOUD-1171 -->

- Es wurde ein Problem behoben, das verhinderte, dass Patch-Fehler Bereitstellungsfehler verursachen.<!-- MAGECLOUD-1170 -->

- Es wurde ein Fehler behoben, der verhindert hat, dass `ece-tools` die Ausführung stoppt und eine Ausnahme auslöst, wenn keine Patches angewendet werden können.<!-- MAGECLOUD-1152 -->

- Es wurde ein Problem behoben, das beim Laden der Storefront nach der Aktivierung der HTML-Minimierung in der Admin-Konsole Fehler verursachte.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Gelöste Probleme:**

- Jetzt können Sie hängengebliebene Cron-Aufträge ](https://support.magento.com/hc/en-us/articles/360033099451) über einen CLI-Befehl in allen Umgebungen über SSH-Zugriff manuell zurücksetzen. [ Der Bereitstellungsprozess setzt Cron-Aufträge automatisch zurück.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Gelöste Probleme:**

- Es wurde ein Problem behoben, das dazu führte, dass Seiten eine Zeitüberschreitung verursachten, da Redis zu lange zum Lesen/Schreiben brauchte. Sie können jetzt den Parameter `disable_locking` in Redis-Konfigurationen verwenden, um dieses Problem zu verhindern.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Gelöste Probleme:**

- Der [!DNL RabbitMQ]-Konfigurationsprozess ruft jetzt alle erforderlichen Parameter automatisch ab.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Neue Funktionen:**

- Adobe Commerce in der Cloud-Infrastruktur unterstützt jetzt Bereiche und [Strategien zur Bereitstellung statischer Inhalte](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). Wir haben den Parameter `–s` mit der Standardeinstellung `quick` für die Strategie zur Bereitstellung statischer Inhalte hinzugefügt. Sie können die Umgebungsvariable [SCD_STRATEGY](../environment/variables-deploy.md) verwenden, um diese Strategien für Build- und Bereitstellungsaktionen anzupassen und zu verwenden. Diese Variable unterstützt die Optionen `standard`, `quick` oder `compact`. Wenn Sie &quot;`compact`&quot;auswählen, wird der Wert &quot;`STATIC_CONTENT_THREADS`&quot;durch &quot;`1`&quot;überschrieben, was die Bereitstellung insbesondere in Produktionsumgebungen verlangsamen kann. Nicht verfügbar in 2.1.<!--- MAGECLOUD-1057 -->

- Wir haben eine Protokolldatei für Umgebungen erstellt, um Build- und Bereitstellungsaktionen zu erfassen und zu kompilieren. Die Datei &quot;`var/log/cloud.log`&quot; befindet sich im Stammverzeichnis der Anwendung.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Gelöste Probleme:**

- Das `ece-tools` -Paket wurde überarbeitet, um es mit Adobe Commerce in der Cloud-Infrastruktur 2.2.0 und höher kompatibel zu machen.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Es wurde ein Problem behoben, durch das verhindert wurde, dass `ece-tools` die Ausführung stoppt und eine Ausnahme auslöst, wenn keine Patches angewendet werden können.<!-- MAGECLOUD-1186 -->

- Es wurde ein Problem behoben, bei dem Ausnahmen ausgelöst wurden, wenn die Kompilierung der Abhängigkeitseinfügung (Di) während der Builds übersprungen wurde.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Es wurde ein Problem behoben, das dazu führte, dass der Bereitstellungsprozess benutzerdefinierte Redis-Konfigurationen in der Datei `env.php` überschrieb.<!-- MAGECLOUD-1019 -->

- Es wurde ein Problem behoben, das zu Umleitungs-Schleifen führte, da diese standardmäßig durch einen sicheren Administrator deaktiviert waren.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Dieses Paket ist nicht mehr mit anderen Versionen von Adobe Commerce in der Cloud-Infrastruktur kompatibel und **sollte nicht** verwendet werden.

### Erste Version

Erste Veröffentlichung von `ece-tools` für Adobe Commerce in der Cloud-Infrastruktur 2.2.0.
