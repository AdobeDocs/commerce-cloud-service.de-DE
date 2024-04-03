---
title: Arbeitnehmer
description: Erfahren Sie, wie Sie die Eigenschaft "Sekundäre"im [!DNL Commerce] Anwendungskonfigurationsdatei.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Eigenschaft &quot;Workers&quot;

Sie können einen Worker definieren, der unabhängig von der Webinstanz ohne laufende Nginx-Instanz ausgeführt werden soll. Der Worker verwendet jedoch denselben Netzwerkspeicher, der von der [!DNL Commerce] Anwendung. Sie müssen keinen Webserver auf der Worker-Instanz einrichten (unter Verwendung von Node.js oder Go), da der Router keine öffentlichen Anfragen an den Worker richten kann. Dadurch ist die Worker-Instanz ideal für Hintergrundaufgaben oder fortlaufend ausgeführte Aufgaben, die das Risiko bergen, eine Bereitstellung zu blockieren.

## Konfigurieren eines Sekundärs

Arbeitnehmer können nur mit Pro Staging- und Produktionsumgebungen verwendet werden. Die Pro-Integration- und Starter-Umgebungen können die [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) -Variable.

So konfigurieren Sie einen Worker in der Staging- oder Produktionsumgebung: [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) und fügen Sie die folgenden Informationen hinzu:

- Projekt-ID
- Umgebungs-ID
- Worker name
- Startbefehle

Sie können einen Prozess pro Worker konfigurieren. Eine einfache, gemeinsame Worker-Konfiguration in der `.magento.app.yaml` -Datei könnte wie folgt aussehen:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

In diesem Beispiel wird ein einzelner Worker mit dem Namen `queue`, mit einer kleinen (S) Ebene der Ressourcenzuordnung und führt die `php ./bin/magento` -Befehl beim Start. Der Arbeiter `queue` wird dann auf jedem Knoten als Worker-Prozess ausgeführt. Wenn der Befehl beendet wird, wird er automatisch neu gestartet.

## Befehle und Überschreibungen

Die `commands.start` -Schlüssel ist erforderlich, um Befehle mit der Worker-Anwendung zu starten. Sie können jeden gültigen Shell-Befehl verwenden, obwohl es ideal ist, die Sprache Ihrer Anwendung zu verwenden. Wenn der von der `start` -Schlüssel beendet wird, wird er automatisch neu gestartet.

>[!IMPORTANT]
>
>Die `deploy` und `post_deploy` Hooks und `crons` -Befehle werden nur im Webcontainer ausgeführt, nicht in Worker-Instanzen.

### Vererbung

Definitionen für die `size`, `relationships`, `access`, `disk` und `mount`, und `variables` -Eigenschaften werden von einem Worker vererbt, es sei denn, sie werden explizit überschrieben.

Die folgenden Eigenschaften werden am häufigsten verwendet, um [Einstellungen der obersten Ebene](properties.md):

- `size`—Zuordnung von weniger Ressourcen zu einem einzelnen Hintergrundprozess
- `variables`—Weisen Sie die Anwendung an, anders zu laufen.

### Zeit und Warteschlange

Obwohl jeder Worker sich in eine Warteschlange hinter einem anderen befindet, erzeugt die folgende Konfiguration eine konsistente Zwei-Sekunden-Trennung der Zeitstempel im `var/time.txt` -Datei, unabhängig vom 8-Sekunden-Schlaf im PHP-Code:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
