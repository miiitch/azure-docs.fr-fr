---
title: Fichier include
description: Fichier include
author: timlt
ms.service: iot-develop
ms.topic: include
ms.date: 05/05/2021
ms.author: timlt
ms.custom: include file
ms.openlocfilehash: 9544e662fde8f39303ea8bbafd7556d9e3b5af07
ms.sourcegitcommit: 38d81c4afd3fec0c56cc9c032ae5169e500f345d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2021
ms.locfileid: "109518271"
---
## <a name="prerequisites"></a>Prérequis
- Si vous n’avez pas d’abonnement Azure, [créez-en un gratuitement](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.
- [Git](https://git-scm.com/downloads).
- [Node.js](https://nodejs.org) version 10 ou ultérieure. Pour vérifier la version de Node, exécutez `node --version`.
- Azure CLI. Vous avez le choix entre deux options pour exécuter les commandes Azure CLI dans ce guide de démarrage rapide :
    - Utilisez Azure Cloud Shell, interpréteur de commandes interactif qui exécute des commandes CLI dans votre navigateur. Cette option est recommandée, car vous n’avez pas besoin d’installer quoi que ce soit. Si vous utilisez Cloud Shell pour la première fois, connectez-vous au [portail Azure](https://portal.azure.com). Suivez les étapes décrites dans [Démarrage rapide de Cloud Shell](/azure/cloud-shell/quickstart) pour **démarrer Cloud Shell** et **sélectionner l’environnement Bash**.
    - Si vous le souhaitez, exécutez Azure CLI sur votre ordinateur local. Ce guide de démarrage rapide requiert Azure CLI version 2.0.76 ou ultérieure. Pour vérifier la version, exécutez `az --version`. Suivez les étapes décrites dans [Installer Azure CLI]( /cli/azure/install-azure-cli) pour installer ou mettre à niveau Azure CLI, l’exécuter et vous connecter. Si vous y êtes invité, installez les extensions Azure CLI lors de la première utilisation.

[!INCLUDE [iot-hub-include-create-hub-cli](iot-hub-include-create-hub-cli.md)]

## <a name="run-a-simulated-device"></a>Exécuter un appareil simulé
Dans cette section, vous allez utiliser le Kit de développement logiciel (SDK) Node.js pour envoyer des messages de votre appareil simulé à votre hub IoT. 

1. Ouvrez une nouvelle fenêtre de console. Vous allez utiliser cette console pour installer le kit SDK Node.js et travailler avec un exemple de code Node.js. Vous devez maintenant avoir deux fenêtres de console ouvertes : celle que vous venez d’ouvrir et la console Cloud Shell ou CLI que vous avez utilisée précédemment pour entrer les commandes CLI.

1. Dans votre console Node, clonez les [exemples du kit SDK Node.js d’appareil Azure IoT](https://github.com/Azure/azure-iot-sdk-node/tree/master/device/samples) sur votre ordinateur local :

    ```console
    git clone https://github.com/Azure/azure-iot-sdk-node
    ```

1. Accédez au répertoire *azure-iot-sdk-node/device/samples/pnp* :

    ```console
    cd azure-iot-sdk-node/device/samples/pnp
    ```

1. Installez le Kit de développement logiciel (SDK) Azure IoT Node.js et les dépendances nécessaires :

    ```console
    npm install
    ```

    Cette commande installe les dépendances appropriées comme spécifié dans le fichier *package.json* du répertoire des exemples d’appareils.

1. Définissez les deux variables d’environnement suivantes pour permettre à votre appareil simulé de se connecter à Azure IoT.
    * Définissez une variable d’environnement appelée `IOTHUB_DEVICE_CONNECTION_STRING`. Pour la valeur de la variable, utilisez la chaîne de connexion de l’appareil que vous avez enregistrée dans la section précédente.
    * Définissez une variable d’environnement appelée `IOTHUB_DEVICE_SECURITY_TYPE`. Pour la variable, utilisez la valeur de chaîne littérale `connectionString`.

    **Windows (cmd)**

    ```console
    set IOTHUB_DEVICE_CONNECTION_STRING=<your connection string here>
    set IOTHUB_DEVICE_SECURITY_TYPE=connectionString
    ```

    > [!NOTE]
    > Pour Windows CMD, il n’y a pas de guillemets avant et après les valeurs de chaîne pour chaque variable.

    **PowerShell**

    ```azurepowershell
    $env:IOTHUB_DEVICE_CONNECTION_STRING='<your connection string here>'
    $env:IOTHUB_DEVICE_SECURITY_TYPE='connectionString'
    ```

    **Bash (Linux ou Windows)**

    ```bash
    export IOTHUB_DEVICE_CONNECTION_STRING="<your connection string here>"
    export IOTHUB_DEVICE_SECURITY_TYPE="connectionString"
    ```
1. Dans votre application CLI, exécutez la commande [az iot hub monitor-events](/cli/azure/iot/hub#az_iot_hub_monitor_events) pour commencer à surveiller les événements sur votre appareil IoT simulé.  Les messages d’événement seront imprimés dans le terminal au fur et à mesure de leur arrivée.

    ```azurecli-interactive
    az iot hub monitor-events --output table --hub-name {YourIoTHubName}
    ```

1. Dans votre console Node, exécutez le code de l’exemple de fichier suivant. Ce code accède à l’appareil IoT simulé et envoie un message au hub IoT.

    Pour exécuter l’exemple Node.js à partir du terminal :
    ```console
    node pnpTemperatureController.js
    ```
    > [!NOTE]
    > Cet exemple de code utilise Azure IoT Plug-and-Play, qui vous permet d’intégrer des appareils intelligents dans vos solutions sans aucune configuration manuelle.  Par défaut, la plupart des exemples de cette documentation utilisent IoT Plug-and-Play. Pour en savoir plus sur les avantages et les cas d’utilisation d’IoT PnP, consultez [Qu’est ce qu’IoT Plug-and-Play ?](../articles/iot-pnp/overview-iot-plug-and-play.md).

Lorsque le code Node.js envoie un message simulé de télémétrie de votre appareil au hub IoT, le message s’affiche dans votre application CLI qui surveille les événements :

```output
Starting event monitor, use ctrl-c to stop...
event:
  component: thermostat1
  interface: dtmi:com:example:TemperatureController;2
  module: ''
  origin: myDevice
  payload:
    temperature: 70.5897683228018

event:
  component: thermostat2
  interface: dtmi:com:example:TemperatureController;2
  module: ''
  origin: myDevice
  payload:
    temperature: 52.87582619316418
```

Votre appareil est maintenant connecté en toute sécurité et envoie des données de télémétrie à Azure IoT Hub.