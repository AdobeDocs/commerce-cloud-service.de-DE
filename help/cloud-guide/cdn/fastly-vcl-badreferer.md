---
title: Blockverweis-Spam
description: Blockieren Sie Spam von Ihrer Site mit dem Fastly Edge-Wörterbuch und einem benutzerdefinierten VCL-Snippet.
feature: Cloud, Configuration, Security
exl-id: 665bac93-75db-424f-be2c-531830d0e59a
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Blockverweis-Spam

Das folgende Beispiel zeigt, wie Sie [Fastly Edge Dictionary](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) mit einem benutzerdefinierten VCL-Snippet konfigurieren, um Verweisspänen aus Ihrer Adobe Commerce auf der Cloud-Infrastruktur-Site zu blockieren.

>[!NOTE]
>
>Es wird empfohlen, benutzerdefinierte VCL-Konfigurationen zu einer Staging-Umgebung hinzuzufügen, in der Sie diese testen können, bevor Sie sie mit der Produktionsumgebung ausführen.

**Voraussetzungen:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Überprüfen Sie Ihre Site-Protokolle auf gefälschte Verweis-URLs und erstellen Sie eine Liste der Domänen, die blockiert werden sollen.

## Erstellen einer Referrer-Blockierungsliste

Edge-Wörterbücher erstellen Schlüssel-Wert-Paare, auf die VCL-Funktionen während der VCL-Snippet-Verarbeitung zugreifen können. In diesem Beispiel erstellen Sie ein Edge-Wörterbuch, das die Liste der zu blockierenden Referrer-Websites bereitstellt.

{{admin-login-step}}

1. Klicken Sie auf **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Schnellkonfiguration** > **Edge-Wörterbücher**.

1. Erstellen Sie den Wörterbuchcontainer:

   - Klicken Sie auf **Container hinzufügen**.

   - Geben Sie auf der Seite *Container* einen **Wörterbuchnamen**—`referrer_blocklist` ein.

   - Wählen Sie **Aktivieren nach der Änderung** aus, um Ihre Änderungen für die Version der von Ihnen bearbeiteten Fastly-Service-Konfiguration bereitzustellen.

   - Klicken Sie auf **Hochladen** , um das Wörterbuch an Ihre Konfiguration des Fastly-Dienstes anzuhängen.

1. Fügen Sie dem Wörterbuch `referrer_blocklist` die Liste der zu blockierenden Domänennamen hinzu:

   - Klicken Sie auf das Symbol Einstellungen für das Wörterbuch `referrer_blocklist` .

   - Fügen Sie Schlüssel-Wert-Paare hinzu und speichern Sie sie im neuen Wörterbuch. In diesem Beispiel ist jeder **Schlüssel** der Domänenname der zu blockierenden Referrer-URL und der **Wert** ist `true`.

     ![Schlechte Wörterbuchelemente des Referrers hinzufügen](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   - Klicken Sie auf **Abbrechen** , um zur Systemkonfigurationsseite zurückzukehren.

1. Klicken Sie auf **Konfiguration speichern**.

1. Aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Weitere Informationen zu Edge-Wörterbüchern finden Sie unter [Erstellen und Verwenden von Edge-Wörterbüchern](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) und [benutzerdefinierten VCL-Snippets](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) in der Schnelldokumentation.

## Erstellen eines benutzerdefinierten VCL-Snippets zum Blockieren von Werber-Spam

Der folgende benutzerdefinierte VCL-Codeausschnitt (JSON-Format) zeigt die Logik zum Überprüfen und Blockieren von Anforderungen. Das VCL-Snippet erfasst den Host einer Referrer-Website in einer Kopfzeile und vergleicht dann den Hostnamen mit der Liste der URLs im Wörterbuch `referrer_blocklist`. Wenn der Hostname übereinstimmt, wird die Anfrage mit einem `403 Forbidden` -Fehler blockiert.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "set req.http.Referer-Host = regsub(req.http.Referer, \"^https?:\/\/?([^:\/s]+).*$\", \"\\1\"); if (table.lookup(referrer_blocklist, req.http.Referer-Host)) { error 403 \"Forbidden\"; }"
}
```

Bevor Sie ein auf diesem Beispiel basierendes Snippet erstellen, überprüfen Sie die Werte, um festzustellen, ob Sie Änderungen vornehmen müssen:

- `name` - Name für das VCL-Snippet. Für dieses Beispiel haben wir `block_bad_referrer` verwendet.

- `dynamic` - Der Wert 0 zeigt ein [reguläres Snippet](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) an, das für die schnelle Konfiguration in das versionierte VCL hochgeladen werden soll.

- `priority` - Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität lautet &quot;`5`&quot;, um diesen Codeausschnitt auszuführen, bevor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen wird. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type` - Gibt einen Speicherort an, an dem das Snippet in die VCL-Version eingefügt werden soll. In diesem Beispiel ist das VCL-Snippet ein `recv` -Snippet. Wenn das Snippet in die VCL-Version eingefügt wird, wird es der UnterRoutine `vcl_recv` hinzugefügt, unter dem standardmäßigen Fastly VCL-Code und über allen Objekten.

- `content` - Das Snippet des VCL-Codes, der in einer Zeile ohne Zeilenumbrüche ausgeführt werden soll.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin](#add-the-custom-vcl-snippet) hinzu. Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert [schnelle Version 1.2.58](fastly-configuration.md#upgrade) oder höher.)

- Speichern Sie das JSON-Codebeispiel in eine Datei (z. B. `allowlist.json`) und laden Sie sie mit der Fastly API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api) hoch. [ Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicken Sie auf **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Klicken Sie auf **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `block_bad_referrer`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - **VCL** Snippet-Inhalt —

     ```conf
     set req.http.Referer-Host = regsub(req.http.Referer,
     "^https?://?([^:/\s]+).*$", "1");
     if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
       error 403 "Forbidden";
     }
     ```

1. Klicken Sie auf **Erstellen**.

   ![Erstellen eines benutzerdefinierten VCL-Codefragments für Referrer-Block](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. Klicken Sie nach dem Neuladen der Seite im Abschnitt *Schnelle Konfiguration* auf **VCL auf Fastly hochladen** .

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte VCL-Version während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie Ihr benutzerdefiniertes VCL-Snippet, um Probleme zu beheben. Laden Sie dann die VCL erneut hoch.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
