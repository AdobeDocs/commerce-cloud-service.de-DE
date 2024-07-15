---
title: Protokollhandler
description: Erfahren Sie, wie Sie Protokollhandler für Adobe Commerce in der Cloud-Infrastruktur konfigurieren.
feature: Cloud, Logs, Configuration
role: Developer
exl-id: d3be7b6d-5778-4c32-865b-31bdb2852a23
source-git-commit: f8e35ecff4bcafda874a87642348e2d2bff5247b
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Protokollhandler

Sie können Log-Handler konfigurieren, um Nachrichten an einen Remote-Protokollierungsserver zu senden. Ein Protokollhandler überträgt Build- und Bereitstellungsprotokolle auf andere Systeme, ähnlich wie Sie Protokolle per Push an Slack und E-Mail senden. Sie können einen _syslog_ -Handler aktivieren, der sich ideal für die Protokollierung von Meldungen im Zusammenhang mit Hardware eignet, oder einen Graulog Extended Log Format (GELF)-Handler, der sich ideal für die Protokollierung von Nachrichten aus Softwareanwendungen eignet.

Im folgenden Beispiel werden diese beiden Handler konfiguriert, indem die Konfiguration zur Datei `.magento.env.yaml` hinzugefügt wird. Informationen zu den Mindestwerten für die Protokollierungsstufe (`min_level`) finden Sie unter [Protokollebenen](#log-levels).

```yaml
log:
  syslog:
    ident: "<syslog-ident>"
    facility: 8 # https://php.net/manual/en/network.constants.php
    min_level: "info"
    logopts: <syslog-logopts>

  syslog_udp:
    host: "<syslog-host>"
    port: <syslog-port>
    facility: 8  # https://php.net/manual/en/network.constants.php
    ident: "<syslog-ident>"
    min_level: "info"

  gelf:
    min_level: "info"
    use_default_formatter: true
    additional: # Some additional information for each log message
      project: "<some-project-id>"
      app_id: "<some-app-id>"
    transport:
      http:
        host: "<http-host>"
        port: <http-port>
        path: "<http-path>"
        connection_timeout: 60
      tcp:
        host: "<tcp-host>"
        port: <tcp-port>
        connection_timeout: 60
      udp:
        host: "<udp-host>"
        port: <udp-port>
        chunk_size: 1024
```

## Protokollebenen

Die Protokollebenen bestimmen die Detaillierungsstufe in den Benachrichtigungsmeldungen. Die folgenden Kategorien auf Protokollebene enthalten jede Protokollebene darunter. Beispielsweise beinhaltet eine `debug` -Ebene die Protokollierung von jeder Ebene, während eine `alert` -Ebene nur Warnhinweise und Notfälle anzeigt.

- **debug** - detaillierte Debugging-Informationen
- **info** - interessante Ereignisse, wie z. B. eine Benutzeranmeldung oder ein SQL-Protokoll
- **Hinweis** - normale, aber wichtige Ereignisse
- **warning**—außergewöhnliche Ereignisse, die keine Fehler sind, wie die Verwendung einer veralteten API oder die schlechte Verwendung einer API
- **error**—Laufzeitfehler, die keine sofortige Aktion erfordern
- **critical** - kritische Bedingungen, z. B. eine nicht verfügbare Anwendungskomponente oder eine unerwartete Ausnahme
- **alert** - sofortiges Handeln erforderlich, z. B. wenn eine Website ausfällt oder die Datenbank nicht verfügbar ist, sodass der Trigger einen SMS-Warnhinweis erhält
- **alert** - System ist nicht verwendbar
