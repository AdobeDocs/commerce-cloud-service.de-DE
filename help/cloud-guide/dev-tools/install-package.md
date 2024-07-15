---
title: Upgrade des Projekts zur Verwendung der ECE-Tools
description: Erfahren Sie, wie Sie Ihr Adobe Commerce auf das Cloud-Infrastrukturprojekt aktualisieren, um das ECE-Tools-Paket zu verwenden und die neuesten Fehlerbehebungen und Funktionen zu nutzen.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: bcdb59f0d2a17e55e8b0479ee69fac06c710638f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Upgrade des Projekts zur Verwendung des ECE-Tools-Pakets

Adobe veraltete die Pakete `magento/magento-cloud-configuration` und `magento/ece-patches` zugunsten des Pakets `ece-tools` , wodurch viele Cloud-Prozesse vereinfacht werden. Wenn Sie ein älteres Adobe Commerce in einem Cloud-Infrastrukturprojekt verwenden, das _nicht_ das Paket `ece-tools` enthält, müssen Sie einen einmaligen, manuellen _Upgrade_ -Prozess für Ihr Projekt durchführen.

>[!WARNING]
>
>Wenn Ihr Projekt das Paket `ece-tools` enthält, können Sie das folgende Upgrade überspringen. Rufen Sie zur Überprüfung die Version [!DNL Commerce] mit dem Befehl `php vendor/bin/ece-tools -V` im Stammverzeichnis Ihres lokalen Projekts ab.

Für dieses Projekt-Upgrade-Verfahren müssen Sie die `magento/magento-cloud-metapackage`-Versionsbegrenzung in der Datei `composer.json` im Stammverzeichnis aktualisieren. Diese Einschränkung ermöglicht Aktualisierungen für Adobe Commerce für Cloud-Infrastruktur-Metapakete - einschließlich der Entfernung veralteter Pakete - ohne die aktuelle Adobe Commerce-Version zu aktualisieren.

{{upgrade-tip}}

## Entfernen veralteter Pakete

Überprüfen Sie vor dem Ausführen eines Upgrades zur Verwendung des `ece-tools`-Pakets die Datei `composer.lock` auf die folgenden veralteten Pakete:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Metapaket aktualisieren

Für jede Adobe Commerce-Version sind unterschiedliche Einschränkungen erforderlich, die auf Folgendes basieren:

```terminal
>=current_version <next_version
```

- Geben Sie für &quot;`current_version`&quot;die zu installierende Adobe Commerce-Version an.
- Geben Sie für `next_version` die nächste Patch-Version nach dem in `current_version` angegebenen Wert an.

Wenn Sie Adobe Commerce `2.3.5-p2` installieren möchten, setzen Sie `current_version` auf `2.3.5` und die `next_version` auf `2.3.6`. Durch die Beschränkung `">=2.3.5 <2.3.6"` wird das neueste verfügbare Paket für 2.3.5 installiert.

Sie können die neueste Metapaket-Einschränkung immer in der [`magento-cloud` Vorlage](https://github.com/magento/magento-cloud/blob/master/composer.json) finden.

Im folgenden Beispiel wird eine Beschränkung für das Adobe Commerce-Metapaket zur Cloud-Infrastruktur auf eine Version festgelegt, die größer oder gleich der aktuellen Version 2.4.7 und kleiner als die nächste Version 2.4.8 ist:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Projekt aktualisieren

Um Ihr Projekt für die Verwendung des `ece-tools`-Pakets zu aktualisieren, müssen Sie das Metapaket und die `.magento.app.yaml` -Hooks-Eigenschaften aktualisieren und eine Composer-Aktualisierung durchführen.

**Aktualisieren des Projekts für die Verwendung von ece-tools**:

1. Aktualisieren Sie die `magento/magento-cloud-metapackage`-Versionsbegrenzung in der Datei `composer.json` .

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Aktualisieren Sie das Metapaket.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Ändern Sie die Hook-Befehle in der Datei &quot;`magento.app.yaml`&quot;.

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

1. Suchen und entfernen Sie die [veralteten Pakete](#remove-deprecated-packages). Die veralteten Pakete können eine erfolgreiche Aktualisierung verhindern.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Es kann erforderlich sein, das `ece-tools` -Paket zu aktualisieren.

   ```bash
   composer update magento/ece-tools
   ```

1. Fügen Sie die Codeänderungen hinzu und übertragen Sie sie. In diesem Beispiel wurden die folgenden Dateien aktualisiert:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Übertragen Sie Ihre Codeänderungen auf den Remote-Server und führen Sie diese Verzweigung mit der Verzweigung `integration` zusammen.

   ```bash
   git push origin <branch-name>
   ```
