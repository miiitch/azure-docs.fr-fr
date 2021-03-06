---
title: Obtenir l’état des traductions
titleSuffix: Azure Cognitive Services
description: La méthode get translations status retourne une liste des demandes de lots soumises et l’état de chaque demande.
services: cognitive-services
author: jann-skotdal
manager: nitinme
ms.service: cognitive-services
ms.subservice: translator-text
ms.topic: reference
ms.date: 04/21/2021
ms.author: v-jansk
ms.openlocfilehash: c3301283f0a7334a7c207ff7c80b4f71a13de465
ms.sourcegitcommit: 2aeb2c41fd22a02552ff871479124b567fa4463c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107864826"
---
# <a name="get-translations-status"></a>Obtenir l’état des traductions

La méthode get translations status retourne une liste des demandes de lots soumises et l’état de chaque demande. Cette liste contient uniquement les demandes de lots soumises par l’utilisateur (en fonction de l’abonnement). L’état de chaque demande est trié par ID.

Si le nombre de demandes dépasse notre limite de pagination, la pagination côté serveur est utilisée. Les réponses paginées indiquent un résultat partiel et incluent un jeton de continuation dans la réponse. L’absence de jeton de continuation signifie qu’aucune page supplémentaire n’est disponible.

Les paramètres de requête $top et $skip peuvent être utilisés pour spécifier un nombre de résultats à retourner et un décalage pour la collection.

Le serveur honore les valeurs spécifiées par le client. Toutefois, les clients doivent être prêts à gérer les réponses qui contiennent une taille de page différente ou un jeton de continuation.

Lorsque $top et $skip sont tous deux inclus, le serveur doit d’abord appliquer $skip, puis $top sur la collection. 

> [!NOTE]
> Si le serveur ne peut pas honorer $top et/ou $skip, il doit retourner une erreur au client afin de l’en informer au lieu d’ignorer simplement les options de requête. Cela réduit le risque que le client émette des hypothèses quant aux données retournées.

## <a name="request-url"></a>URL de la demande

Envoyez une demande `GET` à :
```HTTP
GET https://<NAME-OF-YOUR-RESOURCE>.cognitiveservices.azure.com/translator/text/batch/v1.0-preview.1/batches
```

