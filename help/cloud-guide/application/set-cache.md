---
title: Festlegen des Cache für statische Dateien
description: Erfahren Sie, wie Sie die Cache-Speicheroptionen in der [!DNL Commerce] Anwendungskonfigurationsdatei.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Festlegen des Cache für statische Dateien

Die TTL-Cache (Time-to-Live) für Ihre Medien und statischen Dateien wird im `.magento.app.yaml` Konfigurationsdatei mit der `expires` Schlüssel.

>[!NOTE]
>
>Bevor Sie Ihre Produktionsumgebung aktualisieren, müssen Sie Änderungen in Ihrer Staging-Umgebung testen. [Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) Hilfe bei der Aktualisierung der Konfiguration in diesen Umgebungen.

1. Geben Sie die TTL-Zeit (in Sekunden) im [`web` property](web-property.md) des `.magento.app.yaml` -Datei. Sie können die `expires` Schlüssel unter `locations` oder `"/media"` und `"/static"`.

   Um zu verhindern, dass der Cache abläuft, verwenden Sie den `expires: -1` Schlüssel-Wert-Paar. Siehe folgendes Beispiel:

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
