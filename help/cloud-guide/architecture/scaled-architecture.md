---
title: Skalierte Architektur
description: Erfahren Sie mehr über die Aufspaltungsarchitektur und deren Skalierung zur Erfüllung der Anforderungen.
feature: Cloud, Auto Scaling, Iaas, Logs
exl-id: c54d8772-b6cc-41cc-b1ab-bef7d6f13bf2
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Skalierte Architektur

Die Cloud-Infrastruktur wird entsprechend Ihren Ressourcenanforderungen skaliert, um eine höhere Effizienz zu erzielen. Adobe Commerce on Cloud Infrastructure überwacht Ihre Anwendungen und kann die Kapazität anpassen, um eine stabile, vorhersehbare Leistung zu gewährleisten. Die Konvertierung in diese Architektur hilft, Probleme wie Latenzzeiten oder große Traffic-Spitzen zu vermeiden.

>[!NOTE]
>
>Die skalierte Architektur ist für Adobe Commerce auf Cloud-Infrastrukturkonten mit dem Pro 48-Cluster oder höher verfügbar.

## Aufspaltung-Architektur

Historisch betrachtet bestand die Pro-Architektur aus drei Knoten, von denen jeder einen vollständigen Tech-Stapel enthielt. Jetzt gibt es eine skalierbare Infrastruktur, die eine gestufte Architektur mit mindestens sechs Knoten bietet: drei Knoten für die Hauptdatenbank und die Dienste und drei Knoten für den Webserver. Diese Aufspaltungsarchitektur bietet die Möglichkeit, Ebenen unabhängig zu skalieren, um ein optimales Leistungsgleichgewicht zu erzielen.

### Dienststufe

Es gibt drei Dienstknoten für Datenspeicherung, Cache und Dienste: **OpenSearch** oder **Elasticsearch**, **MariaDB**, **Redis** und mehr. Wenn sich die Service-Tier-Kapazität nähert, besteht die einzige Möglichkeit zum Skalieren darin, die Server-Größe zu erhöhen, z. B. die CPU-Leistung und den Speicher zu erhöhen. Die Kapazität ist auf die Größe des verfügbaren Knotens beschränkt. Da der Datenbankcluster für eine hohe Verfügbarkeit ausgelegt ist, ist es mit den verwendeten Technologien nicht möglich, die horizontale Skalierung zuverlässig durchzuführen.

![Dienstebenenskalierung](../../assets/scaling-service.png)

Betrachten Sie ein Beispiel dafür, dass der Instanztyp des Dienstknotens _m5.2xlarge_ mit 32 GB RAM ist. Ein Dienst, wie die Datenbank, nutzt einen beträchtlichen Speicher (30 GB). Die Skalierung auf die nächste verfügbare Instanzgröße _m5.4xlarge_ bietet 64-Gbit-RAM, wodurch der Speicher verdoppelt wird und die wachsenden Anforderungen der Datenbank erfüllt werden.

Sie können die Leistung der Dienstebene weiter optimieren, indem Sie den Traffic basierend auf dem Knotentyp weiterleiten. Standardmäßig wird der Datenbankknoten vom Webtraffic isoliert. Beispielsweise können Sie Webtraffic auf dem Datenbankknoten bereitstellen.

### Webstufe

Es gibt drei Webknoten für die Verarbeitung von Anforderungen und Webtraffic: **php-fpm** und **NGINX**. Zusätzlich zur vertikalen Skalierung durch Erhöhung von Strom und Speicher kann die Webstufe horizontal skaliert werden, indem Webserver zu einem vorhandenen Cluster hinzugefügt werden, wenn sie auf PHP-Ebene eingeschränkt sind. Unter [Automatische Skalierung](autoscaling.md) erfahren Sie, wie die Webknoten automatisch skaliert werden.

![Skalierung auf Webebene](../../assets/scaling-web.png)

Dies ergänzt die vertikale Skalierung, die von der Dienststufe bereitgestellt wird. Da die Größe und Leistung der Dienststufe skaliert werden, um eine wachsende Datenbank- und Dienstnutzung zu ermöglichen, skaliert die Webstufe Größe, Leistung und Instanzen, um eine Zunahme der Prozessanforderungen und höhere Traffic-Anforderungen zu berücksichtigen.

