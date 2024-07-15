---
title: Erstellen von Variablen
description: Sehen Sie sich die Liste der Umgebungsvariablen an, die Aktionen in der Adobe Commerce-Build-Phase der Cloud-Infrastruktur steuern.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Erstellen von Variablen

Die folgenden _build_ -Variablen steuern Aktionen in der Build-Phase und können Werte von den [globalen Variablen](variables-global.md) übernehmen und überschreiben. Fügen Sie diese Variablen in die `build` -Phase der `.magento.env.yaml`-Datei ein:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Weitere Informationen zum Anpassen des Build- und Bereitstellungsprozesses finden Sie unter

- [Bereitstellungskonfiguration](configure-env-yaml.md)
- [Bereitstellungsprozess](../deploy/process.md)

Die folgenden Variablen wurden in Version 2.2 entfernt:

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Standard**—`1`
- **Version**—Adobe Commerce 2.1.4 und höher

Legen Sie die Verzeichnisverschachtelungsebene zum Speichern von Fehlerberichtsdateien fest, um zu vermeiden, dass der Berichtordner mit Zehntausenden von Dateien gefüllt wird, wodurch die Verwaltung und Überprüfung der Daten erschwert werden kann. Diese Einstellung ist standardmäßig auf `1` eingestellt. In der Regel müssen Sie den Standardwert nur ändern, wenn Sie Probleme bei der Verwaltung von Fehlerberichtsdateien im Verzeichnis `<magento_root>/var/report/` haben.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Geben Sie eine Liste der Adobe Commerce-Qualitäts-Patches an, die während der Bereitstellung angewendet werden sollen.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

