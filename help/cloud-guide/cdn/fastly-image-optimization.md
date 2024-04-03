---
title: Schnelle Bildoptimierung
description: Erfahren Sie, wie Sie die Bildbereitstellung optimieren und die Bildverwaltung für die Adobe Commerce-Site vereinfachen können, indem Sie die schnelle Bildoptimierung aktivieren und konfigurieren.
feature: Cloud, Configuration, Media
exl-id: 20f5c5c3-7c43-493b-b651-82b023cf5db5
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# Schnelle Bildoptimierung

Die schnelle Bildoptimierung (Fastly IO) bietet Echtzeit-Bildbearbeitung und -Optimierung, um die Bildbereitstellung zu beschleunigen und die Verwaltung von Bildquellensätzen für responsive Webanwendungen zu vereinfachen. Nach der Konfiguration bietet Fastly IO die folgenden Bildoptimierungsfunktionen:

- Erzwingen der verlustfreien Konvertierung
- Deep-Image-Optimierung
- Adaptive Pixelverhältnisse
- Unterstützung für gängige Bildformate: PNG, JPEG, GIF und WebP

Bevor Sie die Option Fastly IO aktivieren und konfigurieren, müssen Sie Ihren Fastly-Dienst einrichten und die Herkunftssicherung konfigurieren.

Basierend auf Ihren Konfigurationseinstellungen fügt das Snippet Fastly Image Optimization (Fastly IO) den VCL-Code ein, um die Bildoptimierung durchzuführen, die die Bereitstellung von Produktbildern in der Storefront beschleunigt. Es gibt drei Schritte zum Konfigurieren der Fastly IO: Aktivieren, Konfigurieren und Überprüfen.

## Fastly IO aktivieren

Aktivieren Sie die Fastly Image Optization (Fastly IO) über das Admin-Bedienfeld, indem Sie das Fastly IO VCL-Snippet hochladen. Das Snippet enthält die Schnellkonfigurationsanweisungen zur Verarbeitung aller Bilder über Bildoptimierer unter Verwendung von Standardkonfigurationen.

**Voraussetzungen:**

- Installieren Sie das Fastly-Modul Version 1.2.62 oder höher oder aktualisieren Sie es
- [Fastly Origin-Schutzschild und Back-End konfigurieren](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding)

**So aktivieren Sie Fastly IO**:

