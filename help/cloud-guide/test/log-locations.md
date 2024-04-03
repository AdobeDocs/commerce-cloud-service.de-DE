---
title: Protokolle anzeigen und verwalten
description: Machen Sie sich mit den in der Cloud-Infrastruktur verfügbaren Protokolldateitypen und deren Auffindbarkeit vertraut.
last-substantial-update: 2023-05-23T00:00:00Z
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Protokolle anzeigen und verwalten

Protokolle für Adobe Commerce in Cloud-Infrastrukturprojekten sind zur Fehlerbehebung bei Problemen mit [Hooks erstellen und bereitstellen](../application/hooks-property.md), Cloud-Services und der Adobe Commerce-Anwendung.

Sie können die Protokolle aus dem Dateisystem, dem [!DNL Cloud Console]und die `magento-cloud` CLI.

- **Dateisystem**—Die `/var/log` Das Systemverzeichnis enthält Protokolle für alle Umgebungen. Die `var/log/` enthält App-spezifische Protokolle, die für eine bestimmte Umgebung eindeutig sind. Diese Ordner werden nicht von Knoten in einem Cluster gemeinsam genutzt. In Pro-Produktions- und Staging-Umgebungen müssen Sie die Protokolle auf jedem Knoten überprüfen.

- **[!DNL Cloud Console]**—Sie können Protokollinformationen zum Build, zur Bereitstellung und nach der Bereitstellung in der Umgebung anzeigen. _messages_ Liste.

- **Cloud-CLI**—Sie können lokale Umgebungsprotokolle mit der `magento-cloud log` -Befehl oder Remote-Umgebungsprotokolle mit `magento-cloud ssh` Befehl.

## Protokollspeicherorte

Systemprotokolle werden an den folgenden Speicherorten gespeichert:

- Integration: `/var/log/<log-name>.log`
- Pro Staging: `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro Produktion: `/var/log/platform/<project-ID>/<log-name>.log`

Der Wert von `<project-ID>` hängt vom Projekt ab und davon, ob es sich bei der Umgebung um Staging oder Produktion handelt. Beispielsweise mit einer Projekt-ID von `yw1unoukjcawe`, lautet der Benutzer der Staging-Umgebung . `yw1unoukjcawe_stg` und der Benutzer der Produktionsumgebung `yw1unoukjcawe`.

In diesem Beispiel lautet das Bereitstellungsprotokoll: `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### Remote-Umgebungsprotokolle anzeigen

Die meisten Protokolle enthalten Ereignisse, die in der Remote-Umgebung auftreten. Für Pro gibt es mehrere Knoten und jeder Knoten verfügt über eindeutige Protokolle. Verwenden Sie Folgendes, um eine Liste aller Hosts anzuzeigen:

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Beispielantwort:

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**So zeigen Sie eine Liste der Remote-Umgebungsprotokolle an**:

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Beispiel für Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**So zeigen Sie ein Remote-Protokoll an**:

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Beispiel für Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>In Pro-Umgebungen sind die automatische Protokollierung von Rotation, Komprimierung und Entfernung für Protokolldateien mit einem festen Dateinamen aktiviert. Jeder Protokolldateityp verfügt über ein rotierendes Muster und eine Lebensdauer. Starterumgebungen haben keine Protokollrotation. Ausführliche Informationen zur Protokollrotation und Lebensdauer von komprimierten Protokollen finden Sie unter: `/etc/logrotate.conf` und `/etc/logrotate.d/<various>`

## Protokolle erstellen und bereitstellen

Nachdem Sie Änderungen an Ihre Umgebung gepusht haben, können Sie die Protokollierung von jedem Hook im `var/log/cloud.log` -Datei. Das Protokoll enthält Start- und Stopp-Meldungen für jeden Hook. Im folgenden Beispiel lautet die Meldung &quot;`Starting post-deploy.`&quot; und &quot;`Post-deploy is complete.`&quot;

