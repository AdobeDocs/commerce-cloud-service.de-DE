---
title: SendGrid-E-Mail-Dienst
description: Erfahren Sie mehr über den SendGrid-E-Mail-Dienst für Adobe Commerce in der Cloud-Infrastruktur und wie Sie Ihre DNS-Konfiguration testen können.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: d07447fa8390794c3d019d513f23321fe02e41a1
workflow-type: tm+mt
source-wordcount: '1317'
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
>Vergewissern Sie sich, dass Sie die entsprechenden E-Mail-Adressen für den Store in Admin konfiguriert haben, indem Sie Stores > Konfiguration > Allgemein aufrufen, um Probleme mit der Zustellbarkeit und Domänenüberprüfung zu vermeiden. Sie müssen **[!UICONTROL Use Default]** deaktivieren und die Standardwerte durch eine Domäne ersetzen, deren Inhaber Sie sind. Öffentliche/freigegebene E-Mail-Dienste wie gmail.com und outlook.com sollten beim Senden von E-Mails über das Sendgrid nicht als Absender-E-Mail-Adresse konfiguriert werden.

## E-Mail aktivieren oder deaktivieren

Sie können ausgehende E-Mails für jede Umgebung über die Cloud-Konsole oder die Befehlszeile aktivieren oder deaktivieren.

