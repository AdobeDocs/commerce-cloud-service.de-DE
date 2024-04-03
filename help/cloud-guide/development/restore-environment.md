---
title: Wiederherstellen einer Umgebung
description: Erfahren Sie, wie Sie die Adobe Commerce-Anwendung aus einem Cloud-Infrastrukturprojekt deinstallieren und eine Umgebung in einen stabilen Zustand zurückführen.
role: Developer
topic: Development
exl-id: b76bd6c3-986e-4adc-abd0-5b27db0d8a3b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Wiederherstellen einer Umgebung

Wenn Sie in der Integrationsumgebung auf Probleme stoßen und keine [gültige Sicherung](../storage/snapshots.md)versuchen Sie, Ihre Umgebung mit einer der folgenden Methoden wiederherzustellen:

- Zurücksetzen oder Zurücksetzen des Codes in der Git-Verzweigung
- Deinstallieren Sie die [!DNL Commerce] Applikation
- Neuerstellung erzwingen
- Datenbank manuell zurücksetzen

{{stuck-deployment-tip}}

## Git-Verzweigung zurücksetzen

Wenn Sie Ihre Git-Verzweigung zurücksetzen, wird der Code in der Vergangenheit wieder in einen stabilen Status versetzt.

**So setzen Sie die Verzweigung zurück**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Überprüfen Sie den Git-Commitverlauf. Verwendung `--oneline` um abgekürzte Commits in einer Zeile anzuzeigen:

   ```bash
   git log --oneline
   ```

   Beispielantwort:

   ```terminal
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Wählen Sie einen Commit-Hash, der den letzten bekannten stabilen Status Ihres Codes darstellt.

   Um Ihren Zweig auf seinen ursprünglichen initialisierten Status zurückzusetzen, suchen Sie den ersten Commit, der Ihren Zweig erstellt hat. Sie können `--reverse` um den Verlauf in umgekehrter chronologischer Reihenfolge anzuzeigen.

1. Verwenden Sie die Option zum Zurücksetzen der Festplatte, um Ihren Zweig zurückzusetzen. Seien Sie vorsichtig mit diesem Befehl, da er alle Änderungen seit dem ausgewählten Commit verwirft.

   ```bash
   git reset --hard <commit>
   ```

1. Übertragen Sie Ihre Änderungen in den Trigger einer Neuimplementierung, die Adobe Commerce erneut installiert.

   ```bash
   git push --force <origin> <branch>
   ```

## Commerce deinstallieren

Deinstallieren der [!DNL Commerce] Die Anwendung kehrt Ihre Umgebung in den Originalzustand zurück, indem sie die Datenbank wiederherstellt, die Bereitstellungskonfiguration entfernt und die `var/` Unterverzeichnisse. Durch diese Anleitung wird auch Ihre Git-Verzweigung in einen früheren stabilen Zustand zurückgesetzt. Wenn Sie keine kürzlich erstellte Sicherung haben, aber über SSH auf die Remote-Umgebung zugreifen können, führen Sie die folgenden Schritte aus, um Ihre Umgebung wiederherzustellen:

- Konfigurationsverwaltung deaktivieren
- Adobe Commerce deinstallieren
- Git-Verzweigung zurücksetzen

Durch das Deinstallieren der Adobe Commerce-Software wird die Datenbank gelöscht, die Bereitstellungskonfiguration entfernt und die `var/` Unterverzeichnisse. Es ist wichtig zu deaktivieren [Konfigurationsverwaltung](../store/store-settings.md) damit die vorherigen Konfigurationseinstellungen während der nächsten Bereitstellung nicht automatisch angewendet werden. Stellen Sie sicher, dass Ihr `app/etc/` enthält nicht die `config.php` -Datei.

**Deinstallation der Adobe Commerce-Software**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Entfernen Sie die Konfigurationsdatei.
   - Für Adobe Commerce 2.2 und höher:

     ```bash
     rm app/etc/config.php
     ```

   - Für Adobe Commerce 2.1:

     ```bash
     rm app/etc/config.local.php
     ```

1. Deinstallieren Sie die Adobe Commerce-Anwendung.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Vergewissern Sie sich, dass Adobe Commerce erfolgreich deinstalliert wurde.

   Die folgende Meldung wird angezeigt, um eine erfolgreiche Deinstallation zu bestätigen:

   ```terminal
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Löschen Sie die `var/` Unterverzeichnisse.

   ```bash
   rm -rf var/*
   ```

1. Melden Sie sich ab.

>[!TIP]
>
>Optional ist es empfehlenswert, Build-Caches zu bereinigen.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Neuerstellung erzwingen

Wenn Sie versucht haben, Adobe Commerce zu deinstallieren und Ihre Bereitstellung weiterhin fehlschlägt, können Sie versuchen, eine manuelle Implementierung zu erzwingen.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## Datenbank zurücksetzen

Wenn Sie versucht haben, Adobe Commerce zu deinstallieren, der Befehl fehlgeschlagen ist oder nicht abgeschlossen werden konnte, können Sie die Datenbank manuell zurücksetzen.

**Zurücksetzen der Datenbank**:

1. Wechseln Sie auf Ihrer lokalen Workstation zum Projektverzeichnis.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Stellen Sie eine Verbindung zur Datenbank her.

   ```bash
   mysql -h database.internal
   ```

1. Legen Sie die `main` Datenbank.

   ```shell
   drop database main;
   ```

1. Leere erstellen `main` Datenbank.

   ```shell
   create database main;
   ```

1. Löschen Sie die folgenden Konfigurationsdateien.

   - `config.php`
   - `config.php.bak`
   - `env.php`
   - `env.php.bak`

1. Melden Sie sich ab und Trigger einer Neuimplementierung.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
