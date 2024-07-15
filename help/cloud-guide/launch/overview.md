---
title: Site-Launch
description: Erfahren Sie, wie Sie mit der Vorbereitung des Site-Starts beginnen.
exl-id: a7b3f260-b76e-4220-b521-699548a9928a
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Site-Launch

Wenn Sie die Bereitstellung und Tests in Integrations- und Staging-Umgebungen abgeschlossen haben, können Sie mit der Vorbereitung des Site-Starts beginnen. Zunächst sollten Sie alle Entwicklungs- und Testvorgänge abschließen, bevor Sie in der Produktionsumgebung arbeiten. Sind Sie bereit zum Start? Überprüfen Sie Checklisten, Best Practices und die letzten Schritte, um Ihre Site zu starten.

Wenn Sie diese Informationen vor der Bereitstellung und dem Testen im Staging überprüft haben, sollten Sie die Vorteile von Tests im Staging zuerst im nächsten Abschnitt überprüfen. Staging ist eine nahezu produktionsorientierte Umgebung, die auf ähnlicher Hardware, Konfigurationen, Architektur und Diensten ausgeführt wird. Dadurch können Sie Ihre Ausfallzeiten reduzieren und wichtige Komponenten für Erweiterungen, Dienste, benutzerdefinierte Konfigurationen und das Testen der Benutzerakzeptanz für Händler zur Freigabe Ihrer Sites und Stores bereitstellen.

## Warum sollten Sie vollständig in Integration, Staging und Produktion testen?

Wir empfehlen dringend Tests in der Integration-, Staging- und Produktionsumgebung, da es schwierig ist sicherzustellen, dass Ihr benutzerspezifischer Code, Designs, Erweiterungen und Drittanbieter-Integrationen zusammenarbeiten, um Ihre Stores zu betreiben. Im Folgenden finden Sie allgemeine Probleme, die Sie erkennen und beheben können, wenn Sie die Tests in den Integrations- und Staging-Umgebungen vor der Aktualisierung Ihrer Produktionsumgebung durchführen:

- Staging unterstützt alle Produktionsdienste, Funktionen, Datenbankdaten, Technologiestapel, Architektur und mehr. Es spiegelt die Produktion wider. Wenn also in der Staging-Umgebung Fehler auftreten, erhalten Sie eine Warnung, bevor sie in der Produktion auftreten.

- Code, der in Ihrer lokalen Integrationsumgebung funktioniert, funktioniert möglicherweise nicht in Staging- und Produktionsumgebungen.

- Integrationsumgebungen unterstützen einige in Staging und Produktion verfügbare Dienste nicht, wie Fastly und New Relic.

- [Testen Sie Ihre Site vollständig](../test/guidance.md) mit verschiedenen Tools im Staging für Laden-, Stress-, Leistungs- und Site-Assets.

- Da in Integrationsumgebungen möglicherweise nur Datenbanken mit Testdaten gefüllt sind, die nicht mit einer produktionsähnlichen Umgebung übereinstimmen, können beim Testen in Staging- oder Produktionsumgebungen zusätzliche Fehler oder unerwartetes Verhalten auftreten.

## Voraussetzungen für den Site-Start

Sie benötigen die folgenden Informationen und Ressourcen, um sich auf den Site-Start vorzubereiten:

- CNAME-Datensatzinformationen zum Konfigurieren des DNS

- Liste aller Storefront-Domänen, die zum Zertifikat hinzugefügt werden sollen

- SSL-/TLS-Zertifikat

Als Teil von Adobe Commerce für die Cloud-Infrastrukturanmeldung stellt Adobe ein domänenvalidiertes SSL-/TLS-Zertifikat bereit, das von Let&#39;s Encrypt ausgestellt wurde. Jede Pro Production-, Staging- und Starter Production-Umgebung (`master`) verfügt über ein eindeutiges Zertifikat, das alle Domänen und Subdomänen in dieser Umgebung abdeckt. Diese Zertifikate werden automatisch bereitgestellt und auf Ihre Site hochgeladen, nachdem Sie Ihre DNS-Konfiguration für Entwicklung und Produktion aktualisiert haben. Siehe [Bereitstellen von SSL-/TLS-Zertifikaten](../cdn/fastly-configuration.md#provision-ssltls-certificates).

>[!NOTE]
>
>Wenn Sie Ihr eigenes erweitertes Validierungs-SSL-Zertifikat für Ihr Unternehmen bereitstellen möchten, anstatt das Let&#39;s Encrypt-Zertifikat zu verwenden, wenden Sie sich an Ihren CTA oder senden Sie ein Adobe Commerce-Supportticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).[

## Einrichten des Sicherheitsscan-Tools

>[!NOTE]
>
>Das Sicherheitsscan-Tool verwendet die folgenden öffentlichen IP-Adressen:
>
>```text
>52.87.98.44
>34.196.167.176
>3.218.25.102
>```
>
>Fügen Sie diese IP-Adressen zu einer Zulassungsliste in Ihren Netzwerk-Firewall-Regeln hinzu, damit das Tool Ihre Website scannen kann. Das Tool sendet Anforderungen nur an die Ports 80 und 443.

