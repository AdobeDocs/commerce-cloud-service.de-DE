---
title: Aktivitäts-Stream
description: Erfahren Sie, wie Sie den Aktivitäts-Stream im [!DNL Cloud Console] oder die Cloud-CLI für Adobe Commerce in der Cloud-Infrastruktur.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ffef5ab4-ef40-4073-adc8-a44c61c0d77b
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Aktivitäts-Stream

Die Hauptansicht für jede Umgebung zeigt eine **Aktivität** Liste historischer Ereignisse ähnlich einem Git-Protokoll. Die Aktivitätenliste ist ein Stream der letzten Ereignisse für aktive Umgebungen. Im Folgenden finden Sie eine Liste der Aktivitätstypen und ihrer Symbole, die im Aktivitäts-Stream angezeigt werden:

![Aktivitätstypen](../../assets/activity-types.svg){width="500" align="center"}

## Protokolle anzeigen

Klicken Sie in der Liste &quot;Aktivität&quot;auf das Statussymbol einer Aktivität, um das Protokoll anzuzeigen. Alternativ können Sie auf die ![Mehr](../../assets/icon-more.png){width="32"} (_more_), um auf weitere Optionen zur Verwaltung der Aktivität zuzugreifen. Das folgende Beispiel zeigt ein kurzes Protokoll, das eine Sicherung erstellt. Sie können [Verwenden der Cloud-CLI](#activity-stream-with-cloud-cli) um dasselbe Protokoll anzuzeigen.

![Protokollansicht](../../assets/log-view.png)

## Aktivität verwalten

Einige Aktivitäten befinden sich in einer _running_ oder _pending_ -Status. Sie können auf eine laufende Aktivität reagieren, z. B. auf den Abbruch einer laufenden Bereitstellung. Die folgenden Tabs zeigen zwei Methoden zum Abbrechen einer Aktivität: die [!DNL Cloud Console] oder die Cloud-CLI.

>[!BEGINTABS]

>[!TAB Konsole]

**So brechen Sie eine Aktivität im[!DNL Cloud Console]**:

Sie können auf eine laufende Aktivität reagieren, indem Sie auf die ![Mehr](../../assets/icon-more.png){width="32"} (_more_) und wählen Sie eine Aktion aus, z. B. `Cancel` oder `View log`. Wählen Sie für dieses Beispiel die **Abbrechen** -Option, um die laufende Aktivität anzuhalten.

Nicht alle Aktivitäten haben die Option zum Abbrechen. Beispielsweise wird die Option zum Abbrechen der Anwendungsimplementierung nur während der _build_ Phase. Sobald die Anwendung in die _deploy_ -Phase, können Sie die Aktivität nicht mehr abbrechen. Siehe [Bereitstellungsprozess](../deploy/process.md) über die verschiedenen Phasen.

![Aktivität abbrechen](../../assets/activity-icons/cancel-activity.png){width="450" align="center"}

Wenn Sie über ein Terminal verfügen, auf dem die Bereitstellungsaktivität ausgeführt wird, brechen Sie den Vorgang im [!DNL Cloud Console] führt zur Annullierung im Terminal:

![Aktivität am Terminal abgebrochen](../../assets/activity-icons/activity-cancelled.png){width="300"}

>[!TAB CLI]

**So brechen Sie eine Aktivität in der Cloud-CLI ab**:

1. Identifizieren Sie die laufenden Aktivitäten und wählen Sie eine Aktivitäts-ID aus.

   ```bash
   magento-cloud activity:list --state=in_progress
   ```

1. Abbrechen der Aktivität mit der Aktivitäts-ID:

   ```bash
   magento-cloud activity:cancel wvl5wm7s5vkhy
   ```

>[!ENDTABS]

## Aktivitäts-Stream filtern

Die Möglichkeit, die Aktivitätsliste zu filtern, ist nützlich, wenn Sie nach einer bestimmten Aktivität suchen, z. B. nach einem Backup- oder einem Zusammenführungsereignis.

**So filtern Sie die Aktivitätenliste im[!DNL Cloud Console]**:

1. Wählen Sie eine Umgebung aus und wählen Sie die Aktivität aus **[!UICONTROL All]** anzeigen, um den vollständigen Ereignisverlauf einzuschließen.

1. Klicks ![Filtern nach](../../assets/icon-filterby.png){width="32"} und wählen Sie die **[!UICONTROL Filter by]** options:

   ![Aktivitäten filtern](../../assets/activity-filter.png)

1. Wählen Sie die Aktivität **[!UICONTROL Recent]** die Liste anzeigen und zurücksetzen.

## Stream mit Cloud CLI anzeigen

Die `magento-cloud` CLI bietet die meisten der gleichen Fähigkeiten wie die [!DNL Cloud Console]. Die `activity` -Befehl kann:

- `list` Aktivitätenstrom für eine Umgebung
- `get` Details zu einer bestimmten Aktivität
- anzeigen `log` für eine bestimmte Aktivität
- `cancel` eine Aktivität

**So zeigen Sie den Aktivitäts-Stream mit der Cloud-CLI an**:

1. Auflisten der Aktivitäten für die aktuelle Umgebung.

   ```bash
   magento-cloud activity:list
   ```

1. Jede Aktivität verfügt über eine eindeutige ID. Wählen Sie eine ID aus der vorherigen Liste aus und zeigen Sie die Details für diese Aktivität an.

   ```bash
   magento-cloud activity:get wvl5wm7s5vkhy
   ```

1. Zeigen Sie das vollständige Protokoll für diese Aktivität an.

   ```bash
   magento-cloud activity:log wvl5wm7s5vkhy
   ```

   Beispielantwort:

   ```bash
   Activity ID: wvl5wm7s5vkhy
   Type: environment.backup
   Description: User created a backup of Master
   Created: 2023-09-08T14:03:33+00:00
   State: complete
   Log:
   Creating backup of master
   Created backup eg5pu63egt2dcojkljalzjdopa
   ```
