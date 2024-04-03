---
title: Projektstruktur
description: Erfahren Sie mehr über die Dateistruktur und Projektvorlagen für Adobe Commerce in der Cloud-Infrastruktur.
exl-id: 6dc559bd-116b-4745-a85b-731508e113ff
source-git-commit: 47ef728ea46b137eeaabbdbada940143d8773ef0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Projektstruktur

Ein Adobe Commerce-Projekt zur Cloud-Infrastruktur umfasst wichtige Dateien für Anmeldedaten und die Anwendungskonfiguration. Diese Dateien sind je nach Adobe Commerce-Version als Vorlage verfügbar. Siehe Cloud-Vorlagen, die auf der Adobe Commerce-Version basieren im [`magento/magento-cloud` GitHub-Repository](https://github.com/magento/magento-cloud).

In der folgenden Tabelle werden die in einem Cloud-Projekt enthaltenen Dateien beschrieben:

| Datei | Beschreibung |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Konfigurationsdatei, die umleitet `www` zur Apex-Domäne und `php` -Anwendung zur Bereitstellung von HTTP. Siehe [Routen konfigurieren](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | Eine Konfigurationsdatei, die eine MySQL-Instanz (MariaDB), Redis, OpenSearch oder Elasticsearch definiert. Siehe [Dienste konfigurieren](../services/services-yaml.md). |
| `/app` | Die `code` -Ordner wird für benutzerdefinierte Module verwendet. Die `design` Ordner wird verwendet für [benutzerdefinierte Designs](../store/custom-theme.md). Die `etc` -Ordner enthält Konfigurationsdateien für die Anwendung. |
| `/m2-hotfixes` | Wird für benutzerdefinierte Patches verwendet. |
| `/update` | Ein vom Support-Modul verwendeter Dienstordner. |
| `.gitignore` | Geben Sie an, welche Dateien und Ordner ignoriert werden sollen. Siehe [`.gitignore` reference](#ignoring-files). |
| `.magento.app.yaml` | Eine Konfigurationsdatei, die die Eigenschaften zum Erstellen der Anwendung definiert. Siehe [Anwendung konfigurieren](../application/configure-app-yaml.md). |
| `.magento.env.yaml` | Konfigurationsdatei für die Build-, Bereitstellungs- und Postbereitstellungsphasen. Die `ece-tools` -Paket enthält ein Beispiel dieser Datei. Siehe [Umgebungen konfigurieren](../environment/configure-env-yaml.md). |
| `composer.json` | Ruft Adobe Commerce und die Konfigurationsskripte ab, um Ihre Anwendung vorzubereiten. Siehe [Erforderliche Pakete](../development/overview.md#required-packages). |
| `composer.lock` | Speichert Versionsabhängigkeiten für jedes Paket. Siehe [Erforderliche Pakete](../development/overview.md#required-packages). |
| `magento-vars.php` | Zur Definition [mehrere Stores](../store/multiple-sites.md) und Sites, die Variablen verwenden. |

{style="table-layout:auto"}

>[!NOTE]
>
>Wenn Sie Ihre lokalen Änderungen auf den Remote-Server übertragen, verwendet das Bereitstellungsskript die Werte, die von den Konfigurationsdateien im `.magento` und löscht dann das Skript das Verzeichnis und dessen Inhalt. Ihre lokale Entwicklungsumgebung ist nicht betroffen.

## Stammordner der Anwendung

Der Speicherort des Stammordners der Anwendung hängt von der Umgebung ab.

- **Starter- und Pro-Integration**: `/app`
- **Starterproduktion**: `/<project-ID>`
- **Pro Staging**: `/<project-ID>_stg`
- **Pro Produktion**: `/<project-ID>`

### Schreibgeschützte Verzeichnisse

Die Remote-Umgebungen für Integration, Staging und Produktion sind schreibgeschützt. Die folgenden Verzeichnisse sind *only* Schreibbare Verzeichnisse aus Sicherheitsgründen:

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>In Produktions- und Staging-Umgebungen verfügt jeder Knoten im Cluster mit drei Knoten über eine `/tmp` Verzeichnis, das nicht für die anderen Knoten freigegeben ist.

## Dateien ignorieren

Es gibt eine Basis `.gitignore` Datei mit Adobe Commerce im Projekt-Repository der Cloud-Infrastruktur. Aktuelle Informationen anzeigen [.gitignore-Datei im magento-cloud-Repository](https://github.com/magento/magento-cloud/blob/master/.gitignore). So fügen Sie eine Datei hinzu, die sich im `.gitignore` -Liste verwenden, können Sie die `-f` (erzwungene) Option beim Staging eines Commit:

```bash
git add <path/filename> -f
```

## Basisvorlage ändern

Sie können die folgenden Schritte ausführen, um die Struktur eines vorhandenen Projekts zu ändern und die neueste Basisvorlage für Adobe Commerce in der Cloud-Infrastruktur widerzuspiegeln.

1. Klonen Sie das Projekt auf einer lokalen Workstation.

1. Aktualisieren Sie die `composer.json` mit den folgenden Werten für die `extra` Abschnitt.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Fügen Sie die `.gitignore` Datei, die für die Basisvorlage entwickelt wurde. Wenn Sie beispielsweise die `.gitignore` -Datei für die Vorlage Version 2.2.6 verwenden Sie die [.gitignore für 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) -Datei als Referenz.

1. Löschen Sie den Git-Cache.

   ```bash
   git rm -r --cached .
   ```

1. Fügen Sie Änderungen hinzu und übertragen Sie sie.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
