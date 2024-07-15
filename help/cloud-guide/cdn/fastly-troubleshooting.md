---
title: Schnelle Fehlerbehebung
description: Erfahren Sie, wie Sie das Fastly CDN-Modul und die Services für Adobe Commerce beheben und verwalten.
feature: Cloud, Configuration, Cache, Services
exl-id: e4c47035-cbad-4838-8d44-fa5eaaac42d1
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Schnelle Fehlerbehebung

Verwenden Sie die folgenden Informationen, um das Fastly CDN-Modul für Magento 2 in Ihrer Adobe Commerce in Cloud-Infrastruktur-Projektumgebungen zu beheben und zu verwalten. Sie können beispielsweise die Werte der Antwortheader und das Cache-Verhalten untersuchen, um Probleme mit dem schnellen Service und der Leistung zu beheben.

In Pro-Produktions- und Staging-Umgebungen können Sie [New Relic-Protokolle](../monitor/log-management.md) verwenden, um CDN- und WAF-Protokolldaten schnell anzuzeigen und zu analysieren, um Fehler und Leistungsprobleme zu beheben.

>[!NOTE]
>
>Informationen zum Einrichten und Konfigurieren von Fastly finden Sie unter [Fastly einrichten](fastly.md).

## Fastly Service ID suchen

Sie benötigen die Fastly-Dienst-ID, um eine schnelle Konfiguration über den Administrator durchzuführen oder um Fastly-API-Anfragen für erweiterte schnelle Konfiguration und Fehlerbehebung zu senden.

