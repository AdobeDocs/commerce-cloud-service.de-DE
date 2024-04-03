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

Das folgende Beispiel zeigt, wie Sie [Schnelles Edge-Wörterbuch](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) mit einem benutzerdefinierten VCL-Snippet zum Blockieren von Verweisen von Spam von Ihrer Adobe Commerce auf der Cloud-Infrastruktur-Site.

>[!NOTE]
>
>Es wird empfohlen, benutzerdefinierte VCL-Konfigurationen zu einer Staging-Umgebung hinzuzufügen, in der Sie diese testen können, bevor Sie sie mit der Produktionsumgebung ausführen.

**Voraussetzungen:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Überprüfen Sie Ihre Site-Protokolle auf gefälschte Verweis-URLs und erstellen Sie eine Liste der Domänen, die blockiert werden sollen.

## Erstellen einer Referrer-Blockierungsliste

Edge-Wörterbücher erstellen Schlüssel-Wert-Paare, auf die VCL-Funktionen während der VCL-Snippet-Verarbeitung zugreifen können. In diesem Beispiel erstellen Sie ein Edge-Wörterbuch, das die Liste der zu blockierenden Referrer-Websites bereitstellt.

{{admin-login-step}}

1. Klicks **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Edge-Wörterbücher**.

1. Erstellen Sie den Wörterbuchcontainer:

   - Klicks **Container hinzufügen**.

   - Im *Container* Seite, geben Sie eine **Wörterbuchname**—`referrer_blocklist`.

   - Auswählen **Aktivieren nach der Änderung** , um Ihre Änderungen an der Version der von Ihnen bearbeiteten Fastly-Dienstkonfiguration bereitzustellen.

   - Klicks **Hochladen** , um das Wörterbuch an Ihre Fastly-Service-Konfiguration anzuhängen.

1. Fügen Sie die Liste der Domänennamen hinzu, die dem `referrer_blocklist` Wörterbuch:

   - Klicken Sie auf das Symbol Einstellungen für `referrer_blocklist` Wörterbuch.

   - Fügen Sie Schlüssel-Wert-Paare hinzu und speichern Sie sie im neuen Wörterbuch. In diesem Beispiel wird jeder **Schlüssel** ist der Domänenname einer Referrer-URL, die blockiert werden soll, und **Wert** is `true`.

     ![Schlechte Wörterbuchelemente für Referrer hinzufügen](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   - Klicks **Abbrechen** , um zur Systemkonfigurationsseite zurückzukehren.

1. Klicks **Konfiguration speichern**.

1. Aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Weitere Informationen zu Edge-Wörterbüchern finden Sie unter [Erstellen und Verwenden von Edge-Wörterbüchern](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) und [benutzerdefinierte VCL-Snippets](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) in der Fastly-Dokumentation.

## Erstellen eines benutzerdefinierten VCL-Snippets zum Blockieren von Werber-Spam

Der folgende benutzerdefinierte VCL-Codeausschnitt (JSON-Format) zeigt die Logik zum Überprüfen und Blockieren von Anforderungen. Das VCL-Snippet erfasst den Host einer Referrer-Website in einer Kopfzeile und vergleicht dann den Hostnamen mit der Liste der URLs in der `referrer_blocklist` Wörterbuch. Wenn der Hostname übereinstimmt, wird die Anfrage mit einem `403 Forbidden` Fehler.

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

- `name` — Name für das VCL-Snippet. In diesem Beispiel haben wir `block_bad_referrer`.

- `dynamic` — Wert 0 zeigt eine [reguläres Snippet](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) , um für die Fastly-Konfiguration auf die versionierte VCL hochzuladen.

- `priority` — Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität `5` , um diesen Codeausschnitt vor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type` — Gibt einen Speicherort an, an dem das Snippet in die VCL-Version eingefügt werden soll. In diesem Beispiel ist das VCL-Snippet ein `recv` Snippet. Wenn das Snippet in die VCL-Version eingefügt wird, wird es der `vcl_recv` subroutinemäßig unter dem standardmäßigen Fastly VCL-Code und über allen Objekten.

- `content` — Der Codeausschnitt von VCL, der in einer Zeile ohne Zeilenumbrüche ausgeführt werden soll.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin hinzu.](#add-the-custom-vcl-snippet). Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert [Schnelle Version 1.2.58](fastly-configuration.md#upgrade) oder höher).

- Speichern Sie das JSON-Codebeispiel in einer -Datei (z. B. `allowlist.json`) und [Hochladen mit der Fastly-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

1. Klicks **Benutzerdefiniertes Snippet erstellen**.

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

1. Klicks **Erstellen**.

   ![Erstellen eines benutzerdefinierten VCL-Codefragments für Referrer-Block](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. Nachdem die Seite neu geladen wurde, klicken Sie auf **VCL schnell hochladen** im *Schnelle Konfiguration* Abschnitt.

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte VCL-Version während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie Ihr benutzerdefiniertes VCL-Snippet, um Probleme zu beheben. Laden Sie dann die VCL erneut hoch.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
