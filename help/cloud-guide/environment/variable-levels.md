---
title: Variablenebenen und Optionen
description: Erfahren Sie mehr über die verschiedenen Variablenebenen und -optionen, die beim Anpassen Ihrer Adobe Commerce in der Laufzeitumgebung für Cloud-Infrastruktur-Projekte verwendet werden.
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Variablenebenen

Projektvariablen gelten für alle Umgebungen innerhalb des Projekts. Umgebungsvariablen gelten für eine bestimmte Umgebung oder Verzweigung. Eine Umgebung _übernimmt_ Variablendefinitionen aus der übergeordneten Umgebung.

Sie können einen übernommenen Wert überschreiben, indem Sie die Variable speziell für die Umgebung definieren. Um beispielsweise Variablen für die Entwicklung festzulegen, definieren Sie die Variablenwerte in der Datei `.magento.env.yaml` in der Integrationsumgebung. Diese Werte werden von allen in der Integrationsumgebung verzweigten Umgebungen übernommen. Weitere Informationen zum Konfigurieren Ihrer Umgebung mit der Datei `.magento.env.yaml` finden Sie unter [Bereitstellungskonfiguration](configure-env-yaml.md) .

>[!BEGINTABS]

>[!TAB CLI]

**So legen Sie Variablen mithilfe der Cloud CLI fest**:

- **Projektspezifische Variablen** - Um denselben Wert für _alle_ Umgebungen in Ihrem Projekt festzulegen. Diese Variablen sind beim Erstellen und zur Laufzeit in allen Umgebungen verfügbar.

  ```bash
  magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
  ```

- **Umgebungsspezifische Variablen** - Um einen eindeutigen Wert für eine _spezifische_ -Umgebung festzulegen. Diese Variablen sind zur Laufzeit verfügbar und werden von untergeordneten Umgebungen übernommen. Geben Sie die Umgebung in Ihrem Befehl mit der Option `-e` an.

  ```bash
  magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
  ```

Nachdem Sie projektspezifische Variablen festgelegt haben, müssen Sie die Remote-Umgebung manuell neu bereitstellen, damit die Änderung wirksam wird. Übergeben Sie die neuen Zusagen, um eine Neuimplementierung Trigger.

>[!TAB Konsole]

**So legen Sie Variablen mithilfe des[!DNL Cloud Console]** fest:

1. Klicken Sie im Ordner &quot;_[!DNL Cloud Console]_&quot;auf das Konfigurationssymbol auf der rechten Seite der Projektnavigation.

   ![Projekt konfigurieren](../../assets/icon-configure.png){width="36"}

1. Um eine Variable auf Projektebene festzulegen, klicken Sie unter _Projekteinstellungen_ auf **Variablen**.

   ![Projektvariablen](../../assets/ui-project-variables.png)

1. Um eine Umgebungsvariable festzulegen, wählen Sie in der Liste _Umgebungen_ eine Umgebung aus und klicken Sie auf die Registerkarte **[!UICONTROL Variables]** .

   ![Registerkarte &quot;Umgebungsvariablen&quot;](../../assets/ui-environment-variables.png)

1. Klicken Sie auf **[!UICONTROL Create variable]**.

1. Geben Sie einen Namen und einen Wert für die Variable an. Wählen Sie aus den Optionen aus:

   - Zur Laufzeit verfügbar
   - Verfügbar während der Buildzeit
   - JSON-Wert
   - Sensitive Variable (Wert in der Konsole ausgeblendet und CLI-Antworten)
   - Vererbbar (untergeordnete Umgebungen können Variablen auf Umgebungsebene übernehmen)

1. Klicken Sie auf **[!UICONTROL Create variable]**.

>[!CAUTION]
>
>Durch das Festlegen umgebungsspezifischer Variablen in [!DNL Cloud Console] wird die Umgebung automatisch erneut bereitgestellt.

>[!ENDTABS]

## Sichtbarkeit

Mit dem Befehl `--visible-<build|runtime>` können Sie die Sichtbarkeit einer Variablen während der Build- oder Laufzeitumgebung einschränken. Außerdem gibt es Optionen zum Festlegen von Vererbung und Empfindlichkeit.

Verwenden Sie die folgenden Optionen, um zu verhindern, dass eine Variable angezeigt oder vererbt wird:

- `--inheritable false` - Deaktiviert die Vererbung für untergeordnete Umgebungen. Dies ist nützlich, um reine Produktionswerte für die Verzweigung `master` festzulegen und allen anderen Umgebungen die Verwendung einer Variablen auf Projektebene mit demselben Namen zu ermöglichen.
- `--sensitive true` - markiert die Variable als _nicht lesbar_ im [!DNL Cloud Console]. Sie können die Variable nicht in der Benutzeroberfläche anzeigen. Sie können die Variable jedoch wie jede andere Variable auch im Anwendungscontainer anzeigen.

Im Folgenden wird ein spezieller Fall veranschaulicht, um zu verhindern, dass eine Variable gesehen oder vererbt wird. Sie können diese Optionen nur in der CLI angeben. Dieser Fall bezieht sich nicht auf alle verfügbaren Umgebungsvariablen.

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## Überprüfen von Variablenebenen und -werten

Mithilfe der Cloud-CLI können Sie eine Liste der vorhandenen Variablen anzeigen.

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
