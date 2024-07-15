---
title: Fehlermeldungen für ECE-Tools-Paket
description: Sehen Sie sich eine Liste von Fehlercodes und -nachrichten an, die während der Adobe Commerce beim Erstellen, Bereitstellen und Bereitstellen von Cloud-Infrastruktur-Prozessen auftreten können.
recommendations: noDisplay
role: Developer
exl-id: d8cc8d49-32da-43cf-a105-aa56b5334000
source-git-commit: 9dda6fe7f6a9d6064436820a3c8426ec982b5230
workflow-type: tm+mt
source-wordcount: '2763'
ht-degree: 4%

---

# Fehlermeldungen für ECE-Tools

Diese Fehlernachrichten-Referenz enthält Informationen zur Fehlerbehebung, die während der Adobe Commerce-Erstellung, Bereitstellung und nach der Bereitstellung durchgeführten Prozesse bei der Cloud-Infrastruktur auftreten können.

Alle kritischen und Warnmeldungen, die während der Bereitstellung auftreten, werden in die Dateien `var/log/cloud.log` und `/var/log/cloud.error.log` geschrieben. Die Fehlerprotokolldatei der Cloud enthält nur Fehler aus der neuesten Bereitstellung. Eine leere Datei weist auf eine erfolgreiche Implementierung ohne Fehler hin.

In der Datei `cloud.error.log` wird jeder Eintrag als JSON-Zeichenfolge formatiert, um die Analyse zu vereinfachen:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Fehlermeldungen werden nach einer der Implementierungsphasen kategorisiert: Erstellen, Bereitstellen und Nach der Bereitstellung. Jeder Abschnitt enthält eine Liste der zugehörigen Fehler mit den folgenden Informationen zu jedem Fehler:

- **Fehlercode**: Die von Adobe Commerce zugewiesene Kennung für die Fehlermeldung
- **Staging**: Gibt an, ob der Fehler während der Build-, Bereitstellungs- oder Postbereitstellungsphase aufgetreten ist
- **Schritt**: Gibt den Schritt im Bereitstellungsszenario an, der den Fehler zurückgeben kann. Wenn die Spalte _Schritt_ leer ist, handelt es sich bei dem Fehler um einen allgemeinen Fehler, der von mehreren Schritten oder während Vorverarbeitungsvorgängen zurückgegeben werden kann. Weitere Informationen zu den Schritten zum Erstellen, Bereitstellen und nach der Bereitstellung finden Sie unter [Scenario-basierte Bereitstellung](../deploy/scenario-based.md) .
- **Empfehlung**: Bietet Anleitungen zur Fehlerbehebung und Fehlerbehebung
- **Titel (Fehlerbeschreibung)**: Eine Beschreibung, die die Fehlerursache zusammenfasst
- **Typ**: Gibt an, ob der Fehler ein kritischer Fehler oder eine Warnung ist

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Kritische Fehler

Kritische Fehler weisen auf ein Problem mit der Commerce in der Cloud-Infrastruktur-Projektkonfiguration hin, das zu einem Implementierungsfehler führt, z. B. zu einer falschen, nicht unterstützten oder fehlenden Konfiguration für die erforderlichen Einstellungen. Vor der Bereitstellung müssen Sie die Konfiguration aktualisieren, um diese Fehler zu beheben.

### Build-Phase

