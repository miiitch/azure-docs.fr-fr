---
title: Exigences liées aux schémas de données
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mrbullwinkle
manager: nitinme
ms.service: cognitive-services
ms.subservice: metrics-advisor
ms.topic: include
ms.date: 09/10/2020
ms.author: mbullwin
ms.openlocfilehash: 4c55c25621df1925b6ed6c374d8af88551eb1e46
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "96231427"
---
Metrics Advisor est un service conçu pour la détection, le diagnostic et l’analyse des anomalies dans les séries chronologiques. En tant que service basé sur l’intelligence artificielle, il utilise vos données pour entraîner le modèle utilisé. Ce service accepte des tables de données agrégées avec les colonnes suivantes :

* **Mesure** (obligatoire) : une ou plusieurs colonnes contenant des valeurs numériques.
* **Horodatage** (facultatif) : zéro ou une colonne de type `DateTime` ou `String`. Lorsque cette colonne n’est pas définie, l’horodatage est défini comme heure de début de chaque période d’ingestion. Mettez l’horodatage sous la forme : `yyyy-MM-ddTHH:mm:ssZ`. 
  * **Votre horodatage doit correspondre à la précision de la métrique. Par exemple, une métrique quotidienne doit garantir l’heure, la minute et la seconde sur l’horodatage étiqueté comme `00:00:00`** .
* **Dimension** (facultatif) : Les colonnes peuvent avoir un type de données quelconque. Soyez prudent lorsque vous travaillez avec de grands volumes de colonnes et de valeurs, afin d’éviter le traitement d’un nombre excessif de dimensions.

> [!Note]
> Pour chaque métrique, un seul horodatage doit être utilisé par mesure, correspondant à une seule combinaison de dimensions. Agrégez vos données avant leur intégration ou utilisez la requête pour spécifier les données à ingérer.