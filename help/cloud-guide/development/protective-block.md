---
title: Schutzblock
description: Erfahren Sie mehr über die Schutzblockfunktion von Adobe Commerce in der Cloud-Infrastruktur und wie sie Ihre Site vor bekannten Sicherheitslücken schützt.
feature: Cloud, Configuration, Security
topic: Security
exl-id: bc1def41-9521-4005-872e-9ecaab1d4d16
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Schutzblock

Adobe Commerce in der Cloud-Infrastruktur verfügt über eine Schutzblockierfunktion, die unter bestimmten Umständen den Zugriff auf Websites mit Sicherheitslücken einschränkt. Diese partielle Blockierungsmethode verhindert die Nutzung bekannter Sicherheitslücken. Veraltete Software enthält oft Exploits, daher ist es wichtig, vor diesen Exploits zu schützen, indem der Zugriff auf diese Seiten teilweise blockiert wird.

## Funktionsweise des Schutzblocks

Adobe Commerce unterhält eine Datenbank mit Signaturen bekannter Sicherheitslücken in Open-Source-Software, die häufig in der Cloud-Infrastruktur bereitgestellt werden. Die Sicherheitsprüfung analysiert nur bekannte Schwachstellen in Open-Source-Projekten; sie kann keine Anpassungen untersuchen, die Sie schreiben.

Die Sicherheitsprüfung wird ausgeführt:

- Wenn Sie neuen Code an Git senden
- Wenn neue Sicherheitslücken zur Datenbank hinzugefügt werden

Wenn eine kritische Schwachstelle in Ihrer Anwendung erkannt wird, wird die Git-Push-Benachrichtigung zurückgewiesen.

Es werden zwei Arten von Blöcken ausgeführt:

1. **Vollständiger Block**—für Entwicklungswebsites. Begleitende Fehlermeldung `git push` enthält detaillierte Informationen zur Schwachstelle.

1. **Teilblock**—für Produktions-Websites, die es der Website ermöglichen, meist online zu bleiben. Je nach Art der Sicherheitslücke können Teile einer Anforderung, wie z. B. eine Abfragezeichenfolge, Cookies oder zusätzliche Header, aus GET-Anforderungen entfernt werden. Alle anderen Anfragen können vollständig blockiert werden, z. B. Anmeldung, Formularübermittlung oder Produktkasse.

Die Aufhebung der Sperrung wird nach Beseitigung des Sicherheitsrisikos automatisiert. Der Block wird kurz nach dem Anwenden eines Sicherheits-Upgrades entfernt, durch das die Schwachstelle entfernt wird.

## Aus dem Schutzblock ausschließen

Der Schutzblock dient zum Schutz vor bekannten Sicherheitslücken in der Software, die Sie Adobe Commerce in der Cloud-Infrastruktur bereitstellen.

Sie können den Schutzblock jedoch deaktivieren, indem Sie Folgendes zu [`.magento.app.yaml`](../application/configure-app-yaml.md):

```yaml
   preflight:
      enabled: false
```

Sie können eine bestimmte Prüfung explizit abwählen, z. B.:

```yaml
   preflight:
      enabled: true
      ignore_rules: [ "drupal:SA-CORE-2014-005" ]
```
