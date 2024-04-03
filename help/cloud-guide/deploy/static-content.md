---
title: Statische Inhaltsbereitstellung
description: Erfahren Sie mehr über Strategien für die Bereitstellung von statischen Inhalten wie Bildern, Skripten und CSS in Adobe Commerce für Cloud-Infrastrukturprojekte.
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Implementierungsstrategien für statische Inhalte

Die Bereitstellung statischer Inhalte (SCD) hat erhebliche Auswirkungen auf den Prozess der Speicherbereitstellung, der davon abhängt, wie viel Inhalt generiert werden muss (z. B. Bilder, Skripte, CSS, Videos, Designs, Gebietsschemata und Webseiten) und wann der Inhalt generiert werden soll. Beispielsweise erzeugt die Standardstrategie statischen Inhalt während der [Bereitstellungsphase](process.md#deploy-phase-deploy-phase) wenn sich die Site im Wartungsmodus befindet. Diese Bereitstellungsstrategie nimmt jedoch Zeit in Anspruch, um den Inhalt direkt in den bereitgestellten `pub/static` Verzeichnis. Sie haben verschiedene Optionen oder Strategien, um die Bereitstellungszeit je nach Bedarf zu verbessern.

## JavaScript- und HTML-Inhalte optimieren

Sie können das Bundling und die Minimierung verwenden, um während der Bereitstellung statischer Inhalte optimierte JavaScript- und HTML-Inhalte zu erstellen.

### Inhalte minimieren

Sie können die Ladezeit für die SDK während des Bereitstellungsprozesses verbessern, wenn Sie das Kopieren der statischen Ansichtsdateien in die `var/view_preprocessed` Verzeichnis erstellen _minified_ HTML bei Bedarf. Sie können dies aktivieren, indem Sie die [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) globale Umgebungsvariable auf `true` im `.magento.env.yaml` -Datei.

>[!NOTE]
>
>Beginnen Sie mit der `ece-tools` Paketversion 2002.0.13, ist der Standardwert für die Variable SKIP_HTML_MINIFICATION auf `true`.

Sie können **more** Bereitstellungszeit und Speicherplatz durch Reduzierung der Anzahl unnötiger Designdateien. Beispielsweise können Sie die `magento/backend` Thema auf Englisch und ein benutzerdefiniertes Thema in anderen Sprachen. Sie können diese Designeinstellungen mit dem [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) Umgebungsvariable.

## Implementierungsstrategie auswählen

Die Implementierungsstrategien unterscheiden sich je nachdem, ob Sie während der _build_ Phase, _deploy_ Phase oder _On-Demand_. Wie in der folgenden Tabelle dargestellt, ist das Generieren von statischem Inhalt während der Bereitstellungsphase die am wenigsten optimale Wahl. Selbst bei minimiertem HTML muss jede Inhaltsdatei in den bereitgestellten `~/pub/static` -Verzeichnis, das lange dauern kann. Die Erzeugung von statischen Inhalten bei Bedarf scheint die optimale Wahl zu sein. Wenn die Inhaltsdatei jedoch nicht im Cache vorhanden ist, wird sie zum Zeitpunkt der Anforderung generiert. Dadurch wird dem Benutzererlebnis Ladezeit hinzugefügt. Daher ist das Generieren von statischem Inhalt während der Build-Phase am besten geeignet.

![Vergleich der SCD-Auslastung](../../assets/scd-load-times.png)

### Festlegen der SCD beim Build

Die Generierung von statischem Inhalt während der Build-Phase mit minimiertem HTML ist die optimale Konfiguration für [**Zero-Ausfallzeit** Bereitstellungen](reduce-downtime.md), auch als **idealer Zustand**. Anstatt Dateien auf ein bereitgestelltes Laufwerk zu kopieren, wird ein Symlink aus dem `./init/pub/static` Verzeichnis.

Die Erstellung statischer Inhalte erfordert Zugriff auf Designs und Gebietsschemata. Adobe Commerce speichert Designs im Dateisystem, auf das während der Build-Phase zugegriffen werden kann. Adobe Commerce speichert jedoch Gebietsschemata in der Datenbank. Die Datenbank ist _not_ verfügbar während der Build-Phase. Um den statischen Inhalt während der Build-Phase zu generieren, müssen Sie die `config:dump` im `ece-tools` -Paket, um Gebietsschemata in das Dateisystem zu verschieben. Es liest die Gebietsschemata und speichert sie im `app/etc/config.php` -Datei.

**So konfigurieren Sie Ihr Projekt, um SCD beim Build zu generieren**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Verschieben Sie die Gebietsschemata in das Dateisystem und aktualisieren Sie dann die [`config.php` file](../development/commerce-version.md#create-a-configphp-file).

1. Die `.magento.env.yaml` Die Konfigurationsdatei sollte die folgenden Werte enthalten:

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) is `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) auf der Build-Phase `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) is `compact`

1. Überprüfen der Konfiguration der [Hook nach der Bereitstellung](../application/hooks-property.md) im `.magento.app.yaml` -Datei.

1. Überprüfen Sie Ihre Einstellungen, indem Sie die [Intelligenter Assistent für den idealen Status](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### SCD bei Bedarf festlegen

Die Generierung von SCD On Demand ist für einen Entwicklungs-Workflow in der Integrationsumgebung optimal. Dadurch wird die Bereitstellungszeit verkürzt, sodass Sie Ihre Implementierungen schnell überprüfen und Integrationstests ausführen können. Aktivieren Sie die [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) Umgebungsvariable im globalen Schritt der `.magento.env.yaml` -Datei. Die Variable &quot;SCD_ON_DEMAND&quot;überschreibt alle anderen Konfigurationen, die mit der SCD zusammenhängen, und löscht vorhandenen Inhalt aus der `~/pub/static` Verzeichnis.

Bei Verwendung der On-Demand-Strategie für SCD hilft es, den Cache mit Seiten, die Sie erwarten, vorab zu laden, z. B. die Startseite. Fügen Sie Ihre Liste der erwarteten Seiten im [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) Umgebungsvariable in der Phase nach der Bereitstellung der `.magento.env.yaml` -Datei.

>[!WARNING]
>
>Verwenden Sie nicht die SCD-On-Demand-Strategie in der Produktionsumgebung.

### SCD überspringen

Manchmal können Sie die Generierung statischer Inhalte überspringen. Sie können die [SKIP_SCD](../environment/variables-build.md#skipscd) Umgebungsvariable in der globalen Bühne verwenden, um andere Konfigurationen zu ignorieren, die mit SCD zusammenhängen. Vorhandenen Inhalt in der `~/pub/static` Verzeichnis.
