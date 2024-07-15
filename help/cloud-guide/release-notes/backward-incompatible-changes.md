---
title: Abwärtskompatible Änderungen
description: Erfahren Sie mehr über die Abwärtskompatibilität bei der Aktualisierung vorhandener Cloud-Projekte.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Abwärtskompatible Änderungen

Abwärtskompatible Änderungen erfordern möglicherweise, dass Sie die Cloud-Konfiguration und -Prozesse für vorhandene Cloud-Projekte anpassen, wenn Sie ein Upgrade auf die neueste Version des `ece-tools`-Pakets oder andere Cloud Tools Suite für Commerce-Pakete durchführen.

## Änderungen am `ece-tools` -Paket

Einige Funktionen, die zuvor im `ece-tools` -Paket enthalten waren, werden jetzt in separaten Paketen bereitgestellt. Diese Pakete sind Composer-Abhängigkeiten für `ece-tools`, die automatisch installiert und aktualisiert werden, wenn Sie ece-Tools installieren oder aktualisieren.

Die neue Architektur sollte Ihre Installations- und Aktualisierungsprozesse nicht beeinträchtigen. Möglicherweise müssen Sie jedoch einige Befehlssyntax und Prozesse ändern, wenn Sie mit Ihrem Adobe Commerce-Projekt für Cloud-Infrastruktur arbeiten. Weitere Informationen finden Sie in den folgenden rückwärts inkompatiblen Änderungsinformationen und den Versionshinweisen zur Cloud Tools Suite](cloud-tools-suite.md).[

### Änderungen an den Anforderungen an Dienstversionen

Für Cloud-Projekte, die `ece-tools` v2002.1.0 und höher verwenden, wurde die Mindestanforderung für die PHP-Version von 7.0.x auf 7.1.x geändert. Wenn Ihre Umgebungskonfiguration PHP 7.0 angibt, aktualisieren Sie die [php configuration](../application/php-settings.md) in der `.magento.app.yaml` -Datei.

>[!WARNING]
>
>Aufgrund der Änderung der PHP-Versionsvoraussetzungen unterstützt `ece-tools` 2002.1.0 nur Adobe Commerce für Cloud-Infrastrukturprojekte mit Adobe Commerce 2.1.15 oder höher. Wenn Ihr Projekt eine frühere Version verwendet, müssen Sie [upgrade](../development/commerce-version.md) durchführen, bevor Sie auf `ece-tools` 2002.1.0 aktualisieren.

### Änderungen der Umgebungskonfiguration

Die folgende Tabelle enthält Informationen zu Umgebungsvariablen und anderen Umgebungskonfigurationsdateien, die in `ece-tools` v2002.1.0 entfernt oder veraltet wurden.

| Posten | Ersatz |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` Variable | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` Variable | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` Variable | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` Variable | Keine. Jetzt erstellt der Build immer einen Symlink zum statischen Inhaltsverzeichnis `pub/static`. |
| Datei `build_options.ini` | Verwenden Sie die Datei &quot;[`.magento.env.yaml`](../application/configure-app-yaml.md)&quot;, um Umgebungsvariablen zu konfigurieren, um Build- und Bereitstellungsaktionen in allen Ihren Umgebungen zu verwalten.<p>Wenn Sie eine Cloud-Umgebung erstellen, die die Datei `build_options.ini` enthält, schlägt der Build fehl. |

### CLI-Befehlsänderungen

In der folgenden Tabelle sind die Änderungen an CLI-Befehlen in ECE-Tools v2002.1.0 zusammengefasst, bei denen Sie möglicherweise Befehle oder Skripte aktualisieren müssen.

| Befehl | Ersatz |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

In früheren ECE-Tools-Versionen konnten Sie die Befehle `m2-ece-build` und `m2-ece-deploy` verwenden, um Bereitstellungs-Hooks in der Datei `.magento.app.yaml` zu konfigurieren. Wenn Sie auf Version 2002.1.0 aktualisieren, überprüfen Sie die `hooks` -Konfiguration in der Datei `.magento.app.yaml` auf die veralteten Befehle und ersetzen Sie sie bei Bedarf.

## Änderungen bei Cloud-Patches

- **Entfernen Sie heruntergeladene Patches** - Das `magento/magento-cloud-patches` -Paket bündelt alle Patches, die auf der Seite [Software-Downloads](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) verfügbar sind, und wendet sie automatisch an, wenn Sie sie in der Cloud bereitstellen. Um Patchkonflikte nach einem Upgrade auf ECE-Tools 2002.1.0 oder höher zu vermeiden, entfernen Sie alle von Adobe bereitgestellten Patches, die Sie manuell heruntergeladen und zu Ihrem Projekt hinzugefügt haben.

- **Aktualisieren des Befehls zum Anwenden von Patches** - Wir haben den Befehl zum Anwenden von Patches aus dem Verzeichnis `vendor/bin/ece-tools` in das Verzeichnis `vendor/bin/ece-patches` verschoben. Wenn Sie diesen Befehl zum manuellen Anwenden von Patches verwenden, verwenden Sie den neuen Pfad.

  > Manuelles Anwenden von Patches

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Cloud Docker-Änderungen

- **Die Mindestanforderung für die PHP-Version ist jetzt PHP 7.1** - Wenn Ihr Cloud Docker für Commerce-Host eine frühere Version ausführt, aktualisieren Sie auf PHP v7.1 oder höher.

- **Cloud Docker für Commerce - Befehlsänderungen**-

   - **Aktualisieren von Cloud Docker für Commerce-Befehle für Docker-Build-Vorgänge** - Wir haben den Cloud Docker für Commerce-Befehle aus dem Ordner `vendor/bin/ece-tools` in den Ordner `vendor/bin/ece-docker` verschoben. Aktualisieren Sie Ihre Skripte und Befehle, um den neuen Pfad zu verwenden.

     Verwenden Sie nach dem Upgrade auf `ece-tools` 2002.1.0 den folgenden Befehl, um verfügbare `ece-docker`-Befehle anzuzeigen.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Aktualisieren der Cloud-docker-compse-Befehle** - Wir haben den Pfad zur Befehlsdatei von `./bin/docker` in `./bin/magento-docker` umbenannt. Aktualisieren Sie Ihre Skripte und Befehle, um den neuen Pfad zu verwenden.

   - **Cron-Container, der nicht mehr in der standardmäßigen Docker-Konfiguration enthalten ist**-Jetzt müssen Sie die Option `--with-cron` zum Befehl `ece-docker build:compose` hinzufügen, um den Cron-Container in die Konfiguration der Docker-Umgebung einzuschließen. Siehe [Verwalten von Cron-Aufträgen](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) im Handbuch _Cloud Docker für Commerce_ .

     Skripte, die zuvor Container mit Cron-Aufträgen generiert haben, enthalten jetzt keinen Cron-Container mehr.

   - **Verwenden temporärer Container**-In früheren Versionen wurden die von `bin/magento-docker` -Befehlsvorgängen erstellten Container nicht entfernt, sodass Sie sie für andere Vorgänge verwenden konnten. Jetzt entfernen die `magento-docker`-Befehle alle Container, die sie nach Abschluss des Befehls erstellen.

     Wenn Sie einen Container beibehalten möchten, der durch einen Docker-Composer-Vorgang erstellt wurde, verwenden Sie den Befehl `docker-compose run` anstelle des Befehls `bin/magento-docker` .

   - **Beim Ausführen von Hooks nach der Bereitstellung** - Der Befehl `cloud-deploy` führt keine Hooks nach der Bereitstellung mehr aus. Verwenden Sie den neuen Befehl `cloud-post-deploy` , um nach der Bereitstellung Hooks auszuführen. Aktualisieren Sie Ihre Skripte, um den Befehl zum Ausführen von Hooks nach der Bereitstellung hinzuzufügen.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Wenn Sie die Befehle `docker-compose` direkt verwenden, führen Sie alternativ den Befehl `docker-compose run deploy cloud-post-deploy` nach dem Bereitstellungsbefehl aus.

- **Aktualisieren der Datenbank** - Der Datenbank-Container wird jetzt im beständigen Docker-Volume `magento-db` gespeichert. Wenn Sie die Docker-Umgebung aktualisieren, wird die Datenbank nicht mehr automatisch gelöscht. Verwenden Sie bei Bedarf einen der folgenden Befehle, um ihn manuell zu entfernen.

   - Entfernen Sie den `magento-db` -Container:

     ```bash
     docker volume rm magento-db
     ```

   - Entfernen Sie beim Herunterfahren der Docker-Container alle zugehörigen Volumes:

     ```bash
     docker-compose down -v
     ```

- **Dateisynchronisierungseinstellungen für Archiv- und Sicherungsdateien überschreiben**-Archiv- und Sicherungsdateien mit den folgenden Erweiterungen werden bei Verwendung von Docker-Sync oder Mutagen nicht mehr synchronisiert: SQL, GZ, ZIP und BZ2. Sie können die standardmäßige Dateisynchronisierung für diese Dateitypen außer Kraft setzen, indem Sie die Datei umbenennen und mit einer anderen Erweiterung enden. Beispiel: `synchronize-me.zip-backup`
