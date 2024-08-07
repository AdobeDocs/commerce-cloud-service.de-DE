---
title: GitLab-Integration
description: Erfahren Sie, wie Sie Ihr Adobe Commerce in ein Cloud-Infrastrukturprojekt mit GitLab integrieren.
feature: Cloud, Integration
exl-id: 37fda8a0-7274-422f-9049-243f2e409f26
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# GitLab-Integration

Sie können ein GitLab-Repository konfigurieren, um beim Push von Code-Änderungen automatisch eine Umgebung zu erstellen und bereitzustellen. Diese Integration synchronisiert Ihr GitLab-Repository mit Ihrem Adobe Commerce-Konto für die Cloud-Infrastruktur.

{{private-repository}}

Diese Integration ermöglicht Ihnen Folgendes:

- Erstellen einer Umgebung beim Erstellen einer Verzweigung
- Bereitstellung der Umgebung beim Zusammenführen einer Pull-Anforderung
- Löschen Sie die Umgebung, wenn Sie die Verzweigung löschen

Sie müssen ein GitLab-Token und einen Webhook abrufen, um den Prozess fortzusetzen.

## Voraussetzungen

- Administratorzugriff auf das Adobe Commerce-Projekt in der Cloud-Infrastruktur
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md)-Tool in Ihrer lokalen Umgebung
- Ein GitLab-Konto
- Ein persönliches GitLab-Zugriffstoken mit Schreibzugriff auf das GitLab-Repository. Die ausgewählten Bereiche müssen mindestens `api` und `read_repository` betragen.

## Repository vorbereiten

Klonen Sie Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur von einer bestehenden Umgebung und migrieren Sie die Projektverzweigungen in ein neues, leeres GitLab-Repository, wobei Sie dieselben Zweignamen beibehalten. Es ist **wichtig**, eine identische Git-Struktur beizubehalten, damit Sie keine bestehenden Umgebungen oder Verzweigungen in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt verlieren.

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
   magento-cloud project:get <project-id>
   ```

1. Fügen Sie Ihr GitLab-Repository als Remote-Repository hinzu (vorausgesetzt, GitLab wird in der SaaS-Version verwendet).

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   Der Standardname für die Remote-Verbindung kann `origin` oder `magento` sein. Wenn `origin` vorhanden ist, können Sie einen anderen Namen wählen oder die vorhandene Referenz umbenennen oder löschen. Siehe [git-remote-Dokumentation](https://git-scm.com/docs/git-remote).

1. Stellen Sie sicher, dass Sie die GitLab-Fernbedienung korrekt hinzugefügt haben.

   ```bash
   git remote -v
   ```

   Erwartete Antwort:

   ```
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. Schicken Sie die Projektdateien in Ihr neues GitLab-Repository. Denken Sie daran, alle Zweignamen gleich zu halten.

   ```bash
   git push -u origin master
   ```

   Wenn Sie mit einem neuen GitLab-Repository beginnen, müssen Sie möglicherweise die Option `-f` verwenden, da das Remote-Repository nicht mit Ihrer lokalen Kopie übereinstimmt.

1. Stellen Sie sicher, dass Ihr GitLab-Repository alle Ihre Projektdateien enthält.

## GitLab-Integration aktivieren

Verwenden Sie den Befehl `magento-cloud integration` , um die GitLab-Integration zu aktivieren, und rufen Sie die Payload-URL für den GitLab-Webhook ab, um Aktualisierungen von GitLab an Ihr Adobe Commerce-Projekt zur Cloud-Infrastruktur zu senden.

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| Option | Beschreibung |
| ------ | ----------- |
| `<project-ID>` | Ihre Adobe Commerce-Projekt-ID für die Cloud-Infrastruktur |
| `<your-GitLab-token>` | Das persönliche Zugriffstoken, das Sie für GitLab generiert haben |
| `--base-url` | URL von GitLab (`https://gitlab.com/`, wenn GitLab in seiner SaaS-Version verwendet wird) |
| `--server-project` | Projektname in GitLab (Teil nach der Basis-URL) |
| `--build-merge-requests` | Ein Parameter _optional_ , der Adobe Commerce in der Cloud-Infrastruktur anweist, für jede Zusammenführungsanforderung eine neue Umgebung zu erstellen (`true` standardmäßig) |
| `--merge-requests-clone-parent-data` | Ein Parameter _optional_ , der Adobe Commerce in der Cloud-Infrastruktur anweist, die Daten der übergeordneten Umgebung für Zusammenführungsanfragen zu klonen (`true` standardmäßig) |
| `--fetch-branches` | Ein Parameter _optional_ , der bewirkt, dass Adobe Commerce in der Cloud-Infrastruktur alle Zweige aus der Remote-Umgebung (als inaktive Umgebungen) abruft (`true` standardmäßig). |
| `--prune-branches` | Ein Parameter _optional_ , der Adobe Commerce in der Cloud-Infrastruktur anweist, Zweige zu löschen, die nicht auf der Remote-Site vorhanden sind (`true` standardmäßig) |

