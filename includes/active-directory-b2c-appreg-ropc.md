---
author: msmimart
ms.service: active-directory-b2c
ms.subservice: B2C
ms.topic: include
ms.date: 10/16/2019
ms.author: mimart
ms.openlocfilehash: 38261556579fb5db86fb231b0edf3412eed51d35
ms.sourcegitcommit: 73fb48074c4c91c3511d5bcdffd6e40854fb46e5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106073237"
---
Pour inscrire une application dans votre locataire Azure AD B2C, vous pouvez utiliser notre nouvelle expérience unifiée **Inscriptions d’applications** ou notre expérience héritée **Applications (héritées)** . [En savoir plus sur la nouvelle expérience](../articles/active-directory-b2c/app-registrations-training-guide.md).

#### <a name="app-registrations"></a>[Inscriptions des applications](#tab/app-reg-ga/)

1. Connectez-vous au [portail Azure](https://portal.azure.com).
1. Sélectionnez le filtre **Annuaire et abonnement** dans le menu supérieur, puis l’annuaire qui contient votre locataire Azure AD B2C.
1. Dans le menu de gauche, sélectionnez **Azure AD B2C**. Ou sélectionnez **Tous les services**, puis recherchez et sélectionnez **Azure AD B2C**.
1. Sélectionnez **Inscriptions d’applications**, puis **Nouvelle inscription**.
1. Entrez un **Nom** pour l’application. Par exemple, *ROPC_Auth_app*.
1. Laissez les autres valeurs telles quelles, puis sélectionnez **Inscrire**.
1. Enregistrez l’**ID d’application (client)** pour l’utiliser dans une étape ultérieure.
1. Sous **Gérer**, sélectionnez **Authentification**.
1. Sélectionnez **Essayer la nouvelle expérience** (si elle est indiquée).
1. Sous **Type de client par défaut**, sélectionnez **Oui** pour considérer l’application comme un client public. Ce paramètre est obligatoire pour le flux ROPC.
1. Sélectionnez **Enregistrer**.
1. Dans le menu de gauche, sélectionnez **Manifeste** pour ouvrir l’éditeur de manifeste. 
1. Définissez l’attribut **oauth2AllowImplicitFlow** sur *true* :
    ```json
    "oauth2AllowImplicitFlow": true,
    ```
1. Sélectionnez **Enregistrer**.

#### <a name="applications-legacy"></a>[Applications (héritées)](#tab/applications-legacy/)

1. Connectez-vous au [portail Azure](https://portal.azure.com).
1. Sélectionnez le filtre **Annuaire et abonnement** dans le menu supérieur, puis l’annuaire qui contient votre locataire Azure AD B2C.
1. Dans le menu de gauche, sélectionnez **Azure AD B2C**. Ou sélectionnez **Tous les services**, puis recherchez et sélectionnez **Azure AD B2C**.
1. Sélectionnez **Applications (héritées)** , puis **Ajouter**.
1. Entrez un nom pour l’application. Par exemple, *ROPC_Auth_app*.
1. Pour **Client natif**, sélectionnez **Oui**.
1. Laissez les autres valeurs telles quelles, puis sélectionnez **Créer**.
1. Enregistrez l’**ID D’APPLICATION** pour l’utiliser dans une étape ultérieure.