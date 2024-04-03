---
title: "Verwalten Sie Verzweigungen mit dem [!DNL Cloud Console]"
description: Erfahren Sie, wie Sie die Umgebungsverzweigungen für Adobe Commerce in der Cloud-Infrastruktur mithilfe des [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Verwalten von Verzweigungen mit [!DNL Cloud Console]

Sie können Ihre Umgebungen mit dem [!DNL Cloud Console] oder `magento-cloud` CLI. Ihre Projektdateien werden in einem Git-Repository gespeichert. Sie können Git-Befehle verwenden, um Ihren Code zu verwalten, aber die `magento-cloud` CLI ist für die Interaktion mit Plattformfunktionen konzipiert, die Git-Befehle dagegen nicht. Siehe [Git-Befehle](../dev-tools/cloud-cli-overview.md#git-commands) im Cloud-CLI-Thema.

In diesem Thema wird die Verwendung der [!DNL Cloud Console] an:

- Hinzufügen oder Löschen einer Umgebung
- Synchronisieren (`git pull`) aus der übergeordneten Umgebung
- Zusammenführen (`git push`) zur übergeordneten Umgebung

>[!TIP]
>
>Sie können keine Verzweigungen aus der Staging- und Produktionsumgebung von Pro erstellen. Sie können die Verzweigung über die `master` -Verzweigung.

## Erstellen einer Umgebung

Die Verzweigungsstrategie verwendet einen gemeinsamen Git-Workflow, in dem Sie Code entwickeln und Erweiterungen in einer Entwicklungsverzweigung hinzufügen. Siehe [Starter](../architecture/starter-architecture.md) und [Pro](../architecture/starter-develop-deploy-workflow.md) Architekturübersichten.

- Erstellen Sie für &quot;Starter&quot;eine `staging` -Verzweigung aus `master` Verzweigung und dann Verzweigung von `staging` für die Entwicklung.
- Erstellen Sie für Pro einen Entwicklungszweig aus dem `Integration` Umgebung.

Ihr Konto unterstützt eine begrenzte Anzahl von ![aktive Verzweigung](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} (inaktive) Entwicklungszweige. Verwalten Sie aktive und inaktive Verzweigungen, indem Sie eine Verzweigung hinzufügen oder löschen, indem Sie nur die Variable [!DNL Cloud Console] oder die Cloud-CLI. Bevor Sie einen Zweig löschen können, deaktivieren Sie den Zweig, der im _Umgebungen_ list as _inactive_. Sie können die Verzweigung später erneut aktivieren oder Sie können [die Verzweigung löschen](../dev-tools/cloud-cli-overview.md#) in Umgebungseinstellungen oder unter Verwendung der Cloud-CLI.

Wenn Sie zusätzliche aktive Umgebungen für die Entwicklung benötigen, senden Sie eine [Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**So fügen Sie eine Verzweigung hinzu**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie eine Umgebung aus.

   >[!TIP]
   >
   >Ihr neuer Zweig wird aus dieser Umgebung geklont. Wählen Sie eine übergeordnete Umgebung aus, die der Umgebung ähnelt, die Sie gerade erstellen.

1. Klicks **[!UICONTROL Branch]**.

   ![Erstellen einer Verzweigung](../../assets/button-branch.png){width="150"}

1. Im _Verzweigung von ..._ Formular einen Zweignamen eingeben.

   Umwelt _name_ unterscheidet sich von der Umgebung _ID_ nur, wenn Sie Leerzeichen oder Großbuchstaben im Umgebungsnamen verwenden. Eine Umgebungs-ID besteht aus allen Kleinbuchstaben, Zahlen und zulässigen Symbolen. Großbuchstaben in einem Umgebungsnamen werden in der ID in Kleinbuchstaben umgewandelt; Leerzeichen in einem Umgebungsnamen werden in Bindestriche umgewandelt.

   Ein Umgebungsname **cannot** -Zeichen einschließen, die für Ihre Linux-Shell oder reguläre Ausdrücke reserviert sind. Unzulässige Zeichen sind geschweifte Klammern (`{ }`), Klammern, Sternchen (`*`), spitze Klammern (`>`), Und-Zeichen (`&`), Prozent (<code>%</code>) und anderen Zeichen.

1. Wählen Sie eine **[!UICONTROL Environment type]**.

1. Klicks **[!UICONTROL Create Branch]**.

1. Warten Sie, während die Umgebung bereitgestellt wird.

   Während der Bereitstellung lautet der Umgebungsstatus  **In Bearbeitung**. Nach einer erfolgreichen Bereitstellung ändert sich der Status in ein grünes Häkchen für **success**.

## Inaktive Verzweigung erstellen

Sie können keine inaktive Verzweigung über die Adobe Commerce Cloud-Konsole oder die CLI erstellen. Wenn Sie eine inaktive Verzweigung erstellen möchten, erstellen Sie sie im Git-Repository und pushen Sie mithilfe der `environment.Parent` -Option auf dem Befehl.

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Löschen einer Umgebung

Bevor Sie eine Umgebung löschen können, müssen Sie sie deaktivieren. Sobald eine Umgebung inaktiv ist, können Sie sie löschen.

**So deaktivieren Sie eine Umgebung**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie die Umgebung in der Navigationsleiste aus. _Umgebung_ Liste.

1. Klicken Sie auf das Konfigurationssymbol auf der rechten Seite der oberen Navigationsleiste, um die Umgebungseinstellungen zu öffnen.

1. Im _[!UICONTROL General]_-Registerkarte, scrollen Sie nach unten zum_[!UICONTROL Deactivate environment]_ und klicken Sie auf **[!UICONTROL Deactivate environment and delete data]** und befolgen Sie die Anweisungen.

## Umgebung synchronisieren

Die Synchronisierung einer Umgebung (oder Verzweigung) ist mit dem Szenario `git pull origin <parent>`. Sie können aktualisierten Code aus einer übergeordneten Umgebung synchronisieren. Sie können diese Funktion über die [!DNL Cloud Console] für alle Starter- und Pro-Umgebungen.

Für Pro-Abo können Sie von Staging und Produktion mit Ihrer `master` -Verzweigung. Bei dieser Synchronisierung wird nur Code abgerufen und gepusht, nicht Daten. Um Daten zu synchronisieren, speichern Sie die Datenbankdaten und pushen Sie sie in die Datenbank einer anderen Umgebung. Siehe [Migrieren und Bereitstellen von statischen Dateien und Daten](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**Synchronisieren einer Umgebung**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Klicken Sie in der Umgebungsliste auf den Namen des zu synchronisierenden Zweigs.

1. Klicken Sie auf (Synchronisieren).

   ![Umgebung synchronisieren](../../assets/button-sync.png){width="150"}

1. Wählen Sie die zu synchronisierenden Elemente aus.

   - Ersetzen Sie die Daten (Daten und Dateien). Synchronisiert Änderungen in der Datenbank und den Inhaltsdateien aus der übergeordneten Verzweigung.
   - Merge—(code) synchronisiert aktualisierten Code aus der übergeordneten Verzweigung.

   Dadurch wird auch ein CLI-Befehl erstellt, den Sie kopieren und verwenden können.

1. Klicks **Synchronisieren**.

## Zusammenführen mit der übergeordneten Umgebung

Das Zusammenführen einer Umgebung (oder eines Zweigs) ist mit dem Szenario `git push origin`. Sie werden zusammengeführt, um aktualisierten Code von einer Umgebung in die übergeordnete Umgebung zu pushen. Sie können diesen Code zu `master`. Sie können für Staging und Produktion mithilfe der `merge` Befehl.

**Zusammenführen mit der übergeordneten Umgebung**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Klicken Sie in der Umgebungsliste auf den Namen der zusammenzuführenden Verzweigung.

1. Klicken Sie auf (Zusammenführen).

   ![Zusammenführen einer Umgebung](../../assets/button-merge.png){width="150"}

1. Klicks **Zusammenführen** und bestätigen Sie die Aktion.

## Protokolle anzeigen

Durch die [!DNL Cloud Console]können Sie verschiedene Protokolle für Umgebungen überprüfen, einschließlich Build-, Bereitstellungs- und Bereitstellungsverlauf.

Für **Starter** können Sie Build- und Bereitstellungsprotokolle sowie den Bereitstellungsverlauf überprüfen. Diese Umgebungen umfassen `master` (Produktions-)Zweig und alle damit erstellten Zweige.

Für **Pro** können Sie die folgenden Protokolle in jeder Umgebung überprüfen:

- Integration - Build- und Bereitstellungsverlauf
- Staging: Erstellen Sie Protokolle und den Bereitstellungsverlauf. Verwenden Sie SSH, um sich beim Server anzumelden und Bereitstellungsprotokolle anzuzeigen.
- Produktion - Erstellen Sie Protokolle und den Bereitstellungsverlauf. Verwenden Sie SSH, um sich beim Server anzumelden und Bereitstellungsprotokolle anzuzeigen.

**So zeigen Sie Protokolle in der[!DNL Cloud Console]**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie eine Umgebung aus.

   Die Umgebungsansicht bietet eine [Aktivitätenliste](activity-stream.md) zeigt _kürzlich_ -Ereignisse, einen Eintrag pro versuchter Aktion, einschließlich Synchronisierungen, Zusammenführungen, Verzweigungen, Sicherungen und mehr. Klicks **Alle** für den vollständigen Implementierungsverlauf.

1. Um das Build-Protokoll anzuzeigen, wählen Sie den Link Erfolg oder Fehler pro Bereitstellungsdatensatz im Konto aus.

>[!TIP]
>
>Klicken Sie auf **Filtern nach** für eine Dropdown-Liste und wählen Sie den Typ der anzuzeigenden Nachrichten aus.

## Code aus einem privaten Git-Repository abrufen

Ihr Adobe Commerce-Projekt in der Cloud-Infrastruktur kann Code aus einem privaten Git-Repository enthalten. Beispielsweise können Sie Code für ein benutzerdefiniertes Modul oder Design in einem privaten Repo haben. Dazu müssen Sie den öffentlichen SSH-Schlüssel Ihres Projekts zu Ihrem privaten Git-Repository hinzufügen und Ihr Projekt aktualisieren `composer.json` -Datei.

Um Ihrem privaten GitHub-Repository einen Bereitstellungsschlüssel hinzuzufügen, müssen Sie Administrator dieses Repositorys sein. Mit GitHub können Sie einen Bereitstellungsschlüssel nur für ein Repository verwenden.

Wenn Sie es vorziehen, dass Ihr Projekt auf mehrere Repositorys zugreift, können Sie einen SSH-Schlüssel an ein automatisiertes Benutzerkonto anhängen. Da dieses Konto nicht von einem Menschen verwendet wird, wird es als [Maschinenbenutzer](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Fügen Sie das Maschinenkonto als Mitarbeiter hinzu oder fügen Sie den Maschinenbenutzer einem Team mit Zugriff auf die Repositorys hinzu.

>[!INFO]
>
>Adobe empfiehlt das Hinzufügen und Zusammenführen dieses Codes zu Ihren Projekt-Git-Repositorys. Wenn Sie die Verbindung nicht konfigurieren, treten möglicherweise Build-Probleme auf.

**So suchen Sie Ihren öffentlichen SSH-Schlüssel**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Klicken Sie auf das Konfigurationssymbol auf der rechten Seite der oberen Navigationsleiste.

1. In _Projekteinstellungen_ klicken **[!UICONTROL Deploy Key]**.

1. Kopieren Sie den Bereitstellungsschlüssel zur Verwendung in einer der folgenden Git-basierten Methoden in die Zwischenablage:

>[!BEGINTABS]

>[!TAB GitHub]

### GitHub-Bereitstellungsschlüssel eingeben

Auf GitHub sind Bereitstellungsschlüssel standardmäßig schreibgeschützt.

**So geben Sie Ihren öffentlichen Projektschlüssel als GitHub-Bereitstellungsschlüssel ein**:

1. Melden Sie sich bei Ihrem GitHub-Repository als Administrator an.
1. Klicken Sie auf das Repository **[!UICONTROL Settings]** Registerkarte.

   >[!NOTE]
   >
   >Wenn diese Option nicht angezeigt wird, sind Sie nicht als Repository-Administrator angemeldet und können diese Aufgabe nicht ausführen. Bitten Sie dazu Ihren GitHub-Repository-Administrator.

1. Im _Einstellungen_ Registerkarte in der linken Navigation auf **[!UICONTROL Deploy Keys]**.
1. Klicks **[!UICONTROL Add deploy key]**.
1. Folgen Sie den Anweisungen.

In `composer.json`, verwenden Sie die `<user>@<host>:<.git</code>` Format oder `ssh://<user>@<host>:<port>/<path>.git` bei Verwendung eines nicht standardmäßigen Ports.

>[!TAB Bitbucket]

### Geben Sie den Bitbucket-Bereitstellungsschlüssel ein

**So geben Sie Ihren öffentlichen Projektschlüssel als Bitbucket-Bereitstellungsschlüssel ein**:

1. Melden Sie sich bei Ihrem Bitbucket-Repository als Administrator an.
1. Klicken Sie im linken Navigationsbereich auf **[!UICONTROL Settings]**.
1. Klicken Sie auf Allgemein > **[!UICONTROL Deployment Keys]**.
1. Klicks **[!UICONTROL Add Key]**.
1. Folgen Sie den Anweisungen.

>[!TAB GitLab]

### Geben Sie Ihren GitLab-Bereitstellungsschlüssel ein

**Hinzufügen des öffentlichen SSH-Schlüssels für Ihr Projekt als GitLab-Bereitstellungsschlüssel**:

1. Melden Sie sich bei Ihrem GitLab-Repository als Eigentümer an.
1. Stellen Sie sicher, dass _Pipelines_ für Ihr Projekt aktiviert ist:

   1. Erweitern Sie in den Projekteinstellungen die **[!UICONTROL Visibility, project, features, permissions]** Abschnitt.
   1. Klicken Sie bei Bedarf auf **[!UICONTROL Pipelines]** , um die Option zu aktivieren.

1. Fügen Sie Ihren öffentlichen SSH-Schlüssel zu den CI/CD-Einstellungen hinzu.

   1. Klicken Sie im linken Navigationsbereich auf Einstellungen > **[!UICONTROL CI / CD]**.
   1. Klicken Sie auf Schlüssel bereitstellen . **Erweitern** um den Schlüssel zu konfigurieren.
   1. Im _Bereitstellungsschlüssel_ Fügen Sie dem Formular einen Namen für den Bereitstellungsschlüssel hinzu. **[!UICONTROL Title]** und fügen Sie Ihren öffentlichen SSH-Schlüssel in das **[!UICONTROL Key]** -Feld.
   1. Klicks **[!UICONTROL Add Key]** , um die Konfiguration zu speichern.

>[!ENDTABS]

## Sichere Umgebungen und Zweige

Sie können über einen Webbrowser über die [!DNL Cloud Console]. Möglicherweise verfügen Sie über Sicherheitseinstellungen für Ihre Produktionsumgebung, Stores und Sites. In diesem Abschnitt erhalten Sie Informationen zum Sichern Ihrer Integrations- und Staging-Umgebungen für strikte Anforderungen an Entwickler, DBAs und mehr.

>[!WARNING]
>
>**NICHT** Verwenden Sie die folgenden Methoden zum Schützen von Pro Staging- und Produktionsumgebungen. Dies verhindert das schnelle Zwischenspeichern. Verwenden Sie die [Blockieren](../cdn/fastly-vcl-blocking.md) Funktion im Fastly CDN für Adobe Commerce verfügbar.

**Sichere Umgebungen**:

1. Melden Sie sich bei [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Wählen Sie ein Projekt aus dem _Alle Projekte_ Liste.

1. Wählen Sie eine Umgebung aus und klicken Sie in der Navigationsleiste auf das Konfigurationssymbol .

1. In den Umgebungseinstellungen _Allgemein_ Registerkarte, klicken **ON** für **[!UICONTROL HTTP access control enabled]** um sicheren Zugriff zu aktivieren. Sie können zwischen Anmeldedaten oder IP-Adressen wählen, um nach Zugriff zu filtern.

1. Um nach Anmeldeinformationen zu filtern, klicken Sie auf **[!UICONTROL Add Login]**, geben Sie einen Benutzernamen und ein Kennwort ein und klicken Sie auf **[!UICONTROL Add Login]** hinzugefügt werden.

1. Um nach IP-Adresse zu filtern, geben Sie die IP-Adressen in eine Liste ein mit `deny` oder `allow`. Beispiel:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Klicks **[!UICONTROL Save]**. Dadurch wird die Umgebung erneut bereitgestellt, um die Sicherheit und Einstellungen zu aktualisieren. Adobe empfiehlt, die Umgebung nach Abschluss der Sicherheitseinstellungen zu testen.
