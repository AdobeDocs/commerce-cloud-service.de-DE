---
title: SendGrid-E-Mail-Dienst
description: Erfahren Sie mehr über den SendGrid-E-Mail-Dienst für Adobe Commerce in der Cloud-Infrastruktur und wie Sie Ihre DNS-Konfiguration testen können.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 2b106edcaaacb63c0e785f094b7e1b755885abd0
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# SendGrid-E-Mail-Dienst

Der Proxy-Dienst SendGrid Simple Mail Transfer Protocol (SMTP) bietet ausgehende E-Mail-Authentifizierungs- und Reputationsüberwachungsdienste, einschließlich Unterstützung für:

* Alle ausgehenden E-Mails
* Dedizierte IP-Adressen
* Domain-Registrierung, DomainKeys Identified Mail (DKIM)-Signaturen für die Validierung von E-Mail-Domains (nur für Pro-Staging- und Produktionsumgebungen)
* Benutzerdefinierte Domänenregistrierung (nur für Pro)
* Automatisierte Integration für Starter- und Pro-Integrationsumgebungen. Für Pro-Produktions- und Staging-Umgebungen ist eine manuelle Bereitstellung und Konfiguration während des Hardware-Bereitstellungsprozesses von Infrastructure as a Service (IAAs) erforderlich

Der SMTP-Proxy SendGrid ist nicht zur Verwendung als allgemeiner E-Mail-Server für den Empfang eingehender E-Mails oder zur Verwendung mit E-Mail-Marketing-Kampagnen vorgesehen.

