<properties
	pageTitle="Préchargement d’éléments multimédias sur un point de terminaison CDN Azure"
	description="Découvrez comment précharger du contenu mis en cache sur un point de terminaison CDN."
	services="cdn"
	documentationCenter=".NET"
	authors="camsoper"
	manager="erikre"
	editor=""/>

<tags
	ms.service="cdn"
	ms.workload="tbd"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="02/25/2016" 
	ms.author="casoper"/>

# Préchargement d’éléments multimédias sur un point de terminaison CDN Azure

Par défaut, les éléments sont d'abord mis en cache lorsqu'ils sont demandés. Cela signifie que la première requête de chaque région peut prendre plus de temps puisque le contenu des serveurs Edge ne sera pas mis en cache et que vous devrez transmettre la requête au serveur d'origine. Le préchargement du contenu permet d'éviter cette latence à la première occurrence.

En plus d’offrir une meilleure expérience client, le préchargement de vos ressources mises en cache peut également réduire le trafic réseau sur le serveur d'origine.

> [AZURE.NOTE] Le préchargement des ressources est utile lors de grands événements ou lorsque le contenu est disponible simultanément à un grand nombre d'utilisateurs, par exemple lors de la sortie d’un film ou d'une mise à jour logicielle.

Ce didacticiel vous guide tout au long du préchargement de contenu mis en cache sur tous les nœuds de périphérie CDN Azure.

## Procédure pas à pas

1. Dans le [portail Azure](https://portal.azure.com), recherchez le profil CDN qui contient le point de terminaison que vous souhaitez précharger. Le panneau Profil s’ouvre.

2. Cliquez sur le point de terminaison dans la liste. Le panneau du point de terminaison s’ouvre.

3. Dans le panneau du point de terminaison CDN, cliquez sur le bouton Charger.

	![Panneau du point de terminaison CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)

	Le panneau Charger s’ouvre.

	![Panneau de chargement CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)

4. Entrez le chemin d’accès complet de chaque élément multimédia que vous souhaitez charger (par exemple, */pictures/kitten.png*) dans la zone de texte **Chemin d’accès**.

	> [AZURE.TIP] Après avoir saisi du texte, d’autres zones de texte **Chemin d’accès** s’afficheront pour vous permettre de créer une liste de plusieurs éléments multimédias. Vous pouvez supprimer des éléments multimédias de la liste en cliquant sur le bouton points de suspension (...).
	>
	> Les chemins d’accès doivent se présenter sous la forme d’une URL relative. L’astérisque (*) peut être utilisé comme caractère générique.

    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-paths.png)

5. Cliquez sur le bouton **Charger**.

	![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-button.png)


## Voir aussi
- [Purger un point de terminaison CDN Azure](cdn-purge-endpoint.md)
- [Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison](https://msdn.microsoft.com/library/mt634451.aspx)

<!---HONumber=AcomDC_0302_2016-->