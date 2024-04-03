---
title: B2B-Modul aktivieren
description: Erfahren Sie, wie Sie das Business-to-Business-Modul für Adobe Commerce in der Cloud-Infrastruktur aktivieren.
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# B2B-Modul aktivieren

Wenn Ihre Kunden Unternehmen sind, können Sie das B2B-Modul für Adobe Commerce installieren, um Ihr Adobe Commerce on Cloud Infrastructure Pro-Projekt zu erweitern und so ein Business-to-Business-Modell zu integrieren. Obwohl dieses Thema spezifische Informationen zur Installation und Konfiguration des B2B-Moduls für Adobe Commerce in der Cloud-Infrastruktur enthält, finden Sie weitere B2B-Informationen in den folgenden Handbüchern:

- [Adobe Commerce B2B-Entwicklerhandbuch](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Adobe Commerce B2B-Benutzerhandbuch](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Da B2B ein Modul für Adobe Commerce in der Cloud-Infrastruktur ist, empfiehlt Adobe, Ihre Adobe Commerce-Anwendung vor dem Beginn in einer Integrations- oder Staging-Umgebung bereitzustellen.

## B2B-Modul installieren

Adobe empfiehlt, in einer Entwicklungsverzweigung zu arbeiten, wenn Sie das B2B-Modul zu Ihrem Projekt hinzufügen. Wenn Sie keine Verzweigung haben, lesen Sie [Erstellen einer Verzweigung für die Entwicklung](../development/cli-branches.md#create-a-branch-for-development). Bei der Installation des B2B-Moduls muss die Variable `Magento_B2b` Der Modulname wird automatisch in die `app/etc/config.php` -Datei. Die Datei muss nicht direkt bearbeitet werden.

**Installieren des B2B-Moduls**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Erstellen oder checken Sie einen Entwicklungszweig aus.

1. Fügen Sie das B2B-Modul zum `require` Abschnitt `composer.json` -Datei.

   ```bash
   composer require magento/extension-b2b --no-update
   ```

1. Aktualisieren Sie die Projektabhängigkeiten.

   ```bash
   composer update
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Nachdem der Build und die Bereitstellung abgeschlossen sind, melden Sie sich mit SSH bei der Remote-Umgebung an und überprüfen Sie, ob das B2B-Modul installiert ist.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   Ein Erweiterungsname verwendet das folgende Format: `<VendorName>_<ComponentName>`.

   Beispielantwort:

   ```terminal
   Magento_B2b : Module is enabled
   ```

   Wenn Bereitstellungsfehler auftreten, lesen Sie [Wiederherstellen nach Komponentenfehler](../deploy/recover-failed-deployment.md).

## B2B-Modul aktivieren

Wenn Sie das B2B-Modul mithilfe von Composer installieren, wird das Modul durch den Bereitstellungsprozess automatisch aktiviert. Wenn Sie das B2B-Modul bereits installiert haben, können Sie das Modul mithilfe der CLI aktivieren oder deaktivieren

Aktivieren Sie das B2B-Modul:

```bash
bin/magento module:enable Magento_B2b
```

Beispielantwort:

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

Siehe [Erweiterungen verwalten](extensions.md).

## B2B-Modul konfigurieren

Nach der Installation des B2B-Moduls für Adobe Commerce müssen Sie [Starten der Nachricht für den Verbraucher](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) damit Sie die _Freigegebener Katalog_ -Modul, und Sie müssen [B2B-Funktionen aktivieren](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
