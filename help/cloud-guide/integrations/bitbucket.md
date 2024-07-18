---
title: Bitbucket-Integration
description: Erfahren Sie, wie Sie Ihr Adobe Commerce in das Cloud-Infrastrukturprojekt mit Bitbucket integrieren.
feature: Cloud, Integration
exl-id: cd3cffbe-268f-429b-a2ea-0306159f4a6b
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Bitbucket-Integration

Sie können Ihr Bitbucket-Repository so konfigurieren, dass beim Push von Code-Änderungen automatisch eine Umgebung erstellt und bereitgestellt wird. Diese Integration synchronisiert Ihr Bitbucket-Repository mit Ihrem Adobe Commerce-Konto für die Cloud-Infrastruktur.

{{private-repository}}

## Voraussetzungen

- Administratorzugriff auf das Adobe Commerce-Projekt in der Cloud-Infrastruktur
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md)-Tool in Ihrer lokalen Umgebung
- Ein Bitbucket-Konto
- Administratorzugriff auf das Bitbucket-Repository
- Einen SSH-Zugriffsschlüssel für das Bitbucket-Repository

## Repository vorbereiten

Klonen Sie Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur von einer bestehenden Umgebung und migrieren Sie die Projektverzweigungen in ein neues, leeres Bitbucket-Repository, wobei Sie dieselben Zweignamen beibehalten. Es ist **wichtig**, eine identische Git-Struktur beizubehalten, damit Sie keine bestehenden Umgebungen oder Verzweigungen in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt verlieren.

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

