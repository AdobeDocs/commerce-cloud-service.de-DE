---
source-git-commit: 63c86bab0f3feb5a3a641a7a785ea625338045f4
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---
# ece-tools

**Version**: 2002.2.0

Diese Referenz enthält 34 Befehle, die über das Befehlszeilen-Tool `ece-tools` verfügbar sind.
Die anfängliche Liste wird mithilfe des Befehls `ece-tools list` in Adobe Commerce in der Cloud-Infrastruktur automatisch generiert.

## Allgemein

Diese Referenz wird aus der Anwendungs-Codebase generiert. Um den Inhalt zu ändern, geben Sie uns Feedback _(suchen Sie den Link oben rechts)._ Beitragsrichtlinien finden Sie unter [Codebeiträge](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

### Globale Optionen

#### `--help`, `-h`

Zeigen Sie Hilfe für den angegebenen Befehl an. Wenn kein Befehl angegeben wird, wird die Hilfe zum Listenbefehl angezeigt

- Standard: `false`
- Akzeptiert keinen Wert

#### `--quiet`, `-q`

Keine Nachricht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

#### `--verbose`, `-v|-vv|-vvv`

Erhöhen Sie die Ausführlichkeit der Nachrichten: 1 für die normale Ausgabe, 2 für die ausführlichere Ausgabe und 3 für die Fehlerbehebung.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--ansi`

ANSI-Ausgabe erzwingen (oder deaktivieren —no-ansi)

- Akzeptiert keinen Wert

#### `--no-ansi`

Die Option &quot;—ansi&quot;umkehren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-interaction`, `-n`

Interaktive Fragen stellen

- Standard: `false`
- Akzeptiert keinen Wert


## `_complete`

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

Interner Befehl zum Bereitstellen von Vorschlägen zur Shell-Fertigstellung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--shell`, `-s`

Der Shell-Typ (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Erfordert einen Wert

#### `--input`, `-i`

Ein Array von Eingabe-Token (z. B. COMP_WORDS oder argv)

- Standard: `[]`
- Erfordert einen Wert

#### `--current`, `-c`

Der Index des &quot;input&quot;-Arrays, in dem sich der Cursor befindet (z. B. COMP_CWORD)

- Erfordert einen Wert

#### `--api-version`, `-a`

Die API-Version des Fertigstellungsskripts

- Erfordert einen Wert

#### `--symfony`, `-S`

veraltet

- Erfordert einen Wert


## `build`

```bash
ece-tools build
```

Erstellt eine Anwendung.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `completion`

```bash
ece-tools completion [--debug] [--] [<shell>]
```

Dump des Shell-Fertigstellungsskripts

```
The completion command dumps the shell completion script required
to use shell autocompletion (currently, bash, fish, zsh completion are supported).

Static installation
-------------------

Dump the script to a global completion file and restart your shell:

    bin/ece-tools completion  | sudo tee /etc/bash_completion.d/ece-tools

Or dump the script to a local file and source it:

    bin/ece-tools completion  > completion.sh

    # source the file whenever you use the project
    source completion.sh

    # or add this line at the end of your "~/.bashrc" file:
    source /path/to/completion.sh

Dynamic installation
--------------------

Add this to the end of your shell configuration file (e.g. "~/.bashrc"):

    eval "$(/var/jenkins/workspace/gendocs-ece-tools-cli/bin/ece-tools completion )"
```

### Argumente

#### `shell`

Der Shell-Typ (z. B. &quot;bash&quot;), der Wert der env var &quot;$SHELL&quot; wird verwendet, wenn dies nicht angegeben wird.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--debug`

Fertigstellungs-Debug-Protokoll verfolgen

- Standard: `false`
- Akzeptiert keinen Wert


## `db-dump`

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```

Erstellt Datenbanksicherungen.

### Argumente

#### `databases`

Datenbanken zur Sicherung. Verfügbare Werte: [ Hauptquotenverkäufe]. Wenn der Argumentwert nicht angegeben ist, werden Datenbanksicherungen mit den Anmeldeinformationen erstellt, die in der Umgebungsvariablen `MAGENTO_CLOUD_RELATIONSHIP` oder/und der Eigenschaft `stage.deploy.DATABASE_CONFIGURATION` der Konfigurationsdatei .magento.env.yaml gespeichert sind.

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--remove-definers`, `-d`

Entfernen von Definitionen aus der Datenbank-Dump

- Standard: `false`
- Akzeptiert keinen Wert

#### `--dump-directory`, `-a`

Verwenden Sie ein alternatives Verzeichnis zum Speichern des Dump

- Erfordert einen Wert


## `deploy`

```bash
ece-tools deploy
```

Stellt die Anwendung bereit.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `help`

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```

Hilfe für einen Befehl anzeigen

```
The help command displays help for a given command:

  bin/ece-tools help list

You can also output the help in other formats by using the --format option:

  bin/ece-tools help --format=xml list

To display the list of available commands, please use the list command.
```

### Argumente

#### `command_name`

Der Befehlsname

- Standard: `help`

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat (txt, xml, json oder md)

- Standard: `txt`
- Erfordert einen Wert

#### `--raw`

Ausgabe der Rohbefehl-Hilfe

- Standard: `false`
- Akzeptiert keinen Wert


## `list`

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```

Listen-Befehle

```
The list command lists all commands:

  bin/ece-tools list

You can also display the commands for a specific namespace:

  bin/ece-tools list test

You can also output the information in other formats by using the --format option:

  bin/ece-tools list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  bin/ece-tools list --raw
```

### Argumente

#### `namespace`

Der Namespace-Name

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--raw`

So geben Sie die unformatierte Befehlsliste aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat (txt, xml, json oder md)

- Standard: `txt`
- Erfordert einen Wert

#### `--short`

Überspringen der Beschreibung der Befehlsargumente

- Standard: `false`
- Akzeptiert keinen Wert


## `patch`

```bash
ece-tools patch
```

Wendet benutzerdefinierte Patches an.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `post-deploy`

```bash
ece-tools post-deploy
```

Führt nach Bereitstellungsvorgängen aus.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `run`

```bash
ece-tools run <scenario>...
```

Führen Sie Szenarien aus.

### Argumente

#### `scenario`

Szenario(e)

- Standard: `[]`
- Erforderlich

- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `backup:list`

```bash
ece-tools backup:list
```

Zeigt die Liste der Backup-Dateien an.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `backup:restore`

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

Wiederherstellen wichtiger Konfigurationsdateien. Führen Sie backup:list aus, um die Liste der Backup-Dateien anzuzeigen.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--force`, `-f`

Vorhandene Dateien beim Wiederherstellen einer Sicherung überschreiben

- Standard: `false`
- Akzeptiert keinen Wert

#### `--file`

Ein bestimmter Dateiwiederherstellungspfad

- Akzeptiert einen Wert


## `build:generate`

```bash
ece-tools build:generate
```

Generiert alle erforderlichen Dateien für die Build-Phase.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `build:transfer`

```bash
ece-tools build:transfer
```

Sendet generierte Dateien in das Init-Verzeichnis.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cloud:config:create`

```bash
ece-tools cloud:config:create <configuration>
```

Erstellt eine `.magento.env.yaml` -Datei mit der angegebenen Variablenkonfiguration für Build, Bereitstellung und Bereitstellung. Überschreibt alle vorhandenen `.magento,.env.yaml` -Dateien.

### Argumente

#### `configuration`

Konfiguration im JSON-Format

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cloud:config:update`

```bash
ece-tools cloud:config:update <configuration>
```

Aktualisiert die vorhandene `.magento.env.yaml` -Datei mit der angegebenen Konfiguration. Erstellt `.magento.env.yaml` -Datei, falls sie nicht vorhanden ist.

### Argumente

#### `configuration`

Konfiguration im JSON-Format

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cloud:config:validate`

```bash
ece-tools cloud:config:validate
```

Validiert die Konfigurationsdatei `.magento.env.yaml`

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `config:dump`

```bash
ece-tools config:dumpdump
```

Dump-Konfiguration für die Bereitstellung statischer Inhalte.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cron:disable`

```bash
ece-tools cron:disable
```

Deaktivieren Sie alle Magento-Cron-Prozesse und beenden Sie alle laufenden Prozesse.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cron:enable`

```bash
ece-tools cron:enable
```

Aktiviert Magento-Cron-Prozesse.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cron:kill`

```bash
ece-tools cron:kill
```

Beendet alle Magento-Cron-Prozesse.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `cron:unlock`

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

Entsperren Sie Cron-Aufträge, die im Status &quot;Wird ausgeführt&quot;blieben.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--job-code`

Cron-Auftragscode zum Entsperren.

- Standard: `[]`
- Akzeptiert mehrere Werte


## `dev:generate:schema-error`

```bash
ece-tools dev:generate:schema-error
```

Generiert die Datei dist/error-codes.md aus der Datei schema.error.yaml .

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `dev:git:update-composer`

```bash
ece-tools dev:git:update-composer
```

Aktualisiert den Composer für die Bereitstellung von Git.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `env:config:show`

```bash
ece-tools env:config:show [<variable>...]
```

Zeigt kodierte Cloud-Konfigurationsumgebungsvariablen an.

### Argumente

#### `variable`

Anzuzeigende Umgebungsvariablen, mögliche Optionen: Dienste, Routen, Variablen

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `error:show`

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```

Zeigt Informationen zu Fehlern nach Fehler-ID oder Informationen zu allen Fehlern der letzten Bereitstellung an.

### Argumente

#### `error-code`

Fehlercode, wenn der Befehl nicht übergeben wurde, zeigt Informationen zu allen Fehlern aus der letzten Implementierung an

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--json`, `-j`

Wird verwendet, um Ergebnisse im JSON-Format zu erhalten

- Standard: `false`
- Akzeptiert keinen Wert


## `module:refresh`

```bash
ece-tools module:refresh
```

Aktualisiert die Konfiguration, um neu hinzugefügte Module zu aktivieren.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `schema:generate`

```bash
ece-tools schema:generate
```

Generiert die *.dist-Schemadatei.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:ideal-state`

```bash
ece-tools wizard:ideal-state
```

Überprüft den idealen Konfigurationsstatus.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:master-slave`

```bash
ece-tools wizard:master-slave
```

Überprüft die Master-Slave-Konfiguration.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:scd-on-build`

```bash
ece-tools wizard:scd-on-build
```

Überprüft die SCD bei der Build-Konfiguration.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:scd-on-demand`

```bash
ece-tools wizard:scd-on-demand
```

Überprüft die Konfiguration von SCD bei Bedarf.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:scd-on-deploy`

```bash
ece-tools wizard:scd-on-deploy
```

Überprüft die SCD bei der Bereitstellungskonfiguration.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `wizard:split-db-state`

```bash
ece-tools wizard:split-db-state
```

Überprüft die Möglichkeit, DB aufzuteilen und ob DB bereits geteilt wurde oder nicht.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).
