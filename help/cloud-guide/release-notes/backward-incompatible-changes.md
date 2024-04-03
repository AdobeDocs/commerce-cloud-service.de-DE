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

Abwärtskompatible Änderungen erfordern möglicherweise, dass Sie die Cloud-Konfiguration und -Prozesse für vorhandene Cloud-Projekte anpassen, wenn Sie auf die neueste Version des `ece-tools` oder anderen Cloud Tools Suite für Commerce-Pakete.

## Änderungen an `ece-tools` package

Einige Funktionen, die zuvor im `ece-tools` -Paket wird jetzt in separaten Paketen bereitgestellt. Diese Pakete sind Komponentenabhängigkeiten für `ece-tools`, die automatisch installiert und aktualisiert werden, wenn Sie die einzelnen Tools installieren oder aktualisieren.

Die neue Architektur sollte Ihre Installations- und Aktualisierungsprozesse nicht beeinträchtigen. Möglicherweise müssen Sie jedoch einige Befehlssyntax und Prozesse ändern, wenn Sie mit Ihrem Adobe Commerce-Projekt für Cloud-Infrastruktur arbeiten. Weitere Informationen finden Sie in den folgenden rückwärts inkompatiblen Änderungsinformationen und in der [Versionshinweise zur Cloud Tools Suite](cloud-tools-suite.md).

### Änderungen an den Anforderungen an Dienstversionen

Die Mindestanforderung für die PHP-Version wurde von 7.0.x auf 7.1.x für Cloud-Projekte, die `ece-tools` v2002.1.0 und höher. Wenn Ihre Umgebungskonfiguration PHP 7.0 angibt, aktualisieren Sie die [PHP-Konfiguration](../application/php-settings.md) im `.magento.app.yaml` -Datei.

>[!WARNING]
>
>Aufgrund der Änderung der PHP-Versionsvoraussetzungen, `ece-tools` 2002.1.0 unterstützt nur Adobe Commerce für Cloud-Infrastrukturprojekte mit Adobe Commerce 2.1.15 oder höher. Wenn Ihr Projekt eine frühere Version verwendet, müssen Sie [Upgrade](../development/commerce-version.md) vor der Aktualisierung auf `ece-tools` Juni 2002

### Änderungen der Umgebungskonfiguration

Die folgende Tabelle enthält Informationen zu Umgebungsvariablen und anderen Umgebungskonfigurationsdateien, die in entfernt oder veraltet wurden. `ece-tools` v2002.1.0.

| Posten | Ersatz |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` Variable | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` Variable | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` Variable | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` Variable | Keine. Jetzt erstellt der Build immer einen Symlink zum statischen Inhaltsverzeichnis. `pub/static`. |
| `build_options.ini` file | Verwenden Sie die [`.magento.env.yaml`](../application/configure-app-yaml.md) -Datei, um Umgebungsvariablen zu konfigurieren, um Build- und Bereitstellungsaktionen in allen Umgebungen zu verwalten.<p>Wenn Sie eine Cloud-Umgebung erstellen, die die `build_options.ini` -Datei, schlägt der Build fehl. |

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

In früheren ECE-Tools-Versionen konnten Sie die `m2-ece-build` und `m2-ece-deploy` Befehle zum Konfigurieren von Bereitstellungs-Hooks in der `.magento.app.yaml` -Datei. Wenn Sie auf Version 2002.1.0 aktualisieren, überprüfen Sie die `hooks` Konfiguration in der `.magento.app.yaml` -Datei für die veralteten Befehle verwenden und sie bei Bedarf ersetzen.

## Änderungen bei Cloud-Patches

- **Entfernen heruntergeladener Patches**-Die `magento/magento-cloud-patches` Paket-Bundles für alle Patches, die über das [Softwaredownloads](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) und wendet sie bei der Bereitstellung in der Cloud automatisch an. Um Patchkonflikte nach einem Upgrade auf ECE-Tools 2002.1.0 oder höher zu vermeiden, entfernen Sie alle von Adobe bereitgestellten Patches, die Sie manuell heruntergeladen und zu Ihrem Projekt hinzugefügt haben.

