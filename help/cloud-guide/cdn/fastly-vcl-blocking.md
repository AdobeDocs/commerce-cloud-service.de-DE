---
title: Benutzerdefinierte VCL für das Blockieren von Anforderungen
description: Blockieren eingehender Anfragen nach IP-Adresse mithilfe einer Edge Access Control List (ACL) mit einem benutzerdefinierten VCL-Snippet.
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 0e9ace747cc56808108781e42b97c86756089818
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# Benutzerdefinierte VCL für das Blockieren von Anforderungen

Sie können das Fastly CDN-Modul für Magento 2 verwenden, um eine Edge-ACL mit einer Liste von IP-Adressen zu erstellen, die Sie blockieren möchten. Anschließend können Sie diese Liste mit einem VCL-Snippet verwenden, um eingehende Anfragen zu blockieren. Der Code überprüft die IP-Adresse der eingehenden Anfrage. Wenn es mit einer IP-Adresse übereinstimmt, die in der ACL-Liste enthalten ist, blockiert die Anfrage schnell den Zugriff auf Ihre Site und gibt eine `403 Forbidden error`. Der Zugriff auf alle anderen Client-IP-Adressen ist zulässig.

**Voraussetzungen:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste der zu blockierenden Client-IP-Adressen

## Erstellen von Edge ACL zum Blockieren von Client-IP-Adressen

Sie erstellen eine Edge-ACL, um die Liste der zu blockierenden IP-Adressen zu definieren. Nachdem Sie die ACL erstellt haben, können Sie sie in einem benutzerdefinierten VCL-Snippet verwenden, um den Zugriff auf Ihre Staging- oder Produktions-Site zu verwalten.

Verwalten Sie den Zugriff für Staging- und Produktions-Sites, indem Sie die Edge-ACL mit demselben Namen in beiden Umgebungen erstellen. Der VCL-Snippet-Code gilt für beide Umgebungen.

1. Melden Sie sich beim Administrator an.
1. Navigieren Sie zu **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** > **Vollständiger Seiten-Cache** > **Schnelle Konfiguration**.
1. Erweitern Sie die **Edge ACL** Abschnitt.
1. Klicks **ACL hinzufügen** , um eine Liste zu erstellen. Nennen Sie für dieses Beispiel die Liste &quot;Blockierungsliste&quot;.
1. Geben Sie IP-Adresswerte in die Liste ein. Alle Client-IP-Adressen, die dieser Liste hinzugefügt wurden, werden blockiert und können nicht auf die Site zugreifen.
1. Wählen Sie optional die **Negativ** bei Bedarf.

Sie verweisen auf die Edge-ACL nach Name in Ihrem VCL-Codefragment.

## Erstellen der benutzerdefinierten VCL für die Blockierungsliste

>[!NOTE]
>
>In diesem Beispiel erfahren fortgeschrittene Benutzer, wie ein VCL-Codefragment erstellt wird, um benutzerspezifische Blockierungsregeln für den Upload in den Fastly-Dienst zu konfigurieren. Sie können eine Blockierungsliste oder eine Zulassungsliste basierend auf einem Land vom Adobe Commerce-Administrator mithilfe der [Blockieren](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) im Fastly CDN für Magento 2-Modul verfügbar.

Nachdem Sie die Edge-ACL definiert haben, können Sie damit das VCL-Snippet erstellen, um den Zugriff auf die in der ACL angegebenen IP-Adressen zu blockieren. Sie können dasselbe VCL-Snippet sowohl in der Staging- als auch in der Produktionsumgebung verwenden. Sie müssen das Snippet jedoch separat in jede Umgebung hochladen.

Der folgende benutzerdefinierte VCL-Codeausschnitt (JSON-Format) zeigt die Logik zum Blockieren eingehender Anfragen mit einer Client-IP-Adresse, die mit einer Adresse in der ACL der Blockierungsliste übereinstimmt.

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

Bevor Sie ein auf diesem Beispiel basierendes Snippet erstellen, überprüfen Sie die Werte, um festzustellen, ob Sie Änderungen vornehmen müssen:

