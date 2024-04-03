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

Befolgen Sie die Best Practices für Builds und Implementierungen und verwenden Sie die [Upgrades und Patches](../development/commerce-version.md) Workflow zum Aktualisieren Ihrer Anwendung. Verwenden Sie die folgenden Richtlinien, um Ihre Upgrade- und Nachbearbeitungstätigkeiten zu planen:

- **Projekt sichern**-Sichern Sie die Datenbank vor der Aktualisierung von Adobe Commerce und Drittanbieter- oder benutzerdefinierten Erweiterungen in den Umgebungen für Integration, Staging und Produktion. Siehe [Datenbank sichern](../development/commerce-version.md#project-backup).

- **Kompatibilitätsprobleme prüfen**-

   - Stellen Sie sicher, dass alle benutzerdefinierten Designs mit der neuen Adobe Commerce-Version kompatibel sind

   - Verwenden Sie nach der Aktualisierung von Drittanbieter- und benutzerdefinierten Erweiterungen die `magento-cloud local:build` Befehl zum Überprüfen der Composer-Abhängigkeiten vor der Bereitstellung.

   - Lesen Sie die Adobe Commerce-Versionshinweise und die Dokumentation zu Erweiterungen , um sicherzustellen, dass Sie alle erforderlichen Umgehungen oder Konfigurationsänderungen implementiert haben, um bekannte Funktionsprobleme und Fehler im Zusammenhang mit der Aktualisierung der Adobe Commerce-Version und -Erweiterungen zu beheben.

   - Stellen Sie sicher, dass die installierten Dienstversionen mit der neuen Adobe Commerce-Version kompatibel sind, und aktualisieren Sie die Dienste nach Bedarf. Siehe [Dienste](../services/services-yaml.md).

   - Testen Sie Ihre Datenbank, um alle Probleme zu beheben, die durch Aktualisierungen der Adobe Commerce-Version und -Erweiterungen verursacht wurden.

   - Nehmen Sie alle erforderlichen Aktualisierungen an umgebungsspezifischen Einstellungen vor, bevor Sie sie in der Remote-Umgebung bereitstellen.

   - Stellen Sie sicher, dass die Version des Suchdienstes mit der PHP-Clientversion kompatibel ist. Siehe [Elasticsearch einrichten](../services/elasticsearch.md) oder [Einrichten von OpenSearch](../services/opensearch.md).

- **Überprüfen der Datenbankkonnektivität und des verfügbaren Speichers in Remote-Umgebungen**-

   - Verwenden Sie SSH, um sich beim Remote-Server anzumelden und die Verbindung zur MySQL-Datenbank zu überprüfen. Siehe [Verbindung zur Datenbank herstellen](../services/mysql.md#connect-to-the-database).

   - Überprüfen des verfügbaren Speichers in der Remote-Umgebung - Verwenden Sie die `disk free` -Befehl, um den verfügbaren Speicherplatz in Ihren Cloud-Umgebungen anzuzeigen und zu verwalten. Siehe [Verwalten des Festplattenspeichers](../storage/manage-disk-space.md).

      - Überprüfen Sie die Größe der aktualisierten Datenbank und stellen Sie sicher, dass die Variable `services.yaml` -Datei genügend Speicherplatz zugewiesen ist.

      - Freigeben des Festplattenspeichers - Leeren Sie den Cache und reinigen Sie den `/log` und `/tmp` Ordner vor der Bereitstellung.

- **Planen und Ausführen einer erfolgreichen Aktualisierung in lokalen Umgebungen und Integrationsumgebungen vor der Bereitstellung in Staging**- Testen Sie nach dem Upgrade Ihre Bereitstellung und beheben Sie alle Probleme.

- **Zusammenführen von Code zu Staging und dann zur Produktion**-Testen und beheben Sie alle Probleme in der Staging-Umgebung, bevor Sie Änderungen in die Produktionsumgebung übertragen.

- **Aufgaben nach dem Upgrade abschließen**-

   - Verwenden Sie SSH, um sich beim Remote-Server anzumelden und Folgendes zu überprüfen:

      - Überprüfen Sie den Indexstatus und führen Sie bei Bedarf eine Neuindizierung durch. Siehe [Indexer verwalten](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) im _Konfigurationshandbuch_.

      - Überprüfen Sie die `cron` Protokolle und `cron_schedule` in der Adobe Commerce-Datenbank, um den Cron-Status zu überprüfen und Cron-Aufträge nach Bedarf erneut auszuführen.
Siehe [Protokollierung](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) im _Konfigurationshandbuch_.

   - Schließen Sie die UAT zum Testen der Benutzerakzeptanz nach der Aktualisierung in Staging- und Produktionsumgebungen ab und beheben Sie alle Probleme im Zusammenhang mit Upgrades von Drittanbietern und benutzerdefinierten Erweiterungen.
