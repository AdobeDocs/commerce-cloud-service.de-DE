---
title: Umgebung konfigurieren
description: Erfahren Sie, wie Sie mithilfe von Umgebungsvariablen Build- und Bereitstellungsaktionen in allen Commerce-Umgebungen in Cloud-Infrastrukturumgebungen konfigurieren, einschließlich Pro Staging und Produktion.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Umgebungsvariablen für die Bereitstellung konfigurieren

Die Datei &quot;`.magento.env.yaml`&quot;verwendet Umgebungsvariablen, um die Verwaltung von Build- und Bereitstellungsaktionen in allen Ihren Umgebungen zu zentralisieren, einschließlich Pro Staging und Produktion. Um eindeutige Aktionen in jeder Umgebung zu konfigurieren, müssen Sie diese Datei in jeder Umgebung ändern.

>[!TIP]
>
>Bei YAML-Dateien wird zwischen Groß- und Kleinschreibung unterschieden und Tabs sind nicht zulässig. Achten Sie darauf, einen konsistenten Einzug in der gesamten Datei `.magento.env.yaml` zu verwenden, da Ihre Konfiguration sonst möglicherweise nicht wie erwartet funktioniert. Die Beispiele in der Dokumentation und in der Beispieldatei verwenden den Einzug _two-space_ . Verwenden Sie den Befehl [ece-tools validate](#validate-configuration-file) , um Ihre Konfiguration zu überprüfen.

## Dateistruktur

Die Datei `.magento.env.yaml` enthält zwei Abschnitte: `stage` und `log`. Der Abschnitt `stage` steuert Aktionen, die in den Phasen des [Cloud-Bereitstellungsprozesses](../deploy/process.md) auftreten.

- `stage`—Verwenden Sie den Abschnitt &quot;Staging&quot;, um bestimmte Aktionen für die folgenden Bereitstellungsschritte zu definieren:
   - `global` - Steuert Aktionen sowohl in der Build- als auch in der Bereitstellungsphase und nach der Bereitstellung. Sie können diese Einstellungen in den Abschnitten &quot;Build&quot;, &quot;Bereitstellung&quot;und &quot;Nach der Bereitstellung&quot;überschreiben.
   - `build` - Steuert nur Aktionen in der Build-Phase. Wenn Sie in diesem Abschnitt keine Einstellungen angeben, verwendet die Build-Phase die Einstellungen aus dem globalen Abschnitt.
   - `deploy` - Steuert nur Aktionen in der Bereitstellungsphase. Wenn Sie in diesem Abschnitt keine Einstellungen angeben, verwendet die Bereitstellungsphase Einstellungen aus dem globalen Abschnitt.
   - `post-deploy`—Steuert die Aktionen _nach der_ Bereitstellung Ihrer Anwendung und _nach_, wenn der Container Verbindungen akzeptiert.
- `log` - Verwenden Sie den Protokollabschnitt, um [Benachrichtigungen](set-up-notifications.md) zu konfigurieren, einschließlich Benachrichtigungstypen und Detailebene.
   - `slack` - Konfigurieren Sie eine Nachricht, die an einen Slack-Bot gesendet werden soll.
   - `email` - Konfigurieren Sie eine E-Mail für den Versand an einen oder mehrere E-Mail-Empfänger.
   - [log-Handler](log-handlers.md): Konfigurieren Sie Hardware- und Softwareanwendungsmeldungen, die an einen Remote-Protokollierungsserver gesendet werden.

### Umgebungsvariablen

Das Paket `ece-tools` legt Werte in der Datei `env.php` basierend auf Werten aus [Cloud-Variablen](variables-cloud.md), Variablen, die in der Konfigurationsdatei [!DNL Cloud Console] festgelegt sind, und `.magento.env.yaml` fest. Die Umgebungsvariablen in der Datei `.magento.env.yaml` passen die Cloud-Umgebung an, indem Sie Ihre vorhandene Commerce-Konfiguration überschreiben. Wenn der Standardwert `Not Set` ist, nimmt das `ece-tools` -Paket die Aktion **NO** an und verwendet den Standardwert [!DNL Commerce] oder den Wert aus der MAGENTO_CLOUD_RELATIONSHIPS -Konfiguration. Wenn der Standardwert festgelegt ist, wird dieser Standardwert durch das Paket `ece-tools` festgelegt.

Die folgenden Themen enthalten detaillierte Definitionen aller Variablen, die Sie in der Datei `.magento.env.yaml` verwenden können, z. B. ob ein Standardwert festgelegt ist oder nicht:

- [Global](variables-global.md)—Variablen steuern Aktionen in jeder Phase: Erstellen, Bereitstellen und Nach der Bereitstellung
- [Build](variables-build.md)—Variablen steuern Build-Aktionen
- [Bereitstellen](variables-deploy.md)—Variablen steuern die Bereitstellungsaktionen
- [Nach der Bereitstellung](variables-post-deploy.md)—Variablen steuern Aktionen nach der Bereitstellung

### Konfigurationsdatei über CLI erstellen

Sie können eine `.magento.env.yaml` -Konfigurationsdatei für eine Cloud-Umgebung mit den folgenden `ece-tools` -Befehlen generieren.

>Erstellt eine Konfigurationsdatei

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Aktualisieren von Werten in der Konfigurationsdatei

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Beide Befehle erfordern ein einzelnes Argument: ein JSON-formatiertes Array, das einen Wert für mindestens eine Build-, Bereitstellungs- oder Post-deploy-Variable angibt. Der folgende Befehl legt beispielsweise Werte für die Variablen `SCD_THREADS` und `CLEAN_STATIC_FILES` fest:

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

Erstellen Sie eine `.magento.env.yaml` -Datei mit den folgenden Einstellungen:

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

Sie können den Befehl `cloud:config:update` verwenden, um die neue Datei zu aktualisieren. Beispielsweise ändert der folgende Befehl den Wert `SCD_THREADS` und fügt die Konfiguration `SCD_COMPRESSION_TIMEOUT` hinzu:

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

Die aktualisierte Datei enthält die folgende Konfiguration:

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### Konfigurationsdatei überprüfen

Verwenden Sie den folgenden `ece-tools`-Befehl, um die Konfigurationsdatei `.magento.env.yaml` zu validieren, bevor Sie Änderungen an die Remote-Cloud-Umgebung senden.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

Die folgende Beispielantwort enthält eine Liste der zu korrigierenden Elemente:

```
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP-Konstanten

Sie können PHP-Konstanten in `.magento.env.yaml` -Dateidefinitionen anstelle von Hartkodierungswerten verwenden. Im folgenden Beispiel wird der `driver_options` mithilfe einer PHP-Konstante definiert:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>Das ständige Parsen funktioniert nicht, wenn eine `symfony/yaml` -Paketversion vor 3.2 verwendet wird.

## Umgang mit Fehlern

Wenn ein Fehler aufgrund eines unerwarteten Werts in der Konfigurationsdatei `.magento.env.yaml` auftritt, erhalten Sie eine Fehlermeldung. Beispielsweise enthält die folgende Fehlermeldung eine Liste der vorgeschlagenen Änderungen an jedem Element mit einem unerwarteten Wert und manchmal gültige Optionen:

```
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

Nehmen Sie alle Korrekturen vor, übertragen Sie die Änderungen und übertragen Sie sie. Wenn Sie keine Fehlermeldung erhalten, werden die Änderungen an Ihrer Konfigurationsdatei erfolgreich validiert.

## Optimierung der Konfigurationsverwaltung

Wenn Sie Configuration Management nach dem Ablegen der Konfigurationen aktiviert haben, sollten Sie die SCD_*-Variablen aus der Bereitstellung in die Build-Phase verschieben. Siehe [Bereitstellungsstrategien für statische Inhalte](../deploy/static-content.md).

>Vor der Konfigurationsverwaltung:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

>Nachdem Sie Configuration Management aktiviert haben, verschieben Sie die SCD_*-Variablen in die Build-Phase:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```
