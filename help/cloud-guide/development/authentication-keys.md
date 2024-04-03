---
title: Authentifizierungsschlüssel
description: Erfahren Sie, wie Sie Authentifizierungsschlüssel auf ein Entwicklungsprojekt in Adobe Commerce in der Cloud-Infrastruktur anwenden.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Authentifizierungsschlüssel

Sie müssen über einen Authentifizierungsschlüssel verfügen, um auf das Adobe Commerce-Repository zugreifen und Installations- und Aktualisierungsbefehle für Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur aktivieren zu können. Es gibt zwei Methoden zum Angeben der Autorisierungsberechtigungen für Composer.

- **Authentifizierungsdatei**—Eine Datei, die Ihren Adobe Commerce enthält [Autorisierungsberechtigungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in Ihrer Adobe Commerce auf dem Stammordner der Cloud-Infrastruktur.
- **Umgebungsvariable**—Eine Umgebungsvariable zum Einrichten von Authentifizierungsschlüsseln in Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur, um eine versehentliche Exposition zu verhindern.

>[!BEGINSHADEBOX]

**Sicherheitshinweis**

Adobe empfiehlt die Verwendung der [Umgebungsvariable](#composer-auth-environment-variable) -Methode mit Ihrem Cloud-Projekt verwenden, um eine versehentliche Offenlegung Ihrer Autorisierungsberechtigungen zu verhindern.

Die Authentifizierungsdateimethode ist ideal, wenn Sie Cloud Docker für Commerce als lokales Entwicklungstool verwenden. Achten Sie jedoch darauf, die `auth.json` in ein öffentliches Git-basiertes Repository. Sie können die `auth.json` in die Datei [`.gitignore` file](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Authentifizierungsdatei

**So erstellen Sie eine `auth.json` file**:

1. Wenn Sie keine `auth.json` -Datei in Ihrem Stammverzeichnis des Projekts erstellen.

   - Erstellen Sie mithilfe eines Texteditors eine `auth.json` -Datei in Ihrem Stammverzeichnis des Projekts.
   - Kopieren Sie den Inhalt der [sample `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) in die neue `auth.json` -Datei.

1. Ersetzen `<public-key>` und `<private-key>` mit Ihren Adobe Commerce-Authentifizierungsdaten.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Speichern Sie Ihre Änderungen und beenden Sie den Texteditor.

## Umgebungsvariable Composer auth

Die folgende Methode stellt die beste Möglichkeit dar, die versehentliche Offenlegung vertraulicher Anmeldeinformationen in einem öffentlichen Git-basierten Repository zu verhindern.

**Hinzufügen von Authentifizierungsschlüsseln mit einer Umgebungsvariablen**:

1. Im _[!DNL Cloud Console]_klicken Sie auf das Konfigurationssymbol auf der rechten Seite der Projektnavigation.

   ![Projekt konfigurieren](../../assets/icon-configure.png){width="36"}

1. Im _Projekteinstellungen_ Liste, klicken Sie **[!UICONTROL Variables]**.

1. Klicks **[!UICONTROL Create variable]**.

1. Im **[!UICONTROL Variable name]** Feld, eingeben `env:COMPOSER_AUTH`.

1. Im _Wert_ -Feld hinzufügen, Folgendes hinzufügen und ersetzen `<public-key>` und `<private-key>` mit Ihren Adobe Commerce-Authentifizierungsberechtigungen:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Auswählen **[!UICONTROL Available during buildtime]** und Auswahl aufheben **[!UICONTROL Available during runtime]**.

1. Klicks **[!UICONTROL Create variable]**.

1. Entfernen Sie die `auth.json` -Datei aus jeder Umgebung.
