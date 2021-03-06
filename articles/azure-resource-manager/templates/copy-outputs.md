---
title: Définition de plusieurs instances d’une valeur de sortie
description: Utilisez l’opération copy dans un modèle Azure Resource Manager (modèle ARM) pour retourner une valeur à partir d’un déploiement sur plusieurs itérations.
ms.topic: conceptual
ms.date: 04/01/2021
ms.openlocfilehash: 49050f4c0a494bbfb470b64704a09d8738a727f7
ms.sourcegitcommit: 77d7639e83c6d8eb6c2ce805b6130ff9c73e5d29
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106385732"
---
# <a name="output-iteration-in-arm-templates"></a>Itération de sortie dans les modèles ARM

Cet article explique comment créer plusieurs valeurs pour une sortie dans votre modèle Azure Resource Manager (modèle ARM). En ajoutant la boucle de copie dans la section outputs de votre modèle, vous pouvez retourner dynamiquement plusieurs éléments pendant le déploiement.

Il est également possible d’utiliser la boucle de copie avec des [ressources](copy-resources.md), des [propriétés dans une ressource](copy-properties.md) et des [variables](copy-variables.md).

## <a name="syntax"></a>Syntaxe

# <a name="json"></a>[JSON](#tab/json)

Ajoutez l’élément `copy` à la section de sortie de votre modèle pour renvoyer un certain nombre d’éléments. L’élément copy utilise le format général suivant :

```json
"copy": {
  "count": <number-of-iterations>,
  "input": <values-for-the-output>
}
```

La propriété `count` indique le nombre d’itérations souhaité pour la valeur de sortie.

La propriété `input` spécifie les propriétés que vous souhaitez répéter. Vous créez un tableau d’éléments construits à partir de la valeur de la propriété `input`. Il peut s’agir d’une propriété unique (par exemple, une chaîne) ou d’un objet avec plusieurs propriétés.

# <a name="bicep"></a>[Bicep](#tab/bicep)

Les boucles peuvent être utilisées pour retourner un certain nombre d’éléments pendant le déploiement :

- Itération sur un tableau :

  ```bicep
  output <output-name> array = [for <item> in <collection>: {
    <properties>
  }]

  ```

- Itération sur les éléments d’un tableau

  ```bicep
  output <output-name> array = [for <item>, <index> in <collection>: {
    <properties>
  }]
  ```

- Utilisation de l’index de boucle

  ```bicep
  output <output-name> array = [for <index> in range(<start>, <stop>): {
    <properties>
  }]
  ```

---

## <a name="copy-limits"></a>Limites de copie

Le nombre ne peut pas dépasser 800.

Le nombre ne peut pas être négatif. Il peut être zéro si vous déployez le modèle avec une version récente d’Azure CLI, de PowerShell ou de l’API REST. Plus précisément, vous devez utiliser :

- Azure PowerShell **2.6** ou version ultérieure
- Azure CLI **2.0.74** ou version ultérieure
- API REST version **2019-05-10** ou ultérieure
- Les [déploiements liés](linked-templates.md) doivent utiliser la version **2019-05-10** de l’API ou une version ultérieure pour le type de ressource de déploiement

Les versions antérieures de PowerShell, de l’interface CLI et de l’API REST ne prennent pas en charge le nombre zéro.

## <a name="outputs-iteration"></a>Itération sur les sorties

L’exemple suivant crée un nombre variable de comptes de stockage et retourne un point de terminaison pour chacun d’eux :

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageCount": {
      "type": "int",
      "defaultValue": 2
    }
  },
  "variables": {
    "baseName": "[concat('storage', uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-04-01",
      "name": "[concat(copyIndex(), variables('baseName'))]",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {},
      "copy": {
        "name": "storagecopy",
        "count": "[parameters('storageCount')]"
      }
    }
  ],
  "outputs": {
    "storageEndpoints": {
      "type": "array",
      "copy": {
        "count": "[parameters('storageCount')]",
        "input": "[reference(concat(copyIndex(), variables('baseName'))).primaryEndpoints.blob]"
      }
    }
  }
}
```

# <a name="bicep"></a>[Bicep](#tab/bicep)

```bicep
param storageCount int = 2

