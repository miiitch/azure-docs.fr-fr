---
author: gvashishtha
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: include
ms.date: 04/21/2021
ms.author: gopalv
ms.openlocfilehash: 30237f94d5961d853509e303f50be1e8a42de9b0
ms.sourcegitcommit: 42ac9d148cc3e9a1c0d771bc5eea632d8c70b92a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2021
ms.locfileid: "109846101"
---
Le script d’entrée reçoit les données envoyées à un service web déployé, puis les passe au modèle. Il renvoie ensuite la réponse du modèle au client. *Le script est propre à votre modèle*. Le script d'entrée doit comprendre les données que le modèle attend et renvoie.

Les deux choses que vous devez accomplir dans votre script d’entrée sont les suivantes :

1. Charger votre modèle (à l’aide d’une fonction appelée `init()`)
1. Exécuter votre modèle sur des données d’entrée (à l’aide d’une fonction appelée `run()`)

Pour votre déploiement initial, utilisez un script d'entrée factice qui imprime les données qu'il reçoit.

<!-- ```python
import json

def init():
    print('This is init')

def run(data):
    test = json.loads(data)
    print(f'received data {test}')
    return(f'test is {test}')

``` -->

:::code language="python" source="~/azureml-examples-main/python-sdk/tutorials/deploy-local/source_dir/echo_score.py":::

Enregistrez ce fichier sous le nom `echo_score.py` dans un répertoire appelé `source_dir`.

Par exemple, si un utilisateur appelle votre modèle avec :

```bash
curl -X POST -d '{"this":"is a test"}' -H "Content-Type: application/json" http://localhost:6789/score
```

La valeur suivante est renvoyée :

```bash
"test is {'this': 'is a test'}"
```