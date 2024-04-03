---
title: Upgrade der Commerce-Version
description: Erfahren Sie, wie Sie die Adobe Commerce-Version im Cloud-Infrastrukturprojekt aktualisieren.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 745a9f08353bd5dfbb871ca88947157c145c7c70
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Upgrade der Commerce-Version

Sie können die Codebasis von Adobe Commerce auf eine neuere Version aktualisieren. Lesen Sie vor der Aktualisierung Ihres Projekts die [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im _Installation_ Anleitung für die neuesten Softwareversionsanforderungen.

Abhängig von Ihrer Projektkonfiguration können Ihre Aktualisierungsaufgaben Folgendes umfassen:

- Aktualisierungsdienste wie MariaDB (MySQL), OpenSearch, RabbitMQ und Redis für die Kompatibilität mit neuen Adobe Commerce-Versionen.
- Konvertieren Sie eine ältere Konfigurationsverwaltungsdatei.
- Aktualisieren Sie die `.magento.app.yaml` -Datei mit neuen Einstellungen für Hooks und Umgebungsvariablen.
- Aktualisieren Sie Drittanbietererweiterungen auf die neueste unterstützte Version.
- Aktualisieren Sie die `.gitignore` -Datei.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade von älteren Versionen

Wenn Sie ein Upgrade von einer Commerce-Version starten, die älter als 2.1 ist, können einige Einschränkungen in der Adobe Commerce-Codebasis Ihre Fähigkeit beeinträchtigen, _update_ zu einer bestimmten ECE-Tools-Version oder _Upgrade_ zur nächsten unterstützten Commerce-Version. Verwenden Sie die folgende Tabelle, um den besten Pfad zu ermitteln:

| Aktuelle Version | Aktualisierungspfad |
| ----------------- | ------------ |
| 2.1.3 und früher | Aktualisieren Sie Adobe Commerce auf Version 2.1.4 oder höher, bevor Sie fortfahren. Führen Sie anschließend eine [einmalige Aktualisierung zur Installation der ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für [2002,0,9](../release-notes/cloud-release-archive.md#v200209) und späteren Versionen von 2002.0.x. |
| 2.1.15 - 2.1.16 | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für[2002,0,9](../release-notes/cloud-release-archive.md#v200209) und höher. |
| 2.2.x und höher | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für[2002.0.8](../release-notes/cloud-release-archive.md#v200208) und höher. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Konfigurationsverwaltung

In älteren Versionen von Adobe Commerce, z. B. 2.1.4 oder höher bis 2.2.x oder höher, wurde ein `config.local.php` Datei für die Konfigurationsverwaltung. Adobe Commerce-Version 2.2.0 und höher verwenden Sie die `config.php` -Datei, die genau wie die `config.local.php` -Datei enthält, jedoch unterschiedliche Konfigurationseinstellungen, die eine Liste der aktivierten Module und zusätzliche Konfigurationsoptionen enthalten.

Bei der Aktualisierung von einer älteren Version müssen Sie die `config.local.php` -Datei, um die neuere `config.php` -Datei. Führen Sie die folgenden Schritte aus, um Ihre Konfigurationsdatei zu sichern und eine zu erstellen.

**So erstellen Sie eine temporäre `config.php` file**:

1. Erstellen Sie eine Kopie von `config.local.php` Datei und Namen `config.php`.

1. Fügen Sie diese Datei der `app/etc` Ordner Ihres Projekts.

1. Fügen Sie die Datei hinzu und übertragen Sie sie in Ihre Verzweigung.

1. Schicken Sie die Datei an Ihre Integrationsverzweigung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

>[!WARNING]
>
>Nach dem Upgrade können Sie die `config.php` und generieren Sie eine neue, vollständige Datei. Sie können diese Datei nur löschen, um sie dieses Mal zu ersetzen. Nach der Generierung eines neuen `config.php` -Datei, können Sie die Datei nicht löschen, um eine neue zu generieren. Siehe [Konfigurationsverwaltung und Pipelinebereitstellung](../store/store-settings.md).

### Überprüfen der Abhängigkeiten von Zend Framework Composer

Bei der Aktualisierung auf **2.3.x oder höher ab 2.2.x**, überprüfen Sie, ob die Zend Framework-Abhängigkeiten zum `autoload` -Eigenschaft der `composer.json` Datei zur Unterstützung von Laminas. Dieses Plug-in unterstützt neue Anforderungen für das Zend Framework, das zum Laminas-Projekt migriert wurde. Siehe [Migration des Zend Framework zum Laminas-Projekt](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) auf _Magento DevBlog_.

**So überprüfen Sie die `auto-load:psr-4` Konfiguration**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Sehen Sie sich Ihre Integrationsverzweigung an.

1. Öffnen Sie die `composer.json` in einem Texteditor.

1. Überprüfen Sie die `autoload:psr-4` -Abschnitt für die Zend-Plug-in-Manager-Implementierung für die Abhängigkeit von Controllern.

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

1. Wenn die Zend-Abhängigkeit fehlt, aktualisieren Sie die `composer.json` Datei:

   - Fügen Sie die folgende Zeile zur `autoload:psr-4` Abschnitt.

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

Vor der Aktualisierung des Programms müssen Sie Ihre Projektkonfigurationsdateien aktualisieren, um Änderungen an den Standardkonfigurationseinstellungen für Adobe Commerce in der Cloud-Infrastruktur oder der Anwendung zu berücksichtigen. Die neuesten Standardeinstellungen finden Sie im [Magento-Cloud-GitHub-Repository](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Überprüfen Sie immer die Werte, die in der [.magento.app.yaml](../application/configure-app-yaml.md) -Datei für Ihre installierte Version, da sie steuert, wie Ihre Anwendung erstellt und in der Cloud-Infrastruktur bereitgestellt wird. Das folgende Beispiel bezieht sich auf Version 2.4.6 und verwendet Composer 2.2.21. Die `build: flavor:` -Eigenschaft nicht für Composer 2.x verwendet wird; siehe [Installieren und Verwenden von Composer 2](../application/properties.md#installing-and-using-composer-2).

**So aktualisieren Sie die `.magento.app.yaml` file**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Öffnen und bearbeiten Sie die `magento.app.yaml` -Datei.

1. Aktualisieren Sie die PHP-Optionen.

   ```yaml
   type: php:8.2
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.2.21'
   ```

1. Ändern Sie die `hooks` property `build` und `deploy` Befehle.

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

Überprüfen Sie vor der Aktualisierung immer, ob die Abhängigkeiten in der `composer.json` -Datei mit der Adobe Commerce-Version kompatibel sind.

**So aktualisieren Sie die `composer.json` Datei für Adobe Commerce Version 2.4.4 und höher**:

1. Fügen Sie Folgendes hinzu: `allow-plugins` der `config` Abschnitt:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Fügen Sie das folgende Plug-in zum `require` Abschnitt:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Fügen Sie die folgende Komponente zum `extra:component_paths` Abschnitt:

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
   >Die `magento-cloud db:dump` -Befehl führt die [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) mit dem Befehl `--single-transaction` -Markierung, mit der Sie Ihre Datenbank sichern können, ohne die Tabellen zu sperren.

1. Sichern Sie Code und Medien.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Optional können Sie `[--media]` wenn Sie über eine große Anzahl statischer Dateien verfügen, die sich bereits in der Quell-Code-Verwaltung befinden.

**Sichern der Staging- oder Produktionsumgebung-Datenbank vor der Bereitstellung**:

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

1. Erstellen Sie eine [Datenbank-Dump](../storage/database-dump.md). Um ein Zielverzeichnis für den DB-Dump auszuwählen, verwenden Sie die `--dump-directory` -Option.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Der Dump-Vorgang erstellt eine `dump-<timestamp>.sql.gz` Archivdatei in Ihrem Remote-Projektverzeichnis. Siehe [Datenbank sichern](../storage/database-dump.md).

## Anwendungsaktualisierung

Überprüfen Sie die [Service-Versionen](../services/services-yaml.md#service-versions) Informationen zu den neuesten Anforderungen an die Softwareversion vor der Aktualisierung Ihrer Anwendung.

**Aktualisierung der Anwendungsversion**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Legen Sie die Upgrade-Version mit dem [Syntax für Versionsbeschränkungen](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Sie müssen die Syntax der Versionseinschränkungen verwenden, um die `ece-tools` Paket. Die Versionsbegrenzung finden Sie im Abschnitt `composer.json` -Datei für die Version der [Anwendungsvorlage](https://github.com/magento/magento-cloud/blob/master/composer.json) Sie für das Upgrade verwenden.

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

   `git add -A` ist erforderlich, um alle geänderten Dateien zur Quell-Code-Verwaltung hinzuzufügen, da der Composer Basispakete marshallt. Beide `composer install` und `composer update` Marshalldateien aus dem Basispaket (`magento/magento2-base` und `magento/magento2-ee-base`) in den Paketstamm.

   Die Dateien, die Composer marschiert, gehören zur neuen Version von Adobe Commerce, um die veraltete Version dieser Dateien zu überschreiben. Derzeit ist das Marshalling in Adobe Commerce deaktiviert. Daher müssen Sie die marshaled -Dateien zur Quell-Code-Verwaltung hinzufügen.

1. Warten Sie, bis die Bereitstellung abgeschlossen ist.

1. Überprüfen Sie das Upgrade in Ihrer Integration-, Staging- oder Produktionsumgebung, indem Sie SSH verwenden, um sich anzumelden und die Version zu überprüfen.

   ```bash
   php bin/magento --version
   ```

### Erstellen einer Datei &quot;config.php&quot;

Wie bereits erwähnt [Konfigurationsverwaltung](#configuration-management)nach der Aktualisierung müssen Sie eine aktualisierte `config.php` -Datei. Schließen Sie alle weiteren Konfigurationsänderungen über den Admin in Ihrer Integrationsumgebung ab.

**So erstellen Sie eine systemspezifische Konfigurationsdatei**:

1. Verwenden Sie im Terminal einen SSH-Befehl, um die `/app/etc/config.php` -Datei für die -Umgebung.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Beispiel: Für Pro können Sie die `scd-dump` auf `integration` branch:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Übertragen Sie die `config.php` Datei auf Ihren lokalen Workstations mithilfe von `rsync` oder `scp`. Sie können diese Datei nur lokal zum Zweig hinzufügen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Dadurch wird eine aktualisierte `/app/etc/config.php` -Datei mit einer Modulliste und Konfigurationseinstellungen.

>[!WARNING]
>
>Bei einer Aktualisierung löschen Sie die `config.php` -Datei. Sobald diese Datei Ihrem Code hinzugefügt wurde, sollten Sie **not** Löschen Sie sie. Wenn Sie Einstellungen entfernen oder bearbeiten müssen, bearbeiten Sie die Datei manuell.

### Erweiterungen aktualisieren

Überprüfen Sie Ihre Seiten mit Drittanbietererweiterungen und -modulen in Marketplace oder anderen Unternehmens-Sites und überprüfen Sie die Unterstützung für Adobe Commerce und Adobe Commerce in der Cloud-Infrastruktur. Wenn Sie Erweiterungen und Module von Drittanbietern aktualisieren müssen, empfiehlt Adobe, in einer neuen Integrationsverzweigung zu arbeiten, wobei Ihre Erweiterungen deaktiviert sind.

**Überprüfen und Aktualisieren von Erweiterungen**:

1. Erstellen Sie eine Verzweigung auf Ihrer lokalen Workstation.

1. Deaktivieren Sie Ihre Erweiterungen nach Bedarf.

1. Sofern verfügbar, laden Sie Erweiterungs-Upgrades herunter.

1. Installieren Sie das Upgrade wie in der Dokumentation von Drittanbietern beschrieben.

1. Aktivieren und testen Sie die Erweiterung.

1. Fügen Sie die Codeänderungen hinzu, übertragen Sie sie und übertragen Sie sie auf die Remote-Umgebung.

1. Senden Sie Push-Benachrichtigungen an Ihre Integrationsumgebung und testen Sie sie.

1. Push in die Staging-Umgebung, um sie in einer Produktionsumgebung zu testen.

Adobe empfiehlt dringend, die Produktionsumgebung zu aktualisieren _before_ einschließlich der aktualisierten Erweiterungen in Ihrem Site-Launch-Prozess.

>[!NOTE]
>
>Wenn Sie Ihre Anwendungsversion aktualisieren, wird der Aktualisierungsprozess auf die neueste Version des [Fastly CDN-Modul](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatisch.

## Fehlerbehebung bei der Aktualisierung

Wenn das Upgrade fehlgeschlagen ist, erhalten Sie eine Fehlermeldung im Browser, die darauf hinweist, dass Sie nicht auf Ihre Storefront oder das Admin-Bedienfeld zugreifen können:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Beheben des Fehlers**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Öffnen Sie die `./app/var/report/<error number>` -Datei.

1. [Logs untersuchen](../test/log-locations.md) und bestimmen die Quelle des Problems.

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
