---
title: Umgebungsvariablen
description: Sehen Sie sich eine Liste der für Adobe Commerce spezifischen Umgebungsvariablen in der Cloud-Infrastruktur an.
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Umgebungsvariablen

Mit Adobe Commerce in der Cloud-Infrastruktur können Sie Umgebungsvariablen zuweisen, um Konfigurationsoptionen zu überschreiben. Das Paket `ece-tools` legt Werte in der Datei `env.php` basierend auf Werten aus [Cloud-Variablen](variables-cloud.md), Variablen, die in der Konfigurationsdatei [!DNL Cloud Console] festgelegt sind, und `.magento.env.yaml` fest.

Die Umgebungsvariablen in der Datei `.magento.env.yaml` passen die Cloud-Umgebung an, indem Sie Ihre vorhandene Commerce-Konfiguration überschreiben. Wenn der Standardwert `Not Set` ist, ergreift das `ece-tools` -Paket die Aktion **NO** und verwendet den Standardwert [!DNL Commerce] oder den Wert aus der `MAGENTO_CLOUD_RELATIONSHIPS` -Konfiguration. Wenn der Standardwert festgelegt ist, wird dieser Standardwert durch das Paket `ece-tools` festgelegt.

Zu den Umgebungsvariablen gehören:

- [ADMIN](variables-admin.md)—Variablen überschreiben Projekt-ADMIN-Variablen
- [MAGENTO_CLOUD](variables-cloud.md)—Variablen, die für die Cloud-Infrastruktur spezifisch sind
- In der Datei `.magento.env.yaml` verwendete Variablen:
   - [Global](variables-global.md) - Variablen wirken sich auf die Build-, Bereitstellungs- und Postbereitstellungs-Phasen aus
   - [Build](variables-build.md)—Variablen steuern Build-Aktionen
   - [Bereitstellen](variables-deploy.md)—Variablen steuern die Bereitstellungsaktionen
   - [Post-deploy](variables-post-deploy.md)—Variablen steuern Aktionen nach der Bereitstellung

Variablen sind _hierarchisch_, d. h. wenn eine Variable nicht überschrieben wird, wird sie von der übergeordneten Umgebung übernommen.

Sie können [ADMIN-Variablen](variables-admin.md) über die [!DNL Cloud Console] oder die Adobe Commerce-CLI festlegen. Sie können andere Umgebungsvariablen in der Datei [`.magento.env.yaml`](configure-env-yaml.md) verwalten, um Build- und Bereitstellungsaktionen in allen Ihren Umgebungen zu verwalten - einschließlich Pro Staging und Produktion - ohne ein Support-Ticket zu benötigen.

>[!TIP]
>
>Bei YAML-Dateien wird zwischen Groß- und Kleinschreibung unterschieden und Tabs sind nicht zulässig. Achten Sie darauf, einen konsistenten Einzug in der gesamten Datei `.magento.env.yaml` zu verwenden, da Ihre Konfiguration sonst möglicherweise nicht wie erwartet funktioniert. Die Beispiele in dieser Dokumentation und in der Beispieldatei verwenden den Einzug _two-space_ . Verwenden Sie den Befehl [ece-tools validate](configure-env-yaml.md#validate-configuration-file) , um Ihre Konfiguration zu überprüfen.
