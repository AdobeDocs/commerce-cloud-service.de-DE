---
title: Globale Variablen
description: Sehen Sie sich die Liste der Umgebungsvariablen an, die Aktionen in der Adobe Commerce bei der Bereitstellung der Cloud-Infrastruktur steuern.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Globale Variablen

Globale Variablen steuern Aktionen in jeder Phase des [!DNL Commerce]-Bereitstellungsprozesses: Erstellen, Bereitstellen und Nach der Bereitstellung. Da globale Variablen sich auf jede Phase auswirken, müssen Sie sie in der `global` -Phase der `.magento.env.yaml`-Datei festlegen:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Weitere Informationen zum Anpassen des Build- und Bereitstellungsprozesses finden Sie unter

- [Bereitstellungskonfiguration](configure-env-yaml.md)
- [Bereitstellungsprozess](../deploy/process.md)

## `ENABLE_EVENTING`

- **Standard**-_Nicht festgelegt_
- **Version**—Adobe Commerce 2.4.5 und höher

Wenn auf `true` gesetzt, ermöglicht cron die Ausführung von Nachrichtenwarteschlangenkonsumenten. Adobe I/O-Ereignisse für Adobe Commerce verwenden Nachrichtenwarteschlangen, um die Bereitstellung kritischer Ereignisse zu beschleunigen.

Adobe empfiehlt, die Variable [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) auch zur `deploy` -Phase der `.magento.env.yaml` -Datei hinzuzufügen, wobei `cron_run` auf `true` eingestellt ist.

Das folgende Beispiel zeigt eine vollständig konfigurierte `ENABLE_EVENTING` -Variable.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Standard**-_Nicht festgelegt_
- **Version**—Adobe Commerce 2.4.4 und höher

