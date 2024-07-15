---
title: Benutzerdefinierte VCL für das Zulassen von Anforderungen
description: Filtern Sie eingehende Anfragen und erlauben Sie den Zugriff nach IP-Adresse für Adobe Commerce-Sites mit einer Fastly Edge ACL-Liste und einem benutzerdefinierten VCL-Snippet.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Benutzerdefinierte VCL für das Zulassen von Anforderungen

Sie können eine Fastly Edge ACL-Liste mit einem benutzerdefinierten VCL-Codefragment verwenden, um eingehende Anfragen zu filtern und den Zugriff nach IP-Adresse zuzulassen. Die ACL-Liste gibt die IP-Adressen an, die zugelassen werden sollen.

Erstellen Sie eine Zulassungsliste, um den Zugriff auf Ihre Staging-Umgebung zu beschränken, sodass nur Anforderungen von bestimmten IP-Adressen für interne Entwickler und genehmigte externe Dienste zulässig sind. Sie können auch eine Zulassungsliste erstellen, um den Zugriff auf die Admin in Staging- und Produktionsumgebungen zu sichern.

Im folgenden Beispiel wird gezeigt, wie ein benutzerdefiniertes VCL-Snippet mit einer [Fastly Access Control List (ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) verwendet wird, um den Zugriff auf den Admin für eine Adobe Commerce in der Cloud-Infrastruktur-Projektumgebung zu sichern. Wenn Sie das benutzerdefinierte VCL-Snippet zur Cloud-Umgebung hinzufügen, lässt Fastly nur Anfragen von IP-Adressen zu, die in der ACL enthalten sind.

>[!TIP]
>
>Verwenden Sie für Staging- und Integrationsumgebungen, die nicht öffentlich zugänglich sein sollten, die in [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) verfügbare Option HTTP-Zugriffskontrolle , um den Zugriff auf die gesamte Site nach IP-Adresse zu verwalten.

**Voraussetzungen:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste der Client-IP-Adressen, die in die Zulassungsliste aufgenommen werden sollen

## Erstellen einer Edge ACL für die Zulassung von Client-IP-Adressen

Edge ACLs erstellen IP-Adresslisten zum Verwalten des Zugriffs auf Ihre Site. In diesem Beispiel erstellen Sie eine Edge-ACL und fügen die Liste der Client-IP-Adressen hinzu, die für den Zugriff auf den Admin für Ihre Projektumgebung zugelassen sind.

{{admin-login-step}}

1. Klicken Sie auf **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Edge ACL**.

1. Erstellen Sie den ACL-Container:

   - Klicken Sie auf **ACL hinzufügen**.

   - Geben Sie auf der Seite *ACL-Container* einen **ACL-Namen**—`allowlist` ein.

   - Wählen Sie **Aktivieren nach der Änderung** aus, um Ihre Änderungen für die Version der von Ihnen bearbeiteten Fastly-Service-Konfiguration bereitzustellen.

   - Klicken Sie auf **Hochladen** , um die ACL an Ihre Fastly-Service-Konfiguration anzuhängen.

1. Fügen Sie die Liste der IP-Adressen hinzu, die auf den Admin zugreifen dürfen:

   - Klicken Sie auf das Symbol Einstellungen für die ACL `allowlist` .

   - Fügen Sie den *IP-Wert* für jede Client-IP-Adresse hinzu und speichern Sie ihn.

   - Klicken Sie auf **Abbrechen** , um zur Systemkonfigurationsseite zurückzukehren.

1. Klicken Sie auf **Konfiguration speichern**.

1. Aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

## Erstellen Sie ein benutzerdefiniertes VCL-Snippet, um den Administratorzugriff zu sichern.

Der folgende benutzerdefinierte VCL-Codeausschnitt (JSON-Format) zeigt die Logik zum Filtern von Anforderungen an den Admin und zum Gewähren des Zugriffs, wenn die Client-IP-Adresse mit einer Adresse in der ACL `allowlist` übereinstimmt.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Bevor Sie [ein benutzerdefiniertes Snippet erstellen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) aus diesem Beispiel, überprüfen Sie die Werte, um festzustellen, ob Sie Änderungen vornehmen müssen. Geben Sie dann jeden Wert in die entsprechenden Felder ein, z. B. `type` in das Feld Typ und `content` in das Feld Inhalt .

- `name` - Name für das VCL-Snippet. In diesem Beispiel `allowlist`.

- `priority` - Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität lautet &quot;`5`&quot;, um sofort auszuführen und zu überprüfen, ob Admin-Anfragen von einer zulässigen IP-Adresse stammen. Das Snippet wird ausgeführt, bevor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen wurde. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type` - Gibt einen Speicherort an, an dem das Snippet in den versionierten VCL-Code eingefügt werden soll. Dieser VCL ist ein `recv` -Snippet-Typ, der den Codeausschnitt zur UnterRoutine `vcl_recv` unterhalb des standardmäßigen Fastly VCL-Codes und über allen Objekten hinzufügt.

- `content` - Das auszuführende Codefragment von VCL. In diesem Beispiel filtert der Code Anforderungen an den Admin und ermöglicht den Zugriff, wenn die Client-IP-Adresse mit einer Adresse in der ACL `allowlist` übereinstimmt. Wenn die Adresse nicht übereinstimmt, wird die Anfrage mit dem Fehler `403 Forbidden` blockiert.

  Wenn die URL für Ihren Administrator geändert wurde, ersetzen Sie den Beispielwert `/admin` durch die URL für Ihre Umgebung. Beispiel: `/company-admin`.

Im Codebeispiel ist die Bedingung `!req.http.Fastly-FF` bei der Verwendung von [Origin Shielding](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding) wichtig. Entfernen oder bearbeiten Sie diesen Code nicht.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin](#add-the-custom-vcl-snippet) hinzu. Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert das [schnelle CDN-Modul für Magento 2 Version 1.2.58](fastly-configuration.md#upgrade) oder höher.)

- Speichern Sie das JSON-Codebeispiel in eine Datei (z. B. `allowlist.json`) und laden Sie sie mit der Fastly API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api) hoch. [ Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicken Sie auf **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Klicken Sie auf **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `allowlist`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - Fügen Sie den Codeausschnitt-Inhalt **VCL** hinzu:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Klicken Sie auf **Erstellen** , um die VCL-Snippet-Datei mit dem Namensmuster `type_priority_name.vcl` zu generieren, z. B. `recv_5_allowlist.vcl`

1. Klicken Sie nach dem Neuladen der Seite im Abschnitt *Schnelle Konfiguration* auf **VCL auf Fastly hochladen** , um die Datei zur Konfiguration des Fastly-Dienstes hinzuzufügen.

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte Version des VCL-Codes während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie das benutzerdefinierte VCL-Snippet, um das Problem zu beheben. Laden Sie dann die VCL erneut hoch.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
