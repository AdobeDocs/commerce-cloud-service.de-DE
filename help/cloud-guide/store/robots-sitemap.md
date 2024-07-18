---
title: Sitemap- und Suchmaschinenroboter hinzufügen
description: Erfahren Sie, wie Sie Adobe Commerce in der Cloud-Infrastruktur Sitemap- und Suchmaschinenrobots hinzufügen.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Sitemap- und Suchmaschinenroboter hinzufügen

Der Versuch, die Datei `sitemap.xml` zu generieren und in den Stammordner zu schreiben, führt zu folgendem Fehler:

```
Please make sure that "/" is writable by the web-server.
```

Mit Adobe Commerce in der Cloud-Infrastruktur können Sie nur in bestimmte Ordner schreiben, z. B. `var`, `pub/media`, `pub/static` oder `app/etc`. Wenn Sie die Datei &quot;`sitemap.xml`&quot;mithilfe des Admin-Bedienfelds generieren, müssen Sie den Pfad &quot;`/media/`&quot;angeben.

Sie müssen keine `robots.txt`-Datei generieren, da sie den Inhalt von `robots.txt` bei Bedarf generiert und in der Datenbank speichert. Sie können den Inhalt in Ihrem Browser mit dem Link `<domain.your.project>/robots.txt` oder `<domain.your.project>/robots` anzeigen.

Dies erfordert die ECE-Tools-Version 2002.0.12 und höher mit einer aktualisierten `.magento.app.yaml` -Datei. Ein Beispiel für diese Regeln finden Sie im [magento-cloud-Repository](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**So generieren Sie eine `sitemap.xml` -Datei in Version 2.2 und höher**:

1. Rufen Sie Admin auf.
1. Klicken Sie im Menü _Marketing_ im Abschnitt _SEO &amp; Suche_ auf **Site Map** .
1. Klicken Sie in der Ansicht _Sitemap_ auf **Sitemap hinzufügen**.
1. Geben Sie in der Ansicht _Neue Sitemap_ die folgenden Werte ein:

   - **Dateiname**:`sitemap.xml`
   - **Pfad**:`/media/`

1. Klicken Sie auf **Speichern und generieren**. Die neue Sitemap wird im Raster _Sitemap_ verfügbar.
1. Klicken Sie auf den Pfad in der Spalte _Link für Google_ .

**Hinzufügen von Inhalt zur `robots.txt` Datei**:

1. Rufen Sie Admin auf.
1. Klicken Sie im Menü _Inhalt_ auf **Konfiguration** im Abschnitt _Design_ .
1. Klicken Sie in der Ansicht _Design-Konfiguration_ in der Spalte _Aktion_ auf **Bearbeiten** für die Website.
1. Klicken Sie in der Ansicht _Hauptwebsite_ auf **Suchmaschinen-Roboter**.
1. Aktualisieren Sie das Feld **Benutzerdefinierte Anweisung von robots.txt** bearbeiten .
1. Klicken Sie auf **Konfiguration speichern**.
1. Überprüfen Sie die `<domain.your.project>/robots.txt`-Datei oder die `<domain.your.project>/robots`-URL in Ihrem Browser.

>[!NOTE]
>
>Wenn die `<domain.your.project>/robots.txt` -Datei einen `404 error` generiert, senden Sie ein Adobe Commerce Support-Ticket ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um die Umleitung von `/robots.txt` auf `/media/robots.txt` zu entfernen.[

## Mit Fastly VCL-Snippet umschreiben

Wenn Sie unterschiedliche Domänen haben und separate Sitemaps benötigen, können Sie eine VCL erstellen, um zur entsprechenden Sitemap zu gelangen. Generieren Sie die Datei &quot;`sitemap.xml`&quot;im Admin-Bedienfeld wie oben beschrieben und erstellen Sie dann ein benutzerdefiniertes Fastly VCL-Snippet, um die Umleitung zu verwalten. Siehe [Benutzerdefinierte schnelle VCL-Snippets](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> Sie können benutzerdefinierte VCL-Snippets von der Admin-Benutzeroberfläche oder über die Fastly-API hochladen. Siehe [Beispiele und Tutorials für benutzerdefinierte VCL-Codebeispiele und -Tutorials](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Verwenden eines Fastly VCL-Snippets zur Umleitung

Erstellen Sie ein benutzerdefiniertes VCL-Snippet, um den Pfad für `sitemap.xml` mit den Schlüssel-Wert-Paaren `type` und `content` in `/media/sitemap.xml` umzuschreiben.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

Das folgende Beispiel zeigt, wie der Pfad für `robots.txt` und `sitemap.xml` in `/media/robots.txt` und `/media/sitemap.xml` umgeschrieben wird

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

Erstellen Sie eine `pub/media/domain_robots.txt` -Datei, deren Domäne `domain.com` ist, und verwenden Sie das nächste VCL-Snippet:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

Das VCL-Snippet routet `http://domain.com/robots.txt` und zeigt die Datei `pub/media/domain_robots.txt` an.

Um eine Umleitung für `robots.txt` und `sitemap.xml` in einem einzelnen Snippet zu konfigurieren, erstellen Sie die Dateien `pub/media/domain_robots.txt` und `pub/media/domain_sitemap.xml`, wobei die Domäne `domain.com` ist, und verwenden Sie das nächste VCL-Snippet:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

In der Admin-Konfiguration `sitemap` müssen Sie den Speicherort der Datei mit `pub/media/` anstelle von `/` angeben.

### Konfigurieren der Indizierung nach Suchmaschine

Um die `robots.txt` -Anpassungen zu aktivieren, müssen Sie die Option **Indizierung durch Suchmaschinen ist für`<environment-name>`** in Ihren Projekteinstellungen aktivieren.

![Verwenden Sie den [!DNL Cloud Console], um Umgebungen zu verwalten](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Wenn Sie PWA Studio verwenden und nicht auf Ihre konfigurierte `robots.txt` -Datei zugreifen können, fügen Sie `robots.txt` zur [Vorname-Zulassungsliste](https://github.com/magento/magento2-upward-connector#front-name-allowlist) unter **Stores** > Konfiguration > **Allgemein** > **Web** > UPWARD-PWA-Konfiguration hinzu.
