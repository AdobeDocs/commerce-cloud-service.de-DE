---
title: Firewall-Eigenschaft
description: Siehe Beispiele zum Konfigurieren der Firewall-Eigenschaft in der Konfigurationsdatei der Commerce-Anwendung.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
source-git-commit: a8ecebc87bfae5deaf0fc7ff3e7dd3b255fe3f24
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Firewall-Eigenschaft

>[!IMPORTANT]
>
>Nur Starterprojekte

Bei Starter-Projekten fügt die Eigenschaft `firewall` der Anwendung eine _ausgehende_ -Firewall hinzu. Diese Firewall wirkt sich nicht auf eingehende Anfragen aus. Sie definiert, welche `tcp` ausgehenden Anforderungen _eine Adobe Commerce-Site verlassen können._ Dies wird als Egress-Filterung bezeichnet. Die ausgehende Firewall filtert, was aus Ihrer Site ausgehen kann, also Ihre Site verlassen oder entkommen kann. Durch die Beschränkung von Escape-Funktionen wird Ihrem Server ein leistungsstarkes Sicherheitstool hinzugefügt.

## Standardmäßige Einschränkungsrichtlinien

Die Firewall bietet zwei Standardrichtlinien zur Steuerung des ausgehenden Traffics: `allow` und `deny`. Die `allow` Richtlinie _erlaubt standardmäßig den gesamten ausgehenden Traffic._ Und die `deny` Richtlinie _verweigert_ standardmäßig den gesamten ausgehenden Traffic. Wenn Sie jedoch eine Regel hinzufügen, wird die Standardrichtlinie überschrieben und die Firewall blockiert den von der Regel nicht zulässigen ausgehenden Traffic **all**.

Bei Startplänen wird die Standardrichtlinie auf `allow` gesetzt. Diese Einstellung stellt sicher, dass der gesamte ausgehende Traffic bis zum Hinzufügen Ihrer Ausstiegsfilterregeln entsperrt bleibt. Die Standardrichtlinie kann auf Anfrage auf `deny` gesetzt werden.

**Überprüfen der Standardrichtlinie**:

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

Sofern Sie nicht `deny` für Ihre Richtlinie angefordert haben, sollte der Befehl zeigen, dass Ihre Richtlinie auf `allow` festgelegt ist:

```json
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Schlüsselmitnahme**: Wenn Sie eine ausgehende Regel hinzufügen, blockieren Sie den gesamten ausgehenden Traffic mit Ausnahme der Domänen, IP-Adressen oder Ports, die Sie zur Regel hinzufügen. Daher ist es wichtig, eine vollständige ausgehende Liste zu definieren und zu testen, bevor sie zu Ihrer Produktionssite hinzugefügt wird.

## Firewall-Optionen

Die folgende Beispielkonfiguration in der Datei `.magento.app.yaml` zeigt alle `firewall` -Optionen, die Sie zum Hinzufügen von Regeln für Ihre Ausgangsfilterung verwenden können.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Filterregeln auswerten

Ausgehende Firewall-Konfigurationen bestehen aus Regeln. Sie können beliebig viele Regeln definieren. Die Anforderungen für Regeln lauten wie folgt.

**Jede Regel:**

- Muss mit einem Bindestrich (`-`) beginnen. Durch Hinzufügen eines Kommentars für dieselbe Zeile können Sie eine Regel visuell von der nächsten trennen.
- Muss mindestens eine der folgenden Optionen definieren: `domains`, `ips` oder `ports`.
- Muss das Protokoll `tcp` verwenden. Da dies das Standardprotokoll für alle Regeln ist, können Sie es aus der Regel auslassen.
- Kann `domains` oder `ips` definieren, aber nicht beide in derselben Regel.
- Kann `yaml` Kommentare (`#`) und Zeilenumbrüche enthalten, um die zulässigen Domänen, IP-Adressen und Ports zu organisieren.

Jede Regel verwendet die folgenden Eigenschaften:

### `domains`

Die Option `domains` ermöglicht eine Liste mit vollständig qualifizierten Domänennamen (FQDN).

Wenn eine Regel &quot;`domains`&quot;, aber nicht &quot;`ports`&quot; definiert, lässt die Firewall Domänenanforderungen an beliebige Ports zu.

### `ips`

