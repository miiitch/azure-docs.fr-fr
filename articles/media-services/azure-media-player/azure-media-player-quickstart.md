---
title: Démarrage rapide du Lecteur multimédia Azure
description: Découvrez les étapes de base de la configuration du Lecteur multimédia Azure.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.service: media-services
ms.topic: quickstart
ms.date: 04/05/2021
ms.openlocfilehash: a6fd603318a25e15d1d4dcc1e3eaf75f96fc5ade
ms.sourcegitcommit: 56b0c7923d67f96da21653b4bb37d943c36a81d6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "106448625"
---
# <a name="azure-media-player-quickstart"></a>Démarrage rapide du Lecteur multimédia Azure
Le lecteur multimédia Azure est facile à configurer. Seules quelques minutes sont nécessaires pour récupérer la lecture simple de contenu multimédia à partir de votre compte Azure Media Services. Cette section montre les étapes de base sans entrer dans les détails. Les sections qui suivent fournissent des détails sur l’installation et la configuration du Lecteur multimédia Azure.  Ajoutez simplement ce qui suit à l’élément `<head>` de votre document :

```html
    <link href="//amp.azure.net/libs/amp/latest/skins/amp-default/azuremediaplayer.min.css" rel="stylesheet">
    <script src= "//amp.azure.net/libs/amp/latest/azuremediaplayer.min.js"></script>
```

> [!IMPORTANT]
> Vous ne devez **PAS** utiliser la version `latest` en production, car elle est susceptible de changer à la demande. Remplacez `latest` par une version du Lecteur multimédia Azure. Par exemple, remplacez `latest` par `1.0.0`. Les versions du Lecteur multimédia Azure peuvent être examinées à partir d’[ici](https://amp.azure.net/libs/amp/latest/docs/changelog.html).

## <a name="use-the-video-element"></a>Utiliser l’élément vidéo

Ensuite, utilisez juste l’élément `<video>` comme vous le feriez normalement, mais avec un attribut `data-setup` supplémentaire contenant des options. Ces options peuvent inclure n’importe quelle option Azure Media Services dans un objet JSON valide.

```html
    <video id="vid1" class="azuremediaplayer amp-default-skin" autoplay controls width="640" height="400" poster="poster.jpg" data-setup='{"nativeControlsForTouch": false}'>
        <source src="http://amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest" type="application/vnd.ms-sstr+xml" />
        <p class="amp-no-js">
            To view this video please enable JavaScript, and consider upgrading to a web browser that supports HTML5 video
        </p>
    </video>
```

Si vous ne souhaitez pas utiliser la configuration automatique, vous pouvez omettre l’attribut `data-setup` et initialiser manuellement un élément vidéo.

```javascript
    var myPlayer = amp('vid1', { /* Options */
            "nativeControlsForTouch": false,
            autoplay: false,
            controls: true,
            width: "640",
            height: "400",
            poster: ""
        }, function() {
              console.log('Good to go!');
               // add an event listener
              this.addEventListener('ended', function() {
                console.log('Finished!');
            });
          }
    );
    myPlayer.src([{
        src: "http://amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest",
        type: "application/vnd.ms-sstr+xml"
    }]);
```

## <a name="next-steps"></a>Étapes suivantes ##

- [Installation complète du Lecteur multimédia Azure](./azure-media-player-full-setup.md)
