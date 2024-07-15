---
title: Anpassen von Fehler- und Wartungsseiten
description: Erfahren Sie, wie Sie die standardmäßige Fehlerseite anpassen können, die angezeigt wird, wenn Anforderungen an den Server mit raschem Ursprung fehlschlagen.
feature: Cloud, Configuration, Security
exl-id: 16722821-b928-4872-8cef-7f049e600f0d
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Anpassen von Fehler- und Wartungsseiten

Wenn eine Anfrage an den Fastly-Ursprung fehlschlägt, gibt Fastly Standardantwortseiten mit grundlegender Formatierung und allgemeiner Benachrichtigung zurück, die für Benutzer verwirrend sein können. Beispielsweise gibt Fastly die folgende standardmäßige Fehlerseite zurück, wenn eine Anfrage an die Fastly-Herkunft aufgrund eines 503-Fehlers fehlschlägt.

![Schnelle Standardfehlerseite](../../assets/cdn/fastly-503-example.png)

Sie können Ihre Adobe Commerce Store-Konfiguration aktualisieren, um einige standardmäßige Antwortseiten durch Seiten mit benutzerfreundlicheren Nachrichten und verbessertem HTML-Stil zu ersetzen, wie im folgenden Beispiel gezeigt.

![Schnell benutzerdefinierte Fehlerseite](../../assets/cdn/fastly-new-error-page.png)

Derzeit können Sie die folgenden Schnellantwortseiten für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anpassen.

