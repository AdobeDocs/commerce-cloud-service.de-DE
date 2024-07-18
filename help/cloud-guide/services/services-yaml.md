---
title: Dienste konfigurieren
description: Erfahren Sie, wie Sie von Adobe Commerce in der Cloud-Infrastruktur verwendete Dienste konfigurieren.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: c39332d352f6dcb6f92c312a6ef1b74319d37aa3
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Dienste konfigurieren

Die Datei &quot;`services.yaml`&quot; definiert die Dienste, die von Adobe Commerce in der Cloud-Infrastruktur wie MySQL, Redis und Elasticsearch oder OpenSearch unterstützt und verwendet werden. Sie müssen keine externen Dienstleister abonnieren. Diese Datei befindet sich im Ordner &quot;`.magento`&quot; Ihres Projekts.

Das Bereitstellungsskript verwendet die Konfigurationsdateien im Ordner &quot;`.magento`&quot;, um die Umgebung mit den konfigurierten Diensten bereitzustellen. Ein Dienst wird für Ihre Anwendung verfügbar, wenn er in der Eigenschaft [`relationships`](../application/properties.md#relationships) der Datei `.magento.app.yaml` enthalten ist. Die Datei `services.yaml` enthält die Werte _type_ und _disk_. Der Diensttyp definiert den Dienst _name_ und _version_.

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

Sie können Standardversionen und Festplattenwerte in der aktuellen Datei [default `services.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml) anzeigen. Das folgende Beispiel zeigt die Dienste `mysql`, `redis`, `opensearch` oder `elasticsearch` und `rabbitmq`, die in der Konfigurationsdatei `services.yaml` definiert sind:

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

Sie müssen die Dienstkennung und die Diensttypkonfiguration `type: <name>:<version>` angeben. Wenn der Dienst persistenten Speicher verwendet, müssen Sie einen Festplattenwert angeben.

Verwenden Sie das folgende Format:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

Der Wert `service-id` gibt den Dienst im Projekt an. Sie können nur alphanumerische Kleinbuchstaben verwenden: `a` bis `z` und `0` bis `9`, z. B. `redis`.

Dieser Wert _service-id_ wird in der Eigenschaft [`relationships`](../application/properties.md#relationships) der Konfigurationsdatei `.magento.app.yaml` verwendet:

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

Beim Umbenennen eines Dienstes in der Datei `services.yaml` **wird** dauerhaft entfernt:

- Der vorhandene Dienst vor der Erstellung eines Dienstes mit dem von Ihnen angegebenen neuen Namen.
- Alle vorhandenen Daten für den Dienst werden entfernt. Adobe empfiehlt dringend, dass Sie [Ihre Starterumgebung sichern](../storage/snapshots.md), bevor Sie den Namen eines vorhandenen Dienstes ändern.

### `type`

Der Wert `type` gibt den Dienstnamen und die Version an. Beispiel:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

Der Wert `disk` gibt die Größe des persistenten Festplattenspeichers (in MB) an, der dem Dienst zugewiesen werden soll. Dienste, die persistenten Speicher verwenden, wie MySQL, müssen einen Festplattenwert bereitstellen. Dienste, die Speicher anstelle von persistentem Speicher verwenden, wie z. B. Redis, benötigen keinen Festplattenwert.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Der aktuelle standardmäßige Speicherbetrag pro Projekt beträgt 5 GB oder 512 0 MB. Sie können diesen Betrag zwischen Ihrer Anwendung und den einzelnen Diensten verteilen.

## Service-Beziehungen

In Adobe Commerce für Cloud-Infrastrukturprojekte bestimmen die in der Datei `.magento.app.yaml` konfigurierten Service [beziehungen](../application/properties.md#relationships) , welche Dienste für Ihre Anwendung verfügbar sind.

Sie können die Konfigurationsdaten für alle Dienstbeziehungen aus der Umgebungsvariablen [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) abrufen. Die Konfigurationsdaten umfassen den Dienstnamen, den Typ und die Version sowie alle erforderlichen Verbindungsdetails wie die Portnummer und Anmeldedaten.

**Überprüfen der Beziehungen in der lokalen Umgebung**:

1. Zeigen Sie in Ihrer lokalen Umgebung die Beziehungen für die aktive Umgebung an.

   ```bash
   magento-cloud relationships
   ```

1. Bestätigen Sie die `service` und `type` aus der Antwort. Die Antwort enthält Informationen zur Verbindung, wie die IP-Adresse und die Portnummer.

   >Abgekürzte Probenantwort

   ```yaml
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

   oder verwenden Sie den folgenden `ece-tools`-Befehl, um Beziehungen anzuzeigen:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Bestätigen Sie die `service` und `type` aus der Antwort. Die Antwort enthält Verbindungsinformationen, wie die IP-Adresse und die Portnummer sowie alle erforderlichen Benutzernamen- und Kennwortberechtigungen.

## Dienstversionen

Die Service-Version und die Kompatibilitätsunterstützung für Adobe Commerce in der Cloud-Infrastruktur werden durch Versionen bestimmt, die in der Cloud-Infrastruktur bereitgestellt und getestet werden. Manchmal unterscheiden sie sich von den Versionen, die von lokalen Adobe Commerce-Implementierungen unterstützt werden. Eine Liste der Softwareabhängigkeiten von Drittanbietern, die Adobe mit bestimmten Adobe Commerce- und Magento Open Source-Versionen getestet hat, finden Sie unter [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im Handbuch _Installation_ .

### Software-EOL-Prüfungen

Während des Bereitstellungsprozesses prüft das `ece-tools` -Paket installierte Dienstversionen anhand des Enddatums (End of Life, EOL) für jeden Dienst.

- Wenn eine Dienstversion innerhalb von drei Monaten nach dem Datum der Einstellung der Bereitstellung verfügbar ist, wird eine Benachrichtigung im Bereitstellungsprotokoll angezeigt.
- Wenn das Datum der Einstellung &quot;Ende&quot;in der Vergangenheit liegt, wird eine Warnmeldung angezeigt.

Um die Speichersicherheit zu gewährleisten, aktualisieren Sie installierte Softwareversionen, bevor sie EOL erreichen. Sie können die EOL-Daten in der Datei `eol.yaml` ](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml) der [ece-tools&#39; überprüfen.

### Zu OpenSearch migrieren

{{elasticsearch-support}}

Informationen zur Adobe Commerce-Version 2.4.4 und höher finden Sie unter [Einrichten des OpenSearch-Dienstes](opensearch.md).

## Dienstversion ändern

Sie können die installierte Dienstversion aktualisieren, um die Kompatibilität mit der in Ihrer Cloud-Umgebung bereitgestellten Adobe Commerce-Version sicherzustellen.

Sie können die Dienstversion für einen installierten Dienst nicht direkt herunterstufen. Sie können jedoch einen Dienst mit der erforderlichen Version erstellen. Siehe [Dienstversion herunterladen](#downgrade-version).

### Upgrade der installierten Dienstversion

Sie können die installierte Dienstversion aktualisieren, indem Sie die Dienstkonfiguration in der Datei `services.yaml` aktualisieren.

1. Ändern Sie den [`type`](#type) -Wert für den Dienst in der Datei `.magento/services.yaml` :

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

Wenn Sie die Dienstversion ändern, müssen Sie die Dienstkonfiguration in der Datei `services.yaml` aktualisieren und die Beziehungen in der Datei `.magento.app.yaml` aktualisieren.

**So stufen Sie eine Dienstversion herunter, indem Sie einen vorhandenen Dienst umbenennen**:

1. Benennen Sie den vorhandenen Dienst in der Datei `.magento/services.yaml` um und ändern Sie die Version.

   >[!WARNING]
   >
   >Durch die Umbenennung eines vorhandenen Dienstes wird dieser ersetzt und alle Daten gelöscht. Wenn Sie die Daten beibehalten müssen, erstellen Sie einen Dienst, anstatt den vorhandenen umzubenennen.

   Um beispielsweise die MariaDB-Version für den Dienst _mysql_ von Version 10.4 auf Version 10.3 herabzustufen, ändern Sie die vorhandene Konfiguration _service-id_ und _type_ .

   > Originaldefinition `services.yaml`

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Neue Definition `services.yaml`

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Aktualisieren Sie die Beziehungen in der Datei &quot;`.magento.app.yaml`&quot;.

   > Ursprüngliche `.magento.app.yaml` -Konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Aktualisierte `.magento.app.yaml` -Konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

**So stufen Sie einen Dienst herunter, indem Sie einen Dienst erstellen**:

1. Fügen Sie der Datei `services.yaml` für Ihr Projekt eine Dienstdefinition mit der heruntergestuften Versionsspezifikation hinzu. Siehe _mysql2_ im folgenden Beispiel:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Ändern Sie die Beziehungskonfiguration in der Datei `.magento.app.yaml` , um den neuen Dienst zu verwenden.

   > Ursprüngliche `.magento.app.yaml` -Konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Neue `.magento.app.yaml`-Konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.
