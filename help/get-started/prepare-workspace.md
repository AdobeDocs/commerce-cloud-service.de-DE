---
title: Vorbereitungen für die Entwicklung
description: Erfassen Sie Anmeldeinformationen und erfahren Sie mehr über die Tools, die zum Einrichten eines Entwicklungsarbeitsbereichs für die Verwendung mit Ihrem Commerce on Cloud-Infrastrukturprojekt verfügbar sind.
recommendations: noDisplay, catalog
exl-id: 8f88161f-3580-453b-b977-2c6e3824cc02
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Vorbereitungen für die Entwicklung

Unabhängig davon, ob Sie neu bei Commerce sind oder bereits Commerce-Besitzer sind und zur Cloud-Infrastruktur wechseln, sollten Sie diese Schritte zum Vorbereiten eines Entwicklungsarbeitsbereichs für Ihr Cloud-Projekt verwenden. Wenn Sie einige dieser Schritte bereits durchgeführt haben oder bereits über eine Adobe Commerce-Entwicklungsumgebung verfügen, überprüfen Sie die folgenden Ergebnisse, und fahren Sie mit dem nächsten Schritt fort. Einige Konfigurationen und Workflows unterscheiden sich von einer typischen lokalen Installation.

## Anmeldeinformationen

Bevor Sie einen Arbeitsbereich einrichten, sammeln Sie die folgenden Schlüssel und den Kontozugriff:

- **Authentifizierungsschlüssel (Composer-Schlüssel)**

  Authentifizierungsschlüssel sind 32-stellige Authentifizierungstoken, die sicheren Zugriff auf das Adobe Commerce Composer-Repository (`repo.magento.com`) und alle anderen Git-Dienste bieten, die für die Anwendungsentwicklung erforderlich sind, z. B. GitHub. Ihr Konto kann über mehrere Authentifizierungsschlüssel verfügen. Beginnen Sie bei der Einrichtung des Arbeitsbereichs mit einem bestimmten Schlüssel für Ihr Code-Repository. Wenn Sie keine Schlüssel haben, wenden Sie sich an den Projekteigentümer oder erstellen Sie die [Authentifizierungsschlüssel](../cloud-guide/development/authentication-keys.md) selbst.

- **Cloud-Projekt-Konto**

  Der Projektinhaber sollte Sie zum Adobe Commerce-Projekt für Cloud-Infrastruktur einladen. Wenn Sie die Einladung per E-Mail erhalten, klicken Sie auf den Link und befolgen Sie die Anweisungen zum Erstellen Ihres Kontos. Siehe [Onboarding](onboarding.md).

- **Adobe Commerce-Verschlüsselungsschlüssel**

  Wenn Sie nur ein vorhandenes System importieren, erfassen Sie den Verschlüsselungsschlüssel, der zum Schutz Ihres Zugriffs und Ihrer Daten für die Datenbank verwendet wird. Weitere Informationen zu diesem Schlüssel finden Sie unter [Beheben von Problemen mit dem Verschlüsselungsschlüssel](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Entwicklertools

- **Installieren der Cloud-CLI**

  Installieren Sie die CLI `magento-cloud` , damit Sie Cloud-Umgebungen verwalten und Automatisierungsaufgaben ausführen können. Installationsanweisungen finden Sie unter [Cloud CLI](../cloud-guide/dev-tools/cloud-cli-overview.md) .

- **Docker für lokale Entwicklung und Tests installieren**

  Optional können Sie die Docker-Umgebung verwenden, um die Commerce-Umgebung in der Cloud-Infrastruktur-Umgebung `integration` für die lokale Entwicklung zu emulieren. Es gibt drei wesentliche Komponenten: eine Adobe Commerce v2-Vorlage, Docker Compose und das `ece-tools` -Paket.

   - [Docker-Architektur und allgemeine Befehle](../cloud-guide/dev-tools/cloud-docker.md)
   - [Launch-Docker-Entwicklungsumgebung](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
   - [ECE-Tools-Paket](../cloud-guide/dev-tools/package-overview.md)

- **Git-basierte Dienste integrieren**

  Optional können Sie einen Git-basierten Hosting-Dienst wie GitHub oder GitLab in Adobe Commerce in die Cloud-Infrastruktur integrieren. Siehe [Integrationen](../cloud-guide/integrations/overview.md).

## Projektcode

Eine sichere Verbindung ist für die Interaktion mit den Remote-Umgebungen unerlässlich. Melden Sie sich bei einem neuen Projekt [ bei  [!DNL Cloud Console]](https://console.adobecommerce.com) an und klicken Sie auf **[!UICONTROL No SSH key]**. Dieses Symbol befindet sich rechts neben dem Befehlsfeld und ist sichtbar, wenn das Projekt keinen SSH-Schlüssel enthält. Siehe [Sichere Verbindungen](../cloud-guide/development/secure-connections.md#add-an-ssh-public-key-to-your-account).

**So klonen Sie Ihre Codebase auf Ihrer lokalen Workstation**:

1. Klicken Sie im Tab [[!DNL Cloud Console]](https://console.adobecommerce.com) auf **[!UICONTROL code]** und wählen Sie die Registerkarte **[!UICONTROL Git]** aus.

   ![Klonen Sie Ihren Code](../assets/ui-git-code.png){width="450"}

1. Kopieren Sie den bereitgestellten Befehl `git clone ...` .

1. Erstellen und ändern Sie in einem Terminal das Arbeitsverzeichnis.

1. Fügen Sie den Befehl `git clone ...` ein und führen Sie ihn aus.

>[!TIP]
>
>Adobe stellt Ihre ursprüngliche Projektumgebung mithilfe eines Vorlagen-Repositorys bereit, das Paketanweisungen für eine bestimmte Version von Adobe Commerce enthält. Lesen Sie das Thema [Projektdateistruktur](../cloud-guide/project/file-structure.md) und erfahren Sie mehr über wichtige Projektdateien und Cloud-Vorlagen.
