<properties 
    pageTitle="Didacticiel : Intégration d’Azure Active Directory avec Projectplace | Microsoft Azure" 
    description="Apprenez à utiliser Projectplace avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore." 
    services="active-directory" 
    authors="markusvi"  
    documentationCenter="na" 
    manager="stevenpo"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="01/12/2016" 
    ms.author="markvi" />

#Didacticiel : Intégration d’Azure Active Directory à Projectplace
  
L’objectif de ce didacticiel est de montrer comment intégrer Azure et Projectplace. Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

-   Un abonnement Azure valide
-   Un abonnement Projectplace pour lequel l’authentification unique est activée
  
À l’issue de ce didacticiel, les utilisateurs Azure AD que vous avez affectés à Projectplace pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise Projectplace (connexion initiée par le fournisseur du service) en s’aidant de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).
  
Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :

1.  Activation de l’intégration d’application pour Projectplace
2.  Configuration de l'authentification unique
3.  Configuration de l'approvisionnement des utilisateurs
4.  Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-projectplace-tutorial/IC790217.png "Scénario")
##Activation de l’intégration d’application pour Projectplace
  
Cette section décrit l’activation de l’intégration d’application pour Projectplace.

###Pour activer l’intégration d’application pour Projectplace, procédez comme suit :

1.  Dans le volet de navigation gauche du portail de gestion Azure, cliquez sur **Active Directory**.

    ![Active Directory](./media/active-directory-saas-projectplace-tutorial/IC700993.png "Active Directory")

2.  Dans la liste **Annuaire**, sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.

3.  Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.

    ![Applications](./media/active-directory-saas-projectplace-tutorial/IC700994.png "Applications")

4.  Cliquez sur **Ajouter** en bas de la page.

    ![Ajouter l’application](./media/active-directory-saas-projectplace-tutorial/IC749321.png "Ajouter l’application")

5.  Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.

    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-projectplace-tutorial/IC749322.png "Ajouter une application à partir de la galerie")

6.  Dans la **zone de recherche**, tapez **Projectplace**.

    ![Galerie d’applications](./media/active-directory-saas-projectplace-tutorial/IC790218.png "Galerie d’applications")

7.  Dans le volet des résultats, sélectionnez **Projectplace**, puis cliquez sur **Terminer** pour ajouter l’application.

    ![ProjectPlace](./media/active-directory-saas-projectplace-tutorial/IC790219.png "ProjectPlace")
##Configuration de l'authentification unique
  
Cette section explique comment permettre aux utilisateurs de s’authentifier sur Projectplace avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.

###Pour configurer l’authentification unique, procédez comme suit :

1.  Dans le portail Azure Active Directory, puis dans la page d’intégration d’application **Projectplace**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/IC790220.png "Configurer l’authentification unique")

2.  Dans la page **Comment voulez-vous que les utilisateurs se connectent à Projectplace**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/IC790221.png "Configurer l’authentification unique")

3.  Dans la page **Configurer l’URL de l’application**, dans la zone de texte **URL de connexion de Projectplace**, tapez l’URL de votre locataire Projectplace (par exemple, « **http://company.projectplace.com*"), puis cliquez sur **Suivant**.

    ![Configurer l’URL de l’application](./media/active-directory-saas-projectplace-tutorial/IC790222.png "Configurer l’URL de l’application")

4.  Dans la page **Configurer l’authentification unique sur Projectplace**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/IC790223.png "Configurer l’authentification unique")

5.  Envoyez le fichier de métadonnées à l’équipe du support technique Projectplace.

    >[AZURE.NOTE]La configuration de l’authentification unique doit être effectuée par l’équipe du support technique Projectplace. Vous recevez une notification dès qu’elle est terminée.

6.  Dans le portail Azure Active Directory, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.

    ![Configurer l’authentification unique](./media/active-directory-saas-projectplace-tutorial/IC790227.png "Configurer l’authentification unique")
##Configuration de l'approvisionnement des utilisateurs
  
Pour permettre aux utilisateurs Azure AD de se connecter à Projectplace, vous devez les approvisionner dans Projectplace. Dans le cas de Projectplace, l’approvisionnement est une tâche manuelle.

###Pour approvisionner un compte d’utilisateur, procédez comme suit :

1.  Connectez-vous au site d’entreprise **Projectplace** en tant qu’administrateur.

2.  Accédez à **People**, puis cliquez sur **Members**.

    ![Personnes](./media/active-directory-saas-projectplace-tutorial/IC790228.png "Personnes")

3.  Cliquez sur **Add Member**.

    ![Ajouter des membres](./media/active-directory-saas-projectplace-tutorial/IC790232.png "Ajouter des membres")

4.  Dans la section **Add Member**, procédez comme suit :

    ![Nouveaux membres](./media/active-directory-saas-projectplace-tutorial/IC790233.png "Nouveaux membres")

    1.  Dans la zone de texte **New Members**, entrez l’adresse de messagerie d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte correspondantes.
    2.  Cliquez sur **Envoyer**.

	    >[AZURE.NOTE]Un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé est envoyé au titulaire du compte Azure Active Directory.
    
>[AZURE.NOTE]Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Projectplace pour approvisionner des comptes d’utilisateur Azure Active Directory.

##Affectation d’utilisateurs
  
Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.

###Pour affecter des utilisateurs à Projectplace, procédez comme suit :

1.  Dans le portail Azure AD, créez un compte de test.

2.  Dans la page d’intégration d’application **Projectplace**, cliquez sur **Affecter des utilisateurs**.

    ![Affecter des utilisateurs](./media/active-directory-saas-projectplace-tutorial/IC790234.png "Affecter des utilisateurs")

3.  Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.

    ![Oui](./media/active-directory-saas-projectplace-tutorial/IC767830.png "Oui")
  
Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d’informations sur le volet d’accès, consultez [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).

<!---HONumber=AcomDC_0114_2016-->