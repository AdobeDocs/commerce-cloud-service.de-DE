---
title: Einrichten des RabbitMQ-Dienstes
description: Erfahren Sie, wie Sie den RabbitMQ-Dienst aktivieren, um Nachrichtenwarteschlangen für Adobe Commerce in der Cloud-Infrastruktur zu verwalten.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: adcfbb7217c70122a4003a66d1bec1a623fbf11a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Einrichten [!DNL RabbitMQ] service

Die [Message Queue Framework (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) ist ein System in Adobe Commerce, das Folgendes ermöglicht: [Modul](https://glossary.magento.com/module) , um Nachrichten in Warteschlangen zu veröffentlichen. Außerdem werden die Verbraucher definiert, die die Nachrichten asynchron empfangen.

Der MQF verwendet [RabbitMQ](https://www.rabbitmq.com/) als Messaging Broker, der eine skalierbare Plattform für den Versand und Empfang von Nachrichten bietet. Es enthält auch einen Mechanismus zum Speichern nicht zugestellter Nachrichten. [!DNL RabbitMQ] basiert auf der AMQP-Spezifikation 0.9.1 (Advanced Message Queuing Protocol).

>[!WARNING]
>
>Wenn Sie einen vorhandenen AMQP-basierten Dienst bevorzugen, z. B. [!DNL RabbitMQ]Verwenden Sie anstelle von Adobe Commerce für die Cloud-Infrastruktur, um sie für Sie zu erstellen, die [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) Umgebungsvariable, um sie mit Ihrer Site zu verbinden.

{{service-instruction}}

**So aktivieren Sie RabbitMQ**:

1. Fügen Sie den erforderlichen Namen, Typ und Festplattenwert (in MB) zum `.magento/services.yaml` zusammen mit der installierten RabbitMQ-Version.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Konfigurieren Sie die Beziehungen im `.magento.app.yaml` -Datei.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Überprüfen der Dienstbeziehungen](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verbindung zu RabbitMQ zum Debugging herstellen

Für Debugging-Zwecke ist es nützlich, eine direkte Verbindung zu einer Dienstinstanz auf eine der folgenden Arten herzustellen:

- Verbindung zur lokalen Entwicklungsumgebung herstellen
- Verbindung mit der Anwendung herstellen
- Verbinden über eine PHP-Anwendung

### Verbindung zur lokalen Entwicklungsumgebung herstellen

1. Melden Sie sich bei `magento-cloud` CLI und Projekt:

   ```bash
   magento-cloud login
   ```

1. Sehen Sie sich die Umgebung an, in der RabbitMQ installiert und konfiguriert ist.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Verwenden Sie SSH, um eine Verbindung zur Cloud-Umgebung herzustellen:

   ```bash
   magento-cloud ssh
   ```

1. Rufen Sie die RabbitMQ-Verbindungsdetails und Anmeldedaten aus dem [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) Variable:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   oder

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Suchen Sie in der Antwort die RabbitMQ-Informationen, beispielsweise:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Aktivieren Sie die lokale Port-Weiterleitung an RabbitMQ (wenn sich Ihr Projekt in einer anderen Region wie der USA-3, der EU-5 oder der AP-3-Region befindet), ersetzen Sie ``us-3``/``eu-5``/``ap-3`` für ``us``)

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Ein Beispiel für den Zugriff auf die RabbitMQ Management-Webschnittstelle unter `http://localhost:15672` ist:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Während die Sitzung geöffnet ist, können Sie von Ihrer lokalen Workstation aus einen RabbitMQ-Client Ihrer Wahl starten, der für die Verbindung mit dem `localhost:<portnumber>` unter Verwendung der Portnummer, des Benutzernamens und Kennwortinformationen aus der Variablen MAGENTO_CLOUD_RELATIONSHIPS .

### Verbindung mit der Anwendung herstellen

Um eine Verbindung zu RabbitMQ herzustellen, die in einer Anwendung ausgeführt wird, installieren Sie einen Client, z. B. [amqp-utils](https://github.com/dougbarth/amqp-utils)als Projektabhängigkeit in Ihrer `.magento.app.yaml` -Datei.

Beispiel:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Wenn Sie sich in Ihrem PHP-Container anmelden, geben Sie `amqp-` zur Verwaltung Ihrer Warteschlangen verfügbar.

### Verbinden über eine PHP-Anwendung

Um mit Ihrer PHP-Anwendung eine Verbindung zu RabbitMQ herzustellen, fügen Sie ein PHP hinzu [Bibliothek](https://glossary.magento.com/library) in Ihren Quellbaum.
