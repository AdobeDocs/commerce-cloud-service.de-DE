---
title: Launch-Schritte
description: Erfahren Sie, wie Sie den Site-Start abschließen.
exl-id: cf75f89c-94c8-47c1-a23d-93cd9921aab7
source-git-commit: e62236a8937ae1dd10df3c736b2e945be155d236
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Launch-Schritte

Nach dem Testen und Fertigstellen Ihrer Start-Checkliste können Sie die letzten Schritte zum Starten starten. Diese Schritte umfassen die Eingabe von Tickets, die Übertragung des Site-Zugriffs und schließlich die Prüfung Ihres Stores bei Live.

Adobe-Support-Mitarbeiter arbeiten mit Ihnen durch den Prozess, überprüfen den Status und helfen bei Fragen oder Problemen. Alle Probleme sollten mit Tickets nachverfolgt werden, um am besten zu erfassen, was passiert ist und wie es gelöst wurde. Wenn Sie mit kontinuierlichen Iterationen beginnen, die Aktualisierungen in Ihrem gestarteten Store bereitstellen, treten möglicherweise wieder ähnliche Probleme auf. Diese Tickets können dabei helfen, die Probleme zu erkennen und Ihre Bereitstellungsaufgaben anzupassen.

## Wenden Sie sich an Adobe, um Ihre Website zu starten.

Wenden Sie sich an den Adobe Commerce-Support und aktualisieren Sie alle Tickets für den Website-Start (Go Live) mit dem geplanten Datum und der geplanten Uhrzeit, um zu wechseln und Ihren Store zu starten.

## DNS zur neuen Site wechseln

Der Wert &quot;Time-to-Live changed&quot;ist wichtig, um Ihre geänderte Domäne zu überprüfen. Wenn Sie die A- und CNAME-Datensätze ändern, dauert die Aktualisierung die für die TTL konfigurierte Zeit, um die Daten korrekt zu aktualisieren. Weitere Informationen zu DNS-Einstellungen finden Sie unter [DNS-Konfigurationen](checklist.md#update-dns-configuration-with-production-settings).

### So wechseln Sie zur neuen Site:

1. Rufen Sie Ihren DNS-Dienst auf.

1. Aktualisieren Sie Ihre A- und CNAME-Einträge für Ihre Domänen und Hostnamen.

1. Warten Sie, bis die TTL-Zeit vergangen ist, und starten Sie Ihren Webbrowser neu.

1. Greifen Sie über die Storefront-Domäne auf Ihren Store zu.

## Testen des Live Stores

Führen Sie einige UAT-Tests in Ihrem Live Store durch, um sicherzustellen, dass alles ordnungsgemäß geladen und die Aktionen ausgeführt werden. Eine Liste der Tests finden Sie unter [Testen der Bereitstellung](../test/staging-and-production.md#complete-uat-testing).

## Nach dem Start

Adobe überprüft und überwacht die Website, um sicherzustellen, dass alle Dienste und der Zugriff grün sind. Wir bleiben bei Bedarf zur Verfügung, um zu überprüfen, ob alle Systemprotokolle, Dienste, Caching und Funktionen wie Sie und Ihre Kunden benötigen, funktionieren.

Wenn Probleme auftreten, erstellen und verfolgen Sie Probleme mit dem Support. Binden Sie so viele Informationen wie möglich ein, einschließlich Datum/Uhrzeit, spezifischer Funktionen mit einem Problem, Symptomen und ungerade Verhaltensweisen, Erweiterungen und mehr. Wir untersuchen die Protokolle, das Problem und arbeiten mit Ihnen zusammen, um so schnell wie möglich eine Lösung zu finden.
