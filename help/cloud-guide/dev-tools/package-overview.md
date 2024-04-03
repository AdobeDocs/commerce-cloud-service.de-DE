---
title: '[!DNL ECE-Tools] Package'
description: Informationen zum [!DNL ECE-Tools] und wie es bei der Verwaltung und Bereitstellung von Adobe Commerce hilft.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-Tools-Paket

Die [!DNL ECE-Tools] -Paket ist ein Satz von Skripten und Tools, die zur Verwaltung und Bereitstellung der [!DNL Commerce] Anwendung. Die `ece-tools` Das -Paket vereinfacht viele Prozesse, z. B. das Verwalten von Cron-Aufträgen, das Überprüfen der Projektkonfiguration und das Anwenden von Adobe-Patches und Hotfixes. Sie können die [Open-Source [!DNL ECE-Tools] Code-Repository auf GitHub][ece-repo].

{{ece-tools-package}}

Die `ece-tools` Das -Paket ist mit Adobe Commerce kompatibel (ab Version 2.1.4) und enthält Skripte und Adobe Commerce zu Cloud-Infrastrukturbefehlen, die Ihnen helfen, Ihren Code zu verwalten und Ihre Projekte automatisch zu erstellen und bereitzustellen.

In der folgenden Liste sind die verfügbaren `ece-tools` Befehle:

```bash
php ./vendor/bin/ece-tools list
```

## Erstellen und Bereitstellen

Die `ece-tools` Das -Paket enthält Befehle zum Ausführen von Vorgängen für die Build-, Bereitstellungs- und Postbereitstellungsphasen des Starts Ihrer Adobe Commerce in der Cloud-Infrastrukturanwendung. Beispiel: die `php ./vendor/bin/ece-tools build` -Befehl startet den Prozess zum Erstellen der Anwendung.

Standardmäßig werden diese `ece-tools` -Befehle befinden sich in der [Hooks-Eigenschaft](../application/hooks-property.md) des `.magento.app.yaml` Konfigurationsdatei.

## Docker-Konfigurationsgenerator

Die `ece-tools` -Paket enthält eine Abhängigkeit für die [magento/magento-cloud-docker] -Paket, das Funktionen und Konfigurationsdateien für Docker-Bilder bereitstellt, um eine Docker-Entwicklungsumgebung für Adobe Commerce in der Cloud-Infrastruktur zu starten. Sie können Cloud Docker für Commerce auch als eigenständiges Paket ausführen. Siehe [Docker-Entwicklung](../dev-tools/cloud-docker.md).

## Dienste, Routen und Variablen

Sie können die `ece-tools` Paket, um detaillierte Informationen zum Base64-kodierten anzuzeigen [Cloud-Variablen](../environment/variables-cloud.md) wird in jeder Cloud-Umgebung verwendet. Der folgende Befehl zeigt alle Dienste, Routen und Variablen.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Um einen bestimmten Satz von Informationen anzuzeigen, verwenden Sie folgendes Format:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services`—Zeigt die Beziehungsdaten aus der `MAGENTO_CLOUD_RELATIONSHIPS` Umgebungsvariable, definiert in der `services.yaml` -Datei.
- `routes`—Zeigt die konfigurierten Routen für das Projekt an, indem Sie die `MAGENTO_CLOUD_ROUTES` Umgebungsvariable.
- `variables`—Zeigt die konfigurierten Variablen für das Projekt an, indem Sie die `MAGENTO_CLOUD_VARIABLES` Umgebungsvariable.

Beispielausgabe für die `services` Option:

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Umgebungskonfiguration überprüfen

Es stehen verschiedene Überprüfungsbefehle zur Verfügung, mit denen Sie die Konfiguration Ihres Projekts bewerten können. Siehe [Smart-Assistenten](../deploy/smart-wizards.md) im _Implementierung optimieren_ für eine detaillierte Beschreibung der einzelnen Assistenten-Befehle. Die `wizard:ideal-state` -Befehl wird während der Build-Phase automatisch ausgeführt. So überprüfen Sie den idealen Zustand Ihres Projekts:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Sie müssen die `wizard:ideal-state` in der Remote-Cloud-Umgebung. Der Befehl gibt immer die `The configured state is not ideal` Fehler bei Ausführung in der lokalen Entwicklungsumgebung.

Beispielausgabe:

```terminal
Ideal state is configured
```

Siehe [Versionshinweise für Eece-Tools](../release-notes/cloud-tools-suite.md).

## Adobe-Patches und benutzerdefinierte Patches

Die `ece-tools` -Paket enthält eine Abhängigkeit für die [magento/magento-cloud-patches] bietet Adobe-Patches und Hotfixes, die die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen verbessern und die schnelle Bereitstellung wichtiger Fehlerbehebungen unterstützen. Der &quot;stellt auch benutzerdefinierte Patches bereit, die Sie zu Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur hinzufügen. Siehe [Anwenden von Patches](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
