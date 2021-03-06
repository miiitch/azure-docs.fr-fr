---
title: Attribuer une stratégie d’accès Azure Key Vault (CLI)
description: Comment utiliser Azure CLI pour attribuer une stratégie d’accès Key Vault à un principal de sécurité ou à une identité d’application.
services: key-vault
author: msmbaldwin
tags: azure-resource-manager
ms.service: key-vault
ms.subservice: general
ms.topic: how-to
ms.date: 08/27/2020
ms.author: mbaldwin
ms.openlocfilehash: 349d7453962a736c9f15bb7d31d5a44098f463a4
ms.sourcegitcommit: 4b0e424f5aa8a11daf0eec32456854542a2f5df0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107791946"
---
# <a name="assign-a-key-vault-access-policy"></a>Attribuer une stratégie d’accès Key Vault

Une stratégie d’accès Key Vault détermine si un principal de sécurité donné, à savoir un utilisateur, une application ou un groupe d’utilisateurs, peut effectuer différentes opérations sur des [secrets](../secrets/index.yml), [clés](../keys/index.yml) et [certificats](../certificates/index.yml) de Key Vault. Vous pouvez attribuer des stratégies d’accès à l’aide du [portail Azure](assign-access-policy-portal.md), d’Azure CLI (cet article) ou d’[Azure PowerShell](assign-access-policy-powershell.md).

[!INCLUDE [key-vault-access-policy-limits.md](../../../includes/key-vault-access-policy-limits.md)]

Pour plus d’informations sur la création de groupes dans Azure Active Directory à l’aide d’Azure CLI, consultez [az ad group create](/cli/azure/ad/group#az_ad_group_create) et [az ad group member add](/cli/azure/ad/group/member#az_ad_group_member_add).

## <a name="configure-the-azure-cli-and-sign-in"></a>Configurer Azure CLI et se connecter

1. Pour exécuter des commandes Azure CLI localement, installez [Azure CLI](/cli/azure/install-azure-cli).
 
    Pour exécuter des commandes directement dans le cloud, utilisez le service [Azure Cloud Shell](../../cloud-shell/overview.md).

1. CLI locale uniquement : connectez-vous à Azure à l’aide de la commande `az login` :

    ```bash
    az login
    ```

    La commande `az login` ouvre une fenêtre de navigateur pour recueillir les informations d’identification si nécessaire.

## <a name="acquire-the-object-id"></a>Acquérir l’ID d’objet

Déterminez l’ID d’objet de l’application, du groupe ou de l’utilisateur auquel vous souhaitez attribuer la stratégie d’accès :

- Applications et autres principaux de service : utilisez la commande [az ad sp list](/cli/azure/ad/sp#az_ad_sp_list) pour récupérer vos principaux de service. Examinez la sortie de la commande pour déterminer l’ID d’objet du principal de sécurité auquel vous souhaitez attribuer la stratégie d’accès.

    ```azurecli-interactive
    az ad sp list --show-mine
    ```

- Groupes : utilisez la commande [az ad group list](/cli/azure/ad/group#az_ad_group_list), en filtrant les résultats avec le paramètre `--display-name` :

     ```azurecli-interactive
    az ad group list --display-name <search-string>
    ```

- Utilisateurs : utilisez la commande [az ad user show](/cli/azure/ad/user#az_ad_user_show), en passant l’adresse e-mail de l’utilisateur dans le paramètre `--id` :

    ```azurecli-interactive
    az ad user show --id <email-address-of-user>
    ```

## <a name="assign-the-access-policy"></a>Attribuer la stratégie d’accès
    
Utilisez la commande [az key vault set-policy](/cli/azure/keyvault#az_keyvault_set_policy) pour attribuer les autorisations souhaitées :

```azurecli-interactive
az keyvault set-policy --name myKeyVault --object-id <object-id> --secret-permissions <secret-permissions> --key-permissions <key-permissions> --certificate-permissions <certificate-permissions>
```

Remplacez `<object-id>` par l’ID objet de votre principal de sécurité.

Vous avez uniquement besoin d’inclure `--secret-permissions`, `--key-permissions`et `--certificate-permissions` lors de l’attribution d’autorisations à ces types particuliers. Les valeurs autorisées pour `<secret-permissions>`, `<key-permissions>` et `<certificate-permissions>` sont indiquées dans la documentation de la commande [az keyvault set-policy](/cli/azure/keyvault#az_keyvault_set_policy).

## <a name="next-steps"></a>Étapes suivantes

- [Sécurité d’Azure Key Vault : Gestion des identités et des accès](security-overview.md#identity-management)
- [Sécuriser votre coffre de clés](security-overview.md)
- [Guide du développeur Azure Key Vault](developers-guide.md)