Mit dem Security Scan Tool können Sie Ihre Store-Websites regelmäßig überwachen und Updates auf bekannte Sicherheitsrisiken, Malware und veraltete Software erhalten. Dieses Tool ist ein kostenloser Dienst, der für alle Implementierungen und Versionen von Adobe Commerce in der Cloud-Infrastruktur verfügbar ist. Sie greifen über Ihr [Commerce Marketplace-Konto](https://account.magento.com/customer/account/login) auf das Tool zu.

- Überwachen Sie den Sicherheitsstatus Ihrer Sites und angewendete Sicherheitsupdates.

- Empfangen von Sicherheitsupdates und Site-spezifischen Benachrichtigungen

Informationen zum Einrichten und Verwenden des Sicherheitsscan-Tools finden Sie im [Benutzerhandbuch](https://docs.magento.com/user-guide/magento/security-scan.html) . Normalerweise beginnen Sie mit der Verwendung dieses Tools, wenn Sie mit dem Benutzerakzeptanztest (UAT) beginnen.

Jede Site, die Sie scannen, muss über den Tab Sicherheitsscan registriert werden. Während des Registrierungsprozesses müssen Sie den Haftungsausschluss akzeptieren, bevor Sie mit dem Scannen beginnen können. Sie steuern sowohl den Zeitplan als auch die Autorisierung des Benutzers für den Empfang von Benachrichtigungen, wenn die Überprüfung abgeschlossen ist. Sie können Prüfungen für ein bestimmtes, wiederkehrendes Datum und eine bestimmte Uhrzeit planen oder bei Bedarf eine Überprüfung durchführen.

Das Security Scan Tool verwendet mehrere Benutzeragenten-Zeichenfolgen, um die Malware-Aktivität in Echtzeit zu simulieren. Möglicherweise sehen Sie die folgenden Benutzeragenten in Ihren Analyse- oder Zugriffsprotokollen:

```text
Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0
GuzzleHttp/6.3.3 curl/7.29.0 PHP/7.1.18
Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.120 Safari/537.36
Visbot/2.0 (+http://www.visvo.com/en/webmasters.jsp;bot@visvo.com)
```

## Site durchsuchen

1. Greifen Sie auf Ihr [Commerce Marketplace-Konto](https://account.magento.com/customer/account/login) zu.

1. Klicken Sie auf die Registerkarte Sicherheitsscan und wählen Sie **Gehe zu Sicherheitsscan**.

1. Wählen Sie in der Spalte _Aktionen_ für die Site die Option **Scan ausführen**. Der Status der Benachrichtigung zeigt die geplante Prüfung an.

### So überprüfen Sie den Bericht:

1. Nach Abschluss des Berichts wird eine Benachrichtigung angezeigt.

1. Wählen Sie in der Site-Zeile den Bericht aus, den Sie anzeigen möchten, in der Spalte **Berichte** . Die Bestellung ist von neuester bis älterer Version.

Der Bericht listet Probleme auf, einschließlich fehlgeschlagener Scans, nicht identifizierter Ergebnisse und erfolgreicher Scans. Jeder Eintrag enthält detaillierte Informationen für die Prüfung, eine Liste der zu untersuchenden Probleme und zu ergreifenden Maßnahmen. Einige dieser Aktionen erfordern möglicherweise das Herunterladen und Installieren von Sicherheits-Patches. Fügen Sie erforderliche Patches zu einer Entwicklungsverzweigung auf Ihrer lokalen Workstation hinzu, bevor Sie sie zur Produktionsverzweigung hinzufügen.

Die Scan-Ergebnisse enthalten eine Beschriftung, die den Status der Überprüfung besteht oder fehlschlägt, mit detaillierten Informationen zu den durchgeführten Prüfungen:

- &quot;Fehlgeschlagen&quot;bedeutet, dass die Website eine schwerwiegende Sicherheitslücke aufweist.

- &quot;Nicht identifiziert&quot;bedeutet, dass Ihr Team oder Hosting-Provider eine tiefere Überprüfung durchführen muss, um festzustellen, ob weitere Maßnahmen erforderlich sind.

Die Überprüfungsergebnisse enthalten auch die vorgeschlagenen Behebungsschritte für jeden fehlgeschlagenen Sicherheitstest. Die Ergebnisse der Sicherheitsscans sind nur durch den registrierten Benutzer geschützt und sichtbar. Nur Benutzer, die im Site-Registrierungsprozess benannt sind, erhalten eine Benachrichtigung zum Abschluss der Prüfung.

## Bereit zum Starten Ihrer Site

Wenn Sie bereit sind, den Site-Startprozess zu starten, sehen Sie sich Folgendes an:

- [Checkliste für Launch](checklist.md)

- [Launch-Schritte](steps.md)
