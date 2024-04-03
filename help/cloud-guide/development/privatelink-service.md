---
title: PrivateLink-Dienst
description: Erfahren Sie, wie Sie mit dem PrivateLink-Dienst eine sichere Verbindung zwischen einer privaten Cloud- und Adobe Commerce-Cloud-Plattform in derselben Region herstellen können.
feature: Cloud, Iaas, Security
exl-id: b25548b8-312b-4a74-b242-f4e2ac6cf945
source-git-commit: 5b52157c6c623bb4c765a2d545919df79d81f1da
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# PrivateLink-Dienst

Adobe Commerce on Cloud-Infrastruktur unterstützt die Integration mit [AWS PrivateLink](https://aws.amazon.com/privatelink/) oder [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/) -Dienst. Sie können PrivateLink verwenden, um eine sichere, private Kommunikation zwischen Adobe Commerce in Cloud-Infrastrukturumgebungen mit Diensten und Anwendungen herzustellen, die auf externen Systemen gehostet werden. Sowohl die Adobe Commerce-Anwendung als auch externe Systeme müssen über Virtual Private Cloud (VPC)-Endpunkte zugänglich sein, die auf derselben Cloud-Plattform (AWS oder Azure) innerhalb derselben Cloud-Region konfiguriert sind.

>[!TIP]
>
>PrivateLink eignet sich am besten zum Schützen von Verbindungen für Nicht-HTTP(S)-Integrationen, wie z. B. Datenbank- oder Dateiübertragungen. Wenn Sie Ihre Anwendung mit Adobe Commerce-APIs integrieren möchten, lesen Sie, wie Sie eine [Adobe API-Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _API-Mesh für Adobe Developer App Builder_.

## Funktionen und Support

Die PrivateLink-Dienstintegration für Adobe Commerce in Cloud-Infrastrukturprojekten umfasst die folgenden Funktionen und Support:

- Eine sichere Verbindung zwischen einer Virtual Private Cloud (VPC) eines Kunden und dem Adobe VPC auf derselben Cloud-Plattform (AWS oder Azure) innerhalb derselben Cloud-Region.
- Unterstützung der unidirektionalen oder bidirektionalen Kommunikation zwischen Endpunktdiensten, die unter Adobe und Kunden-VPC verfügbar sind.
- Dienstaktivierung:

   - Öffnen erforderlicher Ports in Adobe Commerce in der Cloud-Infrastruktur-Umgebung
   - Erstverbindung zwischen dem Kunden und Adobe-VPC herstellen
   - Beheben von Verbindungsproblemen bei der Aktivierung

## Einschränkungen

- Unterstützung für PrivateLink ist nur in Pro Produktions- und Staging-Umgebungen verfügbar. Sie ist nicht in lokalen oder Integrationsumgebungen oder in Starter-Projekten verfügbar.
- Sie können keine SSH-Verbindungen mit PrivateLink herstellen. Siehe [SSH-Schlüssel aktivieren](secure-connections.md).
- Die Adobe Commerce-Unterstützung deckt nicht die Fehlerbehebung von Problemen mit AWS PrivateLink ab, die über die Erstaktivierung hinausgehen.
- Die Kunden sind für die Kosten im Zusammenhang mit der Verwaltung ihres eigenen VPC verantwortlich.
- Sie können das HTTPS-Protokoll (Port 443) nicht verwenden, um über Azure Private Link über die Cloud-Infrastruktur eine Verbindung zu Adobe Commerce herzustellen, da [Schnell hergestelltes Verdecken](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html). Diese Einschränkung gilt nicht für AWS PrivateLink.
- PrivateDNS ist nicht verfügbar.

## PrivateLink-Verbindungstypen

Es sind zwei PrivateLink-Verbindungstypen verfügbar, die im folgenden Netzwerkdiagramm dargestellt sind, um eine sichere Kommunikation zwischen Ihrem Speicher und externen Systemen zu gewährleisten, die außerhalb der Cloud-Umgebung gehostet werden.

![PrivateLink-Netzwerkdiagramm](../../assets/privatelink-architecture-diagram.png)

Wählen Sie einen der PrivateLink-Verbindungstypen aus, die am besten für Ihre Adobe Commerce in Cloud-Infrastrukturumgebungen geeignet sind:

- **Unidirektionaler PrivateLink**-Wählen Sie diese Konfiguration, um Daten sicher aus einem Adobe Commerce im Cloud-Infrastrukturspeicher abzurufen.
- **Bidirektionaler PrivateLink**-Wählen Sie diese Konfiguration, um sichere Verbindungen zu und von Systemen außerhalb der Adobe Commerce in der Cloud-Infrastruktur-Umgebung herzustellen. Die bidirektionale Option erfordert zwei Verbindungen:

   - Eine Verbindung zwischen dem VPC des Kunden und dem Adobe VPC
   - Eine Verbindung zwischen dem Adobe VPC und dem VPC des Kunden

>[!TIP]
>
>Wenden Sie sich an Ihren Netzwerkadministrator oder Cloud-Plattformanbieter, um Hilfe bei der Auswahl des Verbindungstyps PrivateLink zu erhalten oder um Hilfe bei der Einrichtung und Verwaltung des VPC zu erhalten. Siehe Dokumentation zur Cloud-Plattform PrivateLink : [AWS PrivateLink](https://aws.amazon.com/privatelink/) oder [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/).

## Aktivierung von PrivateLink anfordern

>[!WARNING]
>
>Die Aktivierung von PrivateLink kann bis zu _fünf_ Geschäftstage. Die Bereitstellung unvollständiger oder ungenauer Informationen kann den Prozess verzögern.

### Voraussetzungen

![check](../../assets/fix.svg) Ein Cloud-Konto (AWS oder Azure) in derselben Region wie die Adobe Commerce in der Cloud-Infrastrukturinstanz.

![check](../../assets/fix.svg) Ein VPC in der Kundenumgebung, der die Dienste hostet, die über PrivateLink verbunden werden sollen. Hilfe zur VPC-Einrichtung finden Sie in der Dokumentation zu AWS oder Azure oder wenden Sie sich an Ihren Netzwerkadministrator.

![check](../../assets/fix.svg) Bei bidirektionalen PrivateLink-Verbindungen müssen Sie die Endpunktdienstkonfiguration für Ihre Anwendung oder Ihren Dienst erstellen und einen Endpunkt in Ihrer VPC-Umgebung erstellen, bevor Sie die Aktivierung von PrivateLink anfordern. Siehe [Für bidirektionale PrivateLink-Verbindungen einrichten](#set-up-for-bidirectional-privatelink-connections).

Erfassen Sie die folgenden Daten, die für die Aktivierung von PrivateLink erforderlich sind:

- **Kundennummer der Cloud** (AWS oder Azure): Muss sich in derselben Region wie die Adobe Commerce in der Cloud-Infrastrukturinstanz befinden
- **Cloud-Region**—Geben Sie die Cloud-Region an, in der das Konto zu Verifizierungszwecken gehostet wird.
- **Dienste und Kommunikationshäfen**—Adobe muss Ports öffnen, um die Dienstkommunikation zwischen VPCs zu ermöglichen, z. B. SQL Port 3306, SFTP Port 222
- **Projekt-ID**- Geben Sie die Adobe Commerce für die Projekt-ID von Cloud Infrastructure Pro an. Sie können die Projekt-ID und andere Projektinformationen wie die folgenden abrufen [Cloud-CLI](../dev-tools/cloud-cli-overview.md) command: `magento-cloud project:info`
- **Verbindungstyp**—Geben Sie eine unidirektionale oder bidirektionale Verbindungstyp an.
- **Endpunktdienst**—Für bidirektionale PrivateLink-Verbindungen geben Sie die DNS-URL für den VPC-Endpunktdienst an, mit dem Adobe eine Verbindung herstellen muss, z. B.: `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **Zugriff auf Endpunkt-Dienst gewährt**—Um eine Verbindung zum externen Dienst herzustellen, gewähren Sie dem Endpunktdienst Zugriff auf den folgenden AWS-Kontoprinzipal: `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Wenn der Zugriff auf den Endpunktdienst nicht möglich ist, wird die bidirektionale PrivateLink-Verbindung zum Dienst in Ihrem VPC **not** hinzugefügt, was die Einrichtung verzögert.

#### Zusätzliche spezifische Voraussetzungen für die Aktivierung von Azure Private Link

- Geben Sie die Cluster-ID an. Melden Sie sich mit SSH bei der Remote-Verbindung an und verwenden Sie den folgenden Befehl: `cat /etc/platform_cluster`
- Für die Verbindung eines externen Dienstes mit Ihrem Adobe Commerce Pro-Cluster benötigen Sie Folgendes:

   - Eine Liste der Ports auf Ihrem Pro-Cluster, die für den neuen externen privaten Endpunkt verfügbar gemacht werden sollen
   - Eine Liste der Azure-Anmelde-IDs für die privaten Endpunktverbindungen

- Um Ihren Adobe Commerce Pro-Cluster mit einem externen Dienst zu verbinden, benötigen Sie Folgendes:

   - Eine Liste der Ressourcen-IDs für die Zieldienste. Externe IDs des privaten Link-Dienstes sehen in etwa wie folgt aus:

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Aktivierungs-Workflow

Im folgenden Workflow wird der Aktivierungsprozess für die PrivateLink-Integration mit Adobe Commerce in der Cloud-Infrastruktur beschrieben.

1. **Kunde** sendet ein Supportticket, um die Aktivierung von PrivateLink mit der Betreffzeile anzufordern `PrivateLink support for <company>`. Fügen Sie die [für die Aktivierung erforderliche Daten](#prerequisites) im Ticket. Adobe verwendet das Supportticket, um die Kommunikation während des Aktivierungsprozesses zu koordinieren.

1. **Adobe** ermöglicht dem Kundenkonto Zugriff auf den Endpunktdienst im Adobe VPC.

   - Aktualisieren Sie die Adobe-Endpunktdienstkonfiguration, um Anfragen zu akzeptieren, die vom AWS- oder Azure-Kundenkonto initiiert wurden.
   - Aktualisieren Sie das Support-Ticket, um den Dienstnamen für den Adobe VPC-Endpunkt anzugeben, mit dem eine Verbindung hergestellt werden soll, beispielsweise `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Kunde** fügt den Adobe-Endpunktdienst zu ihrem Cloud-Konto (AWS oder Azure) hinzu, wodurch eine Verbindungsanforderung an Adobe Trigger wird. Anweisungen finden Sie in der Dokumentation zur Cloud-Plattform :

   - Informationen zu AWS finden Sie unter [Annehmen und Ablehnen von Verbindungsanfragen für Schnittstellenendpunkte].
   - Für Azure siehe [Verbindungsanfragen verwalten].

1. **Adobe** genehmigt die Verbindungsanforderung.

1. Nach Genehmigung der Verbindungsanforderung, **dem Kunden** [prüft die Verbindung](#test-vpc-endpoint-service-connection) zwischen ihrem VPC und dem Adobe VPC.

1. Zusätzliche Schritte zur Aktivierung bidirektionaler Verbindungen:

   - **Adobe** stellt den Prinzipal des Adobe-Kontos (Stammbenutzer für AWS- oder Azure-Konten) bereit und fordert den Zugriff auf den VPC-Endpunktdienst des Kunden an.
   - **Kunde** ermöglicht Adobe den Zugriff auf den Endpunktdienst im VPC des Kunden. Dies setzt voraus, dass der Prinzipal des Adobe-Kontos Zugriff auf `arn:aws:iam::402592597372:root`wie zuvor in der **Zugriff auf Endpunkt-Dienst gewährt** Voraussetzung.

      - Aktualisieren Sie die Konfiguration des Kundenendpunktdienstes, um vom Adobe-Konto initiierte Anfragen zu akzeptieren. Anweisungen finden Sie in der Dokumentation zur Cloud-Plattform :

         - Informationen zu AWS finden Sie unter [Berechtigungen für Ihren Endpunktdienst hinzufügen und entfernen].
         - Für Azure siehe [Verbindung zum privaten Endpunkt verwalten]

      - Stellen Sie Adobe mit dem Endpunktdienstnamen für den Kunden-VPC bereit.

   - **Adobe** fügt den Endpunktdienst für Kunden zum Adobe-Plattformkonto (AWS oder Azure) hinzu, wodurch eine Verbindungsanforderung an den Kunden-VPC Trigger wird.
   - **Kunde** genehmigt die Verbindungsanforderung von Adobe, um das Setup abzuschließen.
   - **Kunde** [prüft die Verbindung](#test-vpc-endpoint-service-connection) von der Adobe VPC.

## Verbindung zum VEC-Endpunktdienst testen

Sie können die Telnet-Anwendung verwenden, um die Verbindung zum VPC-Endpunktdienst zu testen.

**So testen Sie die Verbindung zum VPC-Endpunktdienst**:

1. Im Projektstammordner: **Checkout** die Staging- oder Produktionsumgebung, die für den Zugriff auf den PrivateLink-Endpunktdienst konfiguriert ist.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Führen Sie den folgenden CURL-Befehl aus:

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Beispiel:

   ```terminal
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Beispielerfolgreiche Antwort:

   ```terminal
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Beispiel für fehlgeschlagene Antwort:

   ```terminal
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Stellen Sie sicher, dass der Dienst auf VM wartet.

   ```bash
   netstat -na | grep <port>
   ```

1. Überprüfen Sie den Paketfluss.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Überprüfen Sie die folgenden internen Einstellungen, um sicherzustellen, dass die Konfiguration gültig ist:

   - Einstellungen für Endpunkt- und Endpunktdienste
   - Einstellungen für den Netzwerk-Lastenausgleich (NLB)
   - Die Zielgruppen der NLB und ihre Gesundheit
   - Die netcat/curl-Endpunkt-URL von jeder VM (siehe oben)

   In den folgenden Artikeln finden Sie Hilfe zur Fehlerbehebung bei Verbindungsproblemen:

   - [AWS: Fehlerbehebung für Endpunktdienstverbindungen]
   - [Amazon: Fehlerbehebung bei Verbindungsproblemen mit Azure Private Link]

   Wenn Sie die Fehler nicht beheben können, aktualisieren Sie das Adobe Commerce Support-Ticket, um Hilfe bei der Verbindungsherstellung anzufordern.

## PrivateLink-Konfiguration ändern

[Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um eine vorhandene PrivateLink-Konfiguration zu ändern. Sie können beispielsweise Änderungen wie die folgenden anfordern:

- Entfernen Sie die PrivateLink-Verbindung aus der Adobe Commerce in der Produktions- oder Staging-Umgebung der Cloud-Infrastruktur.
- Ändern Sie die Kundennummer des Cloud-Plattformkontos für den Zugriff auf den Adobe-Endpunktdienst.
- Fügen Sie PrivateLink-Verbindungen vom Adobe VPC zu anderen Endpunktdiensten hinzu oder entfernen Sie diese, die in der VPC-Umgebung des Kunden verfügbar sind.

## Für bidirektionale PrivateLink-Verbindungen einrichten

Der VPC des Kunden muss über die folgenden Ressourcen verfügen, um bidirektionale PrivateLink-Verbindungen zu unterstützen:

- Netzlastausgleich (NLB)
- Eine Endpunktdienstkonfiguration, die den Zugriff auf eine Anwendung oder einen Dienst über den VPC des Kunden ermöglicht
- Ein [Schnittstellenendpunkt] (AWS) oder [privater Endpunkt] (Azure), die es Adobe ermöglicht, eine Verbindung zu Endpunktdiensten herzustellen, die in Ihrem VPC gehostet werden

Wenn diese Ressourcen im VPC des Kunden nicht verfügbar sind, müssen Sie sich bei Ihrem Cloud-Plattformkonto anmelden, um die Konfiguration hinzuzufügen.

- Amazon VPC-Konsole - `https://console.aws.amazon.com/vpc/`
- Azure portal- `https://portal.azure.com`

Anweisungen zum Einrichten von PrivateLink finden Sie in der Dokumentation zur Cloud-Plattform:

- **Dokumentation zu AWS PrivateLink**
   - [Erstellen eines Netzwerk-Lastenausgleichs]
   - [Endpunktdienstkonfiguration erstellen]
   - [Erstellen eines Endpunkts für die Benutzeroberfläche]
   - [Lebenszyklus des Schnittstellenendpunkts]

- **Azure PrivateLink-Dokumentation**
   - [Erstellen eines Lastenausgleichs]
   - [Workflow für Azure Private Link]

<!--Link definitions-->

[Annehmen und Ablehnen von Verbindungsanfragen für Schnittstellenendpunkte]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Berechtigungen für Ihren Endpunktdienst hinzufügen und entfernen]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon: Fehlerbehebung bei Verbindungsproblemen mit Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS: Fehlerbehebung für Endpunktdienstverbindungen]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Workflow für Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Erstellen eines Lastenausgleichs]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Erstellen eines Netzwerk-Lastenausgleichs]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Endpunktdienstkonfiguration erstellen]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Erstellen eines Endpunkts für die Benutzeroberfläche]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[Schnittstellenendpunkt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Verbindung zum privaten Endpunkt verwalten]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Verbindungsanfragen verwalten]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[privater Endpunkt]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
