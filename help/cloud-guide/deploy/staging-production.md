---
title: Bereitstellen in Staging und Produktion
description: Erfahren Sie, wie Sie Ihren Adobe Commerce-Code für Cloud-Infrastruktur in den Staging- und Produktionsumgebungen für weitere Tests bereitstellen.
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 269681efb9925d78ffb608ecbef657be740b5531
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# Bereitstellen in Staging und Produktion

Der Prozess für die Bereitstellung und Live-Schaltung beginnt mit der Entwicklung, läuft weiter bis zum Staging und endet mit der Live-Schaltung in der Produktion. Adobe bietet eine End-to-End-Umgebungslösung zur Sicherstellung konsistenter Konfigurationen. Jede Umgebung unterstützt den direkten URL-Zugriff auf die Storefront sowie den Admin- und SSH-Zugriff für CLI-Befehle.

Wenn Sie bereit sind, Ihren Store bereitzustellen, müssen Sie die Bereitstellung und den Test in der Staging-Umgebung vor der Bereitstellung in der Produktion abschließen. Dieser Abschnitt enthält ausführliche Anweisungen und Informationen zum Build- und Bereitstellungsprozess, zur Migration von Daten und Inhalten sowie zum Testen.

>[!TIP]
>
>Adobe empfiehlt, vor der Bereitstellung eine [Sicherung](../storage/snapshots.md) der Umgebung zu erstellen.

Außerdem können Sie die [Nachverfolgung von Bereitstellungen mit New Relic](../monitor/track-deployments.md) aktivieren, um Bereitstellungsereignisse zu überwachen und die Leistung zwischen Bereitstellungen zu analysieren.

## Starter-Implementierungsfluss

Adobe empfiehlt, eine `staging` -Verzweigung aus der `master` -Verzweigung zu erstellen, um die Entwicklung und Bereitstellung Ihres Starter-Plans optimal zu unterstützen. Anschließend sind zwei Ihrer vier aktiven Umgebungen bereit: `master` für die Produktion und `staging` für die Staging-Umgebung.

Ausführliche Informationen zum Prozess finden Sie unter [Workflow &quot;Starter Dedevelop and Deploy&quot;(Starterentwicklung und -bereitstellung)](../architecture/starter-develop-deploy-workflow.md).

## Pro-Implementierungsfluss

Pro verfügt über eine große Integrationsumgebung mit zwei aktiven Verzweigungen, einer globalen `master`-Verzweigung, Staging- und Produktionsverzweigung. Wenn Sie Ihr Projekt erstellen, kann Code verzweigt, entwickelt und gepusht werden, um Ihre Website zu erstellen und bereitzustellen. Die Integrationsumgebung kann zwar viele Verzweigungen aufweisen, Staging und Produktion verfügen jedoch nur über eine Verzweigung für jede Umgebung.

Detaillierte Informationen zum Prozess finden Sie unter [Pro-Workflow für Entwicklung und Bereitstellung](../architecture/pro-develop-deploy-workflow.md).

## Bereitstellen von Code für Staging

Die Staging-Umgebung bietet eine nahezu produktionsorientierte Umgebung mit einer Datenbank, einem Webserver und allen Diensten, einschließlich Fastly und New Relic. Sie können die Cloud-CLI-Befehle [[!DNL Cloud Console]](../project/overview.md) oder [Cloud-CLI-Befehle](../dev-tools/cloud-cli-overview.md) vollständig über eine Terminal-Anwendung übertragen, zusammenführen und bereitstellen.

### Bereitstellen von Code mit dem [!DNL Cloud Console]

Der [!DNL Cloud Console] bietet Funktionen zum Erstellen, Verwalten und Bereitstellen von Code in Integrations-, Staging- und Produktionsumgebungen für Starter- und Pro-Pläne.

**Stellen Sie für Pro-Projekte die Integrationsverzweigung für Staging bereit**:

