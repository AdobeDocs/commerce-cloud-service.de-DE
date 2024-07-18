---
title: Anwenden von Patches
description: Erfahren Sie, wie Sie Patches in Adobe Commerce auf das Cloud-Infrastrukturprojekt anwenden.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Anwenden von Patches

[Cloud-Patches für Commerce](https://github.com/magento/magento-cloud-patches) und das [Qualitätspatches-Tool](https://github.com/magento/quality-patches) stellen Patches für Ihre installierte Adobe Commerce-Anwendung bereit.

- Das Cloud Patches für Commerce-Paket stellt erforderliche Patches mit kritischen Fehlerbehebungen bereit
- Qualitätsmuster liefern optionale, mit geringen Auswirkungen versehene Qualitätsfixes wie [einzelne Patches](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch), die keine abwärtsinkompatiblen Änderungen enthalten

Unter [Verfügbare Patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) im _Handbuch für Commerce Operations Tools_ finden Sie eine vollständige Liste der veröffentlichten Patches.

Beide Pakete verbessern die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen und unterstützen die schnelle Bereitstellung wichtiger, optionaler und benutzerdefinierter Fehlerbehebungen. Sie können diese Pakete verwenden, um allgemeine Informationen über alle für Commerce verfügbaren Patches anzuwenden, wiederherzustellen und anzuzeigen.

>[!TIP]
>
>Sie können das Tool [Qualitätsmuster-Tool](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) und Cloud-Patches für Commerce als eigenständige Pakete für Magento Open Source- und Adobe Commerce-Projekte verwenden. Es wird empfohlen, das Werkzeug für Qualitätsmuster für Nicht-Cloud-Projekte zu verwenden.

Wenn Sie Änderungen an der Remote-Umgebung bereitstellen, verwendet das `ece-tools`-Paket `magento/magento-cloud-patches` und `magento/quality-patches`, um nach ausstehenden Patches zu suchen, und wendet sie automatisch in der folgenden Reihenfolge an:

1. Wenden Sie alle erforderlichen Commerce-Patches an, die im Cloud-Patches für Commerce -Paket enthalten sind.
1. Wenden Sie ausgewählte optionale Commerce-Patches an, die im Qualitätsmuster-Tool enthalten sind.
1. Wenden Sie benutzerdefinierte Patches im Verzeichnis `/m2-hotfixes` in alphabetischer Reihenfolge nach Patch-Name an.

>[!NOTE]
>
>Wenn Sie das Paket `ece-tools` oder das Paket &quot;Cloud Patches für Commerce&quot;aktualisieren, werden die neuesten erforderlichen Patches beim nächsten Bereitstellen des Projekts angewendet. Alternativ können Sie sie sofort mit dem Befehl `ece-patches apply` CLI bereitstellen und Ihre Cloud-Umgebung erneut bereitstellen. Sie können [erforderliche Patches](https://github.com/magento/magento-cloud-patches/tree/develop/patches) während des Bereitstellungsprozesses nicht überspringen.

## Voraussetzungen

{{upgrade-tip}}

Das Werkzeug für Qualitätsmuster ist eine Abhängigkeit von den Cloud-Patches für Commerce und dem Paket `ece-tools` . Um die neuesten Patches anwenden zu können, muss [die neueste Version der ECE-Tools](../dev-tools/update-package.md) installiert sein. Die erforderliche Mindestversion der ECE-Tools ist 2002.1.2.

## Verfügbare Patches und Status anzeigen

So zeigen Sie die Liste der verfügbaren einzelnen Patches an:

```bash
php ./vendor/bin/ece-patches status
```

Beispielantwort:

```
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

Die Statustabelle enthält die folgenden Arten von Informationen:

- **Typ**:
   - `Optional` - Alle Patches aus dem Quality Patches Tool und dem Cloud Patches-Paket sind für Adobe Commerce- und Magento Open Source-Installationen optional. Für Adobe Commerce in der Cloud-Infrastruktur sind alle Patches optional.
   - `Required` - Alle Patches aus dem Cloud Patches für Commerce-Package sind für Cloud-Kunden erforderlich.
   - `Deprecated` - Der einzelne Patch wird als veraltet markiert und wir empfehlen, ihn zurückzusetzen, wenn Sie ihn angewendet haben. Nachdem Sie einen veralteten Patch zurückgesetzt haben, wird er nicht mehr in der Statustabelle angezeigt.
   - `Custom`—Alle Patches aus dem Verzeichnis &quot;m2-hotfixes&quot;.

- **Status**:
   - `Applied`—Der Patch wurde angewendet.
   - `Not applied`—Der Patch wurde nicht angewendet.
   - `N/A`—Der Status des Patch kann aufgrund von Konflikten nicht definiert werden.

- **Details**:
   - `Affected components` - Die Liste der betroffenen Module.
   - `Required patches` - Die Liste erforderlicher Patches (Abhängigkeiten).
   - `Recommended replacement` - Der Patch, der als Ersatz für einen veralteten Patch empfohlen wird.

## Patch in einer lokalen Umgebung anwenden

Sie können Patches manuell in einer lokalen Umgebung anwenden und vor der Bereitstellung testen.

**So wenden Sie einzelne Patches in einer lokalen Entwicklungsumgebung an**:

1. Fügen Sie die Variable &quot;QUALITY_PATCH&quot;zur Datei `.magento.env.yaml` hinzu und listen Sie die erforderlichen Patches darunter auf.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. Wenden Sie die Patches aus dem Projektstamm an.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   Der Befehl `ece-patches apply` wendet Patches in der folgenden Reihenfolge an:
   - Erforderliche Patches
   - Optionale einzelne Patches
   - Benutzerdefinierte Patches aus dem Verzeichnis `/m2-hotfixes`

1. Löschen Sie den Cache.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Testen Sie die Patches und nehmen Sie die erforderlichen Änderungen an benutzerdefinierten Patches vor.

## Patch in einer Remote-Umgebung anwenden

>[!WARNING]
>
>Es wird dringend empfohlen, alle Patches in einer Integrations- oder Staging-Umgebung zu testen, bevor sie in die Produktionsumgebung bereitgestellt werden.

**So wenden Sie Patches in einer Remote-Umgebung an**:

1. Fügen Sie die Variable `QUALITY_PATCHES` zur Datei `.magento.env.yaml` hinzu und listen Sie die erforderlichen Patches darunter auf.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >Nach dem Upgrade auf eine neue Version von Adobe Commerce müssen Sie Patches erneut anwenden, wenn die Patches nicht in der neuen Version enthalten sind.

1. Fügen Sie die aktualisierte `.magento.env.yaml` -Datei hinzu, übertragen Sie sie und pushen Sie sie.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Anwenden eines benutzerdefinierten Patches

Bei der Bereitstellung wendet ECE-Tools alle Adobe-Patches und benutzerdefinierten Patches an, die Sie dem Ordner &quot;`/m2-hotfixes`&quot;im Projektstamm hinzufügen.

>[!NOTE]
>
>Alle Patch-Dateinamen müssen mit der Erweiterung `.patch` enden.

**So wenden Sie einen benutzerdefinierten Patch auf eine Cloud-Umgebung an und testen ihn**:

1. Erstellen Sie im Projektstamm einen Ordner mit dem Namen &quot;`m2-hotfixes`&quot;, falls dieser nicht vorhanden ist.

   ```bash
   mkdir m2-hotfixes
   ```

1. Kopieren Sie die Patch-Datei in das Verzeichnis `/m2-hotfixes` .

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Testen Sie alle Patches in einer Produktionsumgebung vor der Produktion. Für Adobe Commerce in der Cloud-Infrastruktur können Sie mit dem CLI-Befehl `magento-cloud environment:branch <branch-name>` Zweige erstellen.

## Benutzerdefinierten Patch zurücksetzen

So stellen Sie einen zuvor angewendeten benutzerspezifischen Patch wieder her oder deinstallieren ihn:

1. Löschen Sie die Patch-Datei aus dem Verzeichnis &quot;`/m2-hotfixes`&quot;.

1. Hinzufügen, Übertragen und Push-Code-Änderungen.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Stellen Sie sicher, dass Sie in einer Produktionsumgebung testen. Für Adobe Commerce in der Cloud-Infrastruktur können Sie mit dem CLI-Befehl `magento-cloud environment:branch <branch-name>` Zweige erstellen.

## Anwenden von Patches auf ein Nicht-Cloud-Projekt

Verwenden Sie das [Qualitätsmuster-Tool](https://github.com/magento/quality-patches) für Magento Open Source- und Adobe Commerce-Projekte.

## Patch in einer lokalen Umgebung wiederherstellen

Sie können alle zuvor angewendeten Patches in einer lokalen Entwicklungsumgebung mithilfe der `ece-patches`-CLI zurücksetzen.

So stellen Sie alle angewendeten Patches wieder her:

```bash
php ./vendor/bin/ece-patches revert
```

Mit diesem Befehl werden alle Patches in der folgenden Reihenfolge zurückgesetzt:

- Stellt alle angewendeten benutzerdefinierten Patches aus dem Verzeichnis /m2-hotfixes wieder her.
- Gibt alle angewendeten optionalen individuellen Patches zurück.
- Gibt alle angewendeten erforderlichen Patches zurück.

## Protokollierung

Das Tool &quot;Qualitätsmuster&quot;protokolliert alle Vorgänge in der Datei &quot;`<Project_root>/var/log/patch.log`&quot;.