>[!TIP]
>
>Details zu SendGrid für Ihr Konto finden Sie im [Onboarding-Benutzeroberfläche](https://cloud.magento.com) und wählen Sie die **Projektdetails** > **Hosting-Informationen** Registerkarte.

## E-Mail aktivieren oder deaktivieren

Sie können ausgehende E-Mails für jede Umgebung über die Cloud-Konsole oder die Befehlszeile aktivieren oder deaktivieren.

Ausgehende E-Mails sind in Pro Production- und Staging-Umgebungen standardmäßig aktiviert. Allerdings [!UICONTROL Outgoing emails] kann in den Umgebungseinstellungen deaktiviert angezeigt werden, bis Sie die `enable_smtp` -Eigenschaft über [Befehlszeile](outgoing-emails.md#enable-emails-in-the-cli) oder [Cloud-Konsole](outgoing-emails.md#enable-emails-in-the-cloud-console). Sie können ausgehende E-Mails für Integrations- und Staging-Umgebungen aktivieren, um eine Zwei-Faktor-Authentifizierung durchzuführen oder E-Mails mit Passwörtern für Cloud-Projektbenutzer zurückzusetzen. Siehe [Konfigurieren von E-Mails zum Testen](outgoing-emails.md).

Wenn ausgehende E-Mails in Pro Production- oder Staging-Umgebungen deaktiviert oder wieder aktiviert werden müssen, können Sie eine [Support-Ticket für Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>Aktualisieren der [!UICONTROL enable_smtp] Eigenschaftswert von [Befehlszeile](outgoing-emails.md#enable-emails-in-the-cli) ändert auch die [!UICONTROL Enable outgoing emails] Wert für diese Umgebung auf [Cloud-Konsole](outgoing-emails.md#enable-emails-in-the-cloud-console).

## SendGrid-Dashboard

Alle Cloud-Projekte werden unter einem zentralen Konto verwaltet, sodass nur der Support Zugriff auf das SendGrid-Dashboard hat. SendGrid bietet keine Funktionen zur Einschränkung von Unterkonten.

So überprüfen Sie die Aktivitätsprotokolle auf den Versandstatus oder eine Liste mit nicht, abgelehnt oder blockierten E-Mail-Adressen: [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket). Das Supportteam **cannot** Rufen Sie Aktivitätsprotokolle ab, die älter als 30 Tage sind.

Schließen Sie nach Möglichkeit die folgenden Informationen in Ihre Anfrage ein:

* die betroffenen E-Mail-Adressen
* den betreffenden Zeitraum (nur innerhalb der letzten 30 Tage)
* Betreff der E-Mail

## DomainKeys Identified Mail (DKIM)

DKIM ist eine E-Mail-Authentifizierungstechnologie, mit der Internet Service Provider (ISPs) sowohl legitime als auch gefälschte Absenderadressen identifizieren können. Diese Technik wird häufig bei Phishing- und E-Mail-Betrug eingesetzt. DKIM ist auf einen Domain-Eigentümer angewiesen, der die DNS-Einträge verwaltet. Bei Verwendung von DKIM verwendet der Absenderserver einen privaten Schlüssel, um die Nachrichten zu signieren. Außerdem fügt der Domäneninhaber einen DKIM-Datensatz hinzu, der geändert wurde. `TXT` -Eintrag in die DNS-Einträge der Absender-Domain eintragen. Diese `TXT` -Datensatz enthält einen öffentlichen Schlüssel, den Empfänger-E-Mail-Server verwenden, um die Signatur einer Nachricht zu überprüfen. Die Verschlüsselung mit öffentlichen DKIM-Schlüsseln ermöglicht es Empfängern, die Authentizität eines Absenders zu überprüfen. Siehe [DKIM-Datensätze - Erläuterung](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>Die SendGrid DKIM-Signaturen und die Unterstützung der Domain-Authentifizierung sind nur für Pro-Projekte verfügbar, nicht aber für Starter-Projekte. Ausgehende Transaktions-E-Mails werden daher wahrscheinlich durch Spam-Filter gekennzeichnet. Die Verwendung von DKIM verbessert die Zustellrate als authentifizierter E-Mail-Absender. Um die Zustellrate der Nachrichten zu verbessern, können Sie von Starter auf Pro aktualisieren oder Ihren eigenen SMTP-Server oder E-Mail-Versand-Dienstleister verwenden. Siehe [E-Mail-Verbindungen konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/communications/email-communications) im _Handbuch zu Admin Systems_.

### Sender- und Domain-Authentifizierung

Damit SendGrid Transaktions-E-Mails in Ihrem Namen von Pro Production- oder Staging-Umgebungen sendet, müssen Sie Ihre DNS-Einstellungen so konfigurieren, dass die drei DNS-Einträge der SendGrid-Subdomain enthalten sind. Jedem SendGrid-Konto wird eine eindeutige `TXT` -Datensatz, der zum Authentifizieren ausgehender E-Mails verwendet wird.

**Aktivieren der Domänenauthentifizierung**:

1. Senden einer [Support-Ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) Anfrage zur Aktivierung von DKIM für eine bestimmte Domäne (**Nur Pro-Staging- und Produktionsumgebungen**).
1. Aktualisieren Sie Ihre DNS-Konfiguration mit dem `TXT` und `CNAME` Einträge, die Ihnen im Support-Ticket bereitgestellt werden.

**Beispiel `TXT` Datensatz mit Konto-ID**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Beispiel `CNAME` records**:

| Domäne | Punkte an | Record Type |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM-Signaturen und automatisierte Sicherheit

Beim Einrichten einer authentifizierten Domäne können Sie zwischen automatisierter und manueller Sicherheit wählen. Wenn Sie automatisierte Sicherheit wählen, verwaltet SendGrid Ihre DKIM- und SPF-Datensätze automatisch. Wenn Sie Ihrem Konto eine neue dedizierte Sende-IP-Adresse hinzufügen, aktualisiert SendGrid sofort Ihre DNS-Einstellungen und Ihre DKIM-Signatur. Wenn Sie die automatisierte Sicherheit deaktivieren, sind Sie dafür verantwortlich, Ihre DKIM-Signatur jedes Mal zu aktualisieren, wenn Sie Ihre Versanddomäne ändern.

**Beispiel für automatisierte Sicherheit aktiviert**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Beispiel für deaktivierte automatisierte Sicherheit**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Nachdem die Domänenauthentifizierung eingerichtet wurde, verarbeitet SendGrid automatisch SPF- (Security Policy Framework) und DKIM-Einträge für Sie. Nachdem SendGrid die Variable `CNAME` Einträge zu Ihren DNS-Einträgen hinzufügen, können Sie dedizierte IP-Adressen hinzufügen und andere Kontoaktualisierungen vornehmen, ohne Ihre SPF-Einträge manuell verwalten zu müssen. Siehe [Automatisierte Sicherheit und DKIM-Signatur](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

So testen Sie Ihre DNS-Konfiguration:

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Schwelle für Transaktions-E-Mails

Der Schwellenwert für Transaktions-E-Mails bezieht sich auf die Anzahl der Transaktions-E-Mail-Nachrichten, die Sie von Pro-Umgebungen innerhalb eines bestimmten Zeitraums senden können, z. B. 12.000 E-Mails pro Monat aus Nicht-Produktionsumgebungen. Die Schwelle dient zum Schutz vor Spam-Sendungen und schädigt möglicherweise die Reputation Ihrer E-Mail.

Es gibt keine festen Beschränkungen für die Anzahl der E-Mails, die in der Produktionsumgebung gesendet werden können, solange die Reputation des Absenders mehr als 95 % beträgt. Die Reputation wird durch die Anzahl an nicht zugestellten oder abgelehnten E-Mails und die Tatsache beeinflusst, ob DNS-basierte Spam-Registrierungen Ihre Domain als potenzielle Spam-Quelle gekennzeichnet haben. Siehe [E-Mails werden nicht gesendet, wenn die SendGrid-Gutschriften in Adobe Commerce überschritten wurden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) im _Wissensdatenbank zur Commerce-Unterstützung_.

**Überprüfung der Überschreitung der maximalen Gutschriften**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Überprüfen Sie die `/var/log/mail.log` für `authentication failed : Maxium credits exceeded` Einträge.

   Wenn `authentication failed` Protokolleinträge und **Reputation beim E-Mail-Versand** ist mindestens 95, können Sie [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) , um eine Erhöhung der Kreditzuweisung anzufordern.

### Reputation beim E-Mail-Versand

Die Reputation einer E-Mail-Nachricht ist eine Punktzahl, die von einem Internet Service Provider (ISP) einem Unternehmen zugewiesen wird, das E-Mail-Nachrichten sendet. Je höher der Wert ist, desto wahrscheinlicher ist es, dass ein ISP Nachrichten an den Posteingang eines Empfängers sendet. Wenn die Punktzahl unter eine bestimmte Stufe fällt, kann der ISP Nachrichten an den Spam-Ordner der Empfänger weiterleiten oder Nachrichten sogar vollständig zurückweisen. Die Reputationsbewertung wird durch verschiedene Faktoren bestimmt, z. B. einen Durchschnittswert von 30 Tagen für Ihre IP-Adressen im Vergleich zu anderen IP-Adressen und der Spam-Beschwerderate. Siehe [8 Möglichkeiten zur Überprüfung des Reputation beim E-Mail-Versand](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation).