Betrachten Sie ein Beispiel dafür, dass der Instanztyp des Webknotens _C5.2xlarge mit acht CPUs und 16-Gbit RAM_ ist. Die Anzahl der Anfragen an die Site nahm stark zu. Sie können einen C5.2xlarge-Knoten hinzufügen, um die Zunahme an php-fpm-Prozessen zu verarbeiten, oder Sie können jeden Instanztyp mit 16 CPU und 32 Gb RAM _in_ C5.4xlarge ändern. Das Hinzufügen eines Knotens verringert das Risiko einer unzureichenden Überlagerungskapazität.

## Projektstruktur

Minimalerweise stehen für Pro-Projekte mit der skalierten Architektur sechs Knoten zur Verfügung.

- 3 Webknoten c5.2xlarge (8 CPU, 16 GB RAM)

- 3 Dienstknoten m5.2xlarge (8 CPU, 32 GB RAM)

Jedes Projekt ist jedoch einzigartig und erfordert eine Leistungsüberwachung, um die Ressourcenverwaltung ordnungsgemäß zu analysieren. Jedes Konto enthält den [New Relic-Dienst](../monitor/new-relic-service.md), der automatisch eine Verbindung zu den Anwendungsdaten und Leistungsanalysen herstellt, um eine dynamische Serverüberwachung zu ermöglichen. Insbesondere können Sie den New Relic-Dienst verwenden, um die CPU- und RAM-Auslastung zu überwachen und zu bestimmen, welche Knoten zusätzliche Ressourcen benötigen. Wenn eine Ressource die Kapazität erreicht oder Sie eine Leistungsbeeinträchtigung auf der Grundlage der Analyse feststellen, können Sie eine Anforderung erstellen, um Ihre Infrastruktur entsprechend der Nachfrage zu skalieren.

### SSH-Zugriff

Bestimmte Dateien und Protokolle, z. B. das Verzeichnis `/app/<project-id>/var/log`, werden nicht von Knoten gemeinsam genutzt. Jeder Knoten hat einen eindeutigen SSH-Zugriff. Sie können die CLI `magento-cloud` nicht verwenden, um sich beim Dienst oder bei den Webknoten anzumelden, aber Sie können die Knotenadressen in der Liste SSH-Zugriff in Ihrem [!DNL Cloud Console] finden.

```bash
ssh <node>.<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
```

- `node` 1 bis 3—Adressen für den Zugriff auf Dienstknoten

- `node` 4 bis _n_—Adressen für den Zugriff auf die Webknoten

>[!TIP]
>
>Nach der Anmeldung können Sie die Server-ID und die Rolle bestätigen: Dienstknoten verwenden die Rolle _unified_ und Webknoten verwenden die Rolle _web_ .

Die Beispielantwort bei der Anmeldung bei einem **Dienstknoten** enthält die Rolle _unified_ :

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:unified.

project-id@server-id:~$
```

Die Beispielantwort bei der Anmeldung bei einem **Webknoten** enthält die Rolle _web_ :

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:web.

project-id@server-id:~$
```

### Protokollspeicherorte

Die Protokollspeicherorte variieren je nach Knoten geringfügig. Beispielsweise ist ein Datenbankprotokoll, wie das **MySQL-Fehlerprotokoll**, auf einem Dienstknoten (`/var/log/mysql/mysql-error.log`) verfügbar, aber nicht auf einem Webknoten.

Jedes Pro-Konto beinhaltet den [New Relic Logs-Dienst](../monitor/new-relic-service.md), der automatisch eine Verbindung zu Protokolldaten aus der Anwendung herstellt, um eine dynamische Protokollverwaltung zu ermöglichen. Aggregierte Protokolldaten von allen Knoten werden in der New Relic Logs-Anwendung angezeigt, damit Sie Leistungsprobleme auf bestimmten Knoten in einem Dashboard beheben können.
