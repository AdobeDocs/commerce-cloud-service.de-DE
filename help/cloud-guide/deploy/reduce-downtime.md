---
title: Keine Ausfallzeit-Bereitstellung
description: Erfahren Sie, wie Sie bei der Bereitstellung von Adobe Commerce in Cloud-Infrastrukturprojekten Ausfallzeiten reduzieren können.
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Keine Ausfallzeit-Bereitstellung

Adobe Commerce in der Cloud-Infrastruktur führt die Anwendung in [_Wartung_ mode](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) während der Bereitstellungsphase, in der Ihre Site offline geschaltet wird, bis die Bereitstellung abgeschlossen ist. Die Dauer der Wartungsarbeiten Ihrer Produktions-Site hängt von der Größe der Site, der Anzahl der während der Bereitstellung angewendeten Änderungen und der Konfiguration für die Bereitstellung statischer Inhalte ab. Es ist möglich, Ihr Projekt so zu konfigurieren, dass es mit einer **zero** Ausfallzeiteffekt.

Während des Bereitstellungsprozesses werden alle Verbindungen bis zu 5 Minuten lang in die Warteschlange gestellt, wobei aktive Sitzungen und ausstehende Aktionen beibehalten werden, z. B. zum Warenkorb oder zum Checkout. Nach der Bereitstellung wird die Warteschlange freigegeben und die Verbindungen werden ohne Unterbrechung fortgesetzt. So verwenden Sie _Verbindungsaufbau_ zu Ihrem Vorteil und reduzieren Sie die Bereitstellung auf _zero_ Ausfallzeiten festlegen, müssen Sie Ihr Projekt so konfigurieren, dass die effizienteste Bereitstellungsstrategie verwendet wird.

Führen Sie die folgenden Schritte aus, um die Zeit zu verkürzen, die Ihr Store für die Bereitstellung einer Aktualisierung für die Produktion benötigt:

1. [Aktualisieren Sie auf `ece-tools` package](../dev-tools/install-package.md) oder [aktualisieren `ece-tools` version](../dev-tools/update-package.md)
Ihr Adobe Commerce-Projekt zur Cloud-Infrastruktur muss über die neuesten `ece-tools` -Paket, damit Sie über die verfügbaren Tools verfügen, um eine optimale Implementierung zu konfigurieren. Wenn Sie über die neueste `ece-tools`, fahren Sie mit dem nächsten Schritt fort.

   >[!NOTE]
   >
   >Auch wenn es sich um eine Best Practice handelt, die neuesten `ece-tools` -Paket verwenden, funktioniert die Bereitstellungsmethode ohne Ausfallzeiten mit `ece-tools` [Version 2002.0.13](../release-notes/cloud-release-archive.md#v2002013) und höher.

1. [Konfigurieren der Bereitstellung von statischen Inhalten](static-content.md)
Wenn die Bereitstellung statischer Inhalte in der Bereitstellungsphase fehlschlägt, bleibt Ihre Site im Wartungsmodus hängen. Wenn während der Build-Phase ein Fehler auftritt, vermeidet der Prozess Ausfallzeiten, da er die Bereitstellungsphase nie beginnt. [Generieren von statischem Inhalt während der Build-Phase mit minimiertem HTML](static-content.md#setting-the-scd-on-build), auch als idealer Status bezeichnet, ist die optimale Konfiguration für Bereitstellungen ohne Ausfallzeiten und _verhindert_ Ausfallzeiten bei einem Fehler.

1. [Konfigurieren des Hooks nach der Bereitstellung](../application/hooks-property.md)
Sie müssen den Hook nach der Bereitstellung konfigurieren, um den Cache zu leeren und zu warnen. Standardmäßig erfolgt die Cache-Bereinigung während der Bereitstellungsphase, wenn die Site ausfällt. Wenn Sie den Cache in die Phase nach der Bereitstellung verschieben, bleibt der Cache aktiv, bis die Bereitstellungsphase abgeschlossen ist. Anschließend können Sie den Cache sicher löschen.

   Anpassen der Liste der Seiten, die zum Vorausfüllen des Cache mit der [Umgebungsvariable WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages).

1. [Reduzieren von Designdateien](../environment/variables-deploy.md#scdmatrix)
Sie können die Anzahl unnötiger Designdateien reduzieren, indem Sie die Umgebungsvariable SCD\_MATRIX konfigurieren.

1. [Beschleunigung der Bereitstellung statischer Inhalte](../environment/variables-deploy.md#scdthreads)
Sie können den Bereitstellungsprozess beschleunigen, indem Sie die Umgebungsvariable SCD\_THREADS aktualisieren, um die Anzahl der Threads für die Bereitstellung statischer Inhalte zu erhöhen.

>[!NOTE]
>
>Sie können Ihre Projektkonfiguration auf eine optimale Bereitstellung überprüfen, indem Sie [Ausführen des idealen Statusassistenten](smart-wizards.md#verifying-an-ideal-configuration).
