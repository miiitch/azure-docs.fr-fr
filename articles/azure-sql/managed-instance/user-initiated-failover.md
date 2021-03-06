---
title: Lancer manuellement un basculement sur SQL Managed Instance
description: Découvrez comment basculer manuellement les réplicas principaux et secondaires sur Azure SQL Managed Instance.
services: sql-database
ms.service: sql-managed-instance
ms.custom: seo-lt-2019, sqldbrb=1
ms.devlang: ''
ms.topic: how-to
author: danimir
ms.author: danil
ms.reviewer: douglas, sstein
ms.date: 02/27/2021
ms.openlocfilehash: 3c969c1898e67361e37a825d7976b1c52d08dd24
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "101691142"
---
# <a name="user-initiated-manual-failover-on-sql-managed-instance"></a>Basculement manuel initié par l’utilisateur sur SQL Managed Instance
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

Cet article explique comment basculer manuellement un nœud principal sur des niveaux de service SQL Managed Instance à usage général (GP) et critique pour l’entreprise (BC), et comment basculer manuellement un nœud de réplica secondaire en lecture seule sur le niveau de service BC uniquement.

## <a name="when-to-use-manual-failover"></a>Quand utiliser le basculement manuel

La [haute disponibilité](../database/high-availability-sla.md) est un élément fondamental de SQL Managed Instance ; elle fonctionne de manière transparente pour votre application de base de données. Les basculements entre les nœuds principaux et secondaires en cas de dégradation des nœuds ou de détection des pannes, ou pendant les mises à jour logicielles mensuelles régulières, sont une occurrence attendue pour toutes les applications utilisant SQL Managed Instance dans Azure.

