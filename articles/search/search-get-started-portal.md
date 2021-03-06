<properties 
	pageTitle="Prise en main d’Azure Search | Microsoft Azure  | Prise en main d’Azure Search | DocumentDB | Service de recherche cloud" 
	description="Créez votre première solution de recherche Azure Search à l’aide de ce didacticiel pas à pas. Apprenez à créer un index Azure Search à l’aide de données DocumentDB. Cet exercice se base sur le portail, ne nécessite pas de code, et utilise l’assistant Importation." 
	services="search" 
	documentationCenter="" 
	authors="HeidiSteen" 
	manager="mblythe" 
	editor=""
    tags="azure-portal"/>

<tags 
	ms.service="search" 
	ms.devlang="na" 
	ms.workload="search" 
	ms.topic="hero-article" 
	ms.tgt_pltfrm="na" 
	ms.date="02/10/2016" 
	ms.author="heidist"/>

# Prise en main d’Azure Search dans le portail
> [AZURE.SELECTOR]
- [Portail](search-get-started-portal.md)
- [.NET](search-howto-dotnet-sdk.md)

Cet article est une présentation sans code de Microsoft Azure Search, à l’aide des fonctionnalités intégrées au portail.

Le didacticiel prend l’exemple d’une [base de données Azure DocumentDB](#apdx-sampledata) que vous pouvez créer simplement à l’aide de nos données et d’instructions, mais vous pouvez également adapter ces étapes aux données existantes de votre base de données DocumentDB ou SQL.

> [AZURE.NOTE] Ce didacticiel de prise en main nécessite un [abonnement Azure](../../includes/free-trial-note.md) et un [service Azure Search](search-create-service-portal.md). Si vous n'êtes pas prêt à souscrire un abonnement d'essai, vous pouvez ignorer ce didacticiel et opter pour [Tester Azure App Service](search-tryappservice.md) à la place. Cette option de remplacement vous propose Azure Search avec une application Web ASP.NET gratuitement, une heure par session, sans abonnement obligatoire.
 
## Recherche de votre service

1. Connectez-vous au [portail Azure](https://portal.azure.com).

2. Cliquez sur le tableau de bord des services de votre service Azure Search. Voici quelques façons d'afficher le tableau de bord.
	- Dans la barre de lancement, cliquez sur **Services de recherche**. La barre de lancement répertorie tous les services fournis par votre abonnement. Si un service de recherche a été défini, vous verrez **Services de recherche** dans la liste.
	- Dans la barre de lancement, cliquez sur **Parcourir**, puis entrez « recherche » dans la zone de recherche afin de générer une liste de tous les services de recherche créés dans vos abonnements.

## Vérifier l’espace disponible

De nombreux clients commencent avec le service gratuit. Cette version est limitée à trois index, trois sources de données et trois indexeurs. Avant de commencer, assurez-vous de disposer d’assez d’espace pour stocker des éléments supplémentaires. Cette procédure pas à pas permet de créer une occurrence de chaque objet.

## Création d’un index et chargement des données

Les requêtes de recherche se répètent sur un *index* contenant les données de recherche, les métadonnées et les constructions utilisées pour l’optimisation de certains comportements de recherche. Dans un premier temps, vous devez définir et remplir un index.

Il existe plusieurs façons de créer un index. Si vos données se trouvent dans un magasin de données qu’Azure Search peut analyser (comme une base de données SQL Azure, un serveur SQL sur une machine virtuelle Azure, ou une base de données DocumentDB), vous pouvez créer et remplir un index très facilement à l’aide d’un *indexeur*.

Pour maintenir l’exécution de cette tâche dans le portail, nous allons supposer que les données de DocumentDB peuvent être analysées à l’aide d’un indexeur par le biais de l’Assistant **Importer des données**.

Avant de continuer, créez un [exemple de base de données DocumentDB](#apdx-sampledata) que vous pourrez utiliser avec ce didacticiel. Revenez ensuite à cette section pour effectuer les étapes ci-dessous.

<a id="defineDS"></a>
#### Étape 1 : définir la source de données

1. Dans votre tableau de bord de service Azure Search, cliquez sur **Importer des données** dans la barre de commandes pour lancer un assistant qui crée et remplit un index.

  ![][7]

2. Dans l’assistant, cliquez sur **Source de données** > **DocumentDB** > **Nom**, puis entrez le nom de la source de données. Une source de données est un objet de connexion pouvant être utilisé avec d’autres indexeurs dans Azure Search. Une fois que vous la créez, elle devient disponible en tant que « source de données existante » dans votre service.

3. Choisissez votre compte DocumentDB existant, ainsi que la base de données et la collection. Si vous utilisez les exemples de données que nous vous fournissons, la définition de votre source de données doit ressembler à ceci :

  ![][2]

Notez que nous ignorons la requête. En effet, cette fois-ci, nous n’implémentons pas le suivi des modifications dans notre jeu de données. Si votre jeu de données contient un champ effectuant le suivi des mises à jour d’un enregistrement, vous pouvez configurer un indexeur Azure Search afin d’utiliser le suivi des modifications pour les mises à jour sélectives de votre index.

Cliquez sur **OK** pour terminer cette étape de l’assistant.

#### Étape 2 : définir l’index

Toujours dans l’assistant, cliquez sur **Index** et observez l’aire de conception utilisée pour créer un index Azure Search. Un index nécessite au minimum un nom et une collection de champs, avec un champ marqué comme clé du document. Puisque nous utilisons un jeu de données DocumentDB, les champs sont détectés automatiquement par l’assistant, et l’index est préchargé avec les affectations de type de données et de champs.

  ![][3]

Même si les champs et les types de données sont configurés, vous devez affecter les attributs. Les cases à cocher en haut de la liste de champs sont des *attributs d’index* qui contrôlent l’utilisation du champ.

- **Récupérable** signifie que le champ s’affiche dans la liste des résultats de recherche. En décochant cette case, vous pouvez marquer des champs individuels comme hors limites pour les résultats de recherche, par exemple lorsqu’un champ est utilisé uniquement dans les expressions de filtre. 
- Les options **Filtrable**, **Triable** et **À choix multiples** déterminent si le champ peut être utilisé dans un filtre, un tri ou une structure de navigation à facettes. 
- **Possibilité de recherche** signifie que le champ est inclus dans la recherche en texte intégral. Une recherche est généralement possible sur les chaînes. Les champs numériques et booléens sont souvent marqués comme ne pouvant pas faire l’objet d’une recherche. 

Avant de quitter cette page, marquez les champs de votre index de manière à utiliser les options suivantes (Récupérable, Possibilité de recherche, etc.). La plupart des champs sont récupérables. La plupart des champs de type chaîne peuvent faire l’objet d’une recherche (vous n’avez pas besoin de marquer la clé en Possibilité de recherche). Certains champs tels que genre, orderableOnline, rating et tags sont également filtrables, triables, et à choix multiples.
	
Champ | Type | Options |
------|------|---------|
key | Edm.String | |
albumTitle | Edm.String | Récupérable, Possibilité de recherche |
albumUrl | Edm.String | Récupérable, Possibilité de recherche |
genre | Edm.String | Récupérable, Possibilité de recherche, Filtrable, Triable, À choix multiples |
genreDescription | Edm.String | Récupérable, Possibilité de recherche |
artistName | Edm.String | Récupérable, Possibilité de recherche |
orderableOnline | Edm.Boolean | Récupérable, Filtrable, Triable, À choix multiples |
tags | Collection(Edm.String) | Récupérable, Filtrable, À choix multiples |
price | Edm.Double | Récupérable, Filtrable, À choix multiples |
margin | Edm.Int32 | |
rating | Edm.Int32 | Récupérable, Filtrable, Triable, À choix multiples |
inventory | Edm.Int32 | Affichable dans les résultats d’une recherche |
lastUpdated | Edm.DateTimeOffset | |

Pour donner un point de comparaison, la capture d’écran suivante est une illustration de l’index créé selon les spécifications du tableau précédent.

 ![][4]

Cliquez sur **OK** pour terminer cette étape de l’assistant.

#### Étape 3 : définir l’indexeur

Toujours dans l’assistant **Importer des données**, cliquez sur **Indexeur** > **Nom**, entrez le nom de l’indexeur et utilisez les valeurs par défaut pour toutes les autres valeurs. Cet objet définit un processus exécutable. Une fois que vous le créez, vous pouvez le mettre en planification récurrente, mais pour l’instant, utilisez l’option par défaut pour exécuter l’indexeur une fois et immédiatement quand vous cliquez sur **OK**.

Vos entrées de données d’importation sont normalement toutes remplies et prêtes à l’emploi.

  ![][5]

Pour exécuter l’assistant, cliquez sur **OK** pour démarrer l’importation et fermer l’assistant.

## Vérification de la progression

Pour vérifier la progression, revenez au tableau de bord de service, faites défiler la page vers le bas et double-cliquez sur la vignette **Indexeurs** pour ouvrir la liste des indexeurs. Vous devriez voir l’indexeur que vous venez de créer dans la liste, un état indiquant « en cours » ou la réussite de l’opération, ainsi que le nombre de documents indexés dans Azure Search.

  ![][6]

## Interrogation de l'index

Vous disposez maintenant d’un index de recherche prêt à être interrogé.

L’**Explorateur de recherche** est un outil de requête intégré au portail. Il fournit une zone de recherche afin que vous puissiez vérifier qu’une entrée de recherche retourne les données attendues.

1. Cliquez sur **Explorateur de recherche** dans la barre de commandes.
2. Identifiez l’index actif. Si ce n’est pas celui que vous venez de créer, cliquez sur **Modifier l’index** dans la barre de commandes pour sélectionner l’index de votre choix.
2. Laissez la zone de recherche vide, puis cliquez sur le bouton **Rechercher** pour exécuter une recherche générique renvoyant tous les documents.
3. Entrez quelques requêtes de recherche en texte intégral. Vous pouvez passer en revue les résultats de votre recherche générique afin de vous familiariser avec les artistes, les albums et les genres à rechercher.
4. Essayez d’autres syntaxes de requête à l’aide des [exemples fournis à la fin de cet article](https://msdn.microsoft.com/library/azure/dn798927.aspx) pour trouver des idées, en modifiant votre requête pour utiliser des chaînes de recherche susceptibles d’être trouvées dans votre index.

## Étapes suivantes

Après avoir exécuté une fois l’assistant, vous pouvez revenir en arrière et afficher ou modifier des composants individuels : l’index, l’indexeur ou la source de données. Certaines modifications, telles que le type de données du champ, ne sont pas autorisées dans l’index, mais la plupart des paramètres et des propriétés sont modifiables. Pour afficher les composants individuels, cliquez sur les vignettes **Index**, **Indexeur** ou **Sources de données** sur votre tableau de bord pour afficher une liste des objets existants.

Pour en savoir plus sur les fonctionnalités mentionnées dans cet article, consultez ces liens :

- [Indexeurs](search-indexer-overview.md)
- [Création d’Index (comprend une explication détaillée sur les attributs d’index)](https://msdn.microsoft.com/library/azure/dn798941.aspx)
- [Explorateur de recherche](search-explorer.md)
- [Rechercher des Documents (comprend des exemples de syntaxe de requête)](https://msdn.microsoft.com/library/azure/dn798927.aspx)

Vous pouvez essayer de reproduire ce flux de travail en utilisant l’assistant Importation de données pour d’autres sources de données, comme une base de données SQL Azure ou SQL Server sur des machines virtuelles Azure.

> [AZURE.NOTE] La prise en charge de l’indexeur pour l’indexation Azure Blob Storage a récemment été annoncée, mais cette fonctionnalité n’existe qu’en version préliminaire et n’est pas encore une option du portail. Pour essayer cet indexeur, vous devez écrire du code. Consultez la page [Indexation de documents dans Azure Blob Storage avec Azure Search](search-howto-indexing-azure-blob-storage.md) pour plus d’informations. <a id="apdx-sampledata"></a>


## Annexe : création d’exemples de données dans DocumentDB

Cette section permet de créer une petite base de données dans DocumentDB qui peut être utilisée pour effectuer les tâches de ce didacticiel.

Les instructions suivantes vous donnent des conseils généraux, mais ne sont pas exhaustives. Si vous avez besoin de plus de renseignements sur les tâches ou la navigation dans le portail DocumentDB, vous pouvez consulter la documentation de DocumentDB. Toutefois, la plupart des commandes dont vous avez besoin se trouvent dans la barre de commandes de service en haut du tableau de bord ou dans le panneau de la base de données.

  ![][1]

### Création de la base de données musicstoredb pour ce didacticiel

1. [Cliquez ici](https://github.com/HeidiSteen/azure-search-get-started-sample-data) pour télécharger un fichier ZIP contenant les fichiers de données JSON du magasin de musique. Nous fournissons 246 documents JSON pour ce jeu de données.
2. Ajoutez DocumentDB à votre abonnement, puis ouvrez le tableau de bord du service.
2. Cliquez sur **Ajouter une base de données** pour créer une base de données avec l’identifiant `musicstoredb`. Après sa création, elle apparaît dans une liste de bases de données située en bas de la page.
2. Cliquez sur le nom de la base de données pour ouvrir son panneau.
3. Cliquez sur **Ajouter une collection** pour créer un regroupement avec l’id `musicstorecoll`.
3. Cliquez sur **Explorateur de documents**.
4. Cliquez sur **Ajouter des documents**.
5. Dans **Ajouter un document**, chargez des fichiers JSON par lots de 100 maximum.
	- 386\.json
	- 387\.json
	- . . .
6. Cliquez sur **Explorateur de requête** pour vérifier que les données sont chargées afin de répondre aux exigences de chargement de l’Explorateur de documents.

Pour ce faire, il existe un moyen simple consistant à modifier la requête par défaut de sorte qu’elle sélectionne les 300 premiers éléments (il en existe moins de 300 dans ce jeu de données). Vous pouvez également écrire `select * from musicstorecoll`, puis cliquer sur **Exécuter une requête**.

Vous devriez obtenir la sortie JSON, en commençant par le document n° 386 et en terminant par le document n° 669. Une fois les données chargées, vous pouvez [revenir aux étapes de cette procédure pas à pas](#defineDS) pour créer un index à l’aide de l’**assistant d’importation**.


<!--Image references-->
[1]: ./media/search-get-started-portal/AzureSearch-GetStart-Docdbmenu1.png
[2]: ./media/search-get-started-portal/AzureSearch-GetStart-DataSource.png
[3]: ./media/search-get-started-portal/AzureSearch-GetStart-DefaultIndex.png
[4]: ./media/search-get-started-portal/AzureSearch-GetStart-FinishedIndex.png
[5]: ./media/search-get-started-portal/AzureSearch-GetStart-ImportReady.png
[6]: ./media/search-get-started-portal/AzureSearch-GetStart-IndexerList.png
[7]: ./media/search-get-started-portal/search-data-import-wiz-btn.png

<!---HONumber=AcomDC_0309_2016-->