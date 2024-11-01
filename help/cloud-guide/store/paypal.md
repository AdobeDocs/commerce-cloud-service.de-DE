---
title: PayPal-Zahlungsmethoden einrichten
description: Einrichten von PayPal-Zahlungsmethoden für Adobe Commerce in der Cloud-Infrastruktur.
feature: Cloud, Checkout, Payments
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
source-git-commit: 196efa316b9998c1980412ad96577d7ce42d4aec
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# PayPal-Zahlungsmethoden einrichten

Adobe Commerce on Cloud Infrastructure bietet ein Onboarding-Tool zur Konfiguration von PayPal Express Checkout-Konten direkt über den Administrator. Dieses Tool ist für ECE 2.1.8 und höher verfügbar. Um die Live-Schaltung und die Tests der Zahlungsmethoden von PayPal besser zu unterstützen, können Sie Ihr PayPal Express Checkout-Konto für Sandbox- oder Produktionskonten aktivieren und konfigurieren.

Sie können entweder das Sandbox- oder das Produktionskonto in jeder Umgebung konfigurieren:

* Legen Sie für Integrations- und Staging-Umgebungen Sandbox-Anmeldeinformationen fest.
* Legen Sie für Ihre Produktionsumgebung Sandbox-Anmeldeinformationen für erste Tests fest und ersetzen Sie sie dann durch Live-Produktionsberechtigungen für einen gestarteten Store.

## PayPal-Konto

Obwohl es am besten ist, ein PayPal-Handelskonto zu verwenden, das vorbereitet und konfiguriert wurde, können Sie über den Administrator ein Konto erstellen oder ein persönliches Konto aktualisieren.

[!DNL PayPal onboarding] unterstützt die Verbindung mit den folgenden Konten:

* PayPal-Geschäftskonto
* Persönliches PayPal-Konto, Konvertierung in ein Geschäftskonto. Wenn Sie über ein bestehendes persönliches PayPal-Konto verfügen, können Sie sich mit diesen Anmeldedaten anmelden und dieses Konto bei Abschluss der Synchronisierung auf ein Geschäftskonto aktualisieren.

Wenn Sie noch kein PayPal-Konto haben, erstellen Sie eines. Geben Sie eine E-Mail-Adresse für ein neues Konto ein. Wenn kein passendes PayPal-Konto gefunden wird, befolgen Sie die Anweisungen zum Erstellen eines PayPal Business-Kontos. Oder Sie können ein Konto direkt über [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection) erstellen.

### PayPal-Einschränkungen

PayPal unterstützt die Anbindung von PayPal Express Checkout für Länder auf der ganzen Welt mit Ausnahme der folgenden Einschränkungen:

* Indien und Japan (künftige PayPal-Aktualisierungen können diese Konten unterstützen)
* Israel

Für Brasilien müssen Sie über ein bestehendes PayPal-Geschäftskonto verfügen, um eine Verbindung herzustellen. Während dieses Vorgangs können Sie kein bestehendes persönliches PayPal-Konto für Brasilien konvertieren. Wenn Sie ein Konto benötigen, erstellen Sie [ein PayPal-Geschäftskonto](https://www.paypal.com/us/webapps/mpp/account-selection).

## PayPal Express-Checkout konfigurieren

So konfigurieren Sie PayPal Express Checkout:

1. Rufen Sie den Administrator für die Umgebung auf.
1. Wählen Sie im linken Navigationsbereich **Geschäfte** > **Konfiguration** und dann **Verkauf** > **Zahlungsmethoden** aus.
1. Wählen Sie für PayPal **Konfigurieren** aus. Konfigurationsfelder werden in erweiterbaren Abschnitten für die Einstellungen &quot;Express Checkout&quot;, &quot;Advertise PayPal Credit&quot;und &quot;Einfach&quot;und &quot;Erweitert&quot;angezeigt.
1. Verbinden Sie Ihr PayPal-Konto. Bis das Konto verbunden ist, sind die zu aktivierenden Optionen deaktiviert. Weitere Informationen zu verfügbaren und unterstützten Konten für die Verbindung und Einschränkungen finden Sie unter [PayPal-Konto](#paypal-account).

   * Um Ihr PayPal-Live-Konto zu verbinden, klicken Sie auf Mit PayPal verbinden und befolgen Sie die Anweisungen. Alle Käufe von Kunden, die ein Live-PayPal verwenden, werden vollständig abgeschlossen und berechnen Kunden aktiv in einem Live-Store.
   * Um Ihr Sandbox-Konto für Tests zu verbinden, klicken Sie auf Sandbox-Anmeldeinformationen und befolgen Sie die Anweisungen. Alle Käufe von Kunden, die einen Sandbox PayPal verwenden, werden abgeschlossen, ohne Kunden aktiv in Rechnung zu stellen.

1. Konfigurieren Sie die Einstellungen für den Express-Checkout, um die PayPal-API zu authentifizieren und zu verwenden:

   * **Mit PayPal-Handelskonto verknüpfte E-Mail-Adresse** (Optional) Geben Sie die E-Mail-Adresse ein, die mit Ihrem PayPal-Handelskonto verknüpft ist. Bei dieser E-Mail wird zwischen Groß- und Kleinschreibung unterschieden.
   * **API-Authentifizierungsmethoden** als API-Signatur oder API-Zertifikat.
   * API-Benutzername, Kennwort und Signatur, die von Ihrem PayPal-Konto erfasst werden.
   * **Sandbox-Modus** Wählen Sie &quot;Ja&quot;oder &quot;Nein&quot;, um anzugeben, ob die eingegebenen Anmeldeinformationen für Sandbox sind. Wenn Sie die Produktionsberechtigungen eingegeben haben, wählen Sie &quot;Nein&quot;.
   * **API Verwendet Proxy** , um &quot;Ja&quot;oder &quot;Nein&quot;festzulegen, ob das System einen Proxyserver verwendet, um eine Verbindung zwischen Adobe Commerce und dem PayPal-Zahlungssystem herzustellen. Wenn ja, geben Sie den Proxy-Host und Port ein.

1. Detaillierte Informationen und Schritte zum Konfigurieren Ihres Kontos finden Sie unter [PayPal Express Checkout](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/paypal/paypal-express-checkout) ab Schritt 2 Vollziehen Sie die erforderlichen Einstellungen.

Mit dem konfigurierten und authentifizierten Konto können Sie PayPal-Zahlungsoptionen unter &quot;Erforderliche PayPal-Einstellungen&quot;aktivieren und deaktivieren:

* **Aktivieren Sie diese Lösung** zeigt Kunden über die Website die PayPal-Zahlungsmethode an.
* **Erlebnis für das Auschecken im Kontext aktivieren**
* **PayPal-Guthaben aktivieren** ermöglicht Kunden die PayPal-Kreditfinanzierung ohne zusätzliche Kosten. PayPal zahlt die Bestellung vorab und behandelt alle Rückzahlungen für den Kredit direkt beim Kunden.

## PayPal-Variablen

Fügen Sie bei Verwendung des PayPal-Onboarding-Tools mit Adobe Commerce in der Cloud-Infrastruktur die folgende Variable zum Abschnitt `variables:env` der Datei `magento.app.yaml` hinzu.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

Wenn Sie von 2.1.8 oder höher auf 2.2 aktualisieren, müssen Sie diese Variable dennoch hinzufügen.
