---
title: Eigenschaften
description: Verwenden Sie die Eigenschaftsliste als Referenz bei der Konfiguration der [!DNL Commerce] -Anwendung für die Erstellung und Bereitstellung in der Cloud-Infrastruktur.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Eigenschaften für die Anwendungskonfiguration

Die `.magento.app.yaml` -Datei verwendet Eigenschaften zum Verwalten der Umgebungsunterstützung für [!DNL Commerce] Anwendung.

| Name | Beschreibung | Standard | Erforderlich |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Benutzerrollen anpassen | — | Nein |
| [`crons`](crons-property.md) | Eigenschaften aktualisieren und Cron-Aufträge planen | — | Nein |
| [`dependencies`](#dependencies) | Zusätzliche Abhängigkeiten aktivieren | `php:composer/composer: '2.2.4'` | Nein |
| [`disk`](#disk) | Persistente Festplattengröße definieren | `5120` | Ja |
| [`firewall`](firewall-property.md) | (Nur Starter) Ausgehenden Traffic steuern | — | Nein |
| [`hooks`](hooks-property.md) | Anpassen von Shell-Befehlen für die Build-, Bereitstellungs- und Nach-Bereitstellung-Phasen | — | Nein |
| [`mounts`](#mounts) | Pfade festlegen | Pfade:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Nein |
| [`name`](#name) | Anwendungsnamen definieren | `mymagento` | Ja |
| [`relationships`](#relationships) | Zuordnungsdienste | Dienste:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Nein |
| [`runtime`](#runtime) | Die Laufzeiteigenschaft enthält Erweiterungen, die für die [!DNL Commerce] Anwendung. | Erweiterungen:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | Basisbehälterbild festlegen | `php:8.1` | Ja |
| [`variables`](variables-property.md) | Umgebungsvariable auf eine bestimmte Commerce-Version anwenden | — | Nein |
| [`web`](web-property.md) | Umgang mit externen Anforderungen | — | Ja |
| [`workers`](workers-property.md) | Umgang mit externen Anforderungen | — | Ja, wenn die Webeigenschaft nicht verwendet wird |

{style="table-layout:auto"}

## `name`

Die `name` -Eigenschaft stellt den Anwendungsnamen bereit, der in der [`routes.yaml`](../routes/routes-yaml.md) -Datei, um den HTTP-Upstream zu definieren (standardmäßig `mymagento:http`). Wenn beispielsweise der Wert von `name` is `app`, müssen Sie `app:http` im Upstream-Feld.

>[!WARNING]
>
>Ändern Sie den Namen der Anwendung nicht, nachdem sie bereitgestellt wurde. Dies führt zu Datenverlust.

## `type` und `build`

Die `type`  und `build` -Eigenschaften enthalten Informationen zum Basisbehälterbild zum Erstellen und Ausführen des Projekts.

Die unterstützten `type` Sprache ist PHP. Geben Sie die PHP-Version wie folgt an:

```yaml
type: php:<version>
```

Die `build` -Eigenschaft bestimmt, was standardmäßig beim Erstellen des Projekts geschieht. Die `flavor` gibt einen Standardsatz von auszuführenden Build-Aufgaben an. Das folgende Beispiel zeigt die Standardkonfiguration für `type` und `build` von `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### Installieren und Verwenden von Composer 2

Die `build: flavor:` -Eigenschaft nicht für Composer 2.x verwendet wird. Daher müssen Sie Composer während der Build-Phase manuell installieren. Um Composer 2.x in Ihren Starter- und Pro-Projekten zu installieren und zu verwenden, müssen Sie drei Änderungen an Ihrer `.magento.app.yaml` Konfiguration:

1. Entfernen `composer` als `build: flavor:` und hinzufügen `none`. Diese Änderung verhindert, dass Cloud die standardmäßige Version 1.x von Composer verwendet, um Build-Aufgaben auszuführen.
1. Hinzufügen `composer/composer: '^2.0'` as a `php` Abhängigkeit für die Installation von Composer 2.x.
1. Fügen Sie die `composer` Erstellen von Aufgaben in `build` -Erweiterungspunkt zum Ausführen der Build-Aufgaben mit Composer 2.x.

Verwenden Sie die folgenden Konfigurationsfragmente in Ihrem eigenen `.magento.app.yaml` Konfiguration:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Siehe [Erforderliche Pakete](../development/overview.md#required-packages) Weitere Informationen zu Composer.

## `dependencies`

Geben Sie Abhängigkeiten an, die Ihre Anwendung während des Build-Prozesses möglicherweise benötigt.

Adobe Commerce unterstützt Abhängigkeiten in den folgenden Sprachen:

- PHP
- Ruby
- Node.js

Diese Abhängigkeiten sind unabhängig von den möglichen Abhängigkeiten Ihrer Anwendung und sind in der `PATH`, während des Build-Prozesses und in der Laufzeitumgebung Ihrer Anwendung.

Sie können diese Abhängigkeiten wie folgt angeben:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Verwenden Sie , um die PHP-Konfiguration zur Laufzeit zu ändern, z. B. zum Aktivieren von Erweiterungen. Die folgenden Erweiterungen sind erforderlich:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Siehe [PHP-Einstellungen](php-settings.md) für Details zum Aktivieren von Erweiterungen.

## `disk`

Definiert die persistente Festplattengröße der Anwendung in MB.

```yaml
disk: 5120
```

Die empfohlene Mindestgröße beträgt 256 MB. Wenn der Fehler angezeigt wird `UserError: Error building the project: Disk size may not be smaller than 128MB`erhöhen Sie die Größe auf 256 MB.

>[!NOTE]
>
>Für Pro-Staging- und Produktionsumgebungen müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die `mounts` und `disk` Konfiguration für Ihre Anwendung. Geben Sie beim Senden des Tickets die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihrer `.magento.app.yaml` -Datei.

## `relationships`

Definiert die Dienstzuordnung in der Anwendung.

Die Beziehung `name` ist für die Anwendung im `MAGENTO_CLOUD_RELATIONSHIPS` Umgebungsvariable. Die `<service-name>:<endpoint-name>` Beziehung wird mit den in der Variablen `.magento/services.yaml` -Datei.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Im Folgenden finden Sie ein Beispiel für die standardmäßigen Beziehungen:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Siehe [Dienste](../services/services-yaml.md) für eine vollständige Liste der derzeit unterstützten Service-Typen und -Endpunkte.

## `mounts`

Ein Objekt, dessen Schlüssel Pfade relativ zum Stammverzeichnis der Anwendung sind. Das Mount ist ein schreibbarer Bereich auf der Festplatte für Dateien. Im Folgenden finden Sie eine standardmäßige Liste der im Abschnitt `magento.app.yaml` -Datei mithilfe der `volume_id[/subpath]` Syntax:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

Das Format für das Hinzufügen Ihrer Reittierliste zu dieser Liste lautet wie folgt:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`—Teilt ein Volumen zwischen Ihren Anwendungen in einer Umgebung.
- `disk`—Definiert die für das freigegebene Volume verfügbare Größe.

>[!NOTE]
>
>Für Pro-Staging- und Produktionsumgebungen müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die `mounts` und `disk` Konfiguration für Ihre Anwendung. Geben Sie beim Senden des Tickets die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihrer `.magento.app.yaml` -Datei.

Sie können die Bereitstellung online verfügbar machen, indem Sie sie zum [`web`](web-property.md) Standortblock.

>[!WARNING]
>
>Sobald Ihre Site über Daten verfügt, dürfen Sie die `subpath` Teil des Bereitstellungsnamens. Dieser Wert ist die eindeutige Kennung für die `files` Bereich. Wenn Sie diesen Namen ändern, gehen alle am alten Speicherort gespeicherten Site-Daten verloren.

## `access`

Die `access` -Eigenschaft gibt ein minimales Benutzerrollenlevel an, das SSH-Zugriff auf die Umgebungen erlaubt. Die verfügbaren Benutzerrollen sind:

- `admin`—Kann Einstellungen ändern und Aktionen in der Umgebung ausführen; hat _contributor_ und _Viewer_ Rechte.
- `contributor`—Kann Code in diese Umgebung übertragen und von der Umgebung aus verzweigen; hat _Viewer_ Rechte.
- `viewer`—Kann nur die Umgebung anzeigen.

Die standardmäßige Benutzerrolle lautet `contributor`, wodurch der SSH-Zugriff von Benutzern nur mit _Viewer_ Rechte. Sie können die Benutzerrolle in `viewer` , um nur Benutzern mit _Viewer_ Berechtigungen:

```yaml
access:
    ssh: viewer
```