Überprüfen Sie die Zeitstempel für Protokolleinträge, überprüfen Sie die Protokolle und suchen Sie nach den Protokollen für eine bestimmte Bereitstellung. Im Folgenden finden Sie ein gekürztes Beispiel für die Protokollausgabe, die Sie zur Fehlerbehebung verwenden können:

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>Wenn Sie Ihre Cloud-Umgebung konfigurieren, können Sie [protokollbasierte Slack- und E-Mail-Benachrichtigungen](../environment/set-up-notifications.md) für Build- und Bereitstellungsaktionen.

Die folgenden Protokolle haben einen gemeinsamen Speicherort für alle Cloud-Projekte:

- **Bereitstellungsprotokoll**: `var/log/cloud.log`
- **Fehlerprotokoll bei der letzten Bereitstellung**: `var/log/cloud.error.log`
- **Debug-Protokoll**: `var/log/debug.log`
- **Ausnahmeprotokoll**: `var/log/exception.log`
- **Systemprotokoll**: `var/log/system.log`
- **Support-Protokoll**: `var/log/support_report.log`
- **Berichte**: `var/report/`

Die `cloud.log` -Datei enthält Feedback aus jeder Phase des Bereitstellungsprozesses. Die vom Bereitstellungs-Hook erstellten Protokolle sind für jede Umgebung eindeutig. Das umgebungsspezifische Bereitstellungsprotokoll befindet sich in den folgenden Verzeichnissen:

- **Integration von Starter und Pro**: `/var/log/deploy.log`
- **Pro Staging**: `/var/log/platform/<project-ID>_stg/deploy.log`
- **Pro Produktion**: `/var/log/platform/<project-ID>/deploy.log`

### Bereitstellungsprotokoll

Das Protokoll für jede Bereitstellung verkettet sich mit dem spezifischen `deploy.log` -Datei. Im folgenden Beispiel wird das Bereitstellungsprotokoll der aktuellen Umgebung im Terminal gedruckt:

```bash
magento-cloud log -e <environment-ID> deploy
```

Beispielantwort:

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Fehlerprotokoll

Während des Bereitstellungsprozesses erzeugte Fehler- und Warnmeldungen werden sowohl in die `var/log/cloud.log` und `var/log/cloud.error.log` -Dateien. Die Fehlerprotokolldatei der Cloud enthält nur Fehler und Warnungen aus der neuesten Implementierung. Eine leere Datei weist auf eine erfolgreiche Implementierung ohne Fehler hin.

