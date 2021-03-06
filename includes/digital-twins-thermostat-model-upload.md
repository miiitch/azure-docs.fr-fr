---
author: baanders
description: inclure un fichier pour charger un modèle sur une instance Azure Digital Twins
ms.service: digital-twins
ms.topic: include
ms.date: 4/1/2021
ms.author: baanders
ms.openlocfilehash: 3a9ec169f91ebe048914c3ef2163e4fde7485389
ms.sourcegitcommit: 32ee8da1440a2d81c49ff25c5922f786e85109b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2021
ms.locfileid: "109783667"
---
Le modèle se présente ainsi :
:::code language="json" source="~/digital-twins-docs-samples/models/Thermostat.json":::

Pour **charger ce modèle dans votre instance Twins**, exécutez la commande Azure CLI suivante, qui charge le modèle ci-dessus en tant que JSON inline. Vous pouvez exécuter la commande dans [Azure Cloud Shell](../articles/cloud-shell/overview.md) dans votre navigateur (utilisez l’environnement **Bash**) ou sur votre machine si l’interface CLI est [installée localement](/cli/azure/install-azure-cli).

```azurecli-interactive
az dt model create --models '{  "@id": "dtmi:contosocom:DigitalTwins:Thermostat;1",  "@type": "Interface",  "@context": "dtmi:dtdl:context;2",  "contents": [    {      "@type": "Property",      "name": "Temperature",      "schema": "double"    }  ]}' --dt-name {digital_twins_instance_name}
```