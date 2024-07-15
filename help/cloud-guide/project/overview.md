---
title: Cloud-Infrastrukturprojekt
description: Lesen Sie einen Überblick über die Adobe Commerce zur Cloud-Infrastruktur [!DNL Cloud Console] und erfahren Sie, wie Sie auf die Kontoeinstellungen zugreifen.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Cloud-Infrastrukturprojekt

Das Projekt Adobe Commerce on Cloud Infrastructure umfasst sämtlichen Code in Git-Zweigen, verknüpften Umgebungen und Skripten zur Bereitstellung der [!DNL Commerce] -Anwendung. Umgebungen enthalten Dienste zur Unterstützung der [!DNL Commerce] -Anwendung, einschließlich einer Datenbank, eines Webservers und eines Caching-Servers.

Adobe bietet eine [!DNL Cloud Console]- und Entwicklertools, mit denen Sie alle Aspekte Ihres Projekts vollständig verwalten können. Als Kontoinhaber haben Sie vollen Zugriff auf alle Umgebungen.

## [!DNL Cloud Console]

Der [!DNL Cloud Console] bietet interaktive Methoden zum Erstellen, Verwalten und Bereitstellen von Commerce-Code in einem benutzerfreundlichen Format. [Melden Sie sich bei  [!DNL Cloud Console]](https://console.adobecommerce.com) an, um Ihre Projektliste anzuzeigen. Sie können nur Projekte sehen, auf die Sie als Administrator Zugriff haben, oder Projekte für bestimmte Umgebungstypen. Wenn Sie Adobe Solutions Partner sind, sehen Sie möglicherweise mehrere Projekte für von Ihnen unterstützte Clients.

>[!TIP]
>
>Wenn keine Projekte angezeigt werden, müssen Sie sich an den mit dem Projekt verknüpften [Kontoinhaber oder Projektadministrator](../project/user-access.md) wenden und den Zugriff anfordern. Erstmalige Benutzer finden Informationen zum Thema [Einstieg](../../get-started/onboarding.md#cloud-console) im Leitfaden _Erste Schritte_ .

In der Ansicht &quot;_Alle Projekte_&quot;werden alle Projekte aufgelistet, auf die Sie Zugriff haben. Sie können auf &quot;**[!UICONTROL Show filters]**&quot;klicken und Ihre Projektliste nach Typ, Region oder Plan filtern.

![Projektliste](../../assets/ui-allprojects-list.png)

### Projektübersicht

Wenn Sie ein Projekt aus der Liste _Alle Projekte_ auswählen, wird die Projektübersicht geöffnet. In der Projektübersicht wird immer eine Projektnavigationsleiste angezeigt, die einen Umgebungs-Selektor und eine Konfigurationsschaltfläche enthält:

![Projektnavigation](../../assets/project-nav.png)

Die Projektübersicht zeigt, solange keine Umgebung ausgewählt ist, eine Zusammenfassung der Projektdetails im Vorschaubereich:

- Projektname
- Region, Projekt-ID
- Planen, zugewiesener Speicher, Umgebungen, Benutzer
- Storefront-URL mit Schaltfläche **[!UICONTROL Set a custom domain]**

Und in der Hauptprojektübersicht:

- Die Ansicht &quot;Umgebungen&quot;zeigt eine Listen- oder Baumansicht der (inaktiven) ![aktiven Verzweigungen](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} -Umgebungen.
- [Aktivitäts-Stream](activity-stream.md) zeigt laufende, ausstehende und aktuelle Aktivitäten für das Projekt an.
<!-- - Apps & Services—Shows a topology of service containers -->

Bei **Starter** -Projekten gibt es eine Hierarchie von Verzweigungen, die mit `master` (Produktion) beginnt. Jeder Zweig, den Sie erstellen, wird als untergeordnete Elemente aus dem Zweig `master` angezeigt. Adobe empfiehlt, einen `staging` -Zweig zu erstellen und dann einen `integration` -Zweig für die Entwicklung zu erstellen. Siehe [Starterarchitektur](../architecture/starter-architecture.md).

Für **Pro** gibt es eine Hierarchie von Verzweigungen, die von `production` bis `staging` bis `integration` reicht. Das Symbol ![Dediziertes Symbol](../../assets/icon-dedicated.png){width="32"} zeigt an, dass die Verzweigung in einer dedizierten Umgebung bereitgestellt wird. Alle Zweige, die Sie erstellen, werden als untergeordnete Elemente des Zweigs `integration` angezeigt. Siehe [Pro-Architektur](../architecture/pro-architecture.md).

![Pro Umgebungs-Liste](../../assets/pro-environments.png)

### Umgebungsübersicht

Wenn Sie eine Umgebung in der Projektnavigationsleiste auswählen, wird die Übersicht und die Navigationsleiste so geändert, dass sie sich auf die ausgewählte Umgebung konzentrieren. Die Navigationsleiste enthält Verzweigungssteuerelemente (Verzweigung, Zusammenführen und Synchronisieren) und eine Konfigurationsschaltfläche:

![Umgebung ausgewählt](../../assets/environment-selected.png)

Die Umgebungsübersicht zeigt eine Zusammenfassung der Umgebungsdetails im Vorschaubereich:

- Umgebungsname, Typ
- Region, Projekt-ID
- Datum und Uhrzeit der letzten Aktivität, einschließlich Sicherung
- HTTP-Zugriff und Suchmaschinenstatus
- Der der Umgebung zugewiesene Maschinenname
- Umgebungsstatus (aktiv oder inaktiv)
- Storefront-URL mit Schaltfläche **[!UICONTROL Set a custom domain]**

Und in der Hauptumgebung - Übersicht:

- [Aktivitäts-Stream](activity-stream.md) bildet die Übersicht der Hauptumgebung und zeigt laufende, ausstehende und aktuelle Aktivitäten für die ausgewählte Umgebung an.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- Die Registerkarte [Sicherungen](../storage/snapshots.md#create-a-manual-backup) enthält eine Liste der gespeicherten Sicherungen, den Verlauf der Sicherungsaktionen und die Schaltfläche &quot;Sicherung&quot;.

### Zugriff auf Storefront

Jede aktive Umgebung verfügt über eine Storefront. Wählen Sie in der oberen Navigationsleiste eine Umgebung aus und klicken Sie in der Umgebungsübersicht auf die URL . Außerdem befindet sich rechts oberhalb der Aktivitätenliste eine Liste mit dem Wert **[!UICONTROL URLs]** .

Die Web-Zugriffs-URL kann Folgendes enthalten:

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Eindeutige ID** = 7 zufällige alphanumerische Zeichen
- **Projekt-ID** = Projekt-ID mit 13 Zeichen
- **Region** = Name der AWS- oder Azure-Region, siehe [Regionale IP-Adressen](regional-ip-addresses.md)

Die Pro Production- und Staging-Umgebungen umfassen drei Knoten, auf die Sie über die folgenden Links zugreifen können:

- Lastenausgleich-URLs:

   - `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

- Direkter Zugriff auf einen der drei redundanten Server:

   - `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

  Die Produktions-URL wird vom Content Delivery Network (CDN) verwendet.

## Einstellungen

Öffnen Sie das Bedienfeld _Einstellungen_ , indem Sie auf das Symbol ![Projektsymbol konfigurieren](../../assets/icon-configure.png){width="36"} (Konfigurieren) auf der rechten Seite der Projektnavigation klicken.

### Projekteinstellungen

**[!UICONTROL Project Settings]** erweitert ein Menü mit Steuerelementen auf Projektebene, um Benutzer, Variablen und mehr zu verwalten:

| Option | Beschreibung |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Allgemein | Verwalten Sie die Zeitzone für die Verwendung mit der Planung von Sicherungen oder Wartung. |
| Zugriff | Verwalten Sie den [Benutzerzugriff](user-access.md) für Projekt- und Umgebungstypen. |
| Zertifikate | Zeigen Sie eine Liste der mit dem Projekt verknüpften SSL-Zertifikate an. |
| Bereitstellungsschlüssel | Fügen Sie den öffentlichen Schlüssel zum Projekt-Code-Repository hinzu und zeigen Sie ihn an. |
| Domänen | Fügen Sie dem Projekt einen Domänennamen hinzu. Siehe [Domänen verwalten](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Integrationen | Fügen Sie [Integrationen](../integrations/overview.md) hinzu und verwalten Sie diese, z. B. Statusbenachrichtigungen und Webhooks. |
| Variablen | Fügen Sie [Variablen auf Projektebene](../environment/variable-levels.md) hinzu, die beim Erstellen und zur Laufzeit in allen Umgebungen verfügbar sind. |

{style="table-layout:auto"}

### Umgebungseinstellungen

Klicken Sie auf &quot;**[!UICONTROL Environments]**&quot;und wählen Sie eine bestimmte Umgebung aus der Liste für Steuerelemente aus, um die Site-Einstellungen und Umgebungsvariablen zu verwalten:

| Option | Beschreibung |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Allgemein | Konfigurieren Sie Anzeigename, Umgebungstyp und übergeordnete Umgebung.<br>Wechsel zwischen verschiedenen Umgebungseinstellungen: |
|           | **Ausgehende E-Mails aktivieren**: Senden Sie [ausgehende E-Mails](outgoing-emails.md) aus der Umgebung mit dem SMTP-Protokoll. |
|           | **Aus Suchmaschinen ausblenden**: Blockieren Sie Suchmaschinen-Indexer und -Crawler von der Site. |
|           | **HTTP-Zugriffssteuerung**: Aktivieren Sie die Sicherheitskonfiguration für die [!DNL Cloud Console] mithilfe einer Zugriffskontrolle für die Anmeldung und IP-Adresse. |
|           | Status ist `active` oder `inactive`. Der Großteil Ihrer Arbeit befindet sich in einer aktiven Umgebung. Sie können die Umgebung deaktivieren oder löschen. |
| Variablen | Anzeigen, Erstellen und Verwalten von [Umgebungsvariablen](../environment/variable-levels.md), die zur Laufzeit verfügbar sind. |
| Domänen | Anzeigen einer Liste der [konfigurierten Routen](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**NICHT** Verwenden Sie die HTTP-Zugriffssteuerungsmethode zum Schützen von Pro Staging- und Produktionsumgebungen. Dies verhindert das schnelle Zwischenspeichern. Verwenden Sie stattdessen die Funktion &quot;[Blocking](../cdn/fastly-vcl-blocking.md)&quot;, die im Fastly CDN für Adobe Commerce verfügbar ist.

## Schnelle und New Relic-Anmeldeinformationen

Ihr Projekt umfasst [Fastly](../cdn/fastly.md) und [New Relic](../monitor/new-relic-service.md). Die Projektdetails enthalten Informationen zu Ihrem Projektplan sowie wichtige Lizenzen und Token für diese Integrationen. Nur der Lizenzinhaber hat erstmaligen Zugriff auf die Anmeldedaten und Dienste. Stellen Sie diese Anmeldeinformationen bei Bedarf für technische Ressourcen und Entwicklerressourcen bereit.

- [Fastly](https://www.fastly.com/) bietet Inhaltsbereitstellung (CDN), Bildoptimierung und Sicherheitsdienste (DDoS und WAF) für Ihre Adobe Commerce für Cloud-Infrastrukturprojekte. Siehe [Schnelle Anmeldeinformationen abrufen](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) bietet Anwendungsmetriken und Leistungsinformationen für Staging- und Produktionsumgebungen.

Verwenden Sie die [Cloud-CLI](../dev-tools/cloud-cli-overview.md), um Ihre Integrations-Token, IDs und mehr zu überprüfen:

```bash
magento-cloud subscription:info services
```
