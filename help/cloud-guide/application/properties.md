---
title: Eigenschaften
description: Verwenden der Eigenschaftenliste als Verweis bei der Konfiguration [!DNL Commerce] Anwendung zum Erstellen und Bereitstellen in der Cloud-Infrastruktur.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Eigenschaften für die Anwendungskonfiguration

Die `.magento.app.yaml` Die Datei verwendet Eigenschaften, um die Umgebungsunterstützung für die zu verwalten [!DNL Commerce] Anwendung.

| Name | Beschreibung | Standard | Erforderlich |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Benutzerrollen anpassen | — | Nein |
| [`crons`](crons-property.md) | Spezifikationen aktualisieren und Cron-Aufträge planen | — | Nein |
| [`dependencies`](#dependencies) | Aktivieren zusätzlicher Abhängigkeiten | `php:composer/composer: '2.2.4'` | Nein |
| [`disk`](#disk) | Definieren der Größe der persistenten Festplatte | `5120` | Ja |
| [`firewall`](firewall-property.md) | (Nur Starter) Steuerung des ausgehenden Traffics | — | Nein |
| [`hooks`](hooks-property.md) | Anpassen von Shell-Befehlen für die Build-, Bereitstellungs- und Post-Bereitstellungsphase | — | Nein |
| [`mounts`](#mounts) | Festlegen von Pfaden | Pfade:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Nein |
| [`name`](#name) | Anwendungsnamen definieren | `mymagento` | Ja |
| [`relationships`](#relationships) | Zuordnen von Diensten | Dienste:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Nein |
| [`runtime`](#runtime) | Die Laufzeiteigenschaft enthält Erweiterungen, die für die [!DNL Commerce] Anwendung. | Erweiterungen:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | Festlegen des Bild-Basis-Containers | `php:8.3` | Ja |
| [`variables`](variables-property.md) | Anwenden einer Umgebungsvariablen auf eine bestimmte Commerce-Version | — | Nein |
| [`web`](web-property.md) | Externe Anfragen verarbeiten | — | Ja |
| [`workers`](workers-property.md) | Externe Anfragen verarbeiten | — | Ja, wenn nicht die Web-Eigenschaft verwendet wird |

{style="table-layout:auto"}

## `name`

Die `name` Eigenschaft stellt den Anwendungsnamen bereit, der im [`routes.yaml`](../routes/routes-yaml.md) Datei zum Definieren des Upstreams des HTTP-Codes (standardmäßig ) `mymagento:http`). Wenn beispielsweise der Wert von `name` ist `app`verwenden, müssen Sie `app:http` im Feld „Upstream„.

>[!WARNING]
>
>Ändern Sie den Namen der Anwendung nicht, nachdem sie bereitgestellt wurde. Dies führt zu Datenverlust.

## `type` und `build`

Die `type`  und `build` Eigenschaften enthalten Informationen zum Basis-Container-Image, das zum Erstellen und Ausführen des Projekts verwendet werden soll.

Die unterstützten `type` Sprache ist PHP. Geben Sie die PHP-Version wie folgt an:

```yaml
type: php:<version>
```

Die `build` Die -Eigenschaft bestimmt, was beim Erstellen des Projekts standardmäßig geschieht. Die `flavor` Gibt einen Standardsatz von auszuführenden Build-Aufgaben an. Das folgende Beispiel zeigt die Standardkonfiguration für `type` und `build` von `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.3
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.7.2'
```

### Installieren und Verwenden von Composer 2

Die `build: flavor:` -Eigenschaft wird nicht für Composer 2.x verwendet; daher müssen Sie Composer während der Build-Phase manuell installieren. Um Composer 2.x in Ihren Starter- und Pro-Projekten zu installieren und zu verwenden, müssen Sie drei Änderungen an Ihrem `.magento.app.yaml` Konfiguration:

1. entfernen `composer` als `build: flavor:` und hinzufügen `none`. Diese Änderung verhindert, dass Cloud die standardmäßige Version 1.x von Composer zum Ausführen von Build-Aufgaben verwendet.
1. Hinzufügen `composer/composer: '^2.0'` as a `php` Abhängigkeit für die Installation von Composer 2.x.
1. Hinzufügen des `composer` Erstellen von Aufgaben in einer `build` Hook zum Ausführen der Build-Aufgaben mit Composer 2.x.

Verwenden Sie die folgenden Konfigurationsfragmente in Ihren eigenen `.magento.app.yaml` Konfiguration:

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

Siehe [Erforderliche Pakete](../development/overview.md#required-packages) für weitere Informationen über Composer.

## `dependencies`

Geben Sie die Abhängigkeiten an, die Ihre Anwendung während des Build-Prozesses benötigen könnte.

Adobe Commerce unterstützt Abhängigkeiten von den folgenden Sprachen:

- PHP
- Rubin
- Node.js

Diese Abhängigkeiten sind unabhängig von den etwaigen Abhängigkeiten Ihrer Anwendung und in der `PATH`, während des Build-Prozesses und in der Laufzeitumgebung Ihrer Anwendung.

Sie können diese Abhängigkeiten wie folgt angeben:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Verwenden Sie , um die PHP-Konfiguration zur Laufzeit zu ändern, z. B. um Erweiterungen zu aktivieren. Die folgenden Erweiterungen sind erforderlich:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Siehe [PHP-Einstellungen](php-settings.md) für Details zur Aktivierung von Erweiterungen.

## `disk`

Definiert die persistente Festplattengröße der Anwendung in MB.

```yaml
disk: 5120
```

Die minimal empfohlene Festplattengröße beträgt 256 MB. Wenn der Fehler angezeigt wird `UserError: Error building the project: Disk size may not be smaller than 128MB`, erhöhen Sie die Größe auf 256 MB.

>[!NOTE]
>
>Für Pro Staging- und Produktionsumgebungen müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) So aktualisieren Sie `mounts` und `disk` Konfiguration für Ihr Programm. Wenn Sie das Ticket senden, geben Sie die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihres `.magento.app.yaml` -Datei.

## `relationships`

Definiert die Dienstzuordnung in der Anwendung.

Die Beziehung `name` ist für die Anwendung in der `MAGENTO_CLOUD_RELATIONSHIPS` Umgebungsvariable. Die `<service-name>:<endpoint-name>` Beziehung ist den in der definierten Werten für Name und Typ zugeordnet `.magento/services.yaml` -Datei.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Im Folgenden finden Sie ein Beispiel für die Standardbeziehungen:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Siehe [Dienste](../services/services-yaml.md) Eine vollständige Liste der derzeit unterstützten Diensttypen und Endpunkte finden Sie.

## `mounts`

Ein Objekt, dessen Schlüssel Pfade sind, die relativ zum Stamm des Programms sind. Die Einhängung ist ein beschreibbarer Bereich auf der Festplatte für Dateien. Im Folgenden finden Sie eine standardmäßige Liste der in konfigurierten Bereitstellungen `magento.app.yaml` Datei, die den `volume_id[/subpath]` Syntax:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

Das Format für das Hinzufügen Ihres Mounts zu dieser Liste ist wie folgt:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`- Gibt ein Volume zwischen Ihren Programmen innerhalb einer Umgebung frei.
- `disk`- Definiert die für das freigegebene Volume verfügbare Größe.

>[!NOTE]
>
>Für Pro Staging- und Produktionsumgebungen müssen Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) So aktualisieren Sie `mounts` und `disk` Konfiguration für Ihr Programm. Wenn Sie das Ticket senden, geben Sie die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihres `.magento.app.yaml` -Datei.

Sie können das Einbinden von Web-Seiten zugänglich machen, indem Sie es der [`web`](web-property.md) Standortblock.

>[!WARNING]
>
>Sobald die Site Daten enthält, ändern Sie nicht mehr `subpath` Teil des Bereitstellungsnamens. Dieser Wert ist die eindeutige Kennung für das `files` Bereich. Wenn Sie diesen Namen ändern, gehen alle am alten Speicherort gespeicherten Site-Daten verloren.

## `access`

Die `access` -Eigenschaft gibt eine minimale Benutzerrollenebene an, die SSH-Zugriff auf die Umgebungen erlaubt. Folgende Benutzerrollen sind verfügbar:

- `admin`- Kann Einstellungen ändern und Aktionen in der Umgebung ausführen; hat _Geber_ und _Betrachter_ Rechte.
- `contributor`- Kann Code in diese Umgebung übertragen und von der Umgebung aus eine Verzweigung erstellen; hat _Betrachter_ Rechte.
- `viewer`- Kann nur die Umgebung anzeigen.

Die Standardbenutzerrolle ist `contributor`, wodurch der SSH-Zugriff von Benutzenden mit nur _Betrachter_ Rechte. Sie können die Benutzerrolle ändern in `viewer` um SSH-Zugriff nur für Benutzer mit _Betrachter_ Rechte:

```yaml
access:
    ssh: viewer
```
