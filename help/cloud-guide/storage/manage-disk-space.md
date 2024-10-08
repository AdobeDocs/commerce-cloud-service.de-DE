---
title: Verwalten des Festplattenspeichers
description: Erfahren Sie, wie Sie Speicherplatz über die Befehlszeilenschnittstelle verwalten.
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 0cc0b8e49e2cccf4266ecf84ef935f24fde1c7a4
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Verwalten des Festplattenspeichers

Die Gesamtspeicherkapazität für Ihr Cloud-Projekt finden Sie in Ihrem Adobe Commerce-Vertrag für die Cloud-Infrastruktur und auf Ihrer [Kontoseite](https://accounts.magento.cloud/user). Jede Projektkarte in Ihrem Konto zeigt die Anzahl der _Umgebungen_, die _Speicherkapazität_ in GB und die Anzahl der _Benutzer_. Alternativ können Sie den folgenden Cloud-Befehl verwenden:

```bash
magento-cloud subscription:info | grep storage
```

Beispielantwort:

```
| storage              | 51200
```

Wenn eine Pro-Produktions- oder Staging-Umgebung 95 % der Speicherkapazität erreicht oder überschreitet, wird vom Cloud-Infrastruktur-Monitoring-Tool ein Support-Warnhinweis Trigger, der Sie über eine automatische Steigerung der Speicherkapazität informiert.

Beispielbenachrichtigung:

>[!BEGINSHADEBOX]

_&quot;Unser Monitoring hat den Dateispeicher auf Ihrem Cluster (Projekt-ID-Umgebung) nahezu vollständig erkannt. Die Festplattenauslastung liegt derzeit bei einem kritischen Nutzungsumfang mit weniger als 1 GiB. Das gemeinsam genutzte Speichervolumen wird derzeit von 60 GiB auf 70 GiB aktualisiert, um Ihre Dienste betriebsbereit zu halten. Sehen Sie sich die Verwendung von Produktions- und Staging-Dateien an, um zu sehen, ob Sie Speicherplatz freigeben können.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>Es wird empfohlen, Ihre Speicherkapazität regelmäßig zu überwachen und deutlich unter 90 % zu halten, um diese automatischen Erhöhungen zu vermeiden. Nach der Zuweisung kann die Speichersteigerung für Pro Staging und Produktion nicht mehr rückgängig gemacht werden.

## Integrationsumgebung überprüfen

Sie können die Festplattenspeicherplatznutzung für Ihre Integrationsumgebung mithilfe der `magento-cloud`-CLI überprüfen.

**So überprüfen Sie die ungefähre Festplattenspeicherplatznutzung**:

```bash
magento-cloud db:size
```

Beispielantwort:

```
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Alle Halterungen teilen sich eine Festplatte. Mit der CLI `magento-cloud` können Sie die Festplattenspeicherplatznutzung auf Bereitstellungen überprüfen.

**So überprüfen Sie die ungefähre Festplattenspeicherplatznutzung für Bereitstellungen**:

```bash
magento-cloud mount:size
```

Beispielantwort:

```
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Überprüfen dedizierter Cluster

Bei Pro-Staging- und Produktionsumgebungen können Sie die Speichernutzung in jeder Umgebung mithilfe des Befehls `disk free` überprüfen, der die vom Dateisystem verwendete Festplattenspeichermenge angibt. Sie müssen SSH verwenden, um sich bei einer Remote-Umgebung anzumelden.

```bash
df -h
```

Die Option &quot;`-h`&quot; zeigt den Bericht in einem für Menschen lesbaren Format an (KB, MB oder GB).

In der folgenden Beispielantwort zeigt die `/data/exports` -Bereitstellung den Festplattenspeicher für Medien und die `/data/mysql/` -Bereitstellung zeigt Festplattenspeicher für die Datenbank an:

```
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

Sie können die Antwort einschränken, indem Sie ein Verzeichnis angeben. Beispiel:

```bash
df -h var/
```

Beispielantwort:

```
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Speicherplatz zuweisen

Zwei [Konfigurationsdateien](../environment/overview.md) steuern die Zuweisung von Speicherplatz in den Cloud-Umgebungen: die Datei `.magento.app.yaml` und die Datei `.magento/services.yaml`. Jede Datei enthält die Eigenschaft `disk` , die den Wert der Festplattengröße in MB für die jeweilige Konfiguration definiert. Sie können die Speicherplatzzuweisung nur in Pro-Integration- und Starter-Umgebungen ändern.

>[!IMPORTANT]
>
>Für Pro-Produktions- und Staging-Umgebungen müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um die Speicherplatzzuweisung zu ändern. Eine Vergrößerung der Pro Produktions- und Staging-Umgebungen kann nur in bestimmten Intervallen erfolgen. Je nach aktueller Festplattenspeicherplatzbelegung wird daher unter Umständen empfohlen, die Speicherplatzzuweisung um mindestens 10 GB zu erhöhen. Nach der Zuweisung kann die Speichersteigerung für Pro Staging und Produktion nicht mehr rückgängig gemacht werden. Der Speicher kann nicht auf Ressourcen umverteilt oder neu verteilt werden. Um mehr Dateispeicher hinzuzufügen, reduzieren Sie den für MySQL zugewiesenen Speicherplatz.

### Anwendungsspeicherplatz

Die Datei `.magento.app.yaml` steuert den [persistenten Speicherplatz](../application/properties.md#disk), der für die Anwendung verfügbar ist.

**So erhöhen Sie den Speicherplatz für Ihre Anwendung**:

1. Öffnen Sie in Ihrer lokalen Entwicklungsumgebung die Konfigurationsdatei `.magento.app.yaml` .

1. Legen Sie einen neuen Wert für die Eigenschaft `disk` fest (in MB).

   ```yaml
   disk: <value-mb>
   ```

1. Speichern Sie die Änderungen in der Datei.

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   Die Änderungen werden wirksam, nachdem Sie die aktualisierte YAML-Datei in die Remote-Umgebung gepusht haben.

### Dienstspeicherplatz

Die Datei &quot;`.magento/services.yaml`&quot; steuert den für jeden Dienst verfügbaren Speicherplatz, z. B. MySQL und Redis.

**Erhöhen des Festplattenspeichers für einen Dienst**:

1. Öffnen Sie in Ihrer lokalen Entwicklungsumgebung die Konfigurationsdatei `.magento/services.yaml` .

1. Fügen Sie einen Dienst hinzu oder suchen Sie ihn in der Datei. Weitere Informationen finden Sie unter [ Informationen zum Konfigurieren von Diensten](../services/services-yaml.md).

1. Legen Sie einen neuen Wert für die Disk-Eigenschaft fest (in MB).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Speichern Sie die Änderungen in der Datei.

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   Die Änderungen werden wirksam, nachdem Sie die aktualisierte YAML-Datei in die Remote-Umgebung gepusht haben.

## Festplattenspeicher überwachen

In Pro-Produktionsumgebungen können Sie Speicherplatz und andere Leistungsindikatoren mithilfe der Richtlinie Warnhinweise für Adobe Commerce für New Relic verwalten überwachen. Weitere Informationen finden Sie unter [Überwachen der Leistung mit verwalteten Warnhinweisen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Weitere Anleitungen finden Sie unter [Best Practices zur Lösung von Problemen mit der Datenbankleistung](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## Kein Leerzeichen übrig

Der Build-Cache kann mit der Zeit wachsen. Wenn Sie eine Warnung mit dem Status &quot;`No space left on device`&quot;erhalten, versuchen Sie, den Build-Cache zu leeren und erneut bereitzustellen:

```bash
magento-cloud project:clear-build-cache
```