Découvrez comment déterminer votre [nom de domaine personnalisé](../get-started-with-document-translation.md#find-your-custom-domain-name).

> [!IMPORTANT]
>
> * **Toutes les requêtes d’API adressées au service Traduction de documentation nécessitent un point de terminaison de domaine personnalisé**.
> * Vous ne pouvez pas utiliser le point de terminaison qui se trouve dans la page _Clés et point de terminaison_ de votre ressource du portail Azure, ni le point de terminaison du traducteur global (`api.cognitive.microsofttranslator.com`) pour soumettre des requêtes HTTP au service Traduction de documentation.

## <a name="request-parameters"></a>Paramètres de la demande

Les paramètres de demande transmis à la chaîne de requête sont les suivants :

|Paramètre de requête.|Obligatoire|Description|
|--- |--- |--- |
|$skip|False|Ignorer les entrées $skip dans la collection. Lorsque $top et $skip sont tous deux fournis, $skip est appliqué en premier.|
|$top|False|Prendre les entrées $top dans la collection. Lorsque $top et $skip sont tous deux fournis, $skip est appliqué en premier.|

## <a name="request-headers"></a>En-têtes de requête

Les en-têtes de requête sont les suivants :

|headers|Description|
|--- |--- |
|Ocp-Apim-Subscription-Key|En-tête de requête obligatoire|

## <a name="response-status-codes"></a>Codes d’état de réponse

Voici les codes d’état HTTP qu’une demande peut retourner.

|Code d’état|Description|
|--- |--- |
|200|OK. Demande réussie, et retourne l’état de toutes les opérations. HeadersRetry-After: integerETag: string|
|400|Demande incorrecte. Demande non valide. Vérifiez les paramètres d’entrée.|
|401|Non autorisé. Vérifiez vos informations d’identification.|
|500|Erreur interne du serveur.|
|Autres codes d’état|<ul><li>Trop de demandes</li><li>Serveur temporairement indisponible</li></ul>|

## <a name="get-translations-status-response"></a>Réponse de get translations status

### <a name="successful-get-translations-status-response"></a>Réponse positive de get translations status

Les informations suivantes sont retournées dans une réponse positive.

|Nom|Type|Description|
|--- |--- |--- |
|id|string|ID de l'opération.|
|createdDateTimeUtc|string|Date et heure de création de l’opération.|
|lastActionDateTimeUtc|string|Date et heure de mise à jour de l’état de l’opération.|
|status|String|Liste des états possibles pour un travail ou un document. <ul><li>Opération annulée</li><li>Cancelling</li><li>Failed</li><li>NotStarted</li><li>En cours d’exécution</li><li>Succès</li><li>ValidationFailed</li></ul>|
|Récapitulatif|StatusSummary[]|Résumé contenant les détails listés ci-dessous.|
|summary.total|entier|Nombre total de documents.|
|summary.failed|entier|Nombre de documents ayant échoué.|
|summary.success|entier|Nombre de documents traduits avec succès.|
|summary.inProgress|entier|Nombre de documents en cours de traitement.|
|summary.notYetStarted|entier|Nombre de documents dont le traitement n’a pas encore commencé.|
|summary.cancelled|entier|Nombre de documents annulés.|
|summary.totalCharacterCharged|entier|Nombre total de caractères facturés.|

### <a name="error-response"></a>Réponse d’erreur

|Nom|Type|Description|
|--- |--- |--- |
|code|string|Enums contenant des codes d’erreur généraux. Valeurs possibles :<br/><ul><li>InternalServerError</li><li>InvalidArgument</li><li>InvalidRequest</li><li>RequestRateTooHigh</li><li>ResourceNotFound</li><li>ServiceUnavailable</li><li>Non autorisé</li></ul>|
|message|string|Obtient un message d’erreur général.|
|target|string|Obtient la source de l’erreur. Par exemple, il s’agirait de « documents » ou « document id » dans le cas d’un document non valide.|
|innerError|InnerErrorV2|Nouveau format d’erreur interne, conforme aux instructions de l’API Cognitive Services. Il contient les propriétés obligatoires ErrorCode, message et les propriétés facultatives target, details(paire clé-valeur), et l’erreur interne (qui peut être imbriquée).|
|innerError.code|string|Obtient la chaîne d’erreur de code.|
|innerError.message|string|Obtient un message d’erreur général.|

## <a name="examples"></a>Exemples

### <a name="example-successful-response"></a>Exemple de réponse positive

Voici un exemple de réponse positive :

```JSON
{
  "value": [
    {
      "id": "727bf148-f327-47a0-9481-abae6362f11e",
      "createdDateTimeUtc": "2020-03-26T00:00:00Z",
      "lastActionDateTimeUtc": "2020-03-26T01:00:00Z",
      "status": "Succeeded",
      "summary": {
        "total": 10,
        "failed": 1,
        "success": 9,
        "inProgress": 0,
        "notYetStarted": 0,
        "cancelled": 0,
        "totalCharacterCharged": 0
      }
    }
  ]
}
```

### <a name="example-error-response"></a>Exemple de réponse d’erreur

Voici un exemple de réponse d’erreur : Le schéma des autres codes d’erreur est le même.

Code d’état : 500

```JSON
{
  "error": {
    "code": "InternalServerError",
    "message": "Internal Server Error",
    "target": "Operation",
    "innerError": {
      "code": "InternalServerError",
      "message": "Unexpected internal server error has occurred"
    }
  }
}
```

## <a name="next-steps"></a>Étapes suivantes

Suivez notre guide de démarrage rapide pour en savoir plus sur l’utilisation du service Traduction de document et de la bibliothèque de client.

> [!div class="nextstepaction"]
> [Bien démarrer avec la traduction de documentation](../get-started-with-document-translation.md)
