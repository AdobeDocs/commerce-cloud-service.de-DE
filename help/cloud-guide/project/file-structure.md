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

Ein Adobe Commerce-Projekt zur Cloud-Infrastruktur umfasst wichtige Dateien für Anmeldedaten und die Anwendungskonfiguration. Diese Dateien sind je nach Adobe Commerce-Version als Vorlage verfügbar. Siehe Cloud-Vorlagen, die auf der Adobe Commerce-Version basieren, im [`magento/magento-cloud` GitHub-Repository](https://github.com/magento/magento-cloud) .

In der folgenden Tabelle werden die in einem Cloud-Projekt enthaltenen Dateien beschrieben:

| Datei | Beschreibung |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Konfigurationsdatei, die `www` zur Apex-Domäne und `php` Anwendung zur Bereitstellung von HTTP umleitet. Siehe [Routen konfigurieren](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | Eine Konfigurationsdatei, die eine MySQL-Instanz (MariaDB), Redis, OpenSearch oder Elasticsearch definiert. Siehe [Konfigurieren von Diensten](../services/services-yaml.md). |
| `/app` | Der Ordner `code` wird für benutzerdefinierte Module verwendet. Der Ordner `design` wird für [benutzerdefinierte Designs](../store/custom-theme.md) verwendet. Der Ordner &quot;`etc`&quot; enthält Konfigurationsdateien für die Anwendung. |
| `/m2-hotfixes` | Wird für benutzerdefinierte Patches verwendet. |
| `/update` | Ein vom Support-Modul verwendeter Dienstordner. |
| `.gitignore` | Geben Sie an, welche Dateien und Ordner ignoriert werden sollen. Siehe [`.gitignore` reference](#ignoring-files). |
| `.magento.app.yaml` | Eine Konfigurationsdatei, die die Eigenschaften zum Erstellen der Anwendung definiert. Siehe [Anwendung konfigurieren](../application/configure-app-yaml.md). |
| `.magento.env.yaml` | Konfigurationsdatei für die Build-, Bereitstellungs- und Postbereitstellungsphasen. Das Paket `ece-tools` enthält ein Beispiel dieser Datei. Siehe [Umgebungen konfigurieren](../environment/configure-env-yaml.md). |
| `composer.json` | Ruft Adobe Commerce und die Konfigurationsskripte ab, um Ihre Anwendung vorzubereiten. Siehe [Erforderliche Pakete](../development/overview.md#required-packages). |
| `composer.lock` | Speichert Versionsabhängigkeiten für jedes Paket. Siehe [Erforderliche Pakete](../development/overview.md#required-packages). |
| `magento-vars.php` | Wird verwendet, um [mehrere Stores](../store/multiple-sites.md) und Sites mithilfe von Variablen zu definieren. |

{style="table-layout:auto"}

>[!NOTE]
>
>Wenn Sie Ihre lokalen Änderungen auf den Remote-Server übertragen, verwendet das Bereitstellungsskript die Werte, die von den Konfigurationsdateien im Ordner &quot;`.magento`&quot;definiert wurden, und dann löscht das Skript den Ordner und dessen Inhalt. Ihre lokale Entwicklungsumgebung ist nicht betroffen.

## Stammordner der Anwendung

Der Speicherort des Stammordners der Anwendung hängt von der Umgebung ab.

- **Starter and Pro Integration**: `/app`
- **Starterproduktion**: `/<project-ID>`
- **Pro Staging**: `/<project-ID>_stg`
- **Pro Production**: `/<project-ID>`

### Schreibgeschützte Verzeichnisse

Die Remote-Umgebungen für Integration, Staging und Produktion sind schreibgeschützt. Die folgenden Verzeichnisse sind aus Sicherheitsgründen die *Nur* beschreibbaren Ordner:

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>In Produktions- und Staging-Umgebungen verfügt jeder Knoten im Cluster mit drei Knoten über einen Ordner &quot;`/tmp`&quot;, der nicht für die anderen Knoten freigegeben ist.

## Dateien ignorieren

Es gibt eine Basisdatei mit dem Adobe Commerce für das Projekt-Repository der Cloud-Infrastruktur mit dem Namen `.gitignore` . Siehe die neueste Datei [.gitignore im Magento-Cloud-Repository](https://github.com/magento/magento-cloud/blob/master/.gitignore). Um eine Datei hinzuzufügen, die sich in der Liste `.gitignore` befindet, können Sie beim Staging eines Commit die Option `-f` (erzwingen) verwenden:

```bash
git add <path/filename> -f
```

## Basisvorlage ändern

Sie können die folgenden Schritte ausführen, um die Struktur eines vorhandenen Projekts zu ändern und die neueste Basisvorlage für Adobe Commerce in der Cloud-Infrastruktur widerzuspiegeln.

1. Klonen Sie das Projekt auf einer lokalen Workstation.

1. Aktualisieren Sie die Datei &quot;`composer.json`&quot;mit den folgenden Werten für den Abschnitt &quot;`extra`&quot;.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Fügen Sie die für die Basisvorlage entworfene Datei `.gitignore` hinzu. Wenn Sie beispielsweise die Datei `.gitignore` für die Vorlage Version 2.2.6 benötigen, verwenden Sie die Datei [.gitignore für 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) als Referenz.

1. Löschen Sie den Git-Cache.

   ```bash
   git rm -r --cached .
   ```

1. Fügen Sie Änderungen hinzu und übertragen Sie sie.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