var baseName_var = 'storage${uniqueString(resourceGroup().id)}'

resource baseName 'Microsoft.Storage/storageAccounts@2019-04-01' = [for i in range(0, storageCount): {
  name: '${i}${baseName_var}'
  location: resourceGroup().location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'Storage'
  properties: {}
}]

output storageEndpoints array = [for i in range(0, storageCount): reference(${i}${baseName_var}).primaryEndpoints.blob]
```

---

Le modèle précédent retourne un tableau avec les valeurs suivantes :

```json
[
  "https://0storagecfrbqnnmpeudi.blob.core.windows.net/",
  "https://1storagecfrbqnnmpeudi.blob.core.windows.net/"
]
```

L’exemple suivant retourne trois propriétés à partir des nouveaux comptes de stockage.

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageCount": {
      "type": "int",
      "defaultValue": 2
    }
  },
  "variables": {
    "baseName": "[concat('storage', uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-04-01",
      "name": "[concat(copyIndex(), variables('baseName'))]",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {},
      "copy": {
        "name": "storagecopy",
        "count": "[parameters('storageCount')]"
      }
    }
  ],
  "outputs": {
    "storageInfo": {
      "type": "array",
      "copy": {
        "count": "[parameters('storageCount')]",
        "input": {
          "id": "[reference(concat(copyIndex(), variables('baseName')), '2019-04-01', 'Full').resourceId]",
          "blobEndpoint": "[reference(concat(copyIndex(), variables('baseName'))).primaryEndpoints.blob]",
          "status": "[reference(concat(copyIndex(), variables('baseName'))).statusOfPrimary]"
        }
      }
    }
  }
}
```

# <a name="bicep"></a>[Bicep](#tab/bicep)

```bicep
param storageCount int = 2

var baseName_var = 'storage${uniqueString(resourceGroup().id)}'

resource baseName 'Microsoft.Storage/storageAccounts@2019-04-01' = [for i in range(0, storageCount): {
  name: '${i}${baseName_var}'
  location: resourceGroup().location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'Storage'
  properties: {}
}]

output storageInfo array = [for i in range(0, storageCount): {
  id: reference(concat(i, baseName_var), '2019-04-01', 'Full').resourceId
  blobEndpoint: reference(concat(i, baseName_var)).primaryEndpoints.blob
  status: reference(concat(i, baseName_var)).statusOfPrimary
}]
```

---

L’exemple précédent retourne un tableau avec les valeurs suivantes :

```json
[
  {
    "id": "Microsoft.Storage/storageAccounts/0storagecfrbqnnmpeudi",
    "blobEndpoint": "https://0storagecfrbqnnmpeudi.blob.core.windows.net/",
    "status": "available"
  },
  {
    "id": "Microsoft.Storage/storageAccounts/1storagecfrbqnnmpeudi",
    "blobEndpoint": "https://1storagecfrbqnnmpeudi.blob.core.windows.net/",
    "status": "available"
  }
]
```

## <a name="next-steps"></a>Étapes suivantes

- Pour suivre un tutoriel, consultez [Tutoriel : Créer plusieurs instances de ressources grâce à des modèles ARM](template-tutorial-create-multiple-instances.md).
- Pour connaître les autres utilisations de la boucle de copie, consultez :
  - [Itération de ressource dans les modèles ARM](copy-resources.md)
  - [Itération de propriété dans les modèles ARM](copy-properties.md)
  - [Itération de variable dans les modèles ARM](copy-variables.md)
- Pour plus d’informations sur les différentes sections d’un modèle, consultez [Présentation de la structure et de la syntaxe des modèles ARM](template-syntax.md).
- Pour savoir comment déployer votre modèle, consultez [Déployer des ressources avec des modèles ARM et Azure PowerShell](deploy-powershell.md).
