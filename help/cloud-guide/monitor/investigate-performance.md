---
title: New Relic-Überwachung
description: Erfahren Sie, wie Sie auf Ihr New Relic-Dashboard zugreifen und Daten aus Ihrer Adobe Commerce in einem Cloud-Infrastrukturprojekt analysieren können.
feature: Cloud, Observability
topic: Performance
exl-id: 8d1e2ad6-14d0-4754-9703-960d93e135a9
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# New Relic-Überwachung

New Relic verbindet und überwacht Ihre Infrastruktur und [!DNL Commerce] Anwendung mit PHP-Agenten. Nachdem eine Cloud-Umgebung eine Verbindung zu New Relic hergestellt hat, können Sie sich bei Ihrem New Relic-Konto anmelden, um die vom Agenten erfassten Daten zu überprüfen.

Wählen Sie auf der Seite _APM &amp; Services_ die **Zusammenfassung** aus, um Transaktionsinformationen zu Ihrer Anwendung anzuzeigen. Diese Ansicht hilft Ihnen dabei, potenzielle Fehler zu identifizieren und den allgemeinen Zustand Ihrer Anwendung und Dienste zu überprüfen.

![New Relic-Übersichtsseite des Cloud-Projekts](../../assets/new-relic/dashboard.png)

In dieser Ansicht können Sie Transaktionen verfolgen, die auf langsame Antworten oder Engpässe, den Anwendungsdurchsatz, Webfehler und mehr stoßen.

Getrackte Daten überprüfen:

- **Am zeitintensivsten**: Bestimmen Sie den Zeitverbrauch durch paralleles Verfolgen von Anforderungen. Sie können beispielsweise die höchste Transaktionszeit in Produkt- und Kategorieansichten haben. Wenn eine Kundenkontoseite plötzlich einen hohen Zeitverbrauch aufweist, kann sich die Leistung bei Aufrufen oder Abfragen auf Ihre Anwendung auswirken.

- **Höchster Durchsatz**: Identifizieren Sie die Seiten, die am meisten erreicht werden, basierend auf der Größe und Häufigkeit der übertragenen Bytes.

Alle erfassten Daten geben an, wie viel Zeit mit Aktionen verbracht wurde, die Daten, Abfragen oder _Redis_-Daten übertragen. Wenn Abfragen Probleme verursachen, stellt New Relic Informationen zur Verfolgung und Reaktion auf diese Probleme bereit.

>[!TIP]
>
>Weitere Informationen zur Verwendung dieser Daten zur Fehlerbehebung bei Problemen mit der Anwendungsleistung finden Sie unter [Fehlerbehebung bei der Leistung mit New Relic](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) im _Adobe Commerce Help Center_.

## Überwachen der Leistung mit verwalteten Warnhinweisen

Adobe bietet die Warnrichtlinie _Verwaltet Warnhinweise für Adobe Commerce_ , um Leistungsmetriken zu verfolgen. Die Richtlinie enthält eine Sammlung von Warnhinweisen, die Schwellenwerte und Warnungen für Trigger sowie kritische Benachrichtigungen festlegen, wenn Infrastruktur- oder Anwendungsprobleme die Site-Performance beeinträchtigen. Die Richtlinie verfolgt die folgenden Metriken in Produktionsumgebungen:

| Metrik | Datenerfassung | Verfügbarkeit |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] Ergebnis | APM | Pro und Starter |
| CPU-Auslastung | NRI | Pro |
| Festplattenspeicher | NRI | Pro |
| Fehlerrate | APM | Pro und Starter |
| Speichernutzung | NRI | Pro |
| MariaDB-Abfrage laden | NRI | Pro |
| Redis Memory | NRI | Pro |

Wenn die Site-Infrastruktur oder die Anwendungsbedingungen eine Alarmschwelle Trigger, sendet New Relic Warnhinweise, damit Sie das Problem proaktiv beheben können. Unter [Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) im _Adobe Commerce Help Center_ finden Sie Informationen zu Warnschwellen und Schritte zur Fehlerbehebung, um die Probleme zu beheben, die den Warnhinweis ausgelöst haben.

>[!TIP]
>
>Verwenden Sie für Staging- und Integrationsumgebungen und Starterumgebungen [Statusbenachrichtigungen](../integrations/health-notifications.md), um Speicherplatz zu überwachen.

>[!PREREQUISITES]
>
>- **New Relic-Anmeldeinformationen** - Anmeldedaten für die Anmeldung beim New Relic-Konto für Ihr Cloud-Projekt
>- **Aktive New Relic-Integration** - Stellen Sie sicher, dass Ihre Cloud-Umgebung mit New Relic verbunden ist.
>- **Workflow-Benachrichtigung**—Konfigurieren Sie mindestens einen [Workflow](#set-up-a-workflow-for-notifications) für den Empfang von Warnhinweisen

**So überprüfen Sie die Richtlinie &quot;Managed Alerts for Adobe Commerce&quot;**:

1. Melden Sie sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) an.

