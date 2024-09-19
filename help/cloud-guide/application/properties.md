---
title: Eigenschaften
description: Verwenden Sie die Eigenschaftsliste als Referenz bei der Konfiguration der [!DNL Commerce] Anwendung für die Erstellung und Bereitstellung in der Cloud-Infrastruktur.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: 1d671d7d2b9ef8742f50b23aa56020d82c701fa4
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Eigenschaften für die Anwendungskonfiguration

Die Datei `.magento.app.yaml` verwendet Eigenschaften, um die Umgebungsunterstützung für die Anwendung [!DNL Commerce] zu verwalten.

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
| [`runtime`](#runtime) | Die Laufzeiteigenschaft enthält Erweiterungen, die für die [!DNL Commerce] -Anwendung erforderlich sind. | Erweiterungen:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | Basisbehälterbild festlegen | `php:8.3` | Ja |
| [`variables`](variables-property.md) | Anwenden einer Umgebungsvariablen auf eine bestimmte Commerce-Version | — | Nein |
| [`web`](web-property.md) | Umgang mit externen Anforderungen | — | Ja |
| [`workers`](workers-property.md) | Umgang mit externen Anforderungen | — | Ja, wenn die Webeigenschaft nicht verwendet wird |

{style="table-layout:auto"}

## `name`

Die Eigenschaft `name` stellt den Anwendungsnamen bereit, der in der Datei [`routes.yaml`](../routes/routes-yaml.md) verwendet wird, um den HTTP-Upstream zu definieren (standardmäßig `mymagento:http`). Wenn der Wert von `name` beispielsweise `app` ist, müssen Sie `app:http` im Upstream-Feld verwenden.

>[!WARNING]
>
>Ändern Sie den Namen der Anwendung nicht, nachdem sie bereitgestellt wurde. Dies führt zu Datenverlust.

## `type` und `build`

Die Eigenschaften `type` und `build` enthalten Informationen zum Basisbehälterbild, das erstellt und ausgeführt werden soll.

Die unterstützte Sprache `type` ist PHP. Geben Sie die PHP-Version wie folgt an:

```yaml
type: php:<version>
```

Die Eigenschaft `build` bestimmt, was standardmäßig beim Erstellen des Projekts geschieht. Der `flavor` gibt einen Standardsatz von auszuführenden Build-Aufgaben an. Das folgende Beispiel zeigt die Standardkonfiguration für `type` und `build` von `magento-cloud/.magento.app.yaml`:

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

Die Eigenschaft `build: flavor:` wird nicht für Composer 2.x verwendet. Daher müssen Sie Composer während der Build-Phase manuell installieren. Um Composer 2.x in Ihren Starter- und Pro-Projekten zu installieren und zu verwenden, müssen Sie drei Änderungen an Ihrer `.magento.app.yaml`-Konfiguration vornehmen:

1. Entfernen Sie `composer` als `build: flavor:` und fügen Sie `none` hinzu. Diese Änderung verhindert, dass Cloud die standardmäßige Version 1.x von Composer verwendet, um Build-Aufgaben auszuführen.
1. Fügen Sie `composer/composer: '^2.0'` als `php` -Abhängigkeit für die Installation von Composer 2.x hinzu.
1. Fügen Sie die Build-Aufgaben `composer` einem `build`-Hook hinzu, um die Build-Aufgaben mit Composer 2.x auszuführen.

Verwenden Sie die folgenden Konfigurationsfragmente in Ihrer eigenen `.magento.app.yaml`-Konfiguration:

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

Weitere Informationen zu Composer finden Sie unter [Erforderliche Pakete](../development/overview.md#required-packages) .

## `dependencies`

Geben Sie Abhängigkeiten an, die Ihre Anwendung während des Build-Prozesses möglicherweise benötigt.

Adobe Commerce unterstützt Abhängigkeiten in den folgenden Sprachen:

- PHP
- Ruby
- Node.js

Diese Abhängigkeiten sind unabhängig von den letztendlichen Abhängigkeiten Ihrer Anwendung und stehen in der `PATH`, während des Build-Prozesses und in der Laufzeitumgebung Ihrer Anwendung zur Verfügung.

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

Weitere Informationen zum Aktivieren von Erweiterungen finden Sie unter [PHP-Einstellungen](php-settings.md) .

## `disk`

Definiert die persistente Festplattengröße der Anwendung in MB.

```yaml
disk: 5120
```

Die empfohlene Mindestgröße beträgt 256 MB. Wenn der Fehler `UserError: Error building the project: Disk size may not be smaller than 128MB` auftritt, erhöhen Sie die Größe auf 256 MB.

>[!NOTE]
>
>Bei Staging- und Produktionsumgebungen für Pro müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um die Konfiguration `mounts` und `disk` für Ihre Anwendung zu aktualisieren. Geben Sie beim Senden des Tickets die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihrer `.magento.app.yaml` -Datei hinzu.
>
>Es ist nicht möglich, den Festplattenspeicher in Staging oder Produktion vorübergehend zu erhöhen. Dieser Vorgang kann nicht rückgängig gemacht werden.

## `relationships`

Definiert die Dienstzuordnung in der Anwendung.

Die Beziehung `name` ist für die Anwendung in der Umgebungsvariablen `MAGENTO_CLOUD_RELATIONSHIPS` verfügbar. Die `<service-name>:<endpoint-name>` -Beziehung ist mit den Namen- und Typwerten verknüpft, die in der `.magento/services.yaml` -Datei definiert sind.

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

Eine vollständige Liste der derzeit unterstützten Diensttypen und Endpunkte finden Sie unter [Dienste](../services/services-yaml.md) .

## `mounts`

Ein Objekt, dessen Schlüssel Pfade relativ zum Stammverzeichnis der Anwendung sind. Das Mount ist ein schreibbarer Bereich auf der Festplatte für Dateien. Im Folgenden finden Sie eine Standardliste der in der Datei `magento.app.yaml` mit der Syntax `volume_id[/subpath]` konfigurierten Bereitstellungen:

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

- `shared`—Teilt ein Volumen zwischen Ihren Anwendungen innerhalb einer Umgebung.
- `disk` - Definiert die für das freigegebene Volume verfügbare Größe.

>[!NOTE]
>
>Bei Staging- und Produktionsumgebungen für Pro müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um die Konfiguration `mounts` und `disk` für Ihre Anwendung zu aktualisieren. Geben Sie beim Senden des Tickets die erforderlichen Konfigurationsänderungen an und fügen Sie eine aktualisierte Version Ihrer `.magento.app.yaml` -Datei hinzu.

Sie können die Bereitstellung über das Internet zugänglich machen, indem Sie sie dem Block [`web`](web-property.md) der Positionen hinzufügen.

>[!WARNING]
>
>Sobald Ihre Site über Daten verfügt, ändern Sie nicht den `subpath` -Teil des Bereitstellungsnamens. Dieser Wert ist die eindeutige Kennung für den Bereich `files` . Wenn Sie diesen Namen ändern, gehen alle am alten Speicherort gespeicherten Site-Daten verloren.

## `access`

Die Eigenschaft `access` gibt ein Minimum an Benutzerrollenebene an, das SSH-Zugriff auf die Umgebungen erlaubt. Die verfügbaren Benutzerrollen sind:

- `admin`: Kann Einstellungen ändern und Aktionen in der Umgebung ausführen; verfügt über die Berechtigungen _contributor_ und _viewer_ .
- `contributor`: Kann Code in diese Umgebung und die Verzweigung aus der Umgebung pushen; hat _Viewer_ -Rechte.
- `viewer` - Kann nur die Umgebung anzeigen.

Die standardmäßige Benutzerrolle ist `contributor`, wodurch der SSH-Zugriff von Benutzern mit nur _Viewer_ -Rechten eingeschränkt wird. Sie können die Benutzerrolle in &quot;`viewer`&quot; ändern, um Benutzern mit nur _Viewer_ -Rechten den SSH-Zugriff zu ermöglichen:

```yaml
access:
    ssh: viewer
```
