---
title: Commerce-Version aktualisieren
description: Erfahren Sie, wie Sie die Adobe Commerce-Version im Cloud-Infrastrukturprojekt aktualisieren.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Commerce-Version aktualisieren

Sie können die Adobe Commerce-Code-Basis auf eine neuere Version aktualisieren. Überprüfen Sie vor dem Upgrade Ihres Projekts die Datei [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in der _Installation_ Anleitung für die neuesten Anforderungen an die Softwareversion.

Abhängig von Ihrer Projektkonfiguration können Ihre Upgrade-Aufgaben Folgendes umfassen:

- Aktualisierungsdienste wie MariaDB (MySQL), OpenSearch, RabbitMQ und Redis für die Kompatibilität mit neuen Adobe Commerce-Versionen.
- Konvertieren Sie eine ältere Konfigurationsverwaltungsdatei.
- Aktualisieren von `.magento.app.yaml` -Datei mit neuen Einstellungen für Erweiterungspunkte und Umgebungsvariablen.
- Aktualisieren Sie Erweiterungen von Drittanbietern auf die neueste unterstützte Version.
- Aktualisieren von `.gitignore` -Datei.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade von älteren Versionen

Wenn Sie ein Upgrade von einer Commerce-Version starten, die älter als 2.1 ist, können einige Einschränkungen in der Adobe Commerce-Code-Basis Ihre Möglichkeiten beeinträchtigen, _Aktualisierung_ für eine bestimmte ECE-Tools-Version oder _Upgrade_ zur nächsten unterstützten Commerce-Version wechseln. Verwenden Sie die folgende Tabelle, um den besten Pfad zu ermitteln:

| Aktuelle Version | Aktualisierungspfad |
| ----------------- | ------------ |
| 2.1.3 und früher | Aktualisieren Sie Adobe Commerce auf Version 2.1.4 oder höher, bevor Sie fortfahren. Führen Sie dann einen [Einmaliges Upgrade zur Installation von ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für [2 002,0,9](../release-notes/cloud-release-archive.md#v200209) und späteren Versionen von 2002.0.x. |
| 2.1.15 - 2.1.16 | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für[2 002,0,9](../release-notes/cloud-release-archive.md#v200209) Und später. |
| 2.2.x und höher | [ECE-Tools aktualisieren](../dev-tools/update-package.md) Paket.<br>Siehe Versionshinweise für[2 002,0,8](../release-notes/cloud-release-archive.md#v200208) Und später. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Konfigurationsverwaltung

In älteren Versionen von Adobe Commerce, z. B. 2.1.4 oder höher bis 2.2.x oder höher, wurde ein `config.local.php` -Datei für die Konfigurationsverwaltung. Adobe Commerce Version 2.2.0 und höher verwendet die `config.php` -Datei, die genau wie die `config.local.php` -Datei, aber sie verfügt über verschiedene Konfigurationseinstellungen, die eine Liste Ihrer aktivierten Module und zusätzliche Konfigurationsoptionen enthalten.

Beim Upgrade von einer älteren Version müssen Sie Folgendes migrieren `config.local.php` Datei zur Verwendung der neueren `config.php` -Datei. Führen Sie die folgenden Schritte aus, um Ihre Konfigurationsdatei zu sichern und eine zu erstellen.

**So erstellen Sie ein temporäres `config.php` Datei**:

1. Kopie erstellen von `config.local.php` Datei und Benennen `config.php`.

1. Fügen Sie diese Datei zum hinzu `app/etc` Ordner Ihres Projekts.

1. Fügen Sie die Datei zu Ihrer Verzweigung hinzu und übertragen Sie sie.

1. Übertragen Sie die Datei in die Integrationsverzweigung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

>[!WARNING]
>
>Nach einem Upgrade können Sie die Datei `config.php` Datei erstellen und eine neue, vollständige Datei erstellen. Sie können diese Datei nur einmal löschen, um sie zu ersetzen. Nachdem ein neues erstellt wurde, schließen Sie `config.php` -Datei verwenden, können Sie die Datei nicht löschen, um eine neue Datei zu generieren. Siehe [Konfigurationsverwaltung und Pipeline-Bereitstellung](../store/store-settings.md).

### Überprüfen von Zend Framework Composer-Abhängigkeiten

Beim Upgrade auf **2.3.x oder höher ab 2.2.x**&#x200B;Überprüfen Sie, ob die Abhängigkeiten des Zend-Frameworks zur Datei hinzugefügt wurden. `autoload` Eigenschaft des `composer.json` -Datei, um Laminas zu unterstützen. Dieses Plug-in unterstützt neue Anforderungen für das Zend Framework, das zum Laminas-Projekt migriert wurde. Siehe [Migration von Zend Framework zum Laminas-Projekt](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) am _Magento DevBlog_.

**So überprüfen Sie die `auto-load:psr-4` Konfiguration**:

1. Wechseln Sie auf Ihrer lokalen Workstation in Ihr Projektverzeichnis.

1. Sehen Sie sich Ihre Integrationsverzweigung an.

1. Öffnen Sie `composer.json` -Datei in einem Texteditor speichern.

1. Überprüfen Sie die `autoload:psr-4` -Abschnitt für die Zend Plug-in Manager-Implementierung für Controller-Abhängigkeiten.

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

1. Wenn die Zend-Abhängigkeit fehlt, aktualisieren Sie `composer.json` Datei:

   - Fügen Sie die folgende Zeile zur hinzu. `autoload:psr-4` -Abschnitt.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Aktualisieren Sie die Projektabhängigkeiten.

     ```bash
     composer update
     ```

   - Code-Änderungen hinzufügen, übertragen und per Push übertragen.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Zusammenführen von Änderungen in der Staging-Umgebung und anschließend in der Produktion.

## Konfigurationsdateien

Vor dem Upgrade der Anwendung müssen Sie Ihre Projektkonfigurationsdateien aktualisieren, um Änderungen an den Standardkonfigurationseinstellungen für Adobe Commerce in der Cloud-Infrastruktur oder der Anwendung zu berücksichtigen. Die neuesten Standardeinstellungen finden Sie in der [Magento-Cloud-GitHub-Repository](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Überprüfen Sie immer die in der [.magento.app.yaml](../application/configure-app-yaml.md) -Datei für die installierte Version, da sie steuert, wie Ihr Programm die Cloud-Infrastruktur erstellt und bereitstellt. Das folgende Beispiel gilt für Version 2.4.7 und verwendet Composer 2.7.2. Die `build: flavor:` -Eigenschaft wird nicht für Composer 2.x verwendet; siehe [Installieren und Verwenden von Composer 2](../application/properties.md#installing-and-using-composer-2).

**So aktualisieren Sie `.magento.app.yaml` Datei**:

1. Wechseln Sie auf Ihrer lokalen Workstation in Ihr Projektverzeichnis.

1. Öffnen und bearbeiten Sie `magento.app.yaml` -Datei.

1. Aktualisieren Sie die PHP-Optionen.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Ändern Sie die `hooks` Eigenschaft `build` und `deploy` Befehle.

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

1. Speichern Sie die Datei. Übernehmen oder übertragen Sie noch keine Änderungen an die Remote-Umgebung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

### composer.json

Überprüfen Sie vor einem Upgrade immer, ob die Abhängigkeiten in der `composer.json` -Dateien sind mit der Adobe Commerce-Version kompatibel.

**So aktualisieren Sie `composer.json` -Datei für Adobe Commerce Version 2.4.4 und höher**:

1. Folgendes hinzufügen `allow-plugins` in die `config` Bereich:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Fügen Sie das folgende Plug-in zur hinzu. `require` Bereich:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Fügen Sie die folgende Komponente zur hinzu `extra:component_paths` Bereich:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Speichern Sie die Datei. Übernehmen oder übertragen Sie noch keine Änderungen an Ihre Verzweigung.

1. Fahren Sie mit dem Upgrade-Prozess fort.

## Projekt-Backup

Es wird empfohlen, vor einem Upgrade eine Sicherungskopie des Projekts zu erstellen. Führen Sie die folgenden Schritte aus, um Ihre Integrations-, Staging- und Produktionsumgebungen zu sichern.

**So sichern Sie die Datenbank und den Code Ihrer Integrationsumgebung**:

1. Erstellen Sie eine lokale Sicherung der Remote-Datenbank.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Die `magento-cloud db:dump` Der Befehl führt den aus [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) Befehl mit dem `--single-transaction` -Markierung, mit der Sie Ihre Datenbank sichern können, ohne die Tabellen zu sperren.

1. Sichern Sie Code und Medien.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Optional können Sie auslassen `[--media]` Wenn Sie über eine große Anzahl von statischen Dateien verfügen, die sich bereits in der Versionsverwaltung befinden.

**So sichern Sie die Datenbank der Staging- oder Produktionsumgebung vor der Bereitstellung**:

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

1. Erstellen eines [Datenbank-Dump](../storage/database-dump.md). Um einen Zielordner für den DB-Dump auszuwählen, verwenden Sie `--dump-directory` Option.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Der Dump-Vorgang erstellt eine `dump-<timestamp>.sql.gz` Archivieren Sie die Datei in Ihrem Remote-Projektverzeichnis. Siehe [Datenbank sichern](../storage/database-dump.md).

## Anwendungs-Upgrade

Überprüfen Sie die [Service-Versionen](../services/services-yaml.md#service-versions) Informationen zu den aktuellen Anforderungen an die Softwareversion, bevor Sie Ihr Programm aktualisieren.

**So aktualisieren Sie die Anwendungsversion**:

1. Wechseln Sie auf Ihrer lokalen Workstation in Ihr Projektverzeichnis.

1. Legen Sie die Upgrade-Version mithilfe der [Syntax der Versionsbeschränkung](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Sie müssen die Versionsbeschränkungssyntax verwenden, um erfolgreich zu aktualisieren `ece-tools` Paket. Die Versionsbeschränkung finden Sie in der Datei `composer.json` -Datei für die -Version [Anwendungsvorlage](https://github.com/magento/magento-cloud/blob/master/composer.json) Sie verwenden für das Upgrade.

1. Aktualisieren Sie das Projekt.

   ```bash
   composer update
   ```

1. Code-Änderungen hinzufügen, übertragen und per Push übertragen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` ist erforderlich, um alle geänderten Dateien zur Versionsverwaltung hinzuzufügen, da Composer Basispakete marshallt. Beide `composer install` und `composer update` Marshallen von Dateien aus dem Basispaket (`magento/magento2-base` und `magento/magento2-ee-base`) in den Paketstamm geschrieben.

   Die Dateien, die Composer marshallt, gehören zur neuen Version von Adobe Commerce, um die veraltete Version derselben Dateien zu überschreiben. Derzeit ist das Marshalling in Adobe Commerce deaktiviert, sodass Sie die marshallten Dateien zur Quell-Code-Verwaltung hinzufügen müssen.

1. Warten Sie, bis die Bereitstellung abgeschlossen ist.

1. Überprüfen Sie das Upgrade in Ihrer Integrations-, Staging- oder Produktionsumgebung, indem Sie sich mit SSH anmelden und die Version überprüfen.

   ```bash
   php bin/magento --version
   ```

### Erstellen einer Datei config.php

Wie in erwähnt [Konfigurationsverwaltung](#configuration-management)Nach dem Upgrade müssen Sie eine aktualisierte Datei erstellen. `config.php` -Datei. Schließen Sie alle zusätzlichen Konfigurationsänderungen über den Administrator in Ihrer Integrationsumgebung ab.

**So erstellen Sie eine systemspezifische Konfigurationsdatei**:

1. Verwenden Sie vom Terminal aus einen SSH-Befehl, um das `/app/etc/config.php` -Datei für die Umgebung.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   So führen Sie beispielsweise für Pro Folgendes aus: `scd-dump` am `integration` Verzweigung:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Übertragen Sie die `config.php` Datei auf den lokalen Workstations mithilfe von `rsync` oder `scp`. Sie können diese Datei nur lokal zur Verzweigung hinzufügen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Code-Änderungen hinzufügen, übertragen und per Push übertragen.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Dadurch wird eine aktualisierte generiert `/app/etc/config.php` Datei mit einer Modulliste und Konfigurationseinstellungen.

>[!WARNING]
>
>Für ein Upgrade löschen Sie `config.php` -Datei. Nachdem diese Datei zu Ihrem Code hinzugefügt wurde, sollten Sie **nicht** Löschen Sie sie. Wenn Sie Einstellungen entfernen oder bearbeiten müssen, bearbeiten Sie die Datei manuell.

### Erweiterungen aktualisieren

Überprüfen Sie Ihre Erweiterungs- und Modulseiten von Drittanbietern auf Marketplace oder anderen Unternehmens-Sites und überprüfen Sie die Unterstützung für Adobe Commerce und Adobe Commerce auf Cloud-Infrastrukturen. Wenn Sie Erweiterungen und Module von Drittanbietern aktualisieren müssen, empfiehlt Adobe, mit deaktivierten Erweiterungen in einer neuen Integrationsverzweigung zu arbeiten.

**So überprüfen und aktualisieren Sie Ihre Erweiterungen**:

1. Erstellen Sie eine Verzweigung auf Ihrer lokalen Workstation.

1. Deaktivieren Sie Ihre Erweiterungen nach Bedarf.

1. Laden Sie, sofern verfügbar, Erweiterungs-Upgrades herunter.

1. Installieren Sie das Upgrade, wie in der Dokumentation des Drittanbieters beschrieben.

1. Aktivieren und Testen der Erweiterung.

1. Fügen Sie die Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie auf die Fernbedienung.

1. Push-Benachrichtigung und Testen in Ihrer Integrationsumgebung.

1. Pushen Sie in die Staging-Umgebung, um sie in einer Vorproduktionsumgebung zu testen.

Adobe empfiehlt dringend, die Produktionsumgebung zu aktualisieren _Vorher_ Einschließen der aktualisierten Erweiterungen in Ihren Site-Launch-Prozess.

>[!NOTE]
>
>Wenn Sie die Anwendungsversion aktualisieren, wird der Upgrade-Prozess auf die neueste Version des Programms aktualisiert [Fastly CDN-Modul](../cdn/fastly.md#fastly-cdn-module-for-magento-2) Automatisch.

## Fehlerbehebung bei Upgrades

Wenn das Upgrade fehlgeschlagen ist, erhalten Sie eine Fehlermeldung im Browser, die Sie darauf hinweist, dass Sie nicht auf Ihre Storefront oder das Admin-Panel zugreifen können:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Beheben des Fehlers**:

1. Wechseln Sie auf Ihrer lokalen Workstation in Ihr Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Öffnen Sie `./app/var/report/<error number>` -Datei.

1. [Überprüfen der Protokolle](../test/log-locations.md) und ermitteln Sie die Ursache des Problems.

1. Code-Änderungen hinzufügen, übertragen und per Push übertragen.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
