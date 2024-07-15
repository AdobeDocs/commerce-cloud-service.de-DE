---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Datei zum Ändern benutzerdefinierter VCL für Fastly einschließen

## Ändern des benutzerdefinierten VCL-Snippets

1. [Melden Sie sich bei ](/help/get-started/onboarding.md#access-your-admin-panel) beim Administrator an.

1. Klicken Sie auf **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

   ![Verwalten benutzerdefinierter VCL-Snippets](/help/assets/cdn/fastly-manage-snippets.png)

1. Klicken Sie in der Spalte _Aktion_ auf das Einstellungssymbol neben dem zu bearbeitenden Snippet.

1. Klicken Sie nach dem Neuladen der Seite im Abschnitt _Schnelle Konfiguration_ auf **VCL auf Fastly hochladen** .

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

>[!WARNING]
>
>Die UI-Option _Benutzerdefinierte VCL-Snippets_ zeigt nur die Snippets an, die über den Adobe Commerce-Administrator hinzugefügt wurden. Wenn Sie Snippets mit der Fastly API hinzufügen, verwenden Sie die API, um [sie zu verwalten](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
