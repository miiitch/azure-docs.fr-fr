---
title: Invite de consentement inattendue lors de la connexion à une application | Microsoft Docs
description: Procédure de dépannage à suivre quand un utilisateur voit une invite de consentement inattendue pour une application intégrée à Azure AD
services: active-directory
author: iantheninja
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: troubleshooting
ms.date: 07/11/2017
ms.author: iangithinji
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37e4384b5a1b400f11b7b7d6ab15beec4d2f8de9
ms.sourcegitcommit: 2654d8d7490720a05e5304bc9a7c2b41eb4ae007
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107378055"
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a>Invite de consentement inattendue lors de la connexion à une application

Pour s’exécuter, de nombreuses applications qui s’intègrent à Azure Active Directory nécessitent des autorisations à plusieurs ressources. Quand ces ressources sont également intégrées à Azure Active Directory, vous devez utiliser l’infrastructure de consentement Azure AD pour demander les autorisations nécessaires pour y accéder. 

Une invite de consentement est alors affichée à la première utilisation d’une application (il s’agit généralement d’une opération unique). 

> [!VIDEO https://www.youtube.com/embed/a1AjdvNDda4]

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Scénarios dans lesquels des invites de consentement sont présentées aux utilisateurs

Divers scénarios entraînent l’affichage d’invites supplémentaires :

* Le jeu d’autorisations exigées par l’application a changé.

* L’utilisateur ayant initialement donné son consentement à l’application n’était pas un administrateur, et un autre utilisateur (non-administrateur) utilise l’application pour la première fois.

* L’utilisateur ayant initialement donné son consentement à l’application était un administrateur, mais il n’a pas donné son consentement au nom de toute l’organisation.

* L’application utilise le [consentement incrémentiel et dynamique](../azuread-dev/azure-ad-endpoint-comparison.md#incremental-and-dynamic-consent) pour demander des autorisations supplémentaires après le consentement initial. Ce cas de figure se présente souvent quand les fonctionnalités facultatives d’une application nécessitent des autorisations au-delà de celles exigées pour les fonctionnalités de base.

* Le consentement, bien qu’initialement accordé, a été révoqué.

* Le développeur a configuré l’application pour exiger une invite de consentement à chaque utilisation (ce qui n’est pas recommandé).

## <a name="next-steps"></a>Étapes suivantes

-   [Applications, autorisations et consentement dans Azure Active Directory (point de terminaison v1.0)](../develop/quickstart-register-app.md)

-   [Étendues, autorisations et consentement dans Azure Active Directory (point de terminaison v2.0)](../develop/v2-permissions-and-consent.md)