1. Suchen Sie die Richtlinie _Verwaltete Warnhinweise für Adobe Commerce_ :

   - Klicken Sie im Explorer-Navigationsmenü auf **[!UICONTROL Alerts & AI]**.

   - Klicken Sie unter _Erkennen_ auf **[!UICONTROL Alert Conditions & Policies]**.

   - Stellen Sie sicher, dass Ihr Konto oben in der Ansicht _Bedingungen und Richtlinien für Warnhinweise_ ausgewählt ist.

   - Wählen Sie in der Liste _Richtlinie_ die Richtlinie **Verwaltet Warnhinweise für Adobe Commerce** aus.

     ![Generierte Warnhinweisrichtlinien](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Wenn die Richtlinie _Verwaltet Warnhinweise für Adobe Commerce_ nicht verfügbar ist, finden Sie weitere Informationen unter [Verwaltet Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) im _Adobe Commerce Help Center_.

1. Klicken Sie auf den Tab **[!UICONTROL Alert conditions]** , um die in der Richtlinie definierten Warnungsbedingungen zu überprüfen.

## Erstellen von Warnhinweisrichtlinien

Ändern Sie keine Warnhinweise, die in der Richtlinie &quot;Managed Warnungen for Adobe Commerce&quot;enthalten sind. Adobe aktualisiert und verbessert die Alarmbedingungen in dieser Richtlinie im Laufe der Zeit, wodurch alle Anpassungen überschrieben werden, die Sie zur Richtlinie hinzufügen.

Anstatt einen vorhandenen Warnhinweis zu ändern, können Sie eine Warnhinweisrichtlinie erstellen. Kopieren Sie dann die Warnungsbedingungen in die neue Richtlinie. Siehe [Richtlinien oder Bedingungen aktualisieren](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) in der Dokumentation zu _New Relic_ .

>[!TIP]
>
>Weitere Informationen zu Warnhinweisen, Warnhinweisrichtlinien und Workflows finden Sie unter [Einführung in Warnhinweise](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) in der Dokumentation zu _New Relic_ .

## Einrichten eines Workflows für Benachrichtigungen

Sie können jetzt einen _Workflow_ einrichten, der zuvor als Benachrichtigungskanal bezeichnet wurde, um Benachrichtigungen über die Leistung Ihrer Site auf der Grundlage gefilterter Daten wie einer Warnhinweisrichtlinie zu erhalten. Benachrichtigungen über Leistungsprobleme werden an alle Workflows gesendet, die mit einer Warnhinweisrichtlinie verknüpft sind, wenn die Bedingungen für die Anwendung oder den Trigger der Infrastruktur eine Warnung auslösen. Sie erhalten auch Benachrichtigungen, wenn ein Problem erkannt und geschlossen wird.

New Relic bietet Vorlagen zum Konfigurieren verschiedener Arten von Workflow-Benachrichtigungen, einschließlich E-Mail, Slack, PagerDuty, Webhooks und mehr.

**So konfigurieren Sie einen Workflow**:

1. Melden Sie sich bei Ihrem [New Relic-Konto](https://login.newrelic.com/login) an.

1. Erstellen Sie einen Workflow.

   - Klicken Sie im Explorer-Navigationsmenü auf **[!UICONTROL Alerts & AI]**.

   - Klicken Sie im linken Navigationsbereich unter _Anreichern und Benachrichtigen_ auf **[!UICONTROL Workflows]**.

   - Klicken Sie auf der rechten Seite auf **[!UICONTROL Add a workflow]**.

     ![New Relic fügt einen Workflow hinzu](../../assets/new-relic/add-a-workflow.png)

   - Geben Sie auf der Seite _Workflow konfigurieren_ einen Namen für den Workflow ein.

   - Wählen Sie im Abschnitt _Daten filtern_ die Option **[!UICONTROL Managed Alerts for Adobe Commerce]** aus der Dropdownliste **[!UICONTROL Policy]** aus.

   - Wählen Sie im Abschnitt _Benachrichtigen_ einen Kanal aus und befolgen Sie die Anweisungen.

   - Klicken Sie auf **[!UICONTROL Test workflow]** , um Ihre Konfiguration zu überprüfen.

1. Klicken Sie auf **[!UICONTROL Activate workflow]**.

Weitere Informationen finden Sie in der New Relic-Dokumentation zu [Workflows](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>Für Warnhinweise in der Richtlinie &quot;Managed Alerts für Adobe Commerce&quot;sind standardmäßige Workflows konfiguriert, um Adobe-Teams zu benachrichtigen, die Adobe Commerce für Cloud-Infrastrukturkunden unterstützen. Ändern Sie die Konfiguration für diese Standardkanäle nicht und entfernen Sie keine ihnen zugewiesenen Warnhinweisrichtlinien.
