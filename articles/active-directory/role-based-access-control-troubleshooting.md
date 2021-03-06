<properties
	pageTitle="Résolution des problèmes de contrôle d'accès en fonction du rôle"
	description="Utilisation de différents types de ressources pour le contrôle d'accès en fonction du rôle."
	services="azure-portal"
	documentationCenter="na"
	authors="kgremban"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="01/25/2016"
	ms.author="kgremban"/>

# Résolution des problèmes de contrôle d’accès en fonction du rôle

## Introduction

Le [contrôle d’accès basé sur un rôle](../role-based-access-control-configure.md) est une fonctionnalité puissante qui vous permet de déléguer l’accès affiné aux ressources dans Azure. Cela signifie que vous pouvez en toute sécurité accorder à la personne de votre choix le droit de faire ce qu’elle a besoin de faire, sans plus. Toutefois, le modèle de ressources pour les ressources Azure peut parfois être complexe, et il peut s'avérer difficile de comprendre avec précision pourquoi accorder certaines autorisations.

Ce document vous permet de savoir ce à quoi vous pouvez vous attendre quand vous utilisez les rôles sur le portail Azure. Trois rôles courants sont inclus, qui couvrent tous les types de ressources :

- Propriétaire  
- Collaborateur  
- Lecteur  

Les propriétaires et collaborateurs disposent tous les deux d’un accès complet à toutes les opérations de gestion, mais un collaborateur ne peut pas accorder d’accès à d’autres utilisateurs ou groupes. La situation du rôle de lecteur est un peu plus intéressante, et nous allons nous y attarder. Consultez l’[article Prise en main du contrôle d’accès en fonction du rôle](../role-based-access-control-configure.md) pour plus d’informations sur la façon d’octroyer l’accès.

## Charges de travail App Service

### Fonctionnalités d’accès en écriture

Si vous accordez un accès utilisateur en lecture seule à une seule application web, certaines fonctionnalités sont désactivées, ce que vous n’avez peut-être pas prévu. Les fonctionnalités de gestion suivantes exigent un accès en **écriture** à une application web (Collaborateur ou Propriétaire) et ne sont pas disponibles en lecture seule.

1. Commandes (par ex., start, stop, etc.)
2. Modification de paramètres tels que la configuration générale, les paramètres de mise à l’échelle, les paramètres de sauvegarde et les paramètres d’analyse
3. Accès aux informations d’identification de publication et autres informations secrètes, telles que les paramètres d’application et les chaînes de connexion
4. Diffusion de journaux
5. Configuration des journaux de diagnostic
6. Console (invite de commandes)
7. Déploiements actifs et récents (pour le déploiement continu Git local)
8. Estimation de dépense
9. Tests web
10. Réseau virtuel (accessible à un lecteur uniquement si un réseau virtuel a été précédemment configuré par un utilisateur avec accès en écriture).

Si vous n’accédez à aucune de ces vignettes, vous devez obtenir l’accès Collaborateur à l’application web auprès de votre administrateur.

### Gestion des ressources connexes

Les applications web sont compliqués par la présence de quelques ressources différentes qui interagissent. Voici un groupe de ressources classique avec deux sites web :

![Groupe de ressources d'application web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

En conséquence, si vous accordez à un utilisateur le seul accès au site web, la plupart des fonctionnalités du volet Site web seront désactivées.

1. Les éléments suivants requièrent l'accès au **plan App Service** qui correspond à votre site web :  
    * Affichage du niveau de tarification de l'application web (par ex., Gratuit ou Standard).
    * Configuration de mise à l'échelle (c'est-à-dire le nombre d'instances, la taille de la machine virtuelle, les paramètres de mise à l'échelle automatique).
    * Quotas (par ex., stockage, bande passante, UC).
2. Les éléments suivants requièrent l'accès à l'ensemble du **Groupe de ressources** qui contient le site web :  
    * Certificats et liaisons SSL (car les certificats SSL peuvent être partagés entre différents sites dans le même groupe de ressources et emplacement).
    * Règles d'alerte
    * Paramètres de mise à l'échelle automatique
    * Composants Application Insights
    * Tests web

## Charges de travail des machines virtuelles

Comme pour les applications web, certaines fonctionnalités du volet de la machine virtuelle exigent un accès en écriture à la machine virtuelle ou à d'autres ressources du groupe de ressources.

Les ressources suivantes sont associées aux machines virtuelles :

- Noms de domaine
- Réseaux virtuels
- Comptes de stockage
- Règles d'alerte


1. Les éléments suivants requièrent l'accès en **écriture** à la machine virtuelle :  
    * Points de terminaison
    * Adresses IP
    * Disques
    * Extensions
2. Les éléments suivants requièrent l’accès **en écriture** à la machine virtuelle, ainsi qu’au **Groupe de ressources** (avec le nom de domaine) auxquels ils appartiennent :  
    * Groupe à haute disponibilité
    * Jeu d'équilibrage de la charge
    * Règles d'alerte

Si vous n'accédez à aucune de ces vignettes, vous devez obtenir auprès de votre administrateur l'accès Collaborateur au groupe de ressources.

<!---HONumber=AcomDC_0128_2016-->