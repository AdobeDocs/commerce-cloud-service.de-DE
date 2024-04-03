---
source-git-commit: 28aaae20fa03f31107bcd3fb569350a68842b152
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**Version**: 2002.1.14

Diese Referenz enthält 32 Befehle, die über das `ece-tools` Befehlszeilen-Tool.
Die anfängliche Liste wird automatisch mit der Variablen `ece-tools list` in Adobe Commerce in der Cloud-Infrastruktur.

>[!NOTE]
>
>Diese Referenz wird aus der Anwendungs-Codebase generiert. Um den Inhalt zu ändern, können Sie den Quellcode für die entsprechende Befehlsimplementierung im [codebase](https://github.com/magento/magento-cloud-cli) Repository erstellen und Ihre Änderungen zur Überprüfung einreichen. Eine andere Möglichkeit ist, _Feedback geben_ (finden Sie den Link oben rechts). Beitragsrichtlinien finden Sie unter [Codebeiträge](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `build`

Erstellt eine Anwendung.

```bash
ece-tools build
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `db-dump`

Erstellt Datenbanksicherungen.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Datenbanken zur Sicherung. Verfügbare Werte: [Haupt-Anführungsverkäufe]. Wenn der Argumentwert nicht angegeben ist, werden Datenbanksicherungen mit den im `MAGENTO_CLOUD_RELATIONSHIP` Umgebungsvariable oder/und `stage.deploy.DATABASE_CONFIGURATION` -Eigenschaft der Konfigurationsdatei .magento.env.yaml .

- Standard: `[]`

- Array

### `--remove-definers`, `-d`

Entfernen von Definitionen aus der Datenbank-Dump

- Standard: `false`
- Akzeptiert keinen Wert

### `--dump-directory`, `-a`

Verwenden Sie ein alternatives Verzeichnis zum Speichern des Dump

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `deploy`

Stellt die Anwendung bereit.

```bash
ece-tools deploy
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `help`

Hilfe für einen Befehl anzeigen

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Der Befehlsname

- Standard: `help`


### `--format`

Das Ausgabeformat (txt, xml, json oder md)

- Standard: `txt`
- Erfordert einen Wert

### `--raw`

Ausgabe der Rohbefehl-Hilfe

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `list`

Listen-Befehle

```bash
ece-tools list [--raw] [--format FORMAT] [--] [<namespace>]
```


### `namespace`

Der Namespace-Name


### `--raw`

So geben Sie die unformatierte Befehlsliste aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat (txt, xml, json oder md)

- Standard: `txt`
- Erfordert einen Wert


## `patch`

Wendet benutzerdefinierte Patches an.

```bash
ece-tools patch
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `post-deploy`

Führt nach Bereitstellungsvorgängen aus.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `run`

Führen Sie Szenarien aus.

```bash
ece-tools run <scenario>...
```


### `scenario`

Szenario(e)

- Standard: `[]`

- Erforderlich
- Array

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `backup:list`

Zeigt die Liste der Backup-Dateien an.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `backup:restore`

Wiederherstellen wichtiger Konfigurationsdateien. Führen Sie backup:list aus, um die Liste der Backup-Dateien anzuzeigen.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Vorhandene Dateien beim Wiederherstellen einer Sicherung überschreiben

- Standard: `false`
- Akzeptiert keinen Wert

### `--file`

Ein bestimmter Dateiwiederherstellungspfad

- Akzeptiert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `build:generate`

Generiert alle erforderlichen Dateien für die Build-Phase.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `build:transfer`

Sendet generierte Dateien in das Init-Verzeichnis.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cloud:config:create`

Erstellt eine `.magento.env.yaml` -Datei mit der angegebenen Build-, Bereitstellungs- und Nachbereitstellungsvariablenkonfiguration. Überschreibt vorhandene `.magento,.env.yaml` -Datei.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Konfiguration im JSON-Format

- Erforderlich

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cloud:config:update`

Aktualisiert vorhandene `.magento.env.yaml` -Datei mit der angegebenen Konfiguration. Erstellt `.magento.env.yaml` , wenn sie nicht vorhanden ist.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Konfiguration im JSON-Format

- Erforderlich

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cloud:config:validate`

Überprüfungen `.magento.env.yaml` Konfigurationsdatei

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `config:dump`

Dump-Konfiguration für die Bereitstellung statischer Inhalte.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cron:disable`

Deaktivieren Sie alle Magento-Cron-Prozesse und beenden Sie alle laufenden Prozesse.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cron:enable`

Aktiviert Magento-Cron-Prozesse.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cron:kill`

Beendet alle Magento-Cron-Prozesse.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `cron:unlock`

Entsperren Sie Cron-Aufträge, die im Status &quot;Wird ausgeführt&quot;blieben.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Cron-Auftragscode zum Entsperren.

- Standard: `[]`
- Akzeptiert mehrere Werte

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `dev:generate:schema-error`

Generiert die Datei dist/error-codes.md aus der Datei schema.error.yaml .

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `dev:git:update-composer`

Aktualisiert den Composer für die Bereitstellung von Git.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `env:config:show`

Zeigt kodierte Cloud-Konfigurationsumgebungsvariablen an.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Anzuzeigende Umgebungsvariablen, mögliche Optionen: Dienste, Routen, Variablen

- Standard: `[]`

- Array

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `error:show`

Zeigt Informationen zu Fehlern nach Fehler-ID oder Informationen zu allen Fehlern der letzten Bereitstellung an.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Fehlercode, wenn der Befehl nicht übergeben wurde, zeigt Informationen zu allen Fehlern aus der letzten Implementierung an


### `--json`, `-j`

Wird verwendet, um Ergebnisse im JSON-Format zu erhalten

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `module:refresh`

Aktualisiert die Konfiguration, um neu hinzugefügte Module zu aktivieren.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `schema:generate`

Generiert die *.dist-Schemadatei.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:ideal-state`

Überprüft den idealen Konfigurationsstatus.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:master-slave`

Überprüft die Master-Slave-Konfiguration.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:scd-on-build`

Überprüft die SCD bei der Build-Konfiguration.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:scd-on-demand`

Überprüft die Konfiguration von SCD bei Bedarf.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:scd-on-deploy`

Überprüft die SCD bei der Bereitstellungskonfiguration.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `wizard:split-db-state`

Überprüft die Möglichkeit, DB aufzuteilen und ob DB bereits geteilt wurde oder nicht.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ansi`

ANSI-Ausgabe erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-ansi`

ANSI-Ausgabe deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert

