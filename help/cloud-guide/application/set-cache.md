---
title: Festlegen des Cache für statische Dateien
description: Erfahren Sie, wie Sie die Cache-Speicheroptionen in der Konfigurationsdatei der [!DNL Commerce] Anwendung festlegen.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Festlegen des Cache für statische Dateien

Die TTL-Cache (Time-to-Live) für Ihre Medien- und statischen Dateien wird in der Konfigurationsdatei `.magento.app.yaml` mit dem Schlüssel `expires` festgelegt.

>[!NOTE]
>
>Bevor Sie Ihre Produktionsumgebung aktualisieren, müssen Sie Änderungen in Ihrer Staging-Umgebung testen. [Senden Sie ein Adobe Commerce Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um Hilfe beim Aktualisieren der Konfiguration in diesen Umgebungen zu erhalten.

1. Geben Sie die TTL-Zeit (in Sekunden) in der Eigenschaft [`web` ](web-property.md) der Datei `.magento.app.yaml` an. Sie können den Schlüssel `expires` unter `locations` oder unter `"/media"` und `"/static"` hinzufügen.

   Um zu verhindern, dass der Cache abläuft, verwenden Sie das Schlüssel-Wert-Paar `expires: -1` . Siehe folgendes Beispiel:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. Fügen Sie Code-Änderungen hinzu, übertragen Sie sie und übertragen Sie sie.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
