---
title: Beispiel für die Verwaltung systemspezifischer Einstellungen
description: Hier finden Sie ein Beispiel für die Verwaltung und Synchronisierung von Speicherkonfigurationseinstellungen in allen Adobe Commerce-Umgebungen in Cloud-Infrastruktur.
hidefromtoc: true
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Beispiel für die Verwaltung systemspezifischer Einstellungen

Dieses Beispiel zeigt, wie Sie mit der Konfigurationsverwaltung die Speichereinstellungen in allen Umgebungen konsistent halten.

Das Beispiel verwendet die folgende in [Speichereinstellungen](store-settings.md):

1. Geben Sie Ihre Konfigurationen in den Store-Administrator der Integrationsumgebung ein.
1. Erstellen Sie eine `config.php` Datei speichern und auf Ihre lokale Workstation übertragen.
1. Push `config.php` in die Remote-Integrationsumgebung.
1. Vergewissern Sie sich, dass Ihre Einstellungen im Admin nicht bearbeitbar sind.
1. Nehmen Sie die erforderlichen Änderungen vor:

   * Ändern Sie die Konfigurationseinstellungen in der Integrationsumgebung.
   * Um Konfigurationen hinzuzufügen, führen Sie den Befehl zum Erstellen aus. `config.php` erneut. An die Datei werden neue Konfigurationen angehängt.
   * Um vorhandene Konfigurationen zu entfernen oder zu bearbeiten, bearbeiten Sie die Datei manuell.
   * Übernehmen und pushen.

Sie können beispielsweise die folgenden Einstellungen festlegen:

