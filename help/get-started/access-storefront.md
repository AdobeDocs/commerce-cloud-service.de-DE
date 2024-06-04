---
title: Zugriff auf Ihr Commerce Admin-Bedienfeld
description: Erfahren Sie, wie Sie auf Ihr Commerce Admin-Bedienfeld zugreifen können.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 3ca09243dc0a714c1d86cccf9f0620a8a39fd1e1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Zugriff auf Ihr Commerce Admin-Bedienfeld

Benutzer, die über Administratorzugriff auf das Commerce Admin-Bedienfeld verfügen, können Benutzer hinzufügen, Store-Dienste konfigurieren, die Einrichtung von Stores und die Anpassung abschließen und vieles mehr.

Bei einem neuen Projekt besteht der erste Schritt nach Erhalt der Begrüßungs-E-Mail darin, den Administratorzugriff auf das Projekt zu sichern, indem das Kennwort im Lizenzeigentümer-Konto geändert wird. Der Standardbenutzername für dieses Konto ist die E-Mail-Adresse des Lizenzinhabers.

Sie können eine Kennwortänderungsanforderung mit einer der folgenden Methoden senden:

- Suchen Sie die Begrüßungs-E-Mail, die an die E-Mail-Adresse des Lizenzinhabers gesendet wird, folgen Sie dem Link und ändern Sie Ihr Kennwort.

- Kopieren Sie die Store-URL aus der [[!DNL Cloud Console]](../cloud-guide/project/overview.md) in einen Browser. Anschließend anhängen `/admin` an das Ende der URL, um die Anmeldeseite zu öffnen. Klicken Sie auf **Kennwort vergessen?** -Link, um eine Passwortänderungsanfrage an die E-Mail-Adresse des Lizenzinhabers zu senden.

Nachdem Sie die Kennwortänderungsanforderung gesendet haben, überprüfen Sie Ihre E-Mail auf die Benachrichtigung zum Zurücksetzen des Kennworts. Wenn Sie die E-Mail nicht erhalten, überprüfen Sie Ihren Spam-Ordner.

>[!TIP]
>
>Wenn das Zurücksetzen des Kennworts fehlschlägt oder Sie sich nicht im Admin-Bedienfeld anmelden können, kann ein Benutzer mit Administratorzugriff über SSH eine Verbindung zum Projekt herstellen und einen Admin-Benutzer über die `admin:user:create` CLI-Befehl. Siehe [Erstellen, Bearbeiten oder Entsperren eines Administratorkontos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) im _Installationshandbuch_.

## Überwachen des Site-Zustands

Die [Site-weites Analyse-Tool](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) ist ein proaktives Self-Service-Tool und zentrales Repository mit detaillierten Systemeinblicken und Empfehlungen, um die Sicherheit und Bedienbarkeit Ihrer Adobe Commerce-Installation sicherzustellen. Es bietet rund um die Uhr eine Leistungsüberwachung, Berichte und Beratung in Echtzeit, um potenzielle Probleme zu identifizieren und bessere Sichtbarkeit in Bezug auf Gesundheit, Sicherheit und Anwendungskonfigurationen der Website zu erreichen. Dies trägt zur Verkürzung der Auflösungszeit und zur Verbesserung der Site-Stabilität und -Leistung bei. Sie können das Site-weite Analyse-Tool direkt über die [Admin-Bereich](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-2-logging-in-to-your-site-wide-analysis-tool-dashboard-from-your-stores-admin-panel) oder von [dedizierte Domäne](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-1-logging-in-to-your-site-wide-analysis-tool-dashboard-directly-from-the-site-wide-analysis-tool-domain-for-adobe-commerce-on-cloud-infrastructure-only) (Adobe Commerce nur für Cloud-Infrastrukturprojekte).
