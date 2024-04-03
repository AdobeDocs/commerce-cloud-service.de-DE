---
title: "Melden Sie sich bei [!DNL Cloud Console]"
description: Informationen zum [!DNL Cloud Console] für Adobe Commerce in Cloud-Infrastruktur.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Anmelden bei [!DNL Cloud Console]

Die [!DNL Cloud Console] bietet interaktive Methoden zum Erstellen, Verwalten und Bereitstellen von Commerce-Code. Die [!DNL Cloud Console] ist ein moderneres, benutzerfreundlicheres Erlebnis und bildet die Grundlage für zukünftige Verbesserungen der Benutzeroberfläche.

[Melden Sie sich bei [!DNL Cloud Console]](https://console.adobecommerce.com) , um Ihre Projektliste anzuzeigen.

![Projektliste](../assets/ui-allprojects-list.png)

## Funktionen

Zu den neuen oder verbesserten Funktionen gehören:

- Klare Übersicht über Projekt- und Umgebungsmerkmale
- Aktivitäts-Stream mit sortierbarem Verlauf
- Manuelles Backup-Management und -Verlauf für Starter-Projekte
- Erweiterte Protokollansichten
- Sortierbare Listen
- Einfache Formulare und Anleitungen zum Hinzufügen von Integrationen
- Einhaltung der Web Content Accessibility Guidelines (WCAG)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

Die neuen oder verbesserten Funktionen sind wie folgt:

| Funktion | Verbesserungen |
| -------------- | ----------------------------------- |
| [Aktivitäts-Stream](../cloud-guide/project/activity-stream.md) | Interagieren Sie mit einer sortierbaren Liste laufender, ausstehender oder historischer Aktionen. Wählen Sie eine Aktivität aus und zeigen Sie Protokolle an oder brechen Sie einen laufenden Build ab. |
| [Projekt- und Umgebungsübersichten](../cloud-guide/project/overview.md#project-overview) | Öffnen Sie Ihr Projekt und sehen Sie sich die Übersicht über die Projektdetails und die Umgebungsliste an. Die Umgebungsübersicht bietet weitere Details zum Umgebungsstatus, zum Anwendungszugriff und zu den letzten Aktivitäten. |
| [Integrationsformulare](../cloud-guide/integrations/overview.md) | Verwenden Sie einfache Formulare und Anleitungen, um Integrationen hinzuzufügen, wie z. B. Bitbucket- oder Slack-Benachrichtigungen. |
| [Projektliste](../cloud-guide/project/overview.md#cloud-console) | Die _Alle Projekte_ -Ansicht listet alle Projekte auf, auf die Sie Zugriff haben. Sie können auf **[!UICONTROL Show filters]** und filtern Sie Ihre Projektliste nach Typ, Region oder Plan. |
| [Sichtbarkeitsoptionen für Variablen](../cloud-guide/environment/variable-levels.md) | Beschränken Sie die Sichtbarkeit einer Variablen auf Projekt- oder Umgebungsebene während der Build- oder Laufzeit. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Konsolenfragen

**_Wo finde ich die Snapshots-Funktion?_**?

Für [!DNL Starter] Projekte, heißt die Snapshots-Funktion jetzt _Backups_. Sie können eine manuelle Sicherung Ihrer [!DNL Starter] -Umgebung aus [!DNL Cloud Console] oder erstellen Sie einen Schnappschuss aus der Cloud-CLI. Sie müssen über eine Administratorrolle für die Umgebung verfügen.

Wählen Sie in der Projektnavigationsleiste eine Umgebung aus. Die Umgebung muss aktiv sein. Wählen Sie die **[!UICONTROL Backups]** Registerkarte. Diese Option ist derzeit nicht für Pro-Umgebungen verfügbar.

**_Wobei die Liste der konfigurierten Routen für die Umgebung ist_**?

Die Liste der konfigurierten Routen finden Sie auf der _Dienste_ für eine Umgebung.

Wählen Sie in der Projektnavigationsleiste eine Umgebung aus. Wählen Sie die **[!UICONTROL Services]** Registerkarte. Die **Router** -Übersicht zeigt die konfigurierten Routen an. Derzeit können Sie keine Route aus dem neuen [!DNL Cloud Console].

## Kontomenü

In der oberen rechten Ecke finden Sie Ihr Kontomenü. Klicken Sie auf den Abwärtspfeil für das Menü und wählen Sie **[!UICONTROL My Profile]**. Im _Mein Profil_ anzeigen, können Sie Ihre Benutzerdetails und Anzeigeeinstellungen steuern, [Sicherheitsauthentifizierung](../cloud-guide/project/user-access.md#user-authentication-requirements), [API-Token](../cloud-guide/project/user-access.md#create-an-api-token), und [SSH-Schlüssel](../cloud-guide/development/secure-connections.md).
