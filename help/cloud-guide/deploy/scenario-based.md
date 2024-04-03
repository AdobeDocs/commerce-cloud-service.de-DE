---
title: Szenario-basierte Bereitstellung
description: Erfahren Sie, wie Sie Adobe Commerce in Cloud-Infrastrukturbereitstellungen mithilfe benutzerdefinierter Konfigurationsdateien anpassen können.
feature: Cloud, Configuration, Deploy, Build
exl-id: df243068-c7a3-46dd-abe9-9e05198fa343
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Szenario-basierte Bereitstellung

Mit `ece-tools` 2002.1.0 und höher können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um das standardmäßige Bereitstellungsverhalten anzupassen.
Diese Funktion verwendet **Szenarien** und **Schritte** in der Konfiguration:

- **Szenariokonfiguration**-Jeder Bereitstellungshaken ist ein *scenario*, eine XML-Konfigurationsdatei, die die Sequenz- und Konfigurationsparameter zum Ausführen von Bereitstellungsaufgaben beschreibt. Sie konfigurieren die Szenarien im `hooks` Abschnitt `.magento.app.yaml` -Datei.

- **Schrittkonfiguration**-Jedes Szenario verwendet eine Sequenz von *Schritte* in dem die zum Ausführen von Bereitstellungsaufgaben erforderlichen Vorgänge programmatisch beschrieben werden. Sie konfigurieren die Schritte in einer XML-basierten Szenario-Konfigurationsdatei.

Adobe Commerce on Cloud Infrastructure bietet eine Reihe von [Standardszenarien](https://github.com/magento/ece-tools/tree/2002.1/scenario) und [Standardschritte](https://github.com/magento/ece-tools/tree/2002.1/src/Step) im `ece-tools` Paket. Sie können das Bereitstellungsverhalten anpassen, indem Sie benutzerdefinierte XML-Konfigurationsdateien erstellen, um die Standardkonfiguration zu überschreiben oder anzupassen. Sie können auch Szenarien und Schritte verwenden, um Code aus benutzerdefinierten Modulen auszuführen.

## Szenarien mithilfe von Build- und Bereitstellungs-Hooks hinzufügen

Sie fügen die Szenarien zum Erstellen und Bereitstellen von Adobe Commerce zum `hooks` Abschnitt `.magento.app.yaml` -Datei. Jeder Erweiterungspunkt gibt die Szenarien an, die während jeder Phase ausgeführt werden sollen. Das folgende Beispiel zeigt die Standardszenario-Konfiguration.

> `magento.app.yaml` Hooks

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!NOTE]
>
>Mit der Veröffentlichung von `ece-tools` 2002.1.x gibt es eine neue [Hooks-Konfiguration](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property.html) Format. Das ältere Format aus `ece-tools` Versionen 2002.0.x werden weiterhin unterstützt. Sie müssen jedoch auf das neue Format aktualisieren, um die szenario-basierte Bereitstellungsfunktion zu verwenden.

## Überprüfen von Szenario-Schritten

In der Hook-Konfiguration ist jedes Szenario eine XML-Datei, die Schritte zum Ausführen von Build-, Bereitstellungs- oder Post-Bereitstellungsaufgaben enthält. Beispiel: die `scenario/transfer` -Datei umfasst drei Schritte: `compress-static-content`, `clear-init-directory`, und `backup-data`

> `scenario/transfer.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="compress-static-content" type="Magento\MagentoCloud\Step\Build\CompressStaticContent" priority="100"/>
    <step name="clear-init-directory" type="Magento\MagentoCloud\Step\Build\ClearInitDirectory" priority="200"/>
    <step name="backup-data" type="Magento\MagentoCloud\Step\Build\BackupData" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="static-content" xsi:type="object" priority="100">Magento\MagentoCloud\Step\Build\BackupData\StaticContent</item>
                <item name="writable-dirs" xsi:type="object"  priority="200">Magento\MagentoCloud\Step\Build\BackupData\WritableDirectories</item>
            </argument>
        </arguments>
    </step>
</scenario>
```

## Erweitern eines Standardszenarios

Im folgenden Beispiel wird das standardmäßige Bereitstellungsszenario erweitert, indem zusätzliche Bereitstellungskonfigurationsdateien an die Hook-Konfiguration angehängt werden.

```yaml
hooks:
  deploy: |
    php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/<vendor-name>/<module-name>/deploy.xml vendor/<vendor-name>/<module-name>/deploy2.xml
```

