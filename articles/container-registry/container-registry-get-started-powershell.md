---
title: Démarrage rapide – Création d’un registre – PowerShell
description: Apprenez rapidement à créer un registre de conteneurs Docker privé dans Azure Container Registry avec PowerShell.
ms.date: 01/22/2019
ms.topic: quickstart
ms.custom:
- mvc
- devx-track-azurepowershell
- mode-api
ms.openlocfilehash: bd9b93e22081c43dfa3fd934f13da3713120aadb
ms.sourcegitcommit: 49b2069d9bcee4ee7dd77b9f1791588fe2a23937
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2021
ms.locfileid: "107537382"
---
# <a name="quickstart-create-a-private-container-registry-using-azure-powershell"></a>Démarrage rapide : Créer un registre de conteneurs privé avec Azure PowerShell

Azure Container Registry est un service de registre de conteneurs Docker géré et privé que vous utilisez pour créer, stocker et dépanner des images conteneurs Docker. Dans ce démarrage rapide, vous apprenez à créer un registre de conteneurs Azure à l’aide de PowerShell. Vous allez ensuite utiliser des commandes Docker pour envoyer (push) une image conteneur dans le registre, puis tirer (pull) et exécuter l’image à partir de votre registre.

## <a name="prerequisites"></a>Prérequis

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

Ce guide de démarrage rapide nécessite le module Azure PowerShell. Exécutez `Get-Module -ListAvailable Az` pour déterminer la version installée. Si vous devez installer ou mettre à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-az-ps).

Docker doit également être installé en local. Docker fournit des packages pour [macOS][docker-mac], [Windows][docker-windows] et [Linux][docker-linux].

Étant donné qu’Azure Cloud Shell n’inclut pas tous les composants Docker requis (par exemple, le démon `dockerd`), vous ne pouvez pas l’utiliser pour ce démarrage rapide.

## <a name="sign-in-to-azure"></a>Connexion à Azure

Connectez-vous à votre abonnement Azure avec la commande [Connect-AzAccount][Connect-AzAccount] et suivez les instructions indiquées à l’écran.

```powershell
Connect-AzAccount
```

## <a name="create-resource-group"></a>Créer un groupe de ressources

Une fois votre authentification auprès d’Azure effectuée, créez un groupe de ressources avec [New-AzResourceGroup][New-AzResourceGroup]. Un groupe de ressources est un conteneur logique dans lequel vous déployez et gérez vos ressources Azure.

```powershell
New-AzResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-container-registry"></a>Créer un registre de conteneurs

Ensuite, créez un registre de conteneurs dans votre nouveau groupe de ressources avec la commande [New-AzContainerRegistry][New-AzContainerRegistry].

Le nom du registre doit être unique dans Azure et contenir entre 5 et 50 caractères alphanumériques. L’exemple suivant crée un registre appelé « myContainerRegistry007 ». Remplacez *myContainerRegistry007* dans la commande suivante, puis exécutez-la pour créer le registre :

```powershell
$registry = New-AzContainerRegistry -ResourceGroupName "myResourceGroup" -Name "myContainerRegistry007" -EnableAdminUser -Sku Basic
```

Dans ce guide de démarrage rapide, vous allez créer un registre *De base*. Il s’agit d’une option à coût optimisé pour les développeurs qui apprennent à se servir d’Azure Container Registry. Pour plus d’informations sur les niveaux de service disponibles, consultez [Niveaux de service des registres de conteneurs][container-registry-skus].

## <a name="log-in-to-registry"></a>Se connecter au registre

Avant d’extraire et d’envoyer des images conteneurs, vous devez vous connecter au registre. Pour que ce guide de démarrage rapide reste bref, activez l'utilisateur administrateur sur votre registre à l'aide de la commande [Get-AzContainerRegistryCredential][Get-AzContainerRegistryCredential]. Dans les scénarios de production, vous devez utiliser une autre [méthode d'authentification](container-registry-authentication.md) pour l'accès au registre, comme un principal de service. 

```powershell
$creds = Get-AzContainerRegistryCredential -Registry $registry
```

Ensuite, exécutez [docker login][docker-login] pour vous connecter :

```powershell
$creds.Password | docker login $registry.LoginServer -u $creds.Username --password-stdin
```

Une fois l’opération terminée, la commande renvoie `Login Succeeded`.

> [!TIP]
> Azure CLI fournit la commande `az acr login`, qui vous permettra de vous connecter à un registre de conteneurs en utilisant votre [identité individuelle](container-registry-authentication.md#individual-login-with-azure-ad), sans transmettre les informations d'identification Docker.


[!INCLUDE [container-registry-quickstart-docker-push](../../includes/container-registry-quickstart-docker-push.md)]

[!INCLUDE [container-registry-quickstart-docker-pull](../../includes/container-registry-quickstart-docker-pull.md)]

## <a name="clean-up-resources"></a>Nettoyer les ressources

Quand vous avez terminé d’utiliser les ressources créées dans ce guide de démarrage rapide, utilisez la commande [Remove-AzResourceGroup][Remove-AzResourceGroup] pour supprimer le groupe de ressources, le registre de conteneurs et les images conteneur stockées à cet endroit :

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez créé un registre de conteneurs Azure avec Azure PowerShell, envoyé (push) une image conteneur, puis tiré (pull) et exécuté l’image à partir du registre. Passez à présent au tutoriel sur Azure Container Registry (ACR) pour approfondir vos connaissances.

> [!div class="nextstepaction"]
> [Tutoriels sur Azure Container Registry][container-registry-tutorial-prepare-registry]

> [!div class="nextstepaction"]
> [Tutoriels Azure Container Registry Tasks][container-registry-tutorial-quick-task]

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- Links - internal -->
[Connect-AzAccount]: /powershell/module/az.accounts/connect-azaccount
[Get-AzContainerRegistryCredential]: /powershell/module/az.containerregistry/get-azcontainerregistrycredential
[Get-Module]: /powershell/module/microsoft.powershell.core/get-module
[New-AzContainerRegistry]: /powershell/module/az.containerregistry/New-AzContainerRegistry
[New-AzResourceGroup]: /powershell/module/az.resources/new-azresourcegroup
[Remove-AzResourceGroup]: /powershell/module/az.resources/remove-azresourcegroup
[container-registry-tutorial-quick-task]: container-registry-tutorial-quick-task.md
[container-registry-skus]: container-registry-skus.md
[container-registry-tutorial-prepare-registry]: container-registry-tutorial-prepare-registry.md
