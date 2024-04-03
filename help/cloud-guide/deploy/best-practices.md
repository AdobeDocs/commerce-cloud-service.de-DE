---
title: Best Practices bei der Implementierung
description: Entdecken Sie Best Practices für die Bereitstellung von Adobe Commerce in der Cloud-Infrastruktur.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Best Practices bei der Implementierung

Erstellen und stellen Sie Skripte bereit, die aktiviert werden, wenn Sie Code in einer Remote-Umgebung zusammenführen. Diese Skripte verwenden eine Umgebung [Konfigurationsdateien](../environment/overview.md) und Anwendungscode zur Bereitstellung der Cloud-Infrastruktur mit entsprechenden Daten und Diensten. Außerdem werden diese Skripte verwendet, um die Adobe Commerce-Anwendung, Dienste von Drittanbietern und benutzerdefinierte Erweiterungen in der Cloud-Umgebung zu installieren oder zu aktualisieren.

Der Build- und Bereitstellungsprozess unterscheidet sich für jeden Plan geringfügig:

- **Startpläne**—Für die Integrationsumgebung erstellt und stellt jeder aktive Zweig für den Zugriff und die Tests in einer vollständigen Umgebung bereit. Testen Sie den Code nach dem Zusammenführen mit dem `staging` -Verzweigung. Um Ihre Site zu starten, müssen Sie Push `staging` nach `master` zur Bereitstellung in der Produktionsumgebung. Sie haben vollen Zugriff auf alle Zweige über die [!DNL Cloud Console] und die CLI-Befehle.

- **Pro Pläne**—Für die Integrationsumgebung erstellt und stellt jeder aktive Zweig für den Zugriff und die Tests in einer vollständigen Umgebung bereit. Führen Sie Ihren Code zum `integration` -Verzweigung vor dem Zusammenführen zu den Staging- und Produktionsumgebungen. Sie können mit der [!DNL Cloud Console] oder Verwendung von SSH und `magento-cloud` CLI-Befehle.

## Prozess verfolgen

Sie können Build- und Bereitstellungsaktionen in Echtzeit mithilfe des Terminals oder der [!DNL Cloud Console] Statusmeldungen -`in-progress`, `pending`, `success`oder `failed`—anzeigen während des Bereitstellungsprozesses. Sie können Details in den Protokolldateien anzeigen. Siehe [Protokolle anzeigen](../test/log-locations.md).

Wenn Sie externe GitHub-Repositorys verwenden, wird das Protokoll der Vorgänge nicht in der GitHub-Sitzung angezeigt. Sie können jedoch weiterhin Aktivitäten in der Benutzeroberfläche für das externe Repository und die [!DNL Cloud Console]. Siehe [Integrationen](../integrations/overview.md).

