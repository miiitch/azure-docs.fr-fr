---
title: Tutoriel pour configurer les paramètres d’appareil, de mise à jour et horaires d’un appareil Azure Stack Edge Mini R dans le portail Azure
description: Ce tutoriel sur le déploiement d’Azure Stack Edge Mini R vous apprend à configurer les paramètres d’appareil, de mise à jour et horaires de votre appareil physique.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 10/14/2020
ms.author: alkohli
ms.openlocfilehash: 5dd37351295d45944ee2ed273a7acef44ed32865
ms.sourcegitcommit: 73fb48074c4c91c3511d5bcdffd6e40854fb46e5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106065546"
---
# <a name="tutorial-configure-the-device-settings-for-azure-stack-edge-mini-r"></a>Tutoriel : Configurer les paramètres d’appareil pour Azure Stack Edge Mini R

Ce tutoriel explique comment configurer les paramètres d’appareil de votre appareil Azure Stack Edge Mini R avec GPU intégré. Vous pouvez configurer le nom de votre appareil, le serveur de mise à jour et le serveur de temps via l’interface utilisateur web locale.

La configuration de l’appareil peut prendre environ 5 à 7 minutes.

Ce tutoriel vous fournira des informations sur :

> [!div class="checklist"]
>
> * Prérequis
> * Configurer les paramètres des appareils
> * Configurer la mise à jour 
> * Configurer l’heure

## <a name="prerequisites"></a>Prérequis

Avant de configurer les paramètres liés aux appareils sur votre appareil Azure Stack Edge Mini R avec GPU, vérifiez les éléments suivants :

* Pour votre appareil physique :

    - Vous avez installé l’appareil physique, comme indiqué dans [Installer Azure Stack Edge Mini R](azure-stack-edge-mini-r-deploy-install.md).
    - Vous avez configuré le réseau et activé et configuré le réseau de calcul sur votre appareil, comme indiqué dans [Didacticiel : Configurer le réseau pour Azure Stack Edge Mini R avec GPU](azure-stack-edge-mini-r-deploy-configure-network-compute-web-proxy.md).


## <a name="configure-device-settings"></a>Configurer les paramètres des appareils

Procédez comme suit pour configurer les paramètres liés aux appareils :

1. Sur la page **Appareil**, effectuez les opérations suivantes :

    1. Entrez un nom convivial pour votre appareil. Ce nom convivial doit contenir entre 1 et 13 caractères et peut être composé de lettres, de chiffres et de traits d’union.

    2. Fournissez un **Domaine DNS** pour votre appareil. Ce domaine est utilisé pour configurer l’appareil en tant que serveur de fichiers.

    3. Cliquez sur **Appliquer** pour valider et appliquer les paramètres d’appareil que vous avez configurés.

        ![Page « Appareil » de l’interface utilisateur web locale 1](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-1.png)

        Si vous avez modifié le nom de l’appareil et le domaine DNS, les certificats auto-signés qui existaient sur l’appareil ne fonctionneront pas. 

        ![Page « Appareil » de l’interface utilisateur web locale 2](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-2.png)

        Vous devez choisir une des options suivantes lorsque vous configurez des certificats : 
        
        - Générer et télécharger les certificats de l’appareil. 
        - Apporter vos propres certificats pour l’appareil, y compris la chaîne de signature.
    

    4. Lorsque le nom de l’appareil et le domaine DNS sont modifiés, le point de terminaison SMB est créé.  

        ![Page « Appareil » de l’interface utilisateur web locale 3](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/set-up-device-3.png)

    5. Une fois les paramètres appliqués, sélectionnez **Suivant : Mettre à jour le serveur**.


## <a name="configure-update"></a>Configurer la mise à jour

1. Sur la page **Mettre à jour**, vous pouvez maintenant configurer l’emplacement à partir duquel télécharger les mises à jour de votre appareil.  

    - Vous pouvez récupérer les mises à jour directement à partir du **serveur Microsoft Update**.

        ![Page « Mettre à jour le serveur » de l’interface utilisateur web locale](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/update-server-1.png)

        Vous pouvez également choisir de déployer des mises à jour à partir de **WSUS (Windows Server Update Services)** . Indiquez le chemin d’accès au serveur WSUS.
        
        ![Page « Mettre à jour le serveur » de l’interface utilisateur web locale 2](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/update-server-2.png)

        > [!NOTE] 
        > Si un serveur Windows Update distinct est configuré et si vous choisissez de vous connecter via *https* (au lieu de *http*), les certificats de chaîne de signature requis pour se connecter au serveur de mise à jour sont nécessaires. Pour plus d’informations sur la façon de créer et télécharger des certificats, consultez [Gérer les certificats](azure-stack-edge-gpu-manage-certificates.md). Pour travailler en mode déconnecté, comme votre hiérarchisation des appareils Azure Stack Edge vers Modular Data Center, activez l’option WSUS. Pendant l’activation, l’appareil recherche des mises à jour et, si le serveur n’est pas configuré, l’activation échoue. 

2. Sélectionnez **Appliquer**.
3. Une fois le serveur de mise à jour configuré, sélectionnez **Suivant : Heure**.
    

## <a name="configure-time"></a>Configurer l’heure

Procédez comme suit pour configurer les paramètres d’heure sur votre appareil. 

> [!IMPORTANT]
> Bien que les paramètres d’heure soient facultatifs, nous vous recommandons vivement de configurer un serveur NTP principal et un serveur NTP secondaire sur le réseau local de votre appareil. Si un serveur local n’est pas disponible, des serveurs NTP publics peuvent être configurés.

Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud.

1. Sur la page **Heure**, vous pouvez sélectionner le fuseau horaire et les serveurs NTP principal et secondaire de votre appareil.  
    
    1. Dans la liste déroulante **Fuseau horaire**, sélectionnez le fuseau horaire qui correspond à l’emplacement géographique de l’appareil déployé.
        Le fuseau horaire par défaut de votre appareil est PST. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.

    2. Dans la zone **Serveur NTP principal**, entrez le serveur principal de votre appareil ou acceptez la valeur par défaut time.windows.com.  
        Vérifiez que votre réseau autorise le trafic NTP à passer de votre centre de données à Internet.

    3. Si vous le souhaitez, dans la zone **Serveur NTP secondaire**, entrez un serveur secondaire pour votre appareil.

    4. Cliquez sur **Appliquer** pour valider et appliquer les paramètres d’heure que vous avez configurés.

        ![Page « Heure » de l’interface utilisateur web locale](./media/azure-stack-edge-mini-r-deploy-set-up-device-update-time/time-settings-1.png)

2. Une fois les paramètres appliqués, sélectionnez **Suivant : Certificats**.


## <a name="next-steps"></a>Étapes suivantes

Ce tutoriel vous fournira des informations sur :

> [!div class="checklist"]
>
> * Prérequis
> * Configurer les paramètres des appareils
> * Configurer la mise à jour 
> * Configurer l’heure

Pour apprendre à configurer des certificats pour votre appareil Azure Stack Edge Mini R, consultez :

> [!div class="nextstepaction"]
> [Configurer des certificats](./azure-stack-edge-mini-r-deploy-configure-certificates-vpn-encryption.md)
