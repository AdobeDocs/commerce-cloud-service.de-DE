---
title: Anforderungen an ein CMS-Backend umleiten
description: Erfahren Sie, wie Sie eingehende Anfragen von einem Adobe Commerce-Store mithilfe des Fastly Edge-Moduls an eine separate WordPress-Site weiterleiten.
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Anforderungen an ein CMS-Backend umleiten

Eingehende Anforderungen von einem Adobe Commerce-Store werden mithilfe des Fastly Edge Module _Sonstige CMS/Backend-Integration_ mit einem Edge-Wörterbuch an eine separate WordPress-Site weitergeleitet. Sie können einen ähnlichen Prozess ausführen, um Anforderungen an andere CMS-Backends erneut auszuführen.

Verwenden Sie Fastly Edge-Module, um benutzerdefinierten VCL-Code aus dem Admin zu erstellen und hochzuladen, anstatt den VCL-Code manuell zu schreiben und ihn mit der Fastly-API hochzuladen.

>[!NOTE]
>
>Es wird empfohlen, benutzerdefinierte VCL-Konfigurationen zu einer Staging-Umgebung hinzuzufügen, in der Sie diese testen können, bevor Sie die Fastly-Dienstkonfiguration in der Produktionsumgebung aktualisieren.

**Voraussetzungen**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**So senden Sie Anfragen von Adobe Commerce an WordPress**:

1. Aktivieren Sie Fastly Edge Module in der Staging- oder Produktionsumgebung.

   - Melden Sie sich beim Administrator an.

   - Navigieren Sie zu **Stores** > Einstellungen > **Konfiguration** > **Erweitert** > **System** > **Gesamter Seiten-Cache** > **Fastly Configuration** > **Erweiterte Konfiguration**.

   - Setzen Sie den Wert für **Fastly Edge Modules** auf **Ja**.

   - Speichern Sie die Konfiguration.

1. Identifizieren Sie die URL-Pfade, die zum WordPress-Backend umgeleitet werden sollen.

1. Führen Sie die folgenden Aufgaben aus, um den Fastly-Dienst zu konfigurieren und den benutzerdefinierten VCL-Code für die Umleitung von Anforderungen an das WordPress-Backend zu erstellen.

   - Erstellen Sie ein Edge-Wörterbuch, das die Pfade angibt, die vom Adobe Commerce-Store zum Backend umgeleitet werden sollen.

   - Fügen Sie das WordPress-Backend zur Konfiguration des Fastly-Dienstes hinzu und fügen Sie die Anforderungsbedingung für die URL-Neuschreibungen hinzu.

   - Konfigurieren Sie das Edge-Modul _Sonstige CMS/Backend-Integration_ , um die URL-Neuschreibungen von Adobe Commerce zum WordPress-Backend zu verarbeiten.

     Detaillierte Anweisungen finden Sie unter [Fastly Edge Module - Other CMS/Backend integration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in der Dokumentation zum _Fastly CDN-Modul für Magento 2_.

1. Testen Sie nach dem Aktualisieren der Fastly-Dienstkonfiguration Ihren Adobe Commerce Store, um sicherzustellen, dass die angegebenen URL-Anforderungen für WordPress korrekt umgeleitet werden.
