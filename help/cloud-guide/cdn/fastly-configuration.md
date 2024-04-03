---
title: Fastly Services konfigurieren
description: Erfahren Sie, wie Sie Fastly-Dienste für Ihr Adobe Commerce-Projekt einrichten und konfigurieren.
feature: Cloud, Configuration, Iaas, Cache, Security
exl-id: c53ff3bd-3df2-45fb-933e-d3b29f7edf4e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 0%

---

# Fastly Services konfigurieren

Für Adobe Commerce ist in Staging- und Produktionsumgebungen der Cloud-Infrastruktur eine schnelle Bereitstellung erforderlich.

Schnell arbeitet mit Varnish zusammen, um schnelle Caching-Funktionen und eine [Netzwerk zur Inhaltsbereitstellung](https://glossary.magento.com/content-delivery-network) (CDN) für statische Assets. Schnell stellt auch eine Web Application Firewall (WAF) bereit, um Ihre Site und Cloud-Infrastruktur zu schützen. Um Ihre Site und die Cloud-Infrastruktur vor bösartigem Traffic und Angriffen zu schützen, leiten Sie den gesamten eingehenden Site-Traffic schnell weiter.

>[!NOTE]
>
>Fastly ist nicht in Integrationsumgebungen verfügbar.

Führen Sie die folgenden Schritte aus, um Fastly zu einem frühen Zeitpunkt in Ihrem Site-Entwicklungsprozess zu aktivieren, zu konfigurieren und zu testen, um einen sicheren Zugriff auf Ihre Site zu ermöglichen.

- Schnelles Abrufen von Anmeldeinformationen für Staging- und Produktionsumgebungen
- Fastly-CDN-Zwischenspeicherung aktivieren
- Fastly VCL-Snippets hochladen
- DNS-Konfiguration aktualisieren, um Traffic zum Fastly-Dienst zu leiten
- Schnelles Zwischenspeichern testen

>[!NOTE]
>
>Nachdem Sie die anfängliche Fastly-Konfiguration aktiviert und überprüft haben, können Sie die Konfiguration anpassen. Sie können beispielsweise zusätzliche Optionen wie Bildoptimierung, Edge-Module und benutzerdefinierten VCL-Code aktivieren. Siehe [Cache-Konfiguration anpassen](fastly-custom-cache-configuration.md).

## Schnelles Abrufen von Anmeldedaten

Während der Projektbereitstellung fügt Adobe Ihr Projekt zum [Schnelles Dienstkonto](fastly.md#fastly-service-account-and-credentials) für Adobe Commerce in der Cloud-Infrastruktur und erstellt Fastly-Kontoanmeldeinformationen für den Starter `master` und Pro Staging- und Produktionsumgebungen. Jede Umgebung verfügt über eindeutige Anmeldeinformationen.

Sie benötigen die Fastly-Anmeldeinformationen, um Fastly CDN-Dienste vom Admin zu konfigurieren und schnelle API-Anfragen zu senden.

>[!NOTE]
>
>Mit Adobe Commerce in der Cloud-Infrastruktur können Sie nicht direkt auf den Schnelladministrator zugreifen. Verwenden Sie den Administrator , um die Schnelle Konfiguration für Ihre Umgebungen zu überprüfen und zu aktualisieren. Wenn Sie ein Problem nicht mit den Schnellfunktionen in Admin lösen können, senden Sie eine [Support-Ticket für Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

Verwenden Sie die folgenden Methoden, um die Fastly-Dienst-ID und das API-Token für Ihre Umgebung zu finden und zu speichern:

**So zeigen Sie Ihre Fastly-Anmeldedaten an**:

Die Methode zum Anzeigen von Anmeldedaten unterscheidet sich bei Pro- und Starter-Projekten.

- Von IaaS bereitgestellter freigegebener Ordner: Verwenden Sie in Pro-Projekten SSH, um eine Verbindung zu Ihrem Server herzustellen und die Fastly-Anmeldeinformationen von der `/mnt/shared/fastly_tokens.txt` -Datei. Staging- und Produktionsumgebungen verfügen über eindeutige Anmeldeinformationen. Sie müssen die Anmeldeinformationen für jede Umgebung abrufen.

- Lokaler Arbeitsbereich - Verwenden Sie in der Befehlszeile den `magento-cloud` CLI bis [Liste und Überprüfung](../environment/variables-cloud.md#viewing-environment-variables) Schnelle Umgebungsvariablen.

  ```bash
  magento-cloud variable:get -e <environment-ID>
  ```

- [!DNL Cloud Console]—Überprüfen Sie die folgenden Umgebungsvariablen in der [Umgebungskonfiguration](../project/overview.md#configure-environment).

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_API_KEY`

   - `CONFIG__DEFAULT__SYSTEM__FULL_PAGE_CACHE__FASTLY__FASTLY_SERVICE_ID`

>[!NOTE]
>
>Wenn Sie die Fastly-Anmeldeinformationen für die Staging- oder Produktionsumgebungen nicht finden können, wenden Sie sich an Ihren Adobe Customer Technical Advisor (CTA).

## Schnelles Zwischenspeichern aktivieren

Sie benötigen die folgenden Komponenten, um Fastly-Dienste zu aktivieren und zu konfigurieren:

- Neueste Version der [Fastly CDN für Magento 2-Modul](fastly.md#fastly-cdn-module-for-magento-2) in den Staging- und Produktionsumgebungen installiert. Siehe [Schnelles Upgrade](#upgrade-the-fastly-module).

- [Schnelle Anmeldeinformationen](#get-fastly-credentials) für Adobe Commerce in Staging- und Produktionsumgebungen der Cloud-Infrastruktur

**So aktivieren Sie die schnelle CDN-Zwischenspeicherung in Staging und Produktion**:

{{admin-login-step}}

1. Klicks **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** und erweitern **Vollständiger Seiten-Cache**.

   ![Zum Auswählen schnell erweitern](../../assets/cdn/fastly-menu.png)

1. Im _Caching-Anwendung_ -Abschnitt, die Auswahl aus **Systemwert verwenden** und wählen Sie **Fastly CDN** aus der Dropdown-Liste.

   ![Schnell auswählen](../../assets/cdn/fastly-enable-admin.png)

1. Erweitern **Schnelle Konfiguration** und [Zwischenspeicheroptionen auswählen](https://github.com/fastly/fastly-magento2/blob/master/Documentation/CONFIGURATION.md#configure-the-module).

1. Klicken Sie nach dem Konfigurieren der Zwischenspeicheroptionen auf **Konfiguration speichern** oben auf der Seite.

1. Löschen Sie den Cache gemäß der Benachrichtigung.

1. Fahren Sie mit der Konfiguration von Fastly fort, indem Sie zurück zu **Stores** > **Einstellungen** > **Konfiguration** > **Erweitert** > **System** > **Schnelle Konfiguration**.

### Schnelles Testen von Anmeldeinformationen

1. Navigieren Sie im Admin zu **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** > **Schnelle Konfiguration**.

1. Fügen Sie bei Bedarf die **Fastly Service ID** und **API-Token** -Werte für Ihre Projektumgebung.

   ![Schnelle Anmeldeinformationen - Admin](../../assets/cdn/fastly-credentials-admin-ui.png)

   >[!NOTE]
   >
   >Wählen Sie den Link nicht aus, um das Fastly API-Token zu erstellen. Verwenden Sie stattdessen die [Schnelle Anmeldedaten (Dienst-ID und API-Token), die von Adobe bereitgestellt werden](#get-fastly-credentials) bereitgestellt von Adobe.

1. Klicks **Testen von Anmeldeinformationen**.

1. Wenn der Test erfolgreich ist, klicken Sie auf **Konfiguration speichern** und leeren Sie dann den Cache.

   Wenn der Test fehlschlägt, überprüfen Sie, ob die richtigen Dienst-ID- und API-Token-Werte mit den Anmeldeinformationen für die aktuelle Umgebung übereinstimmen.

   Wenn der Test erneut fehlschlägt, senden Sie ein Adobe Commerce-Supportticket oder kontaktieren Sie Ihren Adobe-Kundenbetreuer. Schließen Sie bei Pro-Projekten die URLs für Ihre Produktions- und Staging-Sites ein. Schließen Sie bei Einstiegsprojekten die URLs für Ihre `Master` und Staging-Site.

>[!NOTE]
>
>Anweisungen zum Ändern der Fastly-API-Token-Anmeldeinformationen für eine Staging- oder Produktionsumgebung finden Sie unter [Fastly-Anmeldeinformationen ändern](fastly.md#change-fastly-api-token).

### VCL schnell hochladen

Laden Sie nach der Aktivierung des Fastly-Moduls die standardmäßige [VCL-Code](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets) zu den Fastly-Servern. Dieser Code bietet eine Reihe von VCL-Snippets, die die Konfigurationseinstellungen zum Aktivieren der Zwischenspeicherung und anderer Fastly CDN-Dienste für Ihre Adobe Commerce in der Cloud-Infrastruktur festlegen.

>[!NOTE]
>
>Fastly-Caching-Dienste funktionieren erst, wenn Sie den ersten Upload des Fastly VCL-Codes auf die Adobe Commerce-Staging- und -Produktions-Sites abgeschlossen haben.

**Hochladen der Fastly VCL**:

1. Im _Schnelle Konfiguration_ Abschnitt, klicken Sie auf **VCL schnell hochladen** wie in der folgenden Abbildung dargestellt.

   ![Laden Sie eine Magento VCL schnell hoch.](../../assets/cdn/fastly-upload-vcl-admin.png)

1. Nach Abschluss des Uploads aktualisieren Sie den Cache gemäß der Benachrichtigung oben auf der Seite.

## Bereitstellen von SSL-/TLS-Zertifikaten

Adobe stellt ein domänenvalidiertes SSL-/TLS-Zertifikat zur Verfügung, das den sicheren HTTPS-Traffic von Fastly aus verschlüsselt. Adobe stellt für jede Pro Production-, Staging- und Starter Production-Umgebung ein Zertifikat bereit, um alle Domänen in dieser Umgebung zu schützen. Ausführliche Informationen zum bereitgestellten Zertifikat finden Sie unter [Adobe von SSL-Zertifikaten (TLS) für Adobe Commerce in der Cloud-Infrastruktur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq.html).

>[!NOTE]
>
>Sie können Ihr eigenes TLS- oder SSL-Zertifikat bereitstellen, anstatt das von Adobe bereitgestellte Zertifikat &quot;Let&#39;s Encrypt&quot;zu verwenden. Dieser Prozess erfordert jedoch zusätzliche Arbeit für die Einrichtung und Wartung. Um diese Option zu wählen, senden Sie ein Adobe Commerce-Supportticket oder arbeiten Sie mit Adobe zusammen, um Ihrer Adobe Commerce benutzerdefinierte gehostete Zertifikate in Cloud-Infrastrukturumgebungen hinzuzufügen.

Um die SSL-/TLS-Zertifikate für Adobe Commerce-Umgebungen zu aktivieren, führt die Adobe-Automatisierung die folgenden Schritte aus:

- Überprüfen des Domänenbesitzes
- Stellt ein SSL-/TLS-Zertifikat bereit, das bestimmte Top-Level- und Subdomains für Ihre Stores abdeckt.
- Lädt das Zertifikat in die Cloud-Umgebung hoch, wenn die Site live ist

Für diese Automatisierung müssen Sie die DNS-Konfiguration für Ihre Site aktualisieren, um Informationen zur Domänenvalidierung bereitzustellen. Verwendung **one** der folgenden Methoden:

- **DNS-Validierung**-Aktualisieren Sie bei Live-Sites Ihre DNS-Konfiguration mit CNAME-Einträgen, die auf den Fastly-Dienst verweisen.
- **ACME-Challenge CNAME-Einträge**-Aktualisieren Sie Ihre DNS-Konfiguration mit ACME-Challenge-CNAME-Einträgen, die von Adobe für jede Domäne in Ihrer Umgebung bereitgestellt werden.

>[!TIP]
>
>Wenn Sie eine Produktionsdomäne haben, die nicht aktiv ist, verwenden Sie die CNAME-Einträge für die ACME-Anfrage zur Domänenvalidierung. Durch frühzeitiges Hinzufügen der Einträge zur DNS-Konfiguration kann Adobe das SSL-/TLS-Zertifikat mit den richtigen Domänen bereitstellen, bevor die Site gestartet wird. Bevor Sie mit der Produktion beginnen, müssen Sie diese Platzhalterdatensätze durch die von Adobe bereitgestellten CNAME-Einträge ersetzen.

Wenn die Domänenvalidierung abgeschlossen ist, stellt Adobe das TLS/SSL-Zertifikat verschlüsseln bereit und lädt es in die Live-Staging- oder Produktionsumgebungen hoch. Dieser Vorgang kann bis zu 12 Stunden dauern. Es wird empfohlen, die DNS-Konfigurationsaktualisierungen einige Tage im Voraus durchzuführen, um Verzögerungen bei der Site-Entwicklung und beim Website-Start zu vermeiden.

## DNS-Konfiguration mit Entwicklungsparametern aktualisieren

Während des anfänglichen Einrichtungsprozesses können Sie die folgenden URLs verwenden, um die schnelle Zwischenspeicherung in Staging- und Produktionsumgebungen zu konfigurieren und zu testen:

- Für Pro Staging und Produktion:

   - `mcprod.<your-domain>.com`
   - `mcstaging.<your-domain>.com`

- Nur für Starterproduktion:

   - `mcprod.<your-domain>.com`

Diese standardmäßigen Pre-Production-URLs sind verfügbar, nachdem Ihr Projekt bereitgestellt wurde. Der Wert für `"your-domain"` ist der Domänenname, den Sie beim Onboarding-Prozess angegeben haben.

>[!NOTE]
>
>Sie können in Starter-Projekten keine benutzerdefinierte Domäne für eine Nicht-Produktionsumgebung angeben.

Um Traffic von Ihren Store-URLs an den Fastly-Dienst zu leiten, aktualisieren Sie Ihre DNS-Konfiguration. Wenn Sie die Konfiguration aktualisieren, stellt Adobe automatisch die erforderlichen SSL-/TLS-Zertifikate bereit und lädt sie in Ihre Cloud-Umgebungen hoch. Diese Bereitstellung kann bis zu 12 Stunden dauern.

>[!NOTE]
>
>Wenn Sie bereit sind, Ihre Produktions-Site zu starten, müssen Sie die DNS-Konfiguration erneut aktualisieren, um Ihre Produktionsdomänen auf den Fastly-Dienst zu verweisen und zusätzliche Konfigurationsaufgaben durchzuführen. Siehe [Checkliste für Launch](../launch/checklist.md).

**Voraussetzungen:**

- Aktivieren Sie das Fastly-Modul.
- Laden Sie den standardmäßigen Fastly VCL-Code hoch.
- Stellen Sie für jede Umgebung eine Liste mit Top-Level- und Subdomains zur Adobe bereit oder senden Sie ein Adobe Commerce Support-Ticket.
- Warten Sie auf die Bestätigung, dass die angegebenen Domänen zu Ihren Cloud-Umgebungen hinzugefügt wurden.
- Fügen Sie bei Starter-Projekten die Domänen Ihrer Fastly-Service-Konfiguration hinzu. Siehe [Domänen verwalten](fastly-custom-cache-configuration.md#manage-domains).
- Informationen zum Aktualisieren der DNS-Konfiguration erhalten Sie bei Ihrem [DNS-Registrar](https://lookup.icann.org/) für die richtige Methode für Ihren Domain-Dienst.

**So aktualisieren Sie Ihre DNS-Konfiguration für die Entwicklung**:

1. Verweisen Sie die Pre-Production-URLs auf den Fastly-Dienst, indem Sie CNAME-Einträge hinzufügen: `prod.magentocloud.map.fastly.net`, zum Beispiel:

   | Domäne oder Subdomäne | CNAME |
   |---------------------------|----------------------------------|
   | mcprod.your-domain.com | prod.magentocloud.map.fastly.net |
   | mcstaging.your-domain.com | prod.magentocloud.map.fastly.net |

   Wenn die CNAME-Einträge aktiv sind, stellt Adobe Zertifikate bereit und lädt die SSL-/TLS-Zertifikate hoch.

   >[!NOTE]
   >
   >Wenn Sie planen, Apex-Domänen (`your-domain.com`) für Ihre Produktions-Site müssen Sie DNS-Adressdatensätze (A-Datensätze) so konfigurieren, dass sie auf die Fastly-Server-IP-Adressen verweisen. Siehe [DNS-Konfiguration mit Produktionseinstellungen aktualisieren](../launch/checklist.md#to-update-dns-configuration-for-site-launch).


1. Fügen Sie ACME-Challenge-CNAME-Einträge für die Domänenvalidierung und Vorbereitstellung von SSL-/TLS-Produktionszertifikaten hinzu, z. B.:

   | Domäne oder Subdomäne | CNAME |
   |-------------------------------------------|-------------------------------------------|
   | _acme-challenge.your-domain.com | 0123456789abcdef.validation.magento.cloud |
   | _acme-challenge.www.your-domain.com | 9573186429stuvwx.validation.magento.com |
   | _acme-challenge.mystore.your-domain.com | 1234567898zxywvu.validation.magento.cloud |
   | _acme-challenge.subdomain.your-domain.com | 1098765743lmnopq.validation.magento.cloud |

   >[!NOTE]
   >
   >Die ACME-Anforderungsdatensätze in diesem Beispiel sind Platzhalter, die nicht zur Bereitstellung Ihrer Adobe Commerce-Staging- und -Produktionsstandorte vorgesehen sind. Erhalten Sie die richtigen ACME-Provokations-Datensatzinformationen für Ihr Projekt, indem Sie sich an Adobe wenden.

   Nachdem Sie die CNAME-Einträge hinzugefügt haben, validiert Adobe die Domänen und stellt das SSL-/TLS-Zertifikat für die Umgebung bereit. Wenn Sie die DNS-Konfiguration aktualisieren, um den Traffic von diesen Domänen zum Fastly-Dienst zu leiten, lädt Adobe das Zertifikat in die Umgebung hoch.

1. Aktualisieren Sie die Adobe Commerce-Basis-URL.

   - Verwenden Sie SSH, um sich bei der Produktionsumgebung anzumelden.

     ```bash
     magento-cloud ssh
     ```

   - Verwenden Sie die Cloud-CLI, um die Basis-URL für Ihren Store zu ändern.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://mcstaging.your-domain.com/"
     ```

   >[!NOTE]
   >
   >Alternativ zur Verwendung der Cloud-CLI können Sie die Basis-URL über die [Admin](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html)

1. Starten Sie den Webbrowser neu.

1. Testen Sie Ihre Website.

## Schnelles Zwischenspeichern testen

Nachdem Sie die DNS-Konfigurationsänderungen abgeschlossen haben, verwenden Sie die [cURL](https://curl.se/) Befehlszeilen-Tool, um zu überprüfen, ob der Fastly-Cache funktioniert.

**Überprüfen der Antwortheader**:

1. Verwenden Sie in einem Terminal Folgendes: `curl` -Befehl zum Testen Ihrer Live-Site-URL:

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 https://<live-URL>
   ```

   Wenn Sie keine statische Route festgelegt oder die DNS-Konfiguration für die Domänen auf Ihrer Live-Site abgeschlossen haben, verwenden Sie die `--resolve` -Markierung, die die DNS-Namensauflösung umgeht.

   ```bash
   curl -vo /dev/null -H Fastly-Debug:1 --resolve <live-URL-hostname>:443:<live-IP-address>
   ```

1. Überprüfen Sie in der Antwort die [Kopfzeilen](fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) um sicherzustellen, dass Fastly funktioniert. Folgende eindeutige Header sollten in der Antwort angezeigt werden:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Wenn die Header nicht über die richtigen Werte verfügen, lesen Sie [Beheben von Fehlern in den Antwortheadern](fastly-troubleshooting.md#curl) für Hilfe zur Fehlerbehebung.

## Upgrade des Fastly-Moduls

Aktualisiert das Fastly CDN für Magento 2-Modul schnell, um Probleme zu beheben, die Leistung zu steigern und neue Funktionen bereitzustellen.
Wir empfehlen, das Fastly-Modul in Ihren Staging- und Produktionsumgebungen auf die [neueste Version](https://github.com/fastly/fastly-magento2/blob/master/VERSION).

Nach der Aktualisierung des Moduls müssen Sie den VCL-Code hochladen, um die Änderungen auf die Fastly-Dienstkonfiguration anzuwenden.

>[!WARNING]
>
> Wenn Sie den standardmäßigen Fastly VCL-Code mit einer benutzerdefinierten Version angepasst haben, überschreibt das Upgrade des Fastly-Moduls Ihre Änderungen. Wenn Sie benutzerdefinierte VCL-Snippets mit eindeutigen Namen hinzugefügt haben, werden diese Änderungen während des Aktualisierungsprozesses beibehalten. Es empfiehlt sich, die Staging-Umgebung zu aktualisieren und die Änderungen zu validieren, bevor sie auf die Produktionsumgebung angewendet werden.

**Überprüfen der Version des Fastly CDN-Moduls für Magento 2**:

1. Wechseln Sie zum Stammverzeichnis Ihrer Cloud-Umgebung.

1. Überprüfen Sie mithilfe von Composer die installierte Version.

   ```bash
   composer show *fastly*
   ```

1. Wenn die Variable [neueste Version](https://github.com/fastly/fastly-magento2/releases) nicht installiert ist, führen Sie die Schritte zum Aktualisieren des Fastly-Moduls aus.

**So aktualisieren Sie das Fastly-Modul**:

1. Verwenden Sie in Ihrer lokalen Integrationsumgebung die folgenden Modulinformationen, um [Aktualisieren des Fastly-Moduls](../store/extensions.md#upgrade-an-extension).

   ```text
   module name: fastly/magento2
   repository: https://github.com/fastly/fastly-magento2.git
   ```

1. Senden Sie Ihre Aktualisierungen an die Staging-Umgebung.

1. Melden Sie sich bei Admin für Ihre Staging-Umgebung bei an. [VCL-Code hochladen](#upload-vcl-to-fastly).

1. [Schnelle Dienste überprüfen](fastly-troubleshooting.md#verify-or-debug-fastly-services) auf der Adobe Commerce Staging-Site.

Nachdem Sie die Fastly-Dienste auf der Staging-Site überprüft haben, wiederholen Sie den Aktualisierungsprozess in der Produktionsumgebung.

>[!TIP]
>
> Wenn Sie Probleme mit Fastly-Diensten in Ihren Adobe Commerce-Umgebungen haben, lesen Sie den Abschnitt [Adobe Commerce - Schnellere Fehlerbehebung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/magento-fastly-troubleshooter.html).
