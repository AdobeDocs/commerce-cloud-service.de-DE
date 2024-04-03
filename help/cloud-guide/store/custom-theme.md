---
title: Benutzerdefiniertes Design
description: Erfahren Sie, wie Sie ein benutzerdefiniertes Design mit Adobe Commerce in der Cloud-Infrastruktur installieren.
feature: Cloud, Themes
exl-id: f08134ab-daea-471d-a927-02531d36a809
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Benutzerdefiniertes Design

Sie können ein oder mehrere Designs installieren, um sie für einen oder alle Ihrer Stores und Sites in Ihrem Projekt zu verwenden. Designs umfassen mehrere statische Dateien, darunter Bilder, Schriftarten, CSS, JavaScript, PHP und mehr, um Ihre Geschäfte vollständig zu entwerfen. Sie können das Design hinzufügen, indem Sie entweder den Code in das Dateisystem extrahieren oder den Composer verwenden.

## Manuelles Installieren eines Designs

Um ein Design manuell zu installieren, muss sich der Code des Designs in einem komprimierten Archiv oder in einer Verzeichnisstruktur wie der folgenden befinden:

```text
<VendorName>
  ├── composer.json
      ├── etc
      │   └── view.xml
      ├── media
      ├── registration.php
      ├── theme.xml
      └── web
          ├── css
          │   └── source
          ├── fonts
          ├── images
          └── js
```

**Manuelles Installieren eines Designs**:

1. Kopieren Sie den Code des Designs unter `<Project root dir>/app/design/frontend` für ein Storefront-Design oder `<Project root dir>/app/design/adminhtml` für ein Admin-Design. Stellen Sie sicher, dass der Ordner der obersten Ebene `<VendorName>`; andernfalls wird das Design nicht ordnungsgemäß installiert.

   ```bash
   cp -r ExampleTheme <project-root>/app/design/frontend
   ```

1. Bestätigen Sie das Design, das an die richtige Stelle kopiert wurde.

   * Storefront-Design: `ls <project-root>/app/design/frontend`
   * Admin-Design: `ls <project-root>/app/design/adminhtml`

   Ein Beispiel:

   Beispiel-Design-Adobe Commerce

1. Fügen Sie Dateien hinzu und übertragen Sie sie.

   ```bash
   git add -A && git commit -m "Add theme"
   ```

1. Schicken Sie die Dateien an Ihren Zweig.

   ```bash
   git push origin <branch name>
   ```

1. Warten Sie, bis die Bereitstellung abgeschlossen ist.
1. Melden Sie sich beim Administrator an.
1. Klicks **Inhalt** > Design > **Designs**.

   Das Design wird im rechten Bereich angezeigt.

## Installieren eines Designs mithilfe von Composer

Die Installation eines Designs mit Composer entspricht der Installation jeder anderen Erweiterung mit Composer. Siehe [Module installieren, verwalten und aktualisieren](extensions.md) für Details.

So installieren Sie ein Design mit Composer:

1. Kaufen Sie das Design über Commerce Marketplace.
1. Rufen Sie den Namen des Designs Composer ab.
1. Wechseln Sie in den Stammordner von Adobe Commerce und geben Sie den Befehl ein:

   ```bash
   composer require <vendor>/<name>:<version>
   ```

   Beispiel:

   ```bash
   composer require zero1/theme-fashionista-theme:1.0.0
   ```

1. Warten Sie, bis die Abhängigkeiten aktualisiert wurden.
1. Geben Sie die folgenden Befehle ein:

   ```bash
   git add -A && git commit -m "Add theme"
   ```

   ```bash
   git push origin <branch name>
   ```

1. Melden Sie sich beim Administrator an.
1. Klicks **Inhalt** > Design > **Designs**.

   Das Design wird im rechten Bereich angezeigt.

## Mehrere Designs

Wenn Sie mehrere Designs verwenden, z. B. verschiedene Designs pro Gebietsschema, überprüfen Sie die `SCD_MATRIX` Umgebungsvariable zum Anpassen der Designbereitstellung. Siehe [build](../environment/variables-build.md#scd_matrix) oder [deploy](../environment/variables-deploy.md#scd_matrix) in den [Umgebungskonfiguration](../environment/configure-env-yaml.md).
