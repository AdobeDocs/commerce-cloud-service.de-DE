---
source-git-commit: c160be020d855983eaf7a06d04cee6e27819b2a0
workflow-type: tm+mt
source-wordcount: '21467'
ht-degree: 0%

---
# Magento-Cloud (Adobe Commerce über Cloud-Infrastruktur)

<!-- The template to render with above values -->
**Version**: 1.46.1

Diese Referenz enthält 119 Befehle, die über das `magento-cloud` Befehlszeilen-Tool.
Die anfängliche Liste wird automatisch mit der Variablen `magento-cloud list` in Adobe Commerce in der Cloud-Infrastruktur.

>[!NOTE]
>
>Diese Referenz wird aus der Anwendungs-Codebase generiert. Um den Inhalt zu ändern, können Sie den Quellcode für die entsprechende Befehlsimplementierung im [codebase](https://github.com/magento/magento-cloud-cli) Repository erstellen und Ihre Änderungen zur Überprüfung einreichen. Eine andere Möglichkeit ist, _Feedback geben_ (finden Sie den Link oben rechts). Beitragsrichtlinien finden Sie unter [Codebeiträge](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `decode`

Dekodieren einer kodierten Zeichenfolge wie MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

Der zu dekodierende Variablenwert

- Erforderlich

### `--property`, `-P`

Die Eigenschaft, die in der -Variablen angezeigt werden soll

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `docs`

Öffnen Sie die Online-Dokumentation

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Suchbegriff(e)

- Standard: `[]`

- Array

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `help`

Zeigt Hilfe für einen Befehl an

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

Ausgabe der Rohbefehl-Hilfe

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

So geben Sie die unformatierte Befehlsliste aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Fahren Sie mit der Ausführung von Befehlen fort, selbst wenn eine Ausnahme aufgetreten ist.

- Standard: `false`
- Akzeptiert keinen Wert

### `--sort`

Eine Eigenschaft zum Sortieren der Liste der Projektoptionen

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

Reihenfolge der Projektoptionen umkehren

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:cancel`

Aktivität abbrechen

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste stornierbare Aktivität.


### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:get`

Detaillierte Informationen zu einer einzelnen Aktivität anzeigen

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Aktivität.


### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

### `--type`, `-t`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--state`

Filtern nach Status (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder cancelled. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

### `--incomplete`, `-i`

Schließen Sie nur unvollständige Aktivitäten ein (bei Auswahl einer Standardaktivität). Dies ist eine Kurzschrift für \&lt;info>—state=in_progress,pending\&lt;/info>

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:list`

Liste der Aktivitäten für eine Umgebung oder ein Projekt abrufen

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Filteraktivitäten nach Typ Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann &quot;cron&quot;Aktivitäten vom Typ &quot;environment.cron&quot;auswählen. Die Zeichen % oder * können als Platzhalter verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Aktivitäten nach Typ ausschließen Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Der erste Teil des Aktivitätsnamens kann weggelassen werden, z. B. kann &quot;cron&quot;Aktivitäten vom Typ &quot;environment.cron&quot;ausschließen. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

### `--start`

Es werden nur Aktivitäten aufgelistet, die vor diesem Datum erstellt wurden

- Erfordert einen Wert

### `--state`

Aktivitäten nach Status filtern: in_progress, pending, complete oder abgebrochen. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Aktivitäten nach Ergebnis filtern: Erfolg oder Fehler

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

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, created*, description*, progress*, state*, result*, completed, environment, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `activity:log`

Protokoll für eine Aktivität anzeigen

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Aktivität.


### `--refresh`

Intervall für die Aktivitätsaktualisierung (Sekunden). Auf 0 setzen, um die Aktualisierung zu deaktivieren.

- Standard: `3`
- Erfordert einen Wert

### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Filtern nach Typ (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter für den Typ verwendet werden, z. B. &#39;%var%&#39; zur Auswahl variablenbezogener Aktivitäten.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Nach Typ ausschließen (bei Auswahl einer Standardaktivität). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--state`

Filtern nach Status (bei Auswahl einer Standardaktivität): in_progress, pending, complete oder cancelled. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Filtern nach Ergebnis (bei Auswahl einer Standardaktivität): Erfolg oder Fehler

- Erfordert einen Wert

### `--incomplete`, `-i`

Schließen Sie nur unvollständige Aktivitäten ein (bei Auswahl einer Standardaktivität). Dies ist eine Kurzschrift für \&lt;info>—state=in_progress,pending\&lt;/info>

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`, `-a`

Prüfung der letzten Aktivitäten in allen Umgebungen (bei Auswahl einer Standardaktivität)

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `app:config-get`

Konfiguration einer App anzeigen

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Nur Liste mit App-Namen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: name*, type*, disk, path, size (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:api-token-login`

Bei der Magento Cloud über ein API-Token anmelden

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:browser-login`

Bei der Magento Cloud über einen Browser anmelden

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Melden Sie sich erneut an, auch wenn Sie bereits angemeldet sind

- Standard: `false`
- Akzeptiert keinen Wert

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `auth:logout`

Aus Magento Cloud abmelden

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Abmelden von allen lokalen Sitzungen

- Standard: `false`
- Akzeptiert keinen Wert

### `--other`

Abmelden von anderen lokalen Sitzungen

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Server-ID

- Erfordert einen Wert

### `--server_token`

Server-Token

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Der Pfad zur Datei mit dem privaten Zertifikatschlüssel

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatskettendatei

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:delete`

Zertifikat aus dem Projekt löschen

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

Die Zertifikatkennung (oder der Anfang)

- Erforderlich

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:get`

Zertifikat anzeigen

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

Die Zertifikatkennung (oder der Anfang)

- Erforderlich

### `--property`, `-P`

Die anzuzeigende Zertifikateigenschaft

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `certificate:list`

Projektzertifikate auflisten

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Filtern nach Domain-Namen (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

- Erfordert einen Wert

### `--exclude-domain`

Zertifikate ausschließen, die mit dem Domänennamen übereinstimmen (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

- Erfordert einen Wert

### `--issuer`

Nach Emittenten filtern

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

Sowohl abgelaufene als auch nicht abgelaufene Zertifikate anzeigen

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

Nur eine Liste der Domänennamen zurückgeben, die von den Zertifikaten abgedeckt sind

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: erstellt, Domänen, abgelaufen, ID, Aussteller. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Standard: `HEAD`


### `--property`, `-P`

Die angezeigte commit-Eigenschaft.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `commit:list`

Auflisten von Commits

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

Das Git-Commit-SHA für den Start. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.


### `--limit`

Die Anzahl der anzuzeigenden Commits.

- Standard: `10`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: author, date, sha, summary. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `db:dump`

Lokalen Dump der Remote-Datenbank erstellen

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

Das Schema, das abgelegt werden soll. Unterlassen der Verwendung des Standardschemas (normalerweise &quot;main&quot;).

- Erfordert einen Wert

### `--file`, `-f`

Ein benutzerdefinierter Dateiname für die Ablage

- Erfordert einen Wert

### `--directory`, `-d`

Ein benutzerdefiniertes Verzeichnis für den Dump

- Erfordert einen Wert

### `--gzip`, `-z`

Komprimieren Sie die Ablage mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

### `--timestamp`, `-t`

Fügen Sie einen Zeitstempel zum Dateinamen der Dump-Datei hinzu.

- Standard: `false`
- Akzeptiert keinen Wert

### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

### `--table`

Zu berücksichtigende Tabelle(n)

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-table`

Auszuschließende Tabelle

- Standard: `[]`
- Erfordert einen Wert

### `--schema-only`

Nur Schemas ablegen, keine Daten

- Standard: `false`
- Akzeptiert keinen Wert

### `--charset`

Die Zeichensatzkodierung für die Dump

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Zeigt Größen in Byte an.

- Standard: `false`
- Akzeptiert keinen Wert

### `--cleanup`, `-C`

Überprüfen Sie, ob Tabellen bereinigt werden können, und zeigen Sie mir Empfehlungen an (nur InnoDb).

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: max, percent_used, used. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Rohe, nicht tabellarische Ausgabe erzeugen

- Standard: `false`
- Akzeptiert keinen Wert

### `--schema`

Das zu verwendende Schema. Unterlassen der Verwendung des Standardschemas (normalerweise &quot;main&quot;). Übergeben Sie eine leere Zeichenfolge, um kein Schema zu verwenden.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:add`

Hinzufügen einer neuen Domäne zum Projekt

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domänenname

- Erforderlich

### `--cert`

Der Pfad zur Zertifikatdatei für diese Domäne

- Erfordert einen Wert

### `--key`

Der Pfad zur privaten Schlüsseldatei für das angegebene Zertifikat.

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatskettendatei(en) für das bereitgestellte Zertifikat

- Standard: `[]`
- Erfordert einen Wert

### `--attach`

Die Produktionsdomäne, die diese in den Routen der Umgebung ersetzt. Erforderlich für Nicht-Produktions-Umgebungsdomänen.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:delete`

Eine Domäne aus dem Projekt löschen

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domänenname

- Erforderlich

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:get`

Detaillierte Informationen für eine Domäne anzeigen

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

Der Domänenname


### `--property`, `-P`

Die anzuzeigende Domäneneigenschaft

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:list`

Liste aller Domänen abrufen

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: name*, ssl*, created_at*, registered_name, replacement_for, type, updated_at (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `domain:update`

Domain aktualisieren

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Domänenname

- Erforderlich

### `--cert`

Der Pfad zur Zertifikatdatei für diese Domäne

- Erfordert einen Wert

### `--key`

Der Pfad zur privaten Schlüsseldatei für das angegebene Zertifikat.

- Erfordert einen Wert

### `--chain`

Der Pfad zur Zertifikatskettendatei(en) für das bereitgestellte Zertifikat

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Zu aktivierende Umgebung(n)

- Standard: `[]`

- Array

### `--parent`

Festlegen einer neuen übergeordneten Umgebung vor der Aktivierung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:branch`

Verzweigung einer Umgebung

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die ID der Umgebung, die ausgecheckt werden soll. Beispiel: &quot;sprint2&quot;


### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die zu löschenden Umgebungen. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`

- Array

### `--delete-branch`

Löschen von Git-Zweigen für inaktive Umgebungen ohne Bestätigung

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-delete-branch`

Löschen Sie keine Git-Verzweigungen (inaktive Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Löschen Sie alle Umgebungen eines Typs (Hinzufügung zu anderen ausgewählten Umgebungen) Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--only-type`, `-t`

Nur Löschumgebungen eines bestimmten Typs Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen getrennt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude`

Umgebung(en), die nicht gelöscht werden soll. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`

Umgebungstypen, deren Werte nicht gelöscht werden sollen, können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--inactive`

Löschen Sie alle inaktiven Umgebungen (Hinzufügung zu allen anderen ausgewählten Umgebungen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--merged`

Löschen Sie alle zusammengeführten Umgebungen (Hinzufügen zu allen anderen ausgewählten Umgebungen)

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:http-access`

Aktualisieren von HTTP-Zugriffseinstellungen für eine Umgebung

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Zugriffsbeschränkungen im Format &quot;permission:address&quot;. Verwenden Sie 0, um alle Adressen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

### `--auth`

HTTP Basic auth credentials im Format &quot;username:password&quot;. Verwenden Sie 0, um alle Berechtigungen zu löschen.

- Standard: `[]`
- Erfordert einen Wert

### `--enabled`

Ob die Zugriffskontrolle aktiviert werden soll: 1 zur Aktivierung, 0 zur Deaktivierung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:info`

Eigenschaften für eine Umgebung lesen oder festlegen

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Neuen Wert für die Eigenschaft festlegen


### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Eine URL zum Git-Repository

- Erforderlich

### `--profile`

Der Name des Profils

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:list`

Liste der Umgebungen abrufen

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Inaktive Umgebungen nicht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Geben Sie eine einfache Liste von Umgebungs-IDs aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Ob die Liste aktualisiert werden soll.

- Standard: `1`
- Erfordert einen Wert

### `--sort`

Eine Eigenschaft, die nach

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

Sortieren in umgekehrter (absteigender) Reihenfolge

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Filtern Sie die Liste nach Umgebungstyp(en). Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, status*, type*, created, machine_name, updated (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:logs`

Protokolle einer Umgebung lesen

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

Der Protokolltyp, z. B. &quot;access&quot; oder &quot;error&quot;


### `--lines`

Die Anzahl der anzuzeigenden Zeilen

- Standard: `100`
- Erfordert einen Wert

### `--tail`

Kontinuierliches Verfolgen des Protokolls

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die zusammenzuführende Umgebung


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:pause`

Anhalten einer Umgebung

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:push`

Push-Code in eine Umgebung

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

Die Quell-Referenz: ein Zweigname oder Commit-Hash

- Standard: `HEAD`


### `--target`

Der Name der Zielverzweigung. Die Standardeinstellung ist der aktuelle Zweig.

- Erfordert einen Wert

### `--force`, `-f`

Nicht-schnelle Aktualisierungen zulassen

- Standard: `false`
- Akzeptiert keinen Wert

### `--force-with-lease`

Nicht-schnelle Aktualisierungen zulassen, wenn die Remote-Tracking-Verzweigung auf dem neuesten Stand ist

- Standard: `false`
- Akzeptiert keinen Wert

### `--set-upstream`, `-u`

Legen Sie die Zielumgebung als Upstream für die Quellverzweigung fest. Dadurch wird auch das Zielprojekt als Remote für das lokale Repository festgelegt.

- Standard: `false`
- Akzeptiert keinen Wert

### `--activate`

Aktivieren der Umgebung vor dem Pushen

- Standard: `false`
- Akzeptiert keinen Wert

### `--parent`

Festlegen der neuen übergeordneten Umgebung (nur mit —activate verwendet)

- Erfordert einen Wert

### `--type`

Umgebungstyp festlegen (nur mit —activate verwendet)

- Erfordert einen Wert

### `--no-clone-parent`

Klonen Sie nicht die Daten des übergeordneten Zweigs (nur mit —activate verwendet)

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:redeploy`

Bereitstellung einer Umgebung

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:relationships`

Anzeigen der Beziehungen einer Umgebung

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

Umwelt


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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:resume`

Fortsetzen einer angehaltenen Umgebung

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Zu kopierende Dateien. Verwenden Sie das Präfix remote: , um Remote-Standorte zu definieren.

- Standard: `[]`

- Array

### `--recursive`, `-r`

rekursiv ganze Verzeichnisse kopieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:ssh`

SSH in die aktuelle Umgebung

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Ein Befehl zum Ausführen in der Umgebung.

- Standard: `[]`

- Array

### `--pipe`

Geben Sie nur die SSH-URL aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--all`

Geben Sie alle SSH-URLs (für jede App) aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:synchronize`

Synchronisieren des Codes und/oder der Daten einer Umgebung von der übergeordneten Umgebung

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

Was synchronisiert werden soll: &quot;code&quot;, &quot;data&quot; oder beides

- Standard: `[]`

- Array

### `--rebase`

Synchronisieren Sie den Code durch Rebasing anstelle der Zusammenführung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Gibt nur die URL für die primäre Route zurück

- Standard: `false`
- Akzeptiert keinen Wert

### `--browser`

Der zum Öffnen der URL zu verwendende Browser. Legen Sie 0 für keine fest.

- Erfordert einen Wert

### `--pipe`

Geben Sie die URL für stdout aus.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `environment:xdebug`

Öffnen Sie einen Tunnel zu Xdebug in der Umgebung

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:activity:get`

Detaillierte Informationen zu einer einzelnen Integrationsaktivität anzeigen

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `activity`

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Integrationsaktivität.


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

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:activity:list`

Liste der Aktivitäten für eine Integration abrufen

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--type`

Aktivitäten nach Typ filtern Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--exclude-type`, `-x`

Aktivitäten nach Typ ausschließen Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden. Die Zeichen % oder * können als Platzhalter zum Ausschließen von Typen verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--limit`

Anzahl der angezeigten Ergebnisse begrenzen

- Standard: `10`
- Erfordert einen Wert

### `--start`

Es werden nur Aktivitäten aufgelistet, die vor diesem Datum erstellt wurden

- Erfordert einen Wert

### `--state`

Filtern von Aktivitäten nach Status. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--result`

Aktivitäten nach Ergebnis filtern

- Erfordert einen Wert

### `--incomplete`, `-i`

Nur unvollständige Aktivitäten auflisten

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, created*, description*, type*, state*, result*, completed (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Aktivitäts-ID. Die Standardeinstellung ist die neueste Integrationsaktivität.


### `--timestamps`, `-t`

Zeitstempel neben jeder Nachricht anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;.

- Erfordert einen Wert

### `--base-url`

Die Basis-URL der Serverinstallation

- Erfordert einen Wert

### `--bitbucket-url`

Die Basis-URL der Bitbucket Server-Installation

- Erfordert einen Wert

### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

### `--token`

Ein Authentifizierungs- oder Zugriffstoken für die Integration

- Erfordert einen Wert

### `--key`

Ein Bitbucket OAuth-Verbraucherschlüssel

- Erfordert einen Wert

### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

### `--license-key`

Der New Relic Logs-Lizenzschlüssel

- Erfordert einen Wert

### `--server-project`

Das Projekt (z. B. &quot;namespace/repo&quot;)

- Erfordert einen Wert

### `--repository`

Das zu verfolgende Repository (z. B. &quot;owner/repository&quot;)

- Erfordert einen Wert

### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests`

Erstellen jeder Pull-Anforderung als Umgebung

- Standard: `true`
- Erfordert einen Wert

### `--build-draft-pull-requests`

Erstellen von Entwurfs-Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests-post-merge`

Pull-Anforderungen basierend auf ihrem Postzusammenführungsstatus erstellen

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

Daten der übergeordneten Umgebung für Pull-Anforderungen klonen

- Standard: `true`
- Erfordert einen Wert

### `--resync-pull-requests`

Synchronisieren von Umgebungsdaten für Pull-Anforderungen bei jedem Build

- Standard: `false`
- Erfordert einen Wert

### `--fetch-branches`

Abrufen aller Zweige aus der Remote-Umgebung (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

### `--prune-branches`

Löschen von Zweigen, die nicht auf der Remote-Site vorhanden sind

- Standard: `true`
- Erfordert einen Wert

### `--resources-init`

Die Ressourcen, die beim Initialisieren eines neuen Dienstes verwendet werden sollen (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Erfordert einen Wert

### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

### `--shared-key`

Webhook: der gemeinsame JWS-geheime Schlüssel

- Erfordert einen Wert

### `--file`

Der Name einer lokalen Datei mit dem hochzuladenden Skript

- Erfordert einen Wert

### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

### `--states`

Eine Liste der Status, auf die reagiert werden soll, z. B. ausstehend, in_progress, complete

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

[Optional] Benutzerdefinierte Absenderadresse für Warnhinweis-E-Mails

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

Die Kategorie Sumo Logic , die zum Filtern verwendet wird

- Erfordert einen Wert

### `--index`

Splunk-Index

- Erfordert einen Wert

### `--sourcetype`

Splunk-Ereignistyp

- Erfordert einen Wert

### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

### `--syslog-host`

Syslog-Relais/Collector-Host

- Erfordert einen Wert

### `--syslog-port`

Syslog Relais/Collector Port

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

HTTP-Header zur Verwendung in POST-Anfragen. Trennen Sie Namen und Werte durch einen Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:delete`

Integration aus einem Projekt löschen

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Die Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:get`

Details einer Integration anzeigen

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Eine Integrations-ID. Leer lassen, um aus einer Liste auszuwählen.


### `--property`, `-P`

Die anzuzeigende Integrationseigenschaft

- Akzeptiert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:list`

Liste der Projektintegration(n) anzeigen

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: ID, Zusammenfassung, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:update`

Integration aktualisieren

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Die ID der zu aktualisierenden Integration


### `--type`

Der Integrationstyp (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;.

- Erfordert einen Wert

### `--base-url`

Die Basis-URL der Serverinstallation

- Erfordert einen Wert

### `--bitbucket-url`

Die Basis-URL der Bitbucket Server-Installation

- Erfordert einen Wert

### `--username`

Der Benutzername des Bitbucket-Servers

- Erfordert einen Wert

### `--token`

Ein Authentifizierungs- oder Zugriffstoken für die Integration

- Erfordert einen Wert

### `--key`

Ein Bitbucket OAuth-Verbraucherschlüssel

- Erfordert einen Wert

### `--secret`

Ein Bitbucket OAuth-Kundengeheimnis

- Erfordert einen Wert

### `--license-key`

Der New Relic Logs-Lizenzschlüssel

- Erfordert einen Wert

### `--server-project`

Das Projekt (z. B. &quot;namespace/repo&quot;)

- Erfordert einen Wert

### `--repository`

Das zu verfolgende Repository (z. B. &quot;owner/repository&quot;)

- Erfordert einen Wert

### `--build-merge-requests`

GitLab: Erstellen von Zusammenführungsanfragen als Umgebungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests`

Erstellen jeder Pull-Anforderung als Umgebung

- Standard: `true`
- Erfordert einen Wert

### `--build-draft-pull-requests`

Erstellen von Entwurfs-Pull-Anforderungen

- Standard: `true`
- Erfordert einen Wert

### `--build-pull-requests-post-merge`

Pull-Anforderungen basierend auf ihrem Postzusammenführungsstatus erstellen

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

Daten der übergeordneten Umgebung für Pull-Anforderungen klonen

- Standard: `true`
- Erfordert einen Wert

### `--resync-pull-requests`

Synchronisieren von Umgebungsdaten für Pull-Anforderungen bei jedem Build

- Standard: `false`
- Erfordert einen Wert

### `--fetch-branches`

Abrufen aller Zweige aus der Remote-Umgebung (als inaktive Umgebungen)

- Standard: `true`
- Erfordert einen Wert

### `--prune-branches`

Löschen von Zweigen, die nicht auf der Remote-Site vorhanden sind

- Standard: `true`
- Erfordert einen Wert

### `--resources-init`

Die Ressourcen, die beim Initialisieren eines neuen Dienstes verwendet werden sollen (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Erfordert einen Wert

### `--url`

Die URL oder der API-Endpunkt für die Integration

- Erfordert einen Wert

### `--shared-key`

Webhook: der gemeinsame JWS-geheime Schlüssel

- Erfordert einen Wert

### `--file`

Der Name einer lokalen Datei mit dem hochzuladenden Skript

- Erfordert einen Wert

### `--events`

Eine Liste der Ereignisse, auf die reagiert werden soll, z. B. environment.push

- Standard: `*`
- Erfordert einen Wert

### `--states`

Eine Liste der Status, auf die reagiert werden soll, z. B. ausstehend, in_progress, complete

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

[Optional] Benutzerdefinierte Absenderadresse für Warnhinweis-E-Mails

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

Die Kategorie Sumo Logic , die zum Filtern verwendet wird

- Erfordert einen Wert

### `--index`

Splunk-Index

- Erfordert einen Wert

### `--sourcetype`

Splunk-Ereignistyp

- Erfordert einen Wert

### `--protocol`

Syslog-Transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Erfordert einen Wert

### `--syslog-host`

Syslog-Relais/Collector-Host

- Erfordert einen Wert

### `--syslog-port`

Syslog Relais/Collector Port

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

HTTP-Header zur Verwendung in POST-Anfragen. Trennen Sie Namen und Werte durch einen Doppelpunkt (:).

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `integration:validate`

Bestehende Integration validieren

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `local:build`

Aktuelles Projekt lokal erstellen

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Zu erstellende Anwendung(en) angeben

- Standard: `[]`

- Array

### `--abslinks`, `-a`

Absolute Links verwenden

- Standard: `false`
- Akzeptiert keinen Wert

### `--source`, `-s`

Das Quellverzeichnis. Die Standardeinstellung ist der aktuelle Projektstamm.

- Erfordert einen Wert

### `--destination`, `-d`

Das Ziel, mit dem der Webstamm jeder App symverknüpft wird. Standard: _www

- Erfordert einen Wert

### `--copy`, `-c`

Kopieren Sie in ein Build-Verzeichnis, anstatt symlink aus der Quelle zu verwenden.

- Standard: `false`
- Akzeptiert keinen Wert

### `--clone`

Verwenden Sie Git, um die aktuelle HEAD in den Build-Ordner zu klonen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--run-deploy-hooks`

Ausführen von &quot;deploy&quot;und/oder &quot;post_deploy&quot;

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-clean`

Alte Builds nicht entfernen

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-archive`

Erstellen oder Verwenden Sie kein Build-Archiv

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-backup`

vorherigen Build nicht sichern

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-cache`

Zwischenspeicherung deaktivieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-build-hooks`

Führen Sie keine Post-Build-Hooks aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-deps`

Build-Abhängigkeiten nicht lokal installieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--working-copy`

Entfernen: Verwenden Sie Git, um ein Repository jedes Drupal-Moduls zu klonen, anstatt einfach eine Version herunterzuladen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--concurrency`

DRush: Legen Sie die Anzahl gleichzeitiger Projekte fest, die gleichzeitig verarbeitet werden.

- Standard: `4`
- Erfordert einen Wert

### `--lock`

Löschen: Eine Sperrdatei erstellen oder aktualisieren (nur verfügbar mit DRush-Version 7+)

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `local:dir`

Lokalen Projektstamm suchen

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

Das zu suchende Unterverzeichnis (&#39;local&#39;, &#39;web&#39; oder &#39;shared&#39;)


### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:all`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Anzeigen von CPU-, Festplatten- und Speichermetriken für eine Umgebung

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder mehr (je nach Projekt), Standardeinstellung \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_used, tmp_inodes _limit, tmp_inodes_percent, tmp_inodes_used, Typ (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:cpu`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Anzeigen der CPU-Auslastung einer Umgebung

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder mehr (je nach Projekt), Standardeinstellung \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder mehr (je nach Projekt), Standardeinstellung \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--tmp`

Temporäre Festplattenauslastung melden (Spalten anzeigen: Zeitstempel, Dienst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `metrics:memory`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Speichernutzung einer Umgebung anzeigen

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--range`, `-r`

Der Zeitraum. Metriken werden für diese Dauer bis zur Endzeit (—to) geladen. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>5m\&lt;/comment>, Maximum \&lt;comment>8h\&lt;/comment> oder mehr (je nach Projekt), Standardeinstellung \&lt;comment>10m\&lt;/comment>.

- Erfordert einen Wert

### `--interval`, `-i`

Das Zeitintervall. Die Standardeinstellung ist eine Division des Bereichs. Sie können Einheiten angeben: Stunden (h), Minuten (m) oder Sekunden (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Erfordert einen Wert

### `--to`

Endzeit. Die Standardeinstellung ist jetzt.

- Erfordert einen Wert

### `--latest`, `-1`

Nur den letzten einzelnen Datenpunkt anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--service`, `-s`

Filtern nach Dienst- oder Anwendungsnamen Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--type`

Filtern nach Diensttyp (wenn —service nicht bereitgestellt ist). Die Version ist nicht erforderlich. Die Zeichen % oder * können als Platzhalter verwendet werden.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: timestamp*, service*, used*, limit*, percent*, type (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:download`

Herunterladen von Dateien von einem Rich-Rich-Rsync-Server

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Download von allen Reittieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--mount`, `-m`

Die -Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

### `--target`

Das Verzeichnis, in das die Dateien heruntergeladen werden. Wenn —all verwendet wird, wird der Bereitstellungspfad angehängt

- Erfordert einen Wert

### `--source-path`

Verwenden Sie den Quellpfad des Mount (anstelle des Bereitstellungspfads) als Unterverzeichnis des Ziels, wenn —all verwendet wird.

- Standard: `false`
- Akzeptiert keinen Wert

### `--delete`

Ob irrelevante Dateien im Zielverzeichnis gelöscht werden

- Standard: `false`
- Akzeptiert keinen Wert

### `--exclude`

Vom Download auszuschließende Datei(en) (Muster)

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:list`

Liste der Reittiere abrufen

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Geben Sie nur die Bereitstellungspfade aus (1 pro Zeile)

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Definition, Pfad. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:size`

Überprüfen Sie die Festplattenauslastung der Bereitstellungen.

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Größen in Byte anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--refresh`

Cache aktualisieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: verfügbar, max, mounts, percent_used, size, used. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `mount:upload`

Hochladen von Dateien in eine -Bereitstellung mithilfe von Rsync

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

Ein Verzeichnis mit hochzuladenden Dateien

- Erfordert einen Wert

### `--mount`, `-m`

Die -Bereitstellung (als App-relativer Pfad)

- Erfordert einen Wert

### `--delete`

Ob irrelevante Dateien im Bereitstellungsfenster gelöscht werden

- Standard: `false`
- Akzeptiert keinen Wert

### `--exclude`

Vom Hochladen auszuschließende Datei(en) (Muster)

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--instance`, `-I`

Instanz-ID

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `operation:list`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Auflisten von Laufzeitvorgängen in einer Umgebung

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Beschränken Sie nicht die Länge des anzuzeigenden Befehls. Der Standardwert beträgt 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: service*, name*, start*, role, stop (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `operation:run`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Ausführen eines Vorgangs für die Umgebung

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Der Vorgangsname


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--worker`

Arbeitername

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Das Verzeichnis, in das geklont werden soll. Die Standardeinstellung ist der Projekttitel


### `--environment`, `-e`

Die zu klonende Umgebungs-ID. Die Standardeinstellung ist die Projektnummer oder die erste verfügbare Umgebung.

- Erfordert einen Wert

### `--depth`

Erstellen eines flachen Klons: begrenzt die Anzahl der Commits im Verlauf

- Erfordert einen Wert

### `--build`

Erstellen des Projekts nach dem Klonen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:info`

Eigenschaften für ein Projekt lesen oder festlegen

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Neuen Wert für die Eigenschaft festlegen


### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:list`

Liste aller aktiven Projekte abrufen

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Geben Sie eine einfache Liste von Projekt-IDs aus. Deaktiviert die Paginierung.

- Standard: `false`
- Akzeptiert keinen Wert

### `--region`

Nach Region filtern (genaue Übereinstimmung)

- Erfordert einen Wert

### `--title`

Nach Titel filtern (Suche ohne Unterscheidung zwischen Groß- und Kleinschreibung)

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

Eine Eigenschaft, die nach

- Standard: `title`
- Erfordert einen Wert

### `--reverse`

Sortieren in umgekehrter (absteigender) Reihenfolge

- Standard: `false`
- Akzeptiert keinen Wert

### `--page`

Seitenzahl. Dies ermöglicht die Paginierung, trotz Konfiguration oder —count. Wird ignoriert, wenn —pipe angegeben ist.

- Erfordert einen Wert

### `--count`, `-c`

Die Anzahl der pro Seite anzuzeigenden Projekte. Verwenden Sie 0, um die Paginierung zu deaktivieren. Wird ignoriert, wenn —page angegeben ist.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, region*, created_at, organization_id, organization_label, organization_name, status (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `project:set-remote`

Remote-Projekt für das aktuelle Git-Repository festlegen

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:cat`

Datei im Projekt-Repository lesen

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

Der Pfad zur Datei

- Erforderlich

### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:ls`

Auflisten von Dateien im Projekt-Repository

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

Stilausgabe ähnlich &quot;git ls-tree&quot;

- Standard: `false`
- Akzeptiert keinen Wert

### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `repo:read`

Ordner oder Datei im Projekt-Repository lesen

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Der Pfad zum Verzeichnis oder zur Datei


### `--commit`, `-c`

Der Commit SHA. Dies kann auch Suffixe vom Typ &quot;HEAD&quot;und Caret (^) oder Tilde (~) für übergeordnete Commits akzeptieren.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Eine Route-ID zur Auswahl

- Erfordert einen Wert

### `--primary`, `-1`

Primäre Route auswählen

- Standard: `false`
- Akzeptiert keinen Wert

### `--property`, `-P`

Die anzuzeigende Eigenschaft

- Erfordert einen Wert

### `--refresh`

Den Zwischenspeicher von Routen umgehen

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `route:list`

Alle Routen für eine Umgebung auflisten

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

Die Umgebungs-ID


### `--refresh`

Den Zwischenspeicher von Routen umgehen

- Standard: `false`
- Akzeptiert keinen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: route*, type*, to*, url (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `self:update`

CLI auf die neueste Version aktualisieren

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Nur Aktualisierung zwischen kleineren oder Patch-Versionen

- Standard: `false`
- Akzeptiert keinen Wert

### `--unstable`

Aktualisierung auf eine neue instabile Version, falls verfügbar

- Standard: `false`
- Akzeptiert keinen Wert

### `--manifest`

Speicherort der Manifestdatei überschreiben

- Erfordert einen Wert

### `--current-version`

Aktuelle Version überschreiben

- Erfordert einen Wert

### `--timeout`

Eine Zeitüberschreitung für die Versionsüberprüfung

- Standard: `30`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:list`

Auflisten von Diensten im Projekt

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Nur eine Liste mit Dienstnamen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Festplatte, Name, Größe, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:dump`

Erstellen eines binären Archivierungs-Dump von Daten aus MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Die zu löschende Sammlung

- Erfordert einen Wert

### `--gzip`, `-z`

Komprimieren Sie die Ablage mit gzip

- Standard: `false`
- Akzeptiert keinen Wert

### `--stdout`, `-o`

Ausgabe in STDOUT anstelle einer Datei

- Standard: `false`
- Akzeptiert keinen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:export`

Daten aus MongoDB exportieren

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Zu exportierende Kollektion

- Erfordert einen Wert

### `--jsonArray`

Daten als einzelnes JSON-Array exportieren

- Standard: `false`
- Akzeptiert keinen Wert

### `--type`

Der Exporttyp, z. B. &quot;csv&quot;

- Erfordert einen Wert

### `--fields`, `-f`

Zu exportierende Felder

- Standard: `[]`
- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:restore`

Wiederherstellen eines binären Datenarchiv-Dump in MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Die wiederherzustellende Sammlung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `service:mongo:shell`

MongoDB-Shell verwenden

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Übergeben eines JavaScript-Fragments an die Shell

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Argumente zum Hinzufügen zum Befehl &quot;Redis&quot;


### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:create`

Schnappschuss einer Umgebung erstellen

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Umwelt


### `--live`

Live Backup: Beenden Sie die Umgebung nicht. Wenn diese Einstellung festgelegt ist, bleibt die Umgebung aktiv und während der Sicherung für Verbindungen geöffnet. Dadurch werden Ausfallzeiten reduziert, wodurch das Risiko besteht, Daten in einem inkonsistenten Zustand zu sichern.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die ID der Momentaufnahme. Erforderlich im nicht interaktiven Modus.


### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:get`

Anzeigen eines Umgebungs-Snapshots

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Die ID der Momentaufnahme. Der Standardwert ist der neueste.


### `--property`, `-P`

Die anzuzeigende Eigenschaft.

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `snapshot:restore`

Wiederherstellen eines Umgebungs-Snapshots

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

Der Name der Momentaufnahme. Die Standardeinstellung ist die neueste


### `--target`

Die wiederherzustellende Umgebung. Die Standardeinstellung ist die aktuelle Umgebung des Snapshots.

- Erfordert einen Wert

### `--branch-from`

Wenn das —target noch nicht vorhanden ist, gibt dies das übergeordnete Element der neuen Umgebung an

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Beschränken Sie nicht die Länge des anzuzeigenden Befehls. Der Standardwert beträgt 24 Zeilen.

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: App, Befehl, Vorgang. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `source-operation:run`

Quellvorgang ausführen

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Der Vorgangsname


### `--variable`

Variable, die während des Vorgangs im Format \&lt;info>type:name=value\&lt;/info>

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-cert:load`

Erstellen eines SSH-Zertifikats

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Aktualisieren Sie das Zertifikat nur bei Bedarf (schreiben Sie keine SSH-Konfiguration).

- Standard: `false`
- Akzeptiert keinen Wert

### `--new`

Aktualisieren des Zertifikats erzwingen

- Standard: `false`
- Akzeptiert keinen Wert

### `--new-key`

[Veraltet] Verwenden Sie stattdessen —new

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `ssh-key:delete`

SSH-Schlüssel löschen

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: id*, title*, path*, fingerprint (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `subscription:info`

Abonnementeigenschaften lesen und ändern

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

Der Name der Eigenschaft


### `value`

Neuen Wert für die Eigenschaft festlegen


### `--id`, `-s`

Die Abonnement-ID

- Erfordert einen Wert

### `--date-fmt`

Das Datumsformat (als PHP-Datumsformat-Zeichenfolge)

- Standard: `c`
- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:close`

Schließen von SSH-Tunneln

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Schließen aller Tunnel

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:info`

Anzeigen von Beziehungsinformationen für SSH-Tunnel

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

Die anzuzeigende Beziehungseigenschaft

- Erfordert einen Wert

### `--encode`, `-c`

Ausgabe als base64-kodierte JSON

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: port*, project*, environment*, app*, relation*, url (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:open`

SSH-Tunnel für die Beziehungen einer App öffnen

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Remote-Hosts erlauben, eine Verbindung zu lokalen weitergeleiteten Ports herzustellen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `tunnel:single`

Öffnen eines einzelnen SSH-Tunnels für eine App-Beziehung

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Der lokale Port

- Erfordert einen Wert

### `--gateway-ports`, `-g`

Remote-Hosts erlauben, eine Verbindung zu lokalen weitergeleiteten Ports herzustellen

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--app`, `-A`

Der Name der Remote-Anwendung

- Erfordert einen Wert

### `--relationship`, `-r`

Die zu verwendende Dienstbeziehung

- Erfordert einen Wert

### `--identity-file`, `-i`

Eine SSH-Identität (privater Schlüssel) zur Verwendung

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:add`

Einen Benutzer zum Projekt hinzufügen

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--role`, `-r`

Die Projektrolle des Benutzers (&quot;admin&quot;oder &quot;viewer&quot;) oder die Umgebungstyprolle (z. B. &quot;staging:contributor&quot;oder &quot;production:viewer&quot;). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf &quot;none&quot;. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. &quot;%:viewer&quot;, um dem Benutzer die Rolle &quot;Betrachter&quot;für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. &quot;production:v&quot;.

- Standard: `[]`
- Erfordert einen Wert

### `--force-invite`

Senden einer Einladung, auch wenn bereits eine gesendet wurde

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:delete`

Benutzer aus dem Projekt löschen

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

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:get`

Benutzerrollen anzeigen

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--level`, `-l`

Die Rollenebene (&quot;Projekt&quot;oder &quot;Umgebung&quot;)

- Erfordert einen Wert

### `--pipe`

Ausgabe der zu stdout zu sendenden Rolle (nach Durchführung von Änderungen)

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

- Standard: `false`
- Akzeptiert keinen Wert

### `--wait`

Warten Sie, bis der Vorgang abgeschlossen ist (Standard)

- Standard: `false`
- Akzeptiert keinen Wert

### `--role`, `-r`

[Veraltet: Verwenden Sie user:update , um die Benutzerrolle(en) zu ändern.]

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:list`

Projektbenutzer auflisten

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: email*, name*, role*, id*, given_at, updated_at (* = Standardspalten). Das Zeichen &quot;+&quot;kann als Platzhalter für die Standardspalten verwendet werden. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `user:update`

Benutzerrollen in einem Projekt aktualisieren

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Die E-Mail-Adresse des Benutzers


### `--role`, `-r`

Die Projektrolle des Benutzers (&quot;admin&quot;oder &quot;viewer&quot;) oder die Umgebungstyprolle (z. B. &quot;staging:contributor&quot;oder &quot;production:viewer&quot;). Um einen Benutzer aus einem Umgebungstyp zu entfernen, setzen Sie die Rolle auf &quot;none&quot;. Die Zeichen % oder * können als Platzhalter für den Umgebungstyp verwendet werden, z. B. &quot;%:viewer&quot;, um dem Benutzer die Rolle &quot;Betrachter&quot;für alle Typen zu geben. Die Rolle kann abgekürzt werden, z. B. &quot;production:v&quot;.

- Standard: `[]`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:create`

Variable erstellen

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

Der Variablenname


### `--update`, `-u`

Aktualisieren Sie die Variable, falls sie bereits vorhanden ist.

- Standard: `false`
- Akzeptiert keinen Wert

### `--level`, `-l`

Die Ebene, auf der die Variable festgelegt werden soll (&quot;Projekt&quot;oder &quot;Umgebung&quot;)

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

Ob der Variablenwert empfindlich ist

- Standard: `false`
- Erfordert einen Wert

### `--prefix`

Das Präfix des Variablennamens, das den Typ bestimmen kann, z. B. &quot;env&quot;. Gilt nur, wenn der Name noch kein Präfix enthält. (z. B. &quot;none&quot;oder &quot;env:&quot;)

- Standard: `none`
- Erfordert einen Wert

### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt werden kann

- Standard: `true`
- Erfordert einen Wert

### `--visible-build`

Ob die Variable zur Build-Zeit sichtbar sein soll

- Erfordert einen Wert

### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:delete`

Variable löschen

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Variablenname

- Erforderlich

### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:get`

Anzeigen von Variablen

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

Der Name der Variablen


### `--property`, `-P`

Anzeigen einer einzelnen Variableneigenschaft

- Erfordert einen Wert

### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--pipe`

[Veraltete Option] Nur Variablenwert ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

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

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: is_enabled, level, name, value. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `variable:update`

Variable aktualisieren

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Der Variablenname

- Erforderlich

### `--allow-no-change`

Rückkehrerfolg (kein Exitcode), wenn keine Änderungen bereitgestellt wurden

- Standard: `false`
- Akzeptiert keinen Wert

### `--level`, `-l`

Die Variablenebene (&quot;Projekt&quot;, &quot;Umgebung&quot;, &quot;p&quot;oder &quot;e&quot;)

- Erfordert einen Wert

### `--value`

Der Wert der Variablen

- Erfordert einen Wert

### `--json`

Ob der Variablenwert JSON-formatiert ist

- Standard: `false`
- Erfordert einen Wert

### `--sensitive`

Ob der Variablenwert empfindlich ist

- Standard: `false`
- Erfordert einen Wert

### `--enabled`

Ob die Variable in der Umgebung aktiviert werden soll

- Standard: `true`
- Erfordert einen Wert

### `--inheritable`

Ob die Variable von untergeordneten Umgebungen vererbt werden kann

- Standard: `true`
- Erfordert einen Wert

### `--visible-build`

Ob die Variable zur Build-Zeit sichtbar sein soll

- Erfordert einen Wert

### `--visible-runtime`

Ob die Variable zur Laufzeit sichtbar sein soll

- Standard: `true`
- Erfordert einen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--no-wait`, `-W`

Warten Sie nicht, bis der Vorgang abgeschlossen ist.

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

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert


## `worker:list`

Liste aller entsandten Arbeitskräfte

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Ob der Cache aktualisiert werden soll

- Standard: `false`
- Akzeptiert keinen Wert

### `--pipe`

Nur eine Liste mit Worker-Namen ausgeben

- Standard: `false`
- Akzeptiert keinen Wert

### `--project`, `-p`

Die Projekt-ID oder URL

- Erfordert einen Wert

### `--environment`, `-e`

Die Umgebungs-ID. Verwenden Sie &quot;.&quot; , um die Standardumgebung des Projekts auszuwählen.

- Erfordert einen Wert

### `--format`

Das Ausgabeformat: Tabelle, CSV, TSV oder einfach

- Standard: `table`
- Erfordert einen Wert

### `--columns`, `-c`

Anzuzeigende Spalten Verfügbare Spalten: Befehle, Name, Typ. Die Zeichen % oder * können als Platzhalter verwendet werden. Die Werte können durch Kommas (z. B. &quot;a,b,c&quot;) und/oder Leerzeichen aufgeteilt werden.

- Standard: `[]`
- Erfordert einen Wert

### `--no-header`

Geben Sie die Tabellenüberschrift nicht aus

- Standard: `false`
- Akzeptiert keinen Wert

### `--help`, `-h`

Diese Hilfemeldung anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--verbose`, `-v|-vv|-vvv`

Die Ausführlichkeit von Nachrichten erhöhen

- Standard: `false`
- Akzeptiert keinen Wert

### `--version`, `-V`

Diese Anwendungsversion anzeigen

- Standard: `false`
- Akzeptiert keinen Wert

### `--yes`, `-y`

Beantworten Sie Bestätigungsfragen mit &quot;Ja&quot;. Übernehmen Sie den Standardwert für andere Fragen und deaktivieren Sie die Interaktion.

- Standard: `false`
- Akzeptiert keinen Wert

### `--no-interaction`

Stellen Sie keine interaktiven Fragen; akzeptieren Sie Standardwerte. Entspricht der Verwendung der Umgebungsvariablen: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Akzeptiert keinen Wert