>[!NOTE]
>
>In Integrationsumgebungen können Sie die Bereitstellungsprotokolle nicht über die [!DNL Cloud Console]. Diese Funktion ist nur für Produktions- und Staging-Umgebungen verfügbar. Sie können jedoch Protokolle für jede Phase der Implementierung in jeder Umgebung anzeigen, indem Sie die [Build und Bereitstellung](../test/log-locations.md#build-and-deploy-logs) Protokolle. Informationen zur Fehlerbehebung finden Sie im Abschnitt [Referenz zu Bereitstellungsfehlern](../dev-tools/error-reference.md).

Sie können [Implementierungen mit New Relic verfolgen](../monitor/track-deployments.md) um Bereitstellungsereignisse zu überwachen und die Leistung zwischen Bereitstellungen zu analysieren.

## Best Practices für Builds und Implementierungen

Lesen Sie diese Best Practices und Überlegungen für Ihren Implementierungsprozess:

- **Stellen Sie sicher, dass Sie die neueste Version der `ece-tools` package**

  Siehe [Versionshinweise für ECE-Tools](../release-notes/ece-tools-package.md).

- **Folgen Sie dem Build- und Bereitstellungsprozess.**

  Stellen Sie sicher, dass Sie in jeder Umgebung über den richtigen Code verfügen, damit Konfigurationen beim Zusammenführen von Code zwischen Umgebungen nicht überschrieben werden. Um beispielsweise Konfigurationsänderungen auf alle Umgebungen anzuwenden, ändern und testen Sie die Änderungen in der lokalen Umgebung, bevor Sie sie in die Remote-Integrationsumgebung übernehmen. Stellen Sie dann die Änderungen bereit und testen Sie sie in der Staging-Umgebung, bevor Sie sie in der Produktion bereitstellen. Beim Zusammenführen von einer Umgebung zu einer anderen überschreibt die Bereitstellung den gesamten Code in der Umgebung, mit Ausnahme der umgebungsspezifischen Konfiguration und Einstellungen.

- **Umgebungsübergreifend dieselben Variablen verwenden**

  Die Werte für diese Variablen können sich von Umgebung zu Umgebung unterscheiden. Normalerweise benötigen Sie jedoch in jeder Umgebung dieselben Variablen. Siehe [Konfigurationsverwaltung für Speichereinstellungen](../store/store-settings.md).

- **Behalten Sie sensible Konfigurationswerte und Daten in umgebungsspezifischen Variablen bei**

  Zu diesen Werten gehören Variablen, die über die Cloud-CLI (die [!DNL Cloud Console]oder hinzugefügt `env.php` -Datei. Siehe [Variablenebenen](../environment/variable-levels.md).

- **Stellen Sie sicher, dass der gesamte Code in der Umgebungsverzweigung verfügbar ist.**

  Das Referenzieren von Code aus anderen Zweigen, z. B. einem privaten Zweig, kann während des Build- und Bereitstellungsprozesses zu Problemen führen. Wenn Sie beispielsweise von einem privaten Zweig aus auf ein Design verweisen, ist das Design nicht zugänglich und kann nicht mit dem Anwendungscode erstellt werden.

- **Hinzufügen von Erweiterungen, Integrationen und Code in iterierten Verzweigungen**

  Lokales Vornehmen und Testen von Änderungen per Push an `integration`, gefolgt von `staging` und `production`. Testen und beheben Sie Probleme in den einzelnen Umgebungen, bevor Sie die Aktualisierungen zur nächsten Umgebung zusammenführen. Einige Erweiterungen und Integrationen müssen aufgrund von Abhängigkeiten in einer bestimmten Reihenfolge aktiviert und konfiguriert werden. Das Hinzufügen und Testen in Gruppen kann Ihren Build- und Bereitstellungsprozess erheblich vereinfachen und dabei helfen festzustellen, wo Probleme auftreten.

- **Überprüfen von Dienstversionen und -beziehungen und der Fähigkeit, eine Verbindung herzustellen**

  Überprüfen Sie die Dienste, die für Ihre Anwendung verfügbar sind, und stellen Sie sicher, dass Sie die neueste, kompatible Version verwenden. Siehe [Service-Beziehungen](../services/services-yaml.md#service-relationships) und [Systemanforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) im _Installationshandbuch_ für empfohlene Versionen.

- **Testen Sie vor der Bereitstellung in der Staging- und Produktionsumgebung lokal und in der Integrationsumgebung**

  Identifizieren und beheben Sie Probleme in Ihren lokalen und Integrationsumgebungen, um längere Ausfallzeiten bei der Bereitstellung in Staging- und Produktionsumgebungen zu verhindern.

  >[!TIP]
  >
  >Es gibt [Smart-Assistent](../deploy/smart-wizards.md) -Befehle, mit denen Sie überprüfen können, ob Ihre Cloud-Projektkonfiguration den Best Practices für die Build- und Bereitstellungskonfiguration entspricht, einschließlich der Strategie für die Bereitstellung statischer Inhalte (SCD).

- **Stellen Sie nach Abschluss der Tests in lokalen Umgebungen und Integrationsumgebungen die Staging-Umgebung bereit und testen Sie sie**

  Siehe [Staging- und Produktionstests](../test/staging-and-production.md).

- **Konfiguration der Produktionsumgebung überprüfen**

  Führen Sie vor der Bereitstellung in der Produktion die folgenden Aufgaben aus:

   - Stellen Sie sicher, dass Sie mit allen drei Knoten in der Produktionsumgebung eine Verbindung herstellen können. [SSH](../development/secure-connections.md).

   - Stellen Sie sicher, dass die Indexer auf _Planmäßig aktualisieren_. Siehe [Indizierungsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/) im _Entwicklerhandbuch für Erweiterungen_.

   - Bereiten Sie die Umgebung vor, indem Sie alle umgebungsspezifischen Variablen im Produktionscode aktualisieren, die Verfügbarkeit und Kompatibilität der Dienste überprüfen und alle anderen erforderlichen Konfigurationsänderungen vornehmen.

- **Überwachen des Bereitstellungsprozesses**

  Überprüfen Sie die Bereitstellungsstatusmeldungen und beheben Sie Probleme bei Bedarf. Überprüfen der Cloud [logs](../test/log-locations.md#) für detaillierte Protokollmeldungen.

## Aufbau und Implementierung von fünf Phasen der Integration

Die folgenden Phasen erfolgen in Ihrer lokalen Entwicklungsumgebung und in der Integrationsumgebung. Bei Pro-Plänen wird der Code in diesen Anfangsphasen nicht in der Staging- oder Produktionsumgebung bereitgestellt.

### Phase 1: Code- und Konfigurationsvalidierung

Beim erstmaligen Einrichten eines Projekts [die Cloud-Infrastrukturvorlage](https://github.com/magento/magento-cloud) bietet eine Grundlage für die Code-Dateien. Dieses Code-Repo wird in Ihrem Projekt als `master` -Verzweigung.

- **Für Starter**—`master` ist Ihre Produktionsumgebung.
- **Für Pro**—`master` beginnt als Ursprungszweig für die Integrationsumgebung.

Erstellen einer Verzweigung aus `master` für Ihren benutzerdefinierten Code, Ihre Erweiterungen und Module sowie Drittanbieterintegrationen. Es gibt eine Remote-Integrationsumgebung zum Testen Ihres Codes in der Cloud.

Wenn Sie Ihren Code aus Ihrem lokalen Arbeitsbereich in das Remote-Repository pushen, wird eine Reihe von Prüfungen und Codeprüfungen abgeschlossen, bevor Skripte erstellt und bereitgestellt werden. Der integrierte Git-Server überprüft, was Sie übertragen, und nimmt Änderungen vor. Wenn Sie beispielsweise einen OpenSearch-Dienst hinzufügen, überprüft der integrierte Git-Server, ob die Topologie Ihres Clusters entsprechend geändert wird.

Wenn in einer Konfigurationsdatei ein Syntaxfehler auftritt, lehnt der Git-Server die Push-Benachrichtigung ab. Siehe [Schutzblock](../development/protective-block.md).

Diese Phase läuft auch ab `composer install` , um Abhängigkeiten abzurufen.

### Phase 2: Build

>[!NOTE]
>
>Während der Build-Phase befindet sich die Site nicht im Wartungsmodus und wenn Fehler oder Probleme auftreten, wird sie nicht heruntergefahren. Es wird nur der Code erstellt, der sich seit dem vorherigen Build geändert hat.

Diese Phase erstellt die Codebase und führt Hooks im `build` Abschnitt `.magento.app.yaml`. Der standardmäßige Build-Erweiterungspunkt ist der `php ./vendor/bin/ece-tools` und führt Folgendes aus:

- Wendet Patches in `vendor/magento/ece-patches`sowie optionale projektspezifische Patches in `m2-hotfixes`
- Regeneriert den Code und die [Abhängigkeitsinjektion](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) -Konfiguration (d. h. die `generated/` Verzeichnis, das Folgendes enthält: `generated/code` und `generated/metapackage`) mithilfe von `bin/magento setup:di:compile`.
- Prüft, ob die [`app/etc/config.php`](../store/store-settings.md) -Datei in der Codebase vorhanden ist. Adobe Commerce generiert diese Datei automatisch, wenn sie sie während der Build-Phase nicht erkennt, und enthält eine Liste von Modulen und Erweiterungen. Wenn sie vorhanden ist, wird die Build-Phase normal fortgesetzt, statische Dateien werden mit GZIP komprimiert und bereitgestellt, wodurch Ausfallzeiten in der Bereitstellungsphase reduziert werden. Siehe Abschnitt [Build-Optionen](../environment/variables-build.md) , um mehr über das Anpassen oder Deaktivieren der Dateikomprimierung zu erfahren.

>[!WARNING]
>
>Zu diesem Zeitpunkt wurde der Cluster noch nicht erstellt. Versuchen Sie daher nicht, eine Verbindung zu einer Datenbank herzustellen, oder gehen Sie davon aus, dass ein aktiver Daemon-Prozess vorhanden ist.

Nach dem Erstellen der Anwendung wird sie auf einem **schreibgeschütztes Dateisystem**. Sie können bestimmte Bereitstellungspunkte konfigurieren, die gelesen/geschrieben werden sollen. Sie können nicht zum Server FTP hinzufügen und Module hinzufügen. Stattdessen müssen Sie Code zu Ihrem lokalen Repository hinzufügen und ausführen `git push`, der die Umgebung erstellt und bereitstellt. Informationen zur Projektstruktur finden Sie unter [Ordnerstruktur des lokalen Projekts](../project/file-structure.md).

### Phase 3: Vorbereiten der Lösung

Das Ergebnis der Build-Phase ist ein schreibgeschütztes Dateisystem, das als _Slug_. In dieser Phase wird ein Archiv erstellt und der Slug in permanenter Speicherung abgelegt. Wenn Sie das nächste Mal Code per Push senden und ein Dienst sich nicht geändert hat, wird der Slug aus dem Archiv verwendet.

- Beschleunigt die kontinuierliche Integration durch Wiederverwendung von unverändertem Code
- Wenn sich der Code ändert, aktualisiert das Slug für den nächsten Build, um ihn wiederzuverwenden.
- Ermöglicht bei Bedarf die sofortige Wiederherstellung einer Bereitstellung.
- Enthält statische Dateien, wenn die Variable `app/etc/config.php` in der Codebase vorhanden ist

Der Slug enthält alle Dateien und Ordner **Ausschließen der folgenden** in konfigurierte Bereitstellungen `magento.app.yaml`:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Phase 4: Bereitstellen von Schlägern und Clustern

Ihre Anwendungen und alle [Backend](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) Erbringung von Dienstleistungen wie folgt:

- Fügt jeden Dienst in einem Container ein, z. B. Webserver, OpenSearch, [!DNL RabbitMQ]
- Fügt das Lese- und Schreibdateisystem ein (auf einem hochverfügbaren verteilten Speichersystem bereitgestellt)
- Konfiguriert das Netzwerk, damit die Dienste einander (und nur einander) &quot;sehen&quot;können.

>[!NOTE]
>
>Nehmen Sie Ihre Änderungen in einer Git-Verzweigung vor, nachdem die Erstellung und Bereitstellung abgeschlossen und die Push-Benachrichtigung erneut durchgeführt wurde. Alle Umgebungsdateisysteme sind _schreibgeschützt_. Ein schreibgeschütztes System garantiert deterministische Bereitstellungen und verbessert die Sicherheit Ihrer Site erheblich, da kein Prozess in das Dateisystem schreiben kann. Außerdem wird sichergestellt, dass Ihr Code in den Umgebungen für Integration, Staging und Produktion identisch ist.

### Phase 5: Bereitstellungs-Hooks

>[!NOTE]
>
>Diese Phase setzt die [!DNL Commerce] Anwendung im Wartungsmodus bis zum Abschluss der Bereitstellung.

Im letzten Schritt wird ein Bereitstellungsskript ausgeführt, mit dem Sie Daten in Entwicklungsumgebungen anonymisieren, Caches löschen und externe Tools für die kontinuierliche Integration abfragen können. Wenn dieses Skript ausgeführt wird, haben Sie Zugriff auf alle Dienste in Ihrer Umgebung, z. B. Redis.

Wenn die Variable `app/etc/config.php` -Datei nicht in der Codebasis vorhanden ist, werden statische Dateien mit `gzip` und während dieser Phase bereitgestellt werden, wodurch sich die Dauer der Bereitstellungsphase und der Site-Wartung verlängert.

>[!NOTE]
>
>Siehe Abschnitt [Bereitstellungsvariablen](../environment/variables-deploy.md) , um mehr über das Anpassen oder Deaktivieren der Dateikomprimierung zu erfahren.

Es gibt zwei Bereitstellungshaken. Die `pre-deploy.php` -Erweiterungspunkt schließt die erforderliche Bereinigung und den Abruf der Ressourcen und des im Build-Erweiterungspunkt generierten Codes ab. Die `php ./vendor/bin/ece-tools deploy` -Erweiterungspunkt führt eine Reihe von Befehlen und Skripten aus:

- Wenn Adobe Commerce **nicht installiert**, installiert es mit `bin/magento setup:install`aktualisiert die Bereitstellungskonfiguration, `app/etc/env.php`und die Datenbank für Ihre angegebene Umgebung, z. B. Redis und Website-URLs. **Wichtig:** Als Sie die [Erstmalige Bereitstellung](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) während der Einrichtung wurde Adobe Commerce in allen Umgebungen installiert und bereitgestellt.

- Wenn Adobe Commerce **installiert ist** führen Sie alle erforderlichen Aktualisierungen durch. Das Bereitstellungsskript wird ausgeführt `bin/magento setup:upgrade` Aktualisierung des Datenbankschemas und der Daten (die nach Aktualisierung der Erweiterung oder des Kerncodes erforderlich sind) sowie Aktualisierung der Bereitstellungskonfiguration; `app/etc/env.php`und der Datenbank für Ihre Umgebung. Schließlich löscht das Bereitstellungsskript den Adobe Commerce-Cache.

- Das Skript generiert optional statische Webinhalte mithilfe des Befehls . `magento setup:static-content:deploy`.

- Verwendet Bereiche (`-s` Markierung in Build-Skripten) mit der Standardeinstellung `quick` für die Bereitstellungsstrategie für statische Inhalte. Sie können die Strategie mithilfe der Umgebungsvariablen anpassen [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Weitere Informationen zu diesen Optionen und Funktionen finden Sie unter [Bereitstellungsstrategien für statische Dateien](../deploy/static-content.md) und `-s` Markierung für [Bereitstellen von statischen Ansichtsdateien](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>Das Bereitstellungsskript verwendet die Werte, die durch Konfigurationsdateien im `.magento` und löscht dann das Skript das Verzeichnis und dessen Inhalt. Ihre lokale Entwicklungsumgebung ist nicht betroffen.

### Nach der Bereitstellung: Routing konfigurieren

Während die Bereitstellung ausgeführt wird, stoppt der Prozess den eingehenden Traffic am Einstiegspunkt für 60 Sekunden und konfiguriert das Routing neu, sodass Ihr Web-Traffic in den neu erstellten Cluster gelangt.

Eine erfolgreiche Implementierung entfernt den Wartungsmodus, um normalen Zugriff zu ermöglichen, und erstellt Backup-Dateien (BAK) für die `app/etc/env.php` und `app/etc/config.php` Konfigurationsdateien.

Aktivieren Sie die statische Inhaltserstellung mithilfe der `SCD_ON_DEMAND` und konfigurieren Sie die [`post_deploy` Hook](../application/hooks-property.md) so, dass der Cache gelöscht und der Cache vorgeladen wird (erwärmt) _after_ der Container beginnt, Verbindungen zu akzeptieren, und _during_ normalen, eingehenden Traffic.

Informationen zum Überprüfen von Build- und Bereitstellungsprotokollen finden Sie unter [Protokolle anzeigen](../test/log-locations.md#view-and-manage-logs).
