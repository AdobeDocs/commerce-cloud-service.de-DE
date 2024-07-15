---
title: Benachrichtigungen einrichten
description: Erfahren Sie, wie Sie Benachrichtigungen für Adobe Commerce in Cloud-Infrastrukturumgebungen konfigurieren.
feature: Cloud, Configuration, Logs
exl-id: be48abcd-4753-4e89-83fe-0aadfb0415c2
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Benachrichtigungen einrichten

Standardmäßig schreibt Adobe Commerce in der Cloud-Infrastruktur Build- und Bereitstellungsaktionen in die Datei &quot;`app/var/log/cloud.log`&quot;im Stammordner der Adobe Commerce-Anwendung. Optional können Sie Protokolle an ein Messaging-System wie Slack und E-Mail senden, um Echtzeit-Benachrichtigungen zu erhalten.

Beispielsweise können Sie eine Slack-Nachricht senden, um eine Benutzergruppe bei einem fehlgeschlagenen Bereitstellungsprozess zu benachrichtigen und eine Untersuchung darüber einzuleiten, was schiefgelaufen ist.

## Planen von Benachrichtigungen

Beachten Sie vor der Konfiguration von Benachrichtigungen Folgendes:

- Welche Art von Benachrichtigungen möchten Sie erhalten (Slack-Nachrichten, E-Mails, beides)?
- Wie viele Details möchten Sie in den Protokollen sehen?
- Wo möchten Sie Benachrichtigungen einrichten (Integration, Staging, Produktion)?

Beispielsweise können Sie während der ersten Entwicklung E-Mail-Benachrichtigungen mit detaillierten Protokollen zu Ihrer Integrationsumgebung bevorzugen, um Probleme zu beheben, bevor Sie sie in der Staging-Umgebung bereitstellen. Wenn Sie für die Bereitstellung in der Staging- oder Produktionsumgebung bereit sind, sollten Sie eine Slack-Nachricht mit weniger detaillierten Informationen bevorzugen.

>[!NOTE]
>
>Die Konfigurationsdatei, die zum Einrichten von Benachrichtigungen verwendet wird, befindet sich im Stammverzeichnis Ihres Projektverzeichnisses. Sie gilt also, wenn Sie Änderungen an eine Umgebung pushen. Wenn Sie Benachrichtigungen pro Umgebung anpassen möchten, müssen Sie die Konfigurationsdatei ändern, bevor Sie sie an diese Umgebung senden.

## Benachrichtigungen konfigurieren

So konfigurieren Sie Benachrichtigungen:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.
1. Fügen Sie in der Datei &quot;`.magento.env.yaml`&quot;im Projektstamm Ihre Einstellungen für das Messaging-System hinzu, einschließlich der bevorzugten Benachrichtigungsebene [Protokollebenen](log-handlers.md#log-levels).

   Um beispielsweise die E-Mail-Konfigurationen für Slack _und_ zu konfigurieren, verwenden Sie Folgendes:

   ```yaml
   log:
     slack:
       token: "<your-slack-token>"
       channel: "<your-slack-channel>"
       username: "SlackHandler"
       min_level: "info"
     email:
       to: <your-email>
       from: <your-email>
       subject: "Log notification from Adobe Commerce"
       min_level: "notice"
   ```

   >[!NOTE]
   >
   >Adobe Commerce in der Cloud-Infrastruktur sendet nur E-Mails während der Bereitstellungsphase.

1. Übertragen Sie Ihre Änderungen auf den Remote-Server.

   ```bash
   git -A && git commit -m "Configure build/deploy notifications"
   ```

   ```bash
   git push origin <branch-name>
   ```

### Slack-Beispielkonfiguration

Das folgende Beispiel zeigt eine Nur-Slack-Konfiguration:

```yaml
log:
  slack:
    token: "<your-slack-token>"
    channel: "<your-slack-channel>"
    username: "SlackHandler"
    min_level: "info"
```

- `token` - Ihr Slack [Benutzer-Token](https://api.slack.com/docs/token-types#user). Ihr Benutzer-Token autorisiert Adobe Commerce in der Cloud-Infrastruktur zum Senden von Nachrichten.
- `channel` - Der Name des Slack-Kanals Adobe Commerce in der Cloud-Infrastruktur sendet Benachrichtigungen.
- `username`—Benutzername Adobe Commerce in der Cloud-Infrastruktur verwendet , um Benachrichtigungen in Slack zu senden.
- `min_level`—Minimale Protokollebene für Benachrichtigungsmeldungen. Es wird empfohlen, `info` zu verwenden.

### Beispiel für eine E-Mail-Konfiguration

Das folgende Beispiel zeigt eine E-Mail-Konfiguration:

>[!NOTE]
>
>Adobe Commerce in der Cloud-Infrastruktur sendet nur E-Mails während der Bereitstellungsphase.

```yaml
log:
  email:
    to: <your-email>
    from: <your-email>
    subject: "Log notification from Adobe Commerce"
    min_level: "notice"
```

- `to` - E-Mail-Adresse Adobe Commerce in der Cloud-Infrastruktur sendet Benachrichtigungen.
- `from` - E-Mail-Adresse zum Senden von Benachrichtigungsinhalten an Empfänger.
- `subject`—Beschreibung der E-Mail.
- `min_level`—Minimale Protokollebene für Benachrichtigungsmeldungen. Es wird empfohlen, `notice` oder `warning` zu verwenden.