| Fehler-Code | Schritt erstellen | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 2 |  | Kann nicht in die Datei `./app/etc/env.php` schreiben | Das Bereitstellungsskript kann keine erforderlichen Änderungen an der Datei `/app/etc/env.php` vornehmen. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 3 |  | Die Konfiguration ist nicht in der Datei `schema.yaml` definiert | Die Konfiguration ist nicht in der Datei `./vendor/magento/ece-tools/config/schema.yaml` definiert. Überprüfen Sie, ob der Name der Konfigurationsvariablen korrekt und definiert ist. |
| 4 |  | Fehler beim Analysieren der `.magento.env.yaml`-Datei | Das `./.magento.env.yaml` -Dateiformat ist ungültig. Verwenden Sie einen YAML-Parser, um die Syntax zu überprüfen und etwaige Fehler zu beheben. |
| 5 |  | Die Datei `.magento.env.yaml` kann nicht gelesen werden | Die Datei `./.magento.env.yaml` kann nicht gelesen werden. Überprüfen Sie die Dateiberechtigungen. |
| 6 |  | Die Datei `.schema.yaml` kann nicht gelesen werden | Die Datei `./vendor/magento/ece-tools/config/magento.env.yaml` kann nicht gelesen werden. Überprüfen Sie die Dateiberechtigungen und stellen Sie sie erneut bereit (`magento-cloud environment:redeploy`). |
| 7 | refresh-modules | Kann nicht in die Datei `./app/etc/config.php` schreiben | Das Bereitstellungsskript kann keine erforderlichen Änderungen an der Datei `/app/etc/config.php` vornehmen. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 8 | validate-config | Die `composer.json`-Datei kann nicht gelesen werden | Die Datei `./composer.json` kann nicht gelesen werden. Überprüfen Sie die Dateiberechtigungen. |
| 9 | validate-config | Die Datei &quot;`composer.json`&quot; fehlt im erforderlichen Abschnitt zum automatischen Laden | Der erforderliche `autoload` -Abschnitt fehlt in der `composer.json` -Datei. Vergleichen Sie den Abschnitt &quot;Autoload&quot;mit der Datei &quot;`composer.json`&quot;in der Cloud-Vorlage und fügen Sie die fehlende Konfiguration hinzu. |
| 10 | validate-config | Die Datei &quot;`.magento.env.yaml`&quot; enthält eine Option, die nicht im Schema deklariert ist, oder eine Option, die mit einem ungültigen Wert oder einer ungültigen Phase konfiguriert wurde | Die Datei `./.magento.env.yaml` enthält eine ungültige Konfiguration. Detaillierte Informationen finden Sie im Fehlerprotokoll . |
| 11 | refresh-modules | Befehl fehlgeschlagen: `/bin/magento module:enable --all` | Versuchen Sie, `composer update` lokal auszuführen. Übertragen Sie dann die aktualisierte `composer.lock` -Datei und pushen Sie sie. Weitere Informationen finden Sie auch unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 12 | apply-patches | Patch nicht angewendet |  |
| 13 | set-report-dir-nesting-level | Kann nicht in die Datei `/pub/errors/local.xml` schreiben |  |
| 14 | copy-sample-data | Beispieldatendateien konnten nicht kopiert werden |  |
| 15 | compile-di | Befehl fehlgeschlagen: `/bin/magento setup:di:compile` | Weitere Informationen finden Sie unter `cloud.log` . Fügen Sie `VERBOSE_COMMANDS: '-vvv'` zu `.magento.env.yaml` hinzu, um eine detailliertere Befehlsausgabe zu erhalten. |
| 16 | dump-autoload | Befehl fehlgeschlagen: `composer dump-autoload` | Der Befehl `composer dump-autoload` ist fehlgeschlagen. Weitere Informationen finden Sie unter `cloud.log` . |
| 17 | Run-Baler | Der Befehl zum Ausführen von `Baler` für JavaScript-Bundle ist fehlgeschlagen. | Überprüfen Sie die Umgebungsvariable `SCD_USE_BALER` , um sicherzustellen, dass das Baler-Modul für das JS-Bundling konfiguriert und aktiviert ist. Wenn Sie das Baler-Modul nicht benötigen, setzen Sie `SCD_USE_BALER: false`. |
| 18 | compress-static-content | Erforderliches Dienstprogramm wurde nicht gefunden (Timeout, Bash) |  |
| 19 | deploy-static-content | Befehl `/bin/magento setup:static-content:deploy` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 20 | compress-static-content | Statische Inhaltskomprimierung fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . |
| 21 | backup-data: static-content | Statischen Inhalt konnte nicht in das Verzeichnis `init` kopiert werden | Weitere Informationen finden Sie unter `cloud.log` . |
| 22 | backup-data: writable-dirs | Fehlgeschlagen beim Kopieren einiger schreibbarer Verzeichnisse in das Verzeichnis `init` | Schreibbare Verzeichnisse konnten nicht in den Ordner `./init` kopiert werden. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 23 |  | Protokollobjekt kann nicht erstellt werden |  |
| 24 | backup-data: static-content | Fehler beim Bereinigen des Verzeichnisses `./init/pub/static/` | Der Ordner `./init/pub/static` konnte nicht gelöscht werden. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 25 |  | Das Composer-Paket kann nicht gefunden werden | Wenn Sie die Adobe Commerce-Anwendungsversion direkt aus dem GitHub-Repository installiert haben, überprüfen Sie, ob die Umgebungsvariable `DEPLOYED_MAGENTO_VERSION_FROM_GIT` konfiguriert ist. |
| 26 | validate-config | Entfernen Sie die Magento Braintree-Modulkonfiguration, die in Adobe Commerce und Magento Open Source 2.4 und höheren Versionen nicht mehr unterstützt wird. | Das Braintree-Modul wird ab Magento 2.4.0 nicht mehr unterstützt. Entfernen Sie die Variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL aus dem Variablenabschnitt der Datei `.magento.app.yaml` . Verwenden Sie stattdessen eine offizielle Erweiterung der Braintree-Zahlungsunterstützung von der Commerce Marketplace. |

