---
title: Zugriff auf Ihr Commerce Admin-Bedienfeld
description: Erfahren Sie, wie Sie auf Ihr Commerce Admin-Bedienfeld zugreifen können.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Zugriff auf Ihr Commerce Admin-Bedienfeld

Benutzer, die über Administratorzugriff auf das Bedienfeld &quot;Commerce Admin&quot;verfügen, können Benutzer hinzufügen, Store-Dienste konfigurieren, die Einrichtung von Stores abschließen und Anpassungen vornehmen und vieles mehr.

Bei einem neuen Projekt besteht der erste Schritt nach Erhalt der Begrüßungs-E-Mail darin, den Administratorzugriff auf das Projekt zu sichern, indem das Kennwort im Lizenzeigentümer-Konto geändert wird. Der Standardbenutzername für dieses Konto ist die E-Mail-Adresse des Lizenzinhabers.

Sie können eine Kennwortänderungsanforderung mit einer der folgenden Methoden senden:

- Suchen Sie die Begrüßungs-E-Mail, die an die E-Mail-Adresse des Lizenzinhabers gesendet wird, folgen Sie dem Link und ändern Sie Ihr Kennwort.

- Kopieren Sie die Store-URL aus der [[!DNL Cloud Console]](../cloud-guide/project/overview.md) in einen Browser. Anschließend anhängen `/admin` an das Ende der URL, um die Anmeldeseite zu öffnen. Klicken Sie auf **Kennwort vergessen?** -Link, um eine Passwortänderungsanfrage an die E-Mail-Adresse des Lizenzinhabers zu senden.

Nachdem Sie die Kennwortänderungsanforderung gesendet haben, überprüfen Sie Ihre E-Mail auf die Benachrichtigung zum Zurücksetzen des Kennworts. Wenn Sie die E-Mail nicht erhalten, überprüfen Sie Ihren Spam-Ordner.

>[!TIP]
>
>Wenn das Zurücksetzen des Kennworts fehlschlägt oder Sie sich nicht im Admin-Bedienfeld anmelden können, kann ein Benutzer mit Administratorzugriff über SSH eine Verbindung zum Projekt herstellen und einen Admin-Benutzer über die `admin:user:create` CLI-Befehl. Siehe [Erstellen, Bearbeiten oder Entsperren eines Administratorkontos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) im _Installationshandbuch_.
