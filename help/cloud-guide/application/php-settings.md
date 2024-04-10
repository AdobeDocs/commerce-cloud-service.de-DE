---
title: PHP-Einstellungen
description: Erfahren Sie mehr über die optimalen PHP-Einstellungen für die Konfiguration von Commerce-Anwendungen in der Cloud-Infrastruktur.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 94c1e16a07567471d446478e3bd2a33977247ef3
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# PHP-Einstellungen

Sie können auswählen, welche [PHP-Version](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in Ihrem `.magento.app.yaml` Datei:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Wenn Sie auf PHP 8.1 und höher aktualisieren, entfernen Sie JSON aus dem [`runtime: extensions:` Eigenschaft](properties.md#runtime) in der `.magento.app.yaml` Dateien und erneut bereitstellen. Die JSON-Erweiterung wird seit PHP 8.0 in der Cloud-Umgebung installiert.

## Konfigurieren von PHP

Sie können die PHP-Einstellungen für Ihre Umgebung mit einem `php.ini` -Datei, die an die von Adobe Commerce verwaltete Konfiguration angehängt wird.

Fügen Sie in Ihrem Repository Folgendes hinzu: `php.ini` Datei in den Stamm der Anwendung (den Repository-Stamm).

>[!TIP]
>
>Die unsachgemäße Konfiguration von PHP-Einstellungen kann Probleme verursachen, sodass nur erweiterte Administratoren diese Optionen festlegen sollten.

### PHP-Speicherlimit erhöhen

Um die PHP-Speicherbegrenzung zu erhöhen, fügen Sie die folgende Einstellung zur `php.ini` Datei:

```ini
memory_limit = 1G
```

Erhöhen Sie zum Debuggen den Wert auf 2G.

### Optimieren der realpath_cache-Konfiguration

Legen Sie Folgendes fest `realpath_cache` Einstellungen zur Verbesserung der Anwendungsleistung.

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

Diese Einstellungen ermöglichen es PHP-Prozessen, Pfade zu Dateien zwischenzuspeichern, anstatt sie bei jedem Laden der Seite zu suchen. Siehe [Leistungsoptimierung](https://www.php.net/manual/en/ini.core.php) in der PHP-Dokumentation.

>[!NOTE]
>
>Eine Liste der empfohlenen PHP-Konfigurationseinstellungen finden Sie unter [Erforderliche PHP-Einstellungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) in der _Installationshandbuch_.

### Überprüfen der benutzerdefinierten PHP-Einstellungen

Nach dem Pushen der `php.ini` Wenn Sie Änderungen an Ihrer Cloud-Umgebung vornehmen, können Sie überprüfen, ob die benutzerdefinierte PHP-Konfiguration zu Ihrer Umgebung hinzugefügt wurde. Verwenden Sie beispielsweise SSH, um sich bei der Remote-Umgebung anzumelden und die Datei mit etwas Ähnlichem wie dem folgenden anzuzeigen:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Wenn Sie Cloud Docker for Commerce für die lokale Entwicklung verwenden, siehe [Docker-Service-Container](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) für Informationen zur Verwendung eines benutzerdefinierten `php.ini` Datei in einer Docker-Umgebung.

## Erweiterungen aktivieren

Sie können PHP-Erweiterungen in der `runtime:extension` -Abschnitt. Außerdem werden die angegebenen Erweiterungen in den Docker-PHP-Containern verfügbar.

>[!IMPORTANT]
>
>Bevor Sie Erweiterungen aktivieren, müssen Sie wissen, dass die PHP-Version mit dem Betriebssystem kompatibel sein muss, das das Projekt hostet. Bevor Sie fortfahren können, muss Ihre Projektumgebung möglicherweise vom Infrastruktur-Team auf das Betriebssystem aktualisiert werden.

Beispiel in `.magento.app.yaml` Datei:

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

Verwenden Sie SSH, um sich bei einer Umgebung anzumelden und die PHP-Erweiterungen aufzulisten.

```bash
php -m
```

Einzelheiten zu einer bestimmten PHP-Erweiterung finden Sie unter [PHP-Erweiterungsliste](https://www.php.net/manual/en/extensions.alphabetical.php).

Die folgende Tabelle zeigt die unterstützten PHP-Erweiterungen bei der Bereitstellung von Adobe Commerce auf der Cloud-Plattform.

{{$include /help/_includes/templated/php-extensions-cloud.md}}

Die PHP-Modulvoraussetzungen sind an die Adobe Commerce-Version gebunden. Siehe [PHP-Anforderungen](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Unterstützung von Erweiterungen

Für Pro-Projekte benötigen die folgenden Erweiterungen zusätzliche Unterstützung für die Installation:

- `sourceguardian`

Um beispielsweise PHP so einzurichten, dass nur SourceGuardian-geschützte Skripte in allen Umgebungen ausgeführt werden, muss die folgende Option in der `php.ini` Datei:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Siehe [Abschnitt 3.5 der SourceGuardian-Dokumentation](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Dies ist ein Link zu einer PDF_.

[Senden eines Adobe Commerce-Support-Tickets](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) um Hilfe bei der Installation dieser PHP-Erweiterungen in allen Produktionsumgebungen und Pro-Staging-Umgebungen zu erhalten. Einschließen der aktualisierten `.magento/services.yaml` -Datei, `.magento.app.yaml` -Datei mit der aktualisierten PHP-Version und allen zusätzlichen PHP-Erweiterungen. Bei Änderungen an einer Live-Produktionsumgebung müssen Sie mindestens 48 Stunden im Voraus angeben. Es kann bis zu 48 Stunden dauern, bis das Cloud-Infrastruktur-Team Ihr Projekt aktualisiert.

>[!WARNING]
>
>PHP, das mit debug kompiliert wurde, wird nicht unterstützt und der Probe kann mit Folgendem in Konflikt stehen [!DNL XDebug] oder [!DNL XHProf]. Deaktivieren Sie diese Erweiterungen, wenn Sie den Prüfpunkt aktivieren. Die Probe steht in Konflikt mit einigen PHP-Erweiterungen wie [!DNL Pinba] oder IonCube.
