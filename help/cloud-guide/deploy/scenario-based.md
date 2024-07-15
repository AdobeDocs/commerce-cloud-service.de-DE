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

Ab Version `ece-tools` 2002.1.0 können Sie die szenario-basierte Bereitstellungsfunktion verwenden, um das standardmäßige Bereitstellungsverhalten anzupassen.
Diese Funktion verwendet **szenarien** und **Schritte** in der Konfiguration:

- **Szenario-Konfiguration** - Jeder Bereitstellungs-Hook ist ein *szenario*, bei dem es sich um eine XML-Konfigurationsdatei handelt, die die Sequenz- und Konfigurationsparameter zum Ausführen von Bereitstellungsaufgaben beschreibt. Sie konfigurieren die Szenarien im Abschnitt `hooks` der Datei `.magento.app.yaml` .

- **Schrittkonfiguration** - Jedes Szenario verwendet eine Sequenz von *Schritten* , die die zum Ausführen von Bereitstellungsaufgaben erforderlichen Vorgänge programmgesteuert beschreiben. Sie konfigurieren die Schritte in einer XML-basierten Szenario-Konfigurationsdatei.

Adobe Commerce in der Cloud-Infrastruktur bietet eine Reihe von [Standardszenarien](https://github.com/magento/ece-tools/tree/2002.1/scenario) und [Standardschritte](https://github.com/magento/ece-tools/tree/2002.1/src/Step) im Paket `ece-tools`. Sie können das Bereitstellungsverhalten anpassen, indem Sie benutzerdefinierte XML-Konfigurationsdateien erstellen, um die Standardkonfiguration zu überschreiben oder anzupassen. Sie können auch Szenarien und Schritte verwenden, um Code aus benutzerdefinierten Modulen auszuführen.

## Szenarien mithilfe von Build- und Bereitstellungs-Hooks hinzufügen

Sie fügen die Szenarien zum Erstellen und Bereitstellen von Adobe Commerce zum Abschnitt &quot;`hooks`&quot;der Datei &quot;`.magento.app.yaml`&quot;hinzu. Jeder Erweiterungspunkt gibt die Szenarien an, die während jeder Phase ausgeführt werden sollen. Das folgende Beispiel zeigt die Standardszenario-Konfiguration.

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
>Mit der Veröffentlichung von `ece-tools` 2002.1.x gibt es ein neues Format für die [Hooks-Konfiguration](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property.html). Das ältere Format aus den Versionen `ece-tools` 2002.0.x wird weiterhin unterstützt. Sie müssen jedoch auf das neue Format aktualisieren, um die szenario-basierte Bereitstellungsfunktion zu verwenden.

## Überprüfen von Szenario-Schritten

In der Hook-Konfiguration ist jedes Szenario eine XML-Datei, die Schritte zum Ausführen von Build-, Bereitstellungs- oder Post-Bereitstellungsaufgaben enthält. Beispielsweise umfasst die Datei `scenario/transfer` drei Schritte: `compress-static-content`, `clear-init-directory` und `backup-data`

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
   1. `scenario/deploy.xml` (Standard- oder Grundlinienszenario)

- Die Schritte im Szenario mit der höchsten Priorität überschreiben die Schritte mit demselben Namen in den anderen Szenarien. Der Konfiguration werden neue Schritte hinzugefügt. Die gleichen Regeln gelten für mehr als zwei Szenarien, wobei jedes Szenario von rechts nach links priorisiert wird, z. B. (C → B → A).

### Standardschritte entfernen

Sie entfernen Schritte aus Standardszenarien mit dem Parameter `skip` .

Um beispielsweise die Schritte `enable-maintenance-mode` und `set-production-mode` im standardmäßigen Bereitstellungsszenario zu überspringen, erstellen Sie eine Konfigurationsdatei mit der folgenden Konfiguration.

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

Beispielsweise wird im [standardmäßigen Bereitstellungsszenario] der Schritt `enable-maintenance-mode` das standardmäßige PHP-Skript [EnableMaintenanceMode] ausgeführt.

```xml
<step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="300"/>
```

Um diesen Schritt zu überschreiben, erstellen Sie eine benutzerdefinierte Szenario-Konfigurationsdatei, um bei Ausführung des Schritts `enable-maintenance-mode` ein anderes Skript auszuführen.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="VendorName\VendorModule\Step\CustomEnableMaintenanceMode" priority="300"/>
</scenario>
```

### Schrittpriorität ändern

Benutzerdefinierte Szenarien können die Priorität von Standardschritten ändern. Im folgenden Schritt wird die Priorität des Schritts `enable-maintenance-mode` von `300` in `10` geändert, sodass der Schritt zuvor im Bereitstellungsszenario ausgeführt wird.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="10"/>
</scenario>
```

In diesem Beispiel wird der Schritt `enable-maintenance-mode` an den Anfang des Szenarios verschoben, da er eine niedrigere Priorität hat als alle anderen Schritte im standardmäßigen Bereitstellungsszenario.

### Beispiel: Erweitern des Bereitstellungsszenarios

Im folgenden Beispiel wird das [standardmäßige Bereitstellungsszenario] mit den folgenden Änderungen angepasst:

- Ersetzt den Schritt `remove-deploy-failed-flag` durch einen benutzerdefinierten Schritt
- Überspringt den Unterschritt `clean-redis-cache` im Schritt vor der Bereitstellung
- Überspringt den Schritt `unlock-cron-jobs`
- Überspringt den Schritt `validate-config` , um wichtige Validatoren zu deaktivieren
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

Um dieses Skript in Ihrem Projekt zu verwenden, fügen Sie die folgende Konfiguration zur Datei &quot;`.magento.app.yaml`&quot;für Ihr Adobe Commerce on Cloud-Infrastrukturprojekt hinzu:

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
>Sie können die [Standardszenarien](https://github.com/magento/ece-tools/tree/2002.1/scenario) und die [Standardschrittkonfiguration](https://github.com/magento/ece-tools/tree/2002.1/src/Step) im GitHub-Repository überprüfen, um zu bestimmen, welche Szenarien und Schritte für Ihre Aufgaben zum Erstellen, Bereitstellen und Bereitstellen von Projekten angepasst werden sollen.`ece-tools`

## Fügen Sie ein benutzerdefiniertes Modul hinzu, um `ece-tools` zu erweitern

Das Paket `ece-tools` bietet standardmäßige API-Schnittstellen, die den Standards der Semantic Version entsprechen. Alle API-Schnittstellen sind mit der Anmerkung **@api** markiert. Sie können die standardmäßige API-Implementierung durch Ihre eigene ersetzen, indem Sie ein benutzerdefiniertes Modul erstellen und den Standardcode nach Bedarf ändern.

Um das benutzerdefinierte Modul mit Adobe Commerce in der Cloud-Infrastruktur zu verwenden, müssen Sie Ihr Modul in der Erweiterungsliste für das Paket `ece-tools` registrieren. Der Registrierungsprozess ähnelt dem Prozess, den Sie zur Registrierung von Modulen in Adobe Commerce verwenden.

**So registrieren Sie ein Modul beim `ece-tools` -Paket**:

1. Erstellen oder erweitern Sie die Datei `registration.php` im Stammverzeichnis Ihres Moduls.

   ```php?start_inline=1
   \Magento\MagentoCloud\ExtensionRegistrar::register('module-name', __DIR__);
   ```

1. Aktualisieren Sie den Abschnitt &quot;`autoload`&quot; für Ihre Modulkonfigurationsdatei, um die Datei &quot;`registration.php`&quot; zum automatischen Laden von Moduldateien in &quot;`composer.json`&quot;einzuschließen.

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

1. Fügen Sie die Datei `config/services.xml` in Ihr Modul ein. Diese Konfiguration wird über `config/services.xml` aus dem `ece-tools` -Paket zusammengeführt.

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
