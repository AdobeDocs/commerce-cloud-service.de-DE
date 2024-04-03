---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
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
>Vor dem 5. Juni 2020 bereitgestellte Projekte enthielten mehrere kleinere Integrationsumgebungen. Wenn Sie für Tests und Entwicklung eine größere Integrationsumgebung benötigen, fordern Sie eine Aktualisierung auf die Umgebungen für optimierte Integration an. Siehe [Anforderung der Integrationsumgebung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) im _Adobe Commerce Help Center_ für Details.

## Zusammenführungsoptionen {#merge-options}

Standardmäßig überschreibt der Bereitstellungsprozess alle Einstellungen im `env.php` -Datei. Sie können jedoch einen oder mehrere Werte für eine Dienstkonfiguration zusammenführen, ohne alle Werte zu überschreiben.

Legen Sie die `_merge` -Option auf eine der folgenden Optionen:

- `true`—**Zusammenführen** die konfigurierten Dienstwerte mit den Umgebungsvariablenwerten.
- `false`—**Überschreiben** die konfigurierten Dienstwerte mit den Umgebungsvariablenwerten.

## Privates Repository {#private-repository}

>[!NOTE]
>
>Adobe empfiehlt dringend die Verwendung eines privaten Repositorys für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur, um geschützte Informationen oder Entwicklungsarbeiten wie Erweiterungen und vertrauliche Konfigurationen zu schützen.

## Professionelle Selbstbedienungswarnung {#pro-self-service-warning}

>[!WARNING]
>
>Einige **Pro Projekte** ein Support-Ticket zum Aktualisieren der Routenkonfiguration im `routes.yaml` und die Cron-Konfiguration in der `.magento.app.yaml` -Datei. Adobe empfiehlt, die YAML-Konfigurationsdateien in einer Integrationsumgebung zu aktualisieren und zu testen und anschließend Änderungen in der Staging-Umgebung bereitzustellen. Wenn Ihre Änderungen nach der erneuten Bereitstellung nicht auf Staging-Sites angewendet werden und keine entsprechenden Fehlermeldungen im Protokoll vorhanden sind, dann **MUST** [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) beschreibt die versucht Konfigurationsänderungen. Schließen Sie alle aktualisierten YAML-Konfigurationsdateien in das Ticket ein.

## Pro-Services-Unterstützung {#pro-update-service}

>[!TIP]
>Für Pro-Projekte müssen Sie [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) installieren oder aktualisieren [Dienstleistungen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) in `Staging` und `Production` nur Umgebungen.
>
>Geben Sie die erforderlichen Dienständerungen an, fügen Sie Ihre aktualisierte `.magento.app.yaml` und `services.yaml` und geben Sie die PHP-Version im Ticket an. Informationen zu Self-Service-Änderungen an PHP-Versionen, Erweiterungen oder Umgebungseinstellungen finden Sie unter [PHP-Einstellungen](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) in _Anwendungskonfiguration_.
>
>Für Änderungen an einer _live_ Produktionsumgebung (**Nur Pro**), müssen Sie eine Benachrichtigung von mindestens 48 Stunden bereitstellen, damit das Cloud-Infrastruktur-Team genügend Zeit hat, Ressourcen zu mobilisieren und ein sicheres Upgrade durchzuführen.

## Pro Backups {#pro-backups}

>[!TIP]
>
>In Pro-Staging- und Produktionsumgebungen müssen Sie [Senden eines Adobe Commerce Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um ein bestimmtes Backup abzurufen, das Datum, Uhrzeit und Zeitzone im Ticket angibt.
>
>Adobe tut **not** Wiederherstellung von Umgebungen aus einer automatischen Sicherung. Siehe [Wiederherstellen eines DB-Schnappschusses aus Staging oder Produktion](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) für Hilfe bei der Auswahl einer Methode zum Wiederherstellen eines Staging- oder Produktions-Snapshots.

## Warnung erneut bereitstellen {#redeploy-warning}

>[!WARNING]
>
>Der Bereitstellungsprozess beginnt, wenn Sie eine Zusammenführung, Push-Benachrichtigung oder Synchronisation Ihrer Umgebung durchführen oder wenn Sie eine manuelle Neuimplementierung Trigger haben, während der die [!DNL Commerce] Die Anwendung befindet sich im Wartungsmodus. Für eine Produktionsumgebung empfiehlt Adobe, diese Arbeit außerhalb der Spitzenzeiten abzuschließen, um Dienstunterbrechungen zu vermeiden.

## Routenplatzhalter {#route-placeholder}

>[!NOTE]
>
>Die folgenden Routenkonfigurationsbeispiele verwenden Routenvorlagen mit Platzhaltern. Die `{default}` Platzhalter stellt die für Ihre Site konfigurierte Standarddomäne dar. Wenn Ihr Projekt mehrere Domänen hat, verwenden Sie die `{all}` Platzhalter zum Konfigurieren des Routing für die Standarddomäne und alle Aliase. Siehe [Routen konfigurieren](/help/cloud-guide/routes/routes-yaml.md).

## SCD-Timing {#scd-timing-warning}

>[!WARNING]
>
>Wenn Sie nach der Bereitstellung Probleme mit statischen Inhaltsdateien in Ihrer Anwendung haben, z. B. fehlende benutzerdefinierte Designdateien, erhöhen Sie die maximale erwartete Ausführungszeit auf 900 Sekunden oder höher.

## Szenario-basierte Bereitstellung {#scenarios}

>[!NOTE]
>
>Mit [!DNL ECE-Tools] 2002.1.0 und höher können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um die Build-, Bereitstellungs- und Nachbereitstellungsprozesse für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur anzupassen. Siehe [Szenario-basierte Bereitstellung](/help/cloud-guide/deploy/scenario-based.md).

## Dienstanweisung {#service-instruction}

Verwenden Sie die folgenden Anweisungen für die Diensteinrichtung in Pro Integration-Umgebungen und Starter-Umgebungen, einschließlich der `master` -Verzweigung.

>[!NOTE]
>
>[Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um die Dienstkonfiguration in Pro Produktions- und Staging-Umgebungen zu ändern.

## Dienständerung {#service-change-tip}

>[!TIP]
>
>Nach der Ersteinrichtung des Dienstes können Sie die Softwareversion für einen installierten Dienst ändern, indem Sie die `services.yaml` und `.magento.app.yaml` Konfigurationsdateien. Siehe [Dienstversion ändern](/help/cloud-guide/services/services-yaml.md#change-service-version) für Anleitungen zum Upgrade oder Downgrade eines Dienstes.

## Tipps zur blockierten Bereitstellung {#stuck-deployment-tip}

>[!TIP]
>
>Hilfe zu blockierten Bereitstellungen erhalten Sie über die [Fehlerbehebung bei der Adobe Commerce-Bereitstellung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) im _Commerce Help Center_.

## Aktualisierung der ECE-Tools {#ece-tools-package}

>[!NOTE]
>
>Wenn Sie eine Version von Adobe Commerce in einer Cloud-Infrastruktur verwenden, die die Variable `ece-tools` -Paket erstellen, müssen Sie dann eine [einmalige Aktualisierung](/help/cloud-guide/dev-tools/install-package.md) in Ihr Cloud-Projekt klicken, um veraltete Pakete zu entfernen. Wenn Sie derzeit `ece-tools` und Sie müssen es aktualisieren, siehe [ECE-Tools-Paket aktualisieren](/help/cloud-guide/dev-tools/update-package.md).

## Upgrade-Tipp {#upgrade-tip}

>[!TIP]
>
>Bevor Sie mit einem Upgrade- oder Patchprozess beginnen, erstellen Sie einen aktiven Zweig aus der Integrationsumgebung und checken Sie die neue Verzweigung auf Ihrer lokalen Workstation aus. Wenn Sie eine Verzweigung dem Upgrade- oder Patch-Prozess zuweisen, können Sie Störungen Ihrer laufenden Arbeit vermeiden.

<!-- Fastly-related snippets begin -->

## Administratoranmeldung {#admin-login-step}

1. [Anmelden](/help/get-started/onboarding.md#access-your-admin-panel) an den Administrator.

## Benutzerdefinierte VCL-Snippet-Bereitstellung automatisieren {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>Anstatt benutzerdefinierte VCL-Snippets manuell hochzuladen, können Sie Snippets zum `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` -Verzeichnis in Ihrer Umgebung. Snippets in diesem Verzeichnis werden beim Klicken auf _VCL auf Fastly hochladen_ im Commerce Admin. Siehe [Automatisierte Bereitstellung benutzerdefinierter VCL-Snippets](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) im Fastly CDN-Modul für die Magento 2-Dokumentation.

<!-- Fastly-related snippets end -->