1. Bei Ihrer lokalen [Admin](../../get-started/onboarding.md#access-your-admin-panel) als Administrator.

1. Auswählen **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie im rechten Bereich **Vollständiger Seiten-Cache**.

1. Auswählen **Schnelle Konfiguration** > **Bildoptimierung** um die Konfigurationseinstellungen anzugeben.

1. Im _Fastly IO Snippet_ Feld auswählen **Aktivieren/Deaktivieren**.

1. Laden Sie das Fastly IO-Snippet hoch:

   - Auswählen **Standardmäßige IO-Konfigurationsoptionen** , um die Seite mit den standardmäßigen Bildoptimierungs-Konfigurationsoptionen zu öffnen.
   - Auswählen **Hochladen** , um das VCL-Snippet auf Ihren Server hochzuladen.

## Fastly IO konfigurieren

Überprüfen und aktualisieren Sie bei Bedarf die standardmäßigen IO-Konfigurationseinstellungen für die Bildoptimierung. Sie können beispielsweise die WebP- und JPEG-Qualitätsstufen für verlustbehaftete Formate ändern oder das Format für die Bereitstellung von JPEG-Bildern in _Progressiv_ oder _Grundlinie_. Außerdem können Sie Fastly IO für detailliertere Bildoptimierungsfunktionen verwenden, z. B.:

- Erzwingen der verlustfreien Konvertierung
- Deep-Image-Optimierung
- Adaptive Pixelverhältnisse

**So aktualisieren Sie die Schnellstartanleitung**:

1. Im _Schnelle Konfiguration_ in der _Standardmäßige IO-Konfigurationsoptionen_ Feld auswählen **Konfigurieren**.

   ![Anzeigen der Einstellungen der Fastly IO-Konfiguration](../../assets/cdn/fastly-io-default-config.png)

1. Überprüfen und aktualisieren Sie die Fastly IO-Konfigurationseinstellungen auf der _Standardkonfigurationsoptionen für die Bildoptimierung_ Seite:

   ![Fastly IO-Konfiguration überprüfen](../../assets/cdn/fastly-io-config-options.png)

   - **Auto WebP?**- Behalten Sie die Standardeinstellung bei (`Yes`), um Bilder in Browsern, die sie unterstützen, in das WebP-Format zu konvertieren. Wenn Sie die Einstellung auf **Nein**, verwendet Fastly den Bilddateityp, anstatt das Bild in das WebP-Format zu konvertieren.

   - **Standard-WebP-Qualität (verlustbehaftet)**- Behalten Sie die Standardeinstellung bei (`85`) oder geben Sie die Komprimierungsstufe für verlustreiche dateiformatierte Bilder ein. Sie können eine beliebige Ganzzahl von 1 bis 100 angeben.

   - **Standardmäßige JPEG-Formatsteuerelemente** - Behalten Sie die Standardeinstellung bei (`Auto`) oder wählen Sie den JPEG-Typ aus, der für die Bildbereitstellung verwendet werden soll. Wenn der Wert auf den Wert _Auto_, liefert Fastly Bilder mit dem Ausgabetyp, der dem Eingabetyp entspricht. Auswählen _Grundlinie_ , um Bilder zeilenweise anzuzeigen, beginnend von oben links bis unten rechts. Auswählen _Progressiv_ , um ein verschwommenes Bild anzuzeigen, das beim Laden klar wird.

   - **Standardqualität der JPEG**- Behalten Sie die Standardeinstellung bei (`85`) oder geben Sie die Komprimierungsstufe für die Qualität verlustreicher Dateiformate ein. Geben Sie eine beliebige Ganzzahl von 1 bis 100 an.

   - **Vergrößern zulassen?**—Behalten Sie die Standardeinstellung (`No`) oder wählen Sie `Yes` , um Bilder zurückzugeben, die größer als die ursprüngliche Quelldatei sind, damit sie in die angeforderten Dimensionen passen.

   - **Filter vergrößern**- Behalten Sie die Standardeinstellung bei (`Lancsoz3`) oder wählen Sie eine Alternative aus. Diese Einstellung gibt den Filter an, der zum Bereitstellen eines in der Größe angepassten Bildes verwendet wird. Je nach ausgewähltem Filter kann das in der Größe angepasste Bild eine höhere oder niedrigere Anzahl Pixel aufweisen.

      - `Lanczos3` (Standard) - Stellt das Bild mit der besten Qualität bereit. Es erhöht die Fähigkeit, Kanten und lineare Funktionen innerhalb eines Bildes zu erkennen, und verwendet _[!DNL sinc]_Resampling, um den bestmöglichen Wiederaufbau zu ermöglichen.
      - `Lanczos2`—Verwendet denselben Filter wie `Lancsoz3` jedoch mit einer weniger genauen Annäherung der _[!DNL sinc]_Resampling-Funktion.
      - `Bicubic`—Hat einen natürlichen Scharfzeichnungseffekt, wenn ein Bild kleiner gemacht wird.
      - `Bilinear`—Hat einen natürlichen Ausgleichungseffekt, wenn ein Bild größer wird.
      - `Nearest`—Hat einen natürlichen Pixeleffekt bei der Größenanpassung der Pixelgrafik.

1. Nachdem Sie die IO-Konfigurationseinstellungen für den Fastly-Dienst festgelegt haben, wählen Sie **Abbrechen** , um zu den Einstellungen für die schnelle Konfiguration zurückzukehren.

1. In der Bildoptimierungskonfiguration _Deep-Image-Optimierung aktivieren_ Feld auswählen **Ja** um die Deep-Image-Optimierung zu aktivieren.

   ![Fastly IO Deep-Image-Optimierung aktivieren](../../assets/cdn/fastly-io-deep-image-config.png)

   Die Deep-Image-Optimierung ist standardmäßig deaktiviert. Wenn diese Funktion aktiviert ist, ist die integrierte Größenanpassungsfunktion in Adobe Commerce deaktiviert und die Größenanpassung wird an den Fastly IO-Dienst abgeladen. Die Bildoptimierung gilt nur für Produktbilder. Die Größe von CMS-Bildern wird nicht geändert. Siehe [Schnelle Dokumentation](#deep-image-optimization).

1. Nachdem Sie die Deep-Image-Optimierung aktiviert haben, aktivieren Sie die [adaptive Pixelverhältnisse](#adaptive-pixel-ratios) -Funktion verwenden, um Bilder zu generieren, die für die Verwendung auf responsiven Websites optimiert sind.

   ![Fastly IO adaptive Pixelverhältnisse aktivieren](../../assets/cdn/fastly-io-config-adaptive-pixel.png)

   - Im _Aktivieren von Pixelverhältnissen für adaptive Geräte_ Feld auswählen **Ja**.
   - Im _Gerätepixelverhältnisse_ , übernehmen Sie die Standardeinstellung oder wählen Sie die **Systemeingabe** aktivieren, um die Einstellung zu entfernen. Wählen Sie dann das gewünschte Verhältnis aus. Eine höhere Einstellung für das Gerätepixelverhältnis liefert größere Bilder.

1. Auswählen **Konfiguration speichern**.

### Erzwingen der verlustfreien Konvertierung

Standardmäßig erzwingt der Fastly IO-Dienst die Konvertierung verlustfreier Formate wie PNG, BMP oder WEBP in das JPEG/WEBP-Format.

Der Vorteil der erzwungenen verlustbehafteten Konvertierung besteht darin, dass kleinere Bilder bereitgestellt werden.
Wenn Sie beispielsweise das JPEG- oder WEBp-Format anstelle von PNG verwenden, kann die Größe je nach der in der Fastly IO-Konfiguration angegebenen Qualitätsstufe um 60 bis 70 Prozent reduziert werden.

Je nach der für die Bildoptimierung ausgewählten Qualitätsstufe können visuelle Unterschiede bei Bildern auftreten. Beispielsweise werden Alpha-Kanäle/Transparenzen entfernt und durch einen weißen Hintergrund ersetzt, es sei denn, Sie verwenden eine Deep-Image-Optimierung, die die Hintergrundfarbe Ihres Designs verwendet.

Wenn Sie die verlustreiche Konversion deaktivieren (`WebP Auto? = No`), ändert Fastly IO nur JPEG-Bilder für kompatible Browser in das WEBP-Format. Es werden keine anderen Bildtypen geändert. Wenn das Originalbild beispielsweise PNG ist, lautet die Ausgabe vom Fastly IO-Dienst PNG.

### Deep-Image-Optimierung

Die Deep-Image-Optimierung ist standardmäßig deaktiviert. Durch Aktivierung dieser Option wird die integrierte Adobe Commerce-Größenanpassung deaktiviert und vollständig an den Fastly IO-Dienst abgeladen.
Diese Funktion ändert nur die Größe _product_ Bilder. Die Größe von CMS-Bildern wird nicht geändert.

Durch die Aktivierung der Deep-Image-Optimierung wird jedem Bild eine Hintergrundfarbdefinition hinzugefügt, wie in Ihrem Design definiert. Daher werden WebP-Bilder verlustfrei von WebP in verlustfreies WebP umgestellt. Einer der Hauptunterschiede zwischen verlustfrei und verlustfrei besteht darin, dass der Alphakanal verlustfrei von PNG-Bildern entfernt wird, wodurch wesentlich kleinere Bilder bereitgestellt werden. Bilder mit Transparenz können jedoch auf Produkt- und Kampagnenseiten mit einem anderen Hintergrund merkwürdig aussehen.

Beispielsweise stellt der folgende Code die ursprüngliche Quelle für ein Bild aus dem Luma-Design dar:

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/cache/f073062f50e48eb0f0998593e568d857/m/b/mb02-gray-0.jpg"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Wenn die Funktion Fastly IO Deep-Bild-Optimierung aktiviert ist, wird der ursprüngliche Quellcode für das Bild wie im folgenden Beispiel gezeigt umgeschrieben:

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

### Adaptive Pixelverhältnisse

Die Funktion Adaptive Pixelverhältnisse ist nützlich, um Bilder für progressive Webanwendungen zu optimieren. Dadurch können Sie mehrere Bildgrößen und Auflösungen aus einer Bildquellendatei bereitstellen, indem Sie eine `srcset` für jedes Produktbild.

Wenn die Funktion für adaptive Pixelverhältnisse aktiviert ist, stellt der Fastly IO-Dienst ein Bild mit fester Breite bereit, das an verschiedene Varianten angepasst werden kann `device-pixel-ratios`.
Beispielsweise ändert der Dienst die Produktbilddefinition wie im folgenden Beispiel gezeigt:

```html
<img class="product-image-photo"
     srcset="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=2 2x,
  https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=3 3x"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Siehe `srcset` [Browserunterstützung](https://caniuse.com/#feat=srcset) und [Spezifikation](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset).

## Fastly IO überprüfen

Nachdem Sie Fastly IO aktiviert und konfiguriert haben, validieren Sie Ihre Konfiguration, indem Sie Webseitenschnelltests mit und ohne Fastly IO-Aktivierung durchführen. Überprüfen Sie außerdem die Bilder in Ihrem Store, um die Bildgröße und das Erscheinungsbild auf Probleme zu überprüfen.