>[!WARNING]
>
>Der Befehl `magento-cloud integration` überschreibt den Code _all_ in Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur mit dem Code aus Ihrem GitLab-Repository. Dies umfasst alle Verzweigungen, einschließlich der Verzweigung `production` . Diese Aktion erfolgt sofort und kann nicht rückgängig gemacht werden. Als Best Practice ist es wichtig, alle Verzweigungen aus Ihrem Adobe Commerce im Cloud-Infrastrukturprojekt zu klonen und in Ihr GitLab-Repository zu übertragen, bevor Sie die GitLab-Integration hinzufügen.

**Aktivieren der GitLab-Integration**:

1. Fügen Sie vom Terminal die GitLab-Integration zu Ihrem Adobe Commerce on Cloud-Infrastrukturprojekt hinzu:

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. Geben Sie bei Aufforderung `y` ein, um die Integration hinzuzufügen.

   ```
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. Kopieren Sie die **Hook-URL**, die von der Ausgabe der Rückgabe angezeigt wird.

   ```
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### Webhook in GitLab hinzufügen

Um Ereignisse wie Push- oder Zusammenführungsanfragen mit Ihrem Cloud Git-Server zu kommunizieren, müssen Sie [einen Webhook ](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) für Ihr GitLab-Repository erstellen

1. Klicken Sie in Ihrem GitLab-Repository auf die Registerkarte **Einstellungen** .

1. Klicken Sie in der linken Navigationsleiste auf **Webhooks**.

1. Bearbeiten Sie im Formular _Webhooks_ die folgenden Felder:

   - **URL**: Geben Sie den `Hook URL` ein, der zurückgegeben wurde, als Sie die GitLab-Integration aktiviert haben.
   - **Geheimer Token**: Geben Sie bei Bedarf einen Verifizierungsgeheimnis ein.
   - **Trigger**: Aktivieren Sie je nach Bedarf die Optionen `Merge request events` und/oder `Push events`.
   - **Aktivieren Sie die SSL-Verifizierung**: Sie müssen diese Option auswählen.

1. Klicken Sie auf **Webhook hinzufügen**.

### Integration testen

Nach der Konfiguration der GitLab-Integration können Sie mithilfe der `magento-cloud`-CLI überprüfen, ob die Integration funktioniert:

```bash
magento-cloud integration:validate
```

Alternativ können Sie sie testen, indem Sie eine einfache Änderung an Ihr GitLab-Repository senden.

1. Erstellen Sie eine Testdatei.

   ```bash
   touch test.md
   ```

1. Übertragen Sie die Änderung und übertragen Sie sie in Ihr GitLab-Repository.

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. Melden Sie sich bei [[!DNL Cloud Console]](../project/overview.md) an und überprüfen Sie, ob Ihre Commit-Nachricht angezeigt wird und Ihr Projekt bereitgestellt wird.

## Cloud-Verzweigung erstellen

Verwenden Sie den Befehl `magento-cloud` CLI `environment:push` , um eine neue Umgebung zu erstellen und zu aktivieren. Siehe [Erstellen einer Cloud-Verzweigung](bitbucket.md#create-a-cloud-branch).

## Integration entfernen

Verwenden Sie den Befehl `magento-cloud` CLI `integration:delete` , um die Integration zu entfernen. Siehe [Entfernen der Integration](bitbucket.md#remove-the-integration).
