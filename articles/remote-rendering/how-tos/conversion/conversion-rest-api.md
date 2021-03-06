---
title: API REST de conversion de ressources
description: Décrit comment convertir une ressource via l’API REST
author: florianborn71
ms.author: flborn
ms.date: 02/04/2020
ms.topic: how-to
ms.openlocfilehash: e3db4b9c9b4a05142f1327f681b067748cb1a2f9
ms.sourcegitcommit: ac035293291c3d2962cee270b33fca3628432fac
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2021
ms.locfileid: "104951638"
---
# <a name="use-the-model-conversion-rest-api"></a>Utiliser l’API REST de conversion de modèle

Le service de [conversion de modèle](model-conversion.md) est contrôlé via une [API REST](https://en.wikipedia.org/wiki/Representational_state_transfer). Cette API permet de créer des conversions, d’obtenir des propriétés de conversion et de lister les conversions existantes.

## <a name="rest-api-reference"></a>Référence d’API REST

La documentation de référence sur l’API REST de Remote Rendering est disponible [ici](/rest/api/mixedreality/2021-01-01/remoterendering), et les définitions de Swagger sont disponibles [ici](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/mixedreality/data-plane/Microsoft.MixedReality).

Dans le [dépôt d’exemples ARR](https://github.com/Azure/azure-remote-rendering), dans le dossier *Scripts*, nous fournissons un script PowerShell appelé *Conversion.ps1*, qui illustre l’utilisation de notre service. Le script et sa configuration sont décrits ici : [Exemples de scripts PowerShell](../../samples/powershell-example-scripts.md). Nous fournissons également des kits de développement logiciel (SDK) pour [.NET](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/remoterendering/Azure.MixedReality.RemoteRendering/README.md) et [Java]( https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/remoterendering/azure-mixedreality-remoterendering/README.md).

## <a name="next-steps"></a>Étapes suivantes

- [Utiliser Stockage Blob Azure pour une conversion de modèle](blob-storage.md)
- [Conversion de modèle](model-conversion.md)