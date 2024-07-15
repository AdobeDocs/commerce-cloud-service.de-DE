---
title: GitHub-Integration
description: Erfahren Sie, wie Sie Ihr Adobe Commerce-Projekt in die Cloud-Infrastruktur mit GitHub integrieren.
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: 5305452f-4c8d-438c-ac78-e2e1ec2f8cd9
source-git-commit: 4d32fc596064f01eaefe3ee509a655837fa846de
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# GitHub-Integration

Mit der GitHub-Integration können Sie Ihre Adobe Commerce in Cloud-Infrastrukturumgebungen direkt über Ihr GitHub-Repository verwalten. Die Integration verwaltet Inhalte, die bereits in GitHub enthalten sind, und synchronisiert sie mit Ihrem Adobe Commerce im Code-Repository der Cloud-Infrastruktur. Im Wesentlichen wird das Code-Repository zum Spiegel des GitHub-Repositorys.

{{private-repository}}

Diese Integration ermöglicht Ihnen Folgendes:

- Erstellen einer Umgebung beim Erstellen einer Verzweigung
- Bereitstellung der Umgebung beim Zusammenführen einer Pull-Anforderung
- Löschen Sie die Umgebung, wenn Sie die Verzweigung löschen

Sie müssen ein GitHub-Token und einen Webhook abrufen, um den Prozess fortzusetzen.

## Voraussetzungen

- Administratorzugriff auf das Adobe Commerce-Projekt in der Cloud-Infrastruktur
- GitHub-Repository
- GitHub-Token für den persönlichen Zugriff

## GitHub-Token generieren

Erstellen Sie ein klassisches persönliches Zugriffstoken in den GitHub-Entwicklereinstellungen. Sie müssen Mitglied einer Gruppe mit Schreibzugriff auf das GitHub-Repository sein, damit Sie _Push_ an das Repository senden können. Schließen Sie beim Erstellen Ihres Tokens die folgenden Bereiche ein:

- `admin:repo_hook` - Erstellen von Web-Hooks
- `repo`—Integration in Ihr Repository
- `read:org`—Integrieren Sie in Ihr Organisations-Repository.

