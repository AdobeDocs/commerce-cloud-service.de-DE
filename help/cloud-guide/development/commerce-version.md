---
title: Upgrade der Commerce-Version
description: Erfahren Sie, wie Sie die Adobe Commerce-Version im Cloud-Infrastrukturprojekt aktualisieren.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Upgrade der Commerce-Version

Sie können die Codebasis von Adobe Commerce auf eine neuere Version aktualisieren. Bevor Sie Ihr Projekt aktualisieren, lesen Sie die [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im Handbuch _Installation_ , um die neuesten Anforderungen für die Softwareversion anzuzeigen.

Abhängig von Ihrer Projektkonfiguration können Ihre Aktualisierungsaufgaben Folgendes umfassen:

- Aktualisierungsdienste wie MariaDB (MySQL), OpenSearch, RabbitMQ und Redis für die Kompatibilität mit neuen Adobe Commerce-Versionen.
- Konvertieren Sie eine ältere Konfigurationsverwaltungsdatei.
- Aktualisieren Sie die Datei `.magento.app.yaml` mit neuen Einstellungen für Hooks und Umgebungsvariablen.
- Aktualisieren Sie Drittanbietererweiterungen auf die neueste unterstützte Version.
- Aktualisieren Sie die Datei &quot;`.gitignore`&quot;.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade von älteren Versionen

Wenn Sie ein Upgrade von einer Commerce-Version starten, die älter als 2.1 ist, können einige Einschränkungen in der Adobe Commerce-Codebasis Ihre Fähigkeit beeinträchtigen, __ auf eine bestimmte ECE-Tools-Version oder auf _Upgrade_ auf die nächste unterstützte Commerce-Version zu aktualisieren. Verwenden Sie die folgende Tabelle, um den besten Pfad zu ermitteln:

| Aktuelle Version | Aktualisierungspfad |
| ----------------- | ------------ |
| 2.1.3 und früher | Aktualisieren Sie Adobe Commerce auf Version 2.1.4 oder höher, bevor Sie fortfahren. Führen Sie dann ein [ einmaliges Upgrade durch, um ECE-Tools](../dev-tools/install-package.md) zu installieren. |
| 2.1.4 - 2.1.14 | [ECE-Tools](../dev-tools/update-package.md)-Paket aktualisieren.<br>Siehe Versionshinweise für die Versionen [2002.0.9](../release-notes/cloud-release-archive.md#v200209) und höher 2002.0.x . |
| 2.1.15 - 2.1.16 | [ECE-Tools](../dev-tools/update-package.md)-Paket aktualisieren.<br>Siehe Versionshinweise für [2002.0.9](../release-notes/cloud-release-archive.md#v200209) und höher. |
| 2.2.x und höher | [ECE-Tools](../dev-tools/update-package.md)-Paket aktualisieren.<br>Siehe Versionshinweise für [2002.0.8](../release-notes/cloud-release-archive.md#v200208) und höher. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Konfigurationsverwaltung

In älteren Versionen von Adobe Commerce, z. B. 2.1.4 oder höher bis 2.2.x oder höher, wurde eine `config.local.php` -Datei für die Konfigurationsverwaltung verwendet. Adobe Commerce-Version 2.2.0 und höher verwenden die Datei &quot;`config.php`&quot;, die genau wie die Datei &quot;`config.local.php`&quot;funktioniert, aber unterschiedliche Konfigurationseinstellungen aufweist, die eine Liste der aktivierten Module und zusätzliche Konfigurationsoptionen enthalten.

Beim Aktualisieren von einer älteren Version müssen Sie die Datei &quot;`config.local.php`&quot;migrieren, um die neuere Datei &quot;`config.php`&quot;zu verwenden. Führen Sie die folgenden Schritte aus, um Ihre Konfigurationsdatei zu sichern und eine zu erstellen.

**So erstellen Sie eine temporäre `config.php` Datei**:

1. Erstellen Sie eine Kopie der Datei &quot;`config.local.php`&quot; und nennen Sie sie &quot;`config.php`&quot;.

1. Fügen Sie diese Datei zum Ordner `app/etc` Ihres Projekts hinzu.

1. Fügen Sie die Datei hinzu und übertragen Sie sie in Ihre Verzweigung.

1. Schicken Sie die Datei an Ihre Integrationsverzweigung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

>[!WARNING]
>
>Nach dem Upgrade können Sie die Datei &quot;`config.php`&quot; entfernen und eine neue, vollständige Datei erstellen. Sie können diese Datei nur löschen, um sie dieses Mal zu ersetzen. Nach dem Generieren einer neuen, vollständigen `config.php` -Datei können Sie die Datei nicht löschen, um eine neue zu generieren. Siehe [Konfigurationsverwaltung und Pipeline-Bereitstellung](../store/store-settings.md).

### Überprüfen der Abhängigkeiten von Zend Framework Composer

Stellen Sie beim Upgrade auf **2.3.x oder höher von 2.2.x** sicher, dass die Zend Framework-Abhängigkeiten zur Eigenschaft `autoload` der Datei `composer.json` hinzugefügt wurden, um Laminas zu unterstützen. Dieses Plug-in unterstützt neue Anforderungen für das Zend Framework, das zum Laminas-Projekt migriert wurde. Siehe [Migration des Zend Framework zum Laminas-Projekt](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) auf dem _Magento DevBlog_.

**Überprüfen der `auto-load:psr-4` Konfiguration**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Sehen Sie sich Ihre Integrationsverzweigung an.

1. Öffnen Sie die Datei &quot;`composer.json`&quot; in einem Texteditor.

1. Überprüfen Sie den Abschnitt `autoload:psr-4` für die Implementierung des Zend-Plug-in-Managers für die Abhängigkeit der Controller.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Wenn die Zend-Abhängigkeit fehlt, aktualisieren Sie die Datei &quot;`composer.json`&quot;:

   - Fügen Sie die folgende Zeile zum Abschnitt `autoload:psr-4` hinzu.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Aktualisieren Sie die Projektabhängigkeiten.

     ```bash
     composer update
     ```

   - Hinzufügen, Übertragen und Push-Code-Änderungen.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Zusammenführen von Änderungen in der Staging-Umgebung und dann in der Produktion.

## Konfigurationsdateien

Vor der Aktualisierung des Programms müssen Sie Ihre Projektkonfigurationsdateien aktualisieren, um Änderungen an den Standardkonfigurationseinstellungen für Adobe Commerce in der Cloud-Infrastruktur oder der Anwendung zu berücksichtigen. Die neuesten Standardeinstellungen finden Sie im [magento-cloud GitHub-Repository](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Überprüfen Sie stets die Werte in der Datei [.magento.app.yaml](../application/configure-app-yaml.md) für Ihre installierte Version, da sie steuert, wie Ihre Anwendung erstellt und in der Cloud-Infrastruktur bereitgestellt wird. Das folgende Beispiel bezieht sich auf Version 2.4.7 und verwendet Composer 2.7.2. Die Eigenschaft `build: flavor:` wird nicht für Composer 2.x verwendet; siehe [Installieren und Verwenden von Composer 2](../application/properties.md#installing-and-using-composer-2).

**Aktualisieren der `.magento.app.yaml`-Datei**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Öffnen und bearbeiten Sie die Datei &quot;`magento.app.yaml`&quot;.

1. Aktualisieren Sie die PHP-Optionen.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Ändern Sie die Befehle `hooks` property `build` und `deploy`.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Fügen Sie die folgenden Umgebungsvariablen am Ende der Datei hinzu.

   Für Adobe Commerce 2.2.x bis 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Für Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Speichern Sie die Datei. Übertragen oder pushen Sie noch keine Änderungen in die Remote-Umgebung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

### composer.json

Überprüfen Sie vor dem Upgrade immer, ob die Abhängigkeiten in der Datei `composer.json` mit der Adobe Commerce-Version kompatibel sind.

**Aktualisieren der `composer.json`-Datei für Adobe Commerce-Version 2.4.4 und höher**:

1. Fügen Sie dem Abschnitt `config` den folgenden `allow-plugins` hinzu:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Fügen Sie dem Abschnitt `require` das folgende Plug-in hinzu:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Fügen Sie die folgende Komponente zum Abschnitt `extra:component_paths` hinzu:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Speichern Sie die Datei. Übertragen oder pushen Sie noch keine Änderungen in Ihren Zweig.

1. Fahren Sie mit dem Upgrade-Prozess fort.

## Projektsicherung

Es wird empfohlen, vor einer Aktualisierung eine Sicherungskopie Ihres Projekts zu erstellen. Führen Sie die folgenden Schritte aus, um Ihre Integration-, Staging- und Produktionsumgebungen zu sichern.

**Sichern der Datenbank und des Codes der Integrationsumgebung**:

1. Erstellen Sie eine lokale Sicherung der Remote-Datenbank.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Der Befehl `magento-cloud db:dump` führt den Befehl [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) mit dem Flag `--single-transaction` aus, mit dem Sie Ihre Datenbank sichern können, ohne die Tabellen zu sperren.

1. Sichern Sie Code und Medien.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Optional können Sie `[--media]` auslassen, wenn Sie eine große Anzahl statischer Dateien haben, die sich bereits in der Quell-Code-Verwaltung befinden.

**So sichern Sie die Datenbank der Staging- oder Produktionsumgebung vor der Bereitstellung von**:

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

1. Erstellen Sie einen [Datenbank-Dump](../storage/database-dump.md). Verwenden Sie die Option `--dump-directory` , um ein Zielverzeichnis für den DB-Dump auszuwählen.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Der Dump-Vorgang erstellt eine `dump-<timestamp>.sql.gz` -Archivdatei in Ihrem Remote-Projektverzeichnis. Siehe [Datenbank sichern](../storage/database-dump.md).

## Anwendungsaktualisierung

Überprüfen Sie die Informationen zu den [Dienstversionen](../services/services-yaml.md#service-versions) auf die neuesten Anforderungen an die Softwareversion, bevor Sie Ihre Anwendung aktualisieren.

**Aktualisieren der Anwendungsversion**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Legen Sie die Upgrade-Version mit der Syntax der Versionsbegrenzung [ fest.](overview.md#cloud-metapackage)

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Sie müssen die Syntax der Versionsbegrenzung verwenden, um das `ece-tools` -Paket erfolgreich zu aktualisieren. Sie finden die Versionsbeschränkung in der Datei `composer.json` für die Version der [Anwendungsvorlage](https://github.com/magento/magento-cloud/blob/master/composer.json), die Sie für das Upgrade verwenden.

1. Aktualisieren Sie das Projekt.

   ```bash
   composer update
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` ist erforderlich, um alle geänderten Dateien zur Quell-Code-Verwaltung hinzuzufügen, da der Composer Basispakete marshallt. Sowohl `composer install` als auch `composer update` Marshalldateien aus dem Basispaket (`magento/magento2-base` und `magento/magento2-ee-base`) in den Paketstamm.

   Die Dateien, die Composer marschiert, gehören zur neuen Version von Adobe Commerce, um die veraltete Version dieser Dateien zu überschreiben. Derzeit ist das Marshalling in Adobe Commerce deaktiviert. Daher müssen Sie die marshaled -Dateien zur Quell-Code-Verwaltung hinzufügen.

1. Warten Sie, bis die Bereitstellung abgeschlossen ist.

1. Überprüfen Sie das Upgrade in Ihrer Integration-, Staging- oder Produktionsumgebung, indem Sie SSH verwenden, um sich anzumelden und die Version zu überprüfen.

   ```bash
   php bin/magento --version
   ```

### Erstellen einer Datei &quot;config.php&quot;

Wie in [Konfigurationsverwaltung](#configuration-management) erwähnt, müssen Sie nach der Aktualisierung eine aktualisierte `config.php` -Datei erstellen. Schließen Sie alle weiteren Konfigurationsänderungen über den Admin in Ihrer Integrationsumgebung ab.

**Erstellen einer systemspezifischen Konfigurationsdatei**:

1. Verwenden Sie vom Terminal einen SSH-Befehl, um die Datei `/app/etc/config.php` für die Umgebung zu generieren.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Beispiel: Führen Sie für Pro den `scd-dump` -Vorgang für die Verzweigung `integration` aus:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Übertragen Sie die `config.php` -Datei mit `rsync` oder `scp` auf Ihre lokalen Workstations. Sie können diese Datei nur lokal zum Zweig hinzufügen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Dadurch wird eine aktualisierte `/app/etc/config.php` -Datei mit einer Modulliste und Konfigurationseinstellungen generiert.

>[!WARNING]
>
>Bei einem Upgrade löschen Sie die Datei &quot;`config.php`&quot;. Nachdem diese Datei zum Code hinzugefügt wurde, sollten Sie sie **nicht** löschen. Wenn Sie Einstellungen entfernen oder bearbeiten müssen, bearbeiten Sie die Datei manuell.

### Erweiterungen aktualisieren

Überprüfen Sie Ihre Seiten mit Drittanbietererweiterungen und -modulen in Marketplace oder anderen Unternehmens-Sites und überprüfen Sie die Unterstützung für Adobe Commerce und Adobe Commerce in der Cloud-Infrastruktur. Wenn Sie Erweiterungen und Module von Drittanbietern aktualisieren müssen, empfiehlt Adobe, in einer neuen Integrationsverzweigung zu arbeiten, wobei Ihre Erweiterungen deaktiviert sind.

**Überprüfen und Aktualisieren Ihrer Erweiterungen**:

1. Erstellen Sie eine Verzweigung auf Ihrer lokalen Workstation.

1. Deaktivieren Sie Ihre Erweiterungen nach Bedarf.

1. Sofern verfügbar, laden Sie Erweiterungs-Upgrades herunter.

1. Installieren Sie das Upgrade wie in der Dokumentation von Drittanbietern beschrieben.

1. Aktivieren und testen Sie die Erweiterung.

1. Fügen Sie die Codeänderungen hinzu, übertragen Sie sie und übertragen Sie sie auf die Remote-Umgebung.

1. Senden Sie Push-Benachrichtigungen an Ihre Integrationsumgebung und testen Sie sie.

1. Push in die Staging-Umgebung, um sie in einer Produktionsumgebung zu testen.

Adobe empfiehlt dringend, die Produktionsumgebung _vor_ einschließlich der aktualisierten Erweiterungen im Site-Startprozess zu aktualisieren.

>[!NOTE]
>
>Wenn Sie Ihre Anwendungsversion aktualisieren, wird der Aktualisierungsprozess automatisch auf die neueste Version des [Fastly CDN-Moduls](../cdn/fastly.md#fastly-cdn-module-for-magento-2) aktualisiert.

## Fehlerbehebung bei der Aktualisierung

Wenn das Upgrade fehlgeschlagen ist, erhalten Sie eine Fehlermeldung im Browser, die darauf hinweist, dass Sie nicht auf Ihre Storefront oder das Admin-Bedienfeld zugreifen können:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**So beheben Sie den Fehler**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Öffnen Sie die Datei &quot;`./app/var/report/<error number>`&quot;.

1. [Überprüfen Sie die Protokolle](../test/log-locations.md) und ermitteln Sie die Quelle des Problems.

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