Während der Bereitstellung werden die benutzerdefinierten Szenarien anhand der folgenden Regeln mit dem Standardszenario zusammengeführt:

- Szenarien werden anhand ihrer Reihenfolge in der Hook-Definition priorisiert, wobei das letzte aufgelistete Szenario die höchste Priorität hat.

  Im Beispiel haben die Szenarien die folgende Priorität:

   1. `vendor/vendor-name/module-name/deploy2.xml`
   1. `vendor/vendor-name/module-name/deploy.xml`
   1. `scenario/deploy.xml` (Standard- oder Basisszenario)

- Die Schritte im Szenario mit der höchsten Priorität überschreiben die Schritte mit demselben Namen in den anderen Szenarien. Der Konfiguration werden neue Schritte hinzugefügt. Die gleichen Regeln gelten für mehr als zwei Szenarien, wobei jedes Szenario von rechts nach links priorisiert wird, z. B. (C → B → A).

### Standardschritte entfernen

Sie entfernen Schritte aus Standardszenarien mit dem `skip` -Parameter.

Um beispielsweise die Variable `enable-maintenance-mode` und `set-production-mode` Erstellen Sie im standardmäßigen Bereitstellungsszenario eine Konfigurationsdatei, die die folgende Konfiguration enthält.

> `vendor/vendor-name/module-name/deploy-custom-mode-config.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="enable-maintenance-mode" skip="true" />
    <step name="set-production-mode"  skip="true" />
</scenario>
```

Um die benutzerdefinierte Konfigurationsdatei zu verwenden, aktualisieren Sie die standardmäßige `.magento.app.yaml` -Datei.

> `.magento.app.yaml` mit benutzerdefiniertem Bereitstellungsszenario

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-custom-mode-config.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

### Standardschritte ersetzen

Benutzerdefinierte Szenarien können die Standardschritte zur Bereitstellung einer benutzerdefinierten Implementierung ersetzen. Verwenden Sie dazu den standardmäßigen Schrittnamen als Namen für den benutzerdefinierten Schritt.

Beispiel: in der [Standardbereitstellungs-Szenario] die `enable-maintenance-mode` -Schritt führt den Standardwert aus [EnableMaintenanceMode PHP-Skript].

```xml
<step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="300"/>
```

Um diesen Schritt zu überschreiben, erstellen Sie eine benutzerdefinierte Szenario-Konfigurationsdatei, um ein anderes Skript auszuführen, wenn die `enable-maintenance-mode` -Schritt ausgeführt wird.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="VendorName\VendorModule\Step\CustomEnableMaintenanceMode" priority="300"/>
</scenario>
```

### Schrittpriorität ändern

Benutzerdefinierte Szenarien können die Priorität von Standardschritten ändern. Der folgende Schritt ändert die Priorität der `enable-maintenance-mode` Schritt aus `300` nach `10` , damit der Schritt im Bereitstellungsszenario früher ausgeführt wird.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="10"/>
</scenario>
```

In diesem Beispiel wird die `enable-maintenance-mode` Der Schritt wird an den Anfang des Szenarios verschoben, da er eine geringere Priorität hat als alle anderen Schritte im standardmäßigen Bereitstellungsszenario.

### Beispiel: Erweitern des Bereitstellungsszenarios

Im folgenden Beispiel wird die [Standardbereitstellungs-Szenario] mit den folgenden Änderungen:

- Ersetzt die `remove-deploy-failed-flag` Schritt mit einem benutzerdefinierten Schritt
- Überspringt die `clean-redis-cache` Schritt im Schritt vor der Bereitstellung
- Überspringt die `unlock-cron-jobs` Schritt
- Überspringt die `validate-config` Schritt zum Deaktivieren kritischer Validatoren
- Fügt einen neuen Schritt vor der Bereitstellung hinzu

