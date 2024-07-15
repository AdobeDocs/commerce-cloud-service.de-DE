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

- **Authentifizierungsdatei** - Eine Datei, die Ihre Adobe Commerce [Autorisierungsberechtigungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in Ihrer Adobe Commerce im Stammordner der Cloud-Infrastruktur enthält.
- **Umgebungsvariable**: Eine Umgebungsvariable zum Einrichten von Authentifizierungsschlüsseln in Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur, um eine versehentliche Exposition zu verhindern.

>[!BEGINSHADEBOX]

**Sicherheitshinweis**

Adobe empfiehlt die Verwendung der [Umgebungsvariable](#composer-auth-environment-variable) -Methode in Ihrem Cloud-Projekt, um eine versehentliche Offenlegung Ihrer Autorisierungsberechtigungen zu verhindern.

Die Authentifizierungsdateimethode ist ideal, wenn Sie Cloud Docker für Commerce als lokales Entwicklungstool verwenden. Achten Sie jedoch darauf, die `auth.json` -Datei nicht in ein öffentliches Git-basiertes Repository hochzuladen. Sie können die Datei `auth.json` zur Datei [`.gitignore` ](../project/file-structure.md#ignoring-files) hinzufügen.

>[!ENDSHADEBOX]

## Authentifizierungsdatei

**So erstellen Sie eine `auth.json` -Datei**:

1. Wenn Sie keine `auth.json` -Datei im Stammverzeichnis Ihres Projekts haben, erstellen Sie eine.

   - Erstellen Sie mit einem Texteditor eine `auth.json` -Datei in Ihrem Projektstammverzeichnis.
   - Kopieren Sie den Inhalt von [sample `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) in die neue `auth.json`-Datei.

1. Ersetzen Sie `<public-key>` und `<private-key>` durch Ihre Adobe Commerce-Authentifizierungsberechtigungen.

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

1. Klicken Sie im Ordner &quot;_[!DNL Cloud Console]_&quot;auf das Konfigurationssymbol auf der rechten Seite der Projektnavigation.

   ![Projekt konfigurieren](../../assets/icon-configure.png){width="36"}

1. Klicken Sie in der Liste _Projekteinstellungen_ auf **[!UICONTROL Variables]**.

1. Klicken Sie auf **[!UICONTROL Create variable]**.

1. Geben Sie im Feld **[!UICONTROL Variable name]** den Wert `env:COMPOSER_AUTH` ein.

1. Fügen Sie im Feld _Wert_ Folgendes hinzu und ersetzen Sie `<public-key>` und `<private-key>` durch Ihre Adobe Commerce-Authentifizierungsberechtigungen:

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

1. Wählen Sie **[!UICONTROL Available during buildtime]** aus und heben Sie die Auswahl von **[!UICONTROL Available during runtime]** auf.

1. Klicken Sie auf **[!UICONTROL Create variable]**.

1. Entfernen Sie die Datei &quot;`auth.json`&quot; aus jeder Umgebung.
