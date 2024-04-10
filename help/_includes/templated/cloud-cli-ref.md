---
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '21442'
ht-degree: 0%

---
# Magento-Cloud (Adobe Commerce auf Cloud-Infrastruktur)

<!-- The template to render with above values -->
**Version**: 1.46.1

Diese Referenz enthält 119 Befehle, die über die `magento-cloud` Befehlszeilen-Tool.
Die anfängliche Liste wird automatisch mit dem `magento-cloud list` Befehl bei Adobe Commerce in der Cloud-Infrastruktur.

>[!NOTE]
>
>Dieser Verweis wird aus der Anwendungs-Code-Basis generiert. Um den Inhalt zu ändern, können Sie den Quell-Code für die entsprechende Befehlsimplementierung in der [Codebase](https://github.com/magento/magento-cloud-cli) Repository speichern und Ihre Änderungen zur Überprüfung übermitteln. Eine andere Möglichkeit besteht darin, _Geben Sie uns Feedback_ (finden Sie den Link oben rechts). Richtlinien für Beiträge finden Sie unter [Code-Beiträge](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

Löschen des CLI-Cache

```bash
magento-cloud cc
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `decode`

Decodieren einer codierten Zeichenfolge wie MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

Der zu dekodierende Variablenwert

- Erforderlich

### `--property`, `-P`

Die Eigenschaft, die in der Variablen angezeigt werden soll

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `docs`

Öffnen der Onlinedokumentation

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Suchbegriff(e)

- Standard: `[]`

- Array

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Auf 0 für keine festlegen.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL an stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `help`

Zeigt Hilfe zu einem Befehl an

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Der Befehlsname

- Standard: `help`


### `--format`

Das Ausgabeformat (txt, json oder md)

- Standard: `txt`
- Erfordert einen Wert

### `--raw`

So geben Sie die Raw-Befehlshilfe aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `list`

Listet Befehle auf

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

Der auszuführende Befehl

- Erforderlich

### `namespace`

Der Namespace-Name


### `--raw`

So geben Sie die unbearbeitete Befehlsliste aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat (txt, xml, json oder md)

- Standard: `txt`
- Erfordert einen Wert

### `--all`

Alle Befehle anzeigen, einschließlich ausgeblendeter Befehle

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `multi`

Ausführen eines Befehls für mehrere Projekte

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

Der auszuführende Befehl

- Standard: `[]`

- Erforderlich
- Array

### `--projects`, `-p`

Eine Liste der Projekt-IDs, durch Kommas und/oder Leerzeichen getrennt

- Erfordert einen Wert

### `--continue`

Ausführen von Befehlen auch dann fortsetzen, wenn eine Ausnahme auftritt

- Standard: `false`
- Akzeptiert keinen Wert

### `--sort`

Eine Eigenschaft, nach der die Liste der Projektoptionen sortiert werden soll

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

Kehrt die Reihenfolge der Projektoptionen um

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `web`

Öffnen Sie das Projekt in der Web-Benutzeroberfläche

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Auf 0 für keine festlegen.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL an stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:cancel`

Abbrechen einer Aktivität

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die letzte absagbare Aktivität.


### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. „%var%“ zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--all`, `-a`

Aktuelle Aktivitäten in allen Umgebungen überprüfen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:get`

Anzeigen detaillierter Informationen zu einer einzelnen Aktivität

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Standardmäßig wird die letzte Aktivität verwendet.


### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. „%var%“ zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--state`

Nach Status filtern (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder canceled. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

### `--incomplete`, `-i`

Nur unvollständige Aktivitäten einbeziehen (bei Auswahl einer Standardaktivität). Dies ist eine Kurzschreibweise für \&lt;info>—state=in_progress,Pending\&lt;/info>

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`, `-a`

Aktuelle Aktivitäten in allen Umgebungen überprüfen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:list`

Abrufen einer Liste von Aktivitäten für eine Umgebung oder ein Projekt

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Filteraktivitäten nach Typ Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen aufgeteilt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann „cron“ „environment.cron„-Aktivitäten auswählen. Die Zeichen % oder * können als Platzhalter verwendet werden, z. B. „%var%„, um variablenbezogene Aktivitäten auszuwählen.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Ausschließen von Aktivitäten nach Typ. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann „cron“ „environment.cron„-Aktivitäten ausschließen. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

### `--start`

Nur Aktivitäten, die vor diesem Datum erstellt wurden, werden aufgelistet

- Erfordert einen Wert

### `--state`

Aktivitäten nach Status filtern: in Bearbeitung, ausstehend, abgeschlossen oder abgebrochen. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern von Aktivitäten nach Ergebnis: Erfolg oder Fehler

- Erfordert einen Wert

### `--incomplete`, `-i`

Nur unvollständige Aktivitäten auflisten

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`, `-a`

Aktivitäten in allen Umgebungen auflisten

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: ID*, Erstellt*, Beschreibung*, Fortschritt*, Status*, Ergebnis*, Abgeschlossen, Umgebungen, Typ (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:log`

Protokoll einer Aktivität anzeigen

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Standardmäßig wird die letzte Aktivität verwendet.


### `--refresh`

Aktualisierungsintervall der Aktivität (Sekunden). Auf 0 gesetzt, um die Aktualisierung zu deaktivieren.

- Standard: `3`
- Erfordert einen Wert

### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. „%var%“ zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--state`

Nach Status filtern (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder canceled. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

### `--incomplete`, `-i`

Nur unvollständige Aktivitäten einbeziehen (bei Auswahl einer Standardaktivität). Dies ist eine Kurzschreibweise für \&lt;info>—state=in_progress,Pending\&lt;/info>

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`, `-a`

Aktuelle Aktivitäten in allen Umgebungen überprüfen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `app:config-get`

Anzeigen der Konfiguration einer App

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`, `-P`

Die anzuzeigende Konfigurationseigenschaft

- Erfordert einen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--identity-file`, `-i`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `app:list`

Auflisten von Apps im Projekt

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Nur eine Liste der App-Namen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Name*, Typ*, Festplatte, Pfad, Größe (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:api-token-login`

Melden Sie sich mit einem API-Token bei Magento Cloud an

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:browser-login`

Anmelden bei Magento Cloud über einen Browser

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Melden Sie sich erneut an, auch wenn Sie bereits angemeldet sind

- Standard: `false`
- Akzeptiert keinen Wert

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Auf 0 für keine festlegen.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL an stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:info`

Kontoinformationen anzeigen

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

Die anzuzeigende Kontoeigenschaft


### `--no-auto-login`

Überspringt die automatische Anmeldung. Wenn Sie nicht angemeldet sind, wird nichts ausgegeben und der Exitcode ist 0, vorausgesetzt, es werden keine anderen Fehler ausgegeben.

- Standard: `false`
- Akzeptiert keinen Wert

### `--property`, `-P`

Die anzuzeigende Kontoeigenschaft (alternative Syntax)

- Erfordert einen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:logout`

Abmelden von Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Von allen lokalen Sitzungen abmelden

- Standard: `false`
- Akzeptiert keinen Wert

### `--other`

Von anderen lokalen Sitzungen abmelden

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `blackfire:setup`

Einrichten der Blackfire.io-Integration für das Projekt

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

Die Server-ID

- Erfordert einen Wert

### `--server_token`

Das Server-Token

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:add`

Hinzufügen eines SSL-Zertifikats zum Projekt

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

Der Pfad zur Zertifikatdatei

- Erfordert einen Wert

### `--key`

Der Pfad zur Datei mit dem privaten Schlüssel des Zertifikats

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatkettendatei

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:delete`

Löschen eines Zertifikats aus dem Projekt

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

Die Zertifikat-ID (oder der Beginn)

- Erforderlich

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:get`

Anzeigen eines Zertifikats

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

Die Zertifikat-ID (oder der Beginn)

- Erforderlich

### `--property`, `-P`

Die anzuzeigende Zertifikateigenschaft

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:list`

Auflisten von Projektzertifikaten

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Nach Domain-Namen filtern (Suche ohne Unterscheidung von Groß- und Kleinschreibung)

- Erfordert einen Wert

### `--exclude-domain`

Zertifikate ausschließen, Übereinstimmung nach Domain-Namen (Suche ohne Berücksichtigung der Groß-/Kleinschreibung)

- Erfordert einen Wert

### `--issuer`

Nach Aussteller filtern

- Erfordert einen Wert

### `--only-auto`

Nur automatisch bereitgestellte Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-auto`

Nur manuell hinzugefügte Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--ignore-expiry`

Abgelaufene und nicht abgelaufene Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--only-expired`

Nur abgelaufene Zertifikate anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-expired`

Nur nicht abgelaufene Zertifikate anzeigen (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe-domains`

Gibt nur eine Liste der Domain-Namen zurück, die von den Zertifikaten abgedeckt werden

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: erstellt, Domains, Ablaufdatum, ID, Aussteller. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `commit:get`

Commit-Details anzeigen

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

Der Commit SHA. Dies kann auch &quot;HEAD&quot; und Caret-Suffixe (^) oder Tilde-Suffixe (~) für übergeordnete Commits akzeptieren.

- Standard: `HEAD`


### `--property`, `-P`

Die Commit-Eigenschaft zum Anzeigen.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `commit:list`

Commits auflisten

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

Der Git-Commit SHA wird gestartet. Dies kann auch &quot;HEAD&quot; und Caret-Suffixe (^) oder Tilde-Suffixe (~) für übergeordnete Commits akzeptieren.


### `--limit`

Die Anzahl der anzuzeigenden Commits.

- Standard: `10`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Autor, Datum, SHA, Zusammenfassung. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `db:dump`

Erstellen eines lokalen Dumps der Remote-Datenbank

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

Das zu entladende Schema. Lassen Sie die Verwendung des Standardschemas (normalerweise „main„) weg.

- Erfordert einen Wert

### `--file`, `-f`

Ein benutzerdefinierter Dateiname für den Speicherauszug

- Erfordert einen Wert

### `--directory`, `-d`

Ein benutzerdefiniertes Verzeichnis für den Speicherauszug

- Erfordert einen Wert

### `--gzip`, `-z`

Komprimieren Sie den Dump mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

### `--timestamp`, `-t`

Hinzufügen eines Zeitstempels zum Dump-Dateinamen

- Standard: `false`
- Akzeptiert keinen Wert

### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

### `--table`

Einzuschließende Tabelle(n)

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-table`

Auszuschließende Tabelle(n)

- Standard: `[]`
- Erfordert einen Wert

### `--schema-only`

Nur Schemata sichern, keine Daten

- Standard: `false`
- Akzeptiert keinen Wert

### `--charset`

Die Zeichensatzkodierung für den Dump

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `db:size`

Schätzen der Festplattenauslastung einer Datenbank

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`, `-B`

Größe in Byte anzeigen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--cleanup`, `-C`

Überprüfen, ob Tabellen bereinigt werden können, und Empfehlungen anzeigen (nur InnoDb).

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: max, percent_used, used. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `db:sql`

SQL auf der Remote-Datenbank ausführen

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

Eine auszuführende SQL-Anweisung


### `--raw`

Erzeugen von rohen, nicht tabellarischen Ausgaben

- Standard: `false`
- Akzeptiert keinen Wert

### `--schema`

Das zu verwendende Schema. Lassen Sie die Verwendung des Standardschemas (normalerweise „main„) weg. Übergeben Sie eine leere Zeichenfolge, um kein Schema zu verwenden.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:add`

Hinzufügen einer neuen Domain zum Projekt

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domain-Name

- Erforderlich

### `--cert`

Der Pfad zur Zertifikatdatei für diese Domain

- Erfordert einen Wert

### `--key`

Der Pfad zur Datei mit dem privaten Schlüssel für das angegebene Zertifikat.

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatkettendatei bzw. zu den Dateien für das angegebene Zertifikat

- Standard: `[]`
- Erfordert einen Wert

### `--attach`

Die Produktions-Domain, die diese in den Routen der Umgebung ersetzt. Erforderlich für Nicht-Produktions-Umgebungs-Domains.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:delete`

Löschen einer Domain aus dem Projekt

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domain-Name

- Erforderlich

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:get`

Anzeigen detaillierter Informationen für eine Domain

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

Der Domain-Name


### `--property`, `-P`

Die anzuzeigende Domain-Eigenschaft

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:list`

Abrufen einer Liste aller Domains

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: name*, ssl*, created_at*, registered_name, replace_for, type, updated_at (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:update`

Aktualisieren einer Domain

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domain-Name

- Erforderlich

### `--cert`

Der Pfad zur Zertifikatdatei für diese Domain

- Erfordert einen Wert

### `--key`

Der Pfad zur Datei mit dem privaten Schlüssel für das angegebene Zertifikat.

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatkettendatei bzw. zu den Dateien für das angegebene Zertifikat

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:activate`

Aktivieren einer Umgebung

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Die zu aktivierenden Umgebungen

- Standard: `[]`

- Array

### `--parent`

Vor der Aktivierung eine neue übergeordnete Umgebung festlegen

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:branch`

Verzweigen einer Umgebung

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

Die ID (Zweigname) der neuen Umgebung


### `parent`

Das übergeordnete Element der neuen Umgebung


### `--title`

Der Titel der neuen Umgebung

- Erfordert einen Wert

### `--type`

Der Typ der neuen Umgebung

- Erfordert einen Wert

### `--no-clone-parent`

Die Daten der übergeordneten Umgebung nicht klonen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:checkout`

Auschecken einer Umgebung

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

Die ID der Umgebung, die ausgecheckt werden soll. Beispiel: „sprint2“


### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:delete`

Löschen einer oder mehrerer Umgebungen

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Die zu löschenden Umgebungen. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`

- Array

### `--delete-branch`

Löschen von Git-Verzweigungen für inaktive Umgebungen ohne Bestätigung

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-delete-branch`

Löschen Sie keine Git-Verzweigungen (inaktive Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Löschen Sie alle Umgebungen eines Typs (fügen Sie beliebige andere ausgewählte Umgebungen hinzu). Werte können durch Kommas (z. B. „a, b, c„) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--only-type`, `-t`

Nur Umgebungen eines bestimmten Typs löschen Werte können durch Kommas (z. B. „a, b, c„) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude`

Umgebung(en) nicht zu löschen. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`

Umgebungstypen, deren Werte nicht gelöscht werden sollen, können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--inactive`

Alle inaktiven Umgebungen löschen (zu allen anderen ausgewählten hinzufügen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--merged`

Alle zusammengeführten Umgebungen löschen (zu allen anderen ausgewählten hinzufügen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--allow-delete-parent`

Löschen von Umgebungen mit untergeordneten Elementen zulassen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:http-access`

Aktualisieren der HTTP-Zugriffseinstellungen für eine Umgebung

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Zugriffsbeschränkung im Format „permission:address„. 0 verwenden, um alle Adressen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

### `--auth`

Einfache HTTP-Authentifizierungsdaten im Format „username:password„. Verwenden Sie 0, um alle Anmeldeinformationen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

### `--enabled`

Ob die Zugriffssteuerung aktiviert werden soll: 1 zum Aktivieren, 0 zum Deaktivieren

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:info`

Lesen oder Festlegen von Eigenschaften für eine Umgebung

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Legen Sie einen neuen Wert für die Eigenschaft fest


### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:init`

Initialisieren einer Umgebung aus einem öffentlichen Git-Repository

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

Eine URL zu einem Git-Repository

- Erforderlich

### `--profile`

Der Name des Profils

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:list`

Abrufen einer Liste von Umgebungen

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Keine inaktiven Umgebungen anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Ausgabe einer einfachen Liste von Umgebungs-IDs.

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Ob die Liste aktualisiert werden soll.

- Standard: `1`
- Erfordert einen Wert

### `--sort`

Eine Eigenschaft zum Sortieren nach

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

In umgekehrter (absteigender) Reihenfolge sortieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Filtern Sie die Liste nach Umgebungstyp(en). Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: id*, title*, status*, type*, created, machine_name, updated (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:logs`

Lesen der Protokolle einer Umgebung

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

Der Protokolltyp, z. B. „Zugriff“ oder „Fehler“


### `--lines`

Die Anzahl der anzuzeigenden Zeilen

- Standard: `100`
- Erfordert einen Wert

### `--tail`

Protokoll fortlaufend verfolgen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:merge`

Zusammenführen einer Umgebung

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Die zu fusionierende Umgebung


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:pause`

Pausieren einer Umgebung

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:push`

Code in eine Umgebung pushen

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

Die Quellreferenz: ein Zweigname oder Commit-Hash

- Standard: `HEAD`


### `--target`

Der Name der Zielverzweigung. Die Standardeinstellung ist die aktuelle Verzweigung.

- Erfordert einen Wert

### `--force`, `-f`

Nicht-schnelle Vorwärtsaktualisierungen zulassen

- Standard: `false`
- Akzeptiert keinen Wert

### `--force-with-lease`

Nicht-schnelle Weiterleitungen zulassen, wenn die Remote-Tracking-Verzweigung auf dem neuesten Stand ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--set-upstream`, `-u`

Legen Sie die Zielumgebung als Upstream für die Quellverzweigung fest. Dadurch wird auch das Zielprojekt als Remote für das lokale Repository festgelegt.

- Standard: `false`
- Akzeptiert keinen Wert

### `--activate`

Umgebung vor dem Pushen aktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--parent`

Übergeordnete Umgebung festlegen (nur bei Verwendung von —activate)

- Erfordert einen Wert

### `--type`

Umgebungstyp festlegen (nur verwendet mit —activate )

- Erfordert einen Wert

### `--no-clone-parent`

Klonen Sie nicht die Daten der übergeordneten Verzweigung (nur verwendet mit —activate)

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:redeploy`

Erneutes Bereitstellen einer Umgebung

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:relationships`

Beziehungen einer Umgebung anzeigen

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

Die Umgebung


### `--property`, `-P`

Die anzuzeigende Beziehungseigenschaft

- Erfordert einen Wert

### `--refresh`

Ob die Beziehungen aktualisiert werden sollen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:resume`

Fortsetzen pausierter Umgebungen

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:scp`

Kopieren von Dateien in und aus einer Umgebung mithilfe von scp

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

Zu kopierende Dateien Verwenden Sie das Präfix „remote:„, um Remote-Standorte zu definieren.

- Standard: `[]`

- Array

### `--recursive`, `-r`

Rekursives Kopieren ganzer Ordner

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:ssh`

SSH zur aktuellen Umgebung

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Ein Befehl, der in der Umgebung ausgeführt werden soll.

- Standard: `[]`

- Array

### `--pipe`

Ausgabe nur der SSH-URL.

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`

Alle SSH-URLs ausgeben (für jede Anwendung).

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:synchronize`

Synchronisieren des Codes einer Umgebung und/oder der Daten des übergeordneten Elements

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

Zu synchronisierende Elemente: „code„, „data“ oder beides

- Standard: `[]`

- Array

### `--rebase`

Code durch Neubasierung anstatt durch Zusammenführen synchronisieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:url`

Abrufen der öffentlichen URLs einer Umgebung

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`, `-1`

Gibt nur die URL für die primäre Route zurück.

- Standard: `false`
- Akzeptiert keinen Wert

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Auf 0 für keine festlegen.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL an stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:xdebug`

Öffnen eines Tunnels zu Xdebug in der Umgebung

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Der lokale Port

- Standard: `9000`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:activity:get`

Anzeigen detaillierter Informationen zu einer einzelnen Integrationsaktivität

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `activity`

Die Aktivitäts-ID. Standardmäßig wird die letzte Integrationsaktivität verwendet.


### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:activity:list`

Abrufen einer Liste von Aktivitäten für eine Integration

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--type`

Filtern von Aktivitäten nach Typ. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Ausschließen von Aktivitäten nach Typ. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

### `--start`

Nur Aktivitäten, die vor diesem Datum erstellt wurden, werden aufgelistet

- Erfordert einen Wert

### `--state`

Filtern von Aktivitäten nach Status. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern von Aktivitäten nach Ergebnis

- Erfordert einen Wert

### `--incomplete`, `-i`

Nur unvollständige Aktivitäten auflisten

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: id*, created*, description*, type*, state*, result*, completed (* = Default columns). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:activity:log`

Protokoll für eine Integrationsaktivität anzeigen

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `activity`

Die Aktivitäts-ID. Standardmäßig wird die letzte Integrationsaktivität verwendet.


### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

[Veraltete Option, nicht verwendet]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:add`

Hinzufügen einer Integration zum Projekt

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Erfordert einen Wert

### `--base-url`

Die Basis-URL der Server-Installation

- Erfordert einen Wert

### `--bitbucket-url`

Die Basis-URL der Bitbucket-Server-Installation

- Erfordert einen Wert

### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

### `--token`

Ein Authentifizierungs- oder Zugriffs-Token für die Integration

- Erfordert einen Wert

### `--key`

Ein Bitbucket-OAuth-Verbraucherschlüssel

- Erfordert einen Wert

### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

### `--license-key`

Der Lizenzschlüssel für New Relic-Protokolle

- Erfordert einen Wert

### `--server-project`

Das Projekt (z. B. „namespace/repo„)

- Erfordert einen Wert

### `--repository`

Das zu trackende Repository (z. B. „Eigentümer/Repository„)

- Erfordert einen Wert

### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests`

Jede Pull-Anforderung als Umgebung erstellen

- Standard: `true`
- Erfordert einen Wert

### `--build-draft-pull-requests`

Erstellen von Entwürfen für Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests-post-merge`

Erstellen von Pull-Anforderungen basierend auf ihrem Post-Merge-Status

- Standard: `false`
- Erfordert einen Wert

### `--build-wip-merge-requests`

GitLab: WIP-Zusammenführungsanfragen erstellen

- Standard: `true`
- Erfordert einen Wert

### `--merge-requests-clone-parent-data`

GitLab: Daten für Zusammenführungsanfragen klonen

- Standard: `true`
- Erfordert einen Wert

### `--pull-requests-clone-parent-data`

Klonen der Daten der übergeordneten Umgebung für Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--resync-pull-requests`

Daten der Anforderungsumgebung bei jedem Build erneut synchronisieren

- Standard: `false`
- Erfordert einen Wert

### `--fetch-branches`

Alle Verzweigungen aus der Remote-Instanz abrufen (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

### `--prune-branches`

Löschen von Verzweigungen, die auf der Remote-Instanz nicht vorhanden sind

- Standard: `true`
- Erfordert einen Wert

### `--resources-init`

Die beim Initialisieren eines neuen Dienstes zu verwendenden Ressourcen („minimum„, „default„, „manual„, „parent„)

- Erfordert einen Wert

### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

### `--shared-key`

Webhook: der gemeinsame geheime JWS-Schlüssel

- Erfordert einen Wert

### `--file`

Der Name einer lokalen Datei, die das hochzuladende Skript enthält

- Erfordert einen Wert

### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

### `--states`

Eine Liste der Status, auf die Aktionen durchgeführt werden sollen, z. B. „Ausstehend„, „In Bearbeitung„, „Abgeschlossen“

- Standard: `complete`
- Erfordert einen Wert

### `--environments`

Die einzuschließenden Umgebungs-IDs

- Standard: `*`
- Erfordert einen Wert

### `--excluded-environments`

Die auszuschließenden Umgebungs-IDs

- Standard: `[]`
- Erfordert einen Wert

### `--from-address`

[optional] Benutzerdefinierte Absenderadresse für Benachrichtigungs-E-Mails

- Erfordert einen Wert

### `--recipients`

Die E-Mail-Adresse(n) des Empfängers

- Standard: `[]`
- Erfordert einen Wert

### `--channel`

Der Slack-Kanal

- Erfordert einen Wert

### `--routing-key`

Der PagerDuty-Routing-Schlüssel

- Erfordert einen Wert

### `--category`

Die Kategorie „Sumo Logic„, die zum Filtern verwendet wird

- Erfordert einen Wert

### `--index`

Der Splunk-Index

- Erfordert einen Wert

### `--sourcetype`

Der Splunk-Ereignistyp

- Erfordert einen Wert

### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

### `--syslog-host`

Syslog Relais/Collector-Host

- Erfordert einen Wert

### `--syslog-port`

Syslog-Relais-/Kollektor-Port

- Erfordert einen Wert

### `--facility`

Syslog-Einrichtung

- Standard: `1`
- Erfordert einen Wert

### `--message-format`

Syslog-Nachrichtenformat (&#39;rfc3164&#39; oder &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Erfordert einen Wert

### `--auth-mode`

Authentifizierungsmodus (&#39;prefix&#39; oder &#39;structured_data&#39;)

- Standard: `prefix`
- Erfordert einen Wert

### `--auth-token`

Authentifizierungstoken

- Erfordert einen Wert

### `--verify-tls`

Ob die HTTPS-Zertifikatüberprüfung aktiviert werden soll (empfohlen)

- Standard: `true`
- Erfordert einen Wert

### `--header`

In POST-Anfragen zu verwendende HTTP-Header Trennen Sie Namen und Werte mit einem Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:delete`

Löschen einer Integration aus einem Projekt

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Die Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:get`

Anzeigen von Details einer Integration

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--property`, `-P`

Die anzuzeigende Integrationseigenschaft

- Akzeptiert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:list`

Anzeigen einer Liste der Projektintegration(en)

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: ID, Zusammenfassung, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:update`

Aktualisieren einer Integration

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Die ID der zu aktualisierenden Integration


### `--type`

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Erfordert einen Wert

### `--base-url`

Die Basis-URL der Server-Installation

- Erfordert einen Wert

### `--bitbucket-url`

Die Basis-URL der Bitbucket-Server-Installation

- Erfordert einen Wert

### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

### `--token`

Ein Authentifizierungs- oder Zugriffs-Token für die Integration

- Erfordert einen Wert

### `--key`

Ein Bitbucket-OAuth-Verbraucherschlüssel

- Erfordert einen Wert

### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

### `--license-key`

Der Lizenzschlüssel für New Relic-Protokolle

- Erfordert einen Wert

### `--server-project`

Das Projekt (z. B. „namespace/repo„)

- Erfordert einen Wert

### `--repository`

Das zu trackende Repository (z. B. „Eigentümer/Repository„)

- Erfordert einen Wert

### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests`

Jede Pull-Anforderung als Umgebung erstellen

- Standard: `true`
- Erfordert einen Wert

### `--build-draft-pull-requests`

Erstellen von Entwürfen für Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests-post-merge`

Erstellen von Pull-Anforderungen basierend auf ihrem Post-Merge-Status

- Standard: `false`
- Erfordert einen Wert

### `--build-wip-merge-requests`

GitLab: WIP-Zusammenführungsanfragen erstellen

- Standard: `true`
- Erfordert einen Wert

### `--merge-requests-clone-parent-data`

GitLab: Daten für Zusammenführungsanfragen klonen

- Standard: `true`
- Erfordert einen Wert

### `--pull-requests-clone-parent-data`

Klonen der Daten der übergeordneten Umgebung für Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--resync-pull-requests`

Daten der Anforderungsumgebung bei jedem Build erneut synchronisieren

- Standard: `false`
- Erfordert einen Wert

### `--fetch-branches`

Alle Verzweigungen aus der Remote-Instanz abrufen (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

### `--prune-branches`

Löschen von Verzweigungen, die auf der Remote-Instanz nicht vorhanden sind

- Standard: `true`
- Erfordert einen Wert

### `--resources-init`

Die beim Initialisieren eines neuen Dienstes zu verwendenden Ressourcen („minimum„, „default„, „manual„, „parent„)

- Erfordert einen Wert

### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

### `--shared-key`

Webhook: der gemeinsame geheime JWS-Schlüssel

- Erfordert einen Wert

### `--file`

Der Name einer lokalen Datei, die das hochzuladende Skript enthält

- Erfordert einen Wert

### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

### `--states`

Eine Liste der Status, auf die Aktionen durchgeführt werden sollen, z. B. „Ausstehend„, „In Bearbeitung„, „Abgeschlossen“

- Standard: `complete`
- Erfordert einen Wert

### `--environments`

Die einzuschließenden Umgebungs-IDs

- Standard: `*`
- Erfordert einen Wert

### `--excluded-environments`

Die auszuschließenden Umgebungs-IDs

- Standard: `[]`
- Erfordert einen Wert

### `--from-address`

[optional] Benutzerdefinierte Absenderadresse für Benachrichtigungs-E-Mails

- Erfordert einen Wert

### `--recipients`

Die E-Mail-Adresse(n) des Empfängers

- Standard: `[]`
- Erfordert einen Wert

### `--channel`

Der Slack-Kanal

- Erfordert einen Wert

### `--routing-key`

Der PagerDuty-Routing-Schlüssel

- Erfordert einen Wert

### `--category`

Die Kategorie „Sumo Logic„, die zum Filtern verwendet wird

- Erfordert einen Wert

### `--index`

Der Splunk-Index

- Erfordert einen Wert

### `--sourcetype`

Der Splunk-Ereignistyp

- Erfordert einen Wert

### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

### `--syslog-host`

Syslog Relais/Collector-Host

- Erfordert einen Wert

### `--syslog-port`

Syslog-Relais-/Kollektor-Port

- Erfordert einen Wert

### `--facility`

Syslog-Einrichtung

- Standard: `1`
- Erfordert einen Wert

### `--message-format`

Syslog-Nachrichtenformat (&#39;rfc3164&#39; oder &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Erfordert einen Wert

### `--auth-mode`

Authentifizierungsmodus (&#39;prefix&#39; oder &#39;structured_data&#39;)

- Standard: `prefix`
- Erfordert einen Wert

### `--auth-token`

Authentifizierungstoken

- Erfordert einen Wert

### `--verify-tls`

Ob die HTTPS-Zertifikatüberprüfung aktiviert werden soll (empfohlen)

- Standard: `true`
- Erfordert einen Wert

### `--header`

In POST-Anfragen zu verwendende HTTP-Header Trennen Sie Namen und Werte mit einem Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:validate`

Überprüfen einer vorhandenen Integration

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `local:build`

Lokales Erstellen des aktuellen Projekts

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Zu erstellende(s) Programm(e) angeben

- Standard: `[]`

- Array

### `--abslinks`, `-a`

Absolute Links verwenden

- Standard: `false`
- Akzeptiert keinen Wert

### `--source`, `-s`

Das Quellverzeichnis. Standardmäßig wird der aktuelle Projektstamm verwendet.

- Erfordert einen Wert

### `--destination`, `-d`

Das Ziel, mit dem der Webstamm jeder App verknüpft wird. Standard: _www

- Erfordert einen Wert

### `--copy`, `-c`

In ein Build-Verzeichnis kopieren, anstatt von der Quelle aus eine Verknüpfung herzustellen

- Standard: `false`
- Akzeptiert keinen Wert

### `--clone`

Verwenden Sie Git, um die aktuelle HEAD in das Build-Verzeichnis zu klonen

- Standard: `false`
- Akzeptiert keinen Wert

### `--run-deploy-hooks`

Ausführen von Bereitstellungs- und/oder Bereitstellungs-Hooks

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-clean`

Alte Builds nicht entfernen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-archive`

Erstellen oder verwenden Sie kein Build-Archiv

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-backup`

Den vorherigen Build nicht sichern

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-cache`

Cache deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-build-hooks`

Keine Post-Build-Hooks ausführen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-deps`

Build-Abhängigkeiten nicht lokal installieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--working-copy`

Drush: Verwenden Sie Git, um ein Repository jedes Drupal-Moduls zu klonen, anstatt einfach eine Version herunterzuladen

- Standard: `false`
- Akzeptiert keinen Wert

### `--concurrency`

Drush: Legen Sie die Anzahl der gleichzeitigen Projekte fest, die gleichzeitig verarbeitet werden

- Standard: `4`
- Erfordert einen Wert

### `--lock`

Drush: Sperrdatei erstellen oder aktualisieren (nur verfügbar mit Drush Version 7+)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `local:dir`

Suchen des lokalen Projektstamms

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

Der zu suchende Unterordner (&#39;local&#39;, &#39;web&#39; oder &#39;shared&#39;)


### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:all`

Anzeigen von CPU-, Datenträger- und Arbeitsspeichermetriken für eine Umgebung

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zum Endzeitpunkt (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder höher (je nach Projekt), Standard \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Die Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den neuesten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Nach Service- oder Anwendungsnamen filtern Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern Sie nach Service-Typ (wenn —service nicht angegeben ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Zeitstempel*, Service*, CPU_Percent*, MEM_Percent*, Disk_Percent*, TMP_Disk_Percent*, CPU_Limit, CPU_Used, Disk_Limit, Disk_Used, Inodes_Limit, Inodes_Percent, Inodes_Used, MEM_Limit, MEM_Used, TMP_Disk_Limit, TMP_Disk_Used, TMP_Inodes_Limit, TMP_Inodes_Percent, TMP_Inodes_Used, Typ (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:cpu`

CPU-Auslastung einer Umgebung anzeigen

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zum Endzeitpunkt (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder höher (je nach Projekt), Standard \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Die Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den neuesten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Nach Service- oder Anwendungsnamen filtern Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern Sie nach Service-Typ (wenn —service nicht angegeben ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Zeitstempel*, Dienst*, Verwendet*, Limit*, Prozent*, Typ (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:disk-usage`

Anzeigen der Festplattenauslastung einer Umgebung

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zum Endzeitpunkt (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder höher (je nach Projekt), Standard \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Die Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den neuesten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Nach Service- oder Anwendungsnamen filtern Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern Sie nach Service-Typ (wenn —service nicht angegeben ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--tmp`

Bericht zur temporären Festplattenauslastung (zeigt die Spalten: Zeitstempel, Dienst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Zeitstempel*, Dienst*, Verwendet*, Limit*, Prozent*, ipercent*, tmp_percent*, limit, iused, tmp_limit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, Typ (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:memory`

Anzeigen der Speichernutzung einer Umgebung

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zum Endzeitpunkt (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder höher (je nach Projekt), Standard \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Die Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den neuesten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Nach Service- oder Anwendungsnamen filtern Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern Sie nach Service-Typ (wenn —service nicht angegeben ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Zeitstempel*, Dienst*, Verwendet*, Limit*, Prozent*, Typ (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:download`

Dateien von einem Mount herunterladen, mithilfe von rsync

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Download von allen Mounts

- Standard: `false`
- Akzeptiert keinen Wert

### `--mount`, `-m`

Die Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

### `--target`

Das Verzeichnis, in das die Dateien heruntergeladen werden. Wenn —all verwendet wird, wird der Einhängepfad angehängt

- Erfordert einen Wert

### `--source-path`

Verwenden Sie den Quellpfad des Mount (anstelle des Mount-Pfads) als Unterverzeichnis des Ziels, wenn —all verwendet wird

- Standard: `false`
- Akzeptiert keinen Wert

### `--delete`

Ob irrelevante Dateien im Zielverzeichnis gelöscht werden sollen

- Standard: `false`
- Akzeptiert keinen Wert

### `--exclude`

Datei(en) vom Download ausschließen (Muster)

- Standard: `[]`
- Erfordert einen Wert

### `--include`

Nicht auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:list`

Abrufen einer Liste der Reittiere

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Ausgabe nur der Einhängepfade (einer pro Zeile)

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Definition, Pfad. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:size`

Überprüfen der Festplattenauslastung der Bereitstellungen

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Aktualisieren des Cache

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Verfügbar, Max, Einhängevorrichtungen, percent_used, Größen, verwendet. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:upload`

Dateien mithilfe von rsync auf eine Bereitstellung hochladen

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

Ein Verzeichnis mit Dateien zum Hochladen

- Erfordert einen Wert

### `--mount`, `-m`

Die Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

### `--delete`

Gibt an, ob irrelevante Dateien im Mount gelöscht werden sollen

- Standard: `false`
- Akzeptiert keinen Wert

### `--exclude`

Datei(en) vom Upload ausschließen (Muster)

- Standard: `[]`
- Erfordert einen Wert

### `--include`

Nicht auszuschließende Datei(en) (Muster)

- Standard: `[]`
- Erfordert einen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--instance`, `-I`

Eine Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `operation:list`

Auflisten von Laufzeitvorgängen für eine Umgebung

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Die Länge des anzuzeigenden Befehls nicht begrenzen. Der Standardwert ist 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: service*, name*, start*, role, stop (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `operation:run`

Ausführen eines Vorgangs in der Umgebung

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Der Vorgangsname


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Ein Worker-Name

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:clear-build-cache`

Löschen des Build-Cache eines Projekts

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:get`

Lokales Klonen eines Projekts

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

Die Projekt-ID


### `directory`

Das Verzeichnis, in das geklont werden soll. Standardmäßig wird der Projekttitel verwendet


### `--environment`, `-e`

Die zu klonende Umgebungskennung. Die Standardeinstellung ist der Projektstandard oder die erste verfügbare Umgebung.

- Erfordert einen Wert

### `--depth`

Einen flachen Klon erstellen: Begrenzt die Anzahl der Commits im Verlauf.

- Erfordert einen Wert

### `--build`

Erstellen des Projekts nach dem Klonen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:info`

Lesen oder Festlegen von Eigenschaften für ein Projekt

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Legen Sie einen neuen Wert für die Eigenschaft fest


### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:list`

Abrufen einer Liste aller aktiven Projekte

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Ausgabe einer einfachen Liste von Projekt-IDs. Deaktiviert die Paginierung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--region`

Nach Region filtern (exakte Übereinstimmung)

- Erfordert einen Wert

### `--title`

Nach Titel filtern (Suche ohne Unterscheidung von Groß- und Kleinschreibung)

- Erfordert einen Wert

### `--my`

Nur die Projekte anzeigen, deren Inhaber Sie sind

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Ob die Liste aktualisiert werden soll

- Standard: `1`
- Erfordert einen Wert

### `--sort`

Eine Eigenschaft zum Sortieren nach

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

In umgekehrter (absteigender) Reihenfolge sortieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--page`

Seitennummer. Dies ermöglicht die Paginierung, trotz Konfiguration oder —count. Ignoriert, wenn —pipe angegeben ist.

- Erfordert einen Wert

### `--count`, `-c`

Die Anzahl der pro Seite anzuzeigenden Projekte Verwenden Sie 0, um die Paginierung zu deaktivieren. Ignoriert, wenn —page angegeben wurde.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`

Anzuzeigende Spalten. Verfügbare Spalten: id*, title*, region*, created_at, organization_id, organization_label, organization_name, Status (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:set-remote`

Festlegen des Remote-Projekts für das aktuelle Git-Repository

```bash
magento-cloud set-remote [<project>]
```


### `project`

Die Projekt-ID


### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:cat`

Lesen einer Datei im Projekt-Repository

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

Der Pfad zur Datei

- Erforderlich

### `--commit`, `-c`

Der Commit SHA. Dies kann auch &quot;HEAD&quot; und Caret-Suffixe (^) oder Tilde-Suffixe (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:ls`

Auflisten der Dateien im Projekt-Repository

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Der Pfad zu einem Unterverzeichnis


### `--directories`, `-d`

Nur Ordner anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--files`, `-f`

Nur Dateien anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--git-style`

Stilausgabe ähnlich wie „git-tree“

- Standard: `false`
- Akzeptiert keinen Wert

### `--commit`, `-c`

Der Commit SHA. Dies kann auch &quot;HEAD&quot; und Caret-Suffixe (^) oder Tilde-Suffixe (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:read`

Lesen eines Verzeichnisses oder einer Datei im Projekt-Repository

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Der Pfad zum Verzeichnis oder zur Datei


### `--commit`, `-c`

Der Commit SHA. Dies kann auch &quot;HEAD&quot; und Caret-Suffixe (^) oder Tilde-Suffixe (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `route:get`

Anzeigen detaillierter Informationen zu einer Route

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

Die ursprüngliche URL der Route


### `--id`

Eine auszuwählende Routen-ID

- Erfordert einen Wert

### `--primary`, `-1`

Primäre Route auswählen

- Standard: `false`
- Akzeptiert keinen Wert

### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

### `--refresh`

Umgehen des Cache-Speichers von Routen

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert

### `--identity-file`, `-i`

[Veraltete Option, nicht mehr verwendet]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `route:list`

Auflisten aller Routen für eine Umgebung

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

Die Umgebungs-ID


### `--refresh`

Umgehen des Cache-Speichers von Routen

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: route*, type*, to*, url (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `self:install`

Installieren oder Aktualisieren von CLI-Konfigurationsdateien

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

Der Shell-Typ für die automatische Vervollständigung (bash oder zsh)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `self:update`

Aktualisieren der CLI auf die neueste Version

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Nur zwischen Nebenversionen oder Patch-Versionen aktualisieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--unstable`

Aktualisieren Sie auf eine neue instabile Version, falls verfügbar

- Standard: `false`
- Akzeptiert keinen Wert

### `--manifest`

Überschreiben des Speicherorts der Manifestdatei

- Erfordert einen Wert

### `--current-version`

Aktuelle Version überschreiben

- Erfordert einen Wert

### `--timeout`

Ein Timeout für die Versionsüberprüfung

- Standard: `30`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:list`

Auflisten der Services im Projekt

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Ausgabe nur einer Liste von Service-Namen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Datenträger, Name, Größe, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:dump`

Erstellen eines binären Archiv-Dump von Daten aus MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Die Sammlung, die abgelegt werden soll

- Erfordert einen Wert

### `--gzip`, `-z`

Komprimieren Sie den Dump mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:export`

Exportieren von Daten aus MongoDB

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Die zu exportierende Sammlung

- Erfordert einen Wert

### `--jsonArray`

Exportieren von Daten als einzelnes JSON-Array

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Der Exporttyp, z. B. „csv“

- Erfordert einen Wert

### `--fields`, `-f`

Die zu exportierenden Felder

- Standard: `[]`
- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:restore`

Wiederherstellen eines binären Archiv-Dump von Daten in MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Die wiederherzustellende Sammlung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:shell`

Verwenden der MongoDB-Shell

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Übergeben eines JavaScript-Fragments an die Shell

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:redis-cli`

Zugriff auf die Redis-CLI

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

Dem Redis-Befehl hinzuzufügende Argumente


### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:create`

Erstellen eines Snapshots einer Umgebung

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Die Umgebung


### `--live`

Live-Backup: Halten Sie die Umgebung nicht an. Wenn festgelegt, bleibt die Umgebung aktiv und steht während des Backups Verbindungen offen. Dadurch werden Ausfallzeiten reduziert, was das Risiko birgt, dass die Daten in einem inkonsistenten Zustand gesichert werden.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:delete`

Löschen eines Umgebungs-Snapshots

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Die ID des Snapshots. Erforderlich im nicht interaktiven Modus.


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:get`

Umgebungsschnappschuss anzeigen

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Die ID des Snapshots. Die Standardeinstellung ist die neueste .


### `--property`, `-P`

Die anzuzeigende Eigenschaft.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:list`

Verfügbare Momentaufnahmen einer Umgebung auflisten

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:restore`

Wiederherstellen eines Umgebungsschnappschusses

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

Der Name des Snapshots. Standardwert ist die neueste .


### `--target`

Die wiederherzustellende Umgebung. Standardmäßig wird die aktuelle Umgebung des Snapshots verwendet

- Erfordert einen Wert

### `--branch-from`

Wenn —target noch nicht vorhanden ist, wird hier das übergeordnete Element der neuen Umgebung angegeben

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `source-operation:list`

Auflisten von Quellvorgängen in einer Umgebung

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Die Länge des anzuzeigenden Befehls nicht begrenzen. Der Standardwert ist 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: App, Befehl, Vorgang. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `source-operation:run`

Ausführen eines Quellvorgangs

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Der Vorgangsname


### `--variable`

Eine Variable im Format \, die während des Vorgangs festgelegt werden soll.&lt;info>type:name=value\&lt;/info>

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-cert:load`

Erzeugen eines SSH-Zertifikats

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Aktualisieren Sie das Zertifikat nur, falls erforderlich (keine SSH-Konfiguration schreiben)

- Standard: `false`
- Akzeptiert keinen Wert

### `--new`

Aktualisierung des Zertifikats erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--new-key`

[Veraltet] Stattdessen —new verwenden

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-key:add`

Neuen SSH-Schlüssel hinzufügen

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

Der Pfad zu einem vorhandenen öffentlichen SSH-Schlüssel


### `--name`

Ein Name zur Identifizierung des Schlüssels

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-key:delete`

Löschen eines SSH-Schlüssels

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

Die ID des zu löschenden SSH-Schlüssels


### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-key:list`

Abrufen einer Liste von SSH-Schlüsseln in Ihrem Konto

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: ID*, Titel*, Pfad*, Fingerabdruck (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `subscription:info`

Lesen oder Ändern von Abonnementeigenschaften

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Legen Sie einen neuen Wert für die Eigenschaft fest


### `--id`, `-s`

Die Abonnement-ID

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-String)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:close`

SSH-Tunnel schließen

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Alle Tunnel schließen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:info`

Beziehungsinformationen für SSH-Tunnel anzeigen

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

Die anzuzeigende Beziehungseigenschaft

- Erfordert einen Wert

### `--encode`, `-c`

Ausgabe als base64-kodiertes JSON

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:list`

SSH-Tunnel auflisten

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`, `-a`

Alle Tunnel anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Port*, Projekt*, Umgebung*, App*, Beziehung*, URL (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:open`

Öffnen von SSH-Tunneln zu den Beziehungen einer App

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Zulassen, dass Remotehosts eine Verbindung zu lokalen weitergeleiteten Ports herstellen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:single`

Öffnen eines einzelnen SSH-Tunnels zu einer App-Beziehung

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Der lokale Port

- Erfordert einen Wert

### `--gateway-ports`, `-g`

Zulassen, dass Remotehosts eine Verbindung zu lokalen weitergeleiteten Ports herstellen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Service-Beziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine zu verwendende SSH-Identität (privater Schlüssel)

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:add`

Hinzufügen eines Benutzers zum Projekt

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--role`, `-r`

Projektrolle des Benutzers („Admin“ oder „Viewer„) oder Rolle des Umgebungstyps (z. B. „staging:contributor“ oder „production:viewer„). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf „Ohne„. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. „%:viewer„, um dem Benutzer die Rolle „viewer“ für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. „production:v„.

- Standard: `[]`
- Erfordert einen Wert

### `--force-invite`

Einladung senden, auch wenn bereits eine gesendet wurde

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:delete`

Löschen eines Benutzers aus dem Projekt

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

Die E-Mail-Adresse des Benutzers

- Erforderlich

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:get`

Benutzerrolle(n) anzeigen

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--level`, `-l`

Die Rollenebene („Projekt“ oder „Umgebung„)

- Erfordert einen Wert

### `--pipe`

Ausgabe der Rolle an stdout (nach Durchführung von Änderungen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--role`, `-r`

[Veraltet: Verwenden Sie user:update, um die Rolle(n) eines Benutzers zu ändern]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:list`

Auflisten der Projektbenutzer

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: email*, name*, role*, id*, granted_at, updated_at (* = Standardspalten). Das Zeichen „+“ kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:update`

Benutzerrolle(n) in einem Projekt aktualisieren

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--role`, `-r`

Projektrolle des Benutzers („Admin“ oder „Viewer„) oder Rolle des Umgebungstyps (z. B. „staging:contributor“ oder „production:viewer„). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf „Ohne„. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. „%:viewer„, um dem Benutzer die Rolle „viewer“ für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. „production:v„.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:create`

Erstellen einer Variablen

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

Der Variablenname


### `--update`, `-u`

Aktualisieren Sie die Variable, falls sie bereits existiert

- Standard: `false`
- Akzeptiert keinen Wert

### `--level`, `-l`

Die Ebene, auf der die Variable festgelegt werden soll (&#39;Projekt&#39; oder &#39;Umgebung&#39;)

- Erfordert einen Wert

### `--name`

Der Variablenname

- Erfordert einen Wert

### `--value`

Der Wert der Variablen

- Erfordert einen Wert

### `--json`

Ob der Variablenwert JSON-formatiert ist

- Standard: `false`
- Erfordert einen Wert

### `--sensitive`

Ob der Variablenwert sensibel ist

- Standard: `false`
- Erfordert einen Wert

### `--prefix`

Das Präfix des Variablennamens, das dessen Typ bestimmen kann, z. B. „env„. Nur anwendbar, wenn der Name noch kein Präfix enthält. (z. B. „none“ oder „env:„)

- Standard: `none`
- Erfordert einen Wert

### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt wird

- Standard: `true`
- Erfordert einen Wert

### `--visible-build`

Ob die Variable zur Erstellungszeit sichtbar sein soll

- Erfordert einen Wert

### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:delete`

Löschen einer Variablen

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Variablenname

- Erforderlich

### `--level`, `-l`

Variablenebene (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; oder &#39;e&#39;)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:get`

Anzeigen einer Variablen

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

Der Name der Variablen


### `--property`, `-P`

Anzeigen einer einzelnen Variableneigenschaft

- Erfordert einen Wert

### `--level`, `-l`

Variablenebene (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; oder &#39;e&#39;)

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--pipe`

[Veraltete Option] Nur den Variablenwert ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:list`

Listenvariablen

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`, `-l`

Variablenebene (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; oder &#39;e&#39;)

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: is_enabled, level, name, value. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:update`

Aktualisieren einer Variablen

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Variablenname

- Erforderlich

### `--allow-no-change`

Erfolgreiche Rückgabe (kein Exitcode), wenn keine Änderungen angegeben wurden

- Standard: `false`
- Akzeptiert keinen Wert

### `--level`, `-l`

Variablenebene (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; oder &#39;e&#39;)

- Erfordert einen Wert

### `--value`

Der Wert der Variablen

- Erfordert einen Wert

### `--json`

Ob der Variablenwert JSON-formatiert ist

- Standard: `false`
- Erfordert einen Wert

### `--sensitive`

Ob der Variablenwert sensibel ist

- Standard: `false`
- Erfordert einen Wert

### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt wird

- Standard: `true`
- Erfordert einen Wert

### `--visible-build`

Ob die Variable zur Erstellungszeit sichtbar sein soll

- Erfordert einen Wert

### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `worker:list`

Abrufen einer Liste aller bereitgestellten Worker

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Ausgabe nur einer Liste der Arbeitskräftenamen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungskennung. Verwenden Sie „.“ , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder Nur

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten. Verfügbare Spalten: Befehle, Name, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. „a,b,c„) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Tabellenüberschrift nicht ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Erhöhen der Ausführlichkeit von Nachrichten

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Bestätigungsfragen mit „Ja“ beantworten; Standardwert für andere Fragen akzeptieren; Interaktion deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert

