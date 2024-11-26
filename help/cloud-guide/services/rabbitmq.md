---
title: Einrichten des RabbitMQ-Dienstes
description: Erfahren Sie, wie Sie den RabbitMQ-Dienst aktivieren, um Nachrichtenwarteschlangen für Adobe Commerce in der Cloud-Infrastruktur zu verwalten.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: 269681efb9925d78ffb608ecbef657be740b5531
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Einrichten des [!DNL RabbitMQ]-Dienstes

Das [Message Queue Framework (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) ist ein System in Adobe Commerce, das es einem [Modul](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#module) ermöglicht, Nachrichten in Warteschlangen zu veröffentlichen. Außerdem werden die Verbraucher definiert, die die Nachrichten asynchron empfangen.

Der MQF verwendet [RabbitMQ](https://www.rabbitmq.com/) als Messaging-Broker, der eine skalierbare Plattform zum Senden und Empfangen von Nachrichten bietet. Es enthält auch einen Mechanismus zum Speichern nicht zugestellter Nachrichten. [!DNL RabbitMQ] basiert auf der AMQP-Spezifikation 0.9.1 (Advanced Message Queuing Protocol).

>[!WARNING]
>
>Wenn Sie lieber einen vorhandenen AMQP-basierten Dienst wie [!DNL RabbitMQ] verwenden, anstatt sich bei der Erstellung auf die Cloud-Infrastruktur von Adobe Commerce zu verlassen, verwenden Sie die Umgebungsvariable [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) , um ihn mit Ihrer Site zu verbinden.

{{service-instruction}}

**So aktivieren Sie RabbitMQ**:

1. Fügen Sie den erforderlichen Namen, Typ und Festplattenwert (in MB) zusammen mit der installierten RabbitMQ-Version zur Datei &quot;`.magento/services.yaml`&quot;hinzu.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Konfigurieren Sie die Beziehungen in der Datei &quot;`.magento.app.yaml`&quot;.

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

1. [Überprüfen Sie die Dienstbeziehungen](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verbindung zu RabbitMQ zum Debugging herstellen

Für Debugging-Zwecke ist es nützlich, eine direkte Verbindung zu einer Dienstinstanz auf eine der folgenden Arten herzustellen:

- Verbindung zur lokalen Entwicklungsumgebung herstellen
- Verbindung mit der Anwendung herstellen
- Verbinden über eine PHP-Anwendung

### Verbindung zur lokalen Entwicklungsumgebung herstellen

1. Melden Sie sich bei der CLI und dem Projekt `magento-cloud` an:

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

1. Rufen Sie die RabbitMQ-Verbindungsdetails und Anmeldedaten aus der Variable [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) ab:

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

1. Aktivieren Sie die lokale Anschlussweiterleitung an RabbitMQ (wenn sich Ihr Projekt in einer anderen Region wie US-3, EU-5 oder AP-3 befindet, ersetzen Sie ``us-3``/``eu-5``/``ap-3`` durch ``us``).

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Ein Beispiel für den Zugriff auf die RabbitMQ Management-Webschnittstelle unter `http://localhost:15672`:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Während die Sitzung geöffnet ist, können Sie einen von Ihnen ausgewählten RabbitMQ-Client von Ihrer lokalen Workstation aus starten, der für die Verbindung mit dem `localhost:<portnumber>` konfiguriert ist. Verwenden Sie dazu die Portnummer, den Benutzernamen und die Kennwortinformationen aus der Variablen MAGENTO_CLOUD_RELATIONSHIPS .

### Verbindung mit der Anwendung herstellen

Um eine Verbindung zu RabbitMQ herzustellen, die in einer Anwendung ausgeführt wird, installieren Sie einen Client, z. B. [amqp-utils](https://github.com/dougbarth/amqp-utils), als Projektabhängigkeit in Ihrer `.magento.app.yaml`-Datei.

Beispiel:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Wenn Sie sich bei Ihrem PHP-Container anmelden, geben Sie einen beliebigen `amqp-`-Befehl ein, der zur Verwaltung Ihrer Warteschlangen verfügbar ist.

### Verbinden über eine PHP-Anwendung

Um mit Ihrer PHP-Anwendung eine Verbindung zu RabbitMQ herzustellen, fügen Sie eine PHP-Bibliothek zu Ihrem Quellbaum hinzu.
