---
title: Benutzerdefinierte VCL für das Zulassen von Anforderungen
description: Filtern Sie eingehende Anfragen und gewähren Sie den Zugriff nach IP-Adresse für Adobe Commerce-Sites durch eine Fastly Edge ACL-Liste und ein benutzerdefiniertes VCL-Snippet.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Benutzerdefinierte VCL für das Zulassen von Anforderungen

Sie können eine Fastly Edge ACL-Liste mit einem benutzerdefinierten VCL-Codeausschnitt verwenden, um eingehende Anforderungen zu filtern und den Zugriff nach IP-Adresse zuzulassen. Die ACL-Liste gibt die IP-Adressen an, die zugelassen werden sollen.

Erstellen Sie eine Zulassungsliste, um den Zugriff auf Ihre Staging-Umgebung zu beschränken, sodass nur Anforderungen von bestimmten IP-Adressen für interne Entwickler und genehmigte externe Dienste zulässig sind. Sie können auch eine Zulassungsliste erstellen, um den Zugriff auf die Admin in Staging- und Produktionsumgebungen zu sichern.

Das folgende Beispiel zeigt, wie ein benutzerdefiniertes VCL-Snippet mit einer [Fastly Access Control List (ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) , um den Zugriff auf den Admin für eine Adobe Commerce in der Cloud-Infrastruktur-Projektumgebung zu sichern. Wenn Sie das benutzerdefinierte VCL-Snippet zur Cloud-Umgebung hinzufügen, lässt Fastly nur Anfragen von IP-Adressen zu, die in der ACL enthalten sind.

>[!TIP]
>
>Verwenden Sie für Staging- und Integrationsumgebungen, die nicht öffentlich zugänglich sein sollten, die HTTP-Zugriffssteuerungsoption, die im [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) um den Zugriff auf die gesamte Site nach IP-Adresse zu verwalten.

**Voraussetzungen:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste der Client-IP-Adressen, die in die Zulassungsliste aufgenommen werden sollen

## Erstellen von Edge ACL für das Zulassen von Client-IP-Adressen

Edge-ACLs erstellen IP-Adresslisten für die Verwaltung des Zugriffs auf Ihre Site. In diesem Beispiel erstellen Sie eine Edge-ACL und fügen die Liste der Client-IP-Adressen hinzu, die für den Zugriff auf den Admin für Ihre Projektumgebung zugelassen sind.

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Edge ACL**.

1. Erstellen Sie den ACL-Container:

   - Klicks **ACL hinzufügen**.

   - Im *ACL-Container* Seite, geben Sie eine **ACL-Name**—`allowlist`.

   - Auswählen **Aktivieren nach der Änderung** , um Ihre Änderungen an der Version der von Ihnen bearbeiteten Fastly-Dienstkonfiguration bereitzustellen.

   - Klicks **Hochladen** , um die ACL an Ihre Fastly-Service-Konfiguration anzuhängen.

1. Fügen Sie die Liste der IP-Adressen hinzu, die auf den Admin zugreifen dürfen:

   - Klicken Sie auf das Symbol Einstellungen für `allowlist` ACL.

   - Hinzufügen und Speichern der *IP-Wert* für jede Client-IP-Adresse.

   - Klicks **Abbrechen** , um zur Systemkonfigurationsseite zurückzukehren.

1. Klicks **Konfiguration speichern**.

1. Aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

## Erstellen Sie ein benutzerdefiniertes VCL-Snippet, um den Administratorzugriff zu sichern.

Der folgende benutzerdefinierte VCL-Snippet-Code (JSON-Format) zeigt die Logik zum Filtern von Anforderungen an den Admin und zum Gewähren des Zugriffs, wenn die Client-IP-Adresse mit einer Adresse im `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Vorher [Erstellen eines benutzerdefinierten Snippets](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) Überprüfen Sie anhand dieses Beispiels die Werte, um festzustellen, ob Sie Änderungen vornehmen müssen. Geben Sie dann jeden Wert in die entsprechenden Felder ein, beispielsweise `type` in das Feld Typ `content` in das Feld Inhalt .

- `name` — Name für das VCL-Snippet. In diesem Beispiel `allowlist`.

- `priority` — Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität `5` , um sofort auszuführen und zu überprüfen, ob Admin-Anfragen von einer zulässigen IP-Adresse stammen. Das Snippet wird vor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type` — Gibt einen Speicherort an, an dem das Snippet in den versionierten VCL-Code eingefügt werden soll. Diese VCL ist ein `recv` Snippet-Typ , der den Snippet-Code zum `vcl_recv` Subroutine unterhalb des standardmäßigen Fastly VCL-Codes und über allen Objekten.

- `content` — Das auszuführende Codefragment von VCL. In diesem Beispiel filtert der Code Anforderungen an den Admin und ermöglicht den Zugriff, wenn die Client-IP-Adresse mit einer Adresse in der `allowlist` ACL. Wenn die Adresse nicht übereinstimmt, wird die Anfrage mit einer `403 Forbidden` Fehler.

  Wenn die URL für Ihren Administrator geändert wurde, ersetzen Sie den Beispielwert `/admin` mit der URL für Ihre Umgebung. Beispiel: `/company-admin`.

Im Codebeispiel wird die Bedingung `!req.http.Fastly-FF` ist bei Verwendung von [Origin Shielding](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Entfernen oder bearbeiten Sie diesen Code nicht.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin hinzu.](#add-the-custom-vcl-snippet). Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert [Fastly CDN-Modul für Magento 2 Version 1.2.58](fastly-configuration.md#upgrade) oder höher).

- Speichern Sie das JSON-Codebeispiel in einer -Datei (z. B. `allowlist.json`) und [Hochladen mit der Fastly-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

1. Klicks **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `allowlist`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - Fügen Sie die **VCL** Snippet-Inhalt:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Klicks **Erstellen** , um die VCL-Snippet-Datei mit dem Namensmuster zu generieren `type_priority_name.vcl`, beispielsweise `recv_5_allowlist.vcl`

1. Nachdem die Seite neu geladen wurde, klicken Sie auf **VCL schnell hochladen** im *Schnelle Konfiguration* -Abschnitt, um die Datei zur Konfiguration des Fastly-Dienstes hinzuzufügen.

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte Version des VCL-Codes während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie das benutzerdefinierte VCL-Snippet, um das Problem zu beheben. Laden Sie dann die VCL erneut hoch.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