- `name`: Name für das VCL-Snippet. In diesem Beispiel haben wir den Namen `blocklist`.

- `priority`: Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität `5` , um sofort auszuführen und zu überprüfen, ob eine Admin-Anfrage von einer zulässigen IP-Adresse stammt. Das Snippet wird vor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type`: Gibt den Typ des VCL-Snippets an, das die Position des Snippets im generierten VCL-Code bestimmt. In diesem Beispiel verwenden wir `recv`, wodurch der VCL-Code in die `vcl_recv` Subroutine, unterhalb der Bausteinplakette VCL und über allen Objekten. Siehe [Fastly VCL-Codefragment](https://docs.fastly.com/api/config#api-section-snippet) für die Liste der Snippet-Typen.

- `content`: Der auszuführende VCL-Codeausschnitt, der die Client-IP-Adresse überprüft. Wenn sich die IP in der Edge-ACL befindet, wird sie vom Zugriff mit einer `403 Forbidden` -Fehler für die gesamte Website. Der Zugriff auf alle anderen Client-IP-Adressen ist zulässig.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin hinzu.](#add-the-custom-vcl-snippet). Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert [Schnelle Version 1.2.58](fastly-configuration.md#upgrade-fastly-module) oder höher).

- Speichern Sie das JSON-Codebeispiel in einer -Datei (z. B. `blocklist.json`) und [Hochladen mit der Fastly-API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern **Vollständiger Seiten-Cache** > **Schnelle Konfiguration** > **Benutzerdefinierte VCL-Snippets**.

1. Klicks **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `blocklist`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - Fügen Sie die **VCL** Snippet-Inhalt:

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Klicks **Erstellen** , um die VCL-Snippet-Datei mit dem Namensmuster zu generieren `type_priority_name.vcl`, beispielsweise `recv_5_blocklist.vcl`

1. Nachdem die Seite neu geladen wurde, klicken Sie auf **VCL schnell hochladen** im *Schnelle Konfiguration* -Abschnitt, um die Datei zur Konfiguration des Fastly-Dienstes hinzuzufügen.

1. Aktualisieren Sie nach dem Hochladen den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte Version des VCL-Codes während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie das benutzerdefinierte VCL-Snippet, um das Problem zu beheben. Laden Sie dann die VCL erneut hoch.

## Zusätzliche VCL-Beispiele für das Blockieren von Anforderungen

Die folgenden Beispiele zeigen, wie Sie Anforderungen mit Inline-Bedingungsanweisungen statt einer ACL-Liste blockieren.

>[!WARNING]
>
>In diesen Beispielen wird der VCL-Code als JSON-Payload formatiert, die in einer Datei gespeichert und in einer Fastly API-Anfrage gesendet werden kann. Sie können [VCL-Snippet vom Administrator](#add-the-custom-vcl-snippet)oder als JSON-Zeichenfolge mithilfe der Fastly-API. Um eine Validierung zu verhindern, wenn Sie die Fastly-API mit einer JSON-Zeichenfolge verwenden, müssen Sie einen umgekehrten Schrägstrich verwenden, um Sonderzeichen zu maskieren.

Siehe [Verwenden dynamischer VCL-Snippets](https://docs.fastly.com/vcl/vcl-snippets/) in der Fastly VCL Dokumentation.

### VCL-Codebeispiel: Block nach Ländercode

In diesem Beispiel wird der zweistellige ISO 3166-1-Ländercode für das Land verwendet, das mit der IP-Adresse verknüpft ist.

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>Anstatt ein benutzerdefiniertes VCL-Snippet zu verwenden, können Sie die [Blockieren](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) in der Adobe Commerce in der Cloud-Infrastruktur-Admin , um die Blockierung nach Ländercode oder einer Liste von Ländercodes zu konfigurieren.

### VCL-Codebeispiel: Blockierung durch HTTP-Anforderungs-Header für Benutzeragenten

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
