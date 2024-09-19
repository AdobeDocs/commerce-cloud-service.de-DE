---
title: Benutzerdefinierte VCL für das Blockieren von Anforderungen
description: Blockieren eingehender Anfragen nach IP-Adresse mithilfe einer ACL (Edge Access Control List) mit einem benutzerdefinierten VCL-Snippet.
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 16c34b6c693c4d4d5c67b21c79e0cd5d198e047b
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Benutzerdefinierte VCL für das Blockieren von Anforderungen

Sie können das Fastly CDN-Modul für Magento 2 verwenden, um eine Edge-ACL mit einer Liste von IP-Adressen zu erstellen, die Sie blockieren möchten. Anschließend können Sie diese Liste mit einem VCL-Snippet verwenden, um eingehende Anfragen zu blockieren. Der Code überprüft die IP-Adresse der eingehenden Anfrage. Wenn es mit einer in der ACL-Liste enthaltenen IP-Adresse übereinstimmt, blockiert Fastly die Anfrage am Zugriff auf Ihre Site und gibt einen `403 Forbidden error` zurück. Der Zugriff auf alle anderen Client-IP-Adressen ist zulässig.

**Voraussetzungen:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste der zu blockierenden Client-IP-Adressen

## Erstellen von Edge ACL zum Blockieren von Client-IP-Adressen

Sie erstellen eine Edge ACL, um die Liste der zu blockierenden IP-Adressen zu definieren. Nachdem Sie die ACL erstellt haben, können Sie sie in einem benutzerdefinierten VCL-Snippet verwenden, um den Zugriff auf Ihre Staging- oder Produktions-Site zu verwalten.

Verwalten Sie den Zugriff für Staging- und Produktions-Sites, indem Sie die Edge-ACL mit demselben Namen in beiden Umgebungen erstellen. Der VCL-Snippet-Code gilt für beide Umgebungen.

1. Melden Sie sich beim Administrator an.
1. Navigieren Sie zu **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** > **Gesamter Seiten-Cache** > **Schnelle Konfiguration**.
1. Erweitern Sie den Abschnitt **Edge ACL** .
1. Klicken Sie auf **ACL hinzufügen** , um eine Liste zu erstellen. Nennen Sie für dieses Beispiel die Liste &quot;Blockierungsliste&quot;.
1. Geben Sie IP-Adresswerte in die Liste ein. Alle Client-IP-Adressen, die dieser Liste hinzugefügt wurden, werden blockiert und können nicht auf die Site zugreifen.
1. Aktivieren Sie bei Bedarf optional das Kontrollkästchen **Negiert** .

Sie referenzieren die Edge-ACL nach Name in Ihrem VCL-Codefragment-Code.

## Erstellen der benutzerdefinierten VCL für die Blockierungsliste

>[!NOTE]
>
>In diesem Beispiel erfahren fortgeschrittene Benutzer, wie ein VCL-Codefragment erstellt wird, um benutzerspezifische Blockierungsregeln für den Upload in den Fastly-Dienst zu konfigurieren. Sie können vom Adobe Commerce-Administrator eine Blockierungsliste oder eine Zulassungsliste basierend auf dem Land mithilfe der Funktion [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) konfigurieren, die im Fastly CDN für das Magento 2-Modul verfügbar ist.

Nachdem Sie die Edge ACL definiert haben, können Sie sie verwenden, um das VCL-Snippet zu erstellen, um den Zugriff auf die in der ACL angegebenen IP-Adressen zu blockieren. Sie können dasselbe VCL-Snippet sowohl in der Staging- als auch in der Produktionsumgebung verwenden. Sie müssen das Snippet jedoch separat in jede Umgebung hochladen.

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

- `name`: Name für das VCL-Codefragment. Für dieses Beispiel haben wir den Namen `blocklist` verwendet.

- `priority`: Bestimmt, wann das VCL-Snippet ausgeführt wird. Die Priorität lautet &quot;`5`&quot;, um sofort auszuführen und zu überprüfen, ob eine Admin-Anfrage von einer zulässigen IP-Adresse stammt. Das Snippet wird ausgeführt, bevor einem der standardmäßigen Magento VCL-Snippets (`magentomodule_*`) eine Priorität von 50 zugewiesen wurde. Legen Sie die Priorität für jedes benutzerdefinierte Snippet höher oder niedriger als 50 fest, je nachdem, wann Ihr Snippet ausgeführt werden soll. Snippets mit niedrigeren Prioritätswerten werden zuerst ausgeführt.

