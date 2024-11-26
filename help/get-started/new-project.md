---
title: Bereitstellung von Commerce on Cloud
description: Erfahren Sie, wie Sie einen Adobe Customer Technical Advisor für die Bereitstellung Ihres Adobe Commerce-Projekts zur Cloud-Infrastruktur vorbereiten.
recommendations: noDisplay, catalog
role: Admin
exl-id: cfb354b0-c255-4b6e-94aa-c5a6bf7230d6
source-git-commit: 269681efb9925d78ffb608ecbef657be740b5531
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Voraussetzungen für die Bereitstellung von Commerce on Cloud

Beginnen wir mit der Initialisierung Ihres Commerce-Projekts zur Cloud-Infrastruktur!

Bevor Adobe Ihre Commerce in Cloud-Projektumgebungen bereitstellt, sollten Sie die folgenden Strategien berücksichtigen und Antworten für Ihre erste Beratung mit Ihrem Adobe-Account-Team vorbereiten. Verwenden Sie die folgenden Abschnitte als Checkliste, um Sie bei der Vorbereitung auf Ihr Gespräch mit einem technischen Kundenberater zur Bereitstellung eines Cloud-Projekts zu unterstützen:

## Domain-Definition

**Frage 1**: _Welche Domäne oder Domänen beabsichtigen Sie für den Start der Site zu verwenden?_

Bereiten Sie sich auf die Integration der Fastly- und Nginx-Dienste vor, indem Sie Ihre Top-Level-Domänen und Subdomänen für die Pro Staging- und Produktionsumgebungen definieren. Nach der ersten Einrichtung können Sie nur Domänen hinzufügen, indem Sie ein Adobe Commerce-Supportticket senden. Daher wird empfohlen, Ihre Domäneninformationen bereit zu halten.

Beispiele für Produktions- und Staging-Domänen:

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Weitere Anleitungen zu mehreren oder eindeutigen Domänen finden Sie unter [Einrichten mehrerer Websites oder Stores](../cloud-guide/store/multiple-sites.md) im Handbuch _Commerce on Cloud Infrastructure_ .

