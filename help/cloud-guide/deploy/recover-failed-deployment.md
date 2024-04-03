---
title: Wiederherstellen nach Komponentenfehler
description: Erfahren Sie, wie Sie wiederherstellen können, wenn eine Komponente in Adobe Commerce in der Cloud-Infrastruktur nicht ordnungsgemäß bereitgestellt werden kann.
feature: Cloud, Deploy
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
source-git-commit: b44d97f82ef09288807c648010202422c9ac04eb
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Wiederherstellen nach Komponentenfehler

In diesem Thema wird beschrieben, wie Sie eine Wiederherstellung vornehmen können, wenn eine Komponente nicht ordnungsgemäß bereitgestellt werden kann. Typische Beispiele sind Komponenten mit Abhängigkeiten, die von Ihrer Remote-Umgebung nicht erfüllt werden, z. B. inkompatible PHP-Versionen.

Sie können eine fehlgeschlagene Bereitstellung auf eine der folgenden Arten wiederherstellen:

- [Wiederherstellen eines Backups](../storage/snapshots.md#restore-a-snapshot)
- Projekt und Code aus vorherigen Änderungen bereinigen und erneut bereitstellen

## Bereinigen, Entfernen und erneutes Bereitstellen

Um die vorherige Bereitstellung zu bereinigen, identifizieren Sie die Komponente, die hinzugefügt oder aktualisiert wurde, und entfernen Sie sie dann. Melden Sie sich zunächst bei der Remote-Umgebung an und löschen Sie manuell den Inhalt der `var` Verzeichnis. Entfernen Sie dann die Komponente aus dem `composer.json` und stellen Sie die Umgebung erneut bereit.

**So reinigen Sie die `var` Verzeichnisse**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Löschen Sie die `var` Verzeichnissen.

   ```shell
   rm -rf var/*
   ```

1. Melden Sie sich ab.

**So entfernen Sie die Komponente**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Löschen Sie den Cache.

   ```bash
   composer clear-cache
   ```

1. Entfernen Sie die Komponente aus der `composer.json` -Datei.

   ```bash
   composer remove <component-name>:<version>
   ```

   Wenn die folgende Meldung angezeigt wird, müssen Sie nichts weiter unternehmen:

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Warten Sie, bis die Abhängigkeiten aktualisiert wurden.

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Weitere Informationen zum Wiederherstellen einer Umgebung ohne Sicherung finden Sie unter [Wiederherstellen einer Umgebung](../development/restore-environment.md).

{{stuck-deployment-tip}}
