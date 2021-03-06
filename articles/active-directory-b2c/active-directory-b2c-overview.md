<properties
	pageTitle="Azure Active Directory B2C en version préliminaire : vue d’ensemble | Microsoft Azure"
	description="Développement d’applications accessibles aux consommateurs avec Azure Active Directory B2C"
	services="active-directory-b2c"
	documentationCenter=""
	authors="swkrish"
	manager="msmbaldwin"
	editor="bryanla"/>

<tags
	ms.service="active-directory-b2c"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="hero-article"
	ms.date="01/06/2016"
	ms.author="swkrish"/>

# Azure Active Directory B2C en version préliminaire : Inscription et connexion de consommateurs à vos applications

Azure Active Directory B2C est une solution de gestion des identités de cloud complète pour vos applications web et mobiles grand public. Il s’agit d’un service global hautement disponible dont l’échelle s’adapte à des centaines de millions d’identités. Basé sur une plateforme sécurisée à l’échelle de l’entreprise, Azure Active Directory B2C protège vos applications, votre entreprise et vos consommateurs.

Dans le passé, les développeurs d'applications qui souhaitaient inscrire et connecter les consommateurs à leurs applications écrivaient leur propre code. Et ils auraient utilisé des systèmes ou des bases de données locaux pour stocker les noms d'utilisateur et les mots de passe. Azure Active Directory B2C offre aux développeurs un meilleur moyen d'intégrer la gestion des identités des consommateurs dans leurs applications à l'aide d'une plateforme sécurisée basée sur des normes et d'un ensemble complet de stratégies extensibles. Lorsque vous utilisez Azure Active Directory B2C, vos consommateurs peuvent s’inscrire auprès de vos applications à l’aide de leurs comptes sociaux existants (Facebook, Google, Amazon, LinkedIn) ou en créant des informations d’identification (adresse de messagerie et mot de passe, ou nom d’utilisateur et mot de passe) que nous appelons « comptes locaux ».

Azure Active Directory B2C est en version préliminaire. Nous sommes actuellement impatients de recevoir vos commentaires et retours d’expérience. Nous tenons compte de ces commentaires pour apporter des modifications importantes au service et l’améliorer. Pendant cette période, vous ne devez pas publier d’application de production utilisant la version préliminaire. Faites-nous part de vos réflexions via [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/).

## Prise en main

Pour générer une application acceptant l’inscription et la connexion des consommateurs, vous devez commencer par inscrire cette application auprès d’un client Azure Active Directory B2C. Obtenez votre propre client en suivant la procédure décrite dans [Créer un client Azure AD B2C](active-directory-b2c-get-started.md).

Vous pouvez écrire votre application dans le service Azure Active Directory B2C en envoyant directement des messages de protocole à l’aide d’[OAuth 2.0](active-directory-b2c-reference-protocols.md#oauth2-authorization-code-flow) ou d’[Open ID Connect](active-directory-b2c-reference-protocols.md#openid-connect-sign-in-flow) ou en utilisant nos bibliothèques pour faire le travail à votre place. Choisissez votre plateforme préférée dans le tableau suivant et commencez.

[AZURE.INCLUDE [active-directory-b2c-quickstart-table](../../includes/active-directory-b2c-quickstart-table.md)]

## Nouveautés

Revenez souvent pour en savoir plus sur les futures modifications apportées à Azure Active Directory B2C en version préliminaire. Nous tweeterons également à propos des mises à jour via @AzureAD.

- Découvrez notre [infrastructure de stratégie extensible](active-directory-b2c-reference-policies.md) et les types de stratégie que vous pouvez créer et utiliser dans vos applications.
- [Limites, restrictions et contraintes de la version préliminaire](active-directory-b2c-limitations.md) actuelles.

## Articles sur les procédures

Découvrez comment utiliser des fonctionnalités spécifiques d’Azure Active Directory B2C en version préliminaire :

- Configurer des comptes [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Microsoft](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) et [LinkedIn](active-directory-b2c-setup-li-app.md) à utiliser dans vos applications grand public.
- [Utiliser des attributs personnalisés pour recueillir des informations sur vos consommateurs](active-directory-b2c-reference-custom-attr.md).
- [Activer Azure Multi-Factor Authentication dans vos applications grand public](active-directory-b2c-reference-mfa.md).
- [Configurer une réinitialisation de mot de passe libre-service pour vos consommateurs](active-directory-b2c-reference-sspr.md).
- [Personnaliser l’aspect des pages d’inscription, de connexion et des autres pages accessibles aux consommateurs](active-directory-b2c-reference-ui-customization.md) prises en charge par Azure Active Directory B2C.
- [Utiliser l’API Azure Active Directory Graph pour créer, lire, mettre à jour et supprimer des consommateurs par programme](active-directory-b2c-devquickstarts-graph-dotnet.md) dans votre client Azure Active Directory B2C.

## Étapes suivantes

Les liens ci-dessous vous seront utiles pour explorer le service en profondeur :

- Consultez les [informations de tarification relatives à Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
- Pour obtenir une aide sur le dépassement de la capacité de la pile, utilisez les balises [azure-active-directory](http://stackoverflow.com/questions/tagged/azure-active-directory) ou [adal](http://stackoverflow.com/questions/tagged/adal).
- Dites-nous ce que vous pensez de la version préliminaire sur [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/). Votre avis nous intéresse ! Ajoutez « AzureADB2C » dans le titre de votre publication pour nous aider à la repérer.
- Azure Active Directory B2C prend en charge les protocoles standard, OpenID Connect et OAuth 2.0, à l’aide d’un modèle d’inscription d’application que nous appelons « Modèle d’application v2.0 ».
  - [Informations de référence sur les protocoles du modèle d’application v2.0](active-directory-b2c-reference-protocols.md)
  - [Informations de référence sur les jetons du modèle d’application v2.0](active-directory-b2c-reference-tokens.md)
- Consultez les [FAQ sur Azure Active Directory B2C](active-directory-b2c-faqs.md).
- [Dépôt de demandes de support pour Azure Active Directory B2C](active-directory-b2c-support.md).

<!---HONumber=AcomDC_0224_2016-->