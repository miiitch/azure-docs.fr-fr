---
title: Se connecter à des machines virtuelles à l’aide d’un navigateur – Azure | Microsoft Docs
description: Découvrez comment vous connecter à vos machines virtuelles à l’aide d’un navigateur.
ms.topic: article
ms.date: 06/26/2020
ms.openlocfilehash: 352fc5fd3ff53a00d9f62966ecf21417ad898706
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "87288054"
---
# <a name="connect-to-your-virtual-machines-through-a-browser"></a>Connectez-vous à vos machines virtuelles à l’aide d’un navigateur 

DevTest Labs s’intègre à [Azure Bastion](../bastion/index.yml), ce qui vous permet de vous connecter à vos machines virtuelles via un navigateur. Pour plus d’informations sur l’activation de cette fonctionnalité dans DevTest Labs, consultez la page [Activer la connexion du navigateur sur des machines virtuelles du labo](enable-browser-connection-lab-virtual-machines.md).

Une fois la *connexion du navigateur*, les utilisateurs du labo peuvent accéder aux machines virtuelles à l’aide d’un navigateur.  

## <a name="create-a-lab-virtual-machine"></a>Créer une machine virtuelle du labo

Vous devez d’abord créer la machine virtuelle du labo dans un réseau virtuel sur lequel Bastion est configuré. Sélectionnez le deuxième **sous-réseau** que vous avez créé, pas AzureBastionSubnet. Vous pouvez sélectionner un réseau virtuel durant la création de la machine virtuelle en accédant à l’onglet **Paramètres avancés**.

![Créer une machine virtuelle](./media/connect-virtual-machine-through-browser/create-virtual-machine.png)

## <a name="launch-virtual-machine-in-a-browser"></a>Lancez la machine virtuelle dans un navigateur

Une fois la machine virtuelle créée, vous pouvez la lancer dans un navigateur en cliquant sur le bouton *Connexion du navigateur* et en entrant votre nom d’utilisateur et votre mot de passe pour la machine.  

![Lancez dans le navigateur](./media/connect-virtual-machine-through-browser/browser-connect.png)

## <a name="next-steps"></a>Étapes suivantes

[Ajouter une machine virtuelle à un laboratoire dans Azure DevTest Labs](devtest-lab-add-vm.md)
