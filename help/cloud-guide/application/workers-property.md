---
title: Arbeitnehmer
description: Erfahren Sie, wie Sie die Eigenschaft "Sekundäre"in der Konfigurationsdatei der [!DNL Commerce] Anwendung konfigurieren.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Eigenschaft &quot;Workers&quot;

Sie können einen Worker definieren, der unabhängig von der Webinstanz ohne laufende Nginx-Instanz ausgeführt werden soll. Der Worker verwendet jedoch denselben Netzwerkspeicher, der von der [!DNL Commerce] -Anwendung verwendet wird. Sie müssen keinen Webserver auf der Worker-Instanz einrichten (unter Verwendung von Node.js oder Go), da der Router keine öffentlichen Anfragen an den Worker richten kann. Dadurch ist die Worker-Instanz ideal für Hintergrundaufgaben oder fortlaufend ausgeführte Aufgaben, die das Risiko bergen, eine Bereitstellung zu blockieren.

## Konfigurieren eines Sekundärs

Arbeitnehmer können nur mit Pro Staging- und Produktionsumgebungen verwendet werden. Pro-Integration- und Starterumgebungen können die Variable [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) verwenden.

Um einen Worker in Pro Staging oder Produktion zu konfigurieren, senden Sie ein Adobe Commerce-Support-Ticket ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) und fügen Sie die folgenden Informationen hinzu:[

- Projekt-ID
- Umgebungs-ID
- Worker name
- Startbefehle

Sie können einen Prozess pro Worker konfigurieren. Eine einfache, allgemeine Worker-Konfiguration in der Datei `.magento.app.yaml` könnte wie folgt aussehen:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

In diesem Beispiel wird ein einzelner Worker mit dem Namen `queue` mit einer kleinen Ressourcenzuordnung (Größe S) definiert und der Befehl `php ./bin/magento` wird beim Start ausgeführt. Der Worker `queue` wird dann auf jedem Knoten als Worker-Prozess ausgeführt. Wenn der Befehl beendet wird, wird er automatisch neu gestartet.

## Befehle und Überschreibungen

Der Schlüssel `commands.start` ist erforderlich, um Befehle mit der Worker-Anwendung zu starten. Sie können jeden gültigen Shell-Befehl verwenden, obwohl es ideal ist, die Sprache Ihrer Anwendung zu verwenden. Wenn der durch den Schlüssel `start` angegebene Befehl beendet wird, wird er automatisch neu gestartet.

>[!IMPORTANT]
>
>Die Befehle `deploy` und `post_deploy` Hooks und `crons` werden nur im Webcontainer ausgeführt, nicht in Worker-Instanzen.

### Vererbung

Definitionen für die Eigenschaften `size`, `relationships`, `access`, `disk` und `mount` sowie `variables` werden von einem Worker übernommen, sofern dies nicht explizit überschrieben wird.

Die folgenden Eigenschaften werden am häufigsten verwendet, um [Einstellungen der obersten Ebene](properties.md) zu überschreiben:

- `size` - Zuordnung von weniger Ressourcen zu einem einzelnen Hintergrundprozess
- `variables` - Weisen Sie die Anwendung an, anders zu laufen

### Zeit und Warteschlange

Obwohl jeder Worker hinter einem anderen steht, erzeugt die folgende Konfiguration eine konsistente Zwei-Sekunden-Trennung der Zeitstempel in der Datei `var/time.txt`, unabhängig vom acht Sekunden langen Schlaf im PHP-Code:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