1. Fügen Sie Ihr Bitbucket-Repository als Remote-Ressource hinzu.

   ```bash
   git remote add origin git@bitbucket.org:<user-name>/<repo-name>.git
   ```

   Der Standardname für die Remote-Verbindung kann `origin` oder `magento` sein. Wenn `origin` vorhanden ist, können Sie einen anderen Namen wählen oder die vorhandene Referenz umbenennen oder löschen. Siehe [git-remote-Dokumentation](https://git-scm.com/docs/git-remote).

1. Vergewissern Sie sich, dass Sie die Bitbucket-Fernbedienung korrekt hinzugefügt haben.

   ```bash
   git remote -v
   ```

   Erwartete Antwort:

   ```
   origin git@bitbucket.org:<user-name>/<repo-name>.git (fetch)
   origin git@bitbucket.org:<user-name>/<repo-name>.git (push)
   ```

1. Übertragen Sie die Projektdateien in Ihr neues Bitbucket-Repository. Denken Sie daran, alle Zweignamen gleich zu halten.

   ```bash
   git push -u origin master
   ```

   Wenn Sie mit einem neuen Bitbucket-Repository beginnen, müssen Sie möglicherweise die Option `-f` verwenden, da das Remote-Repository nicht mit Ihrer lokalen Kopie übereinstimmt.

1. Stellen Sie sicher, dass Ihr Bitbucket-Repository alle Ihre Projektdateien enthält.

## OAuth-Verbraucher erstellen

Für die Bitbucket-Integration ist ein [OAuth-Benutzer](https://support.atlassian.com/bitbucket-cloud/docs/use-oauth-on-bitbucket-cloud/) erforderlich. Sie benötigen die OAuth `key` und `secret` von diesem Verbraucher, um den nächsten Abschnitt abzuschließen.

**Erstellen eines OAuth-Verbrauchers in Bitbucket**:

1. Melden Sie sich bei Ihrem [Bitbucket](https://id.atlassian.com/login) -Konto an.

1. Klicken Sie auf **Einstellungen** > **Zugriffsverwaltung** > **OAuth**.

1. Klicken Sie auf **Benutzer hinzufügen** und konfigurieren Sie ihn wie folgt:

   ![Bitbucket OAuth-Verbraucherkonfiguration](../../assets/oauth-consumer-config.png)

   >[!WARNING]
   >
   >Eine gültige **Callback-URL** ist nicht erforderlich, Sie müssen jedoch einen Wert in dieses Feld eingeben, um die Integration erfolgreich abzuschließen.

1. Klicken Sie auf **Speichern**.

1. Klicken Sie auf den Verbraucher **Name** , um Ihre OAuth `key` und `secret` anzuzeigen.

1. Kopieren Sie Ihre OAuth `key` und `secret` für die Konfiguration der Integration.

## Integration konfigurieren

1. Navigieren Sie vom Terminal zu Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur.

1. Erstellen Sie eine temporäre Datei mit dem Namen `bitbucket.json` und fügen Sie Folgendes hinzu, wobei Sie die Variablen in spitzen Klammern durch Ihre Werte ersetzen:

   ```json
   {
     "type": "bitbucket",
     "repository": "<bitbucket-user-name/bitbucket-repo-name>",
     "app_credentials": {
       "key": "<oauth-consumer-key>",
       "secret": "<oauth-consumer-secret>"
     },
     "prune_branches": true,
     "fetch_branches": true,
     "build_pull_requests": true,
     "resync_pull_requests": true
   }
   ```

   >[!TIP]
   >
   >Verwenden Sie unbedingt den Namen Ihres Bitbucket-Repositorys und nicht die URL. Die Integration schlägt fehl, wenn Sie eine URL verwenden.

1. Fügen Sie die Integration mit dem CLI-Tool `magento-cloud` zu Ihrem Projekt hinzu.

   >[!WARNING]
   >
   >Der folgende Befehl überschreibt den Code _all_ in Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur mit Code aus Ihrem Bitbucket-Repository. Dies umfasst alle Verzweigungen, einschließlich der Verzweigung `production` . Diese Aktion erfolgt sofort und kann nicht rückgängig gemacht werden. Als Best Practice ist es wichtig, alle Verzweigungen aus Ihrem Adobe Commerce-Projekt in der Cloud-Infrastruktur zu klonen und sie in Ihr Bitbucket-Repository zu übertragen, **bevor** die Bitbucket-Integration hinzufügt.

   ```bash
   magento-cloud project:curl -p '<project-ID>' /integrations -i -X POST -d "$(< bitbucket.json)"
   ```

   Dadurch wird eine lange HTTP-Antwort mit Headern zurückgegeben. Bei erfolgreicher Integration wird der Status-Code 200 oder 201 zurückgegeben. Der Status 400 oder höher zeigt an, dass ein Fehler aufgetreten ist.

1. Löschen Sie die temporäre Datei &quot;`bitbucket.json`&quot;.

1. Überprüfen Sie die Projektintegration.

   ```bash
   magento-cloud integrations -p <project-ID>
   ```

   ```
   +----------+-----------+--------------------------------------------------------------------------------+
   | ID       | Type      | Summary                                                                        |
   +----------+-----------+--------------------------------------------------------------------------------+
   | <int-id> | bitbucket | Repository: bitbucket_Account/magento-int                                      |
   |          |           | Hook URL:                                                                      |
   |          |           | https://magento-url.cloud/api/projects/<project-id>/integrations/<int-id>/hook |
   +----------+-----------+--------------------------------------------------------------------------------+
   ```

   Notieren Sie sich die **Hook-URL** , um einen Webhook in BitBucket zu konfigurieren.

### Webhook in BitBucket hinzufügen

Um Ereignisse wie Push-Benachrichtigungen mit Ihrem Cloud Git-Server zu kommunizieren, benötigen Sie einen Webhook für Ihr BitBucket-Repository. Die auf dieser Seite beschriebene Methode zum Einrichten einer Bitbucket-Integration erstellt automatisch einen Webhook, wenn sie korrekt ausgeführt wird. Es ist wichtig, den Webhook zu überprüfen, um das Erstellen mehrerer Integrationen zu vermeiden.

1. Melden Sie sich bei Ihrem [Bitbucket](https://id.atlassian.com/login) -Konto an.

1. Klicken Sie auf **Repositorys** und wählen Sie Ihr Projekt aus.

1. Klicken Sie auf **Repository-Einstellungen** > **Workflow** > **Webhooks**.

1. Überprüfen Sie den Webhook, bevor Sie fortfahren.

   Wenn der Hook aktiv ist, überspringen Sie die verbleibenden Schritte und [Testen Sie die Integration](#test-the-integration). Der Hook sollte einen ähnlichen Namen haben wie **&quot;Adobe Commerce on cloud Infrastructure &lt;project_id>&quot;** und ein Hook-URL-Format wie: `https://<zone>.magento.cloud/api/projects/<project_id>/integrations/<id>/hook`

1. Klicken Sie auf **Webhook hinzufügen**.

1. Bearbeiten Sie in der Ansicht _Neuen Webhook hinzufügen_ die folgenden Felder:

   - **Titel**: Adobe Commerce-Integration
   - **URL**: Verwenden Sie die Hook-URL aus Ihrer `magento-cloud` Integrationsliste.
   - **Trigger**: Der Standardwert ist ein einfacher _Repository-Push-Vorgang_

1. Klicken Sie auf **Speichern**.

### Integration testen

Nach der Konfiguration der Bitbucket-Integration können Sie mithilfe der `magento-cloud`-CLI überprüfen, ob die Integration funktioniert:

```bash
magento-cloud integration:validate
```

Alternativ können Sie sie testen, indem Sie eine einfache Änderung an Ihr Bitbucket-Repository senden.

1. Erstellen Sie eine Testdatei.

   ```bash
   touch test.md
   ```

1. Übertragen Sie die Änderung in Ihr Bitbucket-Repository.

   ```bash
   git add . && git commit -m "Testing Bitbucket integration" && git push
   ```

1. Melden Sie sich bei [[!DNL Cloud Console]](../project/overview.md) an und überprüfen Sie, ob Ihre Commit-Nachricht angezeigt wird und Ihr Projekt bereitgestellt wird.

   ![Testen der Bitbucket-Integration](../../assets/bitbucket-integration.png)

## Cloud-Verzweigung erstellen

Die Bitbucket-Integration kann keine neuen Umgebungen in Ihrer Adobe Commerce im Cloud-Infrastrukturprojekt aktivieren. Wenn Sie eine Umgebung mit Bitbucket erstellen, müssen Sie die Umgebung manuell aktivieren. Um diesen zusätzlichen Schritt zu vermeiden, empfiehlt es sich, Umgebungen mit dem `magento-cloud` CLI-Tool oder dem [!DNL Cloud Console] zu erstellen.

**So aktivieren Sie eine mit Bitbucket** erstellte Verzweigung:

1. Verwenden Sie die CLI `magento-cloud` , um den Zweig zu verschieben.

   ```bash
   magento-cloud environment:push from-bitbucket
   ```

   ```
   Pushing from-bitbucket to the new environment from-bitbucket
   Activate from-bitbucket after pushing? [Y/n] y
   Parent environment [master]: integration
   --- (Validation and activation messages)
   ```

1. Stellen Sie sicher, dass die Umgebung aktiv ist.

   ```bash
   magento-cloud environment:list
   ```

   ```
   Your environments are:
   +---------------------+----------------+--------+
   | ID                  | Name           | Status |
   +---------------------+----------------+--------+
   | master              | Master         | Active |
   |  integration        | integration    | Active |
   |    from-bitbucket * | from-bitbucket | Active |
   +---------------------+----------------+--------+
   * - Indicates the current environment
   ```

Nachdem Sie eine Umgebung erstellt haben, können Sie die entsprechende Verzweigung mithilfe regulärer Git-Befehle an Ihr Remote-Bitbucket-Repository übertragen. Nachfolgende Änderungen an Ihrer Verzweigung in Bitbucket erstellen und stellen die Umgebung automatisch bereit.

## Integration entfernen

Sie können die Bitbucket-Integration sicher aus Ihrem Projekt entfernen, ohne den Code zu beeinträchtigen.

**Entfernen der Bitbucket-Integration**:

1. Melden Sie sich über das Terminal bei Ihrem Adobe Commerce-Projekt für eine Cloud-Infrastruktur an.

1. Geben Sie Ihre Integrationen an. Sie benötigen die Bitbucket-Integrations-ID, um den nächsten Schritt abzuschließen.

   ```bash
   magento-cloud integration:list
   ```

1. Löschen Sie die Integration.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Außerdem können Sie die Bitbucket-Integration entfernen, indem Sie sich bei Ihrem Bitbucket-Konto anmelden und die OAuth-Finanzhilfe für das Konto _Einstellungen_ widerrufen.

## Integration von Bitbucket-Servern

Um die Bitbucket-Serverintegration zu verwenden, benötigen Sie Folgendes:

- [Bitbucket-Zugriffstoken](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html) - Generieren Sie ein Token, das dem Projekt `read` Zugriff und dem Repository `admin` Zugriff gewährt
- [Bitbucket-Server-URL](https://confluence.atlassian.com/bitbucketserver/specify-the-bitbucket-base-url-776640392.html) - Fügen Sie die Basis-URL Ihrer Bitbucket-Instanz hinzu.

Sie können zwar die Cloud-CLI verwenden, um durch die Integrationsschritte des Bitbucket-Servers zu navigieren, der vollständige Befehl sieht jedoch wie folgt aus:

```bash
magento-cloud integration:add --type=bitbucket_server --base-url=<bitbucket-url> --username=<username> --token=<bitbucket-access-token> --project=<project-ID>
```

Verwenden Sie den Hilfebefehl, um mehr Nutzungsanforderungen und -optionen zu erhalten: `magento-cloud integration:add --help`