- [Serverfehler - Interner Serverfehler, Zeitüberschreitung oder Ausfall der Site-Wartung (Fehlercode 500 oder höher)](#customize-the-503-error-page)
- [WAF-Blockierungsereignisse, die auftreten, wenn die WAF verdächtigen Anforderungs-Traffic erkennt (403 Verboten)](#customize-the-waf-error-page)

**HTML-Kodierungsanforderungen:**

Der HTML-Code für die benutzerdefinierte Seite muss die folgenden Anforderungen erfüllen:

- Der Inhalt kann bis zu 65.535 Zeichen enthalten.
- Geben Sie alle CSS-Inline-Elemente in der HTML-Quelle an.
- Bundle Bilder auf der HTML-Seite mit base64, damit sie auch dann angezeigt werden, wenn Fastly offline ist. Siehe [Daten-URIs auf der CSS-Tricks-Site](https://css-tricks.com/data-uris/).

## Anpassen der Fehlerseite 503

Kunden wird in den folgenden Fällen die standardmäßige 503-Fehlerseite angezeigt:

- Wenn eine Anfrage an den Fastly-Ursprung einen Antwortstatus von mehr als 500 zurückgibt
- Wenn die schnelle Herkunft ausfällt, z. B. eine Zeitüberschreitung, eine Wartungsaktivität oder Gesundheitsprobleme

Sie können die Standardseite anpassen, indem Sie den folgenden HTML-Code anpassen, um die Formatierung an Ihr Adobe Commerce Store-Design anzupassen, und den Titel und die Nachricht nach Bedarf ändern.

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
         <title>503</title>
   </head>
   <body>
      <p>Service unavailable</p>
   </body></html>
```

Stellen Sie sicher, dass die geänderte Quelle im Browser korrekt angezeigt wird. Fügen Sie dann den angepassten HTML-Code zur Schnellkonfiguration hinzu.

So fügen Sie der Fastly-Konfiguration die benutzerdefinierte Antwortseite hinzu:

{{admin-login-step}}

1. Wählen Sie **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie im rechten Bereich den Eintrag **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Benutzerdefinierte synthetische Seiten**.

   ![503-Fehlerseite bearbeiten](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Wählen Sie **HTML festlegen** aus.

1. Kopieren Sie den Quellcode für Ihre benutzerdefinierte Antwortseite und fügen Sie ihn in das HTML-Feld ein.

   ![503-Fehlerseite aktualisieren](../../assets/cdn/fastly-customize-503-response.png)

1. Wählen Sie oben auf der Seite die Option **Hochladen** aus, um die angepasste HTML-Quelle auf den Fastly-Server hochzuladen.

1. Wählen Sie oben auf der Seite **Konfiguration speichern** aus, um die aktualisierte Konfigurationsdatei zu speichern.

1. Aktualisieren Sie den Cache.

   - Wählen Sie in der Benachrichtigung oben auf der Seite den Link *Cache-Verwaltung* aus.

   - Wählen Sie auf der Seite &quot;Cachemanagement&quot;die Option **Magento-Cache leeren**.

## Anpassen der WAF-Fehlerseite

Kunden sehen die folgende standardmäßige WAF-Fehlerseite, wenn eine Anfrage an den Fastly-Ursprung mit einem `403 Forbidden` -Fehler fehlschlägt, der durch ein [WAF](fastly-waf-service.md) -Blockierungsereignis verursacht wird.

![WAF-Fehlerseite](../../assets/cdn/fastly-waf-403-error.png)

Das folgende Codebeispiel zeigt die HTML-Quelle für die Standardseite:

```html
<html>
  <head>
    <title>Magento 403 Forbidden</title>
  </head>
  <body>
    <p>The requested URL was rejected.</p>
    <p>For additional information, please contact support and provide this reference ID:</p>
    <p>"} req.http.x-request-id {"</p>
    <p><button onclick='history.back();'>Go Back</button></p>
  </body>
</html>
```

Sie können die Option **Benutzerdefinierte Synthetische Seiten** > **WAF-Seite bearbeiten** im Schnellkonfigurationsmenü verwenden, um den Standardcode für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anzupassen. Wenn Sie den Code bearbeiten, behalten Sie die folgende Zeile bei, die die Referenz-ID für das WAF-Blockierungsereignis bereitstellt:

```html
<p>"} req.http.x-request-id {"</p>
```

>[!NOTE]
>
>Die Option WAF bearbeiten ist nur verfügbar, wenn der Managed Cloud-WAF-Dienst für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur aktiviert ist.

**So bearbeiten Sie die WAF-Fehlerseite**:

1. [Melden Sie sich bei Admin an](../../get-started/onboarding.md#access-your-admin-panel).

1. Wählen Sie **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie im rechten Bereich den Eintrag **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Benutzerdefinierte synthetische Seiten**.

   ![WAF-Fehlerseitenoption bearbeiten](../../assets/cdn/fastly-custom-synthetic-pages-edit-waf.png)

1. Wählen Sie **WAF-Seite bearbeiten** aus.

1. Füllen Sie die Felder aus, um die HTML zu aktualisieren.

   ![Aktualisieren der WAF-Fehlerseite](../../assets/cdn/fastly-edit-waf-html.png)

   - **Status** - Wählen Sie den Status `403 Forbidden` aus.
   - **MIME type** - Typ `text/html`.
   - **Inhalt** - Bearbeiten Sie die standardmäßige HTML-Antwort, um benutzerdefiniertes CSS hinzuzufügen und den Titel und die Nachricht nach Bedarf zu aktualisieren.

1. Wählen Sie oben auf der Seite die Option **Hochladen** aus, um die angepasste HTML-Quelle auf den Fastly-Server hochzuladen.

1. Wählen Sie oben auf der Seite **Konfiguration speichern** aus, um die aktualisierte Konfigurationsdatei zu speichern.

1. Aktualisieren Sie den Cache.

   - Wählen Sie in der Benachrichtigung oben auf der Seite den Link **Cache-Verwaltung** aus.

   - Wählen Sie auf der Seite &quot;Cachemanagement&quot;die Option **Magento-Cache leeren**.

## Fehlerberichtsnummer anzeigen

Standardmäßig werden alle Adobe Commerce-Fehler schnell hinter dem Fehler *503 Dienst nicht verfügbar* verborgen. Um die Fehlerprotokollberichtnummer anzuzeigen, damit Sie die Fehlerdetails in den Protokollen finden und überprüfen können, öffnen Sie die Website, auf der die Schritte ausgelassen wurden:

1. Rufen Sie die IP-Adresse Ihres Stores ab:

   - Für Staging- und Produktionsumgebungen:

     ```bash
     nslookup {your_project_id}.ent.magento.cloud
     ```

   - Für Pro-Integrationsumgebungen und Starterumgebungen:

     ```bash
     nslookup gw.{your_region}.magentosite.cloud
     ```

1. Fügen Sie Ihre Anwendungsdomäne und IP-Adresse zur Hostdatei auf Ihrer lokalen Workstation hinzu:

   ```text
   {server_IP} {store_domain}
   ```

1. Löschen Sie den Browsercache und die Cookies (oder wechseln Sie in den Inkognito-Modus).

1. Öffnen Sie erneut Ihre Store-Website, um den Fehlercode anzuzeigen.

1. Verwenden Sie den Fehlercode, um die Details in der Fehlerberichtsdatei zu finden:

   - [Mit SSH eine Verbindung zur betroffenen Umgebung herstellen](../development/secure-connections.md#connect-to-a-remote-environment)

   - Suchen Sie die Datei &quot;`./var/report/{error_number}`&quot;.
