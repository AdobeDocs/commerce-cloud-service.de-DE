---
title: Smart-Assistenten
description: Erfahren Sie, wie Sie mithilfe von intelligenten Assistenten bewerten können, ob Ihr Adobe Commerce on Cloud-Infrastrukturprojekt Best Practices für die Bereitstellung befolgt.
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Smart-Assistenten

Mithilfe der intelligenten Assistenten können Sie feststellen, ob Ihre Cloud-Konfiguration Best Practices befolgt. Die verfügbaren Assistenten unterstützen die folgenden Konfigurationen:

- Ideal für minimale Bereitstellungsausfälle
- Lastenausgleichskonfiguration für Datenbank und Redis
- Statische Inhaltsbereitstellung (SCD) für On-Demand, die Build-Phase oder die Bereitstellungsphase

Jeder der Befehle des intelligenten Assistenten bietet eine Überprüfungsantwort und ggf. eine Empfehlung für die richtige Konfiguration.

| Befehl | Beschreibung |
| ------- | ------------|
| `wizard:ideal-state` | Überprüfen Sie, ob sich die SCD in der Phase _Build_ befindet, die Variable `SKIP_HTML_MINIFICATION` auf `true` und der Hook &quot;post_deploy&quot;in der Cloud-Umgebung konfiguriert sind. Nicht zur Verwendung in der lokalen Entwicklungsumgebung. |
| `wizard:master-slave` | Überprüfen Sie, ob die Variable `REDIS_USE_SLAVE_CONNECTION` und die Variable `MYSQL_USE_SLAVE_CONNECTION` den Wert `true` haben. |
| `wizard:scd-on-demand` | Überprüfen Sie, ob die globale Umgebungsvariable `SCD_ON_DEMAND` `true` ist. |
| `wizard:scd-on-build` | Überprüfen Sie, ob die globale Umgebungsvariable `SCD_ON_DEMAND` den Wert `false` hat und die Umgebungsvariable `SKIP_SCD` den Wert `false` für die Phase _build_ aufweist. Überprüft, ob die Datei &quot;`config.php`&quot; Informationen für Stores, Store-Gruppen und Websites enthält. |
| `wizard:scd-on-deploy` | Überprüfen Sie, ob die globale Umgebungsvariable `SCD_ON_DEMAND` den Wert `false` hat und die Umgebungsvariable `SKIP_SCD` den Wert `false` für die Phase _deploy_ aufweist. Stellt sicher, dass die Datei &quot;`config.php`&quot;_NOT_&quot;die Liste der Stores, Store-Gruppen und Websites mit zugehörigen Informationen enthält. |

Beispielsweise können Sie überprüfen, ob Ihre Konfiguration die On-Demand-Funktion von SCD ordnungsgemäß aktiviert:

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Eine erfolgreiche Konfiguration gibt Folgendes zurück:

```terminal
SCD on-demand is enabled
```

Eine fehlgeschlagene Konfiguration gibt zurück:

```terminal
SCD on-demand is disabled
```

## Überprüfen einer idealen Konfiguration

Die _ideale_ -Konfiguration für Ihr Cloud-Projekt trägt dazu bei, Bereitstellungsausfälle zu minimieren, indem der Cache erwärmt und statische Inhalte auf Anforderung des Benutzers generiert werden. Dieser Assistent wird während der Bereitstellung automatisch ausgeführt. Wenn Ihre Cloud nicht für diesen _idealen Status_ konfiguriert ist, erhalten Sie eine Nachricht ähnlich der folgenden:

```terminal
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

Basierend auf der Ausgabe müssen Sie die folgenden Korrekturen an Ihrer Konfiguration vornehmen:

1. Aktivieren Sie die Minimierungsvariable HTML überspringen .

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. Konfigurieren Sie den Hook nach der Bereitstellung.

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. Übernehmen Sie die Codeänderungen und führen Sie den Test erneut aus. Wenn Ihre Konfiguration _ideal_ ist, erhalten Sie die folgende Meldung.

   ```terminal
   Ideal state is configured
   ```
