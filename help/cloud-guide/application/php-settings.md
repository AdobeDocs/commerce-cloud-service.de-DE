---
title: PHP-Einstellungen
description: Erfahren Sie mehr über die optimalen PHP-Einstellungen für die Commerce-Anwendungskonfiguration in der Cloud-Infrastruktur.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 9d20cd11e541d343af158eb3eadcf641fb2751bd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# PHP-Einstellungen

Sie können wählen, welche [Version von PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in Ihrer `.magento.app.yaml`-Datei ausgeführt werden soll:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Wenn Sie auf PHP 8.1 und höher aktualisieren, entfernen Sie JSON aus der [`runtime: extensions:`-Eigenschaft](properties.md#runtime) in der Datei `.magento.app.yaml` und stellen Sie es erneut bereit. Die JSON-Erweiterung wird seit PHP 8.0 in der Cloud-Umgebung installiert.

## PHP konfigurieren

Sie können die PHP-Einstellungen für Ihre Umgebung mithilfe einer `php.ini` -Datei anpassen, die an die von Adobe Commerce verwaltete Konfiguration angehängt ist.

Fügen Sie in Ihrem Repository die Datei `php.ini` zum Stammverzeichnis der Anwendung (dem Repository-Stammordner) hinzu.

>[!TIP]
>
>Fehlerhaftes Konfigurieren von PHP-Einstellungen kann Probleme verursachen, daher sollten nur fortgeschrittene Administratoren diese Optionen festlegen.

### PHP-Speicherbegrenzung erhöhen

Um die PHP-Speicherbegrenzung zu erhöhen, fügen Sie die folgende Einstellung zur Datei `php.ini` hinzu:

```ini
memory_limit = 1G
```

Erhöhen Sie zum Debugging den Wert auf 2G.

### Optimieren der realpath_cache-Konfiguration

Legen Sie die folgenden `realpath_cache` -Einstellungen fest, um die Anwendungsleistung zu verbessern.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Diese Einstellungen ermöglichen es PHP-Prozessen, Pfade zu Dateien zwischenzuspeichern, anstatt sie für jedes Laden der Seite zu suchen. Siehe [Leistungsoptimierung](https://www.php.net/manual/en/ini.core.php) in der PHP-Dokumentation.

>[!NOTE]
>
>Eine Liste der empfohlenen PHP-Konfigurationseinstellungen finden Sie unter [Erforderliche PHP-Einstellungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) im _Installationshandbuch_.

### Benutzerdefinierte PHP-Einstellungen überprüfen

Nachdem Sie die `php.ini`-Änderungen an Ihre Cloud-Umgebung gepusht haben, können Sie überprüfen, ob die benutzerdefinierte PHP-Konfiguration zu Ihrer Umgebung hinzugefügt wurde. Verwenden Sie beispielsweise SSH, um sich bei der Remote-Umgebung anzumelden und die Datei mit einer ähnlichen Funktion anzuzeigen:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Wenn Sie Cloud Docker für Commerce für die lokale Entwicklung verwenden, finden Sie unter [Docker-Dienstcontainer](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) Informationen zur Verwendung einer benutzerdefinierten `php.ini` -Datei in einer Docker-Umgebung.

## Erweiterungen aktivieren

Sie können PHP-Erweiterungen im Abschnitt `runtime:extension` aktivieren oder deaktivieren. Außerdem werden die angegebenen Erweiterungen in den Docker PHP-Containern verfügbar.

>[!IMPORTANT]
>
>Vor der Aktivierung von Erweiterungen ist es wichtig zu verstehen, dass die PHP-Version mit dem Betriebssystem kompatibel sein muss, das das Projekt hostet. Ihre Projektumgebung erfordert möglicherweise eine Aktualisierung des Betriebssystems durch das Infrastrukturteam, bevor Sie fortfahren können.

Beispiel in der Datei `.magento.app.yaml` :

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Verwenden Sie SSH, um sich in einer Umgebung anzumelden und die PHP-Erweiterungen aufzulisten.

```bash
php -m
```

Weitere Informationen zu einer bestimmten PHP-Erweiterung finden Sie in der [PHP-Erweiterungsliste](https://www.php.net/manual/en/extensions.alphabetical.php).

Die folgende Tabelle zeigt die unterstützten PHP-Erweiterungen bei der Bereitstellung von Adobe Commerce auf der Cloud-Plattform.

{{$include /help/_includes/templated/php-extensions-cloud.md}}

Die Anforderungen an PHP-Module sind an die Adobe Commerce-Version gebunden. Siehe [PHP-Anforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Erweiterungsunterstützung

Für Pro-Projekte benötigen die folgenden Erweiterungen zusätzliche Unterstützung für die Installation:

- `ioncube`
- `sourceguardian`

Um beispielsweise PHP so einzurichten, dass nur SourceGuardian-geschützte Skripte in allen Umgebungen ausgeführt werden, muss die folgende Option in der Datei `php.ini` festgelegt sein:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Siehe [Abschnitt 3.5 der SourceGuardian-Dokumentation](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Dies ist ein Link zu einer PDF_.

[Senden Sie ein Adobe Commerce Support-Ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) , um Hilfe bei der Installation dieser PHP-Erweiterungen in allen Produktionsumgebungen und Pro Staging-Umgebungen zu erhalten. Fügen Sie Ihre aktualisierte `.magento/services.yaml`-Datei, `.magento.app.yaml`-Datei mit der aktualisierten PHP-Version und weiteren PHP-Erweiterungen ein. Für Änderungen an einer Live-Produktionsumgebung müssen Sie eine Vorankündigung von mindestens 48 Stunden angeben. Es kann bis zu 48 Stunden dauern, bis das Cloud-Infrastruktur-Team Ihr Projekt aktualisiert.

>[!WARNING]
>
>PHP, das mit debug kompiliert wurde, wird nicht unterstützt und die Probe kann mit [!DNL XDebug] oder [!DNL XHProf] in Konflikt geraten. Deaktivieren Sie diese Erweiterungen beim Aktivieren der Probe. Die Probe steht in Konflikt mit einigen PHP-Erweiterungen wie [!DNL Pinba] oder IonCube.
