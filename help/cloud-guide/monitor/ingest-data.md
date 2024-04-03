---
title: Datenerfassung
description: Erfahren Sie, wie Sie die Commerce-Datenerfassung in New Relic anzeigen und verwalten.
feature: Cloud, Observability
exl-id: f88bf20c-604b-4986-b71c-bb726b2f00b8
source-git-commit: bf3debc5986d51a721537b52ffced58b2ee521ea
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Datenerfassung

New Relic ist auf umfangreiche Daten angewiesen, um eine effektive Überwachung und Analyse zu ermöglichen. Große Datensätze können jedoch zeitnahe Ergebnisse, Leistung und Compliance beeinträchtigen. Dieses Thema enthält einige Anleitungen zum Verwalten der Datenerfassung und zu Strategien zur Verfeinerung Ihrer Daten, sodass sie am effektivsten sind.

New Relic bietet eine _Data Management_ -Ansicht, die die Nutzung Ihres Plans nach Datenquelle zusammenfasst.

**So zeigen Sie Ihre Erfassungsdaten und Quellen an**:

1. Klicken Sie im New Relic-Benutzermenü auf **[!UICONTROL Manage your data]**.
1. Klicks **[!UICONTROL Data management]** im _Administration_ Liste.

   ![Data Management](../../assets/new-relic/data-ingestion.png)

   Die **[!UICONTROL Data ingestion]** -Tab zeigt Daten an, die für den Tag und die Quelle der Daten erfasst wurden.
Im Tab Datenbeibehaltung wird angezeigt, wie lange Daten gespeichert werden.

1. Wählen Sie die **[!UICONTROL Limits]** und sehen Sie sich die Beschränkungen für Ihr Konto an.

Zu den Datenquellen für Adobe Commerce gehören:

- **APM-Ereignisse**—Ereignisdaten, die in Diagrammen und Dashboards verwendet werden
- **Infrastruktur**—Prozess- und Host-Metriken wie CPU, Speicher, Netzwerk
- **Protokollierung**—logs für CDN, APM und Anwendungsserver

Protokolldaten tragen zu einem großen Teil der Erfassung bei. Informationen [Protokolldaten anzeigen und analysieren](log-management.md#view-and-analyze-log-data) und erarbeiten Sie gemeinsam mit Ihrem Adobe-Support-Mitarbeiter eine Strategie für die Erfassung und Speicherung von Daten. Mehr dazu [Datenaufnahme verwalten](https://docs.newrelic.com/docs/data-apis/manage-data/manage-data-coming-new-relic/) im _New Relic-Dokumentation_.
