---
title: Ausgehende E-Mails konfigurieren
description: Erfahren Sie, wie Sie ausgehende E-Mails für Adobe Commerce in der Cloud-Infrastruktur aktivieren.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 75318be63adcbe23bb8b6699b1c59b2b4a3c1a4d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Ausgehende E-Mails konfigurieren

Sie können ausgehende E-Mails für Integrations- (und Staging-Umgebungen nur für Starter) in der Befehlszeile [!DNL Cloud Console] oder der Befehlszeile aktivieren und deaktivieren. Aktivieren Sie ausgehende E-Mails, um zweifakultative Authentifizierung zu senden oder E-Mails mit Passwörtern für Cloud-Projektbenutzer zurückzusetzen.

Ausgehende E-Mails sind standardmäßig in Produktions- und Staging-Umgebungen (nur Pro) aktiviert. Die Einstellung **[!UICONTROL Enable outgoing emails]** kann jedoch in den Umgebungseinstellungen deaktiviert angezeigt werden, unabhängig vom Status, bis Sie die Eigenschaft `enable_smtp` über die Befehlszeile ](#enable-emails-in-the-cli) oder die [Cloud-Konsole](outgoing-emails.md#enable-emails-in-the-cloud-console) festlegen.[

Durch die Aktualisierung des Eigenschaftswerts `enable_smtp` um die Befehlszeile ](#enable-emails-in-the-cli) wird auch der Wert für die Einstellung [!UICONTROL Enable outgoing emails] für diese Umgebung in der Cloud Console geändert.[

>[!NOTE]
>
>Durch Aktivierung/Deaktivierung der Einstellung &quot;**[!UICONTROL Enable outgoing emails]**&quot; werden E-Mails in der Staging- oder Produktionsumgebung von Pro nicht aktiviert/deaktiviert.

{{redeploy-warning}}

## E-Mails in der Cloud Console aktivieren

Verwenden Sie den Umschalter **[!UICONTROL Outgoing emails]** in der Ansicht _Umgebung konfigurieren_ , um die E-Mail-Unterstützung zu aktivieren oder zu deaktivieren.

Wenn ausgehende E-Mails in Pro Production- oder Staging-Umgebungen deaktiviert oder wieder aktiviert werden müssen, können Sie ein [Adobe Commerce-Supportticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) senden.

>[!TIP]
>
>Der ausgehende E-Mail-Status wird möglicherweise nicht für Pro-Staging- oder Produktionsumgebungen in der Cloud Console angezeigt.

**So verwalten Sie den E-Mail-Support über die[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.
1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.
1. Klicken Sie im Projekt-Dashboard auf das Konfigurationssymbol oben rechts.
1. Klicken Sie auf **[!UICONTROL Environments]** und wählen Sie eine bestimmte Umgebung aus der Liste aus (außer Staging und Produktion für Pro).
1. Um ausgehende E-Mails zu aktivieren oder zu deaktivieren, schalten Sie _Ausgehende E-Mails aktivieren_ **Ein** oder **Aus** um.

   ![Ausgehende E-Mail-Konfiguration aktivieren](../../assets/outgoing-emails.png)

Nachdem Sie die Einstellung geändert haben, wird die Umgebung mit der neuen Konfiguration erstellt und bereitgestellt.

## Aktivieren von E-Mails in der CLI

Sie können die E-Mail-Konfiguration für eine aktive Umgebung mithilfe des Befehls `magento-cloud` CLI `environment:info` ändern, um die Eigenschaft `enable_smtp` festzulegen. Durch die Aktivierung von SMTP wird die Umgebungsvariable `MAGENTO_CLOUD_SMTP_HOST` mit der IP-Adresse des SMTP-Hosts zum Senden von E-Mails aktualisiert.

**So verwalten Sie den E-Mail-Support über die Befehlszeile**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Überprüfen Sie die Einstellung für ausgehende E-Mails für die Umgebung.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Ändern Sie die Konfiguration der E-Mail-Unterstützung, indem Sie die Umgebungsvariable `enable_smtp` auf `true` oder `false` setzen.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Warten Sie, bis die Umgebung erstellt und bereitgestellt wurde.

1. Verwenden Sie eine SSH, um sich bei der Remote-Umgebung anzumelden.

1. Überprüfen Sie, ob die E-Mail funktioniert. Senden Sie eine Test-E-Mail an eine Adresse, die Sie überprüfen können.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. Stellen Sie sicher, dass die E-Mail von SendGrid erfasst wird.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
