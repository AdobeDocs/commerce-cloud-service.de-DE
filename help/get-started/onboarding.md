---
title: '''[!DNL Onboarding] zu Commerce"'
description: Greifen Sie auf Ihr Cloud-Konto zu und richten Sie ein Adobe Commerce-Projekt zur Cloud-Infrastruktur ein.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] zu Commerce

Nach der Aktivierung eines Commerce-Abonnements für Cloud-Infrastruktur stehen das ursprüngliche Projekt und der Codezugriff nur der Person zur Verfügung, die als Lizenzinhaber (Kontoinhaber) bezeichnet wurde.

Der Lizenzinhaber ist die Person in Ihrem Unternehmens- oder Finanzunternehmen, die Zahlungen und andere geschäftsbezogene Transaktionen für das Adobe Commerce-Konto für Cloud-Infrastruktur verwaltet. Diese Person dient als Ansprechpartner für Adobe. Wenn Sie den Lizenzinhaber in Ihrem Konto ändern müssen, wenden Sie sich an Ihr Adobe Account Team.

Um Ihr Projekt schnell zu integrieren und damit Sie mit der Entwicklung Ihrer Site für die Live-Bereitstellung beginnen können, müssen Sie die erforderliche Einrichtung abschließen und [!DNL onboarding] Aufgaben. In der Regel startet der Lizenzinhaber den Prozess, indem er den Administratorzugriff sichert und technische Admin-Benutzer erstellt, die bei der Einrichtung, Anpassung und Entwicklungsarbeit helfen können.

## Für ein Cloud-Konto anmelden

Wenn Sie kein Adobe Commerce-Konto für die Cloud-Infrastruktur haben, wenden Sie sich an [Vertrieb]. Wenn Sie sich anmelden, erstellt Adobe Ihr Konto und sendet Ihnen eine Begrüßungs-E-Mail mit Anweisungen zum Zugriff auf die Projektoberfläche. Die E-Mail enthält einen Link, über den Sie sich bei Ihrem Konto anmelden und Ihre erste Projekteinrichtung abschließen können.

### Cloud [!DNL Onboarding] Benutzeroberfläche

Die Seite Adobe Commerce on Cloud Infrastructure Project im[!DNL Onboarding] UI) bietet eine Checkliste für die ersten Schritte, um Ihr Projekt und Ihre Dienste einzurichten, den Zugriff zu bestimmen und mit der Entwicklung zu beginnen. Im OBUI haben Sie folgende Möglichkeiten:

- Fügen Sie einen technischen Administrator hinzu, einen Superuser, der Ihr Projekt und Ihre Verzweigungen verwalten kann.
- Zugriff auf Ihre Projektumgebung, einschließlich eines Links zum [!DNL Cloud Console]
- Führen Sie eine schnelle Benutzerakzeptanztest-Checkliste mit Links zu weiteren Tests durch.

**Öffnen der Projektseite**:

1. Melden Sie sich bei Ihrer [Adobe Commerce-Kundenkonto](https://account.magento.com/customer/account/login).

1. Im _Mein Konto_ klicken Sie auf die **[!UICONTROL Commerce]** , um die Projekte in Ihrem Konto anzuzeigen.

1. Klicks **Projektseite anzeigen** im [Abschnitt &quot;Projekte&quot;](https://cloud.magento.com/cloud/project/).

1. Klicken Sie auf den Projektnamen und öffnen Sie die Seite Cloud-Projekt ([!DNL Onboarding] Benutzeroberfläche).

   ![OBUI-Projektseite](../assets/onboarding-ui.png)

   Durchsuchen Sie das Portal nach hilfreichen Informationen und Optionen, um mit der Planung Ihres Projekts, der Entwicklung von Code und der Vorbereitung auf UAT und Site-Launch zu beginnen.

## Projekt aufrufen und Benutzer hinzufügen

Der Lizenzinhaber kann Benutzerkonten hinzufügen, um den Zugriff auf Code zu ermöglichen, Zweige zu verwalten, Tickets einzugeben und Umgebungen zu unterstützen. Diese Benutzerkonten können interne Entwicklungs-, Berater- und Lösungsspezialisten umfassen.

Normalerweise ist der einzige Benutzer, den der Lizenzinhaber erstellen muss, der _Technischer Administrator_. Der technische Administrator benötigt ein Benutzerkonto mit Administratorzugriff, um Benutzerkonten für Entwickler zu erstellen, Umgebungsberechtigungen festzulegen und alle Zweige und Umgebungen zu verwalten. Der technische Administrator kann ein Entwickler, ein Berater, ein [Adobe Solution Partner](https://business.adobe.com/products/magento/partners.html)oder Sie selbst.

Sie können einen technischen Administrator über das Projektportal erstellen, indem Sie über das [!DNL Cloud Console]oder über die Befehlszeile mit der `magento-cloud` CLI.

### Benutzerregistrierung

Sie können Ihrer Adobe Commerce nur registrierte Benutzer für Cloud-Infrastrukturprojekte und -Umgebungen hinzufügen. Wenn Sie einen neuen Benutzer haben, bitten Sie ihn, [sich für ein Konto registrieren](https://account.magento.com/customer/account/login/) und geben Sie die mit ihrem Kontoprofil verknüpfte E-Mail-Adresse an.

### Zugriff auf freigegebene Konten

Der Lizenzinhaber kann den freigegebenen Zugriff für das Konto einrichten. Mit dem freigegebenen Zugriff können vertrauenswürdige Mitarbeiter und Dienstleister das Help Center zum Senden und Verfolgen von Support-Tickets für Ihre Adobe Commerce in Cloud-Infrastrukturprojekten verwenden. Anweisungen zum Einrichten finden Sie in der [Freigegebener Zugriff] Artikel im Hilfezentrum.

### [!DNL Cloud Console]

Sie können die [[!DNL Cloud Console]](cloud-console.md) , um Ihr Projekt zu verwalten, Benutzerkonten hinzuzufügen und mit der Entwicklung Ihres Stores zu beginnen. Lizenzinhaber, Benutzer technischer Administratoren und Entwickler können die [!DNL Cloud Console] um alle Umgebungen und Verzweigungen, Umgebungsvariablen, Umgebungseinstellungen und Routen zu verwalten.

**So greifen Sie auf die[!DNL Cloud Console]**:

1. Anmelden bei [Mein Konto](https://account.magento.com/customer/account/login).

1. Im _Mein Konto_ klicken Sie auf die **[!UICONTROL Commerce]** , um die Projekte in Ihrem Konto anzuzeigen.

1. Klicken Sie auf **Projekte** und wählen Sie ein Projekt aus.

1. Klicks **Zugang zur Infrastruktur** und klicken Sie anschließend auf **Projektzugriff (Web-Benutzeroberfläche)**.

   ![Cloud-Projektportal](../assets/obui-project-access.png)

## Für Adobe-Status anmelden

Hier erhalten Sie Informationen zu Adobe Commerce in Cloud-Infrastrukturplattformumgebungen und zugehörigen Diensten. [Statusseite].

Die Seite bietet einen Status für Adobe Commerce-Komponenten und -Dienste, gefolgt von Benachrichtigungen zu Vorfällen, Service-Upgrades, geplanten Ausfällen und geplanter Wartung. Jeder, der an Ihrem Projekt arbeitet, kann die Adobe Commerce-Status-Site abonnieren, um Ereignisbenachrichtigungen und -aktualisierungen per E-Mail oder Slack zu erhalten. Sie können Ihr Adobe-Status-Abonnement anpassen, um bestimmte-Produkte nach Regionen und Ereignissen zu verfolgen.

>[!TIP]
>
> Öffnen Sie das neue [!DNL Cloud Console] sowie Projekt- und Umgebungsaktivitäten anzeigen.
>
>**Nächster Schritt**: [Melden Sie sich bei der Cl[!DNL ]oud Console an](cloud-console.md)

<!-- link definitions -->

[Vertrieb]: https://business.adobe.com/products/magento/get-demo.html
[Freigegebener Zugriff]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Statusseite]: https://status.adobe.com/products/503473
