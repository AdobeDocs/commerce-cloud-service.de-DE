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

Im _APM und Services_ Seite, wählen Sie die **Zusammenfassung** um Transaktionsinformationen zu Ihrer Anwendung anzuzeigen. Diese Ansicht hilft Ihnen dabei, potenzielle Fehler zu identifizieren und den allgemeinen Zustand Ihrer Anwendung und Dienste zu überprüfen.

![Übersichtsseite zum Cloud-Projekt - New Relic](../../assets/new-relic/dashboard.png)

In dieser Ansicht können Sie Transaktionen verfolgen, die auf langsame Antworten oder Engpässe, den Anwendungsdurchsatz, Webfehler und mehr stoßen.

Getrackte Daten überprüfen:

- **Meist zeitaufwendig**—Bestimmen Sie den Zeitverbrauch durch paralleles Tracking von Anforderungen. Sie können beispielsweise die höchste Transaktionszeit in Produkt- und Kategorieansichten haben. Wenn eine Kundenkontoseite plötzlich einen hohen Zeitverbrauch aufweist, kann sich die Leistung bei Aufrufen oder Abfragen auf Ihre Anwendung auswirken.

- **Höchster Durchsatz**- Identifizieren Sie die Seiten, die am meisten auf der Grundlage der Größe und Häufigkeit der gesendeten Bytes treffen.

Alle erfassten Daten geben die Zeit an, die mit Aktionen verbracht wurde, die Daten, Abfragen oder _Redis_ Daten. Wenn Abfragen Probleme verursachen, stellt New Relic Informationen zur Verfolgung und Reaktion auf diese Probleme bereit.

>[!TIP]
>
>Weitere Informationen zur Verwendung dieser Daten zur Fehlerbehebung bei Problemen mit der Anwendungsleistung finden Sie unter [Fehlerbehebung bei der Leistung mit New Relic](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) im _Adobe Commerce Help Center_.

## Überwachen der Leistung mit verwalteten Warnhinweisen

Adobe stellt die _Verwaltete Warnhinweise für Adobe Commerce_ Warnhinweisrichtlinie zum Verfolgen von Leistungsmetriken. Die Richtlinie enthält eine Sammlung von Warnhinweisen, die Schwellenwerte und Warnungen für Trigger sowie kritische Benachrichtigungen festlegen, wenn Infrastruktur- oder Anwendungsprobleme die Site-Performance beeinträchtigen. Die Richtlinie verfolgt die folgenden Metriken in Produktionsumgebungen:

| Metrik | Datenerfassung | Verfügbarkeit |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] score | APM | Pro und Starter |
| CPU-Auslastung | NRI | Pro |
| Festplattenspeicher | NRI | Pro |
| Fehlerrate | APM | Pro und Starter |
| Speichernutzung | NRI | Pro |
| MariaDB-Abfrage laden | NRI | Pro |
| Redis Memory | NRI | Pro |

Wenn die Site-Infrastruktur oder die Anwendungsbedingungen eine Alarmschwelle Trigger, sendet New Relic Warnhinweise, damit Sie das Problem proaktiv beheben können. Siehe [Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) im _Adobe Commerce Help Center_ für Details zu Warnschwellen und Schritte zur Fehlerbehebung, um die Probleme zu beheben, die den Warnhinweis ausgelöst haben.

>[!TIP]
>
>Verwenden Sie für Umgebungen und Starterumgebungen für Pro Staging und Integration die [Statusbenachrichtigungen](../integrations/health-notifications.md) , um den Festplattenspeicher zu überwachen.

>[!PREREQUISITES]
>
>- **New Relic-Anmeldeinformationen**—Anmeldedaten für die Anmeldung beim New Relic-Konto für Ihr Cloud-Projekt
>- **Aktive New Relic-Integration**—Stellen Sie sicher, dass Ihre Cloud-Umgebung mit New Relic verbunden ist.
>- **Workflow-Benachrichtigung**—Konfigurieren Sie mindestens eine [Workflow](#set-up-a-workflow-for-notifications) um Warnhinweise zu erhalten

**So überprüfen Sie die Richtlinie &quot;Verwaltete Warnhinweise für Adobe Commerce&quot;**:

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login).

