---
title: MySQL-Dienst einrichten
description: Erfahren Sie, wie Sie den MySQL-Dienst für persistente Datenspeicherung mit Adobe Commerce in der Cloud-Infrastruktur verwalten.
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
source-git-commit: 9be8d1e062ab3dba86bc4d9c9ee8b8ece33d5b75
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# MySQL-Dienst einrichten

Der `mysql`-Dienst bietet eine beständige Datenspeicherung basierend auf den [MariaDB](https://mariadb.com/)-Versionen 10.2 bis 10.4, die die [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) -Speichermodul unterstützt und Funktionen von MySQL 5.6 und 5.7 neu implementiert.

Die Neuindizierung auf MariaDB 10.4 nimmt im Vergleich zu anderen MariaDB- oder MySQL-Versionen mehr Zeit in Anspruch. Siehe [Indexer](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) im Handbuch _Best Practices für die Leistung_.

>[!WARNING]
>
>Gehen Sie beim Aktualisieren von MariaDB von Version 10.1 auf Version 10.2 vorsichtig vor. MariaDB 10.1 ist die letzte Version, die _XtraDB_ als Speicher-Engine unterstützt. MariaDB 10.2 verwendet _InnoDB_ für die Speicher-Engine. Nach dem Upgrade von 10.1 auf 10.2 können Sie die Änderung nicht zurücksetzen. Adobe Commerce unterstützt beide Speicher-Engines. Sie müssen jedoch Erweiterungen und andere von Ihrem Projekt verwendete Systeme überprüfen, um sicherzustellen, dass sie mit MariaDB 10.2 kompatibel sind. Siehe [Inkompatible Änderungen zwischen 10.1 und 10.2](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**So aktivieren Sie MySQL**:

1. Fügen Sie der Datei `.magento/services.yaml` den erforderlichen Namen, Typ und Festplattenwert (in MB) hinzu.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >MySQL-Fehler, wie z. B. `PDO Exception: MySQL server has gone away`, können auf ungenügenden Speicherplatz zurückzuführen sein. Vergewissern Sie sich, dass Sie dem Dienst in der Datei [`.magento/services.yaml`](services-yaml.md#disk) ausreichend Speicherplatz zugewiesen haben.

1. Konfigurieren Sie die Beziehungen in der Datei &quot;`.magento.app.yaml`&quot;.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [Überprüfen Sie die Dienstbeziehungen](services-yaml.md#service-relationships).

{{service-change-tip}}

## MySQL-Datenbank konfigurieren

Sie haben beim Konfigurieren der MySQL-Datenbank die folgenden Optionen:

- **`schemas`** - Ein Schema definiert eine Datenbank. Das Standardschema ist die `main` -Datenbank.
- **`endpoints`**: Jeder Endpunkt stellt eine Berechtigung mit bestimmten Berechtigungen dar. Der standardmäßige Endpunkt ist `mysql`, der `admin` Zugriff auf die `main` -Datenbank hat.
- **`properties`**—Eigenschaften werden verwendet, um zusätzliche Datenbankkonfigurationen zu definieren.

Im Folgenden finden Sie eine grundlegende Beispielkonfiguration in der Datei `.magento/services.yaml` :

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

Mit dem Wert `properties` im obigen Beispiel werden die standardmäßigen `optimizer`-Einstellungen wie im Leitfaden zu Leistungsempfehlungen ](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) empfohlen geändert.[

**MariaDB-Konfigurationsoptionen**:

| Optionen | Beschreibung | Standardwert |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | Der Standardzeichensatz. | utf8mb4 |
| `default_collation` | Die Standardsortierung. | utf8mb4_unicode_ci |
| `max_allowed_packet` | Maximale Größe für Pakete in MB. Bereich `1` bis `100`. | 16 |
| `optimizer_switch` | Legen Sie Werte für den Abfrageoptimierer fest. Siehe [MariaDB-Dokumentation](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Wählen Sie die vom Optimierer verwendeten Statistiken aus. Bereich `1` bis `5`. Siehe [MariaDB-Dokumentation](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 für 10.4 und höher |

### Mehrere Datenbankbenutzer einrichten

Optional können Sie mehrere Benutzer mit unterschiedlichen Berechtigungen für den Zugriff auf die `main` -Datenbank einrichten.

Standardmäßig gibt es einen Endpunkt mit dem Namen `mysql`, der Administratorzugriff auf die Datenbank hat. Um mehrere Datenbankbenutzer einzurichten, müssen Sie mehrere Endpunkte in der Datei `services.yaml` definieren und die Beziehungen in der Datei `.magento.app.yaml` deklarieren. Senden Sie für Pro-Staging- und Produktionsumgebungen ein Adobe Commerce-Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um den zusätzlichen Benutzer anzufordern.[

Verwenden Sie ein verschachteltes Array, um die Endpunkte für den spezifischen Benutzerzugriff zu definieren. Jeder Endpunkt kann den Zugriff auf ein oder mehrere Schemas (Datenbanken) und verschiedene Berechtigungsstufen für jedes einzelne Schema angeben.

Gültige Berechtigungsstufen sind:

- `ro`: Nur SELECT-Abfragen sind zulässig.
- `rw`: SELECT-Abfragen und INSERT-, UPDATE- und DELETE-Abfragen sind zulässig.
- `admin`: Alle Abfragen sind zulässig, einschließlich DDL-Abfragen (CREATE TABLE, DROP TABLE usw.).

Beispiel:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

Im vorherigen Beispiel bietet der Endpunkt `admin` Zugriff auf die Datenbank auf Administratorebene, der Endpunkt `reporter` bietet schreibgeschützten Zugriff und der Endpunkt `importer` bietet Lese- und Schreibzugriff, d. h.:`main`

- Der Benutzer `admin` hat die volle Kontrolle über die Datenbank.
- Der Benutzer `reporter` verfügt nur über SELECT-Berechtigungen.
- Der Benutzer `importer` verfügt über die Berechtigungen SELECT, INSERT, UPDATE und DELETE.

Fügen Sie die im obigen Beispiel definierten Endpunkte zur Eigenschaft `relationships` der Datei `.magento.app.yaml` hinzu. Beispiel:

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>Wenn Sie einen MySQL-Benutzer konfigurieren, können Sie den Zugriffskontrollmechanismus für gespeicherte Prozeduren und Ansichten nicht verwenden.[`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html)

## Verbindung zur Datenbank herstellen

Für den direkten Zugriff auf die MariaDB-Datenbank müssen Sie eine SSH verwenden, um sich bei der Remote-Cloud-Umgebung anzumelden und eine Verbindung zur Datenbank herzustellen.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Rufen Sie die Anmeldedaten für MySQL aus den Eigenschaften `database` und `type` in der Variablen [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) ab.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   oder

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Suchen Sie in der Antwort die MySQL-Informationen. Beispiel:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Stellen Sie eine Verbindung zur Datenbank her.

   - Verwenden Sie für Starter den folgenden Befehl:

     ```bash
     mysql -h database.internal -u <username>
     ```

   - Verwenden Sie für Pro den folgenden Befehl mit Hostname, Portnummer, Benutzername und Kennwort, die aus der Variable &quot;`$MAGENTO_CLOUD_RELATIONSHIPS`&quot;abgerufen werden.

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>Mit dem Befehl `magento-cloud db:sql` können Sie eine Verbindung zur Remote-Datenbank herstellen und SQL-Befehle ausführen.

## Verbindung zur sekundären Datenbank herstellen

>[!IMPORTANT]
>
>Diese Funktion ist nur für Pro Production- und Staging-Cluster verfügbar.

Manchmal müssen Sie eine Verbindung zur sekundären Datenbank herstellen, um die Datenbankleistung zu verbessern oder Probleme mit der Datenbanksperrung zu beheben. Wenn diese Konfiguration erforderlich ist, verwenden Sie `"port" : 3304` , um die Verbindung herzustellen. Weitere Informationen finden Sie unter dem Thema [Best Practices zum Konfigurieren der MySQL-Slave-Verbindung](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) im Handbuch _Best Practices für die Implementierung_ .

## Fehlerbehebung

In den folgenden Adobe Commerce-Supportartikeln finden Sie Hilfe zur Fehlerbehebung bei MySQL-Problemen:

- [Überprüfen langsamer Abfragen und Prozesse MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [Datenbank-Dump in Cloud erstellen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [Fehlerbehebung beim Datenmigrationswerkzeug](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Adobe Commerce-Upgrade: kompakt in dynamische Tabellen 2.2.x, 2.3.x auf 2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
