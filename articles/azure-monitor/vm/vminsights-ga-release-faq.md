---
title: Questions fréquentes sur VM Insights (GA) | Microsoft Docs
description: VM Insights est une solution d’Azure qui combine à la fois l’intégrité et l’analyse des performances du système d’exploitation de la machine virtuelle Azure. En outre, elle identifie automatiquement les composants des applications et leurs dépendances avec les autres ressources, et effectue le mappage de leurs communications respectives. Cet article répond aux questions courantes au sujet de la version en disponibilité générale.
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 01/31/2020
ms.openlocfilehash: fbef73bfe8058110277b200b8c4091fcde110c04
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102031866"
---
# <a name="vm-insights-generally-available-ga-frequently-asked-questions"></a>Questions fréquentes sur la disponibilité générale (GA) de VM Insights
Ces Questions fréquentes (FAQ) sur la disponibilité générale couvrent les modifications apportées au 4e trimestre 2019 et au 1er trimestre 2020, lors de la préparation pour la disponibilité générale.

## <a name="updates-for-vm-insights"></a>Mises à jour de VM Insights
Nous avons publié une nouvelle version de VM Insights en janvier 2020, avant l’annonce de disponibilité générale. Les clients qui activeront VM Insights recevront désormais la version de disponibilité générale. Les clients existants qui utilisent la version de VM Insights du quatrième trimestre de 2019 ou une version antérieure seront invités à effectuer une mise à niveau. Ce FAQ vous aidera à effectuer une mise à niveau à grande échelle si vos déploiements sont volumineux sur plusieurs espaces de travail.


Avec cette mise à niveau, les données de performances VM Insights sont stockées dans la même table *InsightsMetrics* que [Container Insights](../containers/container-insights-overview.md), ce qui vous permet d’interroger plus facilement les deux jeux de données. De plus, cette table vous permet de stocker des jeux de données plus diversifiés que la table utilisée auparavant. 

Nos affichages de performances utilisent désormais les données que nous stockons dans la table *InsightsMetrics*.  Si vous n’avez pas encore effectué la mise à niveau pour utiliser la dernière solution VMInsights sur votre espace de travail, vos graphiques n’afficheront plus d’informations.  Vous pouvez effectuer la mise à niveau à partir de notre page **Prise en main**, comme décrit ci-dessous.


## <a name="what-is-changing"></a>Qu’est-ce qui change ?
Nous avons publié une nouvelle solution, appelée VMInsights, qui offre des fonctionnalités supplémentaires pour la collecte des données ainsi qu’un nouvel emplacement de stockage de ces données dans votre espace de travail Log Analytics. 

Auparavant, nous avons activé la solution ServiceMap sur votre espace de travail et configuré les compteurs de performance dans votre espace de travail Log Analytics pour envoyer les données à la table de *Perf*. Cette nouvelle solution envoie les données à une table nommée *InsightsMetrics* qui est également utilisée par Container Insights. Le schéma de cette table nous permet de stocker des métriques et des jeux de données de service supplémentaires qui ne sont pas compatibles avec le format de la table *Perf*.

Nous avons mis à jour nos graphiques de performances afin d’utiliser les données que nous stockons dans la table *InsightsMetrics*. Vous pouvez effectuer la mise à niveau pour utiliser la table *InsightsMetrics* à partir de notre page **Prise en main**, comme décrit ci-dessous.


## <a name="how-do-i-upgrade"></a>Comment effectuer la mise à niveau ?
Lorsqu’un espace de travail Log Analytics est mis à niveau vers la dernière version d’Azure Monitor sur des machines virtuelles, il met à niveau l’agent de dépendances sur chacune des machines virtuelles attachées à cet espace de travail. Chaque machine virtuelle nécessitant une mise à niveau est identifiée dans l’onglet **Démarrage** de VM Insights dans le portail Azure. Lorsque vous choisissez de mettre à niveau une machine virtuelle, cela met à niveau l’espace de travail pour cette machine virtuelle, ainsi que toutes les autres machines virtuelles attachées à cet espace de travail. Vous pouvez sélectionner une machine virtuelle unique ou plusieurs machines virtuelles, groupes de ressources ou abonnements. 

Utilisez la commande suivante pour mettre à niveau un espace de travail à l’aide de PowerShell :

```PowerShell
Set-AzOperationalInsightsIntelligencePack -ResourceGroupName <resource-group-name> -WorkspaceName <workspace-name> -IntelligencePackName "VMInsights" -Enabled $True
```

