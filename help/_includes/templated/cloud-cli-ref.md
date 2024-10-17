---
source-git-commit: 63c86bab0f3feb5a3a641a7a785ea625338045f4
workflow-type: tm+mt
source-wordcount: '13341'
ht-degree: 0%

---
# Magento-Cloud (Adobe Commerce über Cloud-Infrastruktur)

<!-- The template to render with above values -->

**Version**: 1.46.1

Diese Referenz enthält 119 Befehle, die über das Befehlszeilen-Tool `magento-cloud` verfügbar sind.
Die anfängliche Liste wird mithilfe des Befehls `magento-cloud list` in Adobe Commerce in der Cloud-Infrastruktur automatisch generiert.

## Allgemein

Diese Referenz wird aus der Anwendungs-Codebase generiert. Um den Inhalt zu ändern, können Sie den Quellcode für die entsprechende Befehlsimplementierung im Repository [Codebase](https://github.com/magento/magento-cloud-cli) aktualisieren und Ihre Änderungen zur Überprüfung senden. Eine andere Möglichkeit besteht darin, _Feedback geben_ (den Link oben rechts zu finden). Beitragsrichtlinien finden Sie unter [Codebeiträge](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

### Globale Optionen

#### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: MAGENTO_CLOUD_CLI_NO_INTERACTION=1

- Standard: `false`
- Akzeptiert keinen Wert


## `clear-cache`

```bash
magento-cloud magento-cloud cc
```

Löschen des CLI-Cache

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `decode`

```bash
magento-cloud magento-cloud decode [-P|--property PROPERTY] [--] <value>
```

Dekodieren einer kodierten Zeichenfolge wie MAGENTO_CLOUD_VARIABLES

### Argumente

#### `value`

Der zu dekodierende Variablenwert

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die Eigenschaft, die in der -Variablen angezeigt werden soll

- Erfordert einen Wert


## `docs`

```bash
magento-cloud magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```

Öffnen Sie die Online-Dokumentation

### Argumente

#### `search`

Suchbegriff(e)

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

#### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert


## `help`

```bash
magento-cloud magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```

Zeigt Hilfe für einen Befehl an

```
The help command displays help for a given command:

  magento-cloud help list

You can also output the help in other formats by using the --format option:

  magento-cloud help --format=json list

To display the list of available commands, please use the list command.
```

### Argumente

#### `command_name`

Der Befehlsname

- Standard: `help`

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat (txt, json oder md)

- Standard: `txt`
- Erfordert einen Wert

#### `--raw`

Ausgabe der Rohbefehl-Hilfe

- Standard: `false`
- Akzeptiert keinen Wert


## `list`

```bash
magento-cloud magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```

Listet Befehle auf

```
The list command lists all commands:

  magento-cloud list

You can also display the commands for a specific namespace:

  magento-cloud list project

You can also output the information in other formats by using the --format option:

  magento-cloud list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  magento-cloud list --raw
```

### Argumente

#### `command`

Der auszuführende Befehl

- Erforderlich


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

#### `--all`

Alle Befehle anzeigen, einschließlich ausgeblendeter Befehle

- Standard: `false`
- Akzeptiert keinen Wert


## `multi`

```bash
magento-cloud magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```

Ausführen eines Befehls für mehrere Projekte

### Argumente

#### `cmd`

Der auszuführende Befehl

- Standard: `[]`
- Erforderlich

- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--projects`, `-p`

Eine Liste der Projekt-IDs, durch Kommas und/oder Leerzeichen getrennt

- Erfordert einen Wert

#### `--continue`

Fahren Sie mit der Ausführung von Befehlen fort, selbst wenn eine Ausnahme aufgetreten ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--sort`

Eine Eigenschaft zum Sortieren der Liste der Projektoptionen

- Standard: `title`
- Erfordert einen Wert

#### `--reverse`

Reihenfolge der Projektoptionen umkehren

- Standard: `false`
- Akzeptiert keinen Wert


## `web`

```bash
magento-cloud magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Öffnen Sie das Projekt in der Web-Benutzeroberfläche

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

#### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `activity:cancel`

```bash
magento-cloud magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Aktivität abbrechen

### Argumente

#### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste stornierbare Aktivität.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `activity:get`

```bash
magento-cloud magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```

Detaillierte Informationen zu einer einzelnen Aktivität anzeigen

### Argumente

#### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Aktivität.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

#### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--state`

Filtern nach Status (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder cancelled. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

#### `--incomplete`, `-i`

Schließen Sie nur unvollständige Aktivitäten ein (bei Auswahl einer Standardaktivität). Dies ist eine Kurzanleitung für —state=in_progress,pending

- Standard: `false`
- Akzeptiert keinen Wert

#### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `activity:list`

```bash
magento-cloud magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Liste der Aktivitäten für eine Umgebung oder ein Projekt abrufen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--type`, `-t`

Filteraktivitäten nach Typ Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann &quot;cron&quot;Aktivitäten vom Typ &quot;environment.cron&quot;auswählen. Die Zeichen % oder * können als Platzhalter verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`, `-x`

Aktivitäten nach Typ ausschließen Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann &quot;cron&quot;Aktivitäten vom Typ &quot;environment.cron&quot;ausschließen. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

#### `--start`

Es werden nur Aktivitäten aufgelistet, die vor diesem Datum erstellt wurden

- Erfordert einen Wert

#### `--state`

Aktivitäten nach Status filtern: in_progress, pending, complete oder abgebrochen. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--result`

Aktivitäten nach Ergebnis filtern: Erfolg oder Fehler

- Erfordert einen Wert

#### `--incomplete`, `-i`

Nur unvollständige Aktivitäten auflisten

- Standard: `false`
- Akzeptiert keinen Wert

#### `--all`, `-a`

Aktivitäten in allen Umgebungen auflisten

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, created*, description*, progress*, state*, result*, completed, environment, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `activity:log`

```bash
magento-cloud magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Protokoll für eine Aktivität anzeigen

### Argumente

#### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Aktivität.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Intervall für die Aktivitätsaktualisierung (Sekunden). Auf 0 setzen, um die Aktualisierung zu deaktivieren.

- Standard: `3`
- Erfordert einen Wert

#### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--type`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--state`

Filtern nach Status (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder cancelled. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

#### `--incomplete`, `-i`

Schließen Sie nur unvollständige Aktivitäten ein (bei Auswahl einer Standardaktivität). Dies ist eine Kurzanleitung für —state=in_progress,pending

- Standard: `false`
- Akzeptiert keinen Wert

#### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `app:config-get`

```bash
magento-cloud magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

Konfiguration einer App anzeigen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Konfigurationseigenschaft

- Erfordert einen Wert

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--identity-file`, `-i`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert


## `app:list`

```bash
magento-cloud magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Auflisten von Apps im Projekt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--pipe`

Nur Liste mit App-Namen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: name*, type*, disk, path, size (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:api-token-login`

```bash
magento-cloud magento-cloud auth:api-token-login
```

Bei der Magento Cloud über ein API-Token anmelden

```
Use this command to log in to your Magento Cloud account using an API token.

You can create an account at:
    https://business.adobe.com/products/magento/magento-commerce.html

If you have an account, but you do not already have an API token, you can create one here:
    https://accounts.magento.cloud/user/api-tokens

Alternatively, to log in to the CLI with a browser, run:
    magento-cloud auth:browser-login
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `auth:browser-login`

```bash
magento-cloud magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

Bei der Magento Cloud über einen Browser anmelden

```
Use this command to log in to the Magento Cloud CLI using a web browser.

It launches a temporary local website which redirects you to log in if
necessary, and then captures the resulting authorization code.

Your system's default browser will be used. You can override this using the
--browser option.

Alternatively, to log in using an API token (without a browser), run:
magento-cloud auth:api-token-login

To authenticate non-interactively, configure an API token using the
MAGENTO_CLOUD_CLI_TOKEN environment variable.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--force`, `-f`

Melden Sie sich erneut an, auch wenn Sie bereits angemeldet sind

- Standard: `false`
- Akzeptiert keinen Wert

#### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

#### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:info`

```bash
magento-cloud magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```

Kontoinformationen anzeigen

### Argumente

#### `property`

Die anzuzeigende Kontoeigenschaft

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--no-auto-login`

Überspringt die automatische Anmeldung. Wenn Sie nicht angemeldet sind, wird nichts ausgegeben und der Exitcode ist 0, vorausgesetzt, es werden keine anderen Fehler ausgegeben.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--property`, `-P`

Die anzuzeigende Kontoeigenschaft (alternative Syntax)

- Erfordert einen Wert

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:logout`

```bash
magento-cloud magento-cloud logout [-a|--all] [--other]
```

Aus Magento Cloud abmelden

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--all`, `-a`

Abmelden von allen lokalen Sitzungen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--other`

Abmelden von anderen lokalen Sitzungen

- Standard: `false`
- Akzeptiert keinen Wert


## `blackfire:setup`

```bash
magento-cloud magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Einrichten der Blackfire.io-Integration für das Projekt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--server_id`

Server-ID

- Erfordert einen Wert

#### `--server_token`

Server-Token

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:add`

```bash
magento-cloud magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Hinzufügen eines SSL-Zertifikats zum Projekt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--cert`

Der Pfad zur Zertifikatdatei

- Erfordert einen Wert

#### `--key`

Der Pfad zur Datei mit dem privaten Zertifikatschlüssel

- Erfordert einen Wert

#### `--chain`

Der Pfad zur Zertifikatskettendatei

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:delete`

```bash
magento-cloud magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```

Zertifikat aus dem Projekt löschen

### Argumente

#### `id`

Die Zertifikatkennung (oder der Anfang)

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:get`

```bash
magento-cloud magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```

Zertifikat anzeigen

### Argumente

#### `id`

Die Zertifikatkennung (oder der Anfang)

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Zertifikateigenschaft

- Erfordert einen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `certificate:list`

```bash
magento-cloud magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Projektzertifikate auflisten

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--domain`

Filtern nach Domain-Namen (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

- Erfordert einen Wert

#### `--exclude-domain`

Zertifikate ausschließen, die mit dem Domänennamen übereinstimmen (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

- Erfordert einen Wert

#### `--issuer`

Nach Emittenten filtern

- Erfordert einen Wert

#### `--only-auto`

Nur automatisch bereitgestellte Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-auto`

Nur manuell hinzugefügte Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--ignore-expiry`

Sowohl abgelaufene als auch nicht abgelaufene Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--only-expired`

Nur abgelaufene Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-expired`

Nur nicht abgelaufene Zertifikate anzeigen (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--pipe-domains`

Nur eine Liste der Domänennamen zurückgeben, die von den Zertifikaten abgedeckt sind

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: erstellt, Domänen, abgelaufen, ID, Aussteller. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `commit:get`

```bash
magento-cloud magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```

Commit-Details anzeigen

### Argumente

#### `commit`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Standard: `HEAD`

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die angezeigte commit-Eigenschaft.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `commit:list`

```bash
magento-cloud magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```

Auflisten von Commits

### Argumente

#### `commit`

Das Git-Commit-SHA für den Start. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--limit`

Die Anzahl der anzuzeigenden Commits.

- Standard: `10`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: author, date, sha, summary. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `db:dump`

```bash
magento-cloud magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

Lokalen Dump der Remote-Datenbank erstellen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--schema`

Das Schema, das abgelegt werden soll. Unterlassen der Verwendung des Standardschemas (normalerweise &quot;main&quot;).

- Erfordert einen Wert

#### `--file`, `-f`

Ein benutzerdefinierter Dateiname für die Ablage

- Erfordert einen Wert

#### `--directory`, `-d`

Ein benutzerdefiniertes Verzeichnis für den Dump

- Erfordert einen Wert

#### `--gzip`, `-z`

Komprimieren Sie die Ablage mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

#### `--timestamp`, `-t`

Fügen Sie einen Zeitstempel zum Dateinamen der Dump-Datei hinzu.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

#### `--table`

Zu berücksichtigende Tabelle(n)

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-table`

Auszuschließende Tabelle

- Standard: `[]`
- Erfordert einen Wert

#### `--schema-only`

Nur Schemas ablegen, keine Daten

- Standard: `false`
- Akzeptiert keinen Wert

#### `--charset`

Die Zeichensatzkodierung für die Dump

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `db:size`

```bash
magento-cloud magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

Schätzen der Festplattenauslastung einer Datenbank

```
This is an estimate of the database disk usage. The real size on disk is usually higher because of overhead.

To see more accurate disk usage, run: magento-cloud disk
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--bytes`, `-B`

Zeigt Größen in Byte an.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--cleanup`, `-C`

Überprüfen Sie, ob Tabellen bereinigt werden können, und zeigen Sie mir Empfehlungen an (nur InnoDb).

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: max, percent_used, used. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `db:sql`

```bash
magento-cloud magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```

SQL auf der Remote-Datenbank ausführen

### Argumente

#### `query`

Eine auszuführende SQL-Anweisung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--raw`

Rohe, nicht tabellarische Ausgabe erzeugen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--schema`

Das zu verwendende Schema. Unterlassen der Verwendung des Standardschemas (normalerweise &quot;main&quot;). Übergeben Sie eine leere Zeichenfolge, um kein Schema zu verwenden.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `domain:add`

```bash
magento-cloud magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Hinzufügen einer neuen Domäne zum Projekt

### Argumente

#### `name`

Der Domänenname

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--cert`

Der Pfad zur Zertifikatdatei für diese Domäne

- Erfordert einen Wert

#### `--key`

Der Pfad zur privaten Schlüsseldatei für das angegebene Zertifikat.

- Erfordert einen Wert

#### `--chain`

Der Pfad zur Zertifikatskettendatei(en) für das bereitgestellte Zertifikat

- Standard: `[]`
- Erfordert einen Wert

#### `--attach`

Die Produktionsdomäne, die diese in den Routen der Umgebung ersetzt. Erforderlich für Nicht-Produktions-Umgebungsdomänen.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:delete`

```bash
magento-cloud magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Eine Domäne aus dem Projekt löschen

### Argumente

#### `name`

Der Domänenname

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:get`

```bash
magento-cloud magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```

Detaillierte Informationen für eine Domäne anzeigen

### Argumente

#### `name`

Der Domänenname

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Domäneneigenschaft

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `domain:list`

```bash
magento-cloud magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Liste aller Domänen abrufen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: name*, ssl*, created_at*, registered_name, replacement_for, type, updated_at (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `domain:update`

```bash
magento-cloud magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Domain aktualisieren

### Argumente

#### `name`

Der Domänenname

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--cert`

Der Pfad zur Zertifikatdatei für diese Domäne

- Erfordert einen Wert

#### `--key`

Der Pfad zur privaten Schlüsseldatei für das angegebene Zertifikat.

- Erfordert einen Wert

#### `--chain`

Der Pfad zur Zertifikatskettendatei(en) für das bereitgestellte Zertifikat

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:activate`

```bash
magento-cloud magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Aktivieren einer Umgebung

### Argumente

#### `environment`

Zu aktivierende Umgebung(n)

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--parent`

Festlegen einer neuen übergeordneten Umgebung vor der Aktivierung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:branch`

```bash
magento-cloud magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```

Verzweigung einer Umgebung

### Argumente

#### `id`

Die ID (Zweigname) der neuen Umgebung


#### `parent`

Das übergeordnete Element der neuen Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--title`

Der Titel der neuen Umgebung

- Erfordert einen Wert

#### `--type`

Der Typ der neuen Umgebung

- Erfordert einen Wert

#### `--no-clone-parent`

Die Daten der übergeordneten Umgebung nicht klonen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:checkout`

```bash
magento-cloud magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```

Auschecken einer Umgebung

### Argumente

#### `id`

Die ID der Umgebung, die ausgecheckt werden soll. Beispiel: &quot;sprint2&quot;

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `environment:delete`

```bash
magento-cloud magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Löschen einer oder mehrerer Umgebungen

```
When a Magento Cloud environment is deleted, it will become "inactive": it will
exist only as a Git branch, containing code but no services, databases nor
files.

This command allows you to delete environments as well as their Git branches.
```

### Argumente

#### `environment`

Die zu löschenden Umgebungen. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--delete-branch`

Löschen von Git-Zweigen für inaktive Umgebungen ohne Bestätigung

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-delete-branch`

Löschen Sie keine Git-Verzweigungen (inaktive Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--type`

Löschen Sie alle Umgebungen eines Typs (Hinzufügung zu anderen ausgewählten Umgebungen) Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--only-type`, `-t`

Nur Löschumgebungen eines bestimmten Typs Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude`

Umgebung(en), die nicht gelöscht werden soll. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`

Umgebungstypen, deren Werte nicht gelöscht werden sollen, können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--inactive`

Löschen Sie alle inaktiven Umgebungen (Hinzufügung zu allen anderen ausgewählten Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--merged`

Löschen Sie alle zusammengeführten Umgebungen (Hinzufügen zu allen anderen ausgewählten Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--allow-delete-parent`

Löschen von Umgebungen mit untergeordneten Elementen zulassen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:http-access`

```bash
magento-cloud magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Aktualisieren von HTTP-Zugriffseinstellungen für eine Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--access`

Zugriffsbeschränkungen im Format &quot;permission:address&quot;. Verwenden Sie 0, um alle Adressen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

#### `--auth`

HTTP Basic auth credentials im Format &quot;username:password&quot;. Verwenden Sie 0, um alle Berechtigungen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

#### `--enabled`

Ob die Zugriffskontrolle aktiviert werden soll: 1 zur Aktivierung, 0 zur Deaktivierung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:info`

```bash
magento-cloud magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Eigenschaften für eine Umgebung lesen oder festlegen

### Argumente

#### `property`

Der Name der Eigenschaft


#### `value`

Neuen Wert für die Eigenschaft festlegen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:init`

```bash
magento-cloud magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```

Initialisieren einer Umgebung aus einem öffentlichen Git-Repository

### Argumente

#### `url`

Eine URL zum Git-Repository

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--profile`

Der Name des Profils

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:list`

```bash
magento-cloud magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Liste der Umgebungen abrufen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--no-inactive`, `-I`

Inaktive Umgebungen nicht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--pipe`

Geben Sie eine einfache Liste von Umgebungs-IDs aus.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--refresh`

Ob die Liste aktualisiert werden soll.

- Standard: `1`
- Erfordert einen Wert

#### `--sort`

Eine Eigenschaft, die nach

- Standard: `title`
- Erfordert einen Wert

#### `--reverse`

Sortieren in umgekehrter (absteigender) Reihenfolge

- Standard: `false`
- Akzeptiert keinen Wert

#### `--type`

Filtern Sie die Liste nach Umgebungstyp(en). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, status*, type*, created, machine_name, updated (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `environment:logs`

```bash
magento-cloud magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```

Protokolle einer Umgebung lesen

### Argumente

#### `type`

Der Protokolltyp, z. B. &quot;access&quot; oder &quot;error&quot;

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--lines`

Die Anzahl der anzuzeigenden Zeilen

- Standard: `100`
- Erfordert einen Wert

#### `--tail`

Kontinuierliches Verfolgen des Protokolls

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert


## `environment:merge`

```bash
magento-cloud magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Zusammenführen einer Umgebung

```
This command will initiate a Git merge of the specified environment into its parent environment.
```

### Argumente

#### `environment`

Die zusammenzuführende Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:pause`

```bash
magento-cloud magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Anhalten einer Umgebung

```
Pausing an environment helps to reduce resource consumption and carbon emissions.

The environment will be unavailable until it is resumed. No data will be lost.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:push`

```bash
magento-cloud magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```

Push-Code in eine Umgebung

### Argumente

#### `source`

Die Quell-Referenz: ein Zweigname oder Commit-Hash

- Standard: `HEAD`

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--target`

Der Name der Zielverzweigung. Die Standardeinstellung ist der aktuelle Zweig.

- Erfordert einen Wert

#### `--force`, `-f`

Nicht-schnelle Aktualisierungen zulassen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--force-with-lease`

Nicht-schnelle Aktualisierungen zulassen, wenn die Remote-Tracking-Verzweigung auf dem neuesten Stand ist

- Standard: `false`
- Akzeptiert keinen Wert

#### `--set-upstream`, `-u`

Legen Sie die Zielumgebung als Upstream für die Quellverzweigung fest. Dadurch wird auch das Zielprojekt als Remote für das lokale Repository festgelegt.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--activate`

Aktivieren der Umgebung vor dem Pushen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--parent`

Festlegen der neuen übergeordneten Umgebung (nur mit —activate verwendet)

- Erfordert einen Wert

#### `--type`

Umgebungstyp festlegen (nur mit —activate verwendet)

- Erfordert einen Wert

#### `--no-clone-parent`

Klonen Sie nicht die Daten des übergeordneten Zweigs (nur mit —activate verwendet)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `environment:redeploy`

```bash
magento-cloud magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Bereitstellung einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:relationships`

```bash
magento-cloud magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```

Anzeigen der Beziehungen einer Umgebung

### Argumente

#### `environment`

Umwelt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Beziehungseigenschaft

- Erfordert einen Wert

#### `--refresh`

Ob die Beziehungen aktualisiert werden sollen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `environment:resume`

```bash
magento-cloud magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Fortsetzen einer angehaltenen Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:scp`

```bash
magento-cloud magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```

Kopieren von Dateien in und aus einer Umgebung mithilfe von scp

### Argumente

#### `files`

Zu kopierende Dateien. Verwenden Sie das Präfix remote: , um Remote-Standorte zu definieren.

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--recursive`, `-r`

rekursiv ganze Verzeichnisse kopieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `environment:ssh`

```bash
magento-cloud magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```

SSH in die aktuelle Umgebung

### Argumente

#### `cmd`

Ein Befehl zum Ausführen in der Umgebung.

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--pipe`

Geben Sie nur die SSH-URL aus.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--all`

Geben Sie alle SSH-URLs (für jede App) aus.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `environment:synchronize`

```bash
magento-cloud magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```

Synchronisieren des Codes und/oder der Daten einer Umgebung von der übergeordneten Umgebung

```
This command synchronizes to a child environment from its parent environment.

Synchronizing "code" means there will be a Git merge from the parent to the
child. Synchronizing "data" means that all files in all services (including
static files, databases, logs, search indices, etc.) will be copied from the
parent to the child.
```

### Argumente

#### `synchronize`

Was synchronisiert werden soll: &quot;code&quot;, &quot;data&quot; oder beides

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--rebase`

Synchronisieren Sie den Code durch Rebasing anstelle der Zusammenführung.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:url`

```bash
magento-cloud magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Abrufen der öffentlichen URLs einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--primary`, `-1`

Gibt nur die URL für die primäre Route zurück

- Standard: `false`
- Akzeptiert keinen Wert

#### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

#### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `environment:xdebug`

```bash
magento-cloud magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

Öffnen Sie einen Tunnel zu Xdebug in der Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--port`

Der lokale Port

- Standard: `9000`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `integration:activity:get`

```bash
magento-cloud magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```

Detaillierte Informationen zu einer einzelnen Integrationsaktivität anzeigen

### Argumente

#### `integration`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


#### `activity`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Integrationsaktivität.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `integration:activity:list`

```bash
magento-cloud magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Liste der Aktivitäten für eine Integration abrufen

### Argumente

#### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--type`

Aktivitäten nach Typ filtern Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--exclude-type`, `-x`

Aktivitäten nach Typ ausschließen Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

#### `--start`

Es werden nur Aktivitäten aufgelistet, die vor diesem Datum erstellt wurden

- Erfordert einen Wert

#### `--state`

Filtern von Aktivitäten nach Status. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--result`

Aktivitäten nach Ergebnis filtern

- Erfordert einen Wert

#### `--incomplete`, `-i`

Nur unvollständige Aktivitäten auflisten

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, created*, description*, type*, state*, result*, completed (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert


## `integration:activity:log`

```bash
magento-cloud magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```

Protokoll für eine Integrationsaktivität anzeigen

### Argumente

#### `integration`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


#### `activity`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Integrationsaktivität.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert


## `integration:add`

```bash
magento-cloud magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Hinzufügen einer Integration zum Projekt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--type`

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;.

- Erfordert einen Wert

#### `--base-url`

Die Basis-URL der Serverinstallation

- Erfordert einen Wert

#### `--bitbucket-url`

Die Basis-URL der Bitbucket Server-Installation

- Erfordert einen Wert

#### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

#### `--token`

Ein Authentifizierungs- oder Zugriffstoken für die Integration

- Erfordert einen Wert

#### `--key`

Ein Bitbucket OAuth-Verbraucherschlüssel

- Erfordert einen Wert

#### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

#### `--license-key`

Der New Relic Logs-Lizenzschlüssel

- Erfordert einen Wert

#### `--server-project`

Das Projekt (z. B. &quot;namespace/repo&quot;)

- Erfordert einen Wert

#### `--repository`

Das zu verfolgende Repository (z. B. &quot;owner/repository&quot;)

- Erfordert einen Wert

#### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

#### `--build-pull-requests`

Erstellen jeder Pull-Anforderung als Umgebung

- Standard: `true`
- Erfordert einen Wert

#### `--build-draft-pull-requests`

Erstellen von Entwurfs-Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

#### `--build-pull-requests-post-merge`

Pull-Anforderungen basierend auf ihrem Postzusammenführungsstatus erstellen

- Standard: `false`
- Erfordert einen Wert

#### `--build-wip-merge-requests`

GitLab: WIP-Zusammenführungsanfragen erstellen

- Standard: `true`
- Erfordert einen Wert

#### `--merge-requests-clone-parent-data`

GitLab: Daten für Zusammenführungsanfragen klonen

- Standard: `true`
- Erfordert einen Wert

#### `--pull-requests-clone-parent-data`

Daten der übergeordneten Umgebung für Pull-Anforderungen klonen

- Standard: `true`
- Erfordert einen Wert

#### `--resync-pull-requests`

Synchronisieren von Umgebungsdaten für Pull-Anforderungen bei jedem Build

- Standard: `false`
- Erfordert einen Wert

#### `--fetch-branches`

Abrufen aller Zweige aus der Remote-Umgebung (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

#### `--prune-branches`

Löschen von Zweigen, die nicht auf der Remote-Site vorhanden sind

- Standard: `true`
- Erfordert einen Wert

#### `--resources-init`

Die Ressourcen, die beim Initialisieren eines neuen Dienstes verwendet werden sollen (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Erfordert einen Wert

#### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

#### `--shared-key`

Webhook: der gemeinsame JWS-geheime Schlüssel

- Erfordert einen Wert

#### `--file`

Der Name einer lokalen Datei mit dem hochzuladenden Skript

- Erfordert einen Wert

#### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

#### `--states`

Eine Liste der Status, auf die reagiert werden soll, z. B. ausstehend, in_progress, complete

- Standard: `complete`
- Erfordert einen Wert

#### `--environments`

Die einzuschließenden Umgebungs-IDs

- Standard: `*`
- Erfordert einen Wert

#### `--excluded-environments`

Die auszuschließenden Umgebungs-IDs

- Standard: `[]`
- Erfordert einen Wert

#### `--from-address`

[Optional] Benutzerdefinierte Absenderadresse für Warnhinweis-E-Mails

- Erfordert einen Wert

#### `--recipients`

Die E-Mail-Adresse(n) des Empfängers

- Standard: `[]`
- Erfordert einen Wert

#### `--channel`

Der Slack-Kanal

- Erfordert einen Wert

#### `--routing-key`

Der PagerDuty-Routing-Schlüssel

- Erfordert einen Wert

#### `--category`

Die Kategorie Sumo Logic , die zum Filtern verwendet wird

- Erfordert einen Wert

#### `--index`

Splunk-Index

- Erfordert einen Wert

#### `--sourcetype`

Splunk-Ereignistyp

- Erfordert einen Wert

#### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

#### `--syslog-host`

Syslog-Relais/Collector-Host

- Erfordert einen Wert

#### `--syslog-port`

Syslog Relais/Collector Port

- Erfordert einen Wert

#### `--facility`

Syslog-Einrichtung

- Standard: `1`
- Erfordert einen Wert

#### `--message-format`

Syslog-Nachrichtenformat (&#39;rfc3164&#39; oder &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Erfordert einen Wert

#### `--auth-mode`

Authentifizierungsmodus (&#39;prefix&#39; oder &#39;structured_data&#39;)

- Standard: `prefix`
- Erfordert einen Wert

#### `--auth-token`

Authentifizierungstoken

- Erfordert einen Wert

#### `--verify-tls`

Ob die HTTPS-Zertifikatüberprüfung aktiviert werden soll (empfohlen)

- Standard: `true`
- Erfordert einen Wert

#### `--header`

HTTP-Header zur Verwendung in POST-Anfragen. Trennen Sie Namen und Werte durch einen Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:delete`

```bash
magento-cloud magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Integration aus einem Projekt löschen

### Argumente

#### `id`

Die Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:get`

```bash
magento-cloud magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```

Details einer Integration anzeigen

### Argumente

#### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Integrationseigenschaft

- Akzeptiert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `integration:list`

```bash
magento-cloud magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Liste der Projektintegration(n) anzeigen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: ID, Zusammenfassung, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `integration:update`

```bash
magento-cloud magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Integration aktualisieren

### Argumente

#### `id`

Die ID der zu aktualisierenden Integration

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--type`

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;.

- Erfordert einen Wert

#### `--base-url`

Die Basis-URL der Serverinstallation

- Erfordert einen Wert

#### `--bitbucket-url`

Die Basis-URL der Bitbucket Server-Installation

- Erfordert einen Wert

#### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

#### `--token`

Ein Authentifizierungs- oder Zugriffstoken für die Integration

- Erfordert einen Wert

#### `--key`

Ein Bitbucket OAuth-Verbraucherschlüssel

- Erfordert einen Wert

#### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

#### `--license-key`

Der New Relic Logs-Lizenzschlüssel

- Erfordert einen Wert

#### `--server-project`

Das Projekt (z. B. &quot;namespace/repo&quot;)

- Erfordert einen Wert

#### `--repository`

Das zu verfolgende Repository (z. B. &quot;owner/repository&quot;)

- Erfordert einen Wert

#### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

#### `--build-pull-requests`

Erstellen jeder Pull-Anforderung als Umgebung

- Standard: `true`
- Erfordert einen Wert

#### `--build-draft-pull-requests`

Erstellen von Entwurfs-Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

#### `--build-pull-requests-post-merge`

Pull-Anforderungen basierend auf ihrem Postzusammenführungsstatus erstellen

- Standard: `false`
- Erfordert einen Wert

#### `--build-wip-merge-requests`

GitLab: WIP-Zusammenführungsanfragen erstellen

- Standard: `true`
- Erfordert einen Wert

#### `--merge-requests-clone-parent-data`

GitLab: Daten für Zusammenführungsanfragen klonen

- Standard: `true`
- Erfordert einen Wert

#### `--pull-requests-clone-parent-data`

Daten der übergeordneten Umgebung für Pull-Anforderungen klonen

- Standard: `true`
- Erfordert einen Wert

#### `--resync-pull-requests`

Synchronisieren von Umgebungsdaten für Pull-Anforderungen bei jedem Build

- Standard: `false`
- Erfordert einen Wert

#### `--fetch-branches`

Abrufen aller Zweige aus der Remote-Umgebung (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

#### `--prune-branches`

Löschen von Zweigen, die nicht auf der Remote-Site vorhanden sind

- Standard: `true`
- Erfordert einen Wert

#### `--resources-init`

Die Ressourcen, die beim Initialisieren eines neuen Dienstes verwendet werden sollen (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Erfordert einen Wert

#### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

#### `--shared-key`

Webhook: der gemeinsame JWS-geheime Schlüssel

- Erfordert einen Wert

#### `--file`

Der Name einer lokalen Datei mit dem hochzuladenden Skript

- Erfordert einen Wert

#### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

#### `--states`

Eine Liste der Status, auf die reagiert werden soll, z. B. ausstehend, in_progress, complete

- Standard: `complete`
- Erfordert einen Wert

#### `--environments`

Die einzuschließenden Umgebungs-IDs

- Standard: `*`
- Erfordert einen Wert

#### `--excluded-environments`

Die auszuschließenden Umgebungs-IDs

- Standard: `[]`
- Erfordert einen Wert

#### `--from-address`

[Optional] Benutzerdefinierte Absenderadresse für Warnhinweis-E-Mails

- Erfordert einen Wert

#### `--recipients`

Die E-Mail-Adresse(n) des Empfängers

- Standard: `[]`
- Erfordert einen Wert

#### `--channel`

Der Slack-Kanal

- Erfordert einen Wert

#### `--routing-key`

Der PagerDuty-Routing-Schlüssel

- Erfordert einen Wert

#### `--category`

Die Kategorie Sumo Logic , die zum Filtern verwendet wird

- Erfordert einen Wert

#### `--index`

Splunk-Index

- Erfordert einen Wert

#### `--sourcetype`

Splunk-Ereignistyp

- Erfordert einen Wert

#### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

#### `--syslog-host`

Syslog-Relais/Collector-Host

- Erfordert einen Wert

#### `--syslog-port`

Syslog Relais/Collector Port

- Erfordert einen Wert

#### `--facility`

Syslog-Einrichtung

- Standard: `1`
- Erfordert einen Wert

#### `--message-format`

Syslog-Nachrichtenformat (&#39;rfc3164&#39; oder &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Erfordert einen Wert

#### `--auth-mode`

Authentifizierungsmodus (&#39;prefix&#39; oder &#39;structured_data&#39;)

- Standard: `prefix`
- Erfordert einen Wert

#### `--auth-token`

Authentifizierungstoken

- Erfordert einen Wert

#### `--verify-tls`

Ob die HTTPS-Zertifikatüberprüfung aktiviert werden soll (empfohlen)

- Standard: `true`
- Erfordert einen Wert

#### `--header`

HTTP-Header zur Verwendung in POST-Anfragen. Trennen Sie Namen und Werte durch einen Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:validate`

```bash
magento-cloud magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```

Bestehende Integration validieren

```
This command allows you to check whether an integration is valid.

An exit code of 0 means the integration is valid, while 4 means it is invalid.
Any other exit code indicates an unexpected error.

Integrations are validated automatically on creation and on update. However,
because they involve external resources, it is possible for a valid integration
to become invalid. For example, an access token may be revoked, or an external
repository may be deleted.
```

### Argumente

#### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `local:build`

```bash
magento-cloud magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```

Aktuelles Projekt lokal erstellen

### Argumente

#### `app`

Zu erstellende Anwendung(en) angeben

- Standard: `[]`
- Array

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--abslinks`, `-a`

Absolute Links verwenden

- Standard: `false`
- Akzeptiert keinen Wert

#### `--source`, `-s`

Das Quellverzeichnis. Die Standardeinstellung ist der aktuelle Projektstamm.

- Erfordert einen Wert

#### `--destination`, `-d`

Das Ziel, mit dem der Webstamm jeder App symverknüpft wird. Standard: _www

- Erfordert einen Wert

#### `--copy`, `-c`

Kopieren Sie in ein Build-Verzeichnis, anstatt symlink aus der Quelle zu verwenden.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--clone`

Verwenden Sie Git, um die aktuelle HEAD in den Build-Ordner zu klonen.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--run-deploy-hooks`

Ausführen von &quot;deploy&quot;und/oder &quot;post_deploy&quot;

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-clean`

Alte Builds nicht entfernen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-archive`

Erstellen oder Verwenden Sie kein Build-Archiv

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-backup`

vorherigen Build nicht sichern

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-cache`

Zwischenspeicherung deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-build-hooks`

Führen Sie keine Post-Build-Hooks aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--no-deps`

Build-Abhängigkeiten nicht lokal installieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--working-copy`

Entfernen: Verwenden Sie Git, um ein Repository jedes Drupal-Moduls zu klonen, anstatt einfach eine Version herunterzuladen.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--concurrency`

DRush: Legen Sie die Anzahl gleichzeitiger Projekte fest, die gleichzeitig verarbeitet werden.

- Standard: `4`
- Erfordert einen Wert

#### `--lock`

Löschen: Eine Sperrdatei erstellen oder aktualisieren (nur verfügbar mit DRush-Version 7+)

- Standard: `false`
- Akzeptiert keinen Wert


## `local:dir`

```bash
magento-cloud magento-cloud dir [<subdir>]
```

Lokalen Projektstamm suchen

### Argumente

#### `subdir`

Das zu suchende Unterverzeichnis (&#39;local&#39;, &#39;web&#39; oder &#39;shared&#39;)

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `metrics:all`

```bash
magento-cloud magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

BETA Zeigt CPU-, Datenträger- und Speichermetriken für eine Umgebung an

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 5m, max. 8h oder mehr (je nach Projekt), Standard 10m.

- Erfordert einen Wert

#### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 1 m.

- Erfordert einen Wert

#### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

#### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_used, tmp_inodes _limit, tmp_inodes_percent, tmp_inodes_used, Typ (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `metrics:cpu`

```bash
magento-cloud magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

BETA Anzeigen der CPU-Auslastung einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 5m, max. 8h oder mehr (je nach Projekt), Standard 10m.

- Erfordert einen Wert

#### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 1 m.

- Erfordert einen Wert

#### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

#### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `metrics:disk-usage`

```bash
magento-cloud magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Anzeigen der Festplattenauslastung einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 5m, max. 8h oder mehr (je nach Projekt), Standard 10m.

- Erfordert einen Wert

#### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 1 m.

- Erfordert einen Wert

#### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

#### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--tmp`

Temporäre Festplattenauslastung melden (Spalten anzeigen: Zeitstempel, Dienst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `metrics:memory`

```bash
magento-cloud magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

BETA Speichernutzung einer Umgebung anzeigen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 5m, max. 8h oder mehr (je nach Projekt), Standard 10m.

- Erfordert einen Wert

#### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Mindestens 1 m.

- Erfordert einen Wert

#### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

#### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `mount:download`

```bash
magento-cloud magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

Herunterladen von Dateien von einem Rich-Rich-Rsync-Server

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--all`, `-a`

Download von allen Reittieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--mount`, `-m`

Die -Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

#### `--target`

Das Verzeichnis, in das die Dateien heruntergeladen werden. Wenn —all verwendet wird, wird der Bereitstellungspfad angehängt

- Erfordert einen Wert

#### `--source-path`

Verwenden Sie den Quellpfad des Mount (anstelle des Bereitstellungspfads) als Unterverzeichnis des Ziels, wenn —all verwendet wird.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--delete`

Ob irrelevante Dateien im Zielverzeichnis gelöscht werden

- Standard: `false`
- Akzeptiert keinen Wert

#### `--exclude`

Vom Download auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

#### `--include`

Nicht auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `mount:list`

```bash
magento-cloud magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Liste der Reittiere abrufen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--paths`

Geben Sie nur die Bereitstellungspfade aus (1 pro Zeile)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Definition, Pfad. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert


## `mount:size`

```bash
magento-cloud magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Überprüfen Sie die Festplattenauslastung der Bereitstellungen.

```
Use this command to check the disk size and usage for an application's mounts.

Mounts are directories mounted into the application from a persistent, writable
filesystem. They are configured in the mounts key in the application configuration.

The filesystem's total size is determined by the disk key in the same file.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--refresh`

Cache aktualisieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: verfügbar, max, mounts, percent_used, size, used. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert


## `mount:upload`

```bash
magento-cloud magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

Hochladen von Dateien in eine -Bereitstellung mithilfe von Rsync

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--source`

Ein Verzeichnis mit hochzuladenden Dateien

- Erfordert einen Wert

#### `--mount`, `-m`

Die -Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

#### `--delete`

Ob irrelevante Dateien im Bereitstellungsfenster gelöscht werden

- Standard: `false`
- Akzeptiert keinen Wert

#### `--exclude`

Vom Hochladen auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

#### `--include`

Nicht auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `operation:list`

```bash
magento-cloud magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

BETA Listen-Laufzeitvorgänge in einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--full`

Beschränken Sie nicht die Länge des anzuzeigenden Befehls. Der Standardwert beträgt 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: service*, name*, start*, role, stop (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `operation:run`

```bash
magento-cloud magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```

BETA Ausführen eines Vorgangs für die Umgebung

### Argumente

#### `operation`

Der Vorgangsname

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--worker`

Arbeitername

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `project:clear-build-cache`

```bash
magento-cloud magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

Löschen des Build-Cache eines Projekts

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `project:get`

```bash
magento-cloud magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```

Lokales Klonen eines Projekts

### Argumente

#### `project`

Die Projekt-ID


#### `directory`

Das Verzeichnis, in das geklont werden soll. Die Standardeinstellung ist der Projekttitel

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--environment`, `-e`

Die zu klonende Umgebungs-ID. Die Standardeinstellung ist die Projektnummer oder die erste verfügbare Umgebung.

- Erfordert einen Wert

#### `--depth`

Erstellen eines flachen Klons: begrenzt die Anzahl der Commits im Verlauf

- Erfordert einen Wert

#### `--build`

Erstellen des Projekts nach dem Klonen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `project:info`

```bash
magento-cloud magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Eigenschaften für ein Projekt lesen oder festlegen

### Argumente

#### `property`

Der Name der Eigenschaft


#### `value`

Neuen Wert für die Eigenschaft festlegen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `project:list`

```bash
magento-cloud magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Liste aller aktiven Projekte abrufen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--pipe`

Geben Sie eine einfache Liste von Projekt-IDs aus. Deaktiviert die Paginierung.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--region`

Nach Region filtern (genaue Übereinstimmung)

- Erfordert einen Wert

#### `--title`

Nach Titel filtern (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

- Erfordert einen Wert

#### `--my`

Nur die Projekte anzeigen, deren Inhaber Sie sind

- Standard: `false`
- Akzeptiert keinen Wert

#### `--refresh`

Ob die Liste aktualisiert werden soll

- Standard: `1`
- Erfordert einen Wert

#### `--sort`

Eine Eigenschaft, die nach

- Standard: `title`
- Erfordert einen Wert

#### `--reverse`

Sortieren in umgekehrter (absteigender) Reihenfolge

- Standard: `false`
- Akzeptiert keinen Wert

#### `--page`

Seitenzahl. Dies ermöglicht die Paginierung, trotz Konfiguration oder —count. Wird ignoriert, wenn —pipe angegeben ist.

- Erfordert einen Wert

#### `--count`, `-c`

Die Anzahl der pro Seite anzuzeigenden Projekte. Verwenden Sie 0, um die Paginierung zu deaktivieren. Wird ignoriert, wenn —page angegeben ist.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, region*, created_at, organization_id, organization_label, organization_name, status (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `project:set-remote`

```bash
magento-cloud magento-cloud set-remote [<project>]
```

Remote-Projekt für das aktuelle Git-Repository festlegen

### Argumente

#### `project`

Die Projekt-ID

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `repo:cat`

```bash
magento-cloud magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```

Datei im Projekt-Repository lesen

### Argumente

#### `path`

Der Pfad zur Datei

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `repo:ls`

```bash
magento-cloud magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Auflisten von Dateien im Projekt-Repository

### Argumente

#### `path`

Der Pfad zu einem Unterverzeichnis

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--directories`, `-d`

Nur Ordner anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--files`, `-f`

Nur Dateien anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--git-style`

Stilausgabe ähnlich &quot;git ls-tree&quot;

- Standard: `false`
- Akzeptiert keinen Wert

#### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `repo:read`

```bash
magento-cloud magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Ordner oder Datei im Projekt-Repository lesen

### Argumente

#### `path`

Der Pfad zum Verzeichnis oder zur Datei

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `route:get`

```bash
magento-cloud magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```

Anzeigen detaillierter Informationen zu einer Route

### Argumente

#### `route`

Die ursprüngliche URL der Route

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--id`

Eine Route-ID zur Auswahl

- Erfordert einen Wert

#### `--primary`, `-1`

Primäre Route auswählen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

#### `--refresh`

Den Zwischenspeicher von Routen umgehen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert

#### `--identity-file`, `-i`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert


## `route:list`

```bash
magento-cloud magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```

Alle Routen für eine Umgebung auflisten

### Argumente

#### `environment`

Die Umgebungs-ID

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Den Zwischenspeicher von Routen umgehen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: route*, type*, to*, url (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `self:install`

```bash
magento-cloud magento-cloud self:install [--shell-type SHELL-TYPE]
```

Installieren oder Aktualisieren von CLI-Konfigurationsdateien

```
This command automatically installs shell configuration for the Magento Cloud CLI,
adding autocompletion support and handy aliases. Bash and ZSH are supported.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--shell-type`

Der Shell-Typ für die automatische Vervollständigung (bash oder zsh)

- Erfordert einen Wert


## `self:update`

```bash
magento-cloud magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

CLI auf die neueste Version aktualisieren

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--no-major`

Nur Aktualisierung zwischen kleineren oder Patch-Versionen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--unstable`

Aktualisierung auf eine neue instabile Version, falls verfügbar

- Standard: `false`
- Akzeptiert keinen Wert

#### `--manifest`

Speicherort der Manifestdatei überschreiben

- Erfordert einen Wert

#### `--current-version`

Aktuelle Version überschreiben

- Erfordert einen Wert

#### `--timeout`

Eine Zeitüberschreitung für die Versionsüberprüfung

- Standard: `30`
- Erfordert einen Wert


## `service:list`

```bash
magento-cloud magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Auflisten von Diensten im Projekt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--pipe`

Nur eine Liste mit Dienstnamen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Festplatte, Name, Größe, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:dump`

```bash
magento-cloud magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Erstellen eines binären Archivierungs-Dump von Daten aus MongoDB

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--collection`, `-c`

Die zu löschende Sammlung

- Erfordert einen Wert

#### `--gzip`, `-z`

Komprimieren Sie die Ablage mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

#### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `service:mongo:export`

```bash
magento-cloud magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Daten aus MongoDB exportieren

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--collection`, `-c`

Zu exportierende Kollektion

- Erfordert einen Wert

#### `--jsonArray`

Daten als einzelnes JSON-Array exportieren

- Standard: `false`
- Akzeptiert keinen Wert

#### `--type`

Der Exporttyp, z. B. &quot;csv&quot;

- Erfordert einen Wert

#### `--fields`, `-f`

Zu exportierende Felder

- Standard: `[]`
- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `service:mongo:restore`

```bash
magento-cloud magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Wiederherstellen eines binären Datenarchiv-Dump in MongoDB

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--collection`, `-c`

Die wiederherzustellende Sammlung

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `service:mongo:shell`

```bash
magento-cloud magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

MongoDB-Shell verwenden

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--eval`

Übergeben eines JavaScript-Fragments an die Shell

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `service:redis-cli`

```bash
magento-cloud magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```

Zugriff auf die Redis-CLI

### Argumente

#### `args`

Argumente zum Hinzufügen zum Befehl &quot;Redis&quot;

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `snapshot:create`

```bash
magento-cloud magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Schnappschuss einer Umgebung erstellen

### Argumente

#### `environment`

Umwelt

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--live`

Live Backup: Beenden Sie die Umgebung nicht. Wenn diese Einstellung festgelegt ist, bleibt die Umgebung aktiv und während der Sicherung für Verbindungen geöffnet. Dadurch werden Ausfallzeiten reduziert, wodurch das Risiko besteht, Daten in einem inkonsistenten Zustand zu sichern.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:delete`

```bash
magento-cloud magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```

Löschen eines Umgebungs-Snapshots

### Argumente

#### `id`

Die ID der Momentaufnahme. Erforderlich im nicht interaktiven Modus.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:get`

```bash
magento-cloud magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```

Anzeigen eines Umgebungs-Snapshots

### Argumente

#### `id`

Die ID der Momentaufnahme. Der Standardwert ist der neueste.

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Eigenschaft.

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert


## `snapshot:list`

```bash
magento-cloud magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Verfügbare Momentaufnahmen einer Umgebung auflisten

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `snapshot:restore`

```bash
magento-cloud magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```

Wiederherstellen eines Umgebungs-Snapshots

### Argumente

#### `snapshot`

Der Name der Momentaufnahme. Die Standardeinstellung ist die neueste

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--target`

Die wiederherzustellende Umgebung. Die Standardeinstellung ist die aktuelle Umgebung des Snapshots.

- Erfordert einen Wert

#### `--branch-from`

Wenn das —target noch nicht vorhanden ist, gibt dies das übergeordnete Element der neuen Umgebung an

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `source-operation:list`

```bash
magento-cloud magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Auflisten von Quellvorgängen in einer Umgebung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--full`

Beschränken Sie nicht die Länge des anzuzeigenden Befehls. Der Standardwert beträgt 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: App, Befehl, Vorgang. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `source-operation:run`

```bash
magento-cloud magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```

Quellvorgang ausführen

### Argumente

#### `operation`

Der Vorgangsname

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--variable`

Variable, die während des Vorgangs im Format type:name=value festgelegt wird

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-cert:load`

```bash
magento-cloud magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

Erstellen eines SSH-Zertifikats

```
This command checks if a valid SSH certificate is present, and generates a
new one if necessary.

Certificates allow you to make SSH connections without having previously
uploaded a public key. They are more secure than keys and they allow for
other features.

Normally the certificate is loaded automatically during login, or when
making an SSH connection. So this command is seldom needed.

If you want to set up certificates without login and without an SSH-related
command, for example if you are writing a script that uses an API token via
an environment variable, then you would probably want to run this command
explicitly. For unattended scripts, remember to turn off interaction via
--yes or the MAGENTO_CLOUD_CLI_NO_INTERACTION environment variable.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh-only`

Aktualisieren Sie das Zertifikat nur bei Bedarf (schreiben Sie keine SSH-Konfiguration).

- Standard: `false`
- Akzeptiert keinen Wert

#### `--new`

Aktualisieren des Zertifikats erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--new-key`

[Veraltet] Verwenden Sie stattdessen —new .

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-key:add`

```bash
magento-cloud magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```

Neuen SSH-Schlüssel hinzufügen

```
This command lets you add an SSH key to your account. It can generate a key using OpenSSH.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argumente

#### `path`

Der Pfad zu einem vorhandenen öffentlichen SSH-Schlüssel

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--name`

Ein Name zur Identifizierung des Schlüssels

- Erfordert einen Wert


## `ssh-key:delete`

```bash
magento-cloud magento-cloud ssh-key:delete [<id>]
```

SSH-Schlüssel löschen

```
This command lets you delete SSH keys from your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argumente

#### `id`

Die ID des zu löschenden SSH-Schlüssels

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).


## `ssh-key:list`

```bash
magento-cloud magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Abrufen einer Liste von SSH-Schlüsseln in Ihrem Konto

```
This command lets you list SSH keys in your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, path*, fingerprint (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `subscription:info`

```bash
magento-cloud magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```

Abonnementeigenschaften lesen und ändern

### Argumente

#### `property`

Der Name der Eigenschaft


#### `value`

Neuen Wert für die Eigenschaft festlegen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--id`, `-s`

Die Abonnement-ID

- Erfordert einen Wert

#### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `tunnel:close`

```bash
magento-cloud magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Schließen von SSH-Tunneln

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--all`, `-a`

Schließen aller Tunnel

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `tunnel:info`

```bash
magento-cloud magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Anzeigen von Beziehungsinformationen für SSH-Tunnel

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Die anzuzeigende Beziehungseigenschaft

- Erfordert einen Wert

#### `--encode`, `-c`

Ausgabe als base64-kodierte JSON

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert


## `tunnel:list`

```bash
magento-cloud magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

SSH-Tunnel auflisten

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--all`, `-a`

Alle Tunnel anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: port*, project*, environment*, app*, relation*, url (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:open`

```bash
magento-cloud magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

SSH-Tunnel für die Beziehungen einer App öffnen

```
This command opens SSH tunnels to all of the relationships of an application.

Connections can then be made to the application's services as if they were
local, for example a local MySQL client can be used, or the Solr web
administration endpoint can be accessed through a local browser.

This command requires the posix and pcntl PHP extensions (as multiple
background CLI processes are created to keep the SSH tunnels open). The
tunnel:single command can be used on systems without these
extensions.
```

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--gateway-ports`, `-g`

Remote-Hosts erlauben, eine Verbindung zu lokalen weitergeleiteten Ports herzustellen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `tunnel:single`

```bash
magento-cloud magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

Öffnen eines einzelnen SSH-Tunnels für eine App-Beziehung

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--port`

Der lokale Port

- Erfordert einen Wert

#### `--gateway-ports`, `-g`

Remote-Hosts erlauben, eine Verbindung zu lokalen weitergeleiteten Ports herzustellen

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

#### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

#### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert


## `user:add`

```bash
magento-cloud magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Einen Benutzer zum Projekt hinzufügen

### Argumente

#### `email`

Die E-Mail-Adresse des Benutzers

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--role`, `-r`

Die Projektrolle des Benutzers (&quot;admin&quot;oder &quot;viewer&quot;) oder die Umgebungstyprolle (z. B. &quot;staging:contributor&quot;oder &quot;production:viewer&quot;). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf &quot;none&quot;. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. &quot;%:viewer&quot;, um dem Benutzer die Rolle &quot;Betrachter&quot;für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. &quot;production:v&quot;.

- Standard: `[]`
- Erfordert einen Wert

#### `--force-invite`

Senden einer Einladung, auch wenn bereits eine gesendet wurde

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `user:delete`

```bash
magento-cloud magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```

Benutzer aus dem Projekt löschen

### Argumente

#### `email`

Die E-Mail-Adresse des Benutzers

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `user:get`

```bash
magento-cloud magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```

Benutzerrollen anzeigen

### Argumente

#### `email`

Die E-Mail-Adresse des Benutzers

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--level`, `-l`

Die Rollenebene (&quot;Projekt&quot;oder &quot;Umgebung&quot;)

- Erfordert einen Wert

#### `--pipe`

Ausgabe der zu stdout zu sendenden Rolle (nach Durchführung von Änderungen)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

#### `--role`, `-r`

[Veraltet: Verwenden Sie user:update , um die Benutzerrolle(en) zu ändern]

- Erfordert einen Wert


## `user:list`

```bash
magento-cloud magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Projektbenutzer auflisten

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: email*, name*, role*, id*, given_at, updated_at (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert


## `user:update`

```bash
magento-cloud magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Benutzerrollen in einem Projekt aktualisieren

### Argumente

#### `email`

Die E-Mail-Adresse des Benutzers

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--role`, `-r`

Die Projektrolle des Benutzers (&quot;admin&quot;oder &quot;viewer&quot;) oder die Umgebungstyprolle (z. B. &quot;staging:contributor&quot;oder &quot;production:viewer&quot;). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf &quot;none&quot;. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. &quot;%:viewer&quot;, um dem Benutzer die Rolle &quot;Betrachter&quot;für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. &quot;production:v&quot;.

- Standard: `[]`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:create`

```bash
magento-cloud magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```

Variable erstellen

### Argumente

#### `name`

Der Variablenname

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--update`, `-u`

Aktualisieren Sie die Variable, falls sie bereits vorhanden ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--level`, `-l`

Die Ebene, auf der die Variable festgelegt werden soll (&quot;Projekt&quot;oder &quot;Umgebung&quot;)

- Erfordert einen Wert

#### `--name`

Der Variablenname

- Erfordert einen Wert

#### `--value`

Der Wert der Variablen

- Erfordert einen Wert

#### `--json`

Ob der Variablenwert JSON-formatiert ist

- Standard: `false`
- Erfordert einen Wert

#### `--sensitive`

Ob der Variablenwert empfindlich ist

- Standard: `false`
- Erfordert einen Wert

#### `--prefix`

Das Präfix des Variablennamens, das den Typ bestimmen kann, z. B. &quot;env&quot;. Gilt nur, wenn der Name noch kein Präfix enthält. (z. B. &quot;none&quot;oder &quot;env:&quot;)

- Standard: `none`
- Erfordert einen Wert

#### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

#### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt werden kann

- Standard: `true`
- Erfordert einen Wert

#### `--visible-build`

Ob die Variable zur Build-Zeit sichtbar sein soll

- Erfordert einen Wert

#### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:delete`

```bash
magento-cloud magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Variable löschen

### Argumente

#### `name`

Der Variablenname

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:get`

```bash
magento-cloud magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```

Anzeigen von Variablen

### Argumente

#### `name`

Der Name der Variablen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--property`, `-P`

Anzeigen einer einzelnen Variableneigenschaft

- Erfordert einen Wert

#### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--pipe`

[Veraltete Option] Nur Variablenwert ausgeben

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:list`

```bash
magento-cloud magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Listenvariablen

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: is_enabled, level, name, value. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert


## `variable:update`

```bash
magento-cloud magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Variable aktualisieren

### Argumente

#### `name`

Der Variablenname

- Erforderlich

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--allow-no-change`

Rückkehrerfolg (kein Exitcode), wenn keine Änderungen bereitgestellt wurden

- Standard: `false`
- Akzeptiert keinen Wert

#### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

#### `--value`

Der Wert der Variablen

- Erfordert einen Wert

#### `--json`

Ob der Variablenwert JSON-formatiert ist

- Standard: `false`
- Erfordert einen Wert

#### `--sensitive`

Ob der Variablenwert empfindlich ist

- Standard: `false`
- Erfordert einen Wert

#### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

#### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt werden kann

- Standard: `true`
- Erfordert einen Wert

#### `--visible-build`

Ob die Variable zur Build-Zeit sichtbar sein soll

- Erfordert einen Wert

#### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

#### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert


## `worker:list`

```bash
magento-cloud magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Liste aller entsandten Arbeitskräfte

### Optionen

Globale Optionen finden Sie unter [Globale Optionen](#global-options).

#### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

#### `--pipe`

Nur eine Liste mit Worker-Namen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

#### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

#### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

#### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

#### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Befehle, Name, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

#### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert
