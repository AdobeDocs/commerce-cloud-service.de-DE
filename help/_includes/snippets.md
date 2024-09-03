---
source-git-commit: 762ce3cb6268401b0f5fae5b2280a870aa9c83a5
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---
# Cloud-Snippets

## Elasticsearch-Warnung {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 und höher wird für Adobe Commerce in der Cloud-Infrastruktur nicht unterstützt. Adobe Commerce-Versionen 2.3.7-p3, 2.4.3-p2, 2.4.4 und höher unterstützen den OpenSearch-Dienst. Die Vor-Ort-Anlagen unterstützen weiterhin Elasticsearch.

## Verbesserte Integration {#enhanced-integration-envs}

>[!NOTE]
>
>Vor dem 5. Juni 2020 bereitgestellte Projekte enthielten mehrere kleinere Integrationsumgebungen. Wenn Sie für Tests und Entwicklung eine größere Integrationsumgebung benötigen, fordern Sie eine Aktualisierung auf die Umgebungen für optimierte Integration an. Weitere Informationen finden Sie im Artikel [Anforderung der Integrationsumgebung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) im _Adobe Commerce Help Center_ .

## Zusammenführungsoptionen {#merge-options}

Standardmäßig überschreibt der Bereitstellungsprozess alle Einstellungen in der Datei `env.php`. Sie können jedoch einen oder mehrere Werte für eine Dienstkonfiguration zusammenführen, ohne alle Werte zu überschreiben.

Legen Sie die Option `_merge` auf einen der folgenden Werte fest:

- `true`—**Führen Sie die konfigurierten Dienstwerte mit den Umgebungsvariablenwerten zusammen.**
- `false`—**Überschreiben** Sie die konfigurierten Dienstwerte mit den Umgebungsvariablenwerten.

## Privates Repository {#private-repository}

>[!NOTE]
>
>Adobe empfiehlt dringend die Verwendung eines privaten Repositorys für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur, um geschützte Informationen oder Entwicklungsarbeiten wie Erweiterungen und vertrauliche Konfigurationen zu schützen.

## Professionelle Selbstbedienungswarnung {#pro-self-service-warning}

>[!WARNING]
>
>Einige **Pro-Projekte** benötigen ein Support-Ticket, um die Routenkonfiguration in der Datei `routes.yaml` und die Cron-Konfiguration in der Datei `.magento.app.yaml` zu aktualisieren. Adobe empfiehlt, die YAML-Konfigurationsdateien in einer Integrationsumgebung zu aktualisieren und zu testen und anschließend Änderungen in der Staging-Umgebung bereitzustellen. Wenn Ihre Änderungen nach der erneuten Bereitstellung nicht auf Staging-Sites angewendet werden und keine zugehörigen Fehlermeldungen im Protokoll vorhanden sind, senden Sie ein Adobe Commerce-Supportticket ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), in dem die versucht wurde, die Konfigurationsänderungen zu beschreiben. ****[ Schließen Sie alle aktualisierten YAML-Konfigurationsdateien in das Ticket ein.

## Pro-Services-Unterstützung {#pro-update-service}

>[!TIP]
>Für Pro-Projekte müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um [Dienste](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) nur in `Staging` - und `Production` -Umgebungen zu installieren oder zu aktualisieren.
>
>Geben Sie die erforderlichen Dienständerungen an, fügen Sie Ihre aktualisierten Dateien `.magento.app.yaml` und `services.yaml` ein und geben Sie die PHP-Version im Ticket an. Informationen zu Self-Service-Änderungen an PHP-Versionen, Erweiterungen oder Umgebungseinstellungen finden Sie unter [PHP-Einstellungen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) in _Anwendungskonfiguration_.
>
>Für Änderungen an einer _Live_-Produktionsumgebung (**Nur Pro**) müssen Sie eine Benachrichtigung über mindestens 48 Stunden bereitstellen, damit das Cloud-Infrastrukturteam genügend Zeit hat, Ressourcen zu marsheren und eine sichere Aktualisierung durchzuführen. Der Benachrichtigungszeitraum umfasst keine Wochenenden. Wenn Sie beispielsweise möchten, dass Ihre Service-Upgrades am Montag durchgeführt werden, müssen Sie die Anfrage bis zum vorigen Mittwoch übermitteln.

## Pro Backups {#pro-backups}

>[!TIP]
>
>In Pro-Staging- und Produktionsumgebungen müssen Sie [ein Adobe Commerce-Support-Ticket senden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket), um ein bestimmtes Backup abzurufen, in dem Datum, Uhrzeit und Zeitzone des Tickets angegeben werden.
>
>Adobe stellt **nicht** alle Umgebungen aus einer automatischen Sicherung wieder her. Unter [Wiederherstellen eines DB-Snapshots aus Staging oder Produktion](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) finden Sie Informationen zur Auswahl einer Methode zum Wiederherstellen eines Staging- oder Produktions-Snapshots.

## Warnung erneut bereitstellen {#redeploy-warning}

>[!WARNING]
>
>Der Bereitstellungsprozess beginnt, wenn Sie eine Zusammenführung, Push-Benachrichtigung oder Synchronisation Ihrer Umgebung durchführen oder wenn Sie eine manuelle Neuimplementierung Trigger haben, während der sich die [!DNL Commerce] -Anwendung im Wartungsmodus befindet. Für eine Produktionsumgebung empfiehlt Adobe, diese Arbeit außerhalb der Spitzenzeiten abzuschließen, um Dienstunterbrechungen zu vermeiden.

## Routenplatzhalter {#route-placeholder}

>[!NOTE]
>
>Die folgenden Routenkonfigurationsbeispiele verwenden Routenvorlagen mit Platzhaltern. Der Platzhalter `{default}` stellt die für Ihre Site konfigurierte Standarddomäne dar. Wenn Ihr Projekt mehrere Domänen hat, verwenden Sie den Platzhalter `{all}` , um das Routing für die Standarddomäne und alle Aliase zu konfigurieren. Siehe [Routen konfigurieren](/help/cloud-guide/routes/routes-yaml.md).

## SCD-Timing {#scd-timing-warning}

>[!WARNING]
>
>Wenn Sie nach der Bereitstellung Probleme mit statischen Inhaltsdateien in Ihrer Anwendung haben, z. B. fehlende benutzerdefinierte Designdateien, erhöhen Sie die maximale erwartete Ausführungszeit auf 900 Sekunden oder höher.

## Szenario-basierte Bereitstellung {#scenarios}

>[!NOTE]
>
>Ab Version [!DNL ECE-Tools] 2002.1.0 können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um die Build-, Bereitstellungs- und Nachbereitstellungsprozesse für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anzupassen. Siehe [Scenario-basierte Bereitstellung](/help/cloud-guide/deploy/scenario-based.md).

## Dienstanweisung {#service-instruction}

Verwenden Sie die folgenden Anweisungen für die Diensteinrichtung in Pro Integration-Umgebungen und Starter-Umgebungen, einschließlich der Verzweigung `master` .

>[!NOTE]
>
>[Senden Sie ein Adobe Commerce-Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Dienstkonfiguration in Pro Production- und Staging-Umgebungen zu ändern.

## Dienständerung {#service-change-tip}

>[!TIP]
>
>Nach der Ersteinrichtung des Dienstes können Sie die Softwareversion für einen installierten Dienst ändern, indem Sie die Konfigurationsdateien `services.yaml` und `.magento.app.yaml` aktualisieren. Eine Anleitung zum Aktualisieren oder Herunterstufen eines Dienstes finden Sie unter [Dienstversion ändern](/help/cloud-guide/services/services-yaml.md#change-service-version) .

## Tipps zur blockierten Bereitstellung {#stuck-deployment-tip}

>[!TIP]
>
>Hilfe zu blockierten Bereitstellungen erhalten Sie mit der Fehlerbehebung bei der Adobe Commerce-Bereitstellung ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) im _Commerce Help Center_.[

## Aktualisierung der ECE-Tools {#ece-tools-package}

>[!NOTE]
>
>Wenn Sie eine Version von Adobe Commerce in der Cloud-Infrastruktur verwenden, die das Paket `ece-tools` nicht enthält, müssen Sie ein [ einmaliges Upgrade](/help/cloud-guide/dev-tools/install-package.md) auf Ihr Cloud-Projekt durchführen, um veraltete Pakete zu entfernen. Wenn Sie derzeit das Paket `ece-tools` verwenden und es aktualisieren müssen, finden Sie weitere Informationen unter [ECE-Tools-Paket aktualisieren](/help/cloud-guide/dev-tools/update-package.md) .

## Upgrade-Tipp {#upgrade-tip}

>[!TIP]
>
>Bevor Sie mit einem Upgrade- oder Patchprozess beginnen, erstellen Sie einen aktiven Zweig aus der Integrationsumgebung und checken Sie die neue Verzweigung auf Ihrer lokalen Workstation aus. Wenn Sie eine Verzweigung dem Upgrade- oder Patch-Prozess zuweisen, können Sie Störungen Ihrer laufenden Arbeit vermeiden.

<!-- Fastly-related snippets begin -->

## Administratoranmeldung {#admin-login-step}

1. [Melden Sie sich bei ](/help/get-started/onboarding.md#access-your-admin-panel) beim Administrator an.

## Benutzerdefinierte VCL-Snippet-Bereitstellung automatisieren {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>Anstatt benutzerdefinierte VCL-Snippets manuell hochzuladen, können Sie in Ihrer Umgebung Snippets zum Ordner &quot;`$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom`&quot;hinzufügen. Snippets in diesem Verzeichnis werden automatisch hochgeladen, wenn Sie in Commerce Admin auf _VCL auf Fastly hochladen_ klicken. Informationen zu Magento 2 finden Sie unter [Bereitstellung automatisierter benutzerdefinierter VCL-Snippets](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) im Fastly CDN-Modul.

<!-- Fastly-related snippets end -->
