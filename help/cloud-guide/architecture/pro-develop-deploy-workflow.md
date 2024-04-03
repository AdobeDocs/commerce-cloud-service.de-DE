---
title: Pro Projekt-Workflow
description: Erfahren Sie, wie Sie die Workflows für die Pro-Entwicklung und -Bereitstellung verwenden.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Pro Projekt-Workflow

Das Pro-Projekt umfasst ein einzelnes Git-Repository mit einer globalen `master` Zweigstellen und drei Hauptumgebungen:

1. **Produktion** Umgebung für den Start und die Pflege der Live-Site
1. **Staging** Umgebung für Tests mit allen Diensten
1. **Integration** Entwicklungs- und Testumgebung

![Pro Umgebungsliste](../../assets/pro-environments.png)

Diese Umgebungen `read-only`, wodurch bereitgestellte Codeänderungen von Verzweigungen akzeptiert werden, die von Ihrem lokalen Arbeitsbereich aus gesendet werden. Siehe [Pro Architektur](pro-architecture.md) für einen vollständigen Überblick über die Pro-Umgebungen. Siehe [[!DNL Cloud Console]](../project/overview.md#cloud-console) für einen Überblick über die Pro-Umgebungen in der Projektansicht.

Die folgende Abbildung zeigt den Workflow für die Entwicklung und Bereitstellung von Pro, der einen einfachen Ansatz mit Git-Verzweigung verwendet. You [entwickeln](#development-workflow) Code mit einer aktiven Verzweigung, die auf der `integration` Umgebung, _Push_ und _ziehen_ Code ändert sich von und zu Ihrer Remote-aktiven Verzweigung. Stellen Sie den bestätigten Code von bereit _Zusammenführen_ die Remote-Verzweigung zur Basisverzweigung, die einen automatisierten [Build und Bereitstellung](#deployment-workflow) für diese Umgebung verarbeitet werden.

![Allgemeine Ansicht des Workflows zur Entwicklung der Pro-Architektur](../../assets/pro-dev-workflow.png)

## Entwicklungs-Workflow

Die Integrationsumgebung bietet eine einzige Basis `integration` -Verzweigung, die Ihre Adobe Commerce im Cloud-Infrastrukturcode enthält. Sie können eine weitere Verzweigung der aktiven Umgebung erstellen. Dies ermöglicht bis zu zwei aktive Verzweigungen, die in Platform as a service (PageS)-Containern bereitgestellt werden. Die Anzahl der inaktiven Umgebungen ist unbegrenzt.

{{enhanced-integration-envs}}

Die Projektumgebungen unterstützen einen flexiblen, kontinuierlichen Integrationsprozess. Beginnen Sie mit dem Klonen der `integration` -Verzweigung in Ihren lokalen Projektordner. Erstellen Sie eine Verzweigung oder mehrere Zweige, entwickeln Sie neue Funktionen, konfigurieren Sie Änderungen, fügen Sie Erweiterungen hinzu und stellen Sie Aktualisierungen bereit:

- **Abrufen** Änderungen von `integration`

- **Verzweigung** von `integration`

- **Entwickeln** Code auf einer lokalen Workstation, einschließlich [!DNL Composer] Updates

- **Push** Codeänderungen an Remote-Zugriff und Validierung

- **Zusammenführen** nach `integration` und Test

Mit einer entwickelten Codeverzweigung und den entsprechenden Konfigurationsdateien können Ihre Codeänderungen mit der `integration` für umfassendere Tests. Die `integration` Umgebung eignet sich auch am besten für:

- **Integration von Drittanbieterdiensten**—Nicht alle Dienste sind in der PaaS-Umgebung verfügbar.

- **Konfigurationsverwaltungsdateien erstellen**—Einige Konfigurationseinstellungen sind _Schreibgeschützt_ in einer bereitgestellten Umgebung.

- **Konfigurieren des Stores**- Sie sollten alle Speichereinstellungen vollständig mit der Integrationsumgebung konfigurieren. Sie finden die **Store-Admin-URL** auf _Integration_ Umgebungsansicht in _[!DNL Cloud Console]_.

## Bereitstellungsarbeitsablauf

Jedes Mal, wenn Sie Code von Ihrer lokalen Workstation in die Remote-Umgebung pushen oder Code in einen Umgebungszweig zusammenführen, generieren die Build- und Bereitstellungsskripte neuen Code und stellen die konfigurierten Dienste für die Remote-Umgebung bereit.

Skriptaktionen erstellen:

- Die Site in der Zielumgebung wird während eines Builds weiterhin ausgeführt

- Adobe Commerce auf Cloud-Infrastruktur-Patches und Hotfixes überprüfen und ausführen

- Kompilieren von Code mit einem Build- und Bereitstellungsprotokoll

- Suchen Sie nach Konfigurationsverwaltung , um die Bereitstellung statischer Inhalte während dieser Phase durchzuführen.

- Erstellen oder verwenden Sie ein Beispiel mit unverändertem Code, um den Prozess zu beschleunigen

- Bereitstellung aller Backend-Dienste und -Anwendungen

Skriptaktionen bereitstellen:

- Platzieren Sie die Site in der Zielumgebung in einer _Wartung_ mode

- Statischen Inhalt bereitstellen, wenn er beim Erstellen nicht abgeschlossen wurde

- Installieren oder Aktualisieren von Adobe Commerce in der Cloud-Infrastruktur

- Routing für Traffic konfigurieren

Nach dem Build- und Bereitstellungsprozess wird Ihr Store mit den neuesten Code-Änderungen und -Konfigurationen wieder online geschaltet. Siehe [Bereitstellungsprozess](../deploy/process.md).

### Zusammenführen zur Integration

Kombinieren Sie alle verifizierten Codeänderungen, indem Sie Ihre aktive Entwicklungsverzweigung in der Basis zusammenführen. `integration` -Verzweigung. Sie können alle Ihre Änderungen auf der `integration` Verzweigung vor der Weiterleitung von Änderungen an der Staging-Umgebung.

### Zu Staging zusammenführen

Staging ist eine Produktionsumgebung vor der Produktion, die alle Dienste und Einstellungen so nah wie möglich an der Produktionsumgebung bereitstellt. Push Ihre Codeänderungen immer über die `integration` der Umgebung `staging` -Umgebung, damit Sie mit allen Diensten gründliche Tests durchführen können. Wenn Sie die Staging-Umgebung zum ersten Mal verwenden, müssen Sie Dienste wie [Fastly CDN](../cdn/fastly.md) und [New Relic](../monitor/new-relic-service.md). Konfigurieren Sie Zahlungskanäle, Versand, Benachrichtigungen und andere wichtige Dienste mit Sandbox- oder Testberechtigungen.

Am besten testen sollten Sie jeden Dienst gründlich testen, Ihre Leistungstestwerkzeuge überprüfen und UAT-Tests als Administrator und Kunde durchführen, bis Sie denken, dass Ihr Geschäft für die Produktionsumgebung bereit ist. Siehe [Bereitstellen Ihres Stores](../deploy/staging-production.md).

### Zusammenführen zur Produktion

Führen Sie nach gründlichen Tests in der Staging-Umgebung eine Zusammenführung in die Produktionsumgebung durch und testen Sie sie mithilfe von Live-Anmeldeinformationen gründlich. Zum Zeitpunkt des Starts Ihrer Produktions-Site müssen Kunden in der Lage sein, Käufe abzuschließen, und Administratoren müssen in der Lage sein, den Live Store zu verwalten. In den folgenden Themen finden Sie eine detaillierte, klare Anleitung zur Bereitstellung Ihres Stores und zur Live-Schaltung:

- [Bereitstellen Ihres Stores](../deploy/staging-production.md)
- [Site-Launch](../launch/overview.md)

### Zu globaler Master zusammenführen

Immer eine Kopie des Produktions-Codes an die globale `master` falls es notwendig ist, die Produktionsumgebung zu debuggen, ohne die Dienste zu unterbrechen.

Do **not** Erstellen einer Verzweigung aus Global `master`. Verwenden Sie die `integration` Verzweigung, um neue, aktive Verzweigungen für Entwicklung und Fehlerbehebungen zu erstellen.
