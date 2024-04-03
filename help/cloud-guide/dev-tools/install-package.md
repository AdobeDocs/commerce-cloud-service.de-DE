---
title: Upgrade des Projekts zur Verwendung der ECE-Tools
description: Erfahren Sie, wie Sie Ihr Adobe Commerce auf das Cloud-Infrastrukturprojekt aktualisieren, um das ECE-Tools-Paket zu verwenden und die neuesten Fehlerbehebungen und Funktionen zu nutzen.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Upgrade des Projekts zur Verwendung des ECE-Tools-Pakets

Adobe veraltet die `magento/magento-cloud-configuration` und `magento/ece-patches` Packages zugunsten der `ece-tools` -Paket, das viele Cloud-Prozesse vereinfacht. Wenn Sie ein älteres Adobe Commerce in einem Cloud-Infrastrukturprojekt verwenden, _not_ enthält `ece-tools` -Paket erstellen, müssen Sie eine einmalige, manuelle _Upgrade_ in Ihr Projekt verarbeiten.

>[!WARNING]
>
>Wenn Ihr Projekt `ece-tools` -Paket, können Sie das folgende Upgrade überspringen. Rufen Sie zur Überprüfung die [!DNL Commerce] -Version, die `php vendor/bin/ece-tools -V` in Ihrem lokalen Projektstammverzeichnis.

Für dieses Projekt-Upgrade-Verfahren müssen Sie die `magento/magento-cloud-metapackage` Versionsbegrenzung im `composer.json` Datei im Stammverzeichnis. Diese Einschränkung ermöglicht Aktualisierungen für Adobe Commerce für Cloud-Infrastruktur-Metapakete - einschließlich der Entfernung veralteter Pakete - ohne die aktuelle Adobe Commerce-Version zu aktualisieren.

{{upgrade-tip}}

## Entfernen veralteter Pakete

Vor der Aktualisierung zur Verwendung der `ece-tools` Paket, überprüfen Sie die `composer.lock` -Datei für die folgenden veralteten Pakete:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Metapaket aktualisieren

Für jede Adobe Commerce-Version sind unterschiedliche Einschränkungen erforderlich, die auf Folgendes basieren:

```terminal
>=current_version <next_version
```

- Für `current_version`, geben Sie die zu installierende Adobe Commerce-Version an.
- Für `next_version`, geben Sie die nächste Patch-Version nach dem Wert an, der unter `current_version`.

Wenn Sie Adobe Commerce installieren möchten `2.3.5-p2`, set `current_version` nach `2.3.5` und `next_version` nach `2.3.6`. Die Beschränkung `">=2.3.5 <2.3.6"` installiert das neueste verfügbare Paket für 2.3.5.

Sie finden die neueste Metapaket-Einschränkung immer in der [`magento-cloud` template](https://github.com/magento/magento-cloud/blob/master/composer.json).

Im folgenden Beispiel wird eine Beschränkung für das Adobe Commerce-Metapaket zur Cloud-Infrastruktur auf eine Version festgelegt, die größer oder gleich der aktuellen Version 2.4.5 und kleiner als die nächste Version 2.4.6 ist:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
},
```

## Projekt aktualisieren

Um Ihr Projekt zu aktualisieren, verwenden Sie `ece-tools` -Paket, müssen Sie das Metapaket und das `.magento.app.yaml` Hooks Eigenschaften herstellt und ein Composer-Update durchführt.

**So aktualisieren Sie das Projekt für die Verwendung von Eece-Tools**:

1. Aktualisieren Sie die `magento/magento-cloud-metapackage` Versionsbegrenzung im `composer.json` -Datei.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.5 <2.4.6" --no-update
   ```

1. Aktualisieren Sie das Metapaket.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Ändern Sie die Hook-Befehle in der `magento.app.yaml` -Datei.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Suchen Sie nach und entfernen Sie die [veraltete Pakete](#remove-deprecated-packages). Die veralteten Pakete können eine erfolgreiche Aktualisierung verhindern.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Es kann erforderlich sein, die `ece-tools` Paket.

   ```bash
   composer update magento/ece-tools
   ```

1. Fügen Sie die Codeänderungen hinzu und übertragen Sie sie. In diesem Beispiel wurden die folgenden Dateien aktualisiert:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Übertragen Sie Ihre Codeänderungen auf den Remote-Server und führen Sie diese Verzweigung mit der `integration` -Verzweigung.

   ```bash
   git push origin <branch-name>
   ```
