---
source-git-commit: 8f1ed3067f6daed897151052c8b9f987d3df3a50
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---
# Datei zum Löschen benutzerdefinierter VCL für Fastly einschließen

## Löschen des benutzerdefinierten VCL-Snippets

1. [Anmelden](/help/get-started/onboarding.md#access-your-admin-panel) an den Administrator.

1. Klicks **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

   ![Verwalten benutzerdefinierter VCL-Snippets](/help/assets/cdn/fastly-manage-snippets.png)

1. Im _Aktion_ auf das Papierkorbsymbol neben dem zu löschenden Snippet klicken.

1. Klicken Sie im nächsten modalen Fenster auf **DELETE** und aktivieren Sie eine neue Version.

>[!WARNING]
>
>Die _Benutzerdefinierte VCL-Snippets_ UI-Option zeigt nur die Snippets an, die über den Adobe Commerce Admin hinzugefügt wurden. Wenn Sie Snippets mit der Fastly-API hinzufügen, verwenden Sie die API zu [verwalten](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-vcl-using-the-api).
