---
title: Zweite Staging-Umgebung
description: Lernen Sie die Vorteile und Verwendungszwecke einer zweiten Staging-Umgebung für parallele Tests, Problemisolierung, Versionskontrolle und mehr kennen.
source-git-commit: 51fa75fff952e3832151d47b80baa7f532aa277f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# Zweite Staging-Umgebung

In der Adobe Commerce Cloud-Infrastruktur stellt die Staging-Umgebung umfassende Tests und Validierungen in einer Umgebung sicher, die die Produktionsumgebung widerspiegeln kann. Diese Umgebung ermöglicht es Ihnen, Fehler sicher zu identifizieren und zu beheben und gleichzeitig sicherzustellen, dass alle neuen Funktionen oder Änderungen nahtlos integriert sind, bevor sie sich auf Ihre Live-Site auswirken.

Einige Projekte erfordern einen komplexeren Entwicklungs-Workflow. Um dies zu unterstützen, bietet Adobe eine zusätzliche Staging-Umgebung als Add-On-Option für Ihre Cloud-Infrastruktur. Zwei Staging-Umgebungen sind von Vorteil für komplexe Projekte und die gleichzeitige Teamzusammenarbeit.

Eine sekundäre Staging-Umgebung bietet die folgenden Vorteile:

- **Parallel-Tests**: Mit zwei Staging-Umgebungen können Teams neue Funktionen und wichtige Aktualisierungen gleichzeitig testen, ohne die Entwicklung der jeweils anderen zu beeinträchtigen. Sie können beispielsweise eine Umgebung den Funktionstests zuweisen und gleichzeitig die andere Umgebung für Leistungs- und Stresstests reservieren.

- **Isolierung der Probleme**: Wenn in der primären Staging-Umgebung Fehler oder Probleme auftreten, können Sie diese in der sekundären Umgebung replizieren und diagnostizieren, ohne den Testfortschritt zu stoppen. Dadurch wird sichergestellt, dass die Fehlerbehebung laufende Tests nicht beeinträchtigt.

- **Versionskontrolle**: Verwaltung verschiedener Versionen Ihrer Anwendung effizienter. Die primäre Staging-Umgebung kann den neuesten stabilen Build ausführen, während die sekundären Tests experimentelle Funktionen bieten. Dies hilft Ihnen, Release-Zyklen besser zu verwalten und sicherzustellen, dass experimentelle Änderungen keine stabilen Builds stören.

- **Verbesserte Rollout-Planung**: Sie können verschiedene Bereitstellungsszenarien simulieren. Die primäre Staging-Umgebung kann die aktuelle Produktionseinrichtung nachahmen, während die sekundäre Umgebung für den Test bevorstehender Versionen konfiguriert werden kann.

- **Benutzerakzeptanztests (UAT)**: Bei Verwendung der primären Umgebung für die fortlaufende Entwicklung können Sie UAT eine sekundäre Umgebung zuweisen. Dadurch können Benutzer oder Kunden neue Funktionen in einer kontrollierten Umgebung testen und Feedback dazu geben, ohne dass dies Auswirkungen auf Tests hat.

- **Regressionstests**: Sie können eine Umgebung für nach vorne gerichtete Tests und die andere für Regressionstests verwenden, um sicherzustellen, dass neue Änderungen die vorhandene Funktionalität nicht beeinträchtigen.

- **Schulungen und Demonstrationen**: Verwenden Sie eine Umgebung zum Trainieren neuer Teammitglieder oder zum Demonstrieren neuer Funktionen für Stakeholder. Dadurch wird sichergestellt, dass Schulungsaktivitäten Tests nicht unterbrechen.

- **Einrichtung privater Links**: Master- und Integrationsumgebungen unterstützen keine Einrichtung privater Links. Wenn Ihr Entwicklungs-Workflow zusätzliche Umgebungen erfordert, die über Private Link für Entwicklung, Tests oder einen anderen Zweck verbunden werden, sollten Sie erwägen, eine zusätzliche Staging-Umgebung hinzuzufügen.

Durch die Verwendung von zwei Staging-Umgebungen können Sie die Workflow-Effizienz, das Risikomanagement und die Gesamtqualität Ihrer Anwendung erheblich verbessern. Diese Umgebungen bieten Sicherheit und Flexibilität, die eine Staging-Umgebung nicht bieten könnte.

>[!NOTE]
>
>Dieses Setup ist ein Add-on. Kunden, die eine sekundäre Umgebung wünschen, müssen sich an ihren Vertriebsmitarbeiter wenden, um eine anzufordern. Der Vertriebsmitarbeiter kann Informationen zu Preisen und Bereitstellungsprozess bereitstellen.

Wenn Ihr Projekt bereits über eine zusätzliche Staging-Umgebung verfügt oder Sie erwägen, Ihr aktuelles Projekt zu aktualisieren, beachten Sie die folgenden Bereitstellungszeitpläne und -aufgaben:

- Der Bereitstellungsprozess kann bis zu zwei Wochen dauern, nachdem Sie die Anfrage bei Ihrem Adobe-Vertriebsmitarbeiter bestätigt haben.

- Neue Staging-Umgebungen sind nur in derselben Region wie Ihre aktuellen Staging- und Produktionsumgebungen verfügbar.

- Sie müssen entweder Ihre Integrations- oder Master-Umgebung aktualisieren und angeben, auf welcher Umgebung Ihre sekundäre Staging-Umgebung basieren soll. Die sekundäre Staging-Umgebung kann nicht aus der Staging- oder Produktionsumgebung kopiert werden.

- Nachdem Sie Ihre neue Staging-Umgebung erhalten haben, können Sie sie in Ihren Entwicklungsfluss einbeziehen. Wie bei anderen Umgebungen sind auch Code- und Datenbankaktualisierungen in Ihrer Verantwortung.

## Anfordern der Umgebung

Gehen Sie wie folgt vor, um Ihre Anfrage zu erleichtern:

1. Aktualisieren Sie Ihre Verzweigung.

   Aktualisieren Sie Ihre Integration- oder Masterverzweigung mit dem Code und der Datenbank, die Sie für die neue Umgebung verwenden möchten.

1. Wenden Sie sich an Ihren Vertriebsmitarbeiter.

   Wenden Sie sich an Ihren Adobe Sales-Support-Mitarbeiter und stellen Sie ihm die spezifische Verzweigung zur Verfügung, die Sie als Grundlage für Ihre neue Staging-Umgebung (Integration oder Master) verwenden möchten.

1. Bestätigen Sie die Details.

   Nachdem Sie die Details mit Ihrem Vertriebsmitarbeiter bestätigt haben, warten Sie auf die Bestätigung, dass die Bereitstellungsanfrage empfangen wurde und verarbeitet wird. Wenn der Bereitstellungsprozess abgeschlossen ist, sendet Ihnen das Adobe-Team eine Bestätigung.

1. Stellen Sie in Ihrer neuen Umgebung bereit.

   Führen Sie die [standardmäßigen Bereitstellungsschritte](../deploy/staging-production.md) aus, um Ihren Code und Ihre Datenbank in der neuen Staging-Umgebung bereitzustellen.
