---
title: Benutzerdefinierte VCL zum Umgehen des Fastly-Cache
description: Fehlerbehebung beim Anforderungstraffic an den Herkunftsserver durch Erstellen eines benutzerdefinierten VCL-Snippets, um den Fastly-Cache zu umgehen.
feature: Cloud, Configuration, Cache
exl-id: a2e9dc57-9b5e-4716-9965-a4324442ad00
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Benutzerdefinierte VCL zum Umgehen des Fastly-Cache

Sie können ein benutzerdefiniertes VCL-Snippet erstellen, um den Fastly-Cache zu umgehen, damit Sie die Fehlerbehebung für den Anforderungs-Traffic auf dem Herkunftsserver durchführen können. Sie können beispielsweise ein Snippet erstellen, um festzustellen, ob Site-Probleme durch Caching verursacht werden, oder um Kopfzeilen zu beheben.

Sie können das Snippet so konfigurieren, dass es die schnelle Zwischenspeicherung für Anforderungen von einer bestimmten IP-Adresse oder URL umgeht.

>[!NOTE]
>
>Bevor Sie die benutzerdefinierte VCL-Konfiguration in einer Produktionsumgebung zusammenführen, sollten Sie den Code in der Staging-Umgebung testen.

**Voraussetzungen:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**So umgehen Sie den Fastly-Cache basierend auf IP-Adresse oder URL**:

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

1. Klicks **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `bypass_fastly`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - **VCL** Snippet-Inhalt —

     Das folgende Beispiel umgeht Fastly für eine bestimmte IP-Adresse:

     ```conf
     if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
       return(pass);
     }
     ```

     Das folgende Beispiel umgeht Fastly für ein bestimmtes URL-Muster:

     ```conf
     if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
     ```

     Verwenden Sie für eine exakte URL-Übereinstimmung den `==` Operator anstelle der `~` Operator. Siehe [Fastly VCL-Referenz] für Details.

1. Klicks **Erstellen**.

   ![Schnelles Umgehen des VCL-Codefragments](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. Nachdem die Seite neu geladen wurde, klicken Sie auf **VCL schnell hochladen** im *Schnelle Konfiguration* Abschnitt.

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

   Validiert die aktualisierte VCL-Version während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie Ihr benutzerdefiniertes VCL-Snippet, um Probleme zu beheben. Laden Sie dann die VCL erneut hoch.

Nachdem Sie das VCL-Snippet hinzugefügt haben, können Sie cURL-Befehle verwenden, um Anfragen von der angegebenen IP-Adresse oder URL an den Herkunftsserver zu senden, wie im folgenden Beispiel gezeigt:

```bash
curl -svo /dev/null www.example.com/index.html
```

Überprüfen Sie dann die Antwort, um Probleme mit nicht zwischengespeicherten Inhalten zu beheben.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!--External link definitions-->

[Fastly VCL-Referenz]: https://docs.fastly.com/vcl/