Sie können die Protokolldatei mit dem [Cloud CLI SSH](#view-remote-environment-logs)oder Sie können ECE-Tools verwenden, um die Fehler mit Vorschlägen anzuzeigen:

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Beispielantwort:

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

Die meisten Fehlermeldungen enthalten eine Beschreibung und eine empfohlene Aktion. Verwenden Sie die [Fehlermeldungsreferenz für ECE-Tools](../dev-tools/error-reference.md) , um den Fehlercode für weitere Anleitungen zu suchen. Für weitere Anleitungen verwenden Sie die [Fehlerbehebung bei der Adobe Commerce-Bereitstellung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Anwendungsprotokolle

Ähnlich wie bei Bereitstellungsprotokollen sind die Anwendungsprotokolle für jede Umgebung eindeutig:

| Protokolldatei | Starter- und Pro-Integration | Beschreibung |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Bereitstellungsprotokoll** | `/var/log/deploy.log` | Aktivität aus dem [Bereitstellungs-Hook](../application/hooks-property.md). |
| **Protokoll nach der Bereitstellung** | `/var/log/post_deploy.log` | Aktivität aus dem [Hook nach der Bereitstellung](../application/hooks-property.md). |
| **Cron-Protokoll** | `/var/log/cron.log` | Ausgabe aus Cron-Aufträgen. |
| **Nginx-Zugriffsprotokoll** | `/var/log/access.log` | Beim Start von Nginx werden HTTP-Fehler für fehlende Verzeichnisse und ausgeschlossene Dateitypen angezeigt. |
| **Nginx-Fehlerprotokoll** | `/var/log/error.log` | Startmeldungen, die für das Debugging von Konfigurationsfehlern im Zusammenhang mit Nginx nützlich sind. |
| **PHP-Zugriffsprotokoll** | `/var/log/php.access.log` | Anforderungen an den PHP-Dienst. |
| **PHP FPM-Protokoll** | `/var/log/app.log` | |

Für Staging- und Produktionsumgebungen für Pro sind die Protokolle Bereitstellung, Bereitstellung und Cron nur auf dem ersten Knoten im Cluster verfügbar:

| Protokolldatei | Pro Staging | Pro Produktion |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Bereitstellungsprotokoll** | Nur erster Knoten:<br>`/var/log/platform/<project-ID>_stg/deploy.log` | Nur erster Knoten:<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Protokoll nach der Bereitstellung** | Nur erster Knoten:<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | Nur erster Knoten:<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Cron-Protokoll** | Nur erster Knoten:<br>`/var/log/platform/<project-ID>_stg/cron.log` | Nur erster Knoten:<br>`/var/log/platform/<project-ID>/cron.log` |
| **Nginx-Zugriffsprotokoll** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Nginx-Fehlerprotokoll** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **PHP-Zugriffsprotokoll** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **PHP FPM-Protokoll** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### Archivierte Protokolldateien

Die Anwendungsprotokolle werden einmal täglich komprimiert und archiviert und ein Jahr lang aufbewahrt. Die komprimierten Protokolle werden mit einer eindeutigen ID benannt, die dem `Number of Days Ago + 1`. Beispielsweise wird in Pro-Produktionsumgebungen ein PHP-Zugriffsprotokoll für 21 Tage in der Vergangenheit gespeichert und wie folgt benannt:

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

Die archivierten Protokolldateien werden immer in dem Ordner gespeichert, in dem sich die Originaldatei vor der Komprimierung befunden hat.

>[!NOTE]
>
>**Bereitstellen** und **Nach der Bereitstellung** Protokolldateien werden nicht gedreht und archiviert. Der gesamte Bereitstellungsverlauf wird in diese Protokolldateien geschrieben.

## Dienstprotokolle

Da jeder Dienst in einem separaten Container ausgeführt wird, sind die Dienstprotokolle nicht in der Integrationsumgebung verfügbar. Adobe Commerce in der Cloud-Infrastruktur bietet nur Zugriff auf den Webserver-Container in der Integrationsumgebung. Die folgenden Dienstprotokollspeicherorte gelten für die Pro Production- und Staging-Umgebungen:

- **Redist-Protokoll**: `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **Elasticsearch-Protokoll**: `/var/log/elasticsearch/elasticsearch.log`
- **Java-Speicherbereinigungsprotokoll**: `/var/log/elasticsearch/gc.log`
- **Mail-Protokoll**: `/var/log/mail.log`
- **MySQL-Fehlerprotokoll**: `/var/log/mysql/mysql-error.log`
- **MySQL langsame Protokollierung**: `/var/log/mysql/mysql-slow.log`
- **RabbitMQ-Protokoll**: `/var/log/rabbitmq/rabbit@host1.log`

Dienstprotokolle werden je nach Protokolltyp für verschiedene Zeiträume archiviert und gespeichert. Beispielsweise haben MySQL-Protokolle die kürzeste Lebensdauer, die nach sieben Tagen entfernt wurde.

>[!TIP]
>
>Die Speicherorte der Protokolldateien in der skalierten Architektur hängen vom Knotentyp ab. Siehe [Protokollieren von Speicherorten in der skalierten Architektur](../architecture/scaled-architecture.md#log-locations) Thema.

## Protokolldaten für Pro Production und Staging

Verwenden Sie in Pro Production- und Staging-Umgebungen [Protokollverwaltung von New Relic](../monitor/log-management.md) in Ihr Projekt integriert ist, um aggregierte Protokolldaten aus allen Logs zu verwalten, die mit Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur verknüpft sind.

Das New Relic Logs-Programm bietet ein zentralisiertes Protokollverwaltungs-Dashboard zur Fehlerbehebung und Überwachung von Adobe Commerce in Cloud-Infrastruktur-Produktions- und Staging-Umgebungen. Das Dashboard bietet außerdem Zugriff auf Protokolldaten für die Services Fastly CDN, Image Optimization und Web Application Firewall (WAF). Siehe [New Relic-Dienste](../monitor/new-relic-service.md).