## <a name="what-should-i-do-about-the-performance-counters-in-my-workspace-if-i-install-the-vminsights-solution"></a>Que faire avec les compteurs de performances de mon espace de travail si j’installe la solution VMInsights ?

La méthode précédente d’activation de VM Insights utilisait des compteurs de performances dans votre espace de travail. La version actuelle stocke ces données dans une table nommée `InsightsMetrics`. Vous pouvez choisir de désactiver ces compteurs de performances dans votre espace de travail si vous n’en avez plus besoin. 

>[!NOTE]
>Si vous utilisez des règles d’alerte qui font référence à ces compteurs dans la table `Perf`, vous devez les mettre à jour pour qu’elles référencent les nouvelles données stockées dans la table `InsightsMetrics`. Consultez notre documentation pour obtenir et réutiliser des exemples de requêtes sur des journaux qui font référence à cette table.
>

Si vous préférez garder les compteurs de performances activés, les données ingérées et stockées dans la table `Perf` vous seront facturées, sur la base de [la tarification Log Analytics[(https://azure.microsoft.com/pricing/details/monitor/).

## <a name="how-will-this-change-affect-my-alert-rules"></a>Quel impact ce changement aura-t-il sur mes règles d’alerte ?

Si vous avez créé des [alertes de journal](../alerts/alerts-unified-log.md) qui interrogent la table `Perf` en ciblant les compteurs de performances activés dans l’espace de travail, vous devez mettre à jour ces règles pour qu’elles fassent référence à la table `InsightsMetrics` à la place. Ce conseil s’applique aussi à toutes les règles de recherche dans les journaux qui utilisent `ServiceMapComputer_CL` et `ServiceMapProcess_CL`, car ces jeux de données sont transférés vers les tables `VMComputer` et `VMProcess`.

Nous mettrons à jour ces questions fréquentes et notre documentation pour inclure des exemples de règles d’alerte de recherche dans les journaux pour les jeux de données que nous collectons.

## <a name="how-will-this-change-affect-my-bill"></a>Quel impact ce changement aura-t-il sur ma facture ?

La facturation reste basée sur la quantité de données ingérées et conservées dans votre espace de travail Log Analytics.

Les données de performances des machines que nous collectons sont les mêmes, ont une taille similaire aux données que nous stockions dans la table `Perf` et représentent à peu près le même coût.

## <a name="what-if-i-only-want-to-use-service-map"></a>Puis-je utiliser uniquement la solution Service Map ?

Bien sûr. Des invites sur la prochaine mise à jour s’afficheront dans le portail Azure quand vous accéderez à VM Insights. Une fois la nouvelle solution publiée, vous recevrez une invite vous demandant de mettre à niveau votre version. Si vous préférez utiliser uniquement la fonctionnalité [Maps](vminsights-maps.md), vous pouvez choisir de ne pas effectuer la mise à niveau et de continuer à utiliser la fonctionnalité Maps dans VM Insights et la solution Service Map accessible à partir de votre espace de travail ou de la vignette du tableau de bord.

Si vous choisissez d’activer manuellement les compteurs de performances dans votre espace de travail, vous pourrez peut-être voir les données de certains graphiques de performances à partir d’Azure Monitor. Après avoir publié la nouvelle solution, nous mettrons à jour nos graphiques de performances afin qu’ils fassent les requêtes sur les données stockées dans la table `InsightsMetrics`. Pour voir les données de cette table représentées dans ces graphiques, vous devrez effectuer la mise à niveau vers la nouvelle version de VM Insights.

Le déplacement des données de `ServiceMapComputer_CL` et `ServiceMapProcess_CL` a des répercussions sur Service Map et sur VM Insights. Vous devez donc toujours planifier cette mise à jour.

Si vous choisissez de ne pas effectuer la mise à niveau vers la solution **VMInsights**, vous pourrez continuer à utiliser les versions précédentes de nos classeurs de performances qui font référence aux données de la table `Perf`.  

## <a name="will-the-service-map-data-sets-also-be-stored-in-insightsmetrics"></a>Les jeux de données de Service Map seront-ils également stockés dans InsightsMetrics ?

Les jeux de données ne seront pas dupliqués si vous utilisez les deux solutions. Ces solutions partagent les jeux de données stockés dans les tables `VMComputer` (anciennement ServiceMapComputer_CL), `VMProcess` (anciennement ServiceMapProcess_CL), `VMConnection` et `VMBoundPort`, où sont stockés les jeux de données cartographiques que nous collectons.  

La table `InsightsMetrics` stockera les jeux de données des machines virtuelles, des processus et des services que nous collectons et sera renseignée uniquement si vous utilisez les insights de machines virtuelles et la solution VM Insights. La solution Service Map ne collectera ni ne stockera de données dans la table `InsightsMetrics`.

## <a name="will-i-be-double-charged-if-i-have-the-service-map-and-vminsights-solutions-in-my-workspace"></a>Serai-je facturé à la fois pour la solution Service Map et la solution VMInsights si j’utilise les deux dans mon espace de travail ?

Non, les deux solutions partagent les jeux de données cartographiques que nous stockons dans les tables `VMComputer` (anciennement ServiceMapComputer_CL), `VMProcess` (anciennement ServiceMapProcess_CL), `VMConnection` et `VMBoundPort`. Ces données ne vous seront donc pas facturées deux fois si vous utilisez les deux solutions dans votre espace de travail.

## <a name="if-i-remove-either-the-service-map-or-vminsights-solution-will-it-remove-my-data"></a>Si je supprime la solution Service Map ou VMInsights, mes données seront-elles supprimées ?

Non, les deux solutions partagent les jeux de données cartographiques que nous stockons dans les tables `VMComputer` (anciennement ServiceMapComputer_CL), `VMProcess` (anciennement ServiceMapProcess_CL), `VMConnection` et `VMBoundPort`. Si vous supprimez l’une des solutions, ces jeux de données identifient qu’il reste une solution en place qui utilise les données et les conserve dans l’espace de travail Log Analytics. Les données sont supprimées de votre espace de travail seulement si vous supprimez les deux solutions.

## <a name="health-feature-is-in-limited-public-preview"></a>La fonctionnalité Intégrité est disponible en préversion publique limitée

Nos clients ont été nombreux à nous adresser d’excellents commentaires au sujet de notre fonctionnalité Intégrité pour les machines virtuelles. Cette fonctionnalité suscite un intérêt important en raison de son potentiel de prise en charge des workflows d’analyse. Nous prévoyons d’effectuer toute une série de changements afin d’améliorer la fonctionnalité et de répondre aux attentes de nos clients. 

Afin de minimiser l’impact de ces changements pour les nouveaux clients, nous avons rendu cette fonctionnalité disponible en **préversion publique limitée**. Cette mise à jour a eu lieu en octobre 2019.

Nous prévoyons de relancer la fonctionnalité d’intégrité en 2020, après la disponibilité générale de VM Insights.

## <a name="how-do-existing-customers-access-the-health-feature"></a>Comment les clients existants accéderont-ils à la fonctionnalité Intégrité ?

Les clients existants qui utilisent la fonctionnalité Intégrité continueront d’y accéder normalement. En revanche, les nouveaux clients n’y auront pas accès.  

Pour accéder à la fonctionnalité, vous pouvez ajouter l’indicateur de fonctionnalité `feature.vmhealth=true` à l’URL du Portail Azure [https://portal.azure.com](https://portal.azure.com). Par exemple : `https://portal.azure.com/?feature.vmhealth=true`.

Vous pouvez aussi utiliser cette courte URL, qui définit l’indicateur de fonctionnalité automatiquement : [https://aka.ms/vmhealthpreview](https://aka.ms/vmhealthpreview).

Si vous faites partie des clients existants, vous pouvez continuer à utiliser la fonctionnalité Intégrité sur les machines virtuelles qui sont connectées à une configuration d’espace de travail existante dotée de la fonctionnalité Intégrité.  

## <a name="i-use-vm-health-now-with-one-environment-and-would-like-to-deploy-it-to-a-new-one"></a>J’utilise actuellement la fonctionnalité Intégrité des machines virtuelles et je souhaite la déployer dans un nouvel environnement

Si vous êtes un client existant qui utilise déjà la fonctionnalité Intégrité et que vous souhaitez l’utiliser dans le cadre d’un nouveau lancement, contactez-nous à l’adresse vminsights@microsoft.com pour demander des instructions.

## <a name="next-steps"></a>Étapes suivantes

Pour comprendre les exigences et méthodes qui vous aident à analyser vos machines virtuelles, consultez la section [Déployer VM Insights](./vminsights-enable-overview.md).
