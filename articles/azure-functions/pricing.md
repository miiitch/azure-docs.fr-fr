---
title: Tarification d’Azure Functions
description: Découvrez le fonctionnement de la facturation pour Azure Functions.
author: craigshoemaker
ms.author: cshoe
ms.topic: conceptual
ms.date: 11/20/2020
ms.openlocfilehash: cde1c5ee45edb4472bed992ee9ac4075f8ad05ff
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "95002118"
---
# <a name="azure-functions-pricing"></a>Tarification d’Azure Functions

Azure Functions propose trois sortes de plans tarifaires. Choisissez celui qui répond le mieux à vos besoins :

- **Plan Consommation** : Azure fournit toutes les ressources de calcul nécessaires. Vous n’avez pas à vous préoccuper de la gestion des ressources et seul le temps pendant lequel votre code s’exécute est facturé.

- **Plan Premium** : Vous spécifiez un nombre d’instances préparées à l’utilisation qui sont toujours en ligne et prêtes à répondre immédiatement. Lorsque votre fonction est exécutée, Azure fournit toutes les ressources de calcul supplémentaires nécessaires. Vous payez les instances chauffées au préalable qui s’exécutent en continu ainsi que toutes les instances supplémentaires dont vous avez besoin à mesure qu’Azure effectue le scale-in/scale-out de votre application.

- **Plan App Service** : Exécutez vos fonctions exactement comme vos applications web. Si vous utilisez App Service pour vos autres applications, vos fonctions peuvent s’exécuter sur le même plan, sans coûts supplémentaires.

Pour plus d’informations sur les plans d’hébergement, consultez [Comparaison des plans d’hébergement Azure Functions](functions-scale.md). Vous trouverez toutes les informations sur la tarification sur la [page Tarification de Functions](https://azure.microsoft.com/pricing/details/functions/).