Im folgenden Beispiel werden drei Patches aufgeführt, die während der Bereitstellung angewendet werden sollen.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Siehe [Anwenden von Patches](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

- **Standard**—`6`
- **Version**—Adobe Commerce 2.1.4 und höher

Gibt an, welche [gzip](https://www.gnu.org/software/gzip)-Komprimierungsstufe (`0` bis `9`) beim Komprimieren statischen Inhalts verwendet werden soll. `0` deaktiviert die Komprimierung.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standard**—`600`
- **Version**—Adobe Commerce 2.1.4 und höher

Wenn die zum Komprimieren der statischen Assets benötigte Zeit das Zeitlimit für die Komprimierung überschreitet, wird der Bereitstellungsprozess unterbrochen. Legen Sie die maximale Ausführungszeit in Sekunden für den Befehl zur statischen Inhaltskomprimierung fest.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.4.2 und höher

Setzen Sie dies auf &quot;`true`&quot;, um zu verhindern, dass statische Inhalte für übergeordnete Designs während der Build-Phase generiert werden.

Legen Sie während der Build-Phase den Wert &quot;`SCD_NO_PARENT: false`&quot;fest, damit das Generieren von statischem Inhalt für die übergeordneten Designs keine Auswirkungen auf die Site-Bereitstellung hat oder zu unnötigen Site-Ausfallzeiten führt. Siehe [Bereitstellung statischer Inhalte](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Sie können mehrere Gebietsschemata pro Design konfigurieren. Diese Anpassung beschleunigt den Build-Prozess, indem die Anzahl unnötiger Designdateien verringert wird. Sie können beispielsweise das Design _magento/backend_ auf Englisch und ein benutzerdefiniertes Design in anderen Sprachen erstellen.

Im folgenden Beispiel wird das `Magento/backend` -Design mit drei Gebietsschemas erstellt:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Im folgenden Beispiel werden drei Designs mit drei Gebietsschemas erstellt:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Sie können auch festlegen, dass _nicht_ ein Design bereitstellt:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.2.0 und höher

Ermöglicht Ihnen, die maximale erwartete Ausführungszeit für die Bereitstellung statischer Inhalte zu erhöhen.

Standardmäßig setzt Adobe Commerce in der Cloud-Infrastruktur die maximal erwartete Ausführung auf 900 Sekunden. In einigen Szenarien benötigen Sie jedoch möglicherweise mehr Zeit, um die Bereitstellung statischer Inhalte für ein Cloud-Projekt abzuschließen.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Standard**—`quick`
- **Version**—Adobe Commerce 2.2.0 und höher

Passen Sie die [Bereitstellungsstrategie](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) für statischen Inhalt an. Siehe [Bereitstellen von statischen Ansichtsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Verwenden Sie diese Optionen _nur_ , wenn Sie mehr als ein Gebietsschema haben:

- `standard` - stellt alle statischen Ansichtsdateien für alle Pakete bereit.
- `quick`—(_default_) minimiert die Bereitstellungszeit.
- `compact` - Speichert Speicherplatz auf dem Server. In Adobe Commerce Version 2.2.4 und früher überschreibt diese Einstellung den Wert für `scd_threads` mit dem Wert `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standard**—Automatisch
- **Version**—Adobe Commerce 2.1.4 und höher

Legt die Anzahl der Threads für die Bereitstellung statischer Inhalte fest. Der Standardwert wird basierend auf der erkannten CPU-Thread-Anzahl festgelegt und überschreitet nicht den Wert 4. Durch die Erhöhung der Thread-Anzahl wird die Bereitstellung statischer Inhalte beschleunigt, und die Verringerung der Thread-Anzahl verlangsamt die Bereitstellung. Sie können den Thread-Wert festlegen, beispielsweise:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Um die Bereitstellungszeit weiter zu verkürzen, verwenden Sie [Konfigurationsverwaltung](../store/store-settings.md) mit dem Befehl `scd-dump` , um die statische Bereitstellung in die Build-Phase zu verschieben.

## `SCD_USE_BALER`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.3.0 und höher

[Baler](https://github.com/magento/baler) scannt Ihren generierten JavaScript-Code und erstellt ein optimiertes JavaScript-Bundle. Wenn Sie das optimierte Bundle auf Ihrer Site bereitstellen, kann sich die Anzahl der Netzwerkanforderungen beim Laden Ihrer Site verringern und die Seitenladezeiten verbessern.

Legen Sie diese Einstellung auf &quot;`true`&quot;fest, um Baler nach der Bereitstellung statischer Inhalte auszuführen.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Da Baler in der Alpha-Version verfügbar ist, ist es nicht ratsam, es in Produktionsumgebungen zu verwenden.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Standard**— _Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Setzen Sie dies auf `true` , um den Befehl `composer dump-autoload` während einer Cloud Docker-Installation zu überspringen. Diese Variable ist nur für Cloud Docker-Container mit beschreibbaren Dateisystemen relevant. In solchen Fällen verhindert das Überspringen des Befehls Fehler von anderen Befehlen, die versuchen, auf den Code aus dem gelöschten Verzeichnis `generated` zuzugreifen.

Wenn Adobe Commerce `composer dump-autoload` ausführt, werden automatische Dateien mit Links zu generierten Klassen im Ordner `generated` erstellt, was in Produktionsumgebungen mit schreibgeschützten Dateisystemen kein Problem darstellt. Bei Cloud Docker-Installationen mit beschreibbaren Dateisystemen (die nur zum Testen und Entwickeln mit `./vendor/bin/ece-docker build:compose --with-test` erstellt wurden) können Sie jedoch den Befehl `bin/magento -n setup:upgrade` ohne die Option `--keep-generated` ausführen, wodurch der Ordner `generated` gelöscht wird. Wenn das Verzeichnis gelöscht wird, schlägt der Befehl `composer dump-autoload` fehl, da die automatische Aktualisierung Links zu Dateien im gelöschten Verzeichnis enthält.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Standard**— _Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Setzen Sie dies auf &quot;`true`&quot;, um die Bereitstellung statischer Inhalte während der Build-Phase zu überspringen.

Wenn Sie statischen Inhalt bereits während der Build-Phase mit [Konfigurationsverwaltung](../store/store-settings.md) bereitstellen, können Sie die Bereitstellung statischer Inhalte für einen schnellen Build-Test überspringen.

Setzen Sie in der Erstellungsphase `SKIP_SCD: false` so, dass der statische Inhaltserstellung während der Erstellungsphase erfolgt, wobei der Prozess keine Auswirkungen auf die Site-Bereitstellung hat oder zu unnötigen Site-Ausfallzeiten führt. Siehe [Bereitstellung statischer Inhalte](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivieren oder deaktivieren Sie die Debugging-Ausführlichkeitsstufe für `bin/magento` CLI-Befehle, die während der Bereitstellungsphase ausgeführt werden.[](https://symfony.com/doc/current/console/verbosity.html)

>[!NOTE]
>
>Um VERBOSE_COMMANDS zur Steuerung der Details in der Befehlsausgabe für erfolgreiche und fehlgeschlagene `bin/magento` CLI-Befehle zu verwenden, müssen Sie [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug` festlegen.

Wählen Sie den Detailgrad aus, der in den Protokollen angegeben wird:

- `-v` = normale Ausgabe
- `-vv`= ausführlichere Ausgabe
- `-vvv` = ausführliche Ausgabe, ideal für das Debugging

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
