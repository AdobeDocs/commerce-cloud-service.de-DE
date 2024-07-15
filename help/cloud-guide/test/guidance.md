---
title: Testleitfaden
description: Erfahren Sie mehr über Testtypen und Best Practices für den Start von Adobe Commerce in der Cloud-Infrastruktur.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Testleitfaden

Nach dem Konfigurieren und Anpassen Ihres Adobe Commerce-Projekts für die Cloud-Infrastruktur empfiehlt es sich, Ihre Anwendung gründlich zu testen, bevor Sie die Store-Website starten. Beim Testen können Sie die Erwartungen an die Cluster-Größe ordnungsgemäß verwalten und entsprechend den künftigen Geschäftsanforderungen skalieren.

## Funktionstests

Bei der Entwicklung ist es wichtig, durchgängige Funktionstests für Ihre Adobe Commerce im Cloud-Infrastrukturprojekt durchzuführen. Weitere Informationen finden Sie in den folgenden Anleitungen zum Ausführen von Funktionstests in der Docker-Umgebung:

- **Anwendungstests**: Verwenden Sie das [Magento Functional Testing Framework (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) für Anwendungstests in der Cloud Docker-Umgebung.

- **Code-Tests**: Verwenden Sie das [Codeception testing framework for PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/)-Framework für die Validierung von Code, der für Beiträge zu Cloud-Package-Repositorys vorgesehen ist.

## Best Practices vor dem Start

Beachten Sie die folgenden Testtypen als Best Practice, die vor dem Start der Site durchgeführt werden sollten:

- **Belastungstest**: Führen Sie einen Belastungstest durch, um das Verhalten des Systems bei einer erwarteten Belastung zu verstehen. Testen Sie beispielsweise eine gleichzeitige Anzahl aktiver Benutzer in der Anwendung, wobei jeder Benutzer eine bestimmte Anzahl von Transaktionen innerhalb der festgelegten Dauer durchführt. Dieser Test zeigt die Reaktionszeit wichtiger geschäftskritischer Transaktionen, wie z. B. des Verhaltens von Datenbank- oder Anwendungsservern. Ein Belastungstest kann dabei helfen, Engpässe zu erkennen.

- **Belastungstest**: Stellen Sie die oberen Kapazitätsgrenzen im System infrage, um festzustellen, ob das System ausreichend leistungsfähig ist, wenn die aktuelle Last deutlich über dem erwarteten Maximum liegt.

- **Sicherheitsscan** - Adobe stellt ein kostenloses [Sicherheitsscan-Tool](../launch/overview.md#set-up-the-security-scan-tool) für Ihre Sites bereit.

- **Penetrationstest**: Ist ein autorisierter simulierter Cyberangriff auf ein Computersystem, der dazu bestimmt ist, die Sicherheit des Systems zu bewerten. Der Penetrationstest hilft dabei, Schwächen oder Schwachstellen zu identifizieren, einschließlich des Potenzials für nicht autorisierte Parteien, Zugriff auf Systemfunktionen und Daten zu erhalten.

>[!WARNING]
>
>Kunden dürfen keine Sicherheitsbewertungen der AWS-Infrastruktur oder der AWS-Dienste selbst durchführen. Wenn Sie ein Sicherheitsproblem innerhalb eines der in Ihrer Sicherheitsbewertung beschriebenen AWS-Dienste feststellen, wenden Sie sich sofort an [AWS Security](mailto:aws-security@amazon.com) . Siehe [AWS-Kundenrichtlinien für Penetrationstests](https://aws.amazon.com/security/penetration-testing/).
