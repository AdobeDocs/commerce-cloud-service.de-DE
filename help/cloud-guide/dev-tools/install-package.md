---
title: Projekt auf ECE-Tools aktualisieren
description: Erfahren Sie, wie Sie Ihr Adobe Commerce on Cloud-Infrastrukturprojekt aktualisieren, um das ECE-Tools-Paket zu verwenden und die neuesten Fehlerbehebungen und Funktionen zu nutzen.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: bcdb59f0d2a17e55e8b0479ee69fac06c710638f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Upgrade des Projekts auf das ECE-Tools-Paket

Adobe veraltet `magento/magento-cloud-configuration` und `magento/ece-patches` Pakete zugunsten der `ece-tools` -Paket, das viele Cloud-Prozesse vereinfacht. Wenn Sie ein älteres Adobe Commerce in einem Cloud-Infrastrukturprojekt verwenden, das _nicht_ enthalten `ece-tools` -Paket, dann müssen Sie ein einmaliges, manuelles _Upgrade_ Verarbeiten Sie mit Ihrem Projekt.

>[!WARNING]
>
>Wenn das Projekt Folgendes enthält `ece-tools` das folgende Upgrade überspringen können. Um zu überprüfen, rufen Sie die ab. [!DNL Commerce] Version, die den `php vendor/bin/ece-tools -V` Befehl im lokalen Projektstammverzeichnis.

Für diesen Projekt-Upgrade-Prozess müssen Sie die `magento/magento-cloud-metapackage` Versionsbeschränkung in der `composer.json` -Datei im Stammverzeichnis speichern. Diese Einschränkung ermöglicht Aktualisierungen für Adobe Commerce in Cloud-Infrastruktur-Metapaketen, einschließlich der Entfernung veralteter Pakete, ohne die aktuelle Adobe Commerce-Version zu aktualisieren.

{{upgrade-tip}}

## Veraltete Pakete entfernen

Vor einem Upgrade zur Verwendung von `ece-tools` Paket, überprüfen Sie die `composer.lock` -Datei für die folgenden veralteten Pakete:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Metapaket aktualisieren

Jede Adobe Commerce-Version erfordert eine andere Einschränkung, die auf den folgenden Elementen basiert:

```terminal
>=current_version <next_version
```

- für `current_version`, geben Sie die zu installierende Adobe Commerce-Version an.
- für `next_version`, geben Sie die nächste Patch-Version nach dem in angegebenen Wert an `current_version`.

Wenn Sie Adobe Commerce installieren möchten `2.3.5-p2`, festlegen `current_version` bis `2.3.5` und die `next_version` bis `2.3.6`. Die Einschränkung `">=2.3.5 <2.3.6"` Installiert das neueste verfügbare Paket für 2.3.5.

Die neueste Metapaket-Einschränkung finden Sie immer im [`magento-cloud` Schablone](https://github.com/magento/magento-cloud/blob/master/composer.json).

Im folgenden Beispiel wird eine Einschränkung für das Adobe Commerce on Cloud Infrastructure-Metapaket auf eine beliebige Version festgelegt, die größer oder gleich der aktuellen Version 2.4.7 und kleiner als die nächste Version 2.4.8 ist:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Aktualisieren des Projekts

So aktualisieren Sie Ihr Projekt zur Verwendung von `ece-tools` -Paket aktualisieren, müssen Sie das Metapaket und das `.magento.app.yaml` Erweitern Sie die Eigenschaften und führen Sie eine Composer-Aktualisierung durch.

**So aktualisieren Sie das Projekt auf ECE-Tools**:

1. Aktualisieren von `magento/magento-cloud-metapackage` Versionsbeschränkung in der `composer.json` -Datei.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Aktualisieren Sie das Metapaket.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Ändern Sie die Hook-Befehle im `magento.app.yaml` -Datei.

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

1. Suchen Sie nach und entfernen Sie die [Veraltete Pakete](#remove-deprecated-packages). Die veralteten Pakete können ein erfolgreiches Upgrade verhindern.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Möglicherweise ist es erforderlich, das zu aktualisieren `ece-tools` Paket.

   ```bash
   composer update magento/ece-tools
   ```

1. Fügen Sie die Code-Änderungen hinzu und übertragen Sie sie. In diesem Beispiel wurden die folgenden Dateien aktualisiert:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Code-Änderungen auf den Remote-Server pushen und diese Verzweigung mit der `integration` Verzweigung.

   ```bash
   git push origin <branch-name>
   ```
