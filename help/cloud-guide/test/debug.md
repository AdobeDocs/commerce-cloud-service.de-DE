---
title: Konfigurieren von  [!DNL Xdebug]
description: Erfahren Sie, wie Sie die Xdebug-Erweiterung für das Debugging Ihrer Adobe Commerce in der Cloud-Infrastruktur-Projektentwicklung konfigurieren.
exl-id: bf2d32d8-fab7-439e-8df3-b039e53009d4
source-git-commit: 751456f50e7b017b47c2ff43e008c2d04a558d96
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# Xdebug konfigurieren

[!DNL Xdebug] ist eine Erweiterung zum Debuggen von PHP. Obwohl Sie eine IDE Ihrer Wahl verwenden können, wird im Folgenden beschrieben, wie Sie [!DNL Xdebug] und [!DNL PhpStorm] zum Debugging in Ihrer lokalen Umgebung konfigurieren.

>[!NOTE]
>
>Sie können [!DNL Xdebug] so konfigurieren, dass es in der Cloud-Docker-Umgebung für lokales Debugging ausgeführt wird, ohne die Konfiguration des Adobe Commerce-Projekts in der Cloud-Infrastruktur zu ändern. Siehe [Xdebug für Docker konfigurieren](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/).

Um [!DNL Xdebug] zu aktivieren, müssen Sie eine Datei in Ihrem Git-Repository konfigurieren, Ihre IDE konfigurieren und die Anschlussweiterleitung einrichten. Sie können einige Einstellungen in der Datei `magento.app.yaml` konfigurieren. Push nach der Bearbeitung die Git-Änderungen über alle Starter-Umgebungen und Pro-Integrationsumgebungen hinweg, um [!DNL Xdebug] zu aktivieren. [!DNL Xdebug] ist bereits in Pro Staging- und Produktionsumgebungen verfügbar.

