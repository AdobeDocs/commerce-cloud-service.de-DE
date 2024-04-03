---
title: Dienste konfigurieren
description: Erfahren Sie, wie Sie von Adobe Commerce in der Cloud-Infrastruktur verwendete Dienste konfigurieren.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Dienste konfigurieren

Die `services.yaml` definiert die Dienste, die von Adobe Commerce in Cloud-Infrastrukturen wie MySQL, Redis und Elasticsearch oder OpenSearch unterstützt und verwendet werden. Sie müssen keine externen Dienstleister abonnieren. Diese Datei befindet sich im `.magento` -Verzeichnis Ihres Projekts.

Das Bereitstellungsskript verwendet die Konfigurationsdateien im `.magento` -Verzeichnis, um die Umgebung mit den konfigurierten Diensten bereitzustellen. Ein Dienst wird für Ihre Anwendung verfügbar, wenn er im [`relationships`](../application/properties.md#relationships) -Eigenschaft der `.magento.app.yaml` -Datei. Die `services.yaml` -Datei enthält die _type_ und _Disk_ -Werte. Der Diensttyp definiert den Dienst _name_ und _version_.

Durch das Ändern einer Dienstkonfiguration stellt eine Bereitstellung die Umgebung mit den aktualisierten Diensten bereit, was sich auf die folgenden Umgebungen auswirkt:

- Alle Starterumgebungen einschließlich Produktion `master`
- Umgebungen für Pro-Integration

{{pro-update-service}}

## Standard- und unterstützte Dienste

Die Cloud-Infrastruktur unterstützt und stellt die folgenden Dienste bereit:

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

Sie können Standardversionen und Festplattenwerte in der aktuellen, [default `services.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). Das folgende Beispiel zeigt die `mysql`, `redis`, `opensearch` oder `elasticsearch`, und `rabbitmq` Dienste, die in `services.yaml` Konfigurationsdatei:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## Dienstwerte

Sie müssen die Konfiguration der Dienst-ID und des Diensttyps angeben `type: <name>:<version>`. Wenn der Dienst persistenten Speicher verwendet, müssen Sie einen Festplattenwert angeben.

Verwenden Sie das folgende Format:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

Die `service-id` -Wert gibt den Dienst im Projekt an. Sie können nur alphanumerische Kleinbuchstaben verwenden: `a` nach `z` und `0` nach `9`, beispielsweise `redis`.

Diese _service-id_ -Wert wird in der [`relationships`](../application/properties.md#relationships) -Eigenschaft der `.magento.app.yaml` Konfigurationsdatei:

```yaml
relationships:
    redis: "<name>:redis"
```

Sie können für jeden Diensttyp mehrere Instanzen benennen. Sie können beispielsweise mehrere Redis-Instanzen verwenden - eine für die Sitzung und eine für den Cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

Umbenennen eines Dienstes im `services.yaml` file **permanent entfernen** Folgendes:

- Der vorhandene Dienst vor der Erstellung eines Dienstes mit dem von Ihnen angegebenen neuen Namen.
- Alle vorhandenen Daten für den Dienst werden entfernt. Adobe empfiehlt dringend, dass Sie [Sichern der Starterumgebung](../storage/snapshots.md) bevor Sie den Namen eines vorhandenen Dienstes ändern.

### `type`

Die `type` -Wert gibt den Dienstnamen und die Version an. Beispiel:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

Die `disk` gibt die Größe des persistenten Festplattenspeichers (in MB) an, der dem Dienst zugeordnet werden soll. Dienste, die persistenten Speicher verwenden, wie MySQL, müssen einen Festplattenwert bereitstellen. Dienste, die Speicher anstelle von persistentem Speicher verwenden, wie z. B. Redis, benötigen keinen Festplattenwert.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Der aktuelle standardmäßige Speicherbetrag pro Projekt beträgt 5 GB oder 512 0 MB. Sie können diesen Betrag zwischen Ihrer Anwendung und den einzelnen Diensten verteilen.

## Service-Beziehungen

In Adobe Commerce zu Cloud-Infrastrukturprojekten, Service [Beziehungen](../application/properties.md#relationships) in der `.magento.app.yaml` -Datei bestimmen, welche Dienste für Ihre Anwendung verfügbar sind.

Sie können die Konfigurationsdaten für alle Dienstbeziehungen aus der [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) Umgebungsvariable. Die Konfigurationsdaten umfassen den Dienstnamen, den Typ und die Version sowie alle erforderlichen Verbindungsdetails wie die Portnummer und Anmeldedaten.

**Überprüfen von Beziehungen in einer lokalen Umgebung**:

1. Zeigen Sie in Ihrer lokalen Umgebung die Beziehungen für die aktive Umgebung an.

   ```bash
   magento-cloud relationships
   ```

1. Bestätigen Sie die `service` und `type` aus der Antwort. Die Antwort enthält Informationen zur Verbindung, wie die IP-Adresse und die Portnummer.

   >Abgekürzte Probenantwort

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**Überprüfen von Beziehungen in Remote-Umgebungen**:

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

1. Auflisten der Daten zur Beziehungskonfiguration für alle in der Umgebung konfigurierten Dienste.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   oder verwenden Sie Folgendes `ece-tools` Befehl zum Anzeigen von Beziehungen:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Bestätigen Sie die `service` und `type` aus der Antwort. Die Antwort enthält Verbindungsinformationen, wie die IP-Adresse und die Portnummer sowie alle erforderlichen Benutzernamen- und Kennwortberechtigungen.

## Dienstversionen

Die Service-Version und die Kompatibilitätsunterstützung für Adobe Commerce in der Cloud-Infrastruktur werden durch Versionen bestimmt, die in der Cloud-Infrastruktur bereitgestellt und getestet werden. Manchmal unterscheiden sie sich von den Versionen, die von lokalen Adobe Commerce-Implementierungen unterstützt werden. Siehe [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im _Installation_ Anleitung für eine Liste von Softwareabhängigkeiten von Drittanbietern, die Adobe mit bestimmten Adobe Commerce- und Magento Open Source-Versionen getestet hat.

### Software-EOL-Prüfungen

Während des Bereitstellungsprozesses wird die Variable `ece-tools` -Paket überprüft installierte Service-Versionen anhand des Lebenszyklusdatums (End of Life, EOL) für jeden Dienst.

- Wenn eine Dienstversion innerhalb von drei Monaten nach dem Datum der Einstellung der Bereitstellung verfügbar ist, wird eine Benachrichtigung im Bereitstellungsprotokoll angezeigt.
- Wenn das Datum der Einstellung &quot;Ende&quot;in der Vergangenheit liegt, wird eine Warnmeldung angezeigt.

Um die Speichersicherheit zu gewährleisten, aktualisieren Sie installierte Softwareversionen, bevor sie EOL erreichen. Sie können die EOL-Daten im Abschnitt [ece-tools&#39; `eol.yaml` file](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### Zu OpenSearch migrieren

{{elasticsearch-support}}

Informationen zu Adobe Commerce-Version 2.4.4 und höher finden Sie unter [Einrichten des OpenSearch-Dienstes](opensearch.md).

## Dienstversion ändern

Sie können die installierte Dienstversion aktualisieren, um die Kompatibilität mit der in Ihrer Cloud-Umgebung bereitgestellten Adobe Commerce-Version sicherzustellen.

Sie können die Dienstversion für einen installierten Dienst nicht direkt herunterstufen. Sie können jedoch einen Dienst mit der erforderlichen Version erstellen. Siehe [Downgrade-Service-Version](#downgrade-version).

### Upgrade der installierten Dienstversion

Sie können die installierte Dienstversion aktualisieren, indem Sie die Dienstkonfiguration im Abschnitt `services.yaml` -Datei.

1. Ändern Sie die [`type`](#type) -Wert für den Dienst im `.magento/services.yaml` Datei:

   > Definition des ursprünglichen Dienstes

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Aktualisierte Dienstdefinition

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Downgrade-Version

Sie können einen installierten Dienst nicht direkt herunterladen. Sie haben zwei Optionen:

1. Benennen Sie einen vorhandenen Dienst mit der neuen Version um, die den vorhandenen Dienst und die vorhandenen Daten entfernt und einen neuen hinzufügt.

1. Erstellen Sie einen Dienst und speichern Sie die Daten aus dem vorhandenen Dienst.

Wenn Sie die Dienstversion ändern, müssen Sie die Dienstkonfiguration im `services.yaml` und aktualisieren Sie die Beziehungen in der `.magento.app.yaml` -Datei.

**So aktualisieren Sie eine Dienstversion durch Umbenennen eines vorhandenen Dienstes**:

1. Benennen Sie den vorhandenen Dienst im `.magento/services.yaml` und ändern Sie die Version.

   >[!WARNING]
   >
   >Durch die Umbenennung eines vorhandenen Dienstes wird dieser ersetzt und alle Daten gelöscht. Wenn Sie die Daten beibehalten müssen, erstellen Sie einen Dienst, anstatt den vorhandenen umzubenennen.

   So können Sie beispielsweise die MariaDB-Version für die _mysql_ Dienst von Version 10.4 auf Version 10.3 ändern, die vorhandene _service-id_ und _type_ Konfiguration.

   > Original `services.yaml` Definition

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Neu `services.yaml` Definition

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Aktualisieren Sie die Beziehungen in der `.magento.app.yaml` -Datei.

   > Original `.magento.app.yaml` Konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Aktualisiert `.magento.app.yaml` Konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

**So aktualisieren Sie einen Dienst durch Erstellen eines Dienstes**:

1. Hinzufügen einer Dienstdefinition zum `services.yaml` -Datei für Ihr Projekt mit der heruntergestuften Versionsspezifikation. Siehe _mysql2_ im folgenden Beispiel:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Ändern Sie die Beziehungskonfiguration in der `.magento.app.yaml` -Datei, um den neuen Dienst zu verwenden.

   > Original `.magento.app.yaml` Konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Neu `.magento.app.yaml` Konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.
