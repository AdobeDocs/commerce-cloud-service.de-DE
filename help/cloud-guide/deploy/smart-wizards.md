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
| `wizard:ideal-state` | Überprüfen Sie, ob sich die SCD auf der _build_ stage, die `SKIP_HTML_MINIFICATION` Variable ist `true`und den in der Cloud-Umgebung konfigurierten Hook post_deploy. Nicht zur Verwendung in der lokalen Entwicklungsumgebung. |
| `wizard:master-slave` | Stellen Sie sicher, dass die `REDIS_USE_SLAVE_CONNECTION` und die `MYSQL_USE_SLAVE_CONNECTION` Variable ist `true`. |
| `wizard:scd-on-demand` | Stellen Sie sicher, dass die `SCD_ON_DEMAND` globale Umgebungsvariable ist `true`. |
| `wizard:scd-on-build` | Stellen Sie sicher, dass die `SCD_ON_DEMAND` globale Umgebungsvariable ist `false` und `SKIP_SCD` Umgebungsvariable ist `false` für die _build_ Bühne. Überprüft, ob die `config.php` -Datei enthält Informationen für Stores, Store-Gruppen und Websites. |
| `wizard:scd-on-deploy` | Stellen Sie sicher, dass die `SCD_ON_DEMAND` globale Umgebungsvariable ist `false` und `SKIP_SCD` Umgebungsvariable ist `false` für die _deploy_ Bühne. Überprüft, ob die `config.php` Datei _NOT_ enthalten die Liste der Stores, Store-Gruppen und Websites mit verwandten Informationen. |

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

Die _ideal_ Die Konfiguration für Ihr Cloud-Projekt trägt dazu bei, Bereitstellungsausfälle zu minimieren, indem der Cache erwärmt und statische Inhalte generiert werden, wenn dies vom Benutzer angefordert wird. Dieser Assistent wird während der Bereitstellung automatisch ausgeführt. Wenn Ihre Cloud dafür nicht konfiguriert ist _idealer Zustand_, erhalten Sie eine Nachricht ähnlich der folgenden:

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

1. Übernehmen Sie die Codeänderungen und führen Sie den Test erneut aus. Wann Ihre Konfiguration _ideal_, erhalten Sie die folgende Nachricht.

   ```terminal
   Ideal state is configured
   ```
