---
title: Cloud-Infrastrukturprojekt
description: Überblick über Adobe Commerce zur Cloud-Infrastruktur [!DNL Cloud Console] und erfahren Sie, wie Sie auf die Kontoeinstellungen zugreifen können.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Cloud-Infrastrukturprojekt

Das Projekt Adobe Commerce on Cloud Infrastructure umfasst sämtlichen Code in Git-Zweigen, verknüpften Umgebungen und Skripten zur Bereitstellung der [!DNL Commerce] Anwendung. Umgebungen enthalten Dienste zur Unterstützung der [!DNL Commerce] -Anwendung, einschließlich einer Datenbank, eines Webservers und eines Caching-Servers.

Adobe bietet eine [!DNL Cloud Console] und Entwicklertools , um alle Aspekte Ihres Projekts vollständig zu verwalten. Als Kontoinhaber haben Sie vollen Zugriff auf alle Umgebungen.

## [!DNL Cloud Console]

Die [!DNL Cloud Console] bietet interaktive Methoden zum Erstellen, Verwalten und Bereitstellen von Commerce-Code in einem benutzerfreundlichen Format. [Melden Sie sich bei [!DNL Cloud Console]](https://console.adobecommerce.com) , um Ihre Projektliste anzuzeigen. Sie können nur Projekte sehen, auf die Sie als Administrator Zugriff haben, oder Projekte für bestimmte Umgebungstypen. Wenn Sie Adobe Solutions Partner sind, sehen Sie möglicherweise mehrere Projekte für von Ihnen unterstützte Clients.

>[!TIP]
>
>Wenn keine Projekte angezeigt werden, müssen Sie die [Kontoinhaber oder Projektadministrator](../project/user-access.md) mit dem Projekt verknüpft sind und Zugriff anfordern. Informationen zu Erstbenutzern finden Sie unter [Onboarding-Thema](../../get-started/onboarding.md#cloud-console) im _Erste Schritte_ Handbuch.

Die _Alle Projekte_ -Ansicht listet alle Projekte auf, auf die Sie Zugriff haben. Sie können auf **[!UICONTROL Show filters]** und filtern Sie Ihre Projektliste nach Typ, Region oder Plan.

![Projektliste](../../assets/ui-allprojects-list.png)

### Projektübersicht

Auswählen eines Projekts aus dem _Alle Projekte_ -Liste öffnet die Projektübersicht. In der Projektübersicht wird immer eine Projektnavigationsleiste angezeigt, die einen Umgebungs-Selektor und eine Konfigurationsschaltfläche enthält:

![Projektnavigation](../../assets/project-nav.png)

Die Projektübersicht zeigt, solange keine Umgebung ausgewählt ist, eine Zusammenfassung der Projektdetails im Vorschaubereich:

- Projektname
- Region, Projekt-ID
- Planen, zugewiesener Speicher, Umgebungen, Benutzer
- Storefront-URL mit **[!UICONTROL Set a custom domain]** button

Und in der Hauptprojektübersicht:

- Die Ansicht &quot;Umgebungen&quot;zeigt eine Listen- oder Baumansicht von ![aktive Verzweigung](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} (inaktive) Umgebungen.
- [Aktivitäts-Stream](activity-stream.md) zeigt laufende, ausstehende und aktuelle Aktivitäten für das Projekt an.
<!-- - Apps & Services—Shows a topology of service containers -->

Für **Starter** -Projekte gibt es eine Hierarchie von Verzweigungen, die von `master` (Produktion). Jede von Ihnen erstellte Verzweigung wird als untergeordnete Elemente aus dem `master` -Verzweigung. Adobe empfiehlt, eine `staging` Verzweigung erstellen und dann eine `integration` -Verzweigung zur Entwicklung. Siehe [Starterarchitektur](../architecture/starter-architecture.md).

Für **Pro**, gibt es eine Hierarchie von Verzweigungen, die von `production` nach `staging` nach `integration`. Die ![Dediziertes Symbol](../../assets/icon-dedicated.png){width="32"} -Symbol zeigt an, dass die Verzweigung in einer dedizierten Umgebung bereitgestellt wird. Alle von Ihnen erstellten Zweige werden als untergeordnete Elemente der `integration` -Verzweigung. Siehe [Pro Architektur](../architecture/pro-architecture.md).

![Pro Umgebungsliste](../../assets/pro-environments.png)

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
- Storefront-URL mit **[!UICONTROL Set a custom domain]** button

Und in der Hauptumgebung - Übersicht:

- [Aktivitäts-Stream](activity-stream.md) gibt die Übersicht über die Hauptumgebung sowie laufende, ausstehende und aktuelle Aktivitäten für die ausgewählte Umgebung an.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- [Registerkarte &quot;Backups&quot;](../storage/snapshots.md#create-a-manual-backup) bietet eine Liste der gespeicherten Sicherungen, den Verlauf der Sicherungsaktionen und die Schaltfläche &quot;Sicherung&quot;.

### Zugriff auf Storefront

Jede aktive Umgebung verfügt über eine Storefront. Wählen Sie in der oberen Navigationsleiste eine Umgebung aus und klicken Sie in der Umgebungsübersicht auf die URL . Außerdem gibt es eine **[!UICONTROL URLs]** Liste auf der rechten Seite über der Aktivitätenliste.

Die Web-Zugriffs-URL kann Folgendes enthalten:

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Eindeutige ID** = 7 alphanumerische Zufallszeichen
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

Öffnen Sie die _Einstellungen_ Bedienfeld durch Klicken auf ![Projektsymbol konfigurieren](../../assets/icon-configure.png){width="36"} (Konfigurieren) auf der rechten Seite der Projektnavigation.

### Projekteinstellungen

**[!UICONTROL Project Settings]** erweitert ein Menü mit Steuerelementen auf Projektebene, um Benutzer, Variablen und mehr zu verwalten:

| Option | Beschreibung |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Allgemein | Verwalten Sie die Zeitzone für die Verwendung mit der Planung von Sicherungen oder Wartung. |
| Zugriff | Verwalten [Benutzerzugriff](user-access.md) zu Projekt- und Umgebungstypen. |
| Zertifikate | Zeigen Sie eine Liste der mit dem Projekt verknüpften SSL-Zertifikate an. |
| Bereitstellungsschlüssel | Fügen Sie den öffentlichen Schlüssel zum Projekt-Code-Repository hinzu und zeigen Sie ihn an. |
| Domänen | Fügen Sie dem Projekt einen Domänennamen hinzu. Siehe [Domänen verwalten](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Integrationen | Hinzufügen und Verwalten [Integrationen](../integrations/overview.md), wie z. B. Gesundheitsbenachrichtigungen und Webhooks. |
| Variablen | Hinzufügen [Variablen auf Projektebene](../environment/variable-levels.md) die zur Build- und Laufzeit in allen Umgebungen verfügbar sind. |

{style="table-layout:auto"}

### Umgebungseinstellungen

Klicks **[!UICONTROL Environments]** und wählen Sie eine bestimmte Umgebung aus der Liste für Steuerelemente aus, um die Site-Einstellungen und Umgebungsvariablen zu verwalten:

| Option | Beschreibung |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Allgemein | Konfigurieren Sie Anzeigename, Umgebungstyp und übergeordnete Umgebung.<br>Wechsel zwischen verschiedenen Umgebungseinstellungen: |
|           | **Ausgehende E-Mails aktivieren**: Senden [ausgehende E-Mails](outgoing-emails.md) aus der Umgebung mit dem SMTP-Protokoll. |
|           | **Aus Suchmaschinen ausblenden**: Blockieren Sie Suchmaschinen-Indexer und -Crawler von der Site. |
|           | **HTTP-Zugriffssteuerung**: Aktivieren Sie die Sicherheitskonfiguration für [!DNL Cloud Console] über eine Zugriffskontrolle auf Anmeldedaten und IP-Adressen. |
|           | Status ist `active` oder `inactive`. Der Großteil Ihrer Arbeit befindet sich in einer aktiven Umgebung. Sie können die Umgebung deaktivieren oder löschen. |
| Variablen | Anzeigen, Erstellen und Verwalten [Variablen auf Umgebungsebene](../environment/variable-levels.md) zur Laufzeit verfügbar. |
| Domänen | Anzeigen einer Liste von [konfigurierte Routen](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**NICHT** Verwenden Sie die HTTP-Zugriffssteuerungsmethode zum Schützen von Pro Staging- und Produktionsumgebungen. Dies verhindert das schnelle Zwischenspeichern. Verwenden Sie stattdessen die [Blockieren](../cdn/fastly-vcl-blocking.md) Funktion im Fastly CDN für Adobe Commerce verfügbar.

## Schnelle und New Relic-Anmeldeinformationen

Ihr Projekt umfasst [Fastly](../cdn/fastly.md) und [New Relic](../monitor/new-relic-service.md). Die Projektdetails enthalten Informationen zu Ihrem Projektplan sowie wichtige Lizenzen und Token für diese Integrationen. Nur der Lizenzinhaber hat erstmaligen Zugriff auf die Anmeldedaten und Dienste. Stellen Sie diese Anmeldeinformationen bei Bedarf für technische Ressourcen und Entwicklerressourcen bereit.

- [Fastly](https://www.fastly.com/) bietet Inhaltsbereitstellung (Content Delivery, CDN), Bildoptimierung und Sicherheitsdienste (DDoS und WAF) für Ihre Adobe Commerce in Cloud-Infrastrukturprojekten. Siehe [Schnelles Abrufen von Anmeldedaten](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) bietet Anwendungsmetriken und Leistungsinformationen für Staging- und Produktionsumgebungen.

Verwenden Sie die [Cloud-CLI](../dev-tools/cloud-cli-overview.md) , um Ihre Integrationstoken, -IDs und mehr zu überprüfen:

```bash
magento-cloud subscription:info services
```
