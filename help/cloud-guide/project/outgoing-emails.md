---
title: Ausgehende E-Mails konfigurieren
description: Erfahren Sie, wie Sie ausgehende E-Mails für Adobe Commerce in der Cloud-Infrastruktur aktivieren.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Ausgehende E-Mails konfigurieren

Sie können ausgehende E-Mails für jede Umgebung über die [!DNL Cloud Console] oder über die Befehlszeile. Aktivieren Sie ausgehende E-Mails für Integrations- und Staging-Umgebungen, um Zwei-Faktor-Authentifizierung zu senden oder Passwort-E-Mails für Cloud-Projektbenutzer zurückzusetzen.

Ausgehende E-Mails sind standardmäßig in Produktionsumgebungen aktiviert. Die [!UICONTROL Enable outgoing emails] kann in den Umgebungseinstellungen unabhängig vom Status deaktiviert angezeigt werden, bis Sie die [`enable_smtp` property](#enable-emails-in-the-cli).

{{redeploy-warning}}

## E-Mails in den [!DNL Cloud Console]

Verwenden Sie die **[!UICONTROL Outgoing emails]** Umschalten in der _Umgebung konfigurieren_ anzeigen, um die E-Mail-Unterstützung zu aktivieren oder zu deaktivieren.

**So verwalten Sie den E-Mail-Support über[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.
1. Klicken Sie im Projekt-Dashboard auf das Konfigurationssymbol oben rechts.
1. Klicks **[!UICONTROL Environments]** und wählen Sie eine bestimmte Umgebung aus der Liste aus.
1. Um ausgehende E-Mails zu aktivieren oder zu deaktivieren, schalten Sie _Ausgehende E-Mails aktivieren_ **on** oder **Aus**.

   ![Ausgehende E-Mail-Konfiguration aktivieren](../../assets/outgoing-emails.png)

Nachdem Sie die Einstellung geändert haben, wird die Umgebung mit der neuen Konfiguration erstellt und bereitgestellt.

## Aktivieren von E-Mails in der CLI

Sie können die E-Mail-Konfiguration für eine aktive Umgebung mit dem `magento-cloud` CLI `environment:info` -Befehl zum Festlegen der `enable_smtp` -Eigenschaft. Durch die Aktivierung von SMTP wird die `MAGENTO_CLOUD_SMTP_HOST` Umgebungsvariable mit der IP-Adresse des SMTP-Hosts zum Senden von E-Mails.

**So verwalten Sie den E-Mail-Support über die Befehlszeile**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Überprüfen Sie die Einstellung für ausgehende E-Mails für die Umgebung.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Ändern Sie die Konfiguration der E-Mail-Unterstützung, indem Sie die `enable_smtp` Umgebungsvariable auf `true` oder `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Warten Sie, bis die Umgebung erstellt und bereitgestellt wurde.

1. Verwenden Sie eine SSH, um sich bei der Remote-Umgebung anzumelden.

1. Überprüfen Sie, ob die E-Mail funktioniert. Senden Sie eine Test-E-Mail an eine Adresse, die Sie überprüfen können.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```
