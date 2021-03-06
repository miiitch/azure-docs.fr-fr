---
title: 'L’interface de ligne de commande Azure CLI : Créer une base de données unique'
description: Utilisez cet exemple de script Azure CLI pour créer une base de données unique.
services: sql-database
ms.service: sql-database
ms.subservice: single-database
ms.custom: sqldbrb=1, devx-track-azurecli
ms.devlang: azurecli
ms.topic: sample
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 06/25/2019
ms.openlocfilehash: 00346accbccd67f542a8496ac097b0236c56a08c
ms.sourcegitcommit: 4b0e424f5aa8a11daf0eec32456854542a2f5df0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107773816"
---
# <a name="use-the-azure-cli-to-create-a-single-database-and-configure-a-firewall-rule"></a>Utiliser Azure CLI pour créer une base de données unique et configurer une règle de pare-feu

[!INCLUDE[appliesto-sqldb](../../includes/appliesto-sqldb.md)]

Cet exemple de script Azure CLI crée une base de données unique dans Azure SQL Database et configure une règle de pare-feu au niveau du serveur. Une fois que le script a été exécuté avec succès, la base de données est accessible à partir de tous les services Azure et de l’adresse IP configurée.

Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article. Exécutez `az --version` pour trouver la version. Si vous devez effectuer une installation ou une mise à niveau, consultez [Installer Azure CLI]( /cli/azure/install-azure-cli).

## <a name="sample-script"></a>Exemple de script

### <a name="sign-in-to-azure"></a>Connexion à Azure

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

### <a name="run-the-script"></a>Exécuter le script

[!code-azurecli-interactive[main](../../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh "Create SQL Database")]

### <a name="clean-up-deployment"></a>Nettoyer le déploiement

Utilisez la commande suivante pour supprimer le groupe de ressources et toutes les ressources associées.

```azurecli-interactive
az group delete --name $resource
```

## <a name="sample-reference"></a>Informations de référence sur l’exemple

Ce script utilise les commandes suivantes. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Description |
|---|---|
| [az sql server](/cli/azure/sql/server#az_sql_server_create) | Commandes de serveur |
| [az sql server firewall](/cli/azure/sql/server/firewall-rule#az_sql_server_firewall_rule_create) | Commandes de pare-feu de serveur. |
| [az sql db](/cli/azure/sql/db#az_sql_db_create) | Commandes de base de données. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure).

Vous trouverez des exemples supplémentaires de scripts CLI SQL Database dans [Documentation Azure SQL Database](../az-cli-script-samples-content-guide.md).
