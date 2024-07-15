---
title: Best Practices für die Aktualisierung Ihres Projekts
description: Sehen Sie sich eine Liste mit Best Practices für das Upgrade Ihrer Projektdateien an.
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Best Practices für die Aktualisierung Ihres Projekts

Befolgen Sie die Best Practices für Builds und Bereitstellungen und verwenden Sie den Workflow [Upgrades und Patches](../development/commerce-version.md) , um Ihre Anwendung zu aktualisieren. Verwenden Sie die folgenden Richtlinien, um Ihre Upgrade- und Nachbearbeitungstätigkeiten zu planen:

- **Sichern Sie Ihr Projekt** - Sichern Sie vor dem Aktualisieren von Adobe Commerce und beliebigen Drittanbieter- oder benutzerdefinierten Erweiterungen die Datenbank in den Umgebungen für Integration, Staging und Produktion. Siehe [Sichern der Datenbank](../development/commerce-version.md#project-backup).

- **Prüfen auf Kompatibilitätsprobleme**-

   - Stellen Sie sicher, dass alle benutzerdefinierten Designs mit der neuen Adobe Commerce-Version kompatibel sind

   - Verwenden Sie nach der Aktualisierung von Drittanbieter- und benutzerdefinierten Erweiterungen den Befehl `magento-cloud local:build` , um die Composer-Abhängigkeiten vor der Bereitstellung zu überprüfen.

   - Lesen Sie die Adobe Commerce-Versionshinweise und die Dokumentation zu Erweiterungen , um sicherzustellen, dass Sie alle erforderlichen Umgehungen oder Konfigurationsänderungen implementiert haben, um bekannte Funktionsprobleme und Fehler im Zusammenhang mit der Aktualisierung der Adobe Commerce-Version und -Erweiterungen zu beheben.

   - Stellen Sie sicher, dass die installierten Dienstversionen mit der neuen Adobe Commerce-Version kompatibel sind, und aktualisieren Sie die Dienste nach Bedarf. Siehe [Dienste](../services/services-yaml.md).

   - Testen Sie Ihre Datenbank, um alle Probleme zu beheben, die durch Aktualisierungen der Adobe Commerce-Version und -Erweiterungen verursacht wurden.

   - Nehmen Sie alle erforderlichen Aktualisierungen an umgebungsspezifischen Einstellungen vor, bevor Sie sie in der Remote-Umgebung bereitstellen.

   - Stellen Sie sicher, dass die Version des Suchdienstes mit der PHP-Clientversion kompatibel ist. Siehe [Einrichten von Elasticsearch](../services/elasticsearch.md) oder [Einrichten von OpenSearch](../services/opensearch.md).

- **Überprüfen Sie die Datenbankverbindung und den verfügbaren Speicher in Remote-Umgebungen**-

   - Verwenden Sie SSH, um sich beim Remote-Server anzumelden und die Verbindung zur MySQL-Datenbank zu überprüfen. Siehe [Verbindung zur Datenbank herstellen](../services/mysql.md#connect-to-the-database).

   - Überprüfen Sie den verfügbaren Speicher in der Remote-Umgebung. Verwenden Sie den Befehl `disk free` , um den verfügbaren Speicherplatz in Ihren Cloud-Umgebungen anzuzeigen und zu verwalten. Siehe [Verwalten des Festplattenspeichers](../storage/manage-disk-space.md).

      - Überprüfen Sie die Größe der aktualisierten Datenbank und stellen Sie sicher, dass der Datei `services.yaml` genügend Speicherplatz zugewiesen ist.

      - Freigeben des Festplattenspeichers - Leeren Sie den Cache und bereinigen Sie die Verzeichnisse `/log` und `/tmp` vor der Bereitstellung.

- **Planen und führen Sie eine erfolgreiche Aktualisierung in lokalen Umgebungen und Integrationsumgebungen durch, bevor Sie auf Staging bereitstellen** - Testen Sie Ihre Bereitstellung und lösen Sie alle Probleme.

- **Führen Sie Code zum Staging zusammen, dann zum Produktions-**-Test und lösen Sie alle Probleme in der Staging-Umgebung, bevor Sie Änderungen in die Produktionsumgebung übertragen.

- **Führen Sie die Post-Aktualisierungsaufgaben durch**-

   - Verwenden Sie SSH, um sich beim Remote-Server anzumelden und Folgendes zu überprüfen:

      - Überprüfen Sie den Indexstatus und führen Sie bei Bedarf eine Neuindizierung durch. Siehe [Verwalten der Indexer](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) im _Konfigurationshandbuch_.

      - Überprüfen Sie die Protokolle `cron` und die Tabelle `cron_schedule` in der Adobe Commerce-Datenbank, um den Cron-Status zu überprüfen, und führen Sie die Cron-Aufträge nach Bedarf erneut aus.
Siehe [Protokollierung](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) im _Konfigurationshandbuch_.

   - Schließen Sie die UAT zum Testen der Benutzerakzeptanz nach der Aktualisierung in Staging- und Produktionsumgebungen ab und beheben Sie alle Probleme im Zusammenhang mit Upgrades von Drittanbietern und benutzerdefinierten Erweiterungen.
