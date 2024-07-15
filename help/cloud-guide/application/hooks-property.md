---
title: Hooks-Eigenschaft
description: Siehe Beispiele zum Konfigurieren der Hooks-Eigenschaft in der Konfigurationsdatei der [!DNL Commerce] Anwendung.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hooks-Eigenschaft

Verwenden Sie den Abschnitt &quot;`hooks`&quot;, um Shell-Befehle während der Build-, Bereitstellungs- und Postbereitstellungsphasen auszuführen:

- **`build`**—Führen Sie die Befehle _vor_ aus, um Ihre Anwendung zu verpacken. Dienste wie die Datenbank oder Redis sind nicht verfügbar, da die Anwendung noch nicht bereitgestellt wurde. Fügen Sie benutzerdefinierte Befehle _vor_ dem Standardbefehl `php ./vendor/bin/ece-tools` hinzu, damit benutzerdefiniert generierte Inhalte bis zur Bereitstellungsphase weiterverwendet werden.

- **`deploy`**—Führen Sie die Befehle _nach dem Verpacken und Bereitstellen Ihrer Anwendung durch._ Sie können jetzt auf andere Dienste zugreifen. Da der Standardbefehl `php ./vendor/bin/ece-tools` den Ordner `app/etc` an den richtigen Speicherort kopiert, müssen Sie benutzerdefinierte Befehle _nach_ dem Bereitstellungsbefehl hinzufügen, um zu verhindern, dass benutzerdefinierte Befehle fehlschlagen.

- **`post_deploy`**—Führen Sie die Befehle _nach der_ Bereitstellung Ihrer Anwendung aus und _nach_ beginnt der Container, Verbindungen zu akzeptieren. Der Erweiterungspunkt `post_deploy` löscht den Cache und lädt den Cache vorab (wärmt). Sie können die Seitenliste mithilfe der Variablen `WARM_UP_PAGES` in der Phase [Post-deploy](../environment/variables-post-deploy.md) anpassen. Obwohl dies nicht erforderlich ist, funktioniert dies zusammen mit der Umgebungsvariablen `SCD_ON_DEMAND` .

Das folgende Beispiel zeigt die Standardkonfiguration in der Datei &quot;`.magento.app.yaml`&quot;. Fügen Sie CLI-Befehle unter den Abschnitten `build`, `deploy` oder `post_deploy` _vor_ dem Befehl `ece-tools` hinzu:

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Außerdem können Sie die Build-Phase weiter anpassen, indem Sie die Befehle `generate` und `transfer` verwenden, um zusätzliche Aktionen auszuführen, wenn Sie speziell Code erstellen oder Dateien verschieben.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e` - führt dazu, dass Hooks beim ersten fehlgeschlagenen Befehl fehlschlagen, anstatt beim letzten fehlgeschlagenen Befehl.
- `build:generate` - Wendet Patches an, validiert die Konfiguration, generiert IDs und generiert statische Inhalte, wenn SCD für die Build-Phase aktiviert ist.
- `build:transfer`: Überträgt generierten Code und statischen Inhalt an das endgültige Ziel.

Die Befehle werden aus dem Anwendungsordner (`/app`) ausgeführt. Sie können den Befehl `cd` verwenden, um den Ordner zu ändern. Die Hooks schlagen fehl, wenn der endgültige Befehl in ihnen fehlschlägt. Um sie beim ersten fehlgeschlagenen Befehl fehlschlagen zu lassen, fügen Sie am Anfang des Hooks `set -e` hinzu.

**So kompilieren Sie Sass-Dateien mit grunt**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Kompilieren Sie Sass-Dateien mit `grunt` vor der Bereitstellung statischer Inhalte, was während des Builds geschieht. Setzen Sie den Befehl `grunt` vor den Befehl `build`.

{{scenarios}}
