---
title: Sitemap- und Suchmaschinenroboter hinzufügen
description: Erfahren Sie, wie Sie Adobe Commerce in der Cloud-Infrastruktur Sitemap- und Suchmaschinenrobots hinzufügen.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Sitemap- und Suchmaschinenroboter hinzufügen

Ein Versuch, die `sitemap.xml` in den Stammordner zu laden, führt der folgende Fehler:

```terminal
Please make sure that "/" is writable by the web-server.
```

Mit Adobe Commerce in der Cloud-Infrastruktur können Sie nur in bestimmte Ordner schreiben, z. B. `var`, `pub/media`, `pub/static`oder `app/etc`. Wenn Sie die `sitemap.xml` -Datei mithilfe des Admin-Bedienfelds angeben, müssen Sie die `/media/` Pfad.

Sie müssen keine `robots.txt` -Datei, da sie die `robots.txt` Inhalt nach Bedarf und speichert ihn in der Datenbank. Sie können den Inhalt in Ihrem Browser mit dem `<domain.your.project>/robots.txt` oder `<domain.your.project>/robots` -Link.

Dies erfordert die ECE-Tools-Version 2002.0.12 und höher mit einer aktualisierten Version `.magento.app.yaml` -Datei. Ein Beispiel für diese Regeln finden Sie im Abschnitt [Magento-Cloud-Repository](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**So generieren Sie eine `sitemap.xml` Datei in Version 2.2 und höher**:

1. Rufen Sie Admin auf.
1. Im _Marketing_ Menü, klicken **Site-Map** im _SEO und Suche_ Abschnitt.
1. Im _Site-Map_ Ansicht, klicken Sie **Sitemap hinzufügen**.
1. Im _Neue Site-Map_ -Ansicht die folgenden Werte eingeben:

   - **Dateiname**:`sitemap.xml`
   - **Pfad**:`/media/`

1. Klicks **Speichern und generieren**. Die neue Sitemap wird im _Site-Map_ Gitter.
1. Klicken Sie auf den Pfad im _Link für Google_ Spalte.

**So fügen Sie Inhalte zum `robots.txt` file**:

1. Rufen Sie Admin auf.
1. Im _Inhalt_ Menü, klicken **Konfiguration** im _Design_ Abschnitt.
1. Im _Designkonfiguration_ Ansicht, klicken Sie **Bearbeiten** für die Website im _Aktion_ Spalte.
1. Im _Hauptwebsite_ Ansicht, klicken Sie **Suchmaschinen-Roboter**.
1. Aktualisieren Sie die **Bearbeiten von benutzerdefinierten Anweisungen für robots.txt** -Feld.
1. Klicks **Konfiguration speichern**.
1. Überprüfen Sie die `<domain.your.project>/robots.txt` Datei oder `<domain.your.project>/robots` URL in Ihrem Browser.

>[!NOTE]
>
>Wenn die Variable `<domain.your.project>/robots.txt` -Datei generiert eine `404 error`, [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Umleitung aus `/robots.txt` nach `/media/robots.txt`.

## Mit Fastly VCL-Snippet umschreiben

Wenn Sie unterschiedliche Domänen haben und separate Sitemaps benötigen, können Sie eine VCL erstellen, um zur entsprechenden Sitemap zu gelangen. Generieren Sie die `sitemap.xml` -Datei im Admin-Bedienfeld wie oben beschrieben, erstellen Sie dann ein benutzerdefiniertes Fastly VCL-Snippet, um die Umleitung zu verwalten. Siehe [Benutzerdefinierte Fastly VCL-Snippets](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> Sie können benutzerdefinierte VCL-Snippets von der Admin-Benutzeroberfläche oder über die Fastly-API hochladen. Siehe [Beispiele und Tutorials für benutzerdefinierte VCL-Snippets](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Verwenden eines Fastly VCL-Snippets zur Umleitung

Erstellen Sie ein benutzerdefiniertes VCL-Snippet, um den Pfad für `sitemap.xml` nach `/media/sitemap.xml` mithilfe der `type` und `content` Schlüssel-Wert-Paare.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

Das folgende Beispiel zeigt, wie der Pfad für `robots.txt` und `sitemap.xml` nach `/media/robots.txt` und `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**So verwenden Sie ein Fastly VCL-Snippet für eine bestimmte Domänenumleitung**:

Erstellen Sie eine `pub/media/domain_robots.txt` Datei, wobei die Domäne lautet `domain.com`und verwenden Sie das nächste VCL-Snippet:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

Die VCL-Snippet-Routen `http://domain.com/robots.txt` und stellt die `pub/media/domain_robots.txt` -Datei.

So konfigurieren Sie eine Umleitung für `robots.txt` und `sitemap.xml` in einem einzelnen Snippet erstellen `pub/media/domain_robots.txt` und `pub/media/domain_sitemap.xml` Dateien, wobei die Domäne ist `domain.com` und verwenden Sie das nächste VCL-Snippet:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

Im `sitemap` Admin-Konfiguration festlegen, müssen Sie den Speicherort der Datei angeben, indem Sie `pub/media/` anstelle von `/`.

### Konfigurieren der Indizierung nach Suchmaschine

So aktivieren `robots.txt` Anpassungen festlegen, müssen Sie die **Die Indexierung durch Suchmaschinen ist aktiviert für`<environment-name>`** in den Projekteinstellungen.

![Verwenden Sie die [!DNL Cloud Console] zum Verwalten von Umgebungen](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Wenn Sie PWA Studio verwenden und nicht auf Ihre konfigurierte `robots.txt` Datei hinzufügen `robots.txt` der [Zulassungsliste &quot;Vorname&quot;](https://github.com/magento/magento2-upward-connector#front-name-allowlist) at **Stores** > Konfiguration > **Allgemein** > **Web** > UPWARD PWA Configuration.
