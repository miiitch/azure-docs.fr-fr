---
title: 'Tutoriel : Intégration de l’authentification unique Azure Active Directory à CakeHR | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et CakeHR.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 10/16/2019
ms.author: jeedes
ms.openlocfilehash: 08e028ba057ad57f3d600bc59bf7595c0b1d354c
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "92456567"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-cakehr"></a>Tutoriel : Intégration de l’authentification unique Azure Active Directory à CakeHR

Dans ce tutoriel, vous allez apprendre à intégrer CakeHR à Azure Active Directory (Azure AD). Quand vous intégrez CakeHR à Azure AD, vous pouvez :

* Contrôler dans Azure AD qui a accès à CakeHR.
* Permettre à vos utilisateurs de se connecter automatiquement à CakeHR avec leur compte Azure AD.
* Gérer vos comptes à un emplacement central : le Portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour commencer, vous devez disposer de ce qui suit :

* Un abonnement Azure AD Si vous ne disposez d’aucun abonnement, vous pouvez obtenir [un compte gratuit](https://azure.microsoft.com/free/).
* Un abonnement CakeHR pour lequel l’authentification unique est activée.

## <a name="scenario-description"></a>Description du scénario

Dans ce tutoriel, vous allez configurer et tester l’authentification unique Azure AD dans un environnement de test.

* CakeHR prend en charge l’authentification unique lancée par le **fournisseur de services**

> [!NOTE]
> L’identificateur de cette application étant une valeur de chaîne fixe, une seule instance peut être configurée dans un locataire.

## <a name="adding-cakehr-from-the-gallery"></a>Ajout de CakeHR à partir de la galerie

Pour configurer l’intégration de CakeHR à Azure AD, vous devez ajouter CakeHR, disponible dans la galerie, à votre liste d’applications SaaS gérées.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte professionnel ou scolaire ou avec un compte personnel Microsoft.
1. Dans le panneau de navigation gauche, sélectionnez le service **Azure Active Directory**.
1. Accédez à **Applications d’entreprise**, puis sélectionnez **Toutes les applications**.
1. Pour ajouter une nouvelle application, sélectionnez **Nouvelle application**.
1. Dans la section **Ajouter à partir de la galerie**, tapez **CakeHR** dans la zone de recherche.
1. Sélectionnez **CakeHR** dans le volet de résultats, puis ajoutez l’application. Patientez quelques secondes pendant que l’application est ajoutée à votre locataire.

## <a name="configure-and-test-azure-ad-single-sign-on-for-cakehr"></a>Configurer et tester l’authentification unique Azure AD pour CakeHR

Configurez et testez l’authentification unique Azure AD avec CakeHR à l’aide d’un utilisateur de test appelé **B.Simon**. Pour que l’authentification unique fonctionne, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur CakeHR associé.

Pour configurer et tester l’authentification unique Azure AD avec CakeHR, effectuez les modules suivants :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-sso)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
    * **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec B. Simon.
    * **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à B. Simon d’utiliser l’authentification unique Azure AD.
