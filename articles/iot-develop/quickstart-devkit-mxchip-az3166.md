---
title: 'Démarrage rapide : Connecter un appareil MXCHIP AZ3166 à Azure IoT Central'
description: Le logiciel intégré Azure RTOS permet de connecter un appareil MXCHIP AZ3166 à Azure IoT et d’envoyer des données de télémétrie.
author: timlt
ms.author: timlt
ms.service: iot-develop
ms.devlang: c
ms.topic: quickstart
ms.date: 03/17/2021
ms.openlocfilehash: 66ddc9f080383dac7703b00e62878df7714c4201
ms.sourcegitcommit: 17345cc21e7b14e3e31cbf920f191875bf3c5914
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "110061259"
---
# <a name="quickstart-connect-an-mxchip-az3166-devkit-to-iot-central"></a>Démarrage rapide : Connecter un devkit MXCHIP AZ3166 à IoT Central

**S’applique à** : [Développement d’appareils intégrés](about-iot-develop.md#embedded-device-development)<br>
**Durée totale d’exécution** : 30 minutes

[![Parcourir le code](media/common/browse-code.svg)](https://github.com/azure-rtos/getting-started/tree/master/MXChip/AZ3166)

Dans ce didacticiel, vous utilisez Azure RTOS pour connecter un DevKit IoT MXCHIP AZ3166 (ci-après, DevKit MXCHIP) à Azure IoT. Cet article fait partie de la série [Prise en main du développement d’appareils intégrés Azure IoT](quickstart-device-development.md). La série présente Azure RTOS aux développeurs d’appareils et explique la procédure de connexion de plusieurs kits d’évaluation d’appareil à Azure IoT.

Vous allez effectuer les étapes suivantes :

* Installer un ensemble d’outils de développement intégrés pour la programmation d’un DevKit MXCHIP en C
* Créer une image et la flasher sur le DevKit MXCHIP
* Azure IoT Central permet de créer des composants cloud, d’afficher les propriétés, d’afficher la télémétrie des appareils et d’appeler des commandes directes

## <a name="prerequisites"></a>Prérequis

* PC exécutant Microsoft Windows 10
* [Git](https://git-scm.com/downloads) pour cloner le référentiel
* Matériel

    > * [DevKit IoT MXCHIP AZ3166](https://aka.ms/iot-devkit) (DevKit MXCHIP)
    > * Wi-Fi 2,4 GHz
    > * USB 2.0, câble mâle-mâle micro USB

## <a name="prepare-the-development-environment"></a>Préparer l’environnement de développement

Avant de configurer votre environnement de développement, vous devez cloner un référentiel GitHub qui contient toutes les ressources dont vous avez besoin pour le didacticiel. Ensuite, vous installez un ensemble d’outils de programmation.

### <a name="clone-the-repo-for-the-tutorial"></a>Cloner le référentiel pour le didacticiel

Clonez le référentiel suivant pour télécharger tous les exemples de code d’appareil, les scripts d’installation et les versions hors connexion de la documentation. Si vous avez précédemment cloné ce référentiel dans un autre didacticiel, il n’est pas nécessaire de recommencer.

Pour cloner le référentiel, exécutez la commande suivante :

```shell
git clone --recursive https://github.com/azure-rtos/getting-started.git
```

### <a name="install-the-tools"></a>Installer les outils

Le référentiel cloné contient un script d’installation qui installe et configure les outils requis. Si vous avez installé ces outils dans un autre didacticiel dans le guide de prise en main, il n’est pas nécessaire de recommencer.

> [!NOTE]
> Le script d’installation installe les outils suivants :
> * [CMake](https://cmake.org) : générer
> * [ARM GCC](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm) : compiler
> * [Termite](https://www.compuphase.com/software_termite.htm) : surveiller la sortie du port série pour les appareils connectés

Pour installer les outils :

1. Dans l’Explorateur de fichiers, accédez au chemin d’accès suivant dans le référentiel et exécutez le script d’installation nommé *get-toolchain.bat* :

    > *getting-started\tools\get-toolchain.bat*

1. Après l’installation, ouvrez une nouvelle fenêtre de console pour identifier les modifications de configuration apportées par le script d’installation. Utilisez cette console pour effectuer les tâches de programmation restantes dans le didacticiel. Vous pouvez utiliser Windows CMD, PowerShell ou Git Bash pour Windows.
1. Exécutez le code suivant pour vérifier que CMake version 3.14 ou ultérieure est installé.

    ```shell
    cmake --version
    ```

[!INCLUDE [iot-develop-embedded-create-central-app-with-device](../../includes/iot-develop-embedded-create-central-app-with-device.md)]

## <a name="prepare-the-device"></a>Préparer l’appareil

Pour connecter le DevKit MXCHIP à Azure, vous allez modifier un fichier de configuration pour les paramètres Wi-Fi et Azure IoT, regénérer l’image et la flasher sur l’appareil.

### <a name="add-configuration"></a>Ajouter une configuration

1. Ouvrez le fichier suivant dans un éditeur de texte :

    > *getting-started\MXChip\AZ3166\app\azure_config.h*

1. Affectez aux constantes Wi-Fi les valeurs suivantes à partir de votre environnement local.

    |Nom de la constante|Valeur|
    |-------------|-----|
    |`WIFI_SSID` |{*Votre SSID Wi-Fi*}|
    |`WIFI_PASSWORD` |{*Votre mot de passe Wi-Fi*}|
    |`WIFI_MODE` |{*Une des valeurs de mode de Wi-Fi énumérées dans le fichier*}|

1. Définissez les constantes d’informations de l’appareil Azure IoT sur les valeurs que vous avez enregistrées après avoir créé les ressources Azure.

    |Nom de la constante|Valeur|
    |-------------|-----|
    |`IOT_DPS_ID_SCOPE` |{*Valeur d’étendue de votre ID*}|
    |`IOT_DPS_REGISTRATION_ID` |{*Valeur d’ID de votre appareil*}|
    |`IOT_DEVICE_SAS_KEY` |{*Valeur de votre clé primaire*}|

1. Enregistrez et fermez le fichier.

### <a name="build-the-image"></a>Créer l’image

Dans votre console ou dans l’Explorateur de fichiers, exécutez le script *rebuild.bat* à l’emplacement suivant pour générer l’image :

> *getting-started\MXChip\AZ3166\tools\rebuild.bat*

Une fois la génération terminée, vérifiez que le fichier binaire a été créé dans le chemin d’accès suivant :

> *getting-started\MXChip\AZ3166\build\app\mxchip_azure_iot.bin*

### <a name="flash-the-image"></a>Flasher l’image

1. Dans le DevKit MXCHIP, recherchez le bouton **Réinitialiser** et le port micro USB. Vous pouvez utiliser ces composants dans les étapes suivantes. Les deux sont mis en surbrillance dans l’image suivante :

    :::image type="content" source="media/quickstart-devkit-mxchip-az3166/mxchip-iot-devkit.png" alt-text="Localiser les composants clés sur la carte du DevKit MXChip":::

1. Branchez le câble micro USB au port micro USB du DevKit MXCHIP, puis branchez-le à votre ordinateur.
1. Dans l’Explorateur de fichiers, recherchez le fichier binaire que vous avez créé dans la section précédente.
1. Copiez le fichier binaire *mxchip_azure_iot. bin*.
1. Dans l’Explorateur de fichiers, recherchez l’appareil DevKit MXCHIP connecté à votre ordinateur. L’appareil apparaît en tant que lecteur sur votre système avec l’intitulé de lecteur **AZ3166**.
1. Collez le fichier binaire dans le dossier racine du DevKit MXCHIP. Le processus de flash démarre automatiquement et se termine en quelques secondes.

    > [!NOTE]
    > Au cours de ce processus, un voyant vert s’allume pour le DevKit MXCHIP.

### <a name="confirm-device-connection-details"></a>Vérifier les détails de connexion de l’appareil

Vous pouvez utiliser l’application **Termite** pour surveiller la communication et vérifier que votre appareil est correctement configuré.

1. Démarrez **Termite**.
    > [!TIP]
    > Si vous ne parvenez pas à connecter Termite à votre devkit, installez le [pilote ST-LINK](https://my.st.com/content/ccc/resource/technical/software/driver/files/stsw-link009.zip), puis réessayez. Pour obtenir des étapes supplémentaires, consultez [Résolution des problèmes](https://github.com/azure-rtos/getting-started/blob/master/docs/troubleshooting.md).
1. Sélectionnez **Paramètres**.
1. Dans la boîte de dialogue **Paramètres du port série**, vérifiez les paramètres suivants et mettez à jour si nécessaire :
    * **Vitesse (en bauds)**  : 115 200
    * **Port** : port auquel votre DevKit MXCHIP est connecté. Si plusieurs options de port sont disponibles dans la liste déroulante, vous pouvez trouver le port approprié à utiliser. Ouvrez le **Gestionnaire d'appareils** Windows et affichez les **Ports** pour identifier le port à utiliser.

    :::image type="content" source="media/quickstart-devkit-mxchip-az3166/termite-settings.png" alt-text="Vérifier les paramètres de l’application Termite":::

1. Sélectionnez OK.
1. Appuyez sur le bouton **Réinitialiser** de l’appareil. Le bouton est étiqueté sur l’appareil et situé près du connecteur micro USB.
1. Dans l’application **Termite**, vérifiez les valeurs de point de contrôle suivantes pour confirmer que l’appareil est initialisé et connecté à Azure IoT.

    ```output
    Starting Azure thread

    Initializing WiFi
        Connecting to SSID 'iot'
    SUCCESS: WiFi connected to iot

    Initializing DHCP
        IP address: 10.0.0.123
        Mask: 255.255.255.0
        Gateway: 10.0.0.1
    SUCCESS: DHCP initialized

    Initializing DNS client
        DNS address: 10.0.0.1
    SUCCESS: DNS client initialized

    Initializing SNTP client
        SNTP server 0.pool.ntp.org
        SNTP IP address: 185.242.56.3
        SNTP time update: Nov 16, 2020 23:47:35.385 UTC 
    SUCCESS: SNTP initialized

    Initializing Azure IoT DPS client
        DPS endpoint: global.azure-devices-provisioning.net
        DPS ID scope: ***
        Registration ID: ***
    SUCCESS: Azure IoT DPS client initialized

    Initializing Azure IoT Hub client
        Hub hostname: ***
        Device id: ***
        Model id: dtmi:azurertos:devkit:gsgmxchip;1
    Connected to IoTHub
    SUCCESS: Azure IoT Hub client initialized

    Starting Main loop
    ```

Laissez Termite ouvert pour surveiller la sortie de l’appareil dans les étapes suivantes.

## <a name="verify-the-device-status"></a>Vérifier l’état de l’appareil

Pour consulter l’état de l’appareil dans le portail IoT Central :
1. Dans le tableau de bord de l’application, sélectionnez **Appareils** dans le menu de navigation latéral.
1. Vérifiez que l’**état de l'appareil** est mis à jour en **approvisionné**.
1. Vérifiez que le **modèle d’appareil** est mis à jour en **Guide de prise en main**.

    :::image type="content" source="media/quickstart-devkit-mxchip-az3166/iot-central-device-view-status.png" alt-text="Consulter l’état de l’appareil dans IoT Central":::

## <a name="view-telemetry"></a>Afficher les données de télémétrie

Avec IoT Central, vous pouvez afficher le flux de télémétrie de votre appareil dans le cloud.

Pour afficher la télémétrie dans le portail IoT Central :

1. Dans le tableau de bord de l’application, sélectionnez **Appareils** dans le menu de navigation latéral.
1. Sélectionnez l’appareil dans la liste.
1. Affichez la télémétrie lorsque l’appareil envoie des messages au cloud sous l’onglet **Vue d’ensemble**.

    :::image type="content" source="media/quickstart-devkit-mxchip-az3166/iot-central-device-telemetry.png" alt-text="Afficher la télémétrie de l’appareil dans IoT Central":::

    > [!NOTE]
    > Vous pouvez également surveiller la télémétrie à partir de l’appareil à l’aide de l’application Termite.

## <a name="call-a-direct-method-on-the-device"></a>Appeler une méthode directe sur l’appareil

Vous pouvez également utiliser IoT Central pour appeler une méthode directe que vous avez implémentée sur votre appareil. Les méthodes directes portent un nom et peuvent éventuellement avoir une charge utile JSON, une connexion configurable et un délai d’expiration de méthode. Dans cette section, vous appelez une méthode qui vous permet d’activer ou de désactiver un voyant.

Pour appeler une méthode dans le portail IoT Central :

1. Sélectionnez l’onglet **Commande** sur la page de l’appareil.
1. Sélectionnez **État**, puis **Exécuter**.  Le voyant doit s’allumer.

    :::image type="content" source="media/quickstart-devkit-mxchip-az3166/iot-central-invoke-method.png" alt-text="Appeler une méthode directe sur un appareil":::

1. Désélectionnez **État** et sélectionnez **Exécuter**. Le voyant doit s’éteindre.

## <a name="view-device-information"></a>Affichage des informations sur l’appareil

Vous pouvez afficher les informations de l’appareil à partir d’IoT Central.

Sélectionnez l’onglet **À propos de** sur la page de l’appareil.

:::image type="content" source="media/quickstart-devkit-mxchip-az3166/iot-central-device-about.png" alt-text="Afficher des informations sur l’appareil dans IoT Central":::

## <a name="debugging"></a>Débogage

Pour déboguer l’application, consultez [Débogage avec Visual Studio Code](https://github.com/azure-rtos/getting-started/blob/master/docs/debugging.md).

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous n’avez plus besoin des ressources Azure créées dans ce didacticiel, vous pouvez les supprimer du portail IoT Central. Éventuellement, si vous poursuivez avec un autre didacticiel de ce guide Prise en main, vous pouvez conserver les ressources que vous avez déjà créées et les réutiliser.

Pour supprimer la totalité de l’exemple d’application Azure IoT Central et tous ses appareils et ressources :
1. Sélectionnez **Administration** > **Votre application**.
1. Sélectionnez **Supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez créé une image personnalisée qui contient un exemple de code Azure RTOS, puis vous avez flashé l’image sur l’appareil DevKit MXCHIP. Vous avez également utilisé le portail IoT Central pour créer des ressources Azure, connecter DevKit MXCHIP en toute sécurité à Azure, afficher la télémétrie et envoyer des messages.

* Pour les développeurs d’appareils, l’étape suggérée suivante consiste à voir les autres didacticiels de la série [Prise en main du développement d’appareils intégrés Azure IoT](quickstart-device-development.md).
* Si vous rencontrez des problèmes lors de l’initialisation ou de la connexion de votre appareil après avoir exécuté les procédures décrites dans ce guide, consultez [Résolution des problèmes](https://github.com/azure-rtos/getting-started/blob/master/docs/troubleshooting.md).
* Pour en savoir plus sur l’utilisation des composants Azure RTOS dans l’exemple de code pour ce didacticiel, consultez [Utilisation d’Azure RTOS dans le guide Prise en main](https://github.com/azure-rtos/getting-started/blob/master/docs/using-azure-rtos.md).

    > [!IMPORTANT]
    > Azure RTOS fournit aux fabricants OEM les composants permettant de sécuriser la communication et de créer du code et l’isolation des données à l’aide des mécanismes sous-jacents de protection matérielle MCU/MPU. Toutefois, chaque fabricant OEM est tenu de garantir que son appareil répond aux exigences de sécurité en constante évolution.

