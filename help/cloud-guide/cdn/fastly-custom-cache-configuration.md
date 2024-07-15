---
title: Cache-Konfiguration anpassen
description: Erfahren Sie, wie Sie die Cache-Konfigurationseinstellungen überprüfen und anpassen können, nachdem die Einrichtung des Fastly-Dienstes abgeschlossen ist.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# Cache-Konfiguration anpassen

Nachdem Sie den Fastly-Dienst in Ihren Staging- und Produktionsumgebungen eingerichtet und getestet haben, überprüfen und passen Sie die Cache-Konfigurationseinstellungen an. Beispielsweise können Sie Einstellungen aktualisieren, um TLS zu zwingen, HTTP-Anforderungen an Fastly umzuleiten, Bereinigungsparameter zu aktualisieren und die einfache Authentifizierung zu aktivieren, damit Ihre Site während der Entwicklung mit einem Kennwort geschützt wird.

Die folgenden Abschnitte enthalten eine Übersicht und Anweisungen zum Konfigurieren einiger Cacheeinstellungen. Weitere Informationen zu den verfügbaren Konfigurationsoptionen finden Sie in der Dokumentation zum [Fastly CDN Module for Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) .

## TLS erzwingen

Bietet die Option _TLS erzwingen_ für die Umleitung unverschlüsselter Anfragen (HTTP) an Fastly. Nachdem Ihre Staging- oder Produktionsumgebung mit einem [gültigen SSL-/TLS-Zertifikat](fastly-configuration.md#provision-ssltls-certificates) ausgestattet wurde, können Sie die Schnelle Konfiguration für Ihren Store aktualisieren, um die Option TLS erzwingen zu aktivieren. Weitere Informationen finden Sie im Handbuch zum _Fastly CDN Module for Magento 2_ im Handbuch zum Fastly [Force TLS guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) .

>[!NOTE]
>
>Die Aktivierung der Option TLS erzwingen ist eine empfohlene Best Practice für Adobe Commerce in Cloud-Infrastrukturspeichern.

## Fastly-Timeout erweitern

Die Fastly-Dienstkonfiguration gibt für HTTPS-Anforderungen an den Administrator einen standardmäßigen Timeout-Zeitraum von 180 Sekunden an. Bei einer Anforderungsverarbeitung, die den Timeout-Zeitraum überschreitet, wird ein 503-Fehler zurückgegeben. Daher können Sie 503-Fehler erhalten, wenn Sie Anfragen erhalten, die eine langwierige Verarbeitung erfordern, oder wenn Sie versuchen, Massenvorgänge durchzuführen.

Um Massenaktionen durchzuführen, die länger als 3 Minuten dauern, ändern Sie den Wert _Admin path timeout__ , um Fehler vom Typ 503 zu vermeiden.

>[!NOTE]
>
>Informationen zum Erweitern von Fastly-Timeout-Parametern für andere als Admin in der Fastly-Benutzeroberfläche finden Sie unter [Erhöhen der Timeouts für lange Aufträge](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**So erweitern Sie das Fastly-Timeout für den Admin**:

{{admin-login-step}}

1. Klicken Sie auf &quot;**Stores**&quot;> &quot;Einstellungen&quot;> &quot;**Konfiguration**&quot;> &quot;**Erweitert**&quot;> &quot;**System**&quot;und erweitern Sie &quot;**Vollständiger Seiten-Cache**&quot;.

1. Erweitern Sie im Abschnitt _Schnelle Konfiguration_ den Eintrag **Erweiterte Konfiguration** .

1. Legen Sie den Wert **admin path timeout** in Sekunden fest. Dieser Wert darf nicht mehr als 10 Minuten (600 Sekunden) betragen.

1. Klicken Sie oben auf der Seite auf **Konfiguration speichern** .

1. Nachdem die Seite neu geladen wurde, wählen Sie im Abschnitt _Schnelle Konfiguration_ die Option **VCL auf Fastly hochladen** aus.

Ruft schnell den Admin-Pfad zum Generieren der VCL-Datei aus der `app/etc/env.php`-Konfigurationsdatei ab.

## Bereinigungsoptionen konfigurieren

Bietet auf Ihrer Magento-Cache-Verwaltungsseite schnell mehrere Arten von Bereinigungsoptionen, einschließlich Optionen zum Bereinigen von Produktkategorie, Produkt-Assets und Inhalten. Wenn diese Option aktiviert ist, sucht Fastly nach Ereignissen, um diese Zwischenspeicher automatisch zu löschen. Wenn Sie eine Bereinigungsoption deaktivieren, können Sie die Fastly-Caches nach Abschluss der Aktualisierungen über die Seite &quot;Cache-Verwaltung&quot;manuell bereinigen.

Zu den Bereinigungsoptionen gehören:

- **Kategorie bereinigen** - Löscht den Inhalt der Produktkategorie (nicht den Produktinhalt), wenn Sie ein einzelnes Produkt hinzufügen und aktualisieren. Sie können diese Option deaktivieren und die Bereinigung des Produkts aktivieren, wodurch Produkte und Produktkategorien bereinigt werden.
- **Produkt bereinigen** - Löscht beim Speichern einer einzelnen Änderung an einem Produkt den gesamten Inhalt der Produkt- und Produktkategorie. Die Aktivierung des Bereinigungsprodukts kann hilfreich sein, um sofort Aktualisierungen an Kunden zu erhalten, wenn ein Preis geändert, eine Produktoption hinzugefügt und der Produktbestand nicht vorrätig ist.
- **Bereinigen Sie die CMS-Seite** - Bereinigt Seiteninhalte beim Aktualisieren und Hinzufügen von Seiten zum Adobe Commerce CMS. Beispielsweise können Sie eine Bereinigung durchführen, wenn Sie Ihre Geschäftsbedingungen oder Rückgabebedingungen aktualisieren. Wenn Sie diese Änderungen selten vornehmen, können Sie die automatische Bereinigung deaktivieren.
- **Soft purge** - Legt den Inhalt gemäß dem veralteten Zeitpunkt in &quot;veraltet&quot;und bereinigt ihn. Zusätzlich zu den veralteten Zeiten werden Kunden veraltete Inhalte bereitgestellt, während der Inhalt im Hintergrund schnell aktualisiert wird.

![Bereinigungsoptionen konfigurieren](../../assets/cdn/fastly-purge-options.png)

**So konfigurieren Sie die Optionen für eine schnelle Bereinigung**:

1. Erweitern Sie im Abschnitt _Schnelle Konfiguration_ den Eintrag **Erweiterte Konfiguration** , um die Bereinigungsoptionen anzuzeigen.

1. Wählen Sie für jede Bereinigungsoption **Ja** aus, um die automatische Bereinigung zu aktivieren, oder **Nein**, um die automatische Bereinigung zu deaktivieren.

   Wenn Sie eine Bereinigungsoption deaktivieren, müssen Sie den Cache für diese Kategorie auf der Seite _Cache-Verwaltung_ manuell bereinigen.

1. Klicken Sie oben auf der Seite auf **Konfiguration speichern** .

1. Nachdem die Seite neu geladen wurde, wählen Sie im Abschnitt _Schnelle Konfiguration_ die Option **VCL auf Fastly hochladen** aus.

Weitere Informationen finden Sie unter [Schnellkonfigurationsoptionen](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## GeoIP-Handhabung konfigurieren

Das Fastly-Modul beinhaltet die GeoIP-Handhabung, um Besucher automatisch umzuleiten oder eine Liste von Stores bereitzustellen, die mit der erhaltenen Ländercode übereinstimmen. Wenn Sie bereits eine Erweiterung für die GeoIP-Handhabung verwenden, müssen Sie die Funktionen möglicherweise mit den Fastly-Optionen überprüfen.

**So richten Sie die GeoIp-Handhabung ein**:

{{admin-login-step}}

1. Klicken Sie auf &quot;**Stores**&quot;> &quot;Einstellungen&quot;> &quot;**Konfiguration**&quot;> &quot;**Erweitert**&quot;> &quot;**System**&quot;und erweitern Sie &quot;**Vollständiger Seiten-Cache**&quot;.

1. Erweitern Sie im Abschnitt _Schnelle Konfiguration_ den Eintrag **Erweiterte Konfiguration** .

1. Scrollen Sie nach unten und wählen Sie **Ja** zu **GeoIP aktivieren** aus. Es werden zusätzliche Konfigurationsoptionen angezeigt.

1. Wählen Sie für die GeoIP-Aktion aus, ob der Besucher automatisch mit **Umleitung** umgeleitet wird oder eine Liste mit Stores bereitgestellt wird, aus denen er mit **Dialogfeld** auswählen kann.

1. Wählen Sie für **Länderzuordnung** die Option **Hinzufügen** aus, um einen aus zwei Buchstaben bestehenden Ländercode einzugeben, der einem bestimmten Adobe Commerce-Store aus einer Liste zugeordnet werden soll.

   ![GeoIP-Länderkarten hinzufügen](/help/assets/cdn/fastly-geo-code.png)

1. Klicken Sie oben auf der Seite auf **Konfiguration speichern** .

1. Wählen Sie nach dem Neuladen der Seite im Abschnitt _Schnelle Konfiguration_ die Option **VCL auf Fastly hochladen**.

>[!NOTE]
>
>Die aktuelle Adobe Commerce Fastly GeoIP-Modulimplementierung unterstützt keine Umleitungen zwischen mehreren Websites.

Fastly bietet außerdem eine Reihe von [geolocation-bezogenen VCL-Funktionen](https://developer.fastly.com/reference/vcl/variables/geolocation/) für benutzerdefinierte Geolocation-Codierung.

## Fastly Edge-Module aktivieren

Fastly Edge Module ist ein flexibles Framework, das die Definition von UI-Komponenten und zugehörigen VCL-Code über eine Vorlage ermöglicht. Diese Module erleichtern die Anpassung und Erweiterung der Fastly-Dienstkonfiguration über die Benutzeroberfläche, anstatt benutzerdefinierte VCL-Snippets zu verwenden.

Mit Edge-Modulen können Sie bestimmte Funktionen wie CORS-Kopfzeilen, Cloud Sitemap-Neuschreibungen aktivieren und die Integration zwischen Ihrem Adobe Commerce-Store und anderen CMS oder Back-Ends konfigurieren.

Um auf das Menü &quot;Edge-Module&quot;zuzugreifen, um die verfügbaren Module anzuzeigen, zu konfigurieren und zu verwalten, aktivieren Sie die Option _Fastly Edge modules aktivieren_ . Siehe [Fastly Edge Modules](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) in der Dokumentation zum Fastly CDN-Modul.

## Konfigurieren von Backends und Origin-Shirting

Back-End-Einstellungen bieten eine Feinabstimmung für eine schnelle Leistung mit Origin-Shirting und Timeouts. Ein _Backend_ ist ein bestimmter Ort (IP oder Domäne) mit konfigurierten Einstellungen für den Herkunftsschutz und die Zeitüberschreitung zum Überprüfen und Bereitstellen zwischengespeicherter Inhalte.

_Origin shielding_ leitet alle Anforderungen für Ihren Store an einen bestimmten Point of Presence (POP) weiter. Wenn eine Anforderung empfangen wird, prüft das POP, ob der Inhalt im Cache gespeichert wurde, und stellt ihn bereit. Wenn er nicht zwischengespeichert wird, wird er an das Schild POP weitergeleitet und dann an den Herkunftsserver, der den Inhalt zwischenspeichert. Die Schilder reduzieren den Traffic direkt auf den Ursprung.

Der standardmäßige Fastly VCL-Code gibt Standardwerte für die Herkunftssicherung und Zeitüberschreitungen für Ihre Adobe Commerce auf Cloud-Infrastruktur-Sites an. In einigen Fällen müssen Sie möglicherweise die Standardwerte ändern. Wenn Sie beispielsweise die Fehler &quot;Time to First Byte (TTFB)&quot;erhalten, müssen Sie möglicherweise den Wert _first byte timeout_ anpassen.

>[!NOTE]
>
>Wenn Ihre Site über eine Backend-Integration wie [Wordpress](fastly-vcl-wordpress.md) funktional bereitgestellt werden muss, passen Sie Ihre Fastly-Dienstkonfiguration an, um das Backend hinzuzufügen und Umleitungen von Ihrem Adobe Commerce-Store zu Wordpress zu verwalten. Weitere Informationen finden Sie unter [Fastly Edge Module - Other CMS/Backend integration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in der Dokumentation zum Fastly-Modul.

**Überprüfen der Konfiguration der Backend-Einstellungen**:

{{admin-login-step}}

1. Klicken Sie auf &quot;**Stores**&quot;> &quot;Einstellungen&quot;> &quot;**Konfiguration**&quot;> &quot;**Erweitert**&quot;> &quot;**System**&quot;und erweitern Sie &quot;**Vollständiger Seiten-Cache**&quot;.

1. Erweitern Sie den Abschnitt **Schnelle Konfiguration** .

1. Erweitern Sie **Backend-Einstellungen** und wählen Sie das Zahnrad aus, um das standardmäßige Backend zu überprüfen. Ein Modal wird geöffnet, das aktuelle Einstellungen mit Optionen zum Ändern anzeigt.

   ![Ändern des Backend](../../assets/cdn/fastly-backend.png)

1. Wählen Sie die Position **Schild** (oder das Rechenzentrum) aus.

   Die Standardkonfiguration Schnell für Ihr Projekt legt den Standort fest, der Ihrer Cloud Service-Region am nächsten ist. Wenn Sie es ändern müssen, wählen Sie einen Speicherort neben dem Standardspeicherort aus.

1. Ändern Sie die Timeout-Werte (in Mikrosekunden) für die Verbindung zum Schild, die Zeit zwischen Bytes und die Zeit für das erste Byte. Es wird empfohlen, die standardmäßigen Timeout-Einstellungen beizubehalten.

1. Wählen Sie optional **Backend und Schild nach Bearbeiten oder Speichern aktivieren** aus.

1. Klicken Sie auf **Hochladen** , um Ihre Änderungen zu speichern und sie auf die Fastly-Server hochzuladen.

1. Wählen Sie im Admin **Konfiguration speichern** aus.

Weitere Informationen finden Sie im Leitfaden für Backend-Einstellungen ](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) in der Dokumentation zum Fastly-Modul.[

## Grundlegende Authentifizierung

Grundlegende Authentifizierung ermöglicht den Schutz aller Seiten und Assets auf Ihrer Site.
mit einem Benutzernamen und Kennwort. Wir empfehlen **nicht,** zur Aktivierung der grundlegenden
Authentifizierung in Ihrer Produktionsumgebung. Sie können sie beim Staging konfigurieren
, um Ihre Site während des Entwicklungsprozesses zu schützen. Siehe [Grundlegendes Authentifizierungshandbuch](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) in der Dokumentation zum Fastly CDN-Modul.

Wenn Sie Benutzerzugriff hinzufügen und grundlegende Authentifizierung für das Staging aktivieren, können Sie weiterhin
auf den Admin zugreifen, ohne zusätzliche Anmeldeinformationen zu benötigen.

## Erstellen benutzerdefinierter VCL-Snippets

Fastly unterstützt eine angepasste Version der Varnish Configuration Language (VCL), um die Konfiguration des Fastly-Dienstes anzupassen. Sie können beispielsweise mithilfe von VCL-Codeblöcken mit ACL-Wörterbüchern (Edge and Access Control List) den Zugriff für bestimmte Benutzer oder IP-Adressen zulassen, blockieren oder umleiten.

Anweisungen zum Erstellen benutzerdefinierter VCL-Snippets, Edge-Wörterbücher und ACLs finden Sie unter [Benutzerdefinierte Fastly VCL-Snippets](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Bevor Sie Ihrer Fastly-Modulkonfiguration benutzerdefinierten VCL-Code, Edge-Wörterbücher und ACLs hinzufügen, überprüfen Sie, ob der Fastly-Caching-Dienst mit der Standardkonfiguration funktioniert. Siehe [Schnelles Einrichten](fastly-configuration.md).

## Domänen verwalten

Für sowohl Starter- als auch Pro-Projekte können Sie die Option [!UICONTROL Domains] verwenden, um die Konfiguration der Fastly-Domäne für Ihren Store hinzuzufügen und zu verwalten.

- Wechseln Sie bei Einstiegsprojekten zur Projekt-URL auf der Registerkarte [!UICONTROL Domains] in der Registerkarte [!DNL Cloud Console], um Ihre Projekt-URL hinzuzufügen.

- Senden Sie für Pro-Projekte ein [Adobe Commerce-Supportticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Domäne Ihrer Cloud-Projektkonfiguration hinzuzufügen. Das Supportteam aktualisiert auch die Adobe Commerce Fastly-Kontokonfiguration, um die Domäne hinzuzufügen.

**So verwalten Sie die Konfiguration der Fastly-Domäne über den Admin**:

{{admin-login-step}}

1. Wählen Sie **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** aus und erweitern Sie den **vollständigen Seiten-Cache**.

1. Wählen Sie im Abschnitt Admin _Schnelle Konfiguration_ die Option **Domänen** aus.

1. Klicken Sie auf **Domänen verwalten** , um die Seite Domänen zu öffnen.

1. Fügen Sie die Namen der obersten und untergeordneten Domänen für die Stores in der Cloud-Umgebung hinzu.

   Sie können nur Domänen angeben, die bereits zur Cloud-Infrastrukturkonfiguration hinzugefügt wurden.

   ![Schnellste Domänenkonfiguration für Starter hinzufügen](../../assets/cdn/fastly-starter-activate-domain.png)

1. Klicken Sie auf **Aktivieren** , um die Konfiguration der Fastly-Domäne zu aktualisieren.

>[!NOTE]
>
>Wenn dieselbe Domäne für ein anderes Fastly-Konto konfiguriert wurde, müssen Sie ein Adobe Commerce-Supportticket senden, um die Delegation der Domäne anzufordern, bevor Sie die Domäne zu Adobe Commerce hinzufügen können. Siehe [Mehrere schnelle Konten und zugewiesene Domänen](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Wartungsmodus aktivieren

Verwenden Sie die Option _Wartungsmodus_ , um den administrativen Zugriff auf Ihre Site von bestimmten IP-Adressen aus zuzulassen, während eine Fehlerseite für alle anderen Anforderungen zurückgegeben wird.

**Aktivieren des Wartungsmodus mit Administratorzugriff**:

1. Öffnen Sie den Abschnitt _Schnelle Konfiguration_ im Admin.

1. Aktualisieren Sie im Abschnitt _Edge ACL_ die Zugriffssteuerungsliste (ACL) mit den administrativen IP-Adressen, die auf Ihren Speicher zugreifen können, während er sich im Wartungsmodus befindet.`maint_allow`

   ![Aktualisieren der Zulassungsliste des IP-Wartungsmodus](../../assets/cdn/fastly-maint-allowlist.png)

1. Wählen Sie im Abschnitt _Wartungsmodus_ die Option **Wartungsmodus aktivieren**.

   Nachdem Sie den Wartungsmodus aktiviert haben, wird der gesamte Traffic blockiert, mit Ausnahme der Anforderungen von IP-Adressen in der ACL `maint_allowlist` . Sie können die `maint_allowlist` aktualisieren, um die IP-Adressen in der ACL zu ändern.

   Detaillierte Konfigurationsanweisungen finden Sie im Leitfaden für den Wartungsmodus ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) in der Dokumentation zum Fastly CDN für Magento 2-Modul.[
