---
title: Utiliser MSAL.js avec Azure AD B2C
titleSuffix: Microsoft identity platform
description: Microsoft Authentication Library (MSAL) permet aux applications d’interagir avec Azure AD B2C et d’acquérir des jetons pour appeler des API web sécurisées. Ces API web peuvent être Microsoft Graph, d’autres API Microsoft, des API web de tiers ou vos propres API web.
services: active-directory
author: negoe
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 06/05/2020
ms.author: negoe
ms.reviewer: nacanuma
ms.custom: aaddev devx-track-js
ms.openlocfilehash: 383c9651d6552a327bc9e986d18fbc7832fc94f8
ms.sourcegitcommit: 2e123f00b9bbfebe1a3f6e42196f328b50233fc5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108072186"
---
# <a name="use-the-microsoft-authentication-library-for-javascript-to-work-with-azure-ad-b2c"></a>Utiliser la bibliothèque d’authentification Microsoft pour JavaScript pour travailler avec Azure AD B2C

La [bibliothèque d’authentification Microsoft pour JavaScript (MSAL.js)](https://github.com/AzureAD/microsoft-authentication-library-for-js) permet aux développeurs JavaScript d’authentifier les utilisateurs avec des identités sociales et locales à l’aide d’[Azure Active Directory B2C](../../active-directory-b2c/overview.md) (Azure AD B2C).

En utilisant Azure AD B2C en tant que service de gestion des identités, vous pouvez personnaliser et contrôler la façon dont vos clients s’inscrivent, se connectent et gèrent leurs profils lorsqu’ils utilisent vos applications. Azure AD B2C vous permet également de personnaliser l’interface utilisateur affichée par votre application lors du processus d’authentification.

## <a name="supported-app-types-and-scenarios"></a>Types d’applications et scénarios pris en charge

MSAL.js permet aux [applications monopages](https://docs.microsoft.com/azure/active-directory-b2c/application-types#single-page-applications) de connecter des utilisateurs à Azure AD B2C à l’aide du [flux de code d’autorisation avec PKCE](https://docs.microsoft.com/azure/active-directory-b2c/authorization-code-flow). Avec MSAL.js et Azure AD B2C :

- Les utilisateurs **peuvent** s’authentifier avec leur identité sociale et locale.
- Les utilisateurs **peuvent** être autorisés à accéder aux ressources protégées Azure AD B2C (mais pas aux ressources protégées Azure AD).
- Les utilisateurs **ne peuvent pas** obtenir de jetons pour les API Microsoft (par exemple, MS API Graph) à l’aide d'[autorisations déléguées](https://review.docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent?branch=master#permission-types).
- Les utilisateurs disposant de privilèges d’administrateur **peuvent** obtenir des jetons pour les API Microsoft (par exemple, MS API Graph) à l’aide d'[autorisations déléguées](https://review.docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent?branch=master#permission-types).

Pour plus d’informations, consultez [Utilisation d’Azure AD B2C](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/working-with-b2c.md).

## <a name="next-steps"></a>Étapes suivantes

Suivez le tutoriel pour :

- [Connecter des utilisateurs avec Azure AD B2C dans une application monopage](../../active-directory-b2c/tutorial-single-page-app.md)
- [Appeler une API web protégée par Azure AD B2C](../../active-directory-b2c/tutorial-single-page-app-webapi.md)
