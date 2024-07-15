---
title: Optimieren der Cloud-Implementierung
description: Erfahren Sie, wie Sie den Implementierungsprozess für Adobe Commerce für Cloud-Infrastrukturprojekte optimieren können, einschließlich Ausfallzeiten, statischer Inhaltsbereitstellung, szenarienbasierter Bereitstellung und intelligenter Assistenten.
feature: Cloud, Deploy, SCD
exl-id: 62e5eccb-6919-4a4b-9f50-6105f9d0f3af
source-git-commit: 5c47c8bf9c97fac70ef249f76ecc905df07e4437
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Implementierung optimieren

Die Site-Leistung kann während des Implementierungsprozesses beeinträchtigt sein. Die Dauer, die eine Site bei der Bereitstellung auf einer Produktionssite im Wartungsmodus verbringt, hängt von vielen Faktoren ab, z. B. von der Umgebungskonfiguration und der Menge an Inhalten, die eine Site enthält. Die erste Best Practice zur Optimierung Ihrer Cloud-Implementierung besteht darin, ein [Upgrade durchzuführen, um `ece-tools`](../dev-tools/install-package.md) zu verwenden und von den Paketfunktionen zu profitieren, z. B. Befehlen zum Erstellen einer Sicherung der Datenbank und zur Überprüfung der Umgebungskonfiguration.

Die folgenden Themen helfen Ihnen dabei, die Optimierung des Implementierungsprozesses zu verstehen:

- [Cloud-Bereitstellungsprozess](process.md)
Der Cloud-Implementierungsprozess gliedert sich in drei Phasen. Sie können die Stärken und Schwächen jeder Phase zu Ihrem Vorteil nutzen.

- [Keine Ausfallzeitbereitstellung](reduce-downtime.md)
Erfahren Sie, was während der Bereitstellung geschieht und wie Sie die Ausfallzeit Ihrer Store-Erlebnisse während einer Aktualisierung der Produktionsumgebung reduzieren können.

- [Statische Inhaltsbereitstellung](static-content.md)
Die beste Methode zur Optimierung Ihrer Cloud-Implementierung besteht darin, zu steuern, wie und wann statische Inhalte generiert werden.

- [Smart-Assistenten](smart-wizards.md)
Das Paket `ece-tools` enthält die Befehle des intelligenten Assistenten, um Ihre Projektkonfiguration schnell zu bewerten.

- [Implementierungen mit New Relic verfolgen](../monitor/track-deployments.md)
Verwenden Sie den New Relic-Dienst, um Bereitstellungsereignisse zu überwachen und die Auswirkungen der Bereitstellung auf die Gesamtleistung zu analysieren.