1. Suchen Sie die _Verwaltete Warnhinweise für Adobe Commerce_ Richtlinie:

   - Klicken Sie im Explorer-Navigationsmenü auf **[!UICONTROL Alerts & AI]**.

   - under _Erkennen_ klicken **[!UICONTROL Alert Conditions & Policies]**.

   - Stellen Sie sicher, dass Ihr Konto oben im _Warnungsbedingungen und Richtlinien_ anzeigen.

   - Im _Politik_ Liste auswählen **Verwaltete Warnhinweise für Adobe Commerce** -Richtlinie.

     ![Generierte Richtlinien für Warnhinweise](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Wenn die Variable _Verwaltete Warnhinweise für Adobe Commerce_ -Richtlinie nicht verfügbar ist, siehe [Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) im _Adobe Commerce Help Center_.

1. Klicken Sie auf **[!UICONTROL Alert conditions]** um die in der Richtlinie definierten Warnungsbedingungen zu überprüfen.

## Erstellen von Warnhinweisrichtlinien

Ändern Sie keine Warnhinweise, die in der Richtlinie &quot;Managed Warnungen for Adobe Commerce&quot;enthalten sind. Adobe aktualisiert und verbessert die Alarmbedingungen in dieser Richtlinie im Laufe der Zeit, wodurch alle Anpassungen überschrieben werden, die Sie zur Richtlinie hinzufügen.

Anstatt einen vorhandenen Warnhinweis zu ändern, können Sie eine Warnhinweisrichtlinie erstellen. Kopieren Sie dann die Warnungsbedingungen in die neue Richtlinie. Siehe [Richtlinien oder Bedingungen aktualisieren](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) im _New Relic_ Dokumentation.

>[!TIP]
>
>Siehe [Einführung in Warnhinweise](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) im _New Relic_ Dokumentation für detailliertere Informationen zu Warnhinweisen, Warnhinweisrichtlinien und Workflows.

## Einrichten eines Workflows für Benachrichtigungen

Sie können jetzt eine _Workflow_, früher als Benachrichtigungskanal bezeichnet, um Benachrichtigungen über die Leistung Ihrer Site auf der Grundlage gefilterter Daten zu erhalten, z. B. eine Warnhinweisrichtlinie. Benachrichtigungen über Leistungsprobleme werden an alle Workflows gesendet, die mit einer Warnhinweisrichtlinie verknüpft sind, wenn die Bedingungen für die Anwendung oder den Trigger der Infrastruktur eine Warnung auslösen. Sie erhalten auch Benachrichtigungen, wenn ein Problem erkannt und geschlossen wird.

New Relic bietet Vorlagen zum Konfigurieren verschiedener Arten von Workflow-Benachrichtigungen, einschließlich E-Mail, Slack, PagerDuty, Webhooks und mehr.

**So konfigurieren Sie einen Workflow**:

1. Melden Sie sich bei Ihrer [New Relic-Konto](https://login.newrelic.com/login).

1. Erstellen Sie einen Workflow.

   - Klicken Sie im Explorer-Navigationsmenü auf **[!UICONTROL Alerts & AI]**.

   - Im linken Navigationsbereich unter _Anreichern und Benachrichtigen_ klicken **[!UICONTROL Workflows]**.

   - Klicks **[!UICONTROL Add a workflow]** auf der rechten Seite.

     ![New Relic fügt einen Workflow hinzu](../../assets/new-relic/add-a-workflow.png)

   - Im _Workflow konfigurieren_ -Seite einen Namen für den Workflow eingeben.

   - Im _Daten filtern_ Bereich, wählen Sie **[!UICONTROL Managed Alerts for Adobe Commerce]** aus dem **[!UICONTROL Policy]** Dropdown-Liste.

   - Im _Benachrichtigen_ wählen Sie einen Kanal aus und befolgen Sie die Anweisungen.

   - Klicks **[!UICONTROL Test workflow]** , um Ihre Konfiguration zu überprüfen.

1. Klicks **[!UICONTROL Activate workflow]**.

Weitere Informationen finden Sie in der New Relic-Dokumentation zu [Workflows](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>Für Warnhinweise in der Richtlinie &quot;Managed Alerts für Adobe Commerce&quot;sind standardmäßige Workflows konfiguriert, um Adobe-Teams zu benachrichtigen, die Adobe Commerce für Cloud-Infrastrukturkunden unterstützen. Ändern Sie die Konfiguration für diese Standardkanäle nicht und entfernen Sie keine ihnen zugewiesenen Warnhinweisrichtlinien.
