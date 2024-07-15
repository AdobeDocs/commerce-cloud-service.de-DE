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

Die Bereitstellung statischer Inhalte (SCD) hat erhebliche Auswirkungen auf den Prozess der Speicherbereitstellung, der davon abhängt, wie viel Inhalt generiert werden muss (z. B. Bilder, Skripte, CSS, Videos, Designs, Gebietsschemata und Webseiten) und wann der Inhalt generiert werden soll. Beispielsweise generiert die Standardstrategie statischen Inhalt während der [Bereitstellungsphase](process.md#deploy-phase-deploy-phase), wenn sich die Site im Wartungsmodus befindet. Diese Bereitstellungsstrategie benötigt jedoch Zeit, um den Inhalt direkt in den bereitgestellten `pub/static` -Ordner zu schreiben. Sie haben verschiedene Optionen oder Strategien, um die Bereitstellungszeit je nach Bedarf zu verbessern.

## Optimieren von JavaScript- und HTML-Inhalten

Sie können das Bundling und die Minimierung verwenden, um während der Bereitstellung statischer Inhalte optimierte JavaScript- und HTML-Inhalte zu erstellen.

### Inhalte minimieren

Sie können die Ladezeit der SCD während des Bereitstellungsprozesses verbessern, wenn Sie das Kopieren der statischen Ansichtsdateien in den Ordner &quot;`var/view_preprocessed`&quot;überspringen und bei Anforderung den HTML &quot;_minified_&quot; generieren. Sie können dies aktivieren, indem Sie die globale Umgebungsvariable [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) in der Datei `.magento.env.yaml` auf `true` setzen.

>[!NOTE]
>
>Ab der `ece-tools` -Paketversion 2002.0.13 wird der Standardwert für die Variable SKIP_HTML_MINIFICATION auf `true` gesetzt.

Sie können **mehr** Bereitstellungszeit und Speicherplatz sparen, indem Sie die Anzahl unnötiger Designdateien reduzieren. Sie können beispielsweise das Thema `magento/backend` auf Englisch und ein benutzerdefiniertes Design in anderen Sprachen bereitstellen. Sie können diese Designeinstellungen mit der Umgebungsvariablen [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) konfigurieren.

## Implementierungsstrategie auswählen

Bereitstellungsstrategien unterscheiden sich je nachdem, ob Sie während der _Build_-Phase, der _Bereitstellung_-Phase oder _On-Demand_ statischen Inhalt generieren möchten. Wie in der folgenden Tabelle dargestellt, ist das Generieren von statischem Inhalt während der Bereitstellungsphase die am wenigsten optimale Wahl. Selbst bei minimiertem HTML muss jede Inhaltsdatei in das bereitgestellte Verzeichnis `~/pub/static` kopiert werden, was lange dauern kann. Die Erzeugung von statischen Inhalten bei Bedarf scheint die optimale Wahl zu sein. Wenn die Inhaltsdatei jedoch nicht im Cache vorhanden ist, wird sie zum Zeitpunkt der Anforderung generiert. Dadurch wird dem Benutzererlebnis Ladezeit hinzugefügt. Daher ist das Generieren von statischem Inhalt während der Build-Phase am besten geeignet.

![SCD-Ladevergleich](../../assets/scd-load-times.png)

### Festlegen der SCD beim Build

Die Generierung von statischem Inhalt während der Build-Phase mit minimiertem HTML ist die optimale Konfiguration für [**Zero-Down** -Implementierungen](reduce-downtime.md), auch als **idealer Status** bezeichnet. Anstatt Dateien auf ein bereitgestelltes Laufwerk zu kopieren, wird ein Symlink aus dem Verzeichnis &quot;`./init/pub/static`&quot;erstellt.

Die Erstellung statischer Inhalte erfordert Zugriff auf Designs und Gebietsschemata. Adobe Commerce speichert Designs im Dateisystem, auf das während der Build-Phase zugegriffen werden kann. Adobe Commerce speichert jedoch Gebietsschemata in der Datenbank. Die Datenbank ist während der Build-Phase _nicht_ verfügbar. Um den statischen Inhalt während der Build-Phase zu generieren, müssen Sie den Befehl `config:dump` im Paket `ece-tools` verwenden, um Gebietsschemata in das Dateisystem zu verschieben. Die Gebietsschemata werden gelesen und in der Datei `app/etc/config.php` gespeichert.

**So konfigurieren Sie Ihr Projekt, um SCD auf Build zu generieren**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Verschieben Sie die Gebietsschemata in das Dateisystem und aktualisieren Sie dann die Datei [`config.php`](../development/commerce-version.md#create-a-configphp-file).

1. Die Konfigurationsdatei `.magento.env.yaml` sollte die folgenden Werte enthalten:

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) is `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) auf der Build-Phase ist `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) ist `compact`

1. Überprüfen Sie die Konfiguration des [Post-deploy-Hooks](../application/hooks-property.md) in der Datei `.magento.app.yaml` .

1. Überprüfen Sie Ihre Einstellungen, indem Sie den [Smart-Assistenten für den idealen Status](smart-wizards.md) ausführen.

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### SCD bei Bedarf festlegen

Die Generierung von SCD On Demand ist für einen Entwicklungs-Workflow in der Integrationsumgebung optimal. Dadurch wird die Bereitstellungszeit verkürzt, sodass Sie Ihre Implementierungen schnell überprüfen und Integrationstests ausführen können. Aktivieren Sie die Umgebungsvariable [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) im globalen Schritt der Datei `.magento.env.yaml` . Die Variable &quot;SCD_ON_DEMAND&quot;überschreibt alle anderen Konfigurationen, die mit der SCD zusammenhängen, und löscht vorhandenen Inhalt aus dem Ordner &quot;`~/pub/static`&quot;.

Bei Verwendung der On-Demand-Strategie für SCD hilft es, den Cache mit Seiten, die Sie erwarten, vorab zu laden, z. B. die Startseite. Fügen Sie Ihre Liste der erwarteten Seiten in der Umgebungsvariablen [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) in der Phase nach der Bereitstellung der Datei `.magento.env.yaml` hinzu.

>[!WARNING]
>
>Verwenden Sie nicht die SCD-On-Demand-Strategie in der Produktionsumgebung.

### SCD überspringen

Manchmal können Sie die Generierung statischer Inhalte überspringen. Sie können die Umgebungsvariable [SKIP_SCD](../environment/variables-build.md#skipscd) in der globalen Bühne so festlegen, dass andere Konfigurationen im Zusammenhang mit SCD ignoriert werden. Vorhandenen Inhalt im Verzeichnis `~/pub/static` sind hiervon nicht betroffen.
