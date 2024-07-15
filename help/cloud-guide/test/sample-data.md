---
title: Beispieldaten
description: Erfahren Sie, wie Sie Beispieldaten mit Adobe Commerce in der Cloud-Infrastruktur installieren.
exl-id: 517e549f-15ba-47b3-9236-a1c4d24c917d
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Beispieldaten

Wenn Sie bei der Entwicklung Ihres Stores Beispieldaten benötigen, können Sie Beispieldaten installieren. Diese Daten simulieren einen aktiven Adobe Commerce-Store mit Kunden, Produkten und anderen Daten. Diese Beispieldaten funktionieren am besten mit einer neuen Adobe Commerce für die Installation von Cloud-Infrastrukturvorlagen.

Installieren Sie als Best Practice Beispieldaten in Entwicklungs- und Integrationsumgebungen. Wenn Sie Beispieldaten in der Staging- oder Produktionsumgebung verwenden, müssen Sie die Informationen und Produkte vor der Live-Schaltung [entfernen](#reset-or-uninstall-sample-data).

## Beispieldaten installieren

So installieren Sie Beispieldaten:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Geben Sie im Stammverzeichnis den folgenden Befehl ein, um Beispieldaten hinzuzufügen:

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Warten Sie, bis die Komponenten aktualisiert wurden.

1. Übernehmen Sie die Änderungen und übertragen Sie sie:

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Warten Sie, bis das Projekt bereitgestellt wurde.

1. Vergewissern Sie sich, dass die Installation erfolgreich war, indem Sie in der Integrationsumgebung zu Ihrer Storefront-Seite navigieren. Sie können den URL-Link zur Storefront über die [!DNL Cloud Console] finden.

1. Erstellen Sie eine Momentaufnahme Ihrer Umgebung:

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

Sie können Ihre Entwicklung mit Live-Daten testen!

## Beispieldaten zurücksetzen oder deinstallieren

Sie können Beispieldaten nach demselben Verfahren, das zum Installieren der Beispieldaten verwendet wird, zurücksetzen oder entfernen:

- Beispieldaten löschen: `./bin/magento sampledata:remove`
- Beispieldaten zurücksetzen: `./bin/magento sampledata:reset`
