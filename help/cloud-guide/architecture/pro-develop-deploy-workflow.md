---
title: Pro Projekt-Workflow
description: Erfahren Sie, wie Sie die Workflows für die Pro-Entwicklung und -Bereitstellung verwenden.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: c6d4128792e688485e021bad75d9814a9f4d3b4f
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Pro Projekt-Workflow

Das Pro-Projekt umfasst ein einzelnes Git-Repository mit einer globalen `master`-Verzweigung und drei Hauptumgebungen:

1. **Produktions**-Umgebung zum Starten und Verwalten der Live-Site
1. **Staging**-Umgebung zum Testen mit allen Diensten
1. **Integration**-Umgebung für Entwicklung und Tests

![Pro Umgebungs-Liste](../../assets/pro-environments.png)

Diese Umgebungen sind `read-only` und akzeptieren bereitgestellte Codeänderungen aus Verzweigungen, die von Ihrem lokalen Arbeitsbereich aus gesendet werden. Eine vollständige Übersicht über die Pro-Umgebungen finden Sie unter [Pro-Architektur](pro-architecture.md) . Eine Übersicht über die Liste der Pro-Umgebungen in der Projektansicht finden Sie unter [[!DNL Cloud Console]](../project/overview.md#cloud-console) .

Die folgende Abbildung zeigt den Workflow für die Entwicklung und Bereitstellung von Pro, der einen einfachen Ansatz mit Git-Verzweigung verwendet. Sie [ entwickeln ](#development-workflow) -Code mithilfe einer aktiven Verzweigung, die auf der `integration` -Umgebung basiert. Dabei ändern sich _Push_- und _Pull_-Code von und zu Ihrer Remote-aktiven Verzweigung. Sie stellen den verifizierten Code durch _Zusammenführen_ des Remote-Zweigs mit dem Basis-Zweig bereit, der einen automatisierten [Build- und Bereitstellungsprozess](#deployment-workflow) für diese Umgebung aktiviert.

![Allgemeine Ansicht des Workflows zur Entwicklung der Pro-Architektur](../../assets/pro-dev-workflow.png)

## Entwicklungs-Workflow

Die Integrationsumgebung bietet eine einzige, grundlegende `integration` -Verzweigung, die Ihre Adobe Commerce im Cloud-Infrastrukturcode enthält. Sie können eine weitere Verzweigung der aktiven Umgebung erstellen. Dies ermöglicht bis zu zwei aktive Verzweigungen, die in Platform as a service (PageS)-Containern bereitgestellt werden. Die Anzahl der inaktiven Umgebungen ist unbegrenzt.

{{enhanced-integration-envs}}

Die Projektumgebungen unterstützen einen flexiblen, kontinuierlichen Integrationsprozess. Klonen Sie zunächst die Verzweigung `integration` in Ihren lokalen Projektordner. Erstellen Sie eine Verzweigung oder mehrere Zweige, entwickeln Sie neue Funktionen, konfigurieren Sie Änderungen, fügen Sie Erweiterungen hinzu und stellen Sie Aktualisierungen bereit:

- **Fetch** ändert sich von `integration`

- **Verzweigung** von `integration`

- **Entwickeln** Code auf einer lokalen Workstation, einschließlich [!DNL Composer] Updates

- **Push**-Codeänderungen an Remote-Zugriff und -Validierung

- **Merge** zu `integration` und test

Mit einer entwickelten Codeverzweigung und den entsprechenden Konfigurationsdateien können Ihre Codeänderungen mit der `integration` -Verzweigung zusammengeführt werden, um umfassendere Tests zu ermöglichen. Die `integration` -Umgebung eignet sich auch am besten für:

- **Integrieren von Drittanbieterdiensten**: Nicht alle Dienste sind in der PAs-Umgebung verfügbar.

- **Generieren von Konfigurationsverwaltungsdateien** - Einige Konfigurationseinstellungen sind _schreibgeschützt_ in einer bereitgestellten Umgebung.

- **Konfigurieren des Stores**: Sie sollten alle Speichereinstellungen vollständig mit der Integrationsumgebung konfigurieren. Sie finden die **Store Admin URL** in der Umgebungsansicht _integration_ in der Ansicht _[!DNL Cloud Console]_.

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

- Platzieren Sie die Site in der Zielumgebung im Modus _Wartung_ .

- Statischen Inhalt bereitstellen, wenn er beim Erstellen nicht abgeschlossen wurde

- Installieren oder Aktualisieren von Adobe Commerce in der Cloud-Infrastruktur

- Routing für Traffic konfigurieren

Nach dem Build- und Bereitstellungsprozess wird Ihr Store mit den neuesten Code-Änderungen und -Konfigurationen wieder online geschaltet. Siehe [Bereitstellungsprozess](../deploy/process.md).

### Zusammenführen zur Integration

Kombinieren Sie alle verifizierten Codeänderungen, indem Sie Ihre aktive Entwicklungsverzweigung in der Basis-Verzweigung `integration` zusammenführen. Sie können alle Änderungen in der Verzweigung `integration` testen, bevor Sie Änderungen an der Staging-Umgebung weiterleiten.

### Zu Staging zusammenführen

Staging ist eine Produktionsumgebung vor der Produktion, die alle Dienste und Einstellungen so nah wie möglich an der Produktionsumgebung bereitstellt. Übertragen Sie Ihre Codeänderungen immer von der `integration` -Umgebung in die `staging` -Umgebung, damit Sie mit allen Diensten gründliche Tests durchführen können. Wenn Sie die Staging-Umgebung zum ersten Mal verwenden, müssen Sie Dienste wie [Fastly CDN](../cdn/fastly.md) und [New Relic](../monitor/new-relic-service.md) konfigurieren. Konfigurieren Sie Zahlungskanäle, Versand, Benachrichtigungen und andere wichtige Dienste mit Sandbox- oder Testberechtigungen.

Am besten testen sollten Sie jeden Dienst gründlich testen, Ihre Leistungstestwerkzeuge überprüfen und UAT-Tests als Administrator und Kunde durchführen, bis Sie denken, dass Ihr Geschäft für die Produktionsumgebung bereit ist. Siehe [Bereitstellen Ihres Stores](../deploy/staging-production.md).

{{second-staging}}

### Zusammenführen zur Produktion

Führen Sie nach gründlichen Tests in der Staging-Umgebung eine Zusammenführung in die Produktionsumgebung durch und testen Sie sie mithilfe von Live-Anmeldeinformationen gründlich. Zum Zeitpunkt des Starts Ihrer Produktions-Site müssen Kunden in der Lage sein, Käufe abzuschließen, und Administratoren müssen in der Lage sein, den Live Store zu verwalten. In den folgenden Themen finden Sie eine detaillierte, klare Anleitung zur Bereitstellung Ihres Stores und zur Live-Schaltung:

- [Bereitstellen Ihres Stores](../deploy/staging-production.md)
- [Site-Launch](../launch/overview.md)

### Zu globaler Master zusammenführen

Pushen Sie stets eine Kopie des Produktionscodes an den globalen Ordner &quot;`master`&quot;, falls es notwendig ist, die Produktionsumgebung zu debuggen, ohne die Dienste zu unterbrechen.

Erstellen Sie **nicht** einen Zweig aus Global `master`. Verwenden Sie die Verzweigung `integration` , um neue aktive Verzweigungen für die Entwicklung und Fehlerbehebungen zu erstellen.
