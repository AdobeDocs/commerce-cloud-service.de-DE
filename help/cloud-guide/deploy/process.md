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

Der Bereitstellungsprozess beginnt, wenn Sie eine Zusammenführung, Push-Benachrichtigung oder Synchronisation Ihrer Umgebung durchführen oder wenn Sie eine [manuelle Neuimplementierung](../dev-tools/cloud-cli-overview.md#redeploy-the-environment) Trigger haben. Der Implementierungsprozess nimmt Zeit in Anspruch. Es gibt jedoch Möglichkeiten zur Optimierung der Bereitstellung, die davon abhängen, ob Sie eine Live-Site entwickeln und testen oder mit einer Live-Site arbeiten. Insbesondere können Sie die [Bereitstellung statischer Inhalte](static-content.md) steuern.

Der Implementierungsprozess gliedert sich in drei Phasen: Erstellung, Bereitstellung und Bereitstellung. Jede Phase führt spezifische Aktionen mit eingeschränkten Ressourcen durch:

## ![Build-Phase](../../assets/status-build.png) Build-Phase

In der Phase _build_ werden Container für die in den Konfigurationsdateien definierten Dienste zusammengestellt, Abhängigkeiten basierend auf der Datei `composer.lock` installiert und die in der Datei `.magento.app.yaml` definierten Build-Hooks ausgeführt. Ohne die Möglichkeit, eine Verbindung zu einem Dienst herzustellen oder auf die Datenbank zuzugreifen, hängt die Build-Phase von den Ressourcen ab, die auf die Umgebung beschränkt sind.

## ![Bereitstellungsphase](../../assets/status-deploy.png) Bereitstellungsphase

Die Phase _deploy_ legt eingehende Anforderungen vorübergehend fest und überführt die Site in den [Wartungsmodus](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). In der Bereitstellungsphase werden die neuen Container verwendet und nach der Bereitstellung des Dateisystems Netzwerkverbindungen geöffnet, die im Abschnitt &quot;`relationships`&quot;der Datei &quot;`.magento.app.yaml`&quot;definierten Dienste aktiviert und die in der Datei &quot;`.magento.app.yaml`&quot;definierten Bereitstellungshaken ausgeführt. Alles ist _schreibgeschützt_, mit Ausnahme der Verzeichnisse, die in der Datei `.magento.app.yaml` definiert sind. Standardmäßig enthält die [`mounts` -Eigenschaft](../application/properties.md#mounts) die folgenden Ordner:

- `app/etc`—enthält die Konfigurationsdateien `env.php` und `config.php`
- `pub/media` - enthält alle Mediendaten, wie Produkte oder Kategorien
- `pub/static` - enthält generierte statische Dateien
- `var`—enthält temporäre Dateien, die während der Laufzeit erstellt wurden

Alle anderen Verzeichnisse verfügen über schreibgeschützte Berechtigungen. Die neue Site wird am Ende der Bereitstellungsphase aktiv, wenn sie aus dem Wartungsmodus ausgeht und den temporären Haltepunkt für eingehende Anforderungen freigibt.

In der Bereitstellungsphase werden Kopien der Konfigurationsdateien für die `app/etc/config.php`- und `app/etc/env.php`-Bereitstellung mit der BAK-Erweiterung gespeichert. Weitere Informationen zum Wiederherstellen dieser Dateien finden Sie unter [Speichereinstellungen](../store/store-settings.md#restore-configuration-files) .

## ![Post-Bereitstellungsphase](../../assets/status-post-deploy.png) Post-Bereitstellungsphase

In der Phase _nach der Bereitstellung_ werden die in der Datei `.magento.app.yaml` definierten Hooks nach der Bereitstellung ausgeführt. Die Durchführung einer Aktion in dieser Phase kann die Site-Leistung beeinträchtigen. Sie können jedoch die Umgebungsvariable [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) verwenden, um den Cache zu füllen.

## ![Status überprüfen](../../assets/status-verify.png) Konfigurationen überprüfen

Sie können die optimale Konfiguration für den Status Ihres Projekts testen, indem Sie die [Smart-Assistenten](smart-wizards.md) ausführen.

>[!NOTE]
>
>Ab Version `ece-tools` 2002.1.0 können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um die Build-, Bereitstellungs- und Nachbereitstellungsprozesse für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anzupassen. Siehe [Scenario-basierte Bereitstellung](scenario-based.md).