1. **[Configurer l’authentification unique CakeHR](#configure-cakehr-sso)** pour configurer les paramètres de l’authentification unique côté application.
    * **[Créer un utilisateur de test CakeHR](#create-cakehr-test-user)** pour avoir un équivalent de B.Simon dans CakeHR lié à la représentation Azure AD associée.
1. **[Tester l’authentification unique](#test-sso)** pour vérifier si la configuration fonctionne.

## <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Effectuez les étapes suivantes pour activer l’authentification unique Azure AD dans le Portail Azure.

1. Dans le [Portail Azure](https://portal.azure.com/), accédez à la page d’intégration de l’application **CakeHR**, recherchez la section **Gérer** et sélectionnez **Authentification unique**.
1. Dans la page **Sélectionner une méthode d’authentification unique**, sélectionnez **SAML**.
1. Dans la page **Configurer l’authentification unique avec SAML**, cliquez sur l’icône de modification/stylet de **Configuration SAML de base** pour modifier les paramètres.

   ![Modifier la configuration SAML de base](common/edit-urls.png)

1. Dans la section **Configuration SAML de base**, entrez les valeurs pour les champs suivants :

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<yourcakedomain>.cake.hr/`.

    b. Dans la zone de texte **URL de réponse**, tapez une URL au format suivant : `https://<yourcakedomain>.cake.hr/services/saml/consume`
    > [!NOTE]
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles. Pour obtenir ces valeurs, contactez [l’équipe du support technique de CakeHR](mailto:info@cake.hr). Vous pouvez également consulter les modèles figurant à la section **Configuration SAML de base** dans le portail Azure.

1. Dans la section **Certificat de signature SAML**, cliquez sur le bouton **Modifier** pour ouvrir la boîte de dialogue **Certificat de signature SAML**.

    ![Modifier le certificat de signature SAML](common/edit-certificate.png)

1. Dans la section **Certificat de signature SAML**, copiez la **valeur de l’empreinte** et enregistrez-la dans le Bloc-notes.

    ![Copier la valeur de l’empreinte](common/copy-thumbprint.png)

1. Dans la section **Configurer CakeHR**, copiez l’URL ou les URL appropriées en fonction de vos besoins.

    ![Copier les URL de configuration](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

Dans cette section, vous allez créer un utilisateur de test appelé B. Simon dans le portail Azure.

1. Dans le volet gauche du Portail Azure, sélectionnez **Azure Active Directory**, **Utilisateurs**, puis **Tous les utilisateurs**.
1. Sélectionnez **Nouvel utilisateur** dans la partie supérieure de l’écran.
1. Dans les propriétés **Utilisateur**, effectuez les étapes suivantes :
   1. Dans le champ **Nom**, entrez `B.Simon`.  
   1. Dans le champ **Nom de l’utilisateur**, entrez username@companydomain.extension. Par exemple : `B.Simon@contoso.com`.
   1. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.
   1. Cliquez sur **Créer**.

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser B.Simon à utiliser l’authentification unique Azure en lui accordant l’accès à CakeHR.

1. Dans le portail Azure, sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.
1. Dans la liste des applications, sélectionnez **CakeHR**.
1. Dans la page de vue d’ensemble de l’application, recherchez la section **Gérer** et sélectionnez **Utilisateurs et groupes**.

   ![Lien « Utilisateurs et groupes »](common/users-groups-blade.png)

1. Sélectionnez **Ajouter un utilisateur**, puis **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une attribution**.

    ![Lien Ajouter un utilisateur](common/add-assign-user.png)

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **B. Simon** dans la liste Utilisateurs, puis cliquez sur le bouton **Sélectionner** au bas de l’écran.
1. Si vous attendez une valeur de rôle dans l’assertion SAML, dans la boîte de dialogue **Sélectionner un rôle**, sélectionnez le rôle approprié pour l’utilisateur dans la liste, puis cliquez sur le bouton **Sélectionner** en bas de l’écran.
1. Dans la boîte de dialogue **Ajouter une attribution**, cliquez sur le bouton **Attribuer**.

## <a name="configure-cakehr-sso"></a>Configurer l’authentification unique CakeHR

1. Pour automatiser la configuration dans CakeHR, vous devez installer l’**extension de navigateur My Apps Secure Sign-in** en cliquant sur **Installer l’extension**.

    ![Extension My apps](common/install-myappssecure-extension.png)

1. Après l’ajout de l’extension au navigateur, cliquez sur **Configurer CakeHR** pour être dirigé vers l’application CakeHR. À partir de là, indiquez les informations d’identification de l’administrateur pour vous connecter à CakeHR. Cette extension de navigateur configure automatiquement l’application et automatise les étapes 3 à 5.

    ![Configuration](common/setup-sso.png)

1. Si vous souhaitez configurer manuellement CakeHR, ouvrez une nouvelle fenêtre de navigateur web, connectez-vous à votre site d’entreprise CakeHR en tant qu’administrateur et effectuez les étapes suivantes :

1. Dans le coin supérieur droit de la page, cliquez sur **Profil**, puis accédez à **Paramètres**.

    ![Capture d’écran montrant Profile avec Settings sélectionné.](./media/cakehr-tutorial/config01.png)

1. Sur le côté gauche de la barre de menus, cliquez sur **INTEGRATIONS** > **SAML SSO** (Intégrations > Authentification unique SAML), puis effectuez les étapes suivantes :

    ![Capture d’écran montrant le volet Setting où vous effectuez ces étapes.](./media/cakehr-tutorial/config02.png)

    a. Dans la zone de texte **Entity ID** (ID d’entité), tapez `cake.hr`.

    b. Dans la zone de texte **Authentication URL** (URL d’authentification), collez la valeur **URL de connexion** que vous avez copiée à partir du Portail Azure.

    c. Dans la zone de texte **Key fingerprint (SHA1 format)** (Empreinte de la clé au format SHA1), collez la **valeur de l’empreinte** que vous avez copiée à partir du Portail Azure.

    d. Cochez la case **Enable Single Sign on** (Activer l’authentification unique).

    e. Cliquez sur **Enregistrer**.

### <a name="create-cakehr-test-user"></a>Créer un utilisateur de test CakeHR

Pour se connecter à CakeHR, les utilisateurs Azure AD doivent être provisionnés dans CakeHR. Dans CakeHR, le provisionnement est une tâche manuelle.

**Pour approvisionner un compte d’utilisateur, procédez comme suit :**

1. Connectez-vous à CakeHR en tant qu’administrateur de la sécurité.

2. Sur le côté gauche de la barre de menus, cliquez sur **COMPANY** > **ADD** (Entreprise > Ajouter).

    ![Capture d’écran montrant CakeHR avec COMPANY et ADD sélectionnés.](./media/cakehr-tutorial/config03.png)

3. Dans la boîte de dialogue **Add new employee** (Ajouter un nouvel employé), effectuez les étapes suivantes :

     ![Capture d’écran montrant ajouter Add new employee où vous effectuez ces étapes.](./media/cakehr-tutorial/config04.png)

    a. Dans la zone de texte **Full name** (Nom complet), entrez le nom d’un utilisateur, par exemple B.Simon.

    b. Dans la zone de texte **Work email** (Adresse e-mail professionnelle), entrez l’adresse e-mail de l’utilisateur, par exemple `B.Simon@contoso.com`.

    c. Cliquez sur **CREATE ACCOUNT** (Créer un compte).

## <a name="test-sso"></a>Tester l’authentification unique (SSO) 

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Le fait de cliquer sur la vignette CakeHR dans le panneau d’accès doit vous connecter automatiquement à l’application CakeHR pour laquelle vous avez configuré l’authentification unique. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Ressources supplémentaires

- [Liste de tutoriels sur l’intégration d’applications SaaS avec Azure Active Directory](./tutorial-list.md)

- [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

- [Qu’est-ce que l’accès conditionnel dans Azure Active Directory ?](../conditional-access/overview.md)

- [Essayer CakeHR avec Azure AD](https://aad.portal.azure.com/)