Wenn Fastly in Ihrer Projektumgebung aktiviert ist, können Sie die Dienst-ID vom Admin abrufen. Siehe [Schnelle Anmeldeinformationen abrufen](fastly-configuration.md#get-fastly-credentials).

Entwickler und fortgeschrittene VCL-Benutzer können benutzerdefinierte VCL verwenden, um die Dienst-ID mit der Fastly-Variablen `req.service_id` abzurufen. Sie können beispielsweise die `req.service_id` zur benutzerdefinierten Protokollierungsrichtlinie in Ihrer VCL hinzufügen, um den Dienst-ID-Wert zu erfassen:

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

Sie können denselben VCL für Produktions- und Staging-Umgebungen verwenden. Siehe [Konfigurieren von vcl_log](https://support.fastly.com/hc/en-us/community/posts/360040447172-How-to-configure-vcl-log).

## Probleme mit der Site-Leistung, -Bereinigung und -Cache

Verwenden Sie die folgende Liste, um Probleme im Zusammenhang mit der Konfiguration des Fastly-Dienstes für Ihre Adobe Commerce in der Cloud-Infrastruktur-Umgebung zu identifizieren und zu beheben.

- **Menü &quot;Store&quot;wird nicht angezeigt oder funktioniert nicht** - Möglicherweise verwenden Sie einen Link oder einen temporären Link direkt zum Herkunftsserver, anstatt die Live-Site-URL zu verwenden, oder Sie haben `-H "host:URL"` in einem [cURL-Befehl](#check-live-site-through-fastly) verwendet. Wenn Sie die Option Schnell zum Herkunftsserver umgehen, funktioniert das Hauptmenü nicht und falsche Kopfzeilen werden angezeigt, die das Zwischenspeichern auf der Browserseite zulassen.

- **Obere Navigation funktioniert nicht** - Die obere Navigation beruht auf der Verarbeitung von Edge Side Includes (ESI), die beim Hochladen der standardmäßigen Magento Fastly VCL-Snippets aktiviert wird. Wenn die Navigation nicht funktioniert, lädt [den Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) hoch und überprüft die Site erneut.

- **Geolocation/GeoIP funktioniert nicht** - Die standardmäßigen Magento Fastly VCL-Snippets hängen den Ländercode an die URL an. Wenn der Ländercode nicht funktioniert, lädt [den Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) hoch und überprüft die Site erneut.

- **Seiten werden nicht zwischengespeichert**—Standardmäßig werden keine Seiten mit der Kopfzeile `Set-Cookies` im Cache zwischengespeichert. Adobe Commerce setzt Cookies auch auf zwischenspeicherbaren Seiten (TTL > 0). Die standardmäßige Magento Fastly VCL entfernt diese Cookies auf zwischenspeicherbaren Seiten. Wenn Seiten nicht zwischengespeichert werden, lädt [den Fastly VCL](fastly-configuration.md#upload-vcl-to-fastly) hoch und überprüft die Site erneut.

  Dieses Problem kann auch auftreten, wenn ein Seitenblock in einer Vorlage als unerreichbar markiert ist. In diesem Fall wird das Problem höchstwahrscheinlich durch ein Drittanbietermodul oder eine Erweiterung verursacht, die die Adobe Commerce-Kopfzeilen blockiert oder entfernt. Um das Problem zu beheben, lesen Sie [X-Cache enthält nur MISS, keinen HIT](#x-cache-contains-only-miss-no-hit).

- **Bereinigungsanfragen schlagen fehl**—Beim Senden einer Bereinigungsanforderung wird schnell der folgende Fehler zurückgegeben:

  ```text
  The purge request was not processed successfully.
  ```

  Dieses Problem kann durch eines der folgenden Probleme verursacht werden:

   - Ungültige Fastly-Anmeldeinformationen in der Fastly-Dienstkonfiguration für Adobe Commerce in der Cloud-Infrastruktur-Projektumgebung
   - Ungültiger Code in einem benutzerdefinierten VCL-Snippet

  Informationen zum Beheben des Problems finden Sie unter [Fehler beim Bereinigen des Fastly-Cache in Cloud](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) im Adobe Commerce Help Center.

## 503 Fehler von Fastly

Wenn Fastly 503-Timeout-Fehler zurückgibt, überprüfen Sie die Fehlerprotokolle und die Fehlerseite 503 , um die Grundursache zu identifizieren.

>[!NOTE]
>
>Tritt beim Ausführen von Massenvorgängen die Zeitüberschreitung ein, können Sie die Zeitüberschreitung für den Administrator ](fastly-custom-cache-configuration.md#extend-fastly-timeout) um [verlängern.

Wenn Sie einen 503-Fehler erhalten, überprüfen Sie das Fehlerprotokoll für die Produktions- oder Staging-Umgebung und das php-Zugriffsprotokoll, um das Problem zu beheben.

**Überprüfen der Fehlerprotokolle**:

- [Fehlerprotokoll](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  Dieses Protokoll enthält alle Fehler der Anwendung oder der PHP-Engine, z. B. `memory_limit`- oder `max_execution_time exceeded`-Fehler. Wenn Sie keine Fastly-bezogenen Fehler finden, überprüfen Sie das PHP-Zugriffsprotokoll.

- PHP-Zugriffsprotokoll

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  Suchen Sie im Protokoll nach HTTP-200-Antworten nach der URL, die den 503-Fehler zurückgegeben hat. Wenn Sie die Antwort &quot;200&quot;finden, bedeutet dies, dass Adobe Commerce die Seite ohne Fehler zurückgegeben hat. Dies weist darauf hin, dass das Problem möglicherweise nach dem Intervall aufgetreten ist, das den in der Fastly-Dienstkonfiguration festgelegten `first_byte_timeout` -Wert überschreitet.

Wenn ein 503-Fehler auftritt, gibt Fastly den Grund auf der Fehler- und Wartungsseite zurück. Möglicherweise können Sie den Grund nicht sehen, wenn Sie Code für eine [benutzerdefinierte Antwortseite](fastly-custom-response.md) hinzugefügt haben. Um den Grund-Code auf der Standardfehlerseite anzuzeigen, können Sie den HTML-Code für die benutzerdefinierte Fehlerseite entfernen.

**So überprüfen Sie die Fehlerseite &quot;Fastly 503&quot;**:

{{admin-login-step}}

1. Klicken Sie auf **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System**.

1. Erweitern Sie im rechten Bereich den Eintrag **Vollständiger Seiten-Cache**.

1. Erweitern Sie im Abschnitt **Schnelle Konfiguration** den Eintrag **Benutzerdefinierte synthetische Seiten** , wie in der folgenden Abbildung dargestellt.

   ![Benutzerdefinierte Fehlerseite 503](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Klicken Sie auf **HTML festlegen**.

1. Entfernen Sie den benutzerspezifischen Code. Sie können sie in einem Textprogramm speichern, um sie später erneut hinzuzufügen.

1. Klicken Sie auf **Hochladen** , um Ihre Aktualisierungen schnell zu senden.

1. Klicken Sie oben auf der Seite auf **Konfiguration speichern** .

1. Öffnen Sie die URL, die den 503-Fehler verursacht hat, erneut. Gibt schnell eine Fehlerseite mit dem Grund zurück, wie im folgenden Beispiel gezeigt.

   ![Fastly error](../../assets/cdn/fastly-503-example.png)

## Apex und Subdomänen, die bereits mit einem Fastly-Konto verknüpft sind

Wenn die Apex-Domäne und die Subdomänen für Ihr Adobe Commerce on Cloud-Infrastrukturprojekt bereits mit einem vorhandenen Fastly-Konto mit einer zugewiesenen Service-ID verknüpft sind, können Sie erst starten, nachdem Sie Ihre Schnelle Konfiguration aktualisiert haben:

- Aktualisieren Sie die Konfiguration von apex und subdomain auf dem vorhandenen Fastly-Konto. Siehe [Mehrere schnelle Konten und zugewiesene Domänen](fastly.md#domain).

- [Fastly aktivieren und konfigurieren](fastly-configuration.md#enable-fastly-caching) und die [DNS-Konfiguration](../launch/checklist.md#update-dns-configuration-with-production-settings) abschließen

## Überprüfen oder Debuggen von Fastly-Diensten

Sie können Leistungs- oder Zwischenspeicherungsprobleme für eine Adobe Commerce auf der Cloud-Infrastruktur-Site beheben, indem Sie die Site-URLs testen und die in der Antwort zurückgegebenen Kopfzeilenwerte untersuchen.

### Schnellere Überprüfung der Live-Site

Verwenden Sie die Fastly-API, um die Antwortheader `Fastly-Magento-VCL-Uploaded` und `X-Cache` zu überprüfen, die von Ihrer Live-Site zurückgegeben werden.

Schnelle API-Anfragen werden über die Fastly-Erweiterung übergeben, um eine Antwort von Ihren Ursprungs-Servern zu erhalten. Wenn die Antwort falsche Header zurückgibt, testen Sie die [Herkunftsserver direkt](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**Überprüfen der Antwortheader**:

1. Verwenden Sie in einem Terminal den folgenden `curl`-Befehl, um Ihre Live-Site-URL zu testen:

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   Wenn Sie keine statische Route festgelegt oder die DNS-Konfiguration für die Domänen auf Ihrer Live-Site abgeschlossen haben, verwenden Sie das `--resolve` -Flag, das die DNS-Namensauflösung umgeht.

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >Um diesen Befehl mit der Option `--resolve` verwenden zu können, muss TLS mit Fastly über ein SSL-/TLS-Zertifikat aktiviert sein und die IP-Adresse des Cache-Knotens suchen.

1. Überprüfen Sie in der Antwort die [Kopfzeilen](#check-cache-hit-and-miss-response-headers) , um sicherzustellen, dass Fastly funktioniert. Folgende eindeutige Header sollten in der Antwort angezeigt werden:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Wenn die Header nicht über die richtigen Werte verfügen, finden Sie weitere Informationen unter:

- [Überprüfen des VCL-Uploads](#fastly-vcl-has-not-been-uploaded)

- [X-Cache enthält nur MISS, keinen HIT](#x-cache-contains-only-miss-no-hit)

### Umgehen des schnellen Cache, um Adobe Commerce-Sites zu überprüfen

Wenn der Fastly-Dienst falsche Header zurückgibt, können Sie einen VCL-Snippet erstellen, mit dem Sie Anforderungen senden können, die den Fastly-Cache umgehen. Siehe [Schnellen Cache umgehen](fastly-vcl-bypass-to-origin.md).

Nachdem Sie das VCL-Snippet hinzugefügt haben, verwenden Sie cURL-Befehle, um Anforderungen von der angegebenen IP-Adresse an den Ausgangsserver zu senden. Überprüfen Sie dann die Antworten auf Fehler.

### Überprüfen der Cache-HIT- und MISS-Antwortheader

Stellen Sie sicher, dass die zurückgegebene Antwort die folgenden Informationen enthält:

- Umfasst die Kopfzeile `X-Magento-Tags`

- Der Wert der Kopfzeile `Fastly-Module-Enabled` ist entweder `Yes` oder die Versionsnummer des Fastly for CDN Magento 2-Moduls, das in der Projektumgebung installiert ist

- [Cache-Control: max-age](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) ist größer als 0

- Einstellung [Pragma](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) ist `cache`

Der folgende Ausschnitt aus der Ausgabe des cURL-Befehls zeigt die richtigen Werte für die Header `Pragma`, `X-Magento-Tags` und `Fastly-Module-Enabled`:

```terminal
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>Detaillierte Informationen zu Treffern und Fehlern finden Sie unter [Grundlegendes zu Cache-HIT- und MISS-Kopfzeilen mit abgeschirmten Diensten](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) in der Schnelldokumentation.

### Beheben von Fehlern in Antwortheadern

Dieser Abschnitt enthält Vorschläge zur Behebung von Fehlern, die beim Überprüfen von Antwortheadern mit der Fastly-API zurückgegeben werden.

#### Fastly-Modul ist nicht aktiviert

Wenn das Fastly-Modul nicht aktiviert ist (`Fastly-Module-Enabled: no`) oder die Kopfzeile fehlt, verwenden Sie [SSH, um sich in ](../development/secure-connections.md#connect-to-a-remote-environment) beim Projekt anzumelden. Führen Sie dann den folgenden Befehl aus, um den Modulstatus zu überprüfen.

```bash
php bin/magento module:status Fastly_Cdn
```

Verwenden Sie je nach zurückgegebenem Status die folgenden Anweisungen, um die Konfiguration Fastly zu aktualisieren.

- `Module does not exist`—Wenn das Modul nicht vorhanden ist, installieren und konfigurieren Sie ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) das Fastly CDN Module für Magento 2 in einer Integrationsverzweigung. [ Nach Abschluss der Installation aktivieren und konfigurieren Sie das Modul. Siehe [Schnelles Einrichten](fastly-configuration.md).

- `Module is disabled`—Wenn das Fastly-Modul deaktiviert ist, aktualisieren Sie die Umgebungskonfiguration in einer `integration` -Verzweigung in Ihrer lokalen Umgebung, um sie zu aktivieren. Übertragen Sie dann die Änderungen auf Staging und Produktion. Siehe [Verwalten von Erweiterungen](../store/extensions.md#install-an-extension).

  Wenn Sie [Konfigurationsverwaltung](../store/store-settings.md#configure-store) verwenden, überprüfen Sie den Status des Fastly CDN-Moduls in der Konfigurationsdatei `app/etc/config.php` , bevor Sie Änderungen an die Produktions- oder Staging-Umgebung senden.

  Wenn das Modul in der Datei `config.php` nicht aktiviert ist (`Fastly_CDN => 0`), löschen Sie die Datei und führen Sie den folgenden Befehl aus, um `config.php` mit den neuesten Konfigurationseinstellungen zu aktualisieren.

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### Fast VCL wurde nicht hochgeladen

Wenn die Fastly VCL nicht hochgeladen wurde (`Fastly-Magento-VCL-Uploaded`: `false`), verwenden Sie die Option *VCL hochladen* im Admin, um sie hochzuladen. Siehe [Fastly VCL-Snippets hochladen](fastly-configuration.md#upload-vcl-to-fastly).

#### X-Cache enthält nur MISS, keinen HIT

Wenn die Kopfzeile `X-Cache` `HIT` (`HIT, HIT` oder `HIT, MISS`) enthält, deutet dies darauf hin, dass der zwischengespeicherte Inhalt schnell erfolgreich zurückgegeben wird.

Wenn die Kopfzeile `X-Cache` den Wert `MISS, MISS` aufweist und nicht den Wert `HIT` enthält, führen Sie den Befehl `curl` erneut aus, um sicherzustellen, dass die Seite nicht vor Kurzem aus dem Cache gelöscht wurde.

Wenn Sie dasselbe Ergebnis erhalten, verwenden Sie die [`curl` Befehle](#check-live-site-through-fastly) und überprüfen Sie die [Antwortheader](#check-cache-hit-and-miss-response-headers):

- `Pragma` ist `cache`
- `X-Magento-Tags` vorhanden
- `Cache-Control: max-age` ist größer als 0

Wenn das Problem weiterhin besteht, werden diese Kopfzeilen wahrscheinlich von einer anderen Erweiterung zurückgesetzt. Wiederholen Sie das folgende Verfahren in der Staging-Umgebung, indem Sie alle Erweiterungen deaktivieren und jede einzelne erneut aktivieren, um zu bestimmen, welche Erweiterung die Kopfzeilen zurücksetzt. Nachdem Sie die Erweiterung identifiziert haben, die das Problem verursacht hat, müssen Sie sie in der Produktionsumgebung deaktivieren.

**So identifizieren Sie eine Erweiterung, die Antwortheader zurücksetzt:**

{{admin-login-step}}

1. Navigieren Sie zu **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **Erweitert**.

1. Suchen Sie im Abschnitt *Modulausgabe deaktivieren* im rechten Bereich nach all Ihren Erweiterungen und deaktivieren Sie sie.

1. Klicken Sie auf **Konfiguration speichern**.

1. Klicken Sie auf &quot;**System**&quot;> &quot;**Tools**&quot;> &quot;**Cache-Verwaltung**&quot;.

1. Klicken Sie auf **Magento-Cache leeren**.

1. Führen Sie die folgenden Schritte für jede Erweiterung aus, die möglicherweise Probleme mit Fastly-Kopfzeilen verursacht:

   - Aktivieren Sie jeweils eine Erweiterung, speichern Sie die Konfiguration und leeren Sie den Adobe Commerce-Cache.

   - Führen Sie die [`curl` Befehle](#check-live-site-through-fastly) aus, um die [Antwortheader](#check-cache-hit-and-miss-response-headers) zu überprüfen.

   Wiederholen Sie diesen Vorgang für jede Erweiterung. Wenn die Header für schnelle Antworten nicht mehr angezeigt werden, haben Sie die Erweiterung identifiziert, die Probleme mit Fastly verursacht.

Nachdem Sie die Erweiterung identifiziert haben, die Fastly-Header zurücksetzt, wenden Sie sich für weitere Unterstützung an den Entwickler der Erweiterung. Wir können keine Fehlerbehebungen oder Aktualisierungen bereitstellen, damit Erweiterungen von Drittanbietern mit dem Fastly-Caching funktionieren.

## Schnelle Rollback-Konfiguration

Wenn benutzerspezifische VCL-Snippet-Aktualisierungen oder andere Fastly-Konfigurationsänderungen dazu führen, dass eine Adobe Commerce auf der Cloud-Infrastruktur-Site Fehler beschädigt oder zurückgibt, verwenden Sie den Befehl &quot;Fastly API [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5)&quot;, um zu einer früheren VCL-Version zurückzukehren. Sie können die VCL-Version nicht vom Administrator zurücksetzen.

**Zurücksetzen der VCL-Version**:

1. Um eine Liste der verfügbaren VCL-Versionen für einen Dienst zu erhalten, führen Sie den folgenden Befehl aus

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. Führen Sie den folgenden Befehl aus, um die aktive VCL-Version in eine angegebene Version zu ändern.

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

Weitere Informationen zur Verwendung der Fastly-API zum Überprüfen und Verwalten von VCL finden Sie unter [Verwalten von VCL mithilfe der API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
