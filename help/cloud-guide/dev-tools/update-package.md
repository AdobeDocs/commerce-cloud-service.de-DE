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

Aktualisierung der `ece-tools` -Paket aktualisiert auch das andere [Cloud Tools Suite für Commerce-Pakete](../release-notes/cloud-tools-suite.md), die Abhängigkeiten für `ece-tools`. Daher müssen Sie eine Version von Adobe Commerce in der Cloud-Infrastruktur verwenden, die die `ece-tools` Paket.

{{ece-tools-package}}

**Voraussetzungen**:

- Vor der Aktualisierung `ece-tools`, überprüfen Sie die [Versionshinweise zur Cloud Tools Suite für Commerce](../release-notes/cloud-tools-suite.md).
- Wenn Sie von aktualisieren `ece-tools` 2002.0.22 oder früher bis 2002.1.0, Überprüfung [Abwärtskompatible Änderungen](../release-notes/backward-incompatible-changes.md) und nehmen Sie die erforderlichen Änderungen an Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur vor.
- Überprüfen [Upgrades und Patches](../development/commerce-version.md#upgrade-from-older-versions) um die ECE-Tools-Versionen zu ermitteln, die mit Ihrem Adobe Commerce on Cloud-Infrastrukturprojekt kompatibel sind.

{{upgrade-tip}}

**So aktualisieren Sie die `ece-tools` package**:

1. Führen Sie auf Ihrer lokalen Workstation eine Aktualisierung mit Composer durch.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Wenn Sie nicht weiter aktualisieren können `ece-tools` Version 2002.0.8, siehe [Upgrade des Projekts zur Verwendung des ECE-Tools-Pakets](install-package.md).

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
