---
title: "Verwalten von Zweigen mit dem [!DNL Cloud Console]"
description: Erfahren Sie, wie Sie die Umgebungsverzweigungen für Adobe Commerce in der Cloud-Infrastruktur mit dem [!DNL Cloud Console] verwalten.
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Verwalten von Verzweigungen mit dem [!DNL Cloud Console]

Sie können Ihre Umgebungen mit der CLI [!DNL Cloud Console] oder `magento-cloud` verwalten. Ihre Projektdateien werden in einem Git-Repository gespeichert. Sie können Git-Befehle verwenden, um Ihren Code zu verwalten. Die CLI `magento-cloud` ist jedoch für die Interaktion mit Plattformfunktionen konzipiert, die Git-Befehle dagegen nicht. Siehe [Git-Befehle](../dev-tools/cloud-cli-overview.md#git-commands) im Cloud-CLI-Thema.

In diesem Thema wird erläutert, wie Sie mit dem [!DNL Cloud Console] Folgendes erreichen können:

- Hinzufügen oder Löschen einer Umgebung
- Synchronisieren (`git pull`) von der übergeordneten Umgebung
- Zusammenführen (`git push`) mit der übergeordneten Umgebung

>[!TIP]
>
>Sie können keine Verzweigungen aus der Staging- und Produktionsumgebung von Pro erstellen. Sie können eine Verzweigung vom Zweig `master` durchführen.

## Erstellen einer Umgebung

Die Verzweigungsstrategie verwendet einen gemeinsamen Git-Workflow, in dem Sie Code entwickeln und Erweiterungen in einer Entwicklungsverzweigung hinzufügen. Siehe Architekturübersichten [Starter](../architecture/starter-architecture.md) und [Pro](../architecture/starter-develop-deploy-workflow.md) .

- Erstellen Sie für Starter einen `staging` -Zweig aus der Verzweigung `master` und dann einen Zweig aus `staging` zur Entwicklung.
- Erstellen Sie für Pro einen Entwicklungszweig aus der Umgebung `Integration` .

Ihr Konto unterstützt eine begrenzte Anzahl von (inaktiven) ![aktiven Verzweigungen](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"}. Verwalten Sie aktive und inaktive Verzweigungen, indem Sie eine Verzweigung nur mit dem Wert &quot;[!DNL Cloud Console]&quot;oder der Cloud-CLI hinzufügen oder löschen. Bevor Sie einen Zweig löschen können, deaktivieren Sie den Zweig, der in der Liste _Umgebungen_ als _inactive_ verbleibt. Sie können die Verzweigung zu einem späteren Zeitpunkt reaktivieren oder Sie können den Zweig [löschen](../dev-tools/cloud-cli-overview.md#) in den Umgebungseinstellungen oder mithilfe der Cloud-CLI.

Wenn Sie zusätzliche aktive Umgebungen für die Entwicklung benötigen, senden Sie ein [Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**So fügen Sie einen Zweig hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie eine Umgebung aus.

   >[!TIP]
   >
   >Ihr neuer Zweig wird aus dieser Umgebung geklont. Wählen Sie eine übergeordnete Umgebung aus, die der Umgebung ähnelt, die Sie gerade erstellen.

1. Klicken Sie auf **[!UICONTROL Branch]**.

   ![Erstellen einer Verzweigung](../../assets/button-branch.png){width="150"}

1. Geben Sie im Formular _Verzweigung von ..._ einen Verzweigungsnamen ein.

   Die Umgebung _name_ unterscheidet sich nur dann von der Umgebung _ID_, wenn Sie Leerzeichen oder Großbuchstaben im Umgebungsnamen verwenden. Eine Umgebungs-ID besteht aus allen Kleinbuchstaben, Zahlen und zulässigen Symbolen. Großbuchstaben in einem Umgebungsnamen werden in der ID in Kleinbuchstaben umgewandelt; Leerzeichen in einem Umgebungsnamen werden in Bindestriche umgewandelt.

   Der Umgebungsname **kann keine Zeichen enthalten, die für Ihre Linux-Shell oder reguläre Ausdrücke reserviert sind.** Unzulässige Zeichen sind geschweifte Klammern (`{ }`), Klammern, Sternchen (`*`), spitze Klammern (`>`), Und-Zeichen (`&`), Prozent (<code>%)</code>) und anderen Zeichen.

1. Wählen Sie einen **[!UICONTROL Environment type]** aus.

1. Klicken Sie auf **[!UICONTROL Create Branch]**.

1. Warten Sie, während die Umgebung bereitgestellt wird.

   Während der Bereitstellung lautet der Umgebungsstatus **In Bearbeitung**. Nach einer erfolgreichen Bereitstellung ändert sich der Status in ein grünes Häkchen für **Erfolg**.

## Inaktive Verzweigung erstellen

Sie können keine inaktive Verzweigung über die Adobe Commerce Cloud-Konsole oder die CLI erstellen. Wenn Sie eine inaktive Verzweigung erstellen möchten, erstellen Sie sie im Git-Repository und pushen Sie mithilfe der Option `environment.Parent` im -Befehl.

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Löschen einer Umgebung

Bevor Sie eine Umgebung löschen können, müssen Sie sie deaktivieren. Sobald eine Umgebung inaktiv ist, können Sie sie löschen.

**So deaktivieren Sie eine Umgebung**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie die Umgebung aus der Liste der Navigationsleiste _Umgebung_ aus.

1. Klicken Sie auf das Konfigurationssymbol auf der rechten Seite der oberen Navigationsleiste, um die Umgebungseinstellungen zu öffnen.

1. Scrollen Sie auf der Registerkarte _[!UICONTROL General]_nach unten zum Abschnitt_[!UICONTROL Deactivate environment]_, klicken Sie auf **[!UICONTROL Deactivate environment and delete data]** und befolgen Sie die Anweisungen.

## Umgebung synchronisieren

Das Synchronisieren einer Umgebung (oder Verzweigung) ist mit `git pull origin <parent>` identisch. Sie können aktualisierten Code aus einer übergeordneten Umgebung synchronisieren. Sie können diese Funktion über die [!DNL Cloud Console] für alle Starter- und Pro-Umgebungen verwenden.

Für Pro Plan können Sie von Staging und Produktion mit Ihrer `master` -Verzweigung synchronisieren. Bei dieser Synchronisierung wird nur Code abgerufen und gepusht, nicht Daten. Um Daten zu synchronisieren, speichern Sie die Datenbankdaten und pushen Sie sie in die Datenbank einer anderen Umgebung. Siehe [ Migration und Bereitstellung statischer Dateien und Daten](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**So synchronisieren Sie eine Umgebung**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Klicken Sie in der Umgebungsliste auf den Namen des zu synchronisierenden Zweigs.

1. Klicken Sie auf (Synchronisieren).

   ![Synchronisieren einer Umgebung](../../assets/button-sync.png){width="150"}

1. Wählen Sie die zu synchronisierenden Elemente aus.

   - Ersetzen Sie die Daten (Daten und Dateien). Synchronisiert Änderungen in der Datenbank und den Inhaltsdateien aus der übergeordneten Verzweigung.
   - Merge—(code) synchronisiert aktualisierten Code aus der übergeordneten Verzweigung.

   Dadurch wird auch ein CLI-Befehl erstellt, den Sie kopieren und verwenden können.

1. Klicken Sie auf **Synchronisieren**.

## Zusammenführen mit der übergeordneten Umgebung

Das Zusammenführen einer Umgebung (oder eines Zweigs) entspricht `git push origin`. Sie werden zusammengeführt, um aktualisierten Code von einer Umgebung in die übergeordnete Umgebung zu pushen. Sie können diesen Code mit `master` zusammenführen. Sie können die Bereitstellung für Staging und Produktion mit dem Befehl `merge` durchführen.

**So führen Sie die Zusammenführung mit der übergeordneten Umgebung durch**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Klicken Sie in der Umgebungsliste auf den Namen der zusammenzuführenden Verzweigung.

1. Klicken Sie auf (Zusammenführen).

   ![Zusammenführen einer Umgebung](../../assets/button-merge.png){width="150"}

1. Klicken Sie auf **Zusammenführen** und bestätigen Sie die Aktion.

## Protokolle anzeigen

Mithilfe des [!DNL Cloud Console] können Sie verschiedene Protokolle für Umgebungen überprüfen, einschließlich Build, Bereitstellung und Bereitstellungsverlauf.

Für **Starter** können Sie Build- und Bereitstellungsprotokolle sowie den Bereitstellungsverlauf überprüfen. Zu diesen Umgebungen gehören die Verzweigung `master` (Produktion) und alle daraus erstellten Verzweigungen.

Für **Pro** können Sie die folgenden Protokolle in jeder Umgebung überprüfen:

- Integration - Build- und Bereitstellungsverlauf
- Staging: Erstellen Sie Protokolle und den Bereitstellungsverlauf. Verwenden Sie SSH, um sich beim Server anzumelden und Bereitstellungsprotokolle anzuzeigen.
- Produktion - Erstellen Sie Protokolle und den Bereitstellungsverlauf. Verwenden Sie SSH, um sich beim Server anzumelden und Bereitstellungsprotokolle anzuzeigen.

**So zeigen Sie Protokolle im[!DNL Cloud Console]** an:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie eine Umgebung aus.

   Die Umgebungsansicht bietet eine [Aktivitätsliste](activity-stream.md) , die die Ereignisse _recent_, einen Eintrag pro ausgeführter Aktion einschließlich Synchronisierungen, Zusammenführungen, Verzweigungen, Sicherungen und mehr anzeigt. Klicken Sie auf **Alle** , um den vollständigen Bereitstellungsverlauf anzuzeigen.

1. Um das Build-Protokoll anzuzeigen, wählen Sie den Link Erfolg oder Fehler pro Bereitstellungsdatensatz im Konto aus.

>[!TIP]
>
>Klicken Sie für eine Dropdown-Liste auf das Symbol **Filtern nach** und wählen Sie den Typ der anzuzeigenden Nachrichten aus.

## Code aus einem privaten Git-Repository abrufen

Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur kann Code aus einem privaten Git-Repository enthalten. Beispielsweise können Sie Code für ein benutzerdefiniertes Modul oder Design in einem privaten Repo haben. Dazu müssen Sie den öffentlichen SSH-Schlüssel Ihres Projekts zu Ihrem privaten Git-Repository hinzufügen und Ihre Projekt-Datei `composer.json` aktualisieren.

Um Ihrem privaten GitHub-Repository einen Bereitstellungsschlüssel hinzuzufügen, müssen Sie Administrator dieses Repositorys sein. Mit GitHub können Sie einen Bereitstellungsschlüssel nur für ein Repository verwenden.

Wenn Sie es vorziehen, dass Ihr Projekt auf mehrere Repositorys zugreift, können Sie einen SSH-Schlüssel an ein automatisiertes Benutzerkonto anhängen. Da dieses Konto nicht von einem Benutzer verwendet wird, wird es als [Machine user](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys) bezeichnet. Fügen Sie das Maschinenkonto als Mitarbeiter hinzu oder fügen Sie den Maschinenbenutzer einem Team mit Zugriff auf die Repositorys hinzu.

>[!INFO]
>
>Adobe empfiehlt das Hinzufügen und Zusammenführen dieses Codes zu Ihren Projekt-Git-Repositorys. Wenn Sie die Verbindung nicht konfigurieren, treten möglicherweise Build-Probleme auf.

**So suchen Sie Ihren öffentlichen SSH-Schlüssel**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Klicken Sie auf das Konfigurationssymbol auf der rechten Seite der oberen Navigationsleiste.

1. Klicken Sie in _Projekteinstellungen_ auf **[!UICONTROL Deploy Key]**.

1. Kopieren Sie den Bereitstellungsschlüssel zur Verwendung in einer der folgenden Git-basierten Methoden in die Zwischenablage:

>[!BEGINTABS]

>[!TAB GitHub]

### GitHub-Bereitstellungsschlüssel eingeben

Auf GitHub sind Bereitstellungsschlüssel standardmäßig schreibgeschützt.

**So geben Sie Ihren öffentlichen Projektschlüssel als GitHub-Bereitstellungsschlüssel ein**:

1. Melden Sie sich bei Ihrem GitHub-Repository als Administrator an.
1. Klicken Sie auf die Registerkarte Repository **[!UICONTROL Settings]** .

   >[!NOTE]
   >
   >Wenn diese Option nicht angezeigt wird, sind Sie nicht als Repository-Administrator angemeldet und können diese Aufgabe nicht ausführen. Bitten Sie dazu Ihren GitHub-Repository-Administrator.

1. Klicken Sie auf der Registerkarte _Einstellungen_ im linken Navigationsbereich auf **[!UICONTROL Deploy Keys]**.
1. Klicken Sie auf **[!UICONTROL Add deploy key]**.
1. Folgen Sie den Anweisungen.

Verwenden Sie in `composer.json` das Format `<user>@<host>:<.git</code>` oder `ssh://<user>@<host>:<port>/<path>.git` bei Verwendung eines nicht standardmäßigen Anschlusses.

>[!TAB Bitbucket]

### Geben Sie den Bitbucket-Bereitstellungsschlüssel ein

**So geben Sie Ihren öffentlichen Projektschlüssel als Bitbucket-Bereitstellungsschlüssel ein**:

1. Melden Sie sich bei Ihrem Bitbucket-Repository als Administrator an.
1. Klicken Sie im linken Navigationsbereich auf **[!UICONTROL Settings]**.
1. Klicken Sie auf Allgemein > **[!UICONTROL Deployment Keys]**.
1. Klicken Sie auf **[!UICONTROL Add Key]**.
1. Folgen Sie den Anweisungen.

>[!TAB GitLab]

### Geben Sie Ihren GitLab-Bereitstellungsschlüssel ein

**Hinzufügen des öffentlichen SSH-Schlüssels für Ihr Projekt als GitLab-Bereitstellungsschlüssel**:

1. Melden Sie sich bei Ihrem GitLab-Repository als Eigentümer an.
1. Stellen Sie sicher, dass die Option _Pipelines_ für Ihr Projekt aktiviert ist:

   1. Erweitern Sie in den Projekteinstellungen den Abschnitt **[!UICONTROL Visibility, project, features, permissions]** .
   1. Klicken Sie bei Bedarf auf **[!UICONTROL Pipelines]** , um die Option zu aktivieren.

1. Fügen Sie Ihren öffentlichen SSH-Schlüssel zu den CI/CD-Einstellungen hinzu.

   1. Klicken Sie im linken Navigationsbereich auf Einstellungen > **[!UICONTROL CI / CD]**.
   1. Klicken Sie auf Schlüssel bereitstellen **erweitern** , um den Schlüssel zu konfigurieren.
   1. Fügen Sie im Formular _Schlüssel bereitstellen_ einen Schlüsselnamen für die Bereitstellung zum Feld **[!UICONTROL Title]** hinzu und fügen Sie Ihren öffentlichen SSH-Schlüssel in das Feld **[!UICONTROL Key]** ein.
   1. Klicken Sie auf **[!UICONTROL Add Key]** , um die Konfiguration zu speichern.

>[!ENDTABS]

## Sichere Umgebungen und Zweige

Sie können über einen Webbrowser mit dem Wert &quot;[!DNL Cloud Console]&quot;von einem beliebigen Speicherort aus auf Ihr Projekt und Ihre Umgebungen zugreifen. Möglicherweise verfügen Sie über Sicherheitseinstellungen für Ihre Produktionsumgebung, Stores und Sites. In diesem Abschnitt erhalten Sie Informationen zum Sichern Ihrer Integrations- und Staging-Umgebungen für strikte Anforderungen an Entwickler, DBAs und mehr.

>[!WARNING]
>
>**VERWENDEN SIE NICHT** die folgenden Methoden zum Schützen von Pro Staging- und Produktionsumgebungen. Dies verhindert das schnelle Zwischenspeichern. Verwenden Sie die Funktion [Blocking](../cdn/fastly-vcl-blocking.md) , die im Fastly CDN für Adobe Commerce verfügbar ist.

**So sichern Sie Umgebungen**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com) an.

1. Wählen Sie ein Projekt aus der Liste _Alle Projekte_ aus.

1. Wählen Sie eine Umgebung aus und klicken Sie in der Navigationsleiste auf das Konfigurationssymbol .

1. Klicken Sie auf der Registerkarte &quot;Umgebungseinstellungen _Allgemein_&quot;auf **ON** für **[!UICONTROL HTTP access control enabled]**, um den sicheren Zugriff zu aktivieren. Sie können zwischen Anmeldedaten oder IP-Adressen wählen, um nach Zugriff zu filtern.

1. Um nach Anmeldeinformationen zu filtern, klicken Sie auf &quot;**[!UICONTROL Add Login]**&quot;, geben Sie einen Benutzernamen und ein Kennwort ein und klicken Sie auf &quot;**[!UICONTROL Add Login]**&quot;, um sie hinzuzufügen.

1. Um nach IP-Adresse zu filtern, geben Sie die IP-Adressen in eine Liste mit `deny` oder `allow` ein. Beispiel:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Klicken Sie auf **[!UICONTROL Save]**. Dadurch wird die Umgebung erneut bereitgestellt, um die Sicherheit und Einstellungen zu aktualisieren. Adobe empfiehlt, die Umgebung nach Abschluss der Sicherheitseinstellungen zu testen.