Nach der Konfiguration können Sie CLI-Befehle, Webanfragen und Code debuggen. Beachten Sie, dass alle Cloud-Infrastrukturumgebungen schreibgeschützt sind. Klonen Sie den Code in Ihrer lokalen Entwicklungsumgebung, um das Debugging durchzuführen. Informationen zu Pro-Staging- und Produktionsumgebungen finden Sie unter [zusätzliche Anweisungen](#debug-for-pro-staging-and-production) für [!DNL Xdebug].

## Voraussetzungen

Um [!DNL Xdebug] auszuführen und zu verwenden, benötigen Sie die SSH-URL für die Umgebung. Sie können die Informationen über die [[!DNL Cloud Console]](../project/overview.md) oder Ihre [!DNL Cloud Onboarding UI] finden.

## Xdebug konfigurieren

Gehen Sie wie folgt vor, um [!DNL Xdebug] zu konfigurieren:

- [Arbeiten in einer Verzweigung zum Push von Dateiaktualisierungen](#get-started-with-a-branch)
- [Aktivieren Sie [!DNL Xdebug] für Umgebungen](#enable-xdebug-in-your-environment)
- [IDE konfigurieren](#configure-phpstorm)
- [Einrichten der Anschlussweiterleitung](#set-up-port-forwarding)

### Erste Schritte mit einer Verzweigung

Um [!DNL Xdebug] hinzuzufügen, empfiehlt Adobe, in [einer Entwicklungsverzweigung](../dev-tools/cloud-cli-overview.md#create-an-environment-branch) zu arbeiten.

### Aktivieren Sie Xdebug in Ihrer Umgebung

Sie können [!DNL Xdebug] direkt für alle Starter-Umgebungen und Pro-Integrationsumgebungen aktivieren. Dieser Konfigurationsschritt ist nicht für Pro Production- und Staging-Umgebungen erforderlich. Siehe [Debuggen für Pro Staging und Produktion](#debug-for-pro-staging-and-production).

Um [!DNL Xdebug] für Ihr Projekt zu aktivieren, fügen Sie `xdebug` zum Abschnitt `runtime:extensions` der Datei `.magento.app.yaml` hinzu.

**So aktivieren Sie Xdebug**:

1. Öffnen Sie in Ihrem lokalen Terminal die Datei `.magento.app.yaml` in einem Texteditor.

1. Fügen Sie im Abschnitt `runtime` unter `extensions` den Wert `xdebug` hinzu. Beispiel:

   ```yaml
   runtime:
       extensions:
           - redis
           - xsl
           - newrelic
           - sodium
           - xdebug
   ```

1. Speichern Sie Ihre Änderungen in der Datei `.magento.app.yaml` und beenden Sie den Texteditor.

1. Fügen Sie die Änderungen hinzu, übertragen und pushen Sie sie, um sie erneut bereitzustellen.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Add xdebug"
   ```

   ```bash
   git push origin <environment-ID>
   ```

Bei der Bereitstellung in Starter-Umgebungen und Pro-Integrationsumgebungen ist [!DNL Xdebug] jetzt verfügbar. Fahren Sie mit der Konfiguration Ihrer IDE fort. Informationen zu PHPStorm finden Sie unter [PHPStorm konfigurieren](#configure-phpstorm).

### PHPStorm konfigurieren

Die IDE [PhpStorm](https://www.jetbrains.com/phpstorm/) muss so konfiguriert sein, dass sie mit [!DNL Xdebug] ordnungsgemäß funktioniert.

**So konfigurieren Sie PhpStorm für die Verwendung mit Xdebug**:

1. Öffnen Sie in Ihrem PhpStorm-Projekt das Bedienfeld **Einstellungen** .

   - _macOS_ - Wählen Sie **PHPStorm** > **Voreinstellungen** aus.
   - _Windows/Linux_ - Wählen Sie **Datei** > **Einstellungen** aus.

1. Erweitern Sie im Bedienfeld _Einstellungen_ den Abschnitt **Sprachen und Frameworks** > **PHP** > **Server** und suchen Sie ihn.

1. Klicken Sie auf **+** , um eine Serverkonfiguration hinzuzufügen. Oben ist der Projektname grau.

1. [Optional] Konfigurieren Sie die folgenden Einstellungen für die neue Serverkonfiguration. Siehe [Kein Debug-Server konfiguriert](https://www.jetbrains.com/help/phpstorm/troubleshooting-php-debugging.html#no-debug-server-is-configured) in der Dokumentation zu _PHPStorm_ .

   - **Name**: Geben Sie denselben Namen wie der Hostname ein. Dieser Wert muss mit dem Wert für die Variable `PHP_IDE_CONFIG` in den [CLI-Befehlen debuggen](#debug-cli-commands) übereinstimmen, damit CLI zum Debugging verwendet werden kann.
   - **Host**: Geben Sie den Hostnamen ein.
   - **Port**—Geben Sie `443` ein.
   - **Debugger** - Wählen Sie `Xdebug` aus.

1. Wählen Sie **Pfadzuordnungen verwenden** aus. Im Bereich _Datei/Verzeichnis_ wird der Stamm des Projekts für die `serverName` angezeigt.

1. Klicken Sie in der Spalte **Absoluter Pfad auf dem Server** auf das Symbol **Bearbeiten** und fügen Sie eine Einstellung hinzu, die auf der Umgebung basiert.

   - Für alle Starter-Umgebungen und Pro-Integrationsumgebungen lautet der Remote-Pfad `/app`.
   - Für Staging- und Produktionsumgebungen:

      - Produktion: `/app/<project_code>/`
      - Staging: `/app/<project_code>_stg/`

1. Ändern Sie den Port [!DNL Xdebug] im Bedienfeld **Sprachen und Frameworks** > **PHP** > **Debug** > **Xdebug** > **Debug Port** auf 9000.

1. Klicken Sie auf **Anwenden**.

### Einrichten der Anschlussweiterleitung

Ordnen Sie die `XDEBUG` -Verbindung vom Server Ihrem lokalen System zu. Für jede Art von Debugging müssen Sie Port 9000 von Ihrem Adobe Commerce auf dem Cloud-Infrastrukturserver an Ihren lokalen Computer weiterleiten. Siehe einen der folgenden Abschnitte:

- [Anschlussweiterleitung auf Mac oder UNIX](#port-forwarding-on-mac-or-unix)
- [Anschlussweiterleitung unter Windows](#port-forwarding-on-windows)

#### Anschlussweiterleitung auf Mac oder UNIX®

**So richten Sie die Anschlussweiterleitung auf einem Mac oder in einer UNIX®-Umgebung ein**:

1. Öffnen Sie ein Terminal.

1. Verwenden Sie SSH, um die Verbindung herzustellen.

   ```bash
   ssh -R 9000:localhost:9000 <ssh url>
   ```

   Verwenden Sie die Option `-v` (verbose), damit ein Socket immer dann im Terminal angezeigt wird, wenn er mit dem weitergeleiteten Port verbunden ist.

   Wenn der Fehler &quot;Verbindung nicht möglich&quot;oder &quot;Anschluss auf Remote-Server konnte nicht überwacht werden&quot;angezeigt wird, kann es zu einer weiteren aktiven SSH-Sitzung kommen, die auf dem Server, der Port 9000 belegt, fortbesteht. Wenn diese Verbindung nicht verwendet wird, können Sie sie beenden.

**Fehlerbehebung bei der Verbindung**:

1. Verwenden Sie SSH, um sich bei der Remote-Integration, Staging- oder Produktionsumgebung anzumelden.

1. Anzeigen einer Liste von SSH-Sitzungen: `who`

1. Vorhandene SSH-Sitzungen nach Benutzer anzeigen. Achten Sie darauf, einen anderen Benutzer als Sie nicht zu beeinträchtigen!

   - integration: Benutzernamen ähneln `dd2q5ct7mhgus`
   - Staging: Benutzernamen ähneln `dd2q5ct7mhgus_stg`
   - Produktion: Benutzernamen ähneln `dd2q5ct7mhgus`

1. Für eine Benutzersitzung, die älter als Ihre ist, suchen Sie den Pseudo-Terminal-Wert (PTS), z. B. `pts/0`.

1. Beenden Sie die Prozess-ID (PID), die dem PTS-Wert entspricht.

   ```bash
   ps aux | grep ssh
   kill <PID>
   ```

   Beispielantwort:

   ```terminal
   dd2q5ct7mhgus        5504  0.0  0.0  82612  3664 ?      S    18:45   0:00 sshd: dd2q5ct7mhgus@pts/0
   ```

   Um die Verbindung zu beenden, geben Sie einen Befehl zum Abbrechen mit der Prozess-ID (PID) ein.

   ```bash
   kill 3664
   ```

#### Anschlussweiterleitung unter Windows

Um die Anschlussweiterleitung (SSH-Tunnel) unter Windows einzurichten, müssen Sie Ihre Windows Terminal-Anwendung konfigurieren. In diesem Beispiel wird die Erstellung eines SSH-Tunnels mit [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) beschrieben. Sie können andere Anwendungen wie Cygwin verwenden. Weitere Informationen zu anderen Anwendungen finden Sie in der Dokumentation des Anbieters, die mit diesen Anwendungen bereitgestellt wird.

**So richten Sie einen SSH-Tunnel unter Windows mithilfe von Putty** ein:

1. Falls noch nicht geschehen, laden Sie [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) herunter.

1. Starten Sie Putty.

1. Klicken Sie im Bereich Kategorie auf **Sitzung**.

1. Geben Sie die folgenden Informationen ein:

   - Feld **Hostname (oder IP-Adresse)**: Geben Sie die [SSH-URL](../development/secure-connections.md#connect-to-a-remote-environment) für Ihren Cloud-Server ein.
   - Feld **Port**: Eingabe `22`

   ![Einrichten von Putty](../../assets/xdebug/putty-session.png)

1. Klicken Sie im Bereich _Kategorie_ auf **Verbindung** > **SSH** > **Tunnel**.

1. Geben Sie die folgenden Informationen ein:

   - Feld **Source-Port**: Geben Sie `9000` ein.
   - Feld **Ziel**: Eingabe `127.0.0.1:9000`
   - Klicken Sie auf **Remote**

1. Klicken Sie auf **Hinzufügen**.

   ![Erstellen eines SSH-Tunnels in Putty](../../assets/xdebug/putty-tunnels.png)

1. Klicken Sie im Bereich _Kategorie_ auf **Sitzung**.

1. Geben Sie im Feld **Gespeicherte Sitzungen** einen Namen für diesen SSH-Tunnel ein.

1. Klicken Sie auf **Speichern**.

   ![Speichern Sie Ihren SSH-Tunnel](../../assets/xdebug/putty-session-save.png)

1. Um den SSH-Tunnel zu testen, klicken Sie auf **laden** und dann auf **Öffnen**.

   Wenn der Fehler &quot;Verbindung nicht möglich&quot;angezeigt wird, überprüfen Sie Folgendes:

   - Alle Pfadeinstellungen sind korrekt
   - Sie führen Putty auf dem Computer aus, auf dem sich Ihre privaten Adobe Commerce-SSH-Schlüssel in der Cloud-Infrastruktur befinden

## SSH-Zugriff auf Xdebug-Umgebungen

Zum Initiieren des Debuggens, zum Ausführen des Setups und mehr benötigen Sie die SSH-Befehle für den Zugriff auf die Umgebungen. Sie können diese Informationen über die [[!DNL Cloud Console]](../development/secure-connections.md#use-an-ssh-command) und Ihre Projekttabelle abrufen.

In Starter-Umgebungen und Pro-Integrationsumgebungen können Sie den folgenden `magento-cloud` CLI-Befehl für SSH in diesen Umgebungen verwenden:

```bash
magento-cloud environment:ssh --pipe -e <environment-ID>
```

Um [!DNL Xdebug] zu verwenden, verwenden Sie SSH wie folgt in der Umgebung:

```bash
ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH-URL>
```

Beispiel:

```bash
ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud
```

## Debug für Pro Staging und Produktion

>[!NOTE]
>
>In Pro-Staging- und Produktionsumgebungen ist [!DNL Xdebug] immer verfügbar, da diese Umgebungen über eine spezielle Einrichtung für [!DNL Xdebug] verfügen. Alle normalen Webanfragen werden an einen dedizierten PHP-Prozess weitergeleitet, der nicht über [!DNL Xdebug] verfügt. Daher werden diese Anforderungen normal verarbeitet und unterliegen beim Laden von [!DNL Xdebug] nicht der Leistungsbeeinträchtigung. Wenn eine Webanfrage gesendet wird, die den Schlüssel [!DNL Xdebug] enthält, wird sie an einen separaten PHP-Prozess weitergeleitet, in dem [!DNL Xdebug] geladen ist.

Um [!DNL Xdebug] speziell in der Staging- und Produktionsumgebung von Pro Plan zu verwenden, erstellen Sie einen separaten SSH-Tunnel und eine Websitzung, auf die Sie nur Zugriff haben. Diese Nutzung unterscheidet sich von dem typischen Zugriff, der nur Ihnen und nicht allen Benutzern Zugriff gewährt.

Sie benötigen Folgendes:

- SSH-Befehle für den Zugriff auf die Umgebungen. Sie können diese Informationen über die [[!DNL Cloud Console]](../project/overview.md) oder Ihre [!DNL Cloud Onboarding UI] erhalten.
- Der bei der Konfiguration der Staging- und Pro-Umgebungen festgelegte `xdebug_key` -Wert.

  Der `xdebug_key`-Wert kann mithilfe von SSH gefunden werden, um sich beim primären Knoten anzumelden und auszuführen:

  ```bash
  cat /etc/platform/*/nginx.conf | grep xdebug.sock | head -n1
  ```

**So richten Sie einen SSH-Tunnel zu einer Staging- oder Produktionsumgebung ein**:

1. Öffnen Sie ein Terminal.

1. Bereinigen Sie alle SSH-Sitzungen für jeden Webknoten des Clusters.

   ```bash
   ssh USERNAME@CLUSTER.ent.magento.cloud 'rm /run/platform/USERNAME/xdebug.sock'
   ```

1. Richten Sie den SSH-Tunnel für Xdebug für jeden Webknoten des Clusters ein.

   ```bash
   ssh -R /run/platform/USERNAME/xdebug.sock:localhost:9000 -N USERNAME@CLUSTER.ent.magento.cloud
   ```

**Starten des Debuggens mithilfe der Umgebungs-URL**:

1. Aktivieren Sie das Remote-Debugging. Besuchen Sie die Site im Browser und hängen Sie Folgendes an die URL an, wobei `KEY` für `xdebug_key` steht.

   ```http
   ?XDEBUG_SESSION_START=KEY
   ```

   In diesem Schritt wird das Cookie gesetzt, das Browseranforderungen an Trigger [!DNL Xdebug] sendet.

1. Schließen Sie das Debugging mit [!DNL Xdebug] ab.

1. Wenn Sie bereit sind, die Sitzung zu beenden, verwenden Sie den folgenden Befehl, um das Cookie zu entfernen und das Debugging über den Browser zu beenden, in dem `KEY` für `xdebug_key` Wert ist.

   ```http
   ?XDEBUG_SESSION_STOP=KEY
   ```

   >[!NOTE]
   >
   >Die `XDEBUG_SESSION_START`, die von `POST` -Anforderungen übergeben werden, werden nicht unterstützt.

## CLI-Befehle debuggen

Dieser Abschnitt erläutert das Debugging von CLI-Befehlen.

Debugging von CLI-Befehlen:

1. SSH in den Server, den Sie mit CLI-Befehlen debuggen möchten.

1. Erstellen Sie die folgenden Umgebungsvariablen:

   ```bash
   export XDEBUG_CONFIG='PHPSTORM'
   ```

   ```bash
   export PHP_IDE_CONFIG="serverName=<name of the server that is configured in PHPSTORM>"
   ```

   Diese Variablen werden entfernt, wenn die SSH-Sitzung beendet wird.

1. Debugging beginnen

   Führen Sie in Starterumgebungen und Pro-Integrationsumgebungen den CLI-Befehl zum Debuggen aus.
Sie können Laufzeitoptionen hinzufügen, beispielsweise:

   ```bash
   php -d xdebug.profiler_enable=On -d xdebug.max_nesting_level=9999 bin/magento cache:clean
   ```

   In Pro Staging- und Produktionsumgebungen müssen Sie beim Debugging von CLI-Befehlen den Pfad zur PHP-Konfigurationsdatei [!DNL Xdebug] angeben, z. B.:

   ```bash
   php -c /etc/platform/USERNAME/php.xdebug.ini bin/magento cache:clean
   ```

## Webanfragen debuggen

Die folgenden Schritte helfen Ihnen beim Debugging von Webanfragen.

1. Klicken Sie im Menü _Erweiterung_ auf **Debuggen** , um die Option zu aktivieren.

1. Klicken Sie mit der rechten Maustaste, wählen Sie das Optionsmenü aus und setzen Sie den IDE-Schlüssel auf **PHPSTORM**.

1. Installieren Sie den Client [!DNL Xdebug] im Browser. Konfigurieren und aktivieren Sie es.

### Beispiel: Chrome-Einrichtung

In diesem Abschnitt wird die Verwendung von [!DNL Xdebug] in Chrome mithilfe der [!DNL Xdebug] Helper-Erweiterung beschrieben. Informationen zu [!DNL Xdebug] -Tools für andere Browser finden Sie in der Browserdokumentation.

**So verwenden Sie Xdebug Helper mit Chrome**:

1. Erstellen Sie einen [SSH-Tunnel](#ssh-access-to-xdebug-environments) für den Cloud-Server.

1. Installieren Sie die [Xdebug Helper-Erweiterung](https://chromewebstore.google.com/detail/eadndfjplgieldjbigjakmdgkmoaaaoc) aus dem Chrome-Store.

1. Aktivieren Sie die Erweiterung in Chrome, wie in der folgenden Abbildung dargestellt.

   ![Aktivieren der Xdebug-Erweiterung in Chrome](../../assets/xdebug/enable-chrome-ext.png)

1. Klicken Sie in Chrome mit der rechten Maustaste auf das grüne Helper-Symbol in der Chrome-Symbolleiste.

1. Klicken Sie im Popup-Menü auf **Optionen**.

1. Klicken Sie in der Liste _IDE-Schlüssel_ auf **PhpStorm**.

1. Klicken Sie auf **Speichern**.

   ![Xdebug Helper options](../../assets/xdebug/helper-options.png)

1. Öffnen Sie Ihr PhpStorm-Projekt.

1. Klicken Sie in der oberen Navigationsleiste auf das Symbol **Listening starten** .

   Wenn die Navigationsleiste nicht angezeigt wird, klicken Sie auf **Ansicht** > **Navigationsleiste**.

1. Doppelklicken Sie im Navigationsfenster von PhpStorm auf die zu testende PHP-Datei.

## Lokalen Code debuggen

Aufgrund der schreibgeschützten Umgebungen müssen Sie Code aus einer Umgebung oder einer bestimmten Git-Verzweigung an die lokale Workstation ziehen, um das Debugging durchzuführen.

Die Methode, die Sie wählen, liegt bei Ihnen. Sie haben die folgenden Optionen:

- Checken Sie den Code aus Git aus und führen Sie `composer install` aus.

  Diese Methode funktioniert nur, wenn `composer.json` Pakete in privaten Repositorys referenziert, auf die Sie keinen Zugriff haben. Diese Methode führt dazu, dass die gesamte Adobe Commerce-Codebase abgerufen wird.

- Kopieren Sie die Verzeichnisse `vendor`, `app`, `pub`, `lib` und `setup`

  Diese Methode führt dazu, dass Sie sämtlichen Code haben, den Sie testen können. Je nachdem, wie viele statische Assets Sie haben, kann dies zu einer langen Übertragung mit einem großen Dateivolumen führen.

- Kopieren Sie nur den Ordner &quot;`vendor`&quot;

  Da sich der Großteil des Codes im Verzeichnis `vendor` befindet, führt diese Methode wahrscheinlich zu guten Tests, obwohl sie nicht die gesamte Codebasis testet.

**So komprimieren Sie Dateien und kopieren sie auf Ihren lokalen Computer**:

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

1. Komprimieren Sie die Dateien.

   ```bash
   tar -czf /tmp/<file-name>.tgz <directory list>
   ```

   Um beispielsweise nur den Ordner `vendor` zu komprimieren, gehen Sie folgendermaßen vor:

   ```bash
   tar -czf /tmp/vendor.tgz vendor
   ```

1. Verwenden Sie in Ihrer lokalen Umgebung PhpStorm, um die Dateien zu komprimieren.

   ```bash
   cd <phpstorm project root dir>
   ```

   ```bash
   rsync <SSH-URL>:/tmp/<file-name>.tgz .
   ```

   ```bash
   tar xzf <file-name>.tgz
   ```
