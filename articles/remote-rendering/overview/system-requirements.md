---
title: Configuration système requise
description: Indique la configuration requise pour Azure Remote Rendering
author: florianborn71
ms.author: flborn
ms.date: 02/03/2020
ms.topic: article
ms.custom: references_regions
ms.openlocfilehash: 789233ce1ede751276f965143716694c6feca3ca
ms.sourcegitcommit: 32e0fedb80b5a5ed0d2336cea18c3ec3b5015ca1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "105032787"
---
# <a name="system-requirements"></a>Configuration système requise

Ce chapitre décrit la configuration requise pour utiliser *Azure Remote Rendering* (ARR).

## <a name="development-pc"></a>PC de développement

* Windows 10 version 1903 ou ultérieure.
* Pilotes graphiques à jour.
* Facultatif : [Décodeur vidéo matériel H265](https://www.microsoft.com/p/hevc-video-extensions/9nmzlz57r3t7), si vous souhaitez utiliser l’aperçu local du contenu rendu à distance (par exemple, dans Unity).

> [!IMPORTANT]
> Windows Update ne fournissant pas toujours les pilotes GPU les plus récents, consultez le site web du fabricant de votre GPU pour obtenir les pilotes les plus récents :
>
> * [Pilotes AMD](https://www.amd.com/en/support)
> * [Pilotes Intel](https://www.intel.com/content/www/us/en/support/detect.html)
> * [Pilotes NVIDIA](https://www.nvidia.com/Download/index.aspx)

Le tableau ci-dessous répertorie les GPU qui prennent en charge le décodage vidéo matériel H265.

| Fabricant du GPU | Modèles pris en charge |
|-----------|:-----------|
| NVIDIA | Consultez la **Matrice de prise en charge NVDEC** [en bas de cette page](https://developer.nvidia.com/video-encode-decode-gpu-support-matrix). Votre GPU a besoin d’un Oui dans la colonne **H. 265 4:2:0 8-bit**. |
| AMD | GPU avec au minimum la version 6 du [décodeur vidéo unifié](https://en.wikipedia.org/wiki/Unified_Video_Decoder#UVD_6) d’AMD. |
| Intel | GPU Skylake et plus récents |

Même si vous pouvez installer le codec H265 correct, les propriétés de sécurité des DLL du codec peuvent entraîner des échecs d’initialisation de celui-ci. Le [Guide de résolution des problèmes](../resources/troubleshoot.md#h265-codec-not-available) explique comment résoudre ce problème. Le problème de DLL ne peut se produire que lors de l’utilisation du service dans une application de bureau, par exemple, dans Unity.

## <a name="devices"></a>Appareils

Actuellement, Azure Remote Rendering ne prend en charge que **HoloLens 2** et Windows Desktop comme appareil cible. Consultez la section [Limitations de la plateforme](../reference/limits.md#platform-limitations).

Il est important d’utiliser le codec HEVC le plus récent, car les versions plus récentes présentent des améliorations significatives en matière de latence. Pour déterminer la version installée sur votre appareil :

1. Démarrez **Microsoft Store**.
1. Cliquez sur le bouton **« ... »** dans l’angle supérieur droit.
1. Sélectionnez **Téléchargements et mises à jour**.
1. Dans la liste, recherchez **Extensions vidéo HEVC du fabricant de l’appareil**. Si cet élément n’est pas listé sous les mises à jour, la version la plus récente est déjà installée.
1. Assurez-vous que la version du codec répertorié est au minimum la version **1.0.21821.0**.
1. Cliquez sur le bouton **Obtenir les mises à jour**, puis attendez que l’installation soit terminée.

## <a name="network"></a>Réseau

Une connexion réseau stable à faible latence est essentielle pour une bonne expérience utilisateur.

Consultez le chapitre dédié à la [configuration réseau requise](../reference/network-requirements.md).

Pour résoudre les problèmes de réseau, reportez-vous au [Guide de résolution des problèmes](../resources/troubleshoot.md#unstable-holograms).

### <a name="network-firewall"></a>Pare-feu réseau

### <a name="sdk-version--0176"></a>Version du kit SDK >= 0.1.76

Les machines virtuelles de rendu distant utilisent des adresses IP partagées issues des plages d’adresses IP suivantes :

| Nom             | Région         | Préfixe IP         |
|------------------|:---------------|:------------------|
| Australie Est   | australiaeast  | 20.53.44.240/28   |
| USA Est          | eastus         | 20.62.129.224/28  |
| USA Est 2        | eastus2        | 20.49.103.240/28  |
| Japon Est       | japaneast      | 20.191.165.112/28 |
| Europe Nord     | northeurope    | 52.146.133.64/28  |
| États-Unis - partie centrale méridionale | southcentralus | 20.65.132.80/28   |
| Asie Sud-Est   | southeastasia  | 20.195.64.224/28  |
| Sud du Royaume-Uni         | uksouth        | 51.143.209.144/28 |
| Europe Ouest      | westeurope     | 20.61.99.112/28   |
| USA Ouest 2        | westus2        | 20.51.9.64/28     |

Veillez à ce que vos pare-feu (sur l’appareil, dans les routeurs, etc.) ne bloquent pas ces plages d’adresses IP ni les plages de ports suivantes :

| Port              | Protocol  | Allow    |
|-------------------|---------- |----------|
| 49152-65534       | TCP / UDP | Sortant |

#### <a name="sdk-version--0176"></a>Version du kit SDK < 0.1.76

Vérifiez que vos pare-feu (sur l’appareil, dans les routeurs, etc.) ne bloquent pas les ports suivants :

| Port              | Protocol | Allow    | Description |
|-------------------|----------|----------|-------------|
| 50051             | TCP      | Sortant | Connexion initiale (poignée de main HTTP) |
| 8266              | UDP      | Sortant | Transfert de données |
| 5000, 5433, 8443  | TCP      | Sortant | Requis pour l’[outil ArrInspector](../resources/tools/arr-inspector.md)|


## <a name="software"></a>Logiciel

Les logiciels suivants doivent être installés :

* La dernière version de **Visual Studio 2019** [(télécharger)](https://visualstudio.microsoft.com/vs/older-downloads/)
* [Outils Visual Studio pour Mixed Reality](/windows/mixed-reality/install-the-tools). Plus précisément, les installations de *charge de travail* suivantes sont obligatoires :
  * **Développement Desktop en C++**
  * **Développement de la plateforme Windows universelle (UWP)**
* **Le SDK Windows 10.0.18362.0** [(télécharger)](https://developer.microsoft.com/windows/downloads/windows-10-sdk)
* **GIT** [(télécharger)](https://git-scm.com/downloads)
* Facultatif : Pour afficher le flux vidéo du serveur sur un PC de bureau, vous avez besoin des **Extensions vidéo HEVC** [(lien du Microsoft Store)](https://www.microsoft.com/p/hevc-video-extensions/9nmzlz57r3t7). Vérifiez que la version la plus récente est installée en recherchant des mises à jour dans le Store.

## <a name="unity"></a>Unity

Pour le développement avec Unity, installez une version actuelle de Unity 2019.3 ou 2019.4 LTS [(Télécharger)](https://unity3d.com/get-unity/download). Nous vous recommandons d’utiliser Unity Hub pour gérer les installations.
Veillez à inclure les modules suivants dans votre installation de Unity :
* **UWP** : prise en charge de la build de la plateforme Windows universelle
* **IL2CPP** : prise en charge de la build Windows (IL2CPP)

## <a name="next-steps"></a>Étapes suivantes

* [Démarrage rapide : Afficher un modèle avec Unity](../quickstarts/render-model.md)