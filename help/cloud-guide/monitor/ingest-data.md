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

New Relic bietet eine Ansicht mit dem _Datenmanagement_, in der die Nutzung Ihres Plans nach Datenquelle zusammengefasst wird.

**So zeigen Sie Ihre Erfassungsdaten und -quellen an**:

1. Klicken Sie im New Relic-Benutzermenü auf **[!UICONTROL Manage your data]**.
1. Klicken Sie in der Liste _Administration_ auf **[!UICONTROL Data management]**.

   ![Datenverwaltung](../../assets/new-relic/data-ingestion.png)

   Auf der Registerkarte **[!UICONTROL Data ingestion]** werden die für den Tag erfassten Daten sowie die Quelle der Daten angezeigt.
Im Tab Datenbeibehaltung wird angezeigt, wie lange Daten gespeichert werden.

1. Wählen Sie den Tab **[!UICONTROL Limits]** aus und sehen Sie die Beschränkungen für Ihr Konto.

Zu den Datenquellen für Adobe Commerce gehören:

- **APM-Ereignisse** - Ereignisdaten, die in Diagrammen und Dashboards verwendet werden
- **Infrastruktur** - Verarbeiten und Hosten von Metriken wie CPU, Speicher, Netzwerk
- **Protokollierung** - Protokolle für CDN, APM und Anwendungsserver

Protokolldaten tragen zu einem großen Teil der Erfassung bei. Erfahren Sie, wie Sie [Protokolldaten anzeigen und analysieren](log-management.md#view-and-analyze-log-data) und gemeinsam mit Ihrem Adobe-Support-Mitarbeiter eine Strategie für die Datenerfassung und -aufbewahrung entwickeln können. Weitere Informationen über die [Verwaltung der Datenerfassung](https://docs.newrelic.com/docs/data-apis/manage-data/manage-data-coming-new-relic/) finden Sie in der _New Relic-Dokumentation_.
