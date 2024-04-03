---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Datei zum Ändern benutzerdefinierter VCL für Fastly einschließen

## Ändern des benutzerdefinierten VCL-Snippets

1. [Anmelden](/help/get-started/onboarding.md#access-your-admin-panel) an den Administrator.

1. Klicks **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

   ![Verwalten benutzerdefinierter VCL-Snippets](/help/assets/cdn/fastly-manage-snippets.png)

1. Im _Aktion_ klicken Sie auf das Einstellungssymbol neben dem zu bearbeitenden Snippet.

1. Nachdem die Seite neu geladen wurde, klicken Sie auf **VCL schnell hochladen** im _Schnelle Konfiguration_ Abschnitt.

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

>[!WARNING]
>
>Die _Benutzerdefinierte VCL-Snippets_ UI-Option zeigt nur die Snippets an, die über den Adobe Commerce Admin hinzugefügt wurden. Wenn Sie Snippets mit der Fastly-API hinzufügen, verwenden Sie die API zu [verwalten](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
