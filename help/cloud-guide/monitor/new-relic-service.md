---
title: New Relic-Dienst
description: Erfahren Sie mehr über den New Relic-Dienst, der mit Ihrem Adobe Commerce-Projekt zur Cloud-Infrastruktur verfügbar ist.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Übersicht über den New Relic-Dienst

Alle Adobe Commerce-Projekte in der Cloud-Infrastruktur umfassen den Zugriff auf den New Relic-Dienst, um die Leistung zu überwachen und Ereignisse der [!DNL Commerce] -Anwendung und Cloud-Infrastruktur zu untersuchen.

Die folgenden New Relic-Funktionen stehen für die Verwendung in Produktions- und Staging-Umgebungen zur Verfügung:

- [New Relic APM](#new-relic-apm) (Pro und Starter)
- [New Relic Infrastructure](#new-relic-infrastructure) (nur Pro)
- [New Relic-Protokollverwaltung](#new-relic-logs) (nur Pro)

>[!INFO]
>
>Andere New Relic-Funktionen sind nicht für Adobe Commerce-Projekte verfügbar.

## NEW RELIC APM

[New Relic for Application Performance Management (APM)](https://docs.newrelic.com/introduction-apm/) ist ein Softwareanalyseprodukt, mit dem Sie Anwendungsinteraktionen analysieren und verbessern können. Das New Relic-APM ist für alle Adobe Commerce-Projekte in Cloud-Infrastruktur verfügbar und bietet die folgenden Funktionen:

- **Konzentrieren Sie sich auf bestimmte Transaktionen** - Markieren und überwachen Sie aktiv wichtige Kundenaktionen auf Ihrer Site, z. B. das Hinzufügen zum Warenkorb, das Auschecken oder die Verarbeitung einer Zahlung.
- **Überwachung der Datenbankabfrage** - Suchen und überwachen Sie Datenbankabfragen, die sich auf die Leistung auswirken.
- **App-Zuordnung**: Zeigen Sie alle Anwendungsabhängigkeiten innerhalb Ihrer Site, Erweiterungen und externen Dienste an.
- **[!DNL Apdex]Bewertungen** - Evaluieren Sie die Leistung und erstellen Sie Warnhinweise, die Probleme identifizieren und Sie benachrichtigen, wenn sie auftreten, z. B. die Site-Leistung, die von einem Flash-Verkauf oder einem Web-Ereignis betroffen ist. Siehe [Apdex-Wert](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Verwaltete Warnhinweise für Adobe Commerce** - Verwenden Sie diese New Relic-Warnhinweisrichtlinie, um die Anwendungs- und Infrastrukturleistung anhand der Best Practices der Branche zu überwachen. Siehe [Überwachen der Leistung mit der Warnhinweisrichtlinie für verwaltete Warnhinweise für Adobe Commerce](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **Implementierungen verfolgen** - Überwachen Sie Bereitstellungsereignisse und analysieren Sie die Auswirkungen der Bereitstellung auf die Gesamtleistung. Siehe [Implementierungen verfolgen](track-deployments.md).

Ihr Adobe Commerce on Cloud-Infrastrukturprojekt umfasst die Software für den New Relic-APM-Dienst sowie einen Lizenzschlüssel. Sie müssen keine zusätzliche Software erwerben oder installieren.

## New Relic-Infrastruktur

Zu den Pro-Projekten gehört der Dienst [New Relic Infrastructure (NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/) , der automatisch eine Verbindung zu den Anwendungsdaten und Leistungsanalysen herstellt, um eine dynamische Serverüberwachung zu ermöglichen. Dieser Dienst ist in Pro Production- und Staging-Umgebungen verfügbar.

## New Relic-Protokollverwaltung

Alle Cloud-Infrastrukturprojekte umfassen [New Relic-Protokollverwaltung](log-management.md). Der Dienst ist vorkonfiguriert, um alle Protokolldaten aus Ihren Staging- und Produktionsumgebungen zu aggregieren und in einem zentralen Protokollverwaltungs-Dashboard anzuzeigen.
