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

Mit Adobe Commerce in der Cloud-Infrastruktur können Sie Umgebungsvariablen zuweisen, um Konfigurationsoptionen zu überschreiben. Die `ece-tools` -Paket legt Werte in der `env.php` Datei basierend auf Werten aus [Cloud-Variablen](variables-cloud.md), Variablen, die in der Variablen [!DNL Cloud Console]und die `.magento.env.yaml` Konfigurationsdatei.

Die Umgebungsvariablen in der `.magento.env.yaml` die Cloud-Umgebung durch Überschreiben Ihrer bestehenden Commerce-Konfiguration anpassen. Wenn der Standardwert `Not Set`, dann die `ece-tools` Paket akzeptiert **NO** und verwendet die [!DNL Commerce] Standardwert oder Wert aus dem `MAGENTO_CLOUD_RELATIONSHIPS` Konfiguration. Wenn der Standardwert festgelegt ist, wird die `ece-tools` -Paket verwendet, um diesen Standardwert festzulegen.

Zu den Umgebungsvariablen gehören:

- [ADMIN](variables-admin.md)—variables override project ADMIN variables
- [MAGENTO_CLOUD](variables-cloud.md)—spezifische Variablen für die Cloud-Infrastruktur
- In der Variablen `.magento.env.yaml` Datei:
   - [Global](variables-global.md)—Variablen wirken sich auf die Build-, Bereitstellungs- und Postbereitstellungs-Phasen aus
   - [Build](variables-build.md)—variables steuern Build-Aktionen
   - [Bereitstellen](variables-deploy.md)—variables control deploy actions
   - [Nach der Bereitstellung](variables-post-deploy.md)—variables steuern Aktionen nach der Bereitstellung

Variablen sind _hierarchisch_, was bedeutet, dass eine Variable, die nicht überschrieben wird, von der übergeordneten Umgebung übernommen wird.

Sie können [ADMIN-Variablen](variables-admin.md) aus dem [!DNL Cloud Console] oder die Adobe Commerce-CLI verwenden. Sie können andere Umgebungsvariablen über die [`.magento.env.yaml`](configure-env-yaml.md) -Datei zum Verwalten von Build- und Bereitstellungsaktionen in all Ihren Umgebungen - einschließlich Pro Staging und Produktion - ohne dass ein Support-Ticket erforderlich ist.

>[!TIP]
>
>Bei YAML-Dateien wird zwischen Groß- und Kleinschreibung unterschieden und Tabs sind nicht zulässig. Achten Sie darauf, einen konsistenten Einzug im gesamten `.magento.env.yaml` -Datei oder Ihre Konfiguration funktioniert möglicherweise nicht wie erwartet. Die Beispiele in dieser Dokumentation und in der Beispieldatei verwenden _zwei Leerzeichen_ Einzug. Verwenden Sie die [ece-tools validate, Befehl](configure-env-yaml.md#validate-configuration-file) , um Ihre Konfiguration zu überprüfen.