Die Option `ips` ermöglicht eine Liste von IP-Adressen in der CIDR-Notation. Sie können einzelne IP-Adressen oder IP-Adressbereiche angeben.

Um eine einzelne IP-Adresse anzugeben, fügen Sie das Präfix `/32` CIDR am Ende Ihrer IP-Adresse hinzu:

```
172.217.11.174/32  # google.com
```

Um einen IP-Adressbereich anzugeben, verwenden Sie den Taschenrechner [IP-Bereich bis CIDR](https://ipaddressguide.com/cidr) .

Wenn eine Regel &quot;`ips`&quot;, aber nicht &quot;`ports`&quot; definiert, lässt die Firewall IP-Anfragen an jedem Port zu.

### `ports`

Die Option `ports` ermöglicht eine Liste der Ports von 1 bis 65535. Für die meisten Regeln im Beispiel sind sowohl HTTP- als auch HTTPS-Anfragen für die Ports `80` und `443` zulässig. Für New Relic ist der Zugriff auf Domänen und IP-Adressen jedoch nur über Port `443` möglich, wie in der New Relic-Dokumentation unter [Netzwerkverkehr](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents) empfohlen.

Wenn eine Regel nur `ports` definiert, erlaubt die Firewall den Zugriff auf alle Domänen und IP-Adressen für die definierten Ports.

>[!NOTE]
>
>Port `25`, der SMTP-Port zum Senden von E-Mails, wird immer blockiert, ohne Ausnahme.

### `protocol`

Wie bereits erwähnt, ist TCP das standardmäßige und einzige für Regeln zulässige Protokoll. UDP und seine Ports sind nicht zulässig. Aus diesem Grund können Sie die Option `protocol` in allen Regeln auslassen. Wenn Sie ihn trotzdem einbeziehen möchten, müssen Sie den Wert auf `tcp` setzen, wie in der ersten Regel des Beispiels gezeigt.

## Suchen nach Domänennamen, die zulassen

Mithilfe des folgenden Befehls können Sie die Domänen identifizieren, die in Ihre Ausgangsfilterregeln aufgenommen werden sollen, um die `dns.log` -Datei Ihres Servers zu analysieren und eine Liste aller DNS-Anfragen anzuzeigen, die von Ihrer Site protokolliert wurden:

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

Dieser Befehl zeigt auch DNS-Anfragen an, die von Ihren Egress-Filterregeln vorgenommen, aber blockiert wurden. Die Ausgabe zeigt nicht an, welche Domänen blockiert wurden, sondern nur, dass Anforderungen gestellt wurden. Die Ausgabe zeigt keine Anfragen an, die mithilfe einer IP-Adresse gestellt wurden.

```
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Domänen sind im Gegensatz zu IP-Adressen normalerweise spezifischer und sicherer für die Ausstiegsfilterung. Wenn Sie beispielsweise eine IP-Adresse für einen Dienst hinzufügen, der ein CDN verwendet, gestatten Sie die IP-Adresse für das CDN, das von Hunderten oder Tausenden anderen Domänen verwendet werden kann. Mit einer IP-Adresse können Sie ausgehenden Zugriff auf Tausende andere Server zulassen.

## Egress-Filterregeln testen

Nachdem Sie die Zugriffsregeln für die Domänen und IP-Adressen erfasst und konfiguriert haben, die Ihre Site benötigt, ist es an der Zeit, Push-Benachrichtigungen und Tests durchzuführen.

So testen Sie Ihre Ausgangsfilterregeln:

1. Erstellen Sie ein Shell-Skript mit `curl` Befehlen, um auf die Domänen und IP-Adressen in Ihren Regeln zuzugreifen. Binden Sie Befehle ein, die den Zugriff auf Domänen und IP-Adressen testen, die blockiert werden sollen.

1. Konfigurieren Sie einen `post_deploy` -Hook in Ihrer `.magento.app.yaml`-Datei, um das Skript auszuführen.

1. Schicken Sie Ihre `firewall`-Konfiguration und Ihr Testskript an Ihren `integration`-Zweig.

1. Überprüfen Sie die Ausgabe `post_deploy` von Ihren `curl` Befehlen.

1. Verfeinern Sie Ihre `firewall`-Regeln, aktualisieren Sie Ihr `curl`-Skript, begeben Sie es, pten Sie es und wiederholen Sie es.

### Skriptbeispiel für `curl`

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### Beispiel für `post_deploy`

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
