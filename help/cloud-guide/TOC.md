---
user-guide-title: Handbuch zu Commerce mit Cloud Infrastructure
user-guide-description: Erfahren Sie, wie Sie die Adobe Commerce-Anwendung in der Cloud-Infrastruktur verwalten.
product: magento
feature: Cloud
source-git-commit: ebd434e488b666d34df9562825a612b33495e44d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 7%

---


# Commerce on Cloud Infrastructure {#user-guide}

+ [Commerce](overview.md)
+ Architektur {#architecture}
   + [Cloud-Infrastruktur](architecture/cloud-architecture.md)
   + [Technologiestapel](architecture/tech-stack.md)
   + [Starterarchitektur](architecture/starter-architecture.md)
   + [Starter-Workflow](architecture/starter-develop-deploy-workflow.md)
   + [Pro Architektur](architecture/pro-architecture.md)
   + [Pro Workflow](architecture/pro-develop-deploy-workflow.md)
   + [Skalierte Architektur](architecture/scaled-architecture.md)
   + [Automatische Skalierung](architecture/autoscaling.md)
+ [Erste Schritte](https://experienceleague.adobe.com/docs/commerce-cloud-service/start/overview.html)
+ Versionshinweise {#release-notes}
   + [Cloud Tools-Suite](release-notes/cloud-tools-suite.md)
   + [ECE-Tools-Paket](release-notes/ece-tools-package.md)
   + [Cloud-Patches](release-notes/cloud-patches.md)
   + [Cloud Docker-Paket](release-notes/cloud-docker.md)
   + [Cloud-Komponenten](release-notes/cloud-components.md)
   + [Cloud-Pakete](release-notes/cloud-packages.md)
   + [Abwärtskompatible Änderungen](release-notes/backward-incompatible-changes.md)
   + [Archiv mit Versionshinweisen](release-notes/cloud-release-archive.md)
+ Cloud-Projekt {#project}
   + [Projektübersicht](project/overview.md)
   + [Projektstruktur](project/file-structure.md)
   + [Benutzerzugriff](project/user-access.md)
   + [Authentifizierung mit mehreren Faktoren](project/multi-factor-authentication.md)
   + [Aktivitäts-Stream](project/activity-stream.md)
   + [Ausgehende E-Mails](project/outgoing-emails.md)
   + [SendGrid-E-Mail-Dienst](project/sendgrid.md)
   + [Verwaltung von Konsolenverzweigungen](project/console-branches.md)
   + [Regionale IP-Adressen](project/regional-ip-addresses.md)
+ Entwicklertools {#dev-tools}
   + [Übersicht](dev-tools/overview.md)
   + Cloud CLI {#cloud-cli}
      + [CLI - Übersicht](dev-tools/cloud-cli-overview.md)
      + [CLI-Referenz](dev-tools/cloud-cli-reference.md)
   + [Cloud Docker](dev-tools/cloud-docker.md)
   + ECE-Tools {#ece-tools}
      + [Paketübersicht](dev-tools/package-overview.md)
      + [Einmalige Aktualisierung zur Verwendung der ECE-Tools](dev-tools/install-package.md)
      + [ECE-Tools-Paket aktualisieren](dev-tools/update-package.md)
      + [CLI-Referenz](dev-tools/ece-tools-cli-reference.md)
      + [Fehlerreferenz](dev-tools/error-reference.md)
   + Integrationen {#integrations}
      + [Übersicht](integrations/overview.md)
      + [Bitbucket](integrations/bitbucket.md)
      + [GitHub](integrations/github.md)
      + [GitLab](integrations/gitlab.md)
      + [Statusbenachrichtigungen](integrations/health-notifications.md)
+ Entwicklung {#develop}
   + [Übersicht](development/overview.md)
   + [Authentifizierungsschlüssel](development/authentication-keys.md)
   + [CLI-Zweigverwaltung](development/cli-branches.md)
   + [Sichere Verbindungen](development/secure-connections.md)
   + Bereitstellen {#deploy}
      + [Bereitstellungsprozess](deploy/process.md)
      + [Optimierung](deploy/optimization.md)
      + [Best Practices](deploy/best-practices.md)
      + [Szenario-basierte Bereitstellung](deploy/scenario-based.md)
      + [Keine Ausfallzeit-Bereitstellung](deploy/reduce-downtime.md)
      + [Statische Inhaltsbereitstellung](deploy/static-content.md)
      + [Smart-Assistenten](deploy/smart-wizards.md)
      + [Bereitstellen in Staging und Produktion](deploy/staging-production.md)
      + [Wiederherstellen nach Komponentenfehler](deploy/recover-failed-deployment.md)
   + Test {#test}
      + [Testleitfaden](test/guidance.md)
      + [Protokolle](test/log-locations.md)
      + [Xdebug](test/debug.md)
      + [Beispieldaten](test/sample-data.md)
      + [Staging und Produktion](test/staging-and-production.md)
   + [PrivateLink-Dienst](development/privatelink-service.md)
   + [Schutzblock](development/protective-block.md)
   + [Umgebung wiederherstellen](development/restore-environment.md)
   + Speicher {#storage}
      + [Verwalten des Festplattenspeichers](storage/manage-disk-space.md)
      + [Profildatenbankabfragen](storage/profile-database-queries.md)
      + [Datenbank sichern](storage/database-dump.md)
      + [Backup-Management](storage/snapshots.md)
   + Upgrades und Patches {#upgrade}
      + [Best Practices](development/best-practices.md)
      + [Upgrade der Commerce-Version](development/commerce-version.md)
      + [Anwenden von Patches](development/apply-patches.md)
+ Konfiguration {#configure}
   + [Übersicht](environment/overview.md)
   + Anwendung {#app}
      + [Anwendungsbereitstellung konfigurieren](application/configure-app-yaml.md)
      + [PHP-Einstellungen](application/php-settings.md)
      + Eigenschaften {#properties}
         + [Anwendungseigenschaften](application/properties.md)
         + [Krone](application/crons-property.md)
         + [Firewall (nur Starter)](application/firewall-property.md)
         + [Hooks](application/hooks-property.md)
         + [Variablen](application/variables-property.md)
         + [Web](application/web-property.md)
         + [Arbeitnehmer](application/workers-property.md)
      + [Festlegen des Cache für statische Dateien](application/set-cache.md)
   + Umgebung {#env}
      + [Konfigurieren der Umgebungsbereitstellung](environment/configure-env-yaml.md)
      + [Variablenebenen und Optionen](environment/variable-levels.md)
      + Variablen {#stage} überschreiben
         + [Umgebungsvariablen](environment/variables-intro.md)
         + [ADMIN](environment/variables-admin.md)
         + [Cloud-Variablen](environment/variables-cloud.md)
         + [Global](environment/variables-global.md)
         + [Build](environment/variables-build.md)
         + [Bereitstellen](environment/variables-deploy.md)
         + [Post-Bereitstellung](environment/variables-post-deploy.md)
      + Benachrichtigungen konfigurieren {#log}
         + [Benachrichtigungen](environment/set-up-notifications.md)
         + [Protokollhandler](environment/log-handlers.md)
   + Routen {#routes}
      + [Routen konfigurieren](routes/routes-yaml.md)
      + [Zwischenspeicherung](routes/caching.md)
      + [Umleitungen](routes/redirects.md)
      + [Serverseitige Includes](routes/server-side-includes.md)
   + Dienste {#service}
      + [Dienste konfigurieren](services/services-yaml.md)
      + [Elasticsearch](services/elasticsearch.md)
      + [MySQL](services/mysql.md)
      + [OpenSearch](services/opensearch.md)
      + [RabbitMQ](services/rabbitmq.md)
      + [Redis](services/redis.md)
+ Fastly Services {#cdn}
   + [Übersicht](cdn/fastly.md)
   + Schnelles Setup {#setup-fastly}
      + [Fastly Services konfigurieren](cdn/fastly-configuration.md)
      + [Cache-Konfiguration anpassen](cdn/fastly-custom-cache-configuration.md)
      + [Anpassen von Fehler- und Wartungsseiten](cdn/fastly-custom-response.md)
   + [Web-Anwendungs-Firewall](cdn/fastly-waf-service.md)
   + [Bildoptimierung](cdn/fastly-image-optimization.md)
   + Mit VCL anpassen {#custom-vcl-snippets}
      + [Erste Schritte](cdn/fastly-vcl-custom-snippets.md)
      + [Anforderungen an ein CMS-Backend umleiten](cdn/fastly-vcl-wordpress.md)
      + [Blockverweis-Spam](cdn/fastly-vcl-badreferer.md)
      + [IP-Zulassungsliste](cdn/fastly-vcl-allowlist.md)
      + [IP-Blockierungsliste](cdn/fastly-vcl-blocking.md)
      + [Schnellen Cache umgehen](cdn/fastly-vcl-bypass-to-origin.md)
   + [Schnelle Fehlerbehebung](cdn/fastly-troubleshooting.md)
+ Speichereinstellungen {#configure-store}
   + [Übersicht](store/overview.md)
   + [Best Practices](store/best-practices.md)
   + [Benutzerdefiniertes Design](store/custom-theme.md)
   + [Erweiterungen](store/extensions.md)
   + [B2B-Modul](store/b2b-module.md)
   + [Mehrere Sites](store/multiple-sites.md)
   + [Sitemap- und Suchmaschinenroboter](store/robots-sitemap.md)
   + [Zahlungsmethoden von PayPal](store/paypal.md)
   + [Konfigurationsverwaltung](store/store-settings.md)
+ Launch-Site {#launch}
   + [Übersicht](launch/overview.md)
   + [Checkliste für Launch](launch/checklist.md)
   + [Launch-Schritte](launch/steps.md)
+ Bildschirmseite {#monitor}
   + [Leistung](monitor/performance.md)
   + New Relic-Dienst {#new-relic}
      + [Übersicht über New Relic](monitor/new-relic-service.md)
      + [Konto- und Benutzerverwaltung](monitor/account-management.md)
      + Leistung untersuchen {#investigate}
         + [Richtlinien, Warnhinweise und Workflows](monitor/investigate-performance.md)
         + [Datenerfassung](monitor/ingest-data.md)
         + [Implementierungen verfolgen](monitor/track-deployments.md)
      + [Protokollverwaltung](monitor/log-management.md)
