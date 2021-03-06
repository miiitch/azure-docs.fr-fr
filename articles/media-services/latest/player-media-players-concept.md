---
title: Vue d’ensemble des lecteurs multimédias pour Media Services
description: 'Quels lecteurs multimédias puis-je utiliser avec Azure Media Services ? Pour l’instant : Lecteur multimédia Azure, Shaka et Video.js.'
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: overview
ms.date: 3/08/2021
ms.openlocfilehash: 43d0a8ee82a84a57be7c8ded9e7f5afc172bd9d6
ms.sourcegitcommit: 02bc06155692213ef031f049f5dcf4c418e9f509
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2021
ms.locfileid: "106281262"
---
# <a name="media-players-for-media-services"></a>Lecteurs multimédias pour Media Services

Vous pouvez utiliser plusieurs lecteurs multimédias avec Media Services.

## <a name="azure-media-player"></a>Azure Media Player

Le Lecteur multimédia Azure est un lecteur vidéo pour une grande variété de navigateurs et d’appareils. Lecteur multimédia Azure exploite les normes du secteur, telles que HTML5, Media Source Extensions (MSE) et Encrypted Media Extensions (EME), pour offrir une expérience enrichie de diffusion en continu adaptative. Quand ces standards ne sont pas disponibles sur un appareil ou dans un navigateur, le Lecteur multimédia Azure utilise Flash et Silverlight comme technologies de secours. Quelle que soit la technologie de lecture utilisée, les développeurs bénéficient d’une interface JavaScript unifiée pour accéder aux API. Le contenu fourni par Azure Media Services peut être lu sur un large éventail d’appareils et de navigateurs sans travail supplémentaire.

Consultez la [documentation relative au Lecteur multimédia Azure](../azure-media-player/azure-media-player-overview.md).

## <a name="shaka"></a>Shaka

Shaka Player est une bibliothèque JavaScript open source destinée au contenu multimédia adaptatif. Elle lit les formats multimédias adaptatifs (tels que DASH et HLS) dans un navigateur, sans utiliser de plug-ins ni Flash. À la place, le lecteur Shaka utilise les normes web ouvertes Media Source Extensions et Encrypted Media Extensions.

Consultez [Guide pratique pour utiliser le lecteur Shaka avec Azure Media Services](player-shaka-player-how-to.md).

## <a name="videojs"></a>Video.js

Video.js est un lecteur vidéo qui lit les formats multimédias adaptatifs (comme DASH et HLS) dans un navigateur. Video.js utilise les standards web ouverts MediaSource Extensions et Encrypted Media Extensions. Il prend en charge la lecture vidéo sur les ordinateurs de bureau et les appareils mobiles. Sa documentation officielle est accessible à l’adresse https://docs.videojs.com/.

Consultez [Guide pratique pour utiliser le lecteur Video.js avec Azure Media Services](player-how-to-video-js-player.md).


## <a name="next-steps"></a>Étapes suivantes ##

- [Démarrage rapide du Lecteur multimédia Azure](../azure-media-player/azure-media-player-quickstart.md)