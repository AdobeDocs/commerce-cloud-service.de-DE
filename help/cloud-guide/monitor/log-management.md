---
title: Protokollverwaltung von New Relic
description: Erfahren Sie, wie Sie das New Relic-Protokoll verwenden
feature: Cloud, Logs, Observability
exl-id: d8afb5c0-9727-4123-8944-81cd6ad7cbb7
source-git-commit: ebe1746ee9fd08480da5ad07d7f1f8299ad9af7e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Protokollverwaltung von New Relic

Alle Cloud-Infrastrukturprojekte umfassen [Protokollverwaltung von New Relic](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). Der Dienst ist vorkonfiguriert, um alle Protokolldaten aus Ihren Staging- und Produktionsumgebungen zu aggregieren und in einem zentralen Protokollverwaltungs-Dashboard anzuzeigen.

Die aggregierten Daten enthalten Informationen aus den folgenden Logs:

- Alle `ece-tools` und Anwendungsprotokolle aus `~/var/log` directory
- Protokolle für Cloud-Services aus der `var/log/platform/<project-ID>` directory
- Schnelles CDN und WAF

Wenn Ihr Projekt mit New Relic verbunden ist, können Sie mit dem New Relic Logs-Dienst Aufgaben wie die folgenden ausführen:

- New Relic-Abfragen zum Durchsuchen aggregierter Protokolldaten verwenden
- Protokolldaten über die New Relic Logs-Anwendung visualisieren
- Benutzerdefinierte Diagramme, Dashboards und Warnhinweise erstellen
- Beheben von Leistungsproblemen in einem einzelnen Dashboard

## Protokolldaten anzeigen und analysieren

Verwenden Sie die New Relic Logs-Anwendung, um über die aggregierten Protokolldaten zu suchen und Fehler in Anwendungen, Infrastruktur, CDN und WAF zu beheben. Sie können Diagramme, Dashboards und Warnhinweise mithilfe von Protokolldaten erstellen, die von New Relic-APM- und Infrastrukturdiensten erfasst wurden.

**So verwenden Sie die New Relic Logs-Anwendung**:

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login).

1. Auswählen **Protokolle** über das Navigationsmenü des Explorers.

1. Stellen Sie sicher, dass Ihr Konto oben im _Alle Protokolle_ anzeigen.

1. Wählen Sie einen Zeitraum für die Logs-Abfrage aus.

1. Überprüfen der Infrastrukturprotokolldaten für Cloud Services (Protokolle von `~/var/log/`), die Abfragezeichenfolge eingeben `has: "filePath"` im _Suche nach Protokollen_ -Feld. Klicken Sie anschließend auf **[!UICONTROL Query logs]**.

   Die Namen der Protokolldateien werden im `filePath` mit vollständigen Pfaden zur Protokolldatei.

   ![Protokolldaten des Cloud Project New Relic-Diensts](../../assets/new-relic/var-log-query.png)

1. Geben Sie die Abfragezeichenfolge ein, um die Fastly-Protokolldaten zu überprüfen `has: "client_ip"` im _Suche nach Protokollen_ -Feld. Klicken Sie anschließend auf **[!UICONTROL Query logs]**.

1. Um die Ergebnisse des Schnellprotokolls nach Ländercode zu filtern, klicken Sie auf **[!UICONTROL Add column]**, wählen Sie **[!UICONTROL geo_country_code]**.

   ![CDN-Attributfilter für Cloud Project New Relic](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>Sie können die Abfrageansicht im _Gespeicherte Ansichten_ Dropdown. Klicks **[!UICONTROL Create new]**, geben Sie einen Namen ein, wählen Sie Optionen aus und klicken Sie auf **[!UICONTROL Save view]**.
>
>Siehe [Erste Schritte mit der Protokollverwaltung](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) und [Einführung in die New Relic-Abfragesprache](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) auf _Dokumente für New Relic_ Site.