* Deaktivieren [locale](https://glossary.magento.com/locale) und Einstellungen zur Optimierung statischer Dateien in Ihrer Integrationsumgebung
* Aktivieren der statischen Dateioptimierung in Staging- und Produktionsumgebungen
* Schnelles Konfigurieren in Staging und Produktion mit spezifischen Anmeldeinformationen für jede

_Optimierung statischer Dateien_ bedeutet das Zusammenführen und Minimieren von JavaScript- und Cascading Style Sheets sowie das Minimieren von HTML-Vorlagen. Siehe [Implementierungsstrategien für statische Inhalte](../deploy/static-content.md).

## Voraussetzungen

Um diese Konfigurationsverwaltungsaufgaben durchzuführen, benötigen Sie Folgendes:

* Rolle des Projektlesers mit [Umgebung &quot;admin&quot;](../project/user-access.md) permissions
* Admin-URL und Anmeldeinformationen für Integrations-, Staging- und Produktionsumgebungen

## Konfigurieren des Commerce-Administrators

In der Integrationsumgebung können Sie sich beim Administrator anmelden, um die Systemkonfigurationseinstellungen für Stores, Websites, Module oder Erweiterungen, die statische Dateioptimierung und Systemwerte im Zusammenhang mit der Bereitstellung statischer Inhalte zu ändern. Siehe [Konfigurationsdaten](store-settings.md#scd-performance).

**So ändern Sie die Optimierungseinstellungen für Gebietsschema und statische Dateien**:

1. Melden Sie sich bei der Integrationsumgebung Admin an. Sie können über die [[!DNL Cloud Console]](../project/overview.md).
1. Navigieren Sie zu **Stores** > Einstellungen > **Konfiguration** > Allgemein > **Allgemein**.
1. Erweitern Sie in der Seitennavigation den **Gebietsschemaoptionen**.
1. Aus dem **Gebietsschema** Liste, das Gebietsschema ändern. Sie können es später wieder ändern.

   ![Gebietsschema ändern](../../assets/locale-options.png)

1. Klicks **Konfiguration speichern**.
1. Bei Aufforderung [Cache leeren](https://docs.magento.com/user-guide/system/cache-management.html).
1. Melden Sie sich beim Administrator ab.

## Werte exportieren und config.php auf Ihr lokales System übertragen

Dieser Schritt erzeugt und überträgt die `config.php` Konfigurationsdatei in der Integrationsumgebung mit einem Befehl verwenden, den Sie auf Ihrem lokalen Computer ausführen.

Dieses Verfahren entspricht Schritt 2 im [empfohlene Vorgehensweise](store-settings.md). Nach der Erstellung `config.php`, übertragen Sie es auf Ihr lokales System, damit Sie es zu Git hinzufügen können.

**Erstellen und Übertragen`config.php`**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Änderung an der Integrationsumgebung.

   ```bash
   magento-cloud environment:checkout integration
   ```

1. Erstellen Sie einen lokalen Dump der Remote-Datenbank.

   ```bash
   magento-cloud db:dump
   ```

Das folgende Snippet aus `config.php` zeigt ein Beispiel für die Änderung des Standardgebietsschemas in `en_GB` und Änderung der Einstellungen für die statische Dateioptimierung:

```php?start_inline=1
'general' => [
     'locale' => [
         'code' => 'en_GB',
         'timezone' => 'UTC',
     ],

     ... more ...

 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],
     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],

     ... more ...
```

## Push und Bereitstellung von &quot;config.php&quot;in Umgebungen

Nachdem Sie die `config.php` und übertragen Sie es auf Ihr lokales System, übertragen Sie es auf Git und pushen Sie es in Ihre Umgebungen. Dieses Verfahren entspricht den Schritten 3 und 4 im [empfohlene Vorgehensweise](store-settings.md).

Der folgende Befehl fügt, überträgt und übergibt an die `master` branch:

```bash
git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
```

Vollständige Codebereitstellung für Staging und Produktion. Als Erster drücken Sie auf `staging` und `master` Verzweigungen. Weitere Informationen zu Bereitstellungsbefehlen finden Sie unter [Bereitstellen Ihres Stores](../deploy/staging-production.md).

Warten Sie, bis die Bereitstellung in allen Umgebungen abgeschlossen ist.

## Überprüfen der Konfigurationsänderungen

Nach dem Push `config.php` in Ihren Umgebungen ändern, sollten alle Werte, die Sie geändert haben, im Admin schreibgeschützt sein. In diesem Beispiel sollten die geänderten Standardeinstellungen für Gebietsschema und statische Dateioptimierung nicht im Admin bearbeitet werden können. Diese Konfigurationseinstellungen werden in `config.php`.

Überprüfen der Konfigurationsänderungen:

1. Melden Sie sich in einer der Umgebungen von Admin ab.
1. Melden Sie sich wieder beim Administrator an.
1. Klicks **Stores** > Einstellungen > **Konfiguration** > Allgemein > **Allgemein**.
1. Erweitern Sie im rechten Bereich **Gebietsschemaoptionen**.

   Beachten Sie, dass mehrere Felder nicht bearbeitet werden können, wie im folgenden Beispiel gezeigt. Diese Konfigurationseinstellungen werden von `config.php`.

   ![Bestimmte Werte können nicht mehr im Admin bearbeitet werden](../../assets/locale-options-disabled.png)

1. Melden Sie sich beim Administrator ab.

## Systemspezifische Konfigurationseinstellungen ändern und aktualisieren

Wenn Sie eine dieser Einstellungen ändern müssen, ändern Sie die `config.php` Datei manuell mit einem Texteditor. Nach Abschluss der Bearbeitungen oder Entfernungen können Sie sie bestätigen und in die Remote-Umgebung übertragen, wie in den vorherigen Schritten beschrieben.

Um Konfigurationen hinzuzufügen, ändern Sie Ihre Integrationsumgebung und führen Sie den Befehl erneut aus, um die Datei zu generieren. Alle neuen Konfigurationen werden an den Code in der Datei angehängt. Push it to Git, wie zuvor beschrieben.

Ändern Sie für dieses Beispiel die Optimierungseinstellungen für statische Dateien und fügen Sie eine neue Einstellung für JavaScript hinzu.

### Hinzufügen von Konfigurationen in der Integration

Hinzufügen von Konfigurationswerten zum Integrationsumgebungs-Admin. In diesem Beispiel werden JavaScript-Dateien zusammengeführt.

1. Melden Sie sich von der Integrationsadministratorin ab.
1. Melden Sie sich wieder beim Integrationsadministrator an.
1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **Entwickler**.
1. Erweitern Sie im rechten Bereich **JavaScript-Einstellungen**.
1. Aus dem **Zusammenführen von JavaScript-Dateien** Liste, klicken Sie **Ja**.
1. Klicks **Konfiguration speichern**.
1. Bei Aufforderung [Cache leeren](https://docs.magento.com/user-guide/system/cache-management.html).
1. Melden Sie sich beim Administrator ab.

Wenn Sie den Befehl &quot;dump&quot;erneut ausführen, wird die neue Konfiguration an die Datei angehängt.

```bash
magento-cloud db:dump
```

### Bearbeiten Sie config.php mit neuen Einstellungen

Verwenden Sie auf Ihrer lokalen Seite einen Texteditor, um die aktualisierte `app/etc/config.php` -Datei. Bearbeiten Sie diese Einstellungen, um die Minimierung für JavaScript-, HTML- und CSS-Dateien zu aktivieren.

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],
```

Um Einstellungen zu ändern, um eine Minimierung zu ermöglichen, bearbeiten Sie `'0'` nach `'1'` für `'minify_html'` und jeder `'minify_files'` Option:

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '1',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '1',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '1',
     ],
```

Speichern Sie die Änderungen in der Datei.

### Push the changes to Git

Geben Sie Folgendes ein, um Ihre Änderungen zu übertragen:

```bash
git add app/etc/config.php
```

```bash
git commit -m "Add system-specific configuration and edit settings"
```

```bash
git push origin master
```

Warten Sie, bis die Bereitstellung abgeschlossen ist.

Wiederholen Sie den Bereitstellungsprozess für das Pushen des Codes in alle Umgebungen.
