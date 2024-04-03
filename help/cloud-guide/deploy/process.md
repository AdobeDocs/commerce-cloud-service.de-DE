---
title: Bereitstellungsprozess
description: Erfahren Sie, wie die Bereitstellung für Adobe Commerce in Cloud-Infrastrukturprojekten funktioniert.
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Bereitstellungsprozess

Der Bereitstellungsprozess beginnt, wenn Sie eine Zusammenführung, Push-Benachrichtigung oder Synchronisation Ihrer Umgebung durchführen oder wenn Sie eine [manuelle Neuerstellung](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). Der Implementierungsprozess nimmt Zeit in Anspruch. Es gibt jedoch Möglichkeiten zur Optimierung der Bereitstellung, die davon abhängen, ob Sie eine Live-Site entwickeln und testen oder mit einer Live-Site arbeiten. Insbesondere können Sie die [Bereitstellung statischer Inhalte](static-content.md).

Der Implementierungsprozess gliedert sich in drei Phasen: Erstellung, Bereitstellung und Bereitstellung. Jede Phase führt spezifische Aktionen mit eingeschränkten Ressourcen durch:

## ![Build-Phase](../../assets/status-build.png) Build-Phase

Die _build_ Phasen Assemblieren von Containern für die in den Konfigurationsdateien definierten Dienste, Installiert Abhängigkeiten basierend auf der `composer.lock` und führt die Build-Hooks aus, die in der `.magento.app.yaml` -Datei. Ohne die Möglichkeit, eine Verbindung zu einem Dienst herzustellen oder auf die Datenbank zuzugreifen, hängt die Build-Phase von den Ressourcen ab, die auf die Umgebung beschränkt sind.

## ![Bereitstellungsphase](../../assets/status-deploy.png) Bereitstellungsphase

Die _deploy_ -Phase legt einen temporären Haltepunkt für eingehende Anfragen fest und übergeht die Site auf [Wartungsmodus](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). In der Bereitstellungsphase werden die neuen Container verwendet und nach der Bereitstellung des Dateisystems Netzwerkverbindungen geöffnet. Dadurch werden die in der Variablen `relationships` Abschnitt `.magento.app.yaml` und führt die Bereitstellungshaken aus, die in der Datei `.magento.app.yaml` -Datei. Alles ist _schreibgeschützt_, mit Ausnahme der in der Variablen `.magento.app.yaml` -Datei. Standardmäßig wird die Variable [`mounts` property](../application/properties.md#mounts) enthält die folgenden Verzeichnisse:

- `app/etc`—enthält die `env.php` und `config.php` Konfigurationsdateien
- `pub/media`—enthält alle Mediendaten wie Produkte oder Kategorien
- `pub/static`—enthält generierte statische Dateien
- `var`—enthält temporäre Dateien, die während der Laufzeit erstellt wurden

Alle anderen Verzeichnisse verfügen über schreibgeschützte Berechtigungen. Die neue Site wird am Ende der Bereitstellungsphase aktiv, wenn sie aus dem Wartungsmodus ausgeht und den temporären Haltepunkt für eingehende Anforderungen freigibt.

In der Bereitstellungsphase kopieren Sie die `app/etc/config.php` und `app/etc/env.php` Konfigurationsdateien für die Bereitstellung werden mit der BAK-Erweiterung gespeichert. Siehe [Speichereinstellungen](../store/store-settings.md#restore-configuration-files) , um mehr über die Wiederherstellung dieser Dateien zu erfahren.

## ![Phase nach der Bereitstellung](../../assets/status-post-deploy.png) Phase nach der Bereitstellung

Die _nach der Bereitstellung_ -Phase führt die in der `.magento.app.yaml` -Datei. Die Durchführung einer Aktion in dieser Phase kann sich auf die Site-Leistung auswirken. Sie können jedoch die [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) Umgebungsvariable zum Füllen des Caches.

## ![Überprüfungsstatus](../../assets/status-verify.png) Konfigurationen überprüfen

Sie können die optimale Konfiguration für den Status Ihres Projekts testen, indem Sie die [Smart-Assistenten](smart-wizards.md).

>[!NOTE]
>
>Mit `ece-tools` 2002.1.0 und höher können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um die Build-, Bereitstellungs- und Nachbereitstellungsprozesse für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anzupassen. Siehe [Szenario-basierte Bereitstellung](scenario-based.md).
