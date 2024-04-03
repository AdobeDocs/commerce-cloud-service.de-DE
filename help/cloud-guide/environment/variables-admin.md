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

Wenn Sie die Werte nach der Installation ändern möchten, verbinden Sie sich mit Ihrer Umgebung mithilfe von SSH und verwenden Sie die Adobe Commerce-CLI [`admin:user` command](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) , um die Admin-Benutzeranmeldeinformationen zu erstellen oder zu bearbeiten.

| Variable | Standard | Beschreibung |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | Email-Adresse des Lizenzinhabers | Ein Benutzername für den administrativen Benutzer, der andere Benutzer erstellen kann, einschließlich Administratorbenutzer. |
| `ADMIN_EMAIL` |                             | E-Mail-Adresse für den Administrator. Diese Adresse wird verwendet, um Benachrichtigungen zum Zurücksetzen von Passwörtern zu senden. |
| `ADMIN_PASSWORD` |                             | Kennwort für den administrativen Benutzer. Wenn das Projekt erstellt wird, wird ein zufälliges Kennwort generiert und eine E-Mail an den Lizenzinhaber gesendet. Bei der Projekterstellung sollte der Lizenzinhaber das Kennwort bereits geändert haben. Wenden Sie sich an den Lizenzinhaber, um das aktualisierte Kennwort zu erhalten. |
| `ADMIN_LOCALE` | `en_US` | Das vom Administrator verwendete Standardgebietsschema. |

## Admin-URL

Verwenden Sie die folgende Umgebungsvariable, um den Zugriff auf Ihre Admin-Benutzeroberfläche zu sichern. Falls angegeben, überschreibt dieser Wert die Standard-URL während der Installation.

`ADMIN_URL`—Die relative URL für den Zugriff auf die Admin-Benutzeroberfläche. Die Standard-URL lautet `/admin`. Aus Sicherheitsgründen empfiehlt Adobe, den Standard in eine eindeutige, benutzerdefinierte Admin-URL zu ändern, die sich nicht leicht erraten lässt.

### Ändern der Admin-URL

Adobe empfiehlt, die Umgebungsvariable für die Admin-URL nach der Installation zu ändern. Konfigurieren Sie diese Einstellung aus Sicherheitsgründen, bevor Sie von der geklonten `master` Umgebung. Alle Verzweigungen, die aus dem `master` -Verzweigung übernehmen die Umgebungsvariablen und ihre Werte.

Verwenden Sie die `magento-cloud variable:update` -Befehl, um den Variablenwert zu aktualisieren. (Die `variable:set` nicht mehr unterstützt und nicht verfügbar ist.) Im folgenden Beispiel wird ADMIN_URL auf `newAdmin_A8v10`:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>Die `ADMIN_URL` -Wert akzeptiert Buchstaben (a-z oder A-Z), Zahlen (0-9) und den Unterstrich (_) für einen benutzerdefinierten Administratorpfad. Leerzeichen oder andere Zeichen sind **not** akzeptiert.

**So ändern Sie die URL mithilfe der[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie in der Projektübersicht die Umgebung aus und klicken Sie auf das Konfigurationssymbol.

   ![Projektkonfiguration](../../assets/icon-configure.png){width="36"}

1. Wählen Sie die **Variablen** Registerkarte.

1. Klicks **Variable erstellen**.

1. Geben Sie Folgendes ein:

   - **Variablenname** = `ADMIN_URL`
   - **value** = Neue URL. Setzen Sie beispielsweise die Admin-URL auf `magento_A8v10`.

   Standardmäßig ist `Available during runtime` und `Make inheritable` ausgewählt sind.

1. Klicks **Variable erstellen** und warten, bis die Bereitstellung abgeschlossen ist. Diese Schaltfläche ist nur sichtbar, wenn die erforderlichen Felder Werte enthalten.