Vous pouvez envisager d’exécuter un [basculement manuel](../database/high-availability-sla.md#testing-application-fault-resiliency) sur SQL Managed Instance pour une des raisons suivantes :
- Application de test pour la résilience du basculement avant le déploiement en production
- Test des systèmes de bout en bout pour la résilience des erreurs sur les basculements automatiques
- Tester l’impact du basculement sur les sessions de base de données existantes
- Vérifier si un basculement modifie les performances de bout en bout en raison des modifications de la latence du réseau
- Dans certains cas de dégradations de performances de requête, un basculement manuel peut vous aider à atténuer le problème de performances.

> [!NOTE]
> En vous assurant que vos applications bénéficient d’un basculement résilient avant le déploiement en production, vous atténuez le risque d’erreurs d’application en production et contribuez à la disponibilité des applications pour vos clients. Apprenez-en davantage sur le test de vos applications pour la préparation au cloud grâce à l’enregistrement vidéo [Testing App Cloud Readiness for Failover Resiliency with SQL Managed Instance](https://youtu.be/FACWYLgYDL8) (Tester la préparation au cloud des applications pour la résilience au basculement avec SQL Managed Instance).

## <a name="initiate-manual-failover-on-sql-managed-instance"></a>Basculement manuel initié sur SQL Managed Instance

### <a name="azure-rbac-permissions-required"></a>Autorisations Azure RBAC requises

L’utilisateur qui initie un basculement doit disposer de l’un des rôles Azure suivants :

- Rôle Propriétaire de l’abonnement ; ou
- Rôle [Contributeur Managed Instance](../../role-based-access-control/built-in-roles.md#sql-managed-instance-contributor), ou
- Rôle personnalisé avec l’autorisation suivante :
  - `Microsoft.Sql/managedInstances/failover/action`

### <a name="using-powershell"></a>Utilisation de PowerShell

La version minimale d’Az.Sql doit être la [v2.9.0](https://www.powershellgallery.com/packages/Az.Sql/2.9.0). Envisagez d’utiliser [Azure Cloud Shell](../../cloud-shell/overview.md) du portail Azure, qui dispose toujours de la dernière version de PowerShell disponible. 

Comme condition préalable, utilisez le script PowerShell suivant pour installer les modules Azure requis. En outre, sélectionnez l’abonnement où se trouve la Managed Instance sur laquelle vous souhaitez basculer.

```powershell
$subscription = 'enter your subscription ID here'
Install-Module -Name Az
Import-Module Az.Accounts
Import-Module Az.Sql

Connect-AzAccount
Select-AzSubscription -SubscriptionId $subscription
```

Utilisez la commande PowerShell [Invoke-AzSqlInstanceFailover](/powershell/module/az.sql/invoke-azsqlinstancefailover) avec l’exemple suivant pour lancer le basculement du nœud principal, applicable à la fois aux niveaux de service BC et GP.

```powershell
$ResourceGroup = 'enter resource group of your MI'
$ManagedInstanceName = 'enter MI name'
Invoke-AzSqlInstanceFailover -ResourceGroupName $ResourceGroup -Name $ManagedInstanceName
```

Utilisez la commande PS suivante pour basculer le nœud secondaire de lecture, applicable uniquement au niveau de service BC.

```powershell
$ResourceGroup = 'enter resource group of your MI'
$ManagedInstanceName = 'enter MI name'
Invoke-AzSqlInstanceFailover -ResourceGroupName $ResourceGroup -Name $ManagedInstanceName -ReadableSecondary
```

### <a name="using-cli"></a>Utiliser l'interface CLI

Veillez à installer les derniers scripts CLI.

Utilisez la commande CLI az sql mi failover avec l’exemple suivant pour lancer le basculement du nœud principal, applicable à la fois aux niveaux de service BC et GP.

```cli
az sql mi failover -g myresourcegroup -n myinstancename
```

Utilisez la commande CLI suivante pour basculer le nœud secondaire de lecture, applicable uniquement au niveau de service BC.

```cli
az sql mi failover -g myresourcegroup -n myinstancename --replica-type ReadableSecondary
```

### <a name="using-rest-api"></a>Utilisation de l’API REST

Pour les utilisateurs expérimentés qui auraient peut-être besoin d’automatiser les basculements de leurs instances SQL Managed Instance à des fins d’implémentation d’un pipeline de test continu ou d’atténuations des performances automatisées, cette fonction peut être obtenue par le biais d’un appel d’API. Pour plus d’informations, consultez [Instances gérées - API REST de basculement](/rest/api/sql/managed%20instances%20-%20failover/failover).

Pour initier un basculement à l’aide d’un appel d’API REST, commencez par générer le jeton d’authentification à l’aide du client API de votre choix. Le jeton d’authentification généré est utilisé comme propriété d’autorisation dans l’en-tête de la requête d’API et il est obligatoire.

Le code suivant est un exemple d’URI d’API à appeler :

```HTTP
POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/managedInstances/{managedInstanceName}/failover?api-version=2019-06-01-preview
```

Les propriétés suivantes doivent être passées dans l’appel d’API :

| **Propriété d’API** | **Paramètre** |
| --- | --- |
| subscriptionId | ID d’abonnement sur lequel l’instance gérée est déployée |
| resourceGroupName | Groupe de ressources qui contient l’instance gérée |
| managedInstanceName | Nom de l’instance gérée |
| replicaType | (Facultatif) (Primary ou ReadableSecondary). Ces paramètres représentent le type de réplica à basculer : principal ou secondaire accessible en lecture. S’il n’est pas spécifié, le basculement est initié sur le réplica principal par défaut. |
| api-version | La valeur est statique et doit être actuellement « 2019-06-01-preview » |

La réponse de l’API sera l’une des deux suivantes :

- 202 Accepté
- Une des erreurs de requête 400.

L’état de l’opération peut être suivi en passant en revue les réponses d’API dans les en-têtes de réponse. Pour plus d’informations, consultez la rubrique [État des opérations asynchrones Azure](../../azure-resource-manager/management/async-operations.md).

## <a name="monitor-the-failover"></a>Surveiller le basculement

Pour superviser la progression du basculement lancé par l’utilisateur pour votre instance BC, exécutez la requête T-SQL suivante dans votre client favori (par exemple, SSMS) sur SQL Managed Instance. Il lira les valeurs sys.dm_hadr_fabric_replica_states de la vue système et indiquera les réplicas disponibles sur l’instance. Actualisez la même requête après avoir lancé le basculement manuel.

```T-SQL
SELECT DISTINCT replication_endpoint_url, fabric_replica_role_desc FROM sys.dm_hadr_fabric_replica_states
```

Avant de lancer le basculement, votre sortie indiquera le réplica principal actuel sur le niveau de service BC contenant un nœud principal et trois secondaires dans le groupe de disponibilité AlwaysOn. Lors de l’exécution d’un basculement, l’exécution de cette requête doit indiquer une modification du nœud principal.

Vous ne serez pas en mesure de voir la même sortie avec le niveau de service de GP que celle indiquée ci-dessus pour BC. Cela est dû au fait que le niveau de service GP est basé sur un seul nœud. Vous pouvez utiliser une autre requête T-SQL indiquant l’heure à laquelle le processus SQL a démarré sur le nœud pour l’instance du niveau de service GP :

```T-SQL
SELECT sqlserver_start_time, sqlserver_start_time_ms_ticks FROM sys.dm_os_sys_info
```

La courte perte de connectivité de votre client pendant le basculement, qui dure généralement moins d’une minute, est l’indication de l’exécution du basculement, quel que soit le niveau de service.

> [!NOTE]
> L’achèvement du processus de basculement (et non la brève indisponibilité) peut prendre plusieurs minutes à la fois en cas de charges de travail à **haute intensité**. Cela est dû au fait que le moteur d’instance s’occupe de toutes les transactions en cours sur le serveur principal et rattrape son retard sur le nœud secondaire, avant d’être en mesure de basculer.

> [!IMPORTANT]
> Les limitations fonctionnelles du basculement manuel initié par l’utilisateur sont les suivantes :
> - Un (1) basculement peut être initié sur la même instance gérée toutes les **15 minutes**.
> - Pour les instances BC, il doit exister un quorum de réplicas pour que la requête de basculement soit acceptée.
> - Pour les instances BC, il n’est pas possible de spécifier le réplica secondaire accessible en lecture sur lequel initier le basculement.
> - Le basculement n’est pas autorisé tant que la première sauvegarde complète d’une nouvelle base de données n’est pas terminée par les systèmes de sauvegarde automatisée.
> - Le basculement ne sera pas autorisé si une restauration de la base de données est en cours.

## <a name="next-steps"></a>Étapes suivantes
- Apprenez-en davantage sur le test de vos applications pour la préparation au cloud grâce à l’enregistrement vidéo [Testing App Cloud Readiness for Failover Resiliency with SQL Managed Instance](https://youtu.be/FACWYLgYDL8) (Tester la préparation au cloud des applications pour la résilience au basculement avec SQL Managed Instance).
- Pour en savoir plus sur la haute disponibilité de Managed instance, consultez [Haute disponibilité pour Azure SQL Managed Instance](../database/high-availability-sla.md).
- Pour obtenir une vue d’ensemble, consultez [Présentation d’Azure SQL Managed Instance](sql-managed-instance-paas-overview.md).
