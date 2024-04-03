---
title: Umgebung konfigurieren
description: Erfahren Sie, wie Sie mithilfe von Umgebungsvariablen Build- und Bereitstellungsaktionen für alle Commerce-Umgebungen in Cloud-Infrastrukturumgebungen konfigurieren, einschließlich Pro Staging und Produktion.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Umgebungsvariablen für die Bereitstellung konfigurieren

Die `.magento.env.yaml` -Datei verwendet Umgebungsvariablen, um die Verwaltung von Build- und Bereitstellungsaktionen in all Ihren Umgebungen zu zentralisieren, einschließlich Pro Staging und Produktion. Um eindeutige Aktionen in jeder Umgebung zu konfigurieren, müssen Sie diese Datei in jeder Umgebung ändern.

>[!TIP]
>
>Bei YAML-Dateien wird zwischen Groß- und Kleinschreibung unterschieden und Tabs sind nicht zulässig. Achten Sie darauf, einen konsistenten Einzug im gesamten `.magento.env.yaml` -Datei oder Ihre Konfiguration funktioniert möglicherweise nicht wie erwartet. Die Beispiele in der Dokumentation und in der Beispieldatei verwenden _zwei Leerzeichen_ Einzug. Verwenden Sie die [ece-tools validate, Befehl](#validate-configuration-file) , um Ihre Konfiguration zu überprüfen.

## Dateistruktur

Die `.magento.env.yaml` -Datei enthält zwei Abschnitte: `stage` und `log`. Die `stage` -Abschnitt steuert Aktionen, die in den Phasen der [Cloud-Implementierungsprozess](../deploy/process.md).

- `stage`—Verwenden Sie den Abschnitt &quot;Staging&quot;, um bestimmte Aktionen für die folgenden Phasen der Bereitstellung zu definieren:
   - `global`—Steuert Aktionen sowohl in der Build- als auch in der Bereitstellungsphase und nach der Bereitstellung. Sie können diese Einstellungen in den Abschnitten &quot;Build&quot;, &quot;Bereitstellung&quot;und &quot;Nach der Bereitstellung&quot;überschreiben.
   - `build`—Steuert nur Aktionen in der Build-Phase. Wenn Sie in diesem Abschnitt keine Einstellungen angeben, verwendet die Build-Phase die Einstellungen aus dem globalen Abschnitt.
   - `deploy`—Steuert nur Aktionen in der Bereitstellungsphase. Wenn Sie in diesem Abschnitt keine Einstellungen angeben, verwendet die Bereitstellungsphase Einstellungen aus dem globalen Abschnitt.
   - `post-deploy`—Steuerelemente _after_ Bereitstellen der Anwendung und _after_ der Container beginnt, Verbindungen zu akzeptieren.
- `log`—Konfigurieren Sie den Protokollabschnitt. [Benachrichtigungen](set-up-notifications.md), einschließlich Benachrichtigungstypen und Detailebene.
   - `slack`—Konfigurieren Sie eine Nachricht, die an einen Slack-Bot gesendet werden soll.
   - `email`—Konfigurieren Sie eine E-Mail für den Versand an einen oder mehrere E-Mail-Empfänger.
   - [Protokollhandler](log-handlers.md)—Konfigurieren Sie Hardware- und Softwareanwendungsmeldungen, die an einen Remote-Protokollierungsserver gesendet werden.

### Umgebungsvariablen

Die `ece-tools` -Paket legt Werte in der `env.php` Datei basierend auf Werten aus [Cloud-Variablen](variables-cloud.md), Variablen, die in der Variablen [!DNL Cloud Console]und die `.magento.env.yaml` Konfigurationsdatei. Die Umgebungsvariablen in der `.magento.env.yaml` die Cloud-Umgebung durch Überschreiben Ihrer bestehenden Commerce-Konfiguration anpassen. Wenn der Standardwert `Not Set`, dann die `ece-tools` Paket akzeptiert **NO** und verwendet die [!DNL Commerce] Standardwert oder der Wert aus der MAGENTO_CLOUD_RELATIONSHIPS-Konfiguration. Wenn der Standardwert festgelegt ist, wird die `ece-tools` -Paket verwendet, um diesen Standardwert festzulegen.

Die folgenden Themen enthalten detaillierte Definitionen aller Variablen, die Sie in der Variablen `.magento.env.yaml` Datei:

- [Global](variables-global.md)—Variablen steuern Aktionen in jeder Phase: Erstellen, Bereitstellen und Nach der Bereitstellung
- [Build](variables-build.md)—variables steuern Build-Aktionen
- [Bereitstellen](variables-deploy.md)—variables control deploy actions
- [Nach der Bereitstellung](variables-post-deploy.md)—variables steuern Aktionen nach der Bereitstellung

### Konfigurationsdatei über CLI erstellen

Sie können eine `.magento.env.yaml` Konfigurationsdatei für eine Cloud-Umgebung mithilfe der folgenden `ece-tools` Befehle.

>Erstellt eine Konfigurationsdatei

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Aktualisieren von Werten in der Konfigurationsdatei

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Beide Befehle erfordern ein einzelnes Argument: ein JSON-formatiertes Array, das einen Wert für mindestens eine Build-, Bereitstellungs- oder Post-deploy-Variable angibt. Beispielsweise setzt der folgende Befehl Werte für die `SCD_THREADS` und `CLEAN_STATIC_FILES` Variablen:

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

Und erstellt eine `.magento.env.yaml` -Datei mit den folgenden Einstellungen:

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

Sie können die `cloud:config:update` -Befehl, um die neue Datei zu aktualisieren. Der folgende Befehl ändert beispielsweise die `SCD_THREADS` Wert und fügt die `SCD_COMPRESSION_TIMEOUT` Konfiguration:

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

Verwenden Sie Folgendes `ece-tools` -Befehl zum Validieren der `.magento.env.yaml` Konfigurationsdatei vor dem Übertragen der Änderungen in die Remote-Cloud-Umgebung.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

Die folgende Beispielantwort enthält eine Liste der zu korrigierenden Elemente:

```terminal
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP-Konstanten

Sie können PHP-Konstanten in `.magento.env.yaml` Dateidefinitionen anstelle von Hartkodierungswerten. Im folgenden Beispiel wird die `driver_options` Verwendung einer PHP-Konstante:

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
>Die konstante Analyse funktioniert nicht bei Verwendung einer `symfony/yaml` Paketversion vor 3.2.

## Umgang mit Fehlern

Wenn ein Fehler aufgrund eines unerwarteten Werts im `.magento.env.yaml` Konfigurationsdatei erstellen, erhalten Sie eine Fehlermeldung. Beispielsweise enthält die folgende Fehlermeldung eine Liste der vorgeschlagenen Änderungen an jedem Element mit einem unerwarteten Wert und manchmal gültige Optionen:

```terminal
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

Wenn Sie Configuration Management nach dem Ablegen der Konfigurationen aktiviert haben, sollten Sie die SCD_*-Variablen aus der Bereitstellung in die Build-Phase verschieben. Siehe [Implementierungsstrategien für statische Inhalte](../deploy/static-content.md).

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