> `vendor/vendor-name/module-name/deploy-extended.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <!-- Replace "remove-deploy-failed-flag" step with custom step -->
    <step name="remove-deploy-failed-flag" type="Vendor\ModuleName\Step\Deploy\RemoveDeployFailedFlag" priority="100"/>

    <!-- Skip "clean-redis-cache" sub-step in pre-deploy step -->
    <step name="pre-deploy" type="Magento\MagentoCloud\Step\Deploy\PreDeploy" priority="200">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="clean-redis-cache" xsi:type="object" skip="true"/>
            </argument>
        </arguments>
    </step>

    <!-- Skip step "unlock-cron-jobs" -->
    <step name="unlock-cron-jobs" skip="true"/>

    <!-- Skip critical validators -->
    <step name="validate-config" type="Magento\MagentoCloud\Step\ValidateConfiguration" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="validators" xsi:type="array">
                <item name="critical" xsi:type="array">
                    <item name="database-configuration" xsi:type="object" skip="true"/>
                    <item name="search-configuration" xsi:type="object" skip="true"/>
                </item>
            </argument>
        </arguments>
    </step>

    <!-- Add new step into the beginning of the deploy scenario -->
    <step name="new-pre-deploy-step" type="Vendor\ModuleName\Step\Deploy\PreDeploy" priority="10"/>
</scenario>
```

Um dieses Skript in Ihrem Projekt zu verwenden, fügen Sie die folgende Konfiguration zum `.magento.app.yaml` Datei für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur:

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-extended.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!TIP]
>
>Sie können die [Standardszenarien](https://github.com/magento/ece-tools/tree/2002.1/scenario) und [Standardschrittkonfiguration](https://github.com/magento/ece-tools/tree/2002.1/src/Step) im `ece-tools` GitHub-Repository , um zu bestimmen, welche Szenarien und Schritte für Ihre Aufgaben zum Erstellen, Bereitstellen und nach der Bereitstellung angepasst werden sollen.

## Hinzufügen eines benutzerdefinierten Moduls zum Erweitern `ece-tools`

Die `ece-tools` -Paket bietet standardmäßige API-Schnittstellen, die den Standards der Semantic Version entsprechen. Alle API-Schnittstellen sind mit **@api** -Anmerkung. Sie können die standardmäßige API-Implementierung durch Ihre eigene ersetzen, indem Sie ein benutzerdefiniertes Modul erstellen und den Standardcode nach Bedarf ändern.

Um das benutzerdefinierte Modul mit Adobe Commerce in der Cloud-Infrastruktur zu verwenden, müssen Sie Ihr Modul in der Erweiterungsliste für die `ece-tools` Paket. Der Registrierungsprozess ähnelt dem Prozess, den Sie zur Registrierung von Modulen in Adobe Commerce verwenden.

**So registrieren Sie ein Modul bei der `ece-tools` package**:

1. Erstellen oder erweitern Sie die `registration.php` -Datei im Stammverzeichnis Ihres Moduls.

   ```php?start_inline=1
   \Magento\MagentoCloud\ExtensionRegistrar::register('module-name', __DIR__);
   ```

1. Aktualisieren Sie die `autoload` -Abschnitt für Ihre Modulkonfigurationsdatei, die die `registration.php` Datei zu automatischen Moduldateien in `composer.json`.

   ```json
   {
     "name": "vendor/ece-tools-extend",
     "description": "Extension for ece-tools",
     "type": "magento2-component",
     "version": "1.0.0",
     "license": "OSL-3.0",
     "autoload": {
       "files": [ "registration.php" ],
       "psr-4": {
         "Vendor\\EceToolExtend\\": "src/"
       }
     }
   }
   ```

1. Fügen Sie die `config/services.xml` -Datei in Ihr -Modul. Diese Konfiguration wird zusammengeführt `config/services.xml` von `ece-tools` Paket.

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <container xmlns="http://symfony.com/schema/dic/services"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://symfony.com/schema/dic/services https://symfony.com/schema/dic/services/services-1.0.xsd">
       <services>
           <defaults autowire="true" autoconfigure="true" public="true"/>
   
           <prototype namespace="Vendor\EceToolExtend\" resource="../src/*" exclude="../src/{Test}"/>
   
           <!-- Use your own implementation of EnvironmentDataInterface -->
           <service id="Magento\MagentoCloud\Config\EnvironmentDataInterface" alias="Vendor\EceToolExtend\Config\CustomEnvironmentData" />
       </services>
   </container>
   ```

Weitere Informationen zur Injektion von Abhängigkeiten finden Sie unter [Symfony Dependency Injection](https://symfony.com/doc/current/components/dependency_injection.html).

<!-- link definitions -->

[Standardbereitstellungs-Szenario]: https://github.com/magento/ece-tools/blob/develop/scenario/deploy.xml
[EnableMaintenanceMode PHP-Skript]: https://github.com/magento/ece-tools/blob/develop/src/Step/EnableMaintenanceMode.php