Wenn auf `true` gesetzt, aktiviert Commerce-Webhooks. Der Webhook wird auf einem externen Endpunkt ausgeführt, z. B. einer App Builder-Laufzeitaktion oder eines Bestandsverwaltungssystems von Drittanbietern. Im [_Webhooks-Handbuch_](https://developer.adobe.com/commerce/extensibility/webhooks) wird diese Funktion ausführlich beschrieben.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Überschreibt die minimale Protokollierungsstufe für alle Ausgabestreams ohne Änderung des Codes, was bei der Fehlerbehebung von Problemen bei der Bereitstellung hilfreich ist. Wenn Ihre Bereitstellung beispielsweise fehlschlägt, können Sie diese Variable verwenden, um die Protokollierungsgranularität global zu erhöhen. Siehe [Protokollebenen](log-handlers.md#log-levels). Der Wert `min_level` in den Protokollierungs-Handlern überschreibt diese Einstellung.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>Die Einstellung für die Variable `MIN_LOGGING_LEVEL` ändert nicht die Konfiguration der Protokollebene für den Datei-Handler, der standardmäßig auf `debug` festgelegt ist.

## `SCD_ON_DEMAND`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivieren Sie die Generierung von statischem Inhalt auf Anforderung eines Benutzers (SCD). Statische Inhalte nach Bedarf eignen sich ideal für den Entwicklungs- und Test-Workflow, da dadurch die Bereitstellungszeit verkürzt wird.

Durch das Vorausfüllen des Caches mit dem [`post_deploy`-Hook](../application/hooks-property.md) werden die Site-Ausfallzeiten reduziert. Die Cache-Erwärmung ist nur für Pro-Projekte verfügbar, die Staging- und Produktionsumgebungen in den [!DNL Cloud Console] und für Starter-Projekte enthalten. Fügen Sie die Umgebungsvariable `SCD_ON_DEMAND` in der `.magento.env.yaml` -Datei der `global`-Phase hinzu:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

Die Variable `SCD_ON_DEMAND` überspringt die SCD in beiden Phasen (Build und Bereitstellung), löscht die Ordner `pub/static` und `var/view_preprocessed` und schreibt Folgendes in die Datei `app/etc/env.php`:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.2.0 und höher

Ermöglicht Ihnen, die maximale erwartete Ausführungszeit für die Bereitstellung statischer Inhalte zu erhöhen.

Standardmäßig wird von Adobe Commerce die maximal erwartete Ausführung auf 900 Sekunden festgelegt. In einigen Szenarien benötigen Sie jedoch möglicherweise mehr Zeit, um die Bereitstellung statischer Inhalte für ein Cloud-Projekt abzuschließen.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.4.2 und höher

Setzen Sie dies auf &quot;`true`&quot;, um zu verhindern, dass statische Inhalte für übergeordnete Designs während der Build- und Bereitstellungsphase generiert werden. Wenn diese Option auf &quot;`true`&quot; gesetzt ist, wird weniger statischer Inhalt generiert, was die Gesamterstellungs- und Bereitstellungszeiten verbessert.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.3.0 und höher

[Baler](https://github.com/magento/baler) ist ein Modul, das Ihren generierten JavaScript-Code prüft und ein optimiertes JavaScript-Bundle erstellt. Wenn Sie das optimierte Bundle auf Ihrer Site bereitstellen, kann sich die Anzahl der Netzwerkanforderungen beim Laden Ihrer Site verringern und die Seitenladezeiten verbessern.

Legen Sie diese Einstellung auf &quot;`true`&quot;fest, um Baler nach der Bereitstellung statischer Inhalte auszuführen.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installieren und konfigurieren Sie das Baler-Modul, bevor Sie diese Funktion verwenden. Da Baler in der Alpha-Version verfügbar ist, aktivieren Sie diese Option nur in Staging-Umgebungen.

## `SKIP_HTML_MINIFICATION`

- **Default**:
   - `true`—für `ece-tools` 2002.0.13 und höher
   - `false`—für frühere Versionen von `ece-tools`
- **Version**—Adobe Commerce 2.1.4 und höher

Aktiviert bzw. deaktiviert das Kopieren von statischen Ansichtsdateien in das Verzeichnis `<magento_root>/init/` am Ende der Build-Phase. Wenn der Wert auf `true` gesetzt ist, werden die Dateien nicht kopiert und die HTML-Minimierung ist auf Anfrage verfügbar. Setzen Sie diesen Wert auf `true` , um Ausfallzeiten bei der Bereitstellung in Staging- und Produktionsumgebungen zu reduzieren.

- **`false`**—Kopiert das Verzeichnis `view_preprocessed` am Ende der Build-Phase in das Verzeichnis `<magento_root>/init/` und stellt das Verzeichnis im Verzeichnis `<magento_root>/var` zu Beginn der Bereitstellungsphase wieder her.
- **`true`**—Aktiviert die On-Demand-HTML-Minimierung; kopiert _nicht_ die `<magento_root>var/view_preprocessed` am Ende der Build-Phase in den Ordner `<magento_root>/init/`.

Fügen Sie die Umgebungsvariable `SKIP_HTML_MINIFICATION` in der `.magento.env.yaml` -Datei der `global`-Phase hinzu:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Verwenden Sie die Variable `X_FRAME_CONFIGURATION` , um die Kopfzeilenkonfiguration [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) für Ihre Adobe Commerce-Site zu ändern. Diese Konfiguration steuert, wie der Browser eine Seite in einem `<frame>`, `<iframe>` oder `<object>` rendert. Verwenden Sie eine der folgenden Optionen:

- `DENY`: Seite kann nicht in einem Frame angezeigt werden.
- `SAMEORIGIN`—(Die standardmäßige Adobe Commerce-Einstellung.) Die Seite kann nur in einem Frame mit derselben Herkunft wie die Seite selbst angezeigt werden.

>[!WARNING]
>
>Die Option `ALLOW-FROM <uri>` wird nicht mehr unterstützt, da sie von Adobe Commerce unterstützte Browser nicht mehr unterstützen. Siehe [Browserkompatibilität](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Fügen Sie die Umgebungsvariable `X_FRAME_CONFIGURATION` in der `.magento.env.yaml` -Datei der `global`-Phase hinzu:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
