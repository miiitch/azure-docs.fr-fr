---
author: Juliako
ms.topic: include
ms.date: 11/13/2020
ms.author: juliako
ms.openlocfilehash: db2f6fe6175b8ff4d6371cb7074fb8c83af51c14
ms.sourcegitcommit: 58e5d3f4a6cb44607e946f6b931345b6fe237e0e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "110385627"
---
URL qui est utilisée pour notifier le client (à l’aide d’une requête POST) sur les événements suivants :

- Changement de l’état d’indexation : 
    - Propriétés :    
    
        |Nom|Description|
        |---|---|
        |id|L’ID de la vidéo|
        |state|État de la vidéo|  
    - Exemple : https:\//test.com/notifyme?projectName=MyProject&id=1234abcd&state=Processed
- Personne identifiée dans la vidéo :
  - Propriétés
    
      |Nom|Description|
      |---|---|
      |id| L’ID de la vidéo|
      |faceId|ID de visage qui apparaît dans l’index de la vidéo|
      |knownPersonId|ID de la personne qui est unique au sein d’un modèle de visage|
      |personName|Nom de la personne|
        
    - Exemple : https:\//test.com/notifyme?projectName=MyProject&id=1234abcd&faceid=12&knownPersonId=CCA84350-89B7-4262-861C-3CAC796542A5&personName=Inigo_Montoya 
