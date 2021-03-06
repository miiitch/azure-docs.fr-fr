---
title: Suppression réversible pour les conteneurs (préversion)
titleSuffix: Azure Storage
description: La fonctionnalité de suppression réversible pour les conteneurs (préversion) protège vos données, ce qui vous permet de récupérer plus facilement vos données en cas de modification ou de suppression malencontreuses de celles-ci par une application ou un autre utilisateur du compte de stockage.
services: storage
author: tamram
ms.service: storage
ms.topic: conceptual
ms.date: 03/05/2021
ms.author: tamram
ms.subservice: blobs
ms.custom: references_regions
ms.openlocfilehash: 2efd673d26231e83d820f7971a740d06e9b2a1d2
ms.sourcegitcommit: 4b0e424f5aa8a11daf0eec32456854542a2f5df0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107785412"
---
# <a name="soft-delete-for-containers-preview"></a>Suppression réversible pour les conteneurs (préversion)

La suppression réversible pour les conteneurs (préversion) protège vos données contre les suppressions accidentelles ou malveillantes. Lorsque la suppression réversible de conteneur est activée pour un compte de stockage, tout conteneur supprimé et son contenu sont conservés dans Stockage Azure pour la période que vous spécifiez. Pendant la période de rétention, vous pouvez restaurer des conteneurs précédemment supprimés. La restauration d’un conteneur a pour effet de restaurer tous les blobs figurant dans celui-ci au moment de sa suppression.

Pour la protection de bout en bout de vos données de blobs, Microsoft recommande d’activer les fonctionnalités de protection des données suivantes :

- Suppression réversible de conteneur, pour restaurer un conteneur supprimé. Pour savoir comment activer la suppression réversible de conteneur, consultez [Activer et gérer la suppression réversible pour les conteneurs](soft-delete-container-enable.md).
- Gestion des versions des objets blob, pour gérer automatiquement les versions précédentes d’un objet blob. Lorsque le contrôle de version est activé, vous pouvez restaurer une version antérieure d’un objet blob pour récupérer vos données si celles-ci ont été modifiées ou supprimées par erreur. Pour savoir comment activer le contrôle de version des blobs, consultez [Activer et gérer le contrôle de version des blobs](versioning-enable.md).
- Suppression réversible de blob, pour restaurer un blob ou une version supprimés. Pour savoir comment activer la suppression réversible de blob, consultez [Activer et gérer la suppression réversible pour les blobs](soft-delete-blob-enable.md).

> [!IMPORTANT]
> La suppression réversible de conteneur est actuellement en **préversion**. Consultez l’[Avenant aux conditions d’utilisation des préversions de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) pour connaître les conditions juridiques qui s’appliquent aux fonctionnalités Azure disponibles en version bêta, en préversion ou qui ne sont pas encore en phase de disponibilité générale.

## <a name="how-container-soft-delete-works"></a>Fonctionnement de la suppression réversible de conteneur

Lorsque vous activez la suppression réversible de conteneur, vous pouvez spécifier une période de rétention pour les conteneurs supprimés qui est comprise entre 1 et 365 jours. La période de conservation par défaut est 7 jours. Pendant la période de rétention, vous pouvez récupérer un conteneur supprimé en appelant l’opération **Restore Container**.

Lorsque vous restaurez un conteneur, cela a également pour effet de restaurer les blobs qu’il contient ainsi que leurs versions. Toutefois, vous ne pouvez utiliser une suppression réversible de conteneur que pour restaurer des blobs que si le conteneur proprement dit a été supprimé. Pour restaurer un blob supprimé quand son conteneur parent n’a pas été supprimé, vous devez utiliser la suppression réversible ou le contrôle de version de blob.

> [!WARNING]
> Une suppression réversible de conteneur ne permet de restaurer que des conteneurs entiers et ce qu’ils contenaient au moment de la suppression. Une suppression réversible de conteneur ne permet pas de restaurer un blob supprimé au sein d’un conteneur. Microsoft recommande également d’activer la suppression réversible des objets blob et la gestion des versions d’objets blob pour protéger les objets blob individuels dans un conteneur.

Le diagramme suivant montre comment restaurer un conteneur supprimé quand la suppression réversible de conteneur est activée :

:::image type="content" source="media/soft-delete-container-overview/container-soft-delete-diagram.png" alt-text="Diagramme montrant comment restaurer un conteneur supprimé de manière réversible":::

Lorsque vous restaurez un conteneur, vous pouvez le restaurer avec son nom d’origine si celui-ci n’a pas été réutilisé. Si le nom du conteneur d’origine a été utilisé, vous pouvez restaurer le conteneur avec un nouveau nom.