### Bereitstellungsphase

| Fehler-Code | Bereitstellungsschritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 101 | pre-deploy: cache | Falsche Cache-Konfiguration (fehlender Port oder Host) | Die Cachekonfiguration fehlt die erforderlichen Parameter `server` oder `port`. Weitere Informationen finden Sie unter `cloud.log` . |
| 102 |  | Kann nicht in die Datei `./app/etc/env.php` schreiben | Das Bereitstellungsskript kann keine erforderlichen Änderungen an der Datei `/app/etc/env.php` vornehmen. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 103 |  | Die Konfiguration ist nicht in der Datei `schema.yaml` definiert | Die Konfiguration ist nicht in der Datei `./vendor/magento/ece-tools/config/schema.yaml` definiert. Überprüfen Sie, ob der Name der Konfigurationsvariablen korrekt ist und ob er definiert ist. |
| 104 |  | Fehler beim Analysieren der `.magento.env.yaml`-Datei | Die Konfiguration ist nicht in der Datei `./vendor/magento/ece-tools/config/schema.yaml` definiert. Überprüfen Sie, ob der Name der Konfigurationsvariablen korrekt ist und ob er definiert ist. |
| 105 |  | Die Datei `.magento.env.yaml` kann nicht gelesen werden | Die Datei `./.magento.env.yaml` kann nicht gelesen werden. Überprüfen Sie die Dateiberechtigungen. |
| 106 |  | Die Datei `.schema.yaml` kann nicht gelesen werden |  |
| 107 | pre-deploy: clean-redis-cache | Redis-Cache konnte nicht gelöscht werden | Redis-Cache konnte nicht gelöscht werden. Überprüfen Sie, ob die Redis-Cache-Konfiguration korrekt ist und ob der Redis-Dienst verfügbar ist. Siehe [Setup Redis-Dienst einrichten](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/redis.html). |
| 108 | pre-deploy: set-production-mode | Befehl `/bin/magento maintenance:enable` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 109 | validate-config | Falsche Datenbankkonfiguration | Überprüfen Sie, ob die Umgebungsvariable `DATABASE_CONFIGURATION` richtig konfiguriert ist. |
| 110 | validate-config | Falsche Sitzungskonfiguration | Überprüfen Sie, ob die Umgebungsvariable `SESSION_CONFIGURATION` richtig konfiguriert ist. Die Konfiguration muss mindestens den Parameter `save` enthalten. |
| 111 | validate-config | Falsche Suchkonfiguration | Überprüfen Sie, ob die Umgebungsvariable `SEARCH_CONFIGURATION` richtig konfiguriert ist. Die Konfiguration muss mindestens den Parameter `engine` enthalten. |
| 112 | validate-config | Falsche Ressourcenkonfiguration | Überprüfen Sie, ob die Umgebungsvariable `RESOURCE_CONFIGURATION` richtig konfiguriert ist. Die Konfiguration muss mindestens den Parameter `connection` enthalten. |
| 113 | validate-config:elasticsuite-integrität | ElasticSuite ist installiert, der Elasticsearch-Dienst ist jedoch nicht verfügbar | Überprüfen Sie, ob die Umgebungsvariable `SEARCH_CONFIGURATION` korrekt konfiguriert ist, und stellen Sie sicher, dass der Elasticsearch-Dienst verfügbar ist. |
| 114 | validate-config:elasticsuite-integrität | ElasticSuite ist installiert, es wird jedoch eine andere Suchmaschine verwendet | ElasticSuite ist installiert, aber eine andere Suchmaschine ist konfiguriert. Aktualisieren Sie die Umgebungsvariable &quot;`SEARCH_CONFIGURATION`&quot;, um Elasticsearch zu aktivieren, und überprüfen Sie die Konfiguration des Elasticsearch-Diensts in der Datei &quot;`services.yaml`&quot;. |
| 115 |  | Ausführung der Datenbankabfrage fehlgeschlagen |  |
| 116 | install-update: setup | Befehl `/bin/magento setup:install` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` und `install_upgrade.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 117 | install-update: config-import | Befehl `app:config:import` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 118 |  | Erforderliches Dienstprogramm wurde nicht gefunden (Timeout, Bash) |  |
| 119 | install-update: deploy-static-content | Befehl `/bin/magento setup:static-content:deploy` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 120 | compress-static-content | Statische Inhaltskomprimierung fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . |
| 121 | deploy-static-content:generate | Die bereitgestellte Version kann nicht aktualisiert werden | Die `./pub/static/deployed_version.txt`-Datei kann nicht aktualisiert werden. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 122 | clean-static-content | Statische Inhaltsdateien konnten nicht bereinigt werden |  |
| 123 | install-update: split-db | Befehl `/bin/magento setup:db-schema:split` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 124 | clean-view-preprocessed | Fehler beim Bereinigen des Ordners `var/view_preprocessed` | Der Ordner `./var/view_preprocessed` kann nicht bereinigt werden. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 125 | install-update: reset-password | Die `/var/credentials_email.txt`-Datei konnte nicht aktualisiert werden | Die `/var/credentials_email.txt` -Datei konnte nicht aktualisiert werden. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 126 | install-update: update | Befehl `/bin/magento setup:upgrade` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` und `install_upgrade.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 127 | clean-cache | Befehl `/bin/magento cache:flush` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Um eine detailliertere Befehlsausgabe zu erhalten, fügen Sie die Option `VERBOSE_COMMANDS: '-vvv'` zur Datei `.magento.env.yaml` hinzu. |
| 128 | disable-maintenance-mode | Befehl `/bin/magento maintenance:disable` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Fügen Sie `VERBOSE_COMMANDS: '-vvv'` zu `.magento.env.yaml` hinzu, um eine detailliertere Befehlsausgabe zu erhalten. |
| 129 | install-update: reset-password | Kennwortvorlage kann nicht zurückgesetzt gelesen werden |  |
| 130 | install-update: cache_type | Befehl fehlgeschlagen: `php ./bin/magento cache:enable` | Der Befehl `php ./bin/magento cache:enable` wird nur ausgeführt, wenn Adobe Commerce installiert wurde, die Datei `./app/etc/env.php` jedoch zu Beginn der Bereitstellung fehlte oder leer war. Weitere Informationen finden Sie unter `cloud.log` . Fügen Sie `VERBOSE_COMMANDS: '-vvv'` zu `.magento.env.yaml` hinzu, um eine detailliertere Befehlsausgabe zu erhalten. |
| 131 | install-update | Der Schlüssel `crypt/key` ist nicht in der Datei `./app/etc/env.php` oder der Cloud-Umgebungsvariablen `CRYPT_KEY` vorhanden | Dieser Fehler tritt auf, wenn die `./app/etc/env.php` -Datei nicht vorhanden ist, wenn die Adobe Commerce-Bereitstellung beginnt, oder wenn der `crypt/key` -Wert nicht definiert ist. Wenn Sie die Datenbank aus einer anderen Umgebung migriert haben, rufen Sie den Wert des Verschlüsselungsschlüssels aus dieser Umgebung ab. Fügen Sie dann den Wert der Cloud-Umgebungsvariablen [CRYPT_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#crypt_key) in Ihrer aktuellen Umgebung hinzu. Siehe [Adobe Commerce-Verschlüsselungsschlüssel](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/overview.html#gather-credentials). Wenn Sie versehentlich die Datei `./app/etc/env.php` entfernt haben, verwenden Sie den folgenden Befehl, um sie aus den Sicherungsdateien wiederherzustellen, die aus einer vorherigen Bereitstellung erstellt wurden: `./vendor/bin/ece-tools backup:restore` CLI-Befehl .&quot; |
| 132 |  | Verbindung zum Elasticsearch-Dienst kann nicht hergestellt werden | Überprüfen Sie, ob gültige Elasticsearch-Anmeldeinformationen vorliegen, und stellen Sie sicher, dass der Dienst ausgeführt wird. |
| 137 |  | Verbindung zum OpenSearch-Dienst nicht möglich | Überprüfen Sie, ob gültige OpenSearch-Anmeldeinformationen vorliegen, und stellen Sie sicher, dass der Dienst ausgeführt wird. |
| 133 | validate-config | Entfernen Sie die Magento Braintree-Modulkonfiguration, die in Adobe Commerce oder Magento Open Source 2.4 und höheren Versionen nicht mehr unterstützt wird. | Das Braintree-Modul wird in Adobe Commerce oder Magento Open Source 2.4.0 und höher nicht mehr unterstützt. Entfernen Sie die Variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL aus dem Variablenabschnitt der Datei `.magento.app.yaml` . Verwenden Sie stattdessen eine offizielle Braintree Payments-Erweiterung von der Commerce Marketplace, um Braintree zu unterstützen. |
| 134 | validate-config | Für Adobe Commerce und Magento Open Source 2.4.0 ist die Installation des Elasticsearch-Diensts erforderlich | Installieren des Elasticsearch-Dienstes |
| 138 | validate-config | Für Adobe Commerce und Magento Open Source 2.4.4 muss der OpenSearch- oder Elasticsearch-Dienst installiert sein. | Installieren des OpenSearch-Dienstes |
| 135 | validate-config | Die Suchmaschine muss auf Elasticsearch für Adobe Commerce und Magento Open Source >= 2.4.0 eingestellt sein. | Überprüfen Sie die Variable SEARCH_CONFIGURATION für die Option `engine` . Wenn sie konfiguriert ist, entfernen Sie die Option oder setzen Sie den Wert auf &quot;elasticsearch&quot;. |
| 136 | validate-config | Die Aufspaltungsdatenbank wurde ab Adobe Commerce und Magento Open Source 2.5.0 entfernt. | Wenn Sie eine geteilte Datenbank verwenden, müssen Sie zu einer einzigen Datenbank zurückkehren oder zu ihr migrieren oder einen anderen Ansatz wählen. |
| 139 | validate-config | Falsche Suchmaschine | Diese Adobe Commerce- oder Magento Open Source-Version unterstützt OpenSearch nicht. Sie müssen die Versionen 2.3.7-p3, 2.4.3-p2 oder höher verwenden. |

### Post-Bereitstellungsphase

| Fehler-Code | Post-Bereitstellungsschritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 201 | is-deploy-failed | Bereitstellungsphase fehlgeschlagen |  |
| 202 |  | Die Datei &quot;`./app/etc/env.php`&quot; kann nicht geschrieben werden | Das Bereitstellungsskript kann keine erforderlichen Änderungen an der Datei `/app/etc/env.php` vornehmen. Überprüfen Sie Ihre Dateisystemberechtigungen. |
| 203 |  | Die Konfiguration ist nicht in der Datei `schema.yaml` definiert | Die Konfiguration ist nicht in der Datei `./vendor/magento/ece-tools/config/schema.yaml` definiert. Überprüfen Sie, ob der Name der Konfigurationsvariablen korrekt ist und ob er definiert ist. |
| 204 |  | Fehler beim Analysieren der `.magento.env.yaml`-Datei | Das `./.magento.env.yaml` -Dateiformat ist ungültig. Verwenden Sie einen YAML-Parser, um die Syntax zu überprüfen und etwaige Fehler zu beheben. |
| 205 |  | Die Datei `.magento.env.yaml` kann nicht gelesen werden | Überprüfen Sie die Dateiberechtigungen. |
| 206 |  | Die Datei `.schema.yaml` kann nicht gelesen werden |  |
| 207 | Warmup | Einige Warmup-Seiten konnten nicht vorab geladen werden |  |
| 208 | Time-to-First-Byte | Test der Zeit bis zum ersten Byte (TTFB) fehlgeschlagen |  |
| 227 | clean-cache | Befehl `/bin/magento cache:flush` fehlgeschlagen | Weitere Informationen finden Sie unter `cloud.log` . Fügen Sie `VERBOSE_COMMANDS: '-vvv'` zu `.magento.env.yaml` hinzu, um eine detailliertere Befehlsausgabe zu erhalten. |

### Allgemein

| Fehler-Code | Allgemeiner Schritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 243 |  | Die Konfiguration ist nicht in der Datei `schema.yaml` definiert | Überprüfen Sie, ob der Name der Konfigurationsvariablen korrekt ist und ob er definiert ist. |
| 244 |  | Fehler beim Analysieren der `.magento.env.yaml`-Datei | Das `./.magento.env.yaml` -Dateiformat ist ungültig. Verwenden Sie einen YAML-Parser, um die Syntax zu überprüfen und etwaige Fehler zu beheben. |
| 245 |  | Die Datei `.magento.env.yaml` kann nicht gelesen werden | Die Datei `./.magento.env.yaml` kann nicht gelesen werden. Überprüfen Sie die Dateiberechtigungen. |
| 246 |  | Die Datei `.schema.yaml` kann nicht gelesen werden |  |
| 247 |  | Modul für Eventing kann nicht generiert werden | Weitere Informationen finden Sie unter `cloud.log` . |
| 248 |  | Modul für Eventing kann nicht aktiviert werden | Weitere Informationen finden Sie unter `cloud.log` . |
| 249 |  | AdobeCommerceWebhookPlugins-Modul konnte nicht generiert werden | Weitere Informationen finden Sie unter `cloud.log` . |
| 250 |  | AdobeCommerceWebhookPlugins-Modul konnte nicht aktiviert werden | Weitere Informationen finden Sie unter `cloud.log` . |

## Warnfehler

Warnungsfehler weisen auf ein Problem mit der Commerce in der Cloud-Infrastruktur-Projektkonfiguration hin, z. B. falsche, veraltete, nicht unterstützte oder fehlende Konfigurationseinstellungen für optionale Funktionen, die sich auf den Site-Betrieb auswirken können. Obwohl eine Warnung keinen Bereitstellungsfehler verursacht, sollten Sie Warnmeldungen überprüfen und die Konfiguration aktualisieren, um sie zu beheben.

### Build-Phase

| Fehler-Code | Schritt erstellen | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 1001 | validate-config | Datei app/etc/config.php ist nicht vorhanden |  |
| 1002 | validate-config | Die ./build_options.ini Datei wird nicht mehr unterstützt |  |
| 1003 | validate-config | Der Modulabschnitt fehlt in der freigegebenen Konfigurationsdatei |  |
| 1004 | validate-config | Die Konfiguration ist nicht mit dieser Magento-Version kompatibel |  |
| 1005 | validate-config | SCD-Optionen ignoriert |  |
| 1006 | validate-config | Der konfigurierte Status ist nicht ideal. |  |
| 1007 | Run-Baler | Baler JS Bundling kann nicht verwendet werden |  |

### Bereitstellungsphase

| Fehler-Code | Bereitstellungsschritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 2001 | pre-deploy:cache | Der Cache ist für einen Redis-Dienst konfiguriert, der nicht verfügbar ist. Die Konfiguration wird ignoriert. |  |
| 2002 | validate-config | Der konfigurierte Status ist nicht ideal. |  |
| 2003 | validate-config | Der Wert der Verschachtelungsebene für Fehlerberichte wurde nicht konfiguriert. |  |
| 2004 | validate-config | Ungültige Konfiguration in der ./pub/errors/local.xml. |  |
| 2005 | validate-config | Admin-Daten dienen nur zur Erstellung eines Admin-Benutzers während der ersten Installation. Änderungen an den Admin-Daten werden während des Aktualisierungsprozesses ignoriert. | Nach der ersten Installation können Sie Administratordaten aus der Konfiguration entfernen. |
| 2006 | validate-config | Admin-Benutzer wurde nicht erstellt, da keine Admin-E-Mail festgelegt wurde. | Nach der Installation können Sie einen Admin-Benutzer manuell erstellen: Verwenden Sie ssh, um eine Verbindung zu Ihrer Umgebung herzustellen. Führen Sie dann den Befehl `bin/magento admin:user:create` aus. |
| 2007 | validate-config | Aktualisieren der PHP-Version auf die empfohlene Version |  |
| 2008 | validate-config | Die Solr-Unterstützung wird in Adobe Commerce und Magento Open Source 2.1 nicht mehr unterstützt. |  |
| 2009 | validate-config | Solr wird von Adobe Commerce und Magento Open Source 2.2 oder höher nicht mehr unterstützt. |  |
| 2010 | validate-config | Der Elasticsearch-Dienst wird auf der Infrastrukturebene installiert, jedoch nicht als Suchmaschine. | Erwägen Sie, den Elasticsearch-Dienst aus der Infrastrukturschicht zu entfernen, um die Ressourcennutzung zu optimieren. |
| 2011 | validate-config | Die Elasticsearch-Service-Version auf der Infrastrukturschicht ist nicht mit der aktuellen Version des Elasticsearch-/Elasticsearch-Moduls kompatibel, das von Ihrer Adobe Commerce-Anwendung verwendet wird. |  |
| 2012 | validate-config | Die aktuelle Konfiguration ist nicht mit dieser Version von Adobe Commerce kompatibel |  |
| 2013 | validate-config | SCD-Optionen wurden ignoriert, da der Bereitstellungsprozess nicht in der Build-Phase ausgeführt wurde |  |
| 2014 | validate-config | Die Konfiguration enthält veraltete Variablen oder Werte |  |
| 2015 | validate-config | Die Konfiguration der Umgebung ist nicht gültig. |  |
| 2016 | validate-config | Die Konfiguration des JSON-Typs kann nicht dekodiert werden |  |
| 2017 | validate-config | Die aktuelle Konfiguration ist nicht mit dieser Version von Adobe Commerce kompatibel |  |
| 2018 | validate-config | Einige Dienste sind an EOL übergeben worden |  |
| 2019 | validate-config | Die Konfigurationsoption für die MySQL-Suche ist veraltet | Verwenden Sie stattdessen Elasticsearch. |
| 2029 | validate-config | Die Aufspaltungsdatenbank wird in Adobe Commerce und Magento Open Source 2.4.2 nicht mehr unterstützt und in Version 2.5 entfernt. | Wenn Sie eine geteilte Datenbank verwenden, sollten Sie mit der Planung beginnen, zu einer einzigen Datenbank zurückzukehren oder zu dieser zu migrieren, oder Sie sollten einen alternativen Ansatz verwenden. |
| 2020 | install-update | Adobe Commerce-Installation abgeschlossen, aber die Konfigurationsdatei `app/etc/env.php` fehlte oder war leer. | Die erforderlichen Daten werden aus Umgebungskonfigurationen und aus der Datei .magento.env.yaml wiederhergestellt. |
| 2021 | install-update:db-connection | Für geteilte Datenbanken verwendete benutzerdefinierte Verbindungen |  |
| 2022 | install-update:db-connection | Sie haben eine Datenbankkonfiguration geändert, die nicht mit der Slave-Verbindung kompatibel ist. |  |
| 2023 | install-update:split-db | Die Aktivierung einer geteilten Datenbank wird übersprungen. |  |
| 2024 | install-update:split-db | Die Variable SPLIT_DB fehlt die Konfiguration für die Aufspaltungsverbindungstypen. |  |
| 2025 | install-update:split-db | Slave-Verbindung nicht eingestellt. |  |
| 2026 | pre-deploy:restore-writable-dirs | Fehlgeschlagene Wiederherstellung einiger Daten, die während der Build-Phase in den bereitgestellten Verzeichnissen generiert wurden | Weitere Informationen finden Sie unter `cloud.log` . |
| 2027 | validate-config:mage-mode-variable | Moduswert für die Umgebungsvariable MAGE_MODE nicht unterstützt | Entfernen Sie die Umgebungsvariable MAGE_MODE oder ändern Sie ihren Wert in &quot;Produktion&quot;. Adobe Commerce in der Cloud-Infrastruktur unterstützt nur den Produktionsmodus. |
| 2028 | Remote-Speicher | Remote-Speicher konnte nicht aktiviert werden. | Überprüfen Sie die Anmeldeinformationen für den Remote-Speicher. |
| 2030 | validate-config | Elasticsearch- und OpenSearch-Dienste werden beide auf Infrastrukturebene installiert. Adobe Commerce und Magento Open Source 2.4.4 und höher verwenden standardmäßig OpenSearch | Erwägen Sie, den Elasticsearch- oder OpenSearch-Dienst aus der Infrastrukturschicht zu entfernen, um die Ressourcennutzung zu optimieren. |

### Post-Bereitstellungsphase

| Fehler-Code | Post-Bereitstellungsschritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 3001 | validate-config | Die Debug-Protokollierung ist in Adobe Commerce aktiviert | Um Speicherplatz zu sparen, aktivieren Sie keine Debug-Protokollierung für Ihre Produktionsumgebungen. |
| 3002 | Warmup | Store-URLs können nicht abgerufen werden |  |
| 3003 | Warmup | Store-URL kann nicht abgerufen werden |  |
| 3004 | Backup | Backup-Dateien können nicht erstellt werden |  |

### Allgemein

| Fehler-Code | Allgemeiner Schritt | Fehlerbeschreibung (Titel) | Vorgeschlagene Aktion |
| - | - | - | - |
| 4001 |  | Die Anzahl der Systemprozessoren kann nicht abgerufen werden: |  |
