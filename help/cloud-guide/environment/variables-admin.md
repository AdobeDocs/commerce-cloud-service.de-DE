---
title: ADMIN-Variablen
description: Sehen Sie sich eine Liste der Umgebungsvariablen an, die für die Installation von Adobe Commerce in der Cloud-Infrastruktur verwendet werden.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Admin-Variablen

Benutzer, die über Administratorzugriff auf das Adobe Commerce-Projekt in der Cloud-Infrastruktur verfügen, können die folgenden Projektumgebungsvariablen verwenden, um die Konfigurationseinstellungen für das Administrator-Benutzerkonto für den Zugriff auf die Admin-Benutzeroberfläche zu überschreiben.

## Administratorberechtigungen

Sie können Admin-Benutzeranmeldeinformationen während der Commerce-Installation mit den ADMIN-Variablen in der folgenden Tabelle überschreiben.

Wenn Sie die Werte nach der Installation ändern möchten, verbinden Sie sich mit Ihrer Umgebung mithilfe von SSH und verwenden Sie den Adobe Commerce-CLI-Befehl [`admin:user` Befehl](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) , um die Anmeldeinformationen des Admin-Benutzers zu erstellen oder zu bearbeiten.

| Variable | Standard | Beschreibung |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | Email-Adresse des Lizenzinhabers | Ein Benutzername für den administrativen Benutzer, der andere Benutzer erstellen kann, einschließlich Administratorbenutzer. |
| `ADMIN_EMAIL` |                             | E-Mail-Adresse für den Administrator. Diese Adresse wird verwendet, um Benachrichtigungen zum Zurücksetzen von Passwörtern zu senden. |
| `ADMIN_PASSWORD` |                             | Kennwort für den administrativen Benutzer. Wenn das Projekt erstellt wird, wird ein zufälliges Kennwort generiert und eine E-Mail an den Lizenzinhaber gesendet. Bei der Projekterstellung sollte der Lizenzinhaber das Kennwort bereits geändert haben. Wenden Sie sich an den Lizenzinhaber, um das aktualisierte Kennwort zu erhalten. |
| `ADMIN_LOCALE` | `en_US` | Das vom Administrator verwendete Standardgebietsschema. |

## Admin-URL

Verwenden Sie die folgende Umgebungsvariable, um den Zugriff auf Ihre Admin-Benutzeroberfläche zu sichern. Falls angegeben, überschreibt dieser Wert die Standard-URL während der Installation.

`ADMIN_URL` - Die relative URL für den Zugriff auf die Admin-Benutzeroberfläche. Die Standard-URL lautet `/admin`. Aus Sicherheitsgründen empfiehlt Adobe, den Standard in eine eindeutige, benutzerdefinierte Admin-URL zu ändern, die sich nicht leicht erraten lässt.

### Ändern der Admin-URL

Adobe empfiehlt, die Umgebungsvariable für die Admin-URL nach der Installation zu ändern. Konfigurieren Sie diese Einstellung aus Sicherheitsgründen, bevor Sie von der geklonten `master` -Umgebung verzweigen. Alle aus der Verzweigung `master` erstellten Verzweigungen übernehmen die Variablen auf Umgebungsebene und deren Werte.

Verwenden Sie den Befehl `magento-cloud variable:update` , um den Variablenwert zu aktualisieren. (Der Befehl `variable:set` ist veraltet und nicht verfügbar.) Im folgenden Beispiel wird ADMIN_URL auf `newAdmin_A8v10` aktualisiert:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>Der Wert `ADMIN_URL` akzeptiert Buchstaben (a-z oder A-Z), Zahlen (0-9) und Unterstriche (_) für einen benutzerdefinierten Administratorpfad. Leerzeichen oder andere Zeichen werden **nicht** akzeptiert.

**So ändern Sie die URL mit dem[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie in der Projektübersicht die Umgebung aus und klicken Sie auf das Konfigurationssymbol.

   ![Projektkonfiguration](../../assets/icon-configure.png){width="36"}

1. Wählen Sie die Registerkarte **Variablen** aus.

1. Klicken Sie auf **Variable erstellen**.

1. Geben Sie Folgendes ein:

   - **Variablenname** = `ADMIN_URL`
   - **value** = Neue URL. Setzen Sie beispielsweise die Admin-URL auf &quot;`magento_A8v10`&quot;.

   Standardmäßig sind `Available during runtime` und `Make inheritable` ausgewählt.

1. Klicken Sie auf **Variable erstellen** und warten Sie, bis die Bereitstellung abgeschlossen ist. Diese Schaltfläche ist nur sichtbar, wenn die erforderlichen Felder Werte enthalten.
