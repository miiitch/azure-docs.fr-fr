---
title: Vue d’ensemble du Centre de sauvegarde
description: Cet article fournit une vue d’ensemble du Centre de sauvegarde pour Azure.
ms.topic: conceptual
ms.date: 09/30/2020
ms.openlocfilehash: b42bb2719d03108212f62428dc97ed814899c63c
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "102506046"
---
# <a name="overview-of-backup-center"></a>Vue d’ensemble du Centre de sauvegarde

Le Centre de sauvegarde fournit une **expérience de gestion unifiée unique** dans Azure pour permettre aux entreprises de gouverner, de surveiller, d’opérer et d’analyser les sauvegardes à grande échelle. De ce fait, il est cohérent avec les expériences de gestion natives d’Azure.

Voici quelques-uns des principaux avantages du Centre de sauvegarde :

* **Volet unique pour gérer les sauvegardes** : le Centre de sauvegarde est conçu pour bien fonctionner dans un environnement Azure distribué de grande taille. Vous pouvez utiliser le Centre de sauvegarde pour gérer efficacement les sauvegardes couvrant plusieurs types de charges de travail, coffres, abonnements, régions et locataires [Azure Lighthouse](../lighthouse/overview.md).
* **Gestion centrée sur la source de données** : le Centre de sauvegarde fournit des vues et des filtres centrés sur les sources de données que vous sauvegardez (par exemple, les machines virtuelles et les bases de données). Cela permet à un propriétaire de ressources ou à un administrateur de sauvegarde de surveiller et d’exploiter des sauvegardes d’éléments sans avoir à se concentrer sur le coffre dans lequel un élément est sauvegardé. Une fonctionnalité clé de cette conception est la possibilité de filtrer des affichages en fonction de propriétés spécifiques de la source de donnée, telles que son abonnement, son groupe de ressources et ses balises. Par exemple, si votre organisation a pour habitude d’attribuer des étiquettes différentes à des machines virtuelles qui appartiennent à différents services, vous pouvez utiliser le Centre de sauvegarde afin de filtrer les informations de sauvegarde en fonction des étiquettes des machines virtuelles sous-jacentes sauvegardées, sans avoir à vous préoccuper de l’étiquette du coffre.
* **Expériences connectées** : le Centre de sauvegarde fournit des intégrations natives à des services Azure existants qui permettent une gestion à grande échelle. Par exemple, le Centre de sauvegarde utilise l’expérience [Azure Policy](../governance/policy/overview.md) pour vous aider à gérer vos sauvegardes. Il tire également parti de [classeurs Azure](../azure-monitor/visualize/workbooks-overview.md) et de [journaux Azure Monitor](../azure-monitor/logs/data-platform-logs.md) pour vous aider à afficher des rapports détaillés sur les sauvegardes. Vous n’avez donc pas besoin d’apprendre de nouveaux principes pour utiliser les diverses fonctionnalités qu’offre le Centre de sauvegarde. Vous pouvez également découvrir les ressources de la communauté dans le Centre de sauvegarde.

## <a name="supported-scenarios"></a>Scénarios pris en charge

* Le Centre de sauvegarde est actuellement pris en charge pour la sauvegarde des machines virtuelles Azure, la sauvegarde des machines virtuelles SQL dans Azure, la sauvegarde des machines virtuelles SAP HANA dans Azure, la sauvegarde Azure Files, la sauvegarde des blobs Azure, la sauvegarde des disques managés Azure et la sauvegarde des serveurs Azure Database pour PostgreSQL.
* Pour obtenir une liste détaillée des scénarios pris en charge et non pris en charge, consultez la [Matrice de prise en charge](backup-center-support-matrix.md).

## <a name="get-started"></a>Bien démarrer

Pour bien démarrer avec l’utilisation du Centre de sauvegarde, recherchez **Centre de sauvegarde** dans le portail Azure, puis accédez au tableau de bord du **Centre de sauvegarde**.

![Recherche dans le Centre de sauvegarde](./media/backup-center-overview/backup-center-search.png)

Le premier écran qui s’affiche est la **Vue d’ensemble**. Il contient deux vignettes : **Travaux** et **Instances de sauvegarde**.

![Vignettes du Centre de sauvegarde](./media/backup-center-overview/backup-center-overview-widgets.png)

La vignette **Travaux** affiche une synthèse de tous les travaux de sauvegarde et de restauration associés déclenchés au sein de votre espace de sauvegarde au cours des dernières 24 heures. Vous pouvez afficher des informations sur le nombre de travaux terminés, en échec et en cours. La sélection de l’un des nombres dans cette vignette vous permet d’afficher des informations supplémentaires sur les travaux pour un type de source de données, un type d’opération et un état spécifiques.

La vignette **Instances de sauvegarde** affiche une synthèse de toutes les instances de sauvegarde dans votre espace de sauvegarde. Par exemple, vous pouvez voir le nombre d’instances de sauvegarde en état de suppression réversible par rapport au nombre d’instances toujours configurées pour la protection. La sélection de l’un des nombres figurant dans cette vignette vous permet d’afficher des informations supplémentaires sur les instances de sauvegarde pour un type de source de données et un état de protection spécifiques. Vous pouvez également afficher toutes les instances de sauvegarde dont la source des données sous-jacente est introuvable (la source des données peut être supprimée ou vous n’avez peut-être pas accès à la source des données).

Regardez la vidéo suivante pour comprendre les fonctionnalités du Centre de sauvegarde :

> [!VIDEO https://www.youtube.com/embed/pFRMBSXZcUk?t=497]

Effectuez les [étapes suivantes](#next-steps) pour comprendre les différentes fonctionnalités qu’offre le Centre de sauvegarde et la manière de les utiliser pour gérer efficacement votre espace de sauvegarde.

## <a name="next-steps"></a>Étapes suivantes

* [Surveiller et exécuter des sauvegardes](backup-center-monitor-operate.md)
* [Gérer votre espace de sauvegarde](backup-center-govern-environment.md)
* [Obtenir des insights sur vos sauvegardes](backup-center-obtain-insights.md)
* [Effectuer des actions à l’aide du Centre de sauvegarde](backup-center-actions.md)