Ausgehende E-Mails sind in Pro Production- und Staging-Umgebungen standardmäßig aktiviert. [!UICONTROL Outgoing emails] kann jedoch in den Umgebungseinstellungen deaktiviert angezeigt werden, bis Sie die Eigenschaft `enable_smtp` über die Befehlszeile [](outgoing-emails.md#enable-emails-in-the-cli) oder die [Cloud-Konsole](outgoing-emails.md#enable-emails-in-the-cloud-console) festlegen. Sie können ausgehende E-Mails für Integrations- und Staging-Umgebungen aktivieren, um eine Zwei-Faktor-Authentifizierung durchzuführen oder E-Mails mit Passwörtern für Cloud-Projektbenutzer zurückzusetzen. Siehe [Konfigurieren von E-Mails für Tests](outgoing-emails.md).

Wenn ausgehende E-Mails in Pro Production- oder Staging-Umgebungen deaktiviert oder wieder aktiviert werden müssen, können Sie ein [Adobe Commerce-Supportticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) senden.

>[!TIP]
>
>Wenn Sie den Eigenschaftswert [!UICONTROL enable_smtp] um die Befehlszeile [ ](outgoing-emails.md#enable-emails-in-the-cli) aktualisieren, wird auch der Einstellungswert [!UICONTROL Enable outgoing emails] für diese Umgebung in der [Cloud-Konsole](outgoing-emails.md#enable-emails-in-the-cloud-console) geändert.

## SendGrid-Dashboard

Alle Cloud-Projekte werden unter einem zentralen Konto verwaltet, sodass nur der Support Zugriff auf das SendGrid-Dashboard hat. SendGrid bietet keine Funktionen zur Einschränkung von Unterkonten.

Um die Aktivitätsprotokolle auf den Versandstatus oder eine Liste mit nicht zugestellten, abgelehnten oder blockierten E-Mail-Adressen zu überprüfen, senden Sie ein Adobe Commerce-Supportticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket). [ Das Supportteam **kann** keine Aktivitätsprotokolle abrufen, die älter als 30 Tage sind.

Schließen Sie nach Möglichkeit die folgenden Informationen in Ihre Anfrage ein:

* die betroffenen E-Mail-Adressen
* den betreffenden Zeitraum (nur innerhalb der letzten 30 Tage)
* Betreff der E-Mail

## DomainKeys Identified Mail (DKIM)

DKIM ist eine E-Mail-Authentifizierungstechnologie, mit der Internet Service Provider (ISPs) sowohl legitime als auch gefälschte Absenderadressen identifizieren können. Diese Technik wird häufig bei Phishing- und E-Mail-Betrug eingesetzt. DKIM ist auf einen Domain-Eigentümer angewiesen, der die DNS-Einträge verwaltet. Bei Verwendung von DKIM verwendet der Absenderserver einen privaten Schlüssel, um die Nachrichten zu signieren. Außerdem fügt der Domäneninhaber den DNS-Einträgen der Absender-Domain einen DKIM-Eintrag hinzu, der ein geänderter `TXT` -Datensatz ist. Dieser `TXT` -Datensatz enthält einen öffentlichen Schlüssel, mit dem die E-Mail-Server der Empfänger die Signatur einer Nachricht überprüfen. Die Verschlüsselung mit öffentlichen DKIM-Schlüsseln ermöglicht es Empfängern, die Authentizität eines Absenders zu überprüfen. Siehe [DKIM-Datensätze - Erklärung](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>Die SendGrid DKIM-Signaturen und die Unterstützung der Domänenauthentifizierung sind nur in der Produktions- und Staging-Umgebung für Pro-Projekte verfügbar, jedoch nicht in allen Starter-Umgebungen. Ausgehende Transaktions-E-Mails werden daher wahrscheinlich durch Spam-Filter gekennzeichnet. Die Verwendung von DKIM verbessert die Zustellrate als authentifizierter E-Mail-Absender. Um die Zustellrate der Nachrichten zu verbessern, können Sie von Starter auf Pro aktualisieren oder Ihren eigenen SMTP-Server oder E-Mail-Versand-Dienstleister verwenden. Siehe [E-Mail-Verbindungen konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/communications/email-communications) im _Leitfaden für Admin-Systeme_.

### Sender- und Domain-Authentifizierung

Damit SendGrid Transaktions-E-Mails in Ihrem Namen von Pro Production- oder Staging-Umgebungen sendet, müssen Sie Ihre DNS-Einstellungen so konfigurieren, dass die drei DNS-Einträge der SendGrid-Subdomain enthalten sind. Jedem SendGrid-Konto wird ein eindeutiger `TXT` -Datensatz zugewiesen, der zum Authentifizieren ausgehender E-Mails verwendet wird.

>[!TIP]
>
>Stellen Sie sicher, dass Sie die **[!UICONTROLSE-Mail-Adressen speichern]** mit der entsprechenden Domäne in **[!UICONTROL Stores > Configuration > General > Store Email Addresses]** konfigurieren. Die Domänenauthentifizierung erfolgt für die E-Mail-Adresse des Absenders. Wenn die Standardeinstellung (`example.com`) konfiguriert ist, werden die E-Mails von `example.com` vom Sendgrid blockiert.

**So aktivieren Sie die Domänenauthentifizierung**:

1. Senden Sie ein [Support-Ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket), um die Aktivierung von DKIM für eine bestimmte Domäne anzufordern (**Nur Staging- und Produktionsumgebungen für Pro**).
1. Aktualisieren Sie Ihre DNS-Konfiguration mit den `TXT` - und `CNAME` -Datensätzen, die Ihnen im Supportticket zur Verfügung gestellt werden.

**Beispiel `TXT` -Datensatz mit Konto-ID**:

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

**Beispiel für die automatische Sicherheit deaktiviert**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Nachdem die Domänenauthentifizierung eingerichtet wurde, verarbeitet SendGrid automatisch SPF- (Security Policy Framework) und DKIM-Einträge für Sie. Nachdem SendGrid die `CNAME` Einträge bereitgestellt hat, die Sie Ihren DNS-Einträgen hinzufügen können, können Sie dedizierte IP-Adressen hinzufügen und andere Kontoaktualisierungen vornehmen, ohne Ihre SPF-Einträge manuell verwalten zu müssen. Siehe [Automatisierte Sicherheit und Ihre DKIM-Signatur](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

So testen Sie Ihre DNS-Konfiguration:

```
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Schwelle für Transaktions-E-Mails

Der Schwellenwert für Transaktions-E-Mails bezieht sich auf die Anzahl der Transaktions-E-Mail-Nachrichten, die Sie von Pro-Umgebungen innerhalb eines bestimmten Zeitraums senden können, z. B. 12.000 E-Mails pro Monat aus Nicht-Produktionsumgebungen. Die Schwelle dient zum Schutz vor Spam-Sendungen und schädigt möglicherweise die Reputation Ihrer E-Mail.

Es gibt keine festen Beschränkungen für die Anzahl der E-Mails, die in der Produktionsumgebung gesendet werden können, solange die Reputation des Absenders mehr als 95 % beträgt. Die Reputation wird durch die Anzahl an nicht zugestellten oder abgelehnten E-Mails und die Tatsache beeinflusst, ob DNS-basierte Spam-Registrierungen Ihre Domain als potenzielle Spam-Quelle gekennzeichnet haben. Siehe [Nicht gesendete E-Mails, wenn die SendGrid-Gutschriften in Adobe Commerce überschritten wurden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) in der _Knowledge Base zur Unterstützung von Commerce_.

**Überprüfen, ob die maximalen Guthaben überschritten werden**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Überprüfen Sie die `/var/log/mail.log` auf `authentication failed : Maxium credits exceeded` -Einträge.

   Wenn `authentication failed` Protokolleinträge angezeigt werden und die **Reputation des E-Mail-Versands** mindestens 95 beträgt, können Sie [ein Adobe Commerce-Supportticket senden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) , um eine Erhöhung der Kreditzuweisung anzufordern.

### Reputation beim E-Mail-Versand

Die Reputation einer E-Mail-Nachricht ist eine Punktzahl, die von einem Internet Service Provider (ISP) einem Unternehmen zugewiesen wird, das E-Mail-Nachrichten sendet. Je höher der Wert ist, desto wahrscheinlicher ist es, dass ein ISP Nachrichten an den Posteingang eines Empfängers sendet. Wenn die Punktzahl unter eine bestimmte Stufe fällt, kann der ISP Nachrichten an den Spam-Ordner der Empfänger weiterleiten oder Nachrichten sogar vollständig zurückweisen. Die Reputationsbewertung wird durch verschiedene Faktoren bestimmt, z. B. einen Durchschnittswert von 30 Tagen für Ihre IP-Adressen im Vergleich zu anderen IP-Adressen und der Spam-Beschwerderate. Siehe [8 Möglichkeiten, den Ruf Ihrer E-Mail-Versand zu überprüfen](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation).

### E-Mail-Unterdrückungslisten

Eine E-Mail-Unterdrückungsliste ist eine Liste von Empfängern, an die E-Mails nicht gesendet werden sollten, wenn dies Ihrer Reputation des Versands und den Versandraten schaden würde. Der CAN-SPAM Act muss sicherstellen, dass E-Mail-Absender eine Methode zur Abmeldung von Empfängern haben, die E-Mails abbestellt oder als Spam gekennzeichnet haben. Die Unterdrückungsliste erfasst auch E-Mails, die bounce, blockiert oder ungültig sind.

Um zu verhindern, dass E-Mails an den Spam-Ordner gesendet werden, folgen Sie dem Artikel Best Practices von Sendgrid, [Warum werden meine E-Mails zu Spam?](https://sendgrid.com/en-us/blog/10-tips-to-keep-email-out-of-the-spam-folder).

Wenn manche Empfänger Ihre E-Mails nicht erhalten, können Sie [ein Adobe Commerce Support-Ticket senden](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) , um eine Überprüfung der Unterdrückungslisten anzufordern und die Empfänger bei Bedarf zu entfernen.

Weitere Informationen finden Sie unter [Was ist eine Unterdrückungsliste?](https://sendgrid.com/en-us/blog/what-is-a-suppression-list)