Une fois la période de rétention expirée, le conteneur est définitivement supprimé de Stockage Azure et ne peut pas être récupéré. La période de rétention commence au moment où le conteneur est supprimé. Vous pouvez modifier la période de rétention à tout moment, mais gardez à l’esprit qu’une période de rétention mise à jour s’applique uniquement aux conteneurs nouvellement supprimés. Les conteneurs supprimés avant la mise à jour seront définitivement supprimés conformément à la période de rétention qui était en vigueur au moment de leur suppression.

La désactivation de la suppression réversible de conteneur n’entraîne pas la suppression définitive des conteneurs qui ont été précédemment supprimés de manière réversible. Tous les conteneurs supprimés de manière réversible seront définitivement supprimés à l’expiration de la période de rétention qui était en vigueur au moment de leur suppression.

> [!IMPORTANT]
> La suppression réversible du conteneur ne protège pas contre la suppression d’un compte de stockage. Il protège uniquement contre la suppression des conteneurs dans ce compte. Pour empêcher toute suppression d’un compte de stockage, configurez un verrou sur la ressource du compte de stockage. Pour plus d’informations sur le verrouillage d’un compte de stockage, consultez [Appliquer un verrou Azure Resource Manager à un compte de stockage](../common/lock-account-resource.md).

## <a name="about-the-preview"></a>À propos de la préversion

La suppression réversible de conteneur est disponible en préversion dans toutes les régions Azure.

La version 2019-12-12 ou les versions ultérieures de l’API REST Stockage Azure prennent en charge la suppression réversible de conteneur.

### <a name="storage-account-support"></a>Prise en charge du compte de stockage

La suppression réversible de conteneur est disponible pour les types de comptes de stockage suivants :

- Comptes de stockage v1 et v2 universels
- Comptes de stockage d’objets blob de blocs
- Comptes de stockage d’objets blob

Les comptes de stockage avec espace de noms hiérarchique activé pour une utilisation avec Azure Data Lake Storage Gen2 sont également pris en charge.

### <a name="register-for-the-preview"></a>S’inscrire pour la préversion

Pour vous inscrire à la préversion de la suppression réversible de conteneur, utilisez PowerShell ou Azure CLI pour envoyer une demande d’inscription de la fonctionnalité avec votre abonnement. Une fois votre demande approuvée, vous pouvez activer la suppression réversible de conteneur sur tout compte de stockage v2 universel, compte de stockage de blobs ou compte de stockage d’objets blob de blocs Premium.

# <a name="powershell"></a>[PowerShell](#tab/powershell)

Pour vous inscrire à l’aide de PowerShell, appelez la commande [Register-AzProviderFeature](/powershell/module/az.resources/register-azproviderfeature).

```powershell
# Register for container soft delete (preview)
Register-AzProviderFeature -ProviderNamespace Microsoft.Storage `
    -FeatureName ContainerSoftDelete

# Refresh the Azure Storage provider namespace
Register-AzResourceProvider -ProviderNamespace Microsoft.Storage
```

# <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

Pour vous inscrire avec Azure CLI, appelez la commande [az feature register](/cli/azure/feature#az_feature_register).

```azurecli
az feature register --namespace Microsoft.Storage --name ContainerSoftDelete
az provider register --namespace 'Microsoft.Storage'
```

---

### <a name="check-the-status-of-your-registration"></a>Vérifier l’état de votre inscription

Pour vérifier l’état de votre inscription, utilisez PowerShell ou Azure CLI.

# <a name="powershell"></a>[PowerShell](#tab/powershell)

Pour vérifier l’état de votre inscription à l’aide de PowerShell, appelez la commande [Get-AzProviderFeature](/powershell/module/az.resources/get-azproviderfeature).

```powershell
Get-AzProviderFeature -ProviderNamespace Microsoft.Storage -FeatureName ContainerSoftDelete
```

# <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

Pour vérifier l’état de votre inscription à l’aide d’Azure CLI, appelez la commande [az feature](/cli/azure/feature#az_feature_show).

```azurecli
az feature show --namespace Microsoft.Storage --name ContainerSoftDelete
```

---

## <a name="pricing-and-billing"></a>Tarification et facturation

Aucuns frais supplémentaires ne sont facturés pour activer la suppression réversible de conteneur. Les données qui se trouvent dans des conteneurs supprimés de manière réversible sont facturées au même tarif que les données actives.

## <a name="next-steps"></a>Étapes suivantes

- [Configuration de la suppression réversible de conteneur](soft-delete-container-enable.md)
- [Suppression réversible pour les objets blob](soft-delete-blob-overview.md)
- [Contrôle de version des blobs](versioning-overview.md)