- `type`: Gibt den Typ des VCL-Snippets an, das die Position des Snippets im generierten VCL-Code bestimmt. In diesem Beispiel verwenden wir &quot;`recv`&quot;, wodurch der VCL-Code in die &quot;`vcl_recv`&quot;-UnterRoutine unter der Textbausteinvorlage &quot;VCL&quot;und über allen Objekten eingefügt wird. Die Liste der Ausschnitttypen finden Sie in der Codeausschnitt-Referenz für [Fastly VCL](https://docs.fastly.com/api/config#api-section-snippet) .

- `content`: Das auszuführende VCL-Codefragment, das die Client-IP-Adresse überprüft. Wenn sich die IP in der Edge ACL befindet, wird sie für die gesamte Website mit einem `403 Forbidden` -Fehler vom Zugriff ausgeschlossen. Der Zugriff auf alle anderen Client-IP-Adressen ist zulässig.

Nachdem Sie den Code für Ihre Umgebung überprüft und aktualisiert haben, verwenden Sie eine der folgenden Methoden, um das benutzerdefinierte VCL-Snippet Ihrer Fastly Service-Konfiguration hinzuzufügen:

- [Fügen Sie das benutzerdefinierte VCL-Snippet aus dem Admin](#add-the-custom-vcl-snippet) hinzu. Diese Methode wird empfohlen, wenn Sie auf den Admin zugreifen können. (Erfordert [schnelle Version 1.2.58](fastly-configuration.md#upgrade-fastly-module) oder höher.)

- Speichern Sie das JSON-Codebeispiel in eine Datei (z. B. `blocklist.json`) und laden Sie sie mit der Fastly API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api) hoch. [ Verwenden Sie diese Methode, wenn Sie nicht auf den Admin zugreifen können.

## Hinzufügen des benutzerdefinierten VCL-Snippets

{{admin-login-step}}

1. Klicken Sie auf **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie **Vollständiger Seiten-Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Klicken Sie auf **Benutzerdefiniertes Snippet erstellen**.

1. Fügen Sie die VCL-Snippet-Werte hinzu:

   - **Name** — `blocklist`

   - **Typ** — `recv`

   - **Priorität** — `5`

   - Fügen Sie den Codeausschnitt-Inhalt **VCL** hinzu:

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Klicken Sie auf **Erstellen** , um die VCL-Snippet-Datei mit dem Namensmuster `type_priority_name.vcl` zu generieren, z. B. `recv_5_blocklist.vcl`

1. Klicken Sie nach dem Neuladen der Seite im Abschnitt *Schnelle Konfiguration* auf **VCL auf Fastly hochladen** , um die Datei zur Konfiguration des Fastly-Dienstes hinzuzufügen.

1. Aktualisieren Sie nach dem Hochladen den Cache gemäß der Benachrichtigung oben auf der Seite.

Validiert die aktualisierte Version des VCL-Codes während des Upload-Prozesses schnell. Wenn die Validierung fehlschlägt, bearbeiten Sie das benutzerdefinierte VCL-Snippet, um das Problem zu beheben. Laden Sie dann die VCL erneut hoch.

## Zusätzliche VCL-Beispiele für das Blockieren von Anforderungen

Die folgenden Beispiele zeigen, wie Sie Anforderungen mit Inline-Bedingungsanweisungen statt einer ACL-Liste blockieren.

>[!WARNING]
>
>In diesen Beispielen wird der VCL-Code als JSON-Payload formatiert, die in einer Datei gespeichert und in einer Fastly API-Anfrage gesendet werden kann. Sie können das [VCL-Snippet vom Admin](#add-the-custom-vcl-snippet) oder als JSON-Zeichenfolge mithilfe der Fastly-API senden. Um Überprüfungsfehler zu vermeiden, wenn Sie die Fastly-API mit einer JSON-Zeichenfolge verwenden, müssen Sie einen umgekehrten Schrägstrich verwenden, um Sonderzeichen zu maskieren.

>[!NOTE]
>Wenn Sie das VCL-Snippet vom Admin senden, extrahieren Sie die einzelnen Werte aus dem VCL-Beispielcode und geben Sie sie in die entsprechenden Felder ein. Beispiel:
>- Name: `<name of the VCL>`
>- Dynamisch: `<0/1>`
>- Typ: `<type>`
>- Priorität: `<priority>`
>- Inhalt: `<content>`

Siehe [Verwenden dynamischer VCL-Snippets](https://docs.fastly.com/vcl/vcl-snippets/) in der Fastly VCL-Dokumentation.

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
>Statt ein benutzerdefiniertes VCL-Snippet zu verwenden, können Sie die Funktion Fastly [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) in der Adobe Commerce in der Cloud-Infrastruktur-Admin verwenden, um die Blockierung nach Ländercode oder einer Liste von Ländercodes zu konfigurieren.

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