- **Aktualisieren des Befehls zum Anwenden von Patches**-Wir haben den Befehl zum Anwenden von Patches aus dem `vendor/bin/ece-tools` Verzeichnis in `vendor/bin/ece-patches` Verzeichnis. Wenn Sie diesen Befehl zum manuellen Anwenden von Patches verwenden, verwenden Sie den neuen Pfad.

  > Manuelles Anwenden von Patches

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Cloud Docker-Änderungen

- **Die PHP-Mindestversion ist jetzt PHP 7.1**-Wenn Ihr Cloud Docker für Commerce-Host eine frühere Version ausführt, aktualisieren Sie auf PHP v7.1 oder höher.

- **Cloud Docker für Commerce-Befehlsänderungen**-

   - **Aktualisieren von Cloud Docker für Commerce-Befehle für Docker-Build-Vorgänge**-Wir haben die Befehle Cloud Docker für Commerce aus der `vendor/bin/ece-tools` Verzeichnis in `vendor/bin/ece-docker` Verzeichnis. Aktualisieren Sie Ihre Skripte und Befehle, um den neuen Pfad zu verwenden.

     Nach der Aktualisierung auf `ece-tools` 2002.1.0, verwenden Sie den folgenden Befehl, um die verfügbaren Elemente anzuzeigen `ece-docker` Befehle.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Aktualisieren der Befehle &quot;docker-compse&quot;der Cloud**-Wir haben den Pfad zur Befehlsdatei von `./bin/docker` nach `./bin/magento-docker`. Aktualisieren Sie Ihre Skripte und Befehle, um den neuen Pfad zu verwenden.

   - **Cron-Container ist nicht mehr in der standardmäßigen Docker-Konfiguration enthalten**-Jetzt müssen Sie die `--with-cron` -Option `ece-docker build:compose` -Befehl, um den Cron-Container in die Konfiguration der Docker-Umgebung einzuschließen. Siehe [Verwalten von Cron-Aufträgen](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) im _Cloud Docker für Commerce_ Handbuch.

     Skripte, die zuvor Container mit Cron-Aufträgen generiert haben, enthalten jetzt keinen Cron-Container mehr.

   - **Verwenden temporärer Container**-In früheren Versionen wurden die von `bin/magento-docker` -Befehlsoperationen wurden nicht entfernt, sodass Sie sie für andere Vorgänge verwenden konnten. Nun, die `magento-docker` -Befehle entfernen alle Container, die sie nach Abschluss des Befehls erstellen.

     Wenn Sie einen Container beibehalten möchten, der von einem docker-compse-Vorgang erstellt wurde, verwenden Sie die `docker-compose run` -Befehl anstelle des `bin/magento-docker` Befehl.

   - **Ausführen von Hooks nach der Bereitstellung**-Die `cloud-deploy` -Befehl führt nach der Bereitstellung keine Hooks mehr aus. Verwenden Sie die neuen `cloud-post-deploy` -Befehl zum Ausführen von Hooks nach der Bereitstellung. Aktualisieren Sie Ihre Skripte, um den Befehl zum Ausführen von Hooks nach der Bereitstellung hinzuzufügen.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Wenn Sie `docker-compose` direkt Befehle ausführen, führen Sie die `docker-compose run deploy cloud-post-deploy` nach dem Befehl &quot;deploy&quot;zurück.

- **Datenbank aktualisieren**-Der Datenbank-Container wird jetzt im `magento-db` persistentes Docker-Volumen. Wenn Sie die Docker-Umgebung aktualisieren, wird die Datenbank nicht mehr automatisch gelöscht. Verwenden Sie bei Bedarf einen der folgenden Befehle, um ihn manuell zu entfernen.

   - Entfernen Sie die `magento-db` container:

     ```bash
     docker volume rm magento-db
     ```

   - Entfernen Sie beim Herunterfahren der Docker-Container alle zugehörigen Volumes:

     ```bash
     docker-compose down -v
     ```

- **Dateisynchronisierungseinstellungen für Archiv- und Sicherungsdateien überschreiben**-Archiv- und Backup-Dateien mit den folgenden Erweiterungen werden bei Verwendung von Docker-Sync oder Mutagen nicht mehr synchronisiert: SQL, GZ, ZIP und BZ2. Sie können die standardmäßige Dateisynchronisierung für diese Dateitypen außer Kraft setzen, indem Sie die Datei umbenennen und mit einer anderen Erweiterung enden. Beispiel: `synchronize-me.zip-backup`