Siehe [GitHub: Erstellen](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Repository vorbereiten

Klonen Sie Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur von einer bestehenden Umgebung und migrieren Sie die Projektverzweigungen in ein neues, leeres GitHub-Repository, wobei Sie dieselben Zweignamen beibehalten. Es ist **wichtig**, eine identische Git-Struktur beizubehalten, damit Sie keine bestehenden Umgebungen oder Verzweigungen in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt verlieren.

1. Melden Sie sich über das Terminal bei Ihrem Adobe Commerce-Projekt für eine Cloud-Infrastruktur an.

   ```bash
   magento-cloud login
   ```

1. Geben Sie Ihre Projekte an und kopieren Sie die Projekt-ID.

   ```bash
   magento-cloud project:list
   ```

1. Klonen Sie das Projekt in Ihrer lokalen Umgebung.

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. Fügen Sie Ihr GitHub-Repository als Remote-Repository hinzu.

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   Der Standardname für die Remote-Verbindung kann `origin` oder `magento` sein. Wenn `origin` vorhanden ist, können Sie einen anderen Namen wählen oder die vorhandene Referenz umbenennen oder löschen. Siehe [git-remote-Dokumentation](https://git-scm.com/docs/git-remote).

1. Stellen Sie sicher, dass Sie die GitHub-Fernbedienung korrekt hinzugefügt haben.

   ```bash
   git remote -v
   ```

   Erwartete Antwort:

   ```terminal
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. Schicken Sie die Projektdateien an Ihr neues GitHub-Repository. Denken Sie daran, alle Zweignamen gleich zu halten.

   ```bash
   git push -u origin master
   ```

   Wenn Sie mit einem neuen GitHub-Repository beginnen, müssen Sie möglicherweise die Option `-f` verwenden, da das Remote-Repository nicht mit Ihrer lokalen Kopie übereinstimmt.

1. Stellen Sie sicher, dass Ihr GitHub-Repository alle Ihre Projektdateien enthält.

## GitHub-Integration aktivieren

Bevor Sie beginnen, müssen sich Ihr Projektcode und Ihre Umgebungen im GitHub-Repository befinden. Nach Aktivierung der Integration wird das GitHub-Repository zur Codequelle. Wenn Sie Code-Änderungen an das ursprüngliche `magento`-Repository pushen, wird dieser von der Integration überschrieben, wenn Sie Code-Änderungen an Ihr GitHub-Repository pushen.

Im Folgenden wird die GitHub-Integration aktiviert und eine Payload-URL bereitgestellt, die beim Erstellen eines Webhooks verwendet werden kann.

>[!WARNING]
>
>Der folgende Befehl überschreibt den Code _all_ in Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur mit Code aus Ihrem GitHub-Repository, der alle Verzweigungen einschließlich der Verzweigung `production` enthält. Diese Aktion erfolgt sofort und kann nicht rückgängig gemacht werden. Als Best Practice ist es wichtig, alle Verzweigungen aus Ihrem Adobe Commerce im Cloud-Infrastrukturprojekt zu klonen und sie in Ihr GitHub-Repository zu übertragen, **bevor** die GitHub-Integration hinzufügt.

Sie können die CLI-Aufforderungen mit `magento-cloud integration:add` schrittweise ausführen oder den Integrationsbefehl mit den folgenden Optionen erstellen:

| Option | Erforderlich? | Beschreibung |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | Ja | Die Basis-URL der Serverinstallation, die `https://github.com/` oder ein benutzerdefinierter Wert sein kann. Lassen Sie diese Option weg, wenn Ihr Repository mit öffentlichem GitHub gehostet wird. |
| `--token` | Ja | Das persönliche Zugriffstoken, das Sie für GitHub generiert haben |
| `--repository` | Ja | Der Repository-Name: `owner-or-organisation/repository` |
| `--build-pull-requests` | Optional | Weist Adobe Commerce in der Cloud-Infrastruktur nach dem Zusammenführen einer Pull-Anforderung (`true` standardmäßig) die Bereitstellung an |
| `--fetch-branches` | Optional | Verursacht, dass Adobe Commerce in der Cloud-Infrastruktur Verzweigungen verfolgt und bereitstellt, nachdem Sie eine Verzweigung aktualisiert haben (`true` standardmäßig) |
| `--prune-branches` | Optional | Löschen Sie Zweige, die nicht auf der Remote-Site vorhanden sind (`true` standardmäßig) |

Es gibt viele weitere Optionen, die Sie mithilfe der Hilfeoption sehen können:

```bash
magento-cloud integration:add --help
```

**Aktivieren der GitHub-Integration**:

1. Aktivieren Sie die Integration.

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **Beispiel 1**: Aktivieren Sie die GitHub-Integration für ein persönliches, privates Repository:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **Beispiel 2**: Aktivieren Sie die GitHub-Integration für ein Organisations-Repository:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. Geben Sie bei Aufforderung die erforderlichen Informationen ein.

1. Kopieren Sie die **Payload-URL**, die von der Ausgabe der Ausgabe angezeigt wird.

   ```terminal
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## Webhook in GitHub hinzufügen

Um Ereignisse wie Push-Benachrichtigungen mit Ihrem Cloud Git-Server zu kommunizieren, müssen Sie einen Webhook für Ihr GitHub-Repository erstellen:

1. Klicken Sie in Ihrem GitHub-Repository auf die Registerkarte **Einstellungen** .

1. Klicken Sie in der linken Navigationsleiste auf **Webhooks**.

1. Klicken Sie im Bereich _Webhooks_ auf **Webhook hinzufügen**.

1. Bearbeiten Sie im Formular _Webhooks/Add webhook_ die folgenden Felder:

   - **Payload-URL**: Geben Sie die URL ein, die zurückgegeben wird, wenn Sie die GitHub-Integration aktiviert haben.
   - **Content type**: Wählen Sie **application/json** aus der Liste aus.
   - **Geheimnis**: Geben Sie ein Verifizierungsgeheimnis ein.
   - **Welche Ereignisse möchten Sie auf diesen Webhook Trigger haben?**: Wählen Sie **Alles senden** aus.
   - Aktivieren Sie das Kontrollkästchen **Aktiv** .

1. Klicken Sie auf **Webhook hinzufügen**.

## Integration testen

Nach der Konfiguration der GitHub-Integration können Sie mithilfe der `magento-cloud`-CLI überprüfen, ob die Integration funktioniert:

```bash
magento-cloud integration:validate
```

Alternativ können Sie sie testen, indem Sie eine einfache Änderung an Ihr GitHub-Repository senden.

1. Erstellen Sie eine Testdatei.

   ```bash
   touch test.md
   ```

1. Übertragen Sie die Änderung und übertragen Sie sie in Ihr GitHub-Repository.

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. Melden Sie sich bei [[!DNL Cloud Console]](../project/overview.md) an und überprüfen Sie, ob Ihre Commit-Nachricht angezeigt wird und Ihr Projekt bereitgestellt wird.

## Integration entfernen

Sie können die GitHub-Integration sicher aus Ihrem Projekt entfernen, ohne den Code zu beeinträchtigen.

**Entfernen der GitHub-Integration**:

1. Melden Sie sich über das Terminal bei Ihrem Adobe Commerce-Projekt für eine Cloud-Infrastruktur an.

1. Geben Sie Ihre Integrationen an. Sie benötigen die GitHub-Integrations-ID, um den nächsten Schritt abzuschließen.

   ```bash
   magento-cloud integration:list
   ```

1. Löschen Sie die Integration.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Außerdem können Sie die GitHub-Integration entfernen, indem Sie sich bei Ihrem GitHub-Konto anmelden und den Web-Hook auf der Registerkarte _Webhooks_ des Repositorys entfernen _Einstellungen_.
