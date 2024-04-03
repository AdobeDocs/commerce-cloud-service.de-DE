---
title: Hooks-Eigenschaft
description: Beispiele zum Konfigurieren der Hooks-Eigenschaft finden Sie in der [!DNL Commerce] Anwendungskonfigurationsdatei.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hooks-Eigenschaft

Verwenden Sie die `hooks` -Abschnitt zum Ausführen von Shell-Befehlen während der Build-, Bereitstellungs- und Post-Bereitstellungsphasen:

- **`build`**—Ausführen von Befehlen _before_ Verpacken Sie Ihren Antrag. Dienste wie die Datenbank oder Redis sind nicht verfügbar, da die Anwendung noch nicht bereitgestellt wurde. Hinzufügen benutzerdefinierter Befehle _before_ die Standardeinstellung `php ./vendor/bin/ece-tools` -Befehl, damit benutzerdefiniert generierte Inhalte bis zur Bereitstellungsphase weiterverwendet werden.

- **`deploy`**—Ausführen von Befehlen _after_ Verpacken und Bereitstellen Ihrer Anwendung. Sie können jetzt auf andere Dienste zugreifen. Seit der standardmäßigen `php ./vendor/bin/ece-tools` -Befehl kopiert die `app/etc` Verzeichnis zum richtigen Speicherort hinzufügen, müssen Sie benutzerdefinierte Befehle hinzufügen _after_ den Befehl deploy , um zu verhindern, dass benutzerdefinierte Befehle fehlschlagen.

- **`post_deploy`**—Ausführen von Befehlen _after_ Bereitstellen der Anwendung und _after_ der Container beginnt, Verbindungen zu akzeptieren. Die `post_deploy` -Erweiterungspunkt löscht den Cache und lädt den Cache vorab (wärmt). Sie können die Liste der Seiten mit dem `WARM_UP_PAGES` in der [Phase nach der Bereitstellung](../environment/variables-post-deploy.md). Obwohl dies nicht erforderlich ist, funktioniert dies zusammen mit dem `SCD_ON_DEMAND` Umgebungsvariable.

Das folgende Beispiel zeigt die Standardkonfiguration im `.magento.app.yaml` -Datei. Fügen Sie CLI-Befehle unter dem `build`, `deploy`oder `post_deploy` Abschnitte _before_ die `ece-tools` command:

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

Außerdem können Sie die Build-Phase mithilfe der `generate` und `transfer` -Befehle zum Ausführen zusätzlicher Aktionen beim Erstellen oder Verschieben von Dateien.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e`—führt dazu, dass Hooks beim ersten fehlgeschlagenen Befehl fehlschlagen, anstatt beim letzten fehlgeschlagenen Befehl.
- `build:generate`—wendet Patches an, validiert die Konfiguration, generiert IDs und generiert statische Inhalte, wenn SCD für die Build-Phase aktiviert ist.
- `build:transfer`—überträgt generierten Code und statischen Inhalt an das endgültige Ziel.

Die Befehle werden von der Anwendung ausgeführt (`/app`). Sie können die `cd` -Befehl zum Ändern des Ordners. Die Hooks schlagen fehl, wenn der endgültige Befehl in ihnen fehlschlägt. Um sie beim ersten fehlgeschlagenen Befehl fehlschlagen zu lassen, fügen Sie `set -e` am Anfang des Hakens.

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

Kompilieren Sie Sass-Dateien mit `grunt` vor der Bereitstellung statischer Inhalte, die während des Builds erfolgt. Platzieren Sie die `grunt` -Befehl vor `build` Befehl.

{{scenarios}}
