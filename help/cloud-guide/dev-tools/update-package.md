---
title: ECE-Tools-Paket aktualisieren
description: Erfahren Sie, wie Sie das ECE-Tools-Paket aktualisieren, um die neuesten Fehlerbehebungen und Funktionen zu nutzen, die auf Adobe Commerce in der Cloud-Infrastruktur angewendet werden.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# ECE-Tools-Paket aktualisieren

Durch ein Update des `ece-tools`-Pakets werden auch die anderen [Cloud Tools Suite für Commerce-Pakete](../release-notes/cloud-tools-suite.md) aktualisiert, die von `ece-tools` abhängig sind. Daher müssen Sie eine Version von Adobe Commerce in der Cloud-Infrastruktur verwenden, die das `ece-tools` -Paket unterstützt.

{{ece-tools-package}}

**Voraussetzungen**:

- Bevor Sie `ece-tools` aktualisieren, lesen Sie die Versionshinweise zur [Cloud Tools Suite für Commerce](../release-notes/cloud-tools-suite.md) durch.
- Wenn Sie von `ece-tools` 2002.0.22 oder früher auf 2002.1.0 aktualisieren, überprüfen Sie die [Abwärtskompatiblen Änderungen](../release-notes/backward-incompatible-changes.md) und nehmen Sie die erforderlichen Änderungen an Ihrem Adobe Commerce-Projekt für die Cloud-Infrastruktur vor.
- Überprüfen Sie [Upgrades und Patches](../development/commerce-version.md#upgrade-from-older-versions) , um die ECE-Tools-Versionen zu ermitteln, die mit Ihrem Adobe Commerce on Cloud-Infrastrukturprojekt kompatibel sind.

{{upgrade-tip}}

**Aktualisieren des `ece-tools` -Pakets**:

1. Führen Sie auf Ihrer lokalen Workstation eine Aktualisierung mit Composer durch.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Wenn Sie nicht über die `ece-tools` -Version 2002.0.8 hinaus aktualisieren können, finden Sie weitere Informationen unter [Projekt aktualisieren, um das ECE-Tools-Paket zu verwenden](install-package.md).

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Führen Sie nach der Testvalidierung diese Verzweigung mit der Integrationsverzweigung zusammen.