Weitere Informationen finden Sie unter [Mehrere schnelle Konten und zugewiesene Domänen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly#multiple-fastly-accounts-and-assigned-domains){target="_blank"} , wenn Sie über ein vorhandenes Fastly-Konto verfügen, das dieselbe Apex und dieselben Subdomänen verknüpft, die auf Ihrer Adobe Commerce-Site verwendet werden.

## Transaktions-E-Mail-Domain

**Frage 2**: _Welche Domäne oder Domänen beabsichtigen Sie für Transaktions-E-Mails zu verwenden?_

Adobe Commerce on Cloud verwendet den Proxy-Dienst SendGrid Simple Mail Transfer Protocol (SMTP), der ausgehende E-Mail-Authentifizierungs- und Reputationsüberwachungsdienste bereitstellt. SendGrid sendet Transaktions-E-Mails in Ihrem Namen, daher sind Domäneninformationen erforderlich.

Beispiel für die SendGrid-Domäne: `example@your-store.com`

Weitere Informationen zu Transaktions-E-Mails und Domäneneinstellungen finden Sie unter [SendGrid-Mail-Dienst](../cloud-guide/project/sendgrid.md) im Handbuch _Commerce on Cloud Infrastructure_ .

## Speicherzuweisung

**Frage 3**: _Wie viel von Ihrem vertraglich vereinbarten Speicher planen Sie für den Datei-Upload und für die Datenbank zuzuweisen?_

Adobe Commerce in der Cloud-Infrastruktur verwendet Speicher für die Dateistruktur, die Suchindizierung und die Datenbank. Sie können den Speicher nach Bedarf unterteilen, beginnend mit 10 GB für jede Partition.

Die Menge an Speicherplatz, die Sie für Ihr Cloud-Projekt zugewiesen haben, stellt den Gesamtspeicher für jede Umgebung dar. Wenn Sie beispielsweise 50 GB Speicherplatz gekauft haben, verfügen Sie für jede Umgebung über 50 GB Speicher. Es gibt 50 GB separaten Speicher für Produktion, Staging und jede Integrationsumgebung.

Sie können Ihren vertraglich vereinbarten Speicher jederzeit erhöhen. Für Pro-Produktions- und Staging-Umgebungen müssen Sie ein Adobe Commerce-Support-Ticket senden, um die Speicherplatzzuweisung zu ändern. Eine Vergrößerung der Pro Production- und Staging-Umgebungen kann nur in bestimmten Abständen erfolgen. Je nach aktueller Speichernutzung empfiehlt das Supportteam möglicherweise, die Speicherplatzzuweisung um mindestens 10 GB zu erhöhen. Nach der Zuweisung kann die Speichersteigerung für Pro Staging und Produktion **nicht** zurückgesetzt werden.

Siehe [Verwalten von Speicherplatz](../cloud-guide/storage/manage-disk-space.md) im Handbuch _Commerce in Cloud Infrastructure_.

## Cloud Service-Region

**Frage 4**: _Welche Cloud Service-Region eignet sich am bequemsten zu Ihrer Nähe?_

Wählen Sie entweder Amazon Web Services (AWS) oder Microsoft Azure als Grundlage für Ihre Infrastruktur-as-a-Service-Projekte (IAAs) für Ihre Adobe Commerce in Cloud-Infrastruktur Pro-Projekte. Jeder Dienstleister arbeitet in mehreren Regionen und bietet mehrere Verfügbarkeitszonen. Wählen Sie eine Region aus, die Ihrem Standort entspricht, und reduzieren Sie das Latenzpotenzial und die höheren Kosten.

Siehe [eine Zuordnung der Adobe Commerce-Cloud-Regionen](../cloud-guide/overview.md).

## Verbindungsdienst

**Frage 5**: _Benötigen Sie einen PrivateLink-Dienst? Wenn ja, in welcher Region befindet sich die PrivateLink-Verbindung?_

Adobe Commerce on Cloud Infrastructure unterstützt die Integration mit dem AWS PrivateLink- oder Azure Private Link-Dienst. Obwohl dieser Dienst optional ist, wird PrivateLink verwendet, um eine sichere, private Kommunikation zwischen Cloud-Infrastrukturumgebungen mit Diensten und Anwendungen herzustellen, die auf externen Systemen gehostet werden.

Beachten Sie dabei Ihre Cloud Service-Strategie (AWS oder Azure), damit die Adobe Commerce-Instanz innerhalb derselben Region zugänglich ist. Weitere Informationen zur regionalen Barrierefreiheit finden Sie unter [PrivateLink-Dienst](../cloud-guide/development/privatelink-service.md) im Handbuch _Commerce on Cloud Infrastructure_ .

## Start der Target-Site

**Frage 6**: _Wie lautet Ihr voraussichtliches Zielstartdatum?_

Für das Starten einer Site sind iterative Konfigurationen und Tests erforderlich, um den Erfolg des Site-Starts sicherzustellen. Das Festlegen eines Zieldatums hilft Ihnen und Ihrem Adobe-Account-Team bei der Vorbereitung der endgültigen Aktivitäten vor dem Start, die einen Aufruf zur Koordinierung der letzten Schritte enthalten.

Weitere Informationen finden Sie unter [Übersicht über die Launch-Site](../cloud-guide/launch/overview.md) im Handbuch _Commerce on Cloud Infrastructure_ , um den vollständigen Prozess zu überprüfen und eine Kopie der Launch-Checkliste herunterzuladen.

>[!TIP]
>
> Sehen Sie sich das Cloud-Portal kurz an und greifen Sie auf Ihr neues Cloud-Projekt zu.
>
>**Nächster Schritt**: [Onboarding bei Commerce](onboarding.md)
