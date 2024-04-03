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

Globale Variablen steuern Aktionen in jeder Phase der [!DNL Commerce] Bereitstellungsprozess: Erstellen, Bereitstellen und Nach der Bereitstellung. Da globale Variablen sich auf jede Phase auswirken, müssen Sie sie in der `global` der `.magento.env.yaml` Datei:

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

Wenn festgelegt auf `true`ermöglicht Cron die Ausführung von Nachrichtenwarteschlangen-Verbrauchern. Adobe I/O-Ereignisse für Adobe Commerce verwenden Nachrichtenwarteschlangen, um die Bereitstellung kritischer Ereignisse zu beschleunigen.

Adobe empfiehlt, auch die [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) in die `deploy` der `.magento.env.yaml` Datei mit `cron_run` auf `true`.

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

Wenn festgelegt auf `true`aktiviert Commerce-Webhooks. Der Webhook wird auf einem externen Endpunkt ausgeführt, z. B. einer App Builder-Laufzeitaktion oder eines Inventarverwaltungssystems eines Drittanbieters. Die [_Webhooks-Anleitung_](https://developer.adobe.com/commerce/extensibility/webhooks) beschreibt diese Funktion detailliert.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Überschreibt die minimale Protokollierungsstufe für alle Ausgabestreams ohne Änderung des Codes, was bei der Fehlerbehebung von Problemen bei der Bereitstellung hilfreich ist. Wenn Ihre Bereitstellung beispielsweise fehlschlägt, können Sie diese Variable verwenden, um die Protokollierungsgranularität global zu erhöhen. Siehe [Protokollebenen](log-handlers.md#log-levels). Die `min_level` -Wert in den Protokollierungs-Handlern überschreibt diese Einstellung.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>Die Einstellung für `MIN_LOGGING_LEVEL` ändert nicht die Konfiguration der Protokollebene für den Datei-Handler, der auf `debug` Standardmäßig.

## `SCD_ON_DEMAND`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Aktivieren Sie die Generierung von statischem Inhalt auf Anforderung eines Benutzers (SCD). Statische Inhalte nach Bedarf eignen sich ideal für den Entwicklungs- und Test-Workflow, da dadurch die Bereitstellungszeit verkürzt wird.

Laden Sie den Cache mithilfe des [`post_deploy` Hook](../application/hooks-property.md) reduziert Ausfallzeiten der Site. Die Cache-Erwärmung ist nur für Pro-Projekte verfügbar, die Staging- und Produktionsumgebungen in der [!DNL Cloud Console] und für Starter-Projekte. Fügen Sie die `SCD_ON_DEMAND` Umgebungsvariable auf `global` im Abschnitt `.magento.env.yaml` Datei:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

Die `SCD_ON_DEMAND` überspringt die SCD in beiden Phasen (Build und Bereitstellung), löscht die `pub/static` und `var/view_preprocessed` Ordner und schreibt Folgendes in die `app/etc/env.php` Datei:

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

Legen Sie `true` , um zu verhindern, dass statische Inhalte für übergeordnete Designs während der Build- und Bereitstellungsphase generiert werden. Wenn diese Option auf `true`, werden weniger statische Inhalte generiert, was die Erstellungs- und Bereitstellungszeiten insgesamt verbessert.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.3.0 und höher

[Baler](https://github.com/magento/baler) ist ein Modul, das Ihren generierten JavaScript-Code prüft und ein optimiertes JavaScript-Bundle erstellt. Wenn Sie das optimierte Bundle auf Ihrer Site bereitstellen, kann sich die Anzahl der Netzwerkanforderungen beim Laden Ihrer Site verringern und die Seitenladezeiten verbessern.

Legen Sie `true` , um Baler nach der Bereitstellung statischer Inhalte auszuführen.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installieren und konfigurieren Sie das Baler-Modul, bevor Sie diese Funktion verwenden. Da Baler in der Alpha-Version verfügbar ist, aktivieren Sie diese Option nur in Staging-Umgebungen.

## `SKIP_HTML_MINIFICATION`

- **Standard**:
   - `true`—for `ece-tools` 2002.0.13 und höher
   - `false`—für frühere Versionen von `ece-tools`
- **Version**—Adobe Commerce 2.1.4 und höher

Aktiviert oder deaktiviert das Kopieren von statischen Ansichtsdateien in die `<magento_root>/init/` -Verzeichnis am Ende der Build-Phase. Wenn auf `true`, werden die Dateien nicht kopiert und die HTML-Minimierung ist auf Anfrage verfügbar. Setzen Sie diesen Wert auf `true` zur Reduzierung von Ausfallzeiten bei der Bereitstellung in Staging- und Produktionsumgebungen.

- **`false`**—Kopiert die `view_preprocessed` Verzeichnis in `<magento_root>/init/` am Ende der Build-Phase und stellt den Ordner im `<magento_root>/var` -Verzeichnis am Anfang der Bereitstellungsphase.
- **`true`**—Aktiviert die On-Demand-HTML-Minimierung; tut dies _not_ Kopieren Sie die `<magento_root>var/view_preprocessed` der `<magento_root>/init/` -Verzeichnis am Ende der Build-Phase.

Fügen Sie die `SKIP_HTML_MINIFICATION` Umgebungsvariable auf `global` im Abschnitt `.magento.env.yaml` Datei:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Standard**—_Nicht festgelegt_
- **Version**—Adobe Commerce 2.1.4 und höher

Verwenden Sie die `X_FRAME_CONFIGURATION` zum Ändern der [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) Kopfzeilenkonfiguration für Ihre Adobe Commerce-Site. Diese Konfiguration steuert, wie der Browser eine Seite in einer `<frame>`, `<iframe>`oder `<object>`. Verwenden Sie eine der folgenden Optionen:

- `DENY`- Seite kann nicht in einem Frame angezeigt werden.
- `SAMEORIGIN`—(Die standardmäßige Adobe Commerce-Einstellung.) Die Seite kann nur in einem Frame mit derselben Herkunft wie die Seite selbst angezeigt werden.

>[!WARNING]
>
>Die `ALLOW-FROM <uri>` -Option ist veraltet, da sie von Adobe Commerce unterstützte Browser nicht mehr unterstützen. Siehe [Browserkompatibilität](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Fügen Sie die `X_FRAME_CONFIGURATION` Umgebungsvariable auf `global` im Abschnitt `.magento.env.yaml` Datei:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
