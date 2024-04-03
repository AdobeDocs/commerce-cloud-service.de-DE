---
title: Anwenden von Patches
description: Erfahren Sie, wie Sie Patches in Adobe Commerce auf das Cloud-Infrastrukturprojekt anwenden.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: e67d3259b1b5195147e4e441fe9efd82e48241ab
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Anwenden von Patches

[Cloud-Patches für Commerce](https://github.com/magento/magento-cloud-patches) und [Werkzeug für Qualitätsmuster](https://github.com/magento/quality-patches) Bereitstellen von Patches für Ihre installierte Adobe Commerce-Anwendung.

- Das Cloud Patches für Commerce-Pakete stellt erforderliche Patches mit kritischen Fehlerbehebungen bereit
- Qualitätsmuster liefern optionale, wirkungsarme Korrekturen wie [Einzelpatches](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) die keine abwärtskompatiblen Änderungen enthalten

Siehe [Verfügbare Patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) im _Handbuch für Commerce-Betriebstools_ , um eine vollständige Liste der veröffentlichten Patches zu überprüfen.

Beide Pakete verbessern die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen und unterstützen die schnelle Bereitstellung wichtiger, optionaler und benutzerdefinierter Fehlerbehebungen. Sie können diese Pakete verwenden, um allgemeine Informationen zu allen einzelnen Patches, die für den Handel verfügbar sind, anzuwenden, wiederherzustellen und anzuzeigen.

>[!TIP]
>
>Sie können die [Werkzeug für Qualitätsmuster](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) und Cloud Patches für Commerce als eigenständige Packages für Magento Open Source- und Adobe Commerce-Projekte. Es wird empfohlen, das Werkzeug für Qualitätsmuster für Nicht-Cloud-Projekte zu verwenden.

Wenn Sie Änderungen an der Remote-Umgebung bereitstellen, wird die `ece-tools` -Paket verwendet `magento/magento-cloud-patches` und `magento/quality-patches` , um nach ausstehenden Patches zu suchen und diese automatisch in der folgenden Reihenfolge anzuwenden:

1. Wenden Sie alle erforderlichen Commerce-Patches an, die im Cloud Patches for Commerce-Paket enthalten sind.
1. Wenden Sie ausgewählte optionale Commerce-Patches an, die im Qualitätsmuster-Tool enthalten sind.
1. Anwenden benutzerdefinierter Patches in der `/m2-hotfixes` Verzeichnis in alphabetischer Reihenfolge nach Patch-Name.

>[!NOTE]
>
>Wenn Sie die `ece-tools` oder dem Paket Cloud Patches für Commerce , werden bei der nächsten Bereitstellung Ihres Projekts die neuesten erforderlichen Patches angewendet oder Sie können sie sofort mit der `ece-patches apply` CLI-Befehl und erneute Bereitstellung Ihrer Cloud-Umgebung. Sie können nicht überspringen [erforderliche Patches](https://github.com/magento/magento-cloud-patches/tree/develop/patches) während des Bereitstellungsprozesses.

## Voraussetzungen

{{upgrade-tip}}

Das Tool für Qualitätsmuster ist eine Abhängigkeit von den Cloud-Patches für Commerce und der `ece-tools` Paket. Um die neuesten Patches anwenden zu können, müssen Sie [die neueste Version der ECE-Tools](../dev-tools/update-package.md) installiert. Die erforderliche Mindestversion der ECE-Tools ist 2002.1.2.

## Verfügbare Patches und Status anzeigen

So zeigen Sie die Liste der verfügbaren einzelnen Patches an:

```bash
php ./vendor/bin/ece-patches status
```

Beispielantwort:

```terminal
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
   - `Optional`—Alle Patches des Tools für Qualitätsmuster und des Cloud-Patches-Pakets sind für Installationen von Adobe Commerce und Magento Open Source optional. Für Adobe Commerce in der Cloud-Infrastruktur sind alle Patches optional.
   - `Required`—Alle Patches aus dem Cloud Patches für Commerce-Paket sind für Cloud-Kunden erforderlich.
   - `Deprecated`—Der einzelne Patch wird als veraltet markiert und wir empfehlen, ihn zurückzusetzen, wenn Sie ihn angewendet haben. Nachdem Sie einen veralteten Patch zurückgesetzt haben, wird er nicht mehr in der Statustabelle angezeigt.
   - `Custom`—Alle Patches aus dem Verzeichnis &quot;m2-hotfixes&quot;.

- **Status**:
   - `Applied`—Der Patch wurde angewendet.
   - `Not applied`—Der Patch wurde nicht angewendet.
   - `N/A`—Der Status des Patches kann aufgrund von Konflikten nicht definiert werden.

- **Details**:
   - `Affected components`—Die Liste der betroffenen Module.
   - `Required patches`—Die Liste der erforderlichen Patches (Abhängigkeiten).
   - `Recommended replacement`—Der Patch, der ein empfohlener Ersatz für einen veralteten Patch ist.

## Patch in einer lokalen Umgebung anwenden

Sie können Patches manuell in einer lokalen Umgebung anwenden und vor der Bereitstellung testen.

**So wenden Sie einzelne Patches in einer lokalen Entwicklungsumgebung an**:

1. Fügen Sie die Variable &quot;QUALITY_PATCH&quot;zum `.magento.env.yaml` und führen Sie die erforderlichen Patches darunter auf.

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

   Die `ece-patches apply` -Befehl wendet Patches in der folgenden Reihenfolge an:
   - Erforderliche Patches
   - Optionale einzelne Patches
   - Benutzerdefinierte Patches aus dem `/m2-hotfixes` directory

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

1. Fügen Sie die `QUALITY_PATCHES` in die `.magento.env.yaml` und führen Sie die erforderlichen Patches darunter auf.

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

1. Hinzufügen, Übergeben und Pushen der aktualisierten `.magento.env.yaml` -Datei.

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

Bei der Bereitstellung wendet ECE-Tools alle Adobe-Patches und alle benutzerdefinierten Patches an, die Sie zum `/m2-hotfixes` im Projektstamm.

>[!NOTE]
>
>Alle Patch-Dateinamen müssen mit dem `.patch` -Erweiterung.

**So wenden Sie einen benutzerdefinierten Patch auf eine Cloud-Umgebung an und testen ihn**:

1. Erstellen Sie im Projektstamm einen Ordner mit dem Namen `m2-hotfixes` , wenn es nicht vorhanden ist

   ```bash
   mkdir m2-hotfixes
   ```

1. Kopieren Sie die Patch-Datei in den `/m2-hotfixes` Verzeichnis.

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
   >Testen Sie alle Patches in einer Produktionsumgebung vor der Produktion. Für Adobe Commerce in der Cloud-Infrastruktur können Sie Zweige mit der `magento-cloud environment:branch <branch-name>` CLI-Befehl.

## Benutzerdefinierten Patch zurücksetzen

So stellen Sie einen zuvor angewendeten benutzerspezifischen Patch wieder her oder deinstallieren ihn:

1. Löschen Sie die Patch-Datei aus der `/m2-hotfixes` Verzeichnis.

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
   >Stellen Sie sicher, dass Sie in einer Produktionsumgebung testen. Für Adobe Commerce in der Cloud-Infrastruktur können Sie Zweige mit der `magento-cloud environment:branch <branch-name>` CLI-Befehl.

## Anwenden von Patches auf ein Nicht-Cloud-Projekt

Verwenden Sie die [Werkzeug für Qualitätsmuster](https://github.com/magento/quality-patches) für Magento Open Source- und Adobe Commerce-Projekte.

## Patch in einer lokalen Umgebung wiederherstellen

Sie können alle zuvor angewendeten Patches in einer lokalen Entwicklungsumgebung mithilfe der `ece-patches` CLI.

So stellen Sie alle angewendeten Patches wieder her:

```bash
php ./vendor/bin/ece-patches revert
```

Mit diesem Befehl werden alle Patches in der folgenden Reihenfolge zurückgesetzt:

- Stellt alle angewendeten benutzerdefinierten Patches aus dem Verzeichnis /m2-hotfixes wieder her.
- Gibt alle angewendeten optionalen individuellen Patches zurück.
- Gibt alle angewendeten erforderlichen Patches zurück.

## Protokollierung

Das Tool &quot;Qualitätsmuster&quot;protokolliert alle Vorgänge zum `<Project_root>/var/log/patch.log` -Datei.