1. [Melden Sie sich ](https://accounts.magento.cloud) bei Ihrem Projekt an.
1. Wählen Sie den Zweig `integration` aus.
1. Wählen Sie die Option **Zusammenführen** aus, um sie für das Staging bereitzustellen.

   ![Zusammenführen](../../assets/button-merge.png){width="150"}

1. Schließen Sie alle [Tests](../test/staging-and-production.md) in der Staging-Umgebung ab.
1. Wenn das Staging fertig ist, wählen Sie die Option **Zusammenführen** aus, um sie für die Produktion bereitzustellen.

**Für Starter stellen Sie die Entwicklungsverzweigung für Staging** bereit:

1. [Melden Sie sich ](https://accounts.magento.cloud) bei Ihrem Projekt an.
1. Wählen Sie die vorbereitete Codeverzweigung aus.
1. Wählen Sie die Option **Zusammenführen** aus, um sie für das Staging bereitzustellen.

   ![Zusammenführen](../../assets/button-merge.png){width="150"}

1. Schließen Sie alle [Tests](../test/staging-and-production.md) in der Staging-Umgebung ab.
1. Wenn das Staging fertig ist, wählen Sie die Option **Zusammenführen** aus, um sie für die Produktion bereitzustellen (`master`).

### Bereitstellen von Code mit der Befehlszeile

Die Cloud-CLI bietet Befehle zum Bereitstellen von Code. Sie benötigen SSH- und Git-Zugriff auf Ihr Projekt.

#### Schritt 1: Bereitstellen und Testen der Integrationsumgebung

1. Nachdem Sie sich beim Projekt angemeldet haben, sehen Sie sich die Integrationsumgebung an:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchronisieren Sie Ihre lokale Integrationsumgebung mit der Remote-Umgebung:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Erstellen Sie einen Schnappschuss der Umgebung als Sicherung:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Aktualisieren Sie den Code in Ihrer lokalen Verzweigung nach Bedarf.

1. Hinzufügen, Übertragen und Pushen von Änderungen in die Umgebung.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Umfassende Site-Tests.

#### Schritt 2: Zusammenführen von Änderungen zu Staging und Bereitstellung

1. Sehen Sie sich die Staging-Umgebung an:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchronisieren Sie Ihre lokale Staging-Umgebung mit der Remote-Umgebung:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Erstellen Sie einen Schnappschuss der Umgebung als Sicherung:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Führen Sie die Integrationsumgebung zum Staging zusammen, um Folgendes bereitzustellen:

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Umfassende Site-Tests.

#### Schritt 3: Bereitstellen in der Produktion

1. Checken Sie die lokale Produktionsumgebung aus, synchronisieren Sie sie und erstellen Sie einen Schnappschuss.

1. Führen Sie die Staging-Umgebung zur Produktion zusammen, um Folgendes bereitzustellen:

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Umfassende Site-Tests.

## Migrieren von statischen Dateien

[Statische Dateien](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary) werden in `mounts` gespeichert. Es gibt zwei Methoden zum Migrieren von Dateien von einem Quellbereitstellungsspeicherort, wie z. B. Ihrer lokalen Umgebung, zu einem Ziel-Bereitstellungsspeicherort. Beide Methoden verwenden das Dienstprogramm `rsync` , Adobe empfiehlt jedoch die Verwendung der CLI `magento-cloud` für das Verschieben von Dateien zwischen der lokalen und der Remote-Umgebung. Adobe empfiehlt die Verwendung der `rsync`-Methode beim Verschieben von Dateien von einer Remote-Quelle an einen anderen Remote-Speicherort.

### Migrieren von Dateien mithilfe der CLI

Sie können die CLI-Befehle `mount:upload` und `mount:download` verwenden, um Dateien zwischen der lokalen und der Remote-Umgebung zu migrieren. Beide Befehle verwenden das Dienstprogramm `rsync` , die CLI-Befehle bieten jedoch Optionen und Eingabeaufforderungen, die auf die Adobe Commerce in der Cloud-Infrastrukturumgebung zugeschnitten sind. Wenn Sie beispielsweise den einfachen Befehl ohne Optionen verwenden, fordert Sie die CLI auf, auszuwählen, welche Bereitstellung oder Bereitstellung hochgeladen oder heruntergeladen werden soll.

```bash
magento-cloud mount:download
```

Beispielantwort:

```
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**So laden Sie Dateien aus einem lokalen `pub/media/` -Ordner in den Remote `pub/media/` -Ordner für die aktuelle Umgebung hoch**:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Beispielantwort:

```
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Verwenden Sie die Option `--help` für die Befehle `mount:upload` und `mount:download` , um weitere Optionen anzuzeigen. Beispielsweise gibt es eine `--delete` -Option, um irrelevante Dateien während der Migration zu entfernen.

### Migrieren von Dateien mit rsync

Alternativ können Sie das Dienstprogramm `rsync` verwenden, um Dateien zu migrieren.

```bash
rsync -azvP <source> <destination>
```

Dieser Befehl verwendet die folgenden Optionen:

- `a`-archive
- `z` komprimieren Dateien während der Migration
- `v`-verbose
- `P` partieller Fortschritt

Siehe Hilfe zu [rsync](https://linux.die.net/man/1/rsync) .

>[!NOTE]
>
>Um Medien direkt von Remote-zu-Remote-Umgebungen zu übertragen, müssen Sie die SSH-Agent-Weiterleitung aktivieren, siehe [GitHub-Anleitung](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**So migrieren Sie statische Dateien direkt von Remote-zu-Remote-Umgebungen (schneller Ansatz)**:

1. Verwenden Sie SSH, um sich bei der Quellumgebung anzumelden. Verwenden Sie nicht die CLI `magento-cloud` . Die Verwendung der Option `-A` ist wichtig, da sie die Weiterleitung der Verbindung des Authentifizierungsagenten ermöglicht.

   >[!TIP]
   >
   >Um den Link **SSH access** in Ihrem [!DNL Cloud Console] zu finden, wählen Sie die Umgebung aus und klicken Sie auf **Access Site**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Verwenden Sie den Befehl `rsync` , um den Ordner `pub/media` aus Ihrer Quellumgebung in eine andere Remote-Umgebung zu kopieren.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Melden Sie sich bei der anderen Remote-Umgebung an, um zu überprüfen, ob die Dateien erfolgreich migriert wurden.

## Datenbank migrieren

>[!WARNING]
>
>Der Import und Export von Datenbanken kann lange dauern, was sich auf die Leistung und Verfügbarkeit der Site auswirken kann. Planen Sie Import- und Exportvorgänge außerhalb der Spitzenzeiten, um eine langsame Leistung oder Ausfälle auf Produktions-Sites zu verhindern.

>[!BEGINSHADEBOX]

**Voraussetzung:** Ein Datenbank-Dump (siehe Schritt 3) sollte Trigger der Datenbank enthalten. Vergewissern Sie sich für das Dumping, dass Sie über die Berechtigung [TRIGGER](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger) verfügen.

>[!IMPORTANT]
>
>Die Integrationsumgebungs-Datenbank dient ausschließlich Entwicklungstests und kann Daten enthalten, die Sie nicht in Staging und Produktion migrieren möchten.

Bei kontinuierlichen Integrationsbereitstellungen empfiehlt Adobe **nicht die Migration von** Daten von der Integration in die Staging- und Produktionsumgebung. Sie können Testdaten übergeben oder wichtige Daten überschreiben. Alle wichtigen Konfigurationen werden beim Erstellen und Bereitstellen mithilfe des Befehls [Konfigurationsdatei](../store/store-settings.md) und `setup:upgrade` übergeben.

>[!ENDSHADEBOX]

Adobe **empfiehlt** die Migration von Daten aus der Produktion in die Staging-Umgebung, um Ihre Site vollständig zu testen und in einer Produktionsumgebung mit allen Diensten und Einstellungen zu speichern.

>[!NOTE]
>
>Um Medien direkt von Remote-zu-Remote-Umgebungen zu übertragen, müssen Sie die SSH-Agent-Weiterleitung aktivieren, siehe [GitHub-Anleitung](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Datenbank sichern

Es empfiehlt sich, eine Sicherung der Datenbank zu erstellen. Im folgenden Verfahren wird die Anleitung von [Datenbank sichern](../storage/database-dump.md) verwendet.

**So speichern Sie die Datenbank**:

1. [Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden](../development/secure-connections.md#use-an-ssh-command), die die zu kopierende Datenbank enthält.

1. Führen Sie die Umgebungsbeziehungen auf und notieren Sie sich die Informationen zur Datenbankanmeldung.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   Bei Pro Staging and Production befindet sich der Name der Datenbank in der Variable `MAGENTO_CLOUD_RELATIONSHIPS` (normalerweise identisch mit dem Anwendungsnamen und Benutzernamen).

1. Erstellen Sie eine Sicherung der Datenbank. Verwenden Sie die Option `--dump-directory` , um ein Zielverzeichnis für den DB-Dump auszuwählen.

   Verwenden Sie für Starter-Umgebungen und Pro-Integrationsumgebungen `main` als Namen der Datenbank:

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Dump-Optionen:
   - `--dump-directory=<dir>` - Wählen Sie ein Zielverzeichnis für den Datenbank-Dump
   - `--remove-definers`—DEFINER-Anweisungen aus der Datenbank-Dump entfernen

1. Obwohl die ECE-Tools-Methode bevorzugt wird, besteht eine andere Methode darin, eine Datenbank-Dump-Datei mit nativem MySQL im GZIP-Format zu erstellen.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Wenn Sie eine Authentifizierung mit zwei Faktoren für die Zielumgebung konfiguriert haben, sollten Sie entsprechende 2FA-Tabellen ausschließen, um eine Neukonfiguration nach der Datenbankmigration zu vermeiden:

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Geben Sie `logout` ein, um die SSH-Verbindung zu beenden.

### Datenbank ablegen und neu erstellen

Beim Datenimport müssen Sie eine Datenbank ablegen und erstellen.

**So legen Sie die Datenbank ab und erstellen sie neu**:

1. Richten Sie einen [SSH-Tunnel](../development/secure-connections.md#ssh-tunneling) in die Remote-Umgebung ein.

1. Stellen Sie eine Verbindung zum Datenbankdienst her.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. Legen Sie an der Eingabeaufforderung `MariaDB [main]>` die Datenbank ab.

   Für Starter- und Pro-Integration:

   ```shell
   drop database main;
   ```

   Für die Produktion:

   ```shell
   drop database <cluster-id>;
   ```

   Für das Staging:

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Erstellen Sie die Datenbank neu.

   Für Starter- und Pro-Integration:

   ```shell
   create database main;
   ```

1. Importieren Sie die Datenbank.

   Für Produktion importieren:

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Import für Staging:

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Diese Befehle dekomprimieren die Datenbank-Dump-Datei, entfernen die `DEFINER` -Anweisungen und importieren die Datenbank mit den angegebenen Anmeldeinformationen.
