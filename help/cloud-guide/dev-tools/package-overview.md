---
title: '[!DNL ECE-Tools] package'
description: Erfahren Sie mehr über das [!DNL ECE-Tools] Paket und wie es bei der Verwaltung und Bereitstellung von Adobe Commerce hilft.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-Tools-Paket

Das Paket [!DNL ECE-Tools] ist ein Satz von Skripten und Tools, die für die Verwaltung und Bereitstellung der [!DNL Commerce] -Anwendung entwickelt wurden. Das Paket `ece-tools` vereinfacht viele Prozesse, z. B. das Verwalten von Cron-Aufträgen, das Überprüfen der Projektkonfiguration und das Anwenden von Adobe-Patches und Hotfixes. Sie können das [Open-Source [!DNL ECE-Tools] Code-Repository auf GitHub][ece-repo] anzeigen und dazu beitragen.

{{ece-tools-package}}

Das Paket `ece-tools` ist mit Adobe Commerce kompatibel - beginnend mit Version 2.1.4 - und enthält Skripte und Adobe Commerce zu Cloud-Infrastrukturbefehlen, mit denen Sie Ihren Code verwalten sowie Ihre Projekte automatisch erstellen und bereitstellen können.

In der folgenden Liste sind die verfügbaren `ece-tools`-Befehle aufgeführt:

```bash
php ./vendor/bin/ece-tools list
```

## Erstellen und Bereitstellen

Das Paket `ece-tools` enthält Befehle zum Ausführen von Vorgängen für die Build-, Bereitstellungs- und Post-Bereitstellung-Phasen des Starts Ihrer Adobe Commerce in der Cloud-Infrastrukturanwendung. Beispielsweise startet der Befehl `php ./vendor/bin/ece-tools build` den Build-Prozess der Anwendung.

Standardmäßig befinden sich diese `ece-tools`-Befehle in der [hooks-Eigenschaft](../application/hooks-property.md) der `.magento.app.yaml`-Konfigurationsdatei.

## Docker-Konfigurationsgenerator

Das Paket `ece-tools` enthält eine Abhängigkeit für das Paket [magento/magento-cloud-docker] , das Funktionen und Konfigurationsdateien für Docker-Bilder bereitstellt, um eine Docker-Entwicklungsumgebung für Adobe Commerce in der Cloud-Infrastruktur zu starten. Sie können Cloud Docker für Commerce auch als eigenständiges Paket ausführen. Siehe [Docker-Entwicklung](../dev-tools/cloud-docker.md).

## Dienste, Routen und Variablen

Sie können das Paket `ece-tools` verwenden, um detaillierte Informationen zu den Base64-kodierten [Cloud-Variablen](../environment/variables-cloud.md) anzuzeigen, die in jeder Cloud-Umgebung verwendet werden. Der folgende Befehl zeigt alle Dienste, Routen und Variablen.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Um einen bestimmten Satz von Informationen anzuzeigen, verwenden Sie folgendes Format:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services` - Zeigt die Beziehungsdaten aus der in der Datei `services.yaml` definierten Umgebungsvariablen `MAGENTO_CLOUD_RELATIONSHIPS` an.
- `routes` - Zeigt die konfigurierten Routen für das Projekt mithilfe der Umgebungsvariablen `MAGENTO_CLOUD_ROUTES` an.
- `variables` - Zeigt die konfigurierten Variablen für das Projekt mithilfe der Umgebungsvariablen `MAGENTO_CLOUD_VARIABLES` an.

Beispielausgabe für die Option `services` :

```
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

Es stehen verschiedene Überprüfungsbefehle zur Verfügung, mit denen Sie die Konfiguration Ihres Projekts bewerten können. Eine detaillierte Beschreibung der einzelnen Assistentenbefehle finden Sie unter [Smart-Assistenten](../deploy/smart-wizards.md) im Abschnitt _Implementierung optimieren_ . Der Befehl `wizard:ideal-state` wird während der Build-Phase automatisch ausgeführt. So überprüfen Sie den idealen Zustand Ihres Projekts:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Sie müssen den Befehl `wizard:ideal-state` in der Remote-Cloud-Umgebung ausführen. Der Befehl gibt immer den Fehler `The configured state is not ideal` zurück, wenn er in der lokalen Entwicklungsumgebung ausgeführt wird.

Beispielausgabe:

```
Ideal state is configured
```

Siehe [Versionshinweise für ece-tools](../release-notes/cloud-tools-suite.md).

## Adobe-Patches und benutzerdefinierte Patches

Das Paket `ece-tools` enthält eine Abhängigkeit vom Paket [magento/magento-cloud-patches] , das Adobe-Patches und Hotfixes bereitstellt, die die Integration aller Adobe Commerce-Versionen in Cloud-Umgebungen verbessern und die schnelle Bereitstellung kritischer Fehlerbehebungen unterstützen. Der &quot;stellt auch benutzerdefinierte Patches bereit, die Sie zu Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur hinzufügen. Siehe [Anwenden von Patches](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
