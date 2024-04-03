---
title: Erweiterungen verwalten
description: Erfahren Sie, wie Sie Erweiterungen in Adobe Commerce in der Cloud-Infrastruktur installieren und verwalten.
feature: Cloud, Extensions, Upgrade
exl-id: 9c6e98ca-85da-4342-8402-d576eb382ba2
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Erweiterungen verwalten

Sie können Ihre Adobe Commerce-Anwendungsfunktionen erweitern, indem Sie eine Erweiterung aus dem [Commerce Marketplace](https://marketplace.magento.com). Sie können beispielsweise ein Design hinzufügen, um das Erscheinungsbild Ihrer Storefront zu ändern, oder Sie können ein Sprachpaket hinzufügen, um Ihre Storefront und Ihren Administrator zu lokalisieren.

## Name des Komponisten einer Erweiterung

Obwohl dieser Abschnitt beschreibt, wie Sie den Composer-Namen und die Version einer Erweiterung von Commerce Marketplace abrufen können, können Sie den Namen und die Version von _any_ -Modul in der Composer-Datei des -Moduls. Öffnen Sie die `composer.json` in einem Texteditor speichern und die `"name"` und `"version"` -Werte.

**Abrufen des Komponentennamens eines Moduls vom Commerce Marketplace**:

1. Anmelden bei [Commerce Marketplace](https://marketplace.magento.com) mit dem Benutzernamen und dem Kennwort, die Sie zum Kauf der Komponente verwendet haben.

1. Klicken Sie oben rechts auf Ihren Benutzernamen und wählen Sie **Mein Profil**.

   ![Zugriff auf Ihr Marketplace-Konto](../../assets/marketplace/my-profile.png)

1. Im _Mein Konto_ Seite, klicken **Meine Käufe**.

   ![Kaufverlauf für Marketplace](../../assets/marketplace/my-purchases.png)

1. Im _Meine Käufe_ auf der Seite ein von Ihnen erworbenes Modul auswählen und auf **Technische Details**.

1. Klicks **Kopieren** , um die [!UICONTROL Component name] in die Zwischenablage.

1. Öffnen Sie einen Texteditor, fügen Sie den Komponentennamen ein und fügen Sie ein Doppelpunkt-Zeichen (`:`).

1. In **Technische Details** klicken **Kopieren** , um die [!UICONTROL Component version] in die Zwischenablage.

1. Hängen Sie im Texteditor die Versionsnummer an den Komponentennamen nach dem Doppelpunkt an. Beispiel:

   ```text
   extension-name/magento2:1.0.1
   ```

## Installieren einer Erweiterung

Adobe empfiehlt, in einer Entwicklungsverzweigung zu arbeiten, wenn Sie Ihrer Implementierung eine Erweiterung hinzufügen. Bei der Installation einer Erweiterung wird der Erweiterungsname (`<VendorName>_<ComponentName>`) wird automatisch in die [`app/etc/config.php`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html) -Datei. Die Datei muss nicht direkt bearbeitet werden.

**So installieren Sie eine Erweiterung**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Erstellen oder checken Sie einen Entwicklungszweig aus. Siehe [Verzweigung](../development/cli-branches.md).

1. Fügen Sie mithilfe des Composer-Namens und der Version die Erweiterung zum `require` Abschnitt `composer.json` -Datei.

   ```bash
   composer require <extension-name>:<version> --no-update
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
   git commit -m "Install <extension-name>"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!WARNING]
   >
   >Bei der Installation einer Erweiterung müssen Sie die `composer.lock` Datei, wenn Sie Code-Änderungen an die Remote-Umgebung senden. Die `composer install` -Befehl liest die `composer.lock` -Datei, um die definierten Abhängigkeiten in der Remote-Umgebung zu aktivieren.

1. Nachdem der Build und die Bereitstellung abgeschlossen sind, melden Sie sich mit einer SSH bei der Remote-Umgebung an und überprüfen Sie die installierte Erweiterung.

   ```bash
   bin/magento module:status <extension-name>
   ```

   Ein Erweiterungsname verwendet das folgende Format: `<VendorName>_<ComponentName>`.

   Beispielantwort:

   ```terminal
   Module is enabled
   ```

   Wenn Bereitstellungsfehler auftreten, lesen Sie [Fehler bei der Erweiterungsbereitstellung](../deploy/recover-failed-deployment.md).

## Erweiterungen verwalten

Wenn Sie eine Erweiterung mit Composer hinzufügen, aktiviert der Bereitstellungsprozess die Erweiterung automatisch. Wenn Sie die Erweiterung bereits installiert haben, können Sie sie über die CLI aktivieren oder deaktivieren. Verwenden Sie beim Verwalten von Erweiterungen das folgende Format: `<VendorName>_<ComponentName>`

Aktivieren oder deaktivieren Sie niemals eine Erweiterung, während Sie in den Remote-Umgebungen angemeldet sind.

**So aktivieren oder deaktivieren Sie eine Erweiterung**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Aktivieren oder deaktivieren Sie ein Modul. Die `module` -Befehl aktualisiert die `config.php` -Datei mit dem angeforderten Status des Moduls.

   >Aktivieren Sie ein Modul.

   ```bash
   bin/magento module:enable <module-name>
   ```

   >Deaktivieren Sie ein Modul.

   ```bash
   bin/magento module:disable <module-name>
   ```

1. Wenn Sie ein Modul aktiviert haben, verwenden Sie `ece-tools` , um die Konfiguration zu aktualisieren.

   ```bash
   ./vendor/bin/ece-tools module:refresh
   ```

1. Überprüfen Sie den Status eines Moduls.

   ```bash
   bin/magento module:status <module-name>
   ```

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Disable <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

## Aktualisierung einer Erweiterung

Bevor Sie fortfahren, benötigen Sie den Composer-Namen und die Version für die Erweiterung. Überprüfen Sie außerdem, ob die Erweiterung mit Ihrem Projekt und Ihrer Adobe Commerce-Version kompatibel ist. Insbesondere [die erforderliche PHP-Version überprüfen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) bevor Sie beginnen.

**So aktualisieren Sie eine Erweiterung**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Erstellen oder checken Sie einen Entwicklungszweig aus. Siehe [Verzweigung](../development/cli-branches.md).

1. Öffnen Sie die `composer.json` in einem Texteditor.

1. Suchen Sie Ihre Erweiterung und aktualisieren Sie die Version.

1. Speichern Sie Ihre Änderungen und beenden Sie den Texteditor.

1. Aktualisieren Sie die Projektabhängigkeiten.

   ```bash
   composer update
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

Wenn Fehler auftreten, lesen Sie [Wiederherstellen nach Komponentenfehler](../deploy/recover-failed-deployment.md). Weitere Informationen zur Verwendung von Erweiterungen mit Adobe Commerce finden Sie unter [Erweiterungen](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/extensions.html) im _Administratorhandbuch_.
