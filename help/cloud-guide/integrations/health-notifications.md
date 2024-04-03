---
title: Statusbenachrichtigungen
description: Erfahren Sie, wie Sie Slack-, E-Mail- und PagerDuty-Benachrichtigungen für die Speichernutzung in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt konfigurieren.
feature: Cloud, Observability, Integration
exl-id: d3173098-78ed-42a8-aeb3-9ccbaccc4d32
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Statusbenachrichtigungen

Adobe Commerce in der Cloud-Infrastruktur überwacht die Speichernutzung in allen Anwendungen und Diensten in Ihrer Starter-Umgebung oder Ihrer Pro-Integrationsumgebung. Eine Datenbankdiskette, auf der nicht genügend Speicherplatz zur Verfügung steht, kann zu Datenbeschädigungen führen. Die Statusprüfung erfolgt alle 5 Minuten und kann Sie per E-Mail oder über einen anderen externen Dienst benachrichtigen. Für Statusbenachrichtigungen gibt es drei Warnungen mit geringer Festplatte:

- **Warnung**—verfügbarer Speicherplatz sinkt unter 20 %
- **Kritisch**—verfügbarer Speicherplatz sinkt unter 10 %
- **Alles klar**—verfügbarer Speicherplatz gibt nach einem Ereignis mit geringer Festplatte mehr als 20 % zurück

>[!NOTE]
>
>In Pro-Produktionsumgebungen können Sie die Warnhinweisrichtlinie für verwaltete Warnhinweise für Adobe Commerce für New Relic verwenden, um Speicherplatz zu überwachen. Siehe [Überwachen der Leistung mit verwalteten Warnhinweisen](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

## E-Mail-Benachrichtigungen

Für die E-Mail-Integration im Gesundheitssektor sind eine Ursprungsadresse und mindestens eine Empfängeradresse erforderlich. Sie können dieselbe E-Mail-Adresse für die `from-address` und `recipients` Adresse. Im folgenden Beispiel wird eine E-Mail-Integration für den Gesundheitszustand mit zwei Empfängern registriert:

```bash
magento-cloud integration:add --type health.email --from-address you@example.com --recipients them@example.com --recipients others@example.com
```

## Slack-Kanalbenachrichtigungen

Slack ist ein externer Dienst, der interaktive Apps namens Bots verwendet, um Nachrichten in einem Chat-Raum zu posten. Bevor Sie Statusbenachrichtigungen in Slack empfangen können, müssen Sie eine benutzerdefinierte [Bot-Benutzer](https://api.slack.com/bot-users) für Ihre Slack-Gruppe. Nachdem Sie den Bot-Benutzer für Ihren Kanal oder die Kanäle konfiguriert haben, speichern Sie die [Bot-Token](https://api.slack.com/docs/token-types#bot) von Slack bereitgestellt werden, um Ihre Integration zu registrieren. Im folgenden Beispiel werden Statusbenachrichtigungen in einem Slack-Kanal registriert:

```bash
magento-cloud integration:add --type health.slack --token SLACK_BOT_TOKEN --channel '#slack-channel-name'
```

## PagerDuty-Benachrichtigungen

PagerDuty ist ein externer Dienst, der Mitglieder des On-Call-Teams über wichtige Probleme informieren kann. Bevor Sie Gesundheitsbenachrichtigungen in PagerDuty erhalten können, müssen Sie eine [PagerDuty-Integration](https://developer.pagerduty.com/v2/docs/integrating) , die die Events API Version 2 verwendet. Verwenden Sie den Integrationsschlüssel oder _Routing-Schlüssel_, um Ihre Integration zu registrieren. Im folgenden Beispiel werden Benachrichtigungen für PagerDuty mithilfe eines Routing-Schlüssels registriert:

```bash
magento-cloud integration:add --type health.pagerduty --routing-key PAGERDUTY_ROUTING_KEY
```
