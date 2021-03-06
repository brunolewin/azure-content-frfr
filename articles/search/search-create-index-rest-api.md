<properties
    pageTitle="Créer un index Azure Search à l’aide de l’API REST | Microsoft Azure | Service de recherche cloud hébergé"
    description="Créer un index dans le code à l’aide de l’API REST HTTP d’Azure Search."
    services="search"
    documentationCenter=""
    authors="ashmaka"
    manager=""
    editor=""
    tags="azure-portal"/>

<tags
    ms.service="search"
    ms.devlang="rest-api"
    ms.workload="search"
    ms.topic="get-started-article"
    ms.tgt_pltfrm="na"
    ms.date="03/09/2016"
    ms.author="ashmaka"/>

# Création d’un index Azure Search à l’aide de l’API REST
> [AZURE.SELECTOR]
- [Vue d'ensemble](search-what-is-an-index.md)
- [Portail](search-create-index-portal.md)
- [.NET](search-create-index-dotnet.md)
- [REST](search-create-index-rest-api.md)


Cet article vous guidera dans la création d’un [index](https://msdn.microsoft.com/library/azure/dn798941.aspx) Azure Search à l’aide de l’[API REST Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx). Pour créer un index Azure Search à l’aide de l’API REST, vous allez générer une seule requête POST HTTP sur le point de terminaison URL de votre service Azure Search. Votre définition d’index figurera dans le corps de la requête sous la forme d’un contenu JSON correct.

Avant de suivre ce guide et de passer à la création d’un index, vous devez avoir déjà [créé un service Azure Search](search-create-service-portal.md).

## I. Identifier la clé API d’administration de votre service Azure Search
Maintenant que vous avez configuré un service Azure Search, vous pouvez émettre des requêtes HTTP sur le point de terminaison URL de votre service à l’aide de l’API REST. *Tous les* demandes API doivent cependant inclure la clé API générée pour le service Search que vous avez configuré. L’utilisation d’une clé valide permet d’établir, en fonction de chaque demande, une relation de confiance entre l’application qui envoie la demande et le service qui en assure le traitement.

1. Pour accéder aux clés API de votre service, vous devez vous connecter au [portail Azure](https://portal.azure.com/)
2. Accédez au panneau de votre service Azure Search
3. Cliquez sur l’icône « Clés »

Votre service comporte à la fois des *clés d’administration* et des *clés de requête*.

 - Les *clés d’administration* principales et secondaires vous accordent des droits d’accès complets à toutes les opérations, avec notamment la possibilité de gérer le service ou de créer et supprimer des index, des indexeurs et des sources de données. Deux clés sont à votre disposition afin que vous puissiez continuer à utiliser la clé secondaire si vous décidez de régénérer la clé primaire et inversement.
 - Vos *clés de requête* vous accordent un accès en lecture seule aux index et documents ; elles sont généralement distribuées aux applications clientes qui émettent des demandes de recherche.

Dans le cadre de la création d’un index, vous pouvez utiliser votre clé d’administration principale ou secondaire.

## II. Définir votre index Azure Search à l’aide d’un code JSON correct
Une simple requête HTTP POST transmise à votre service vous permet de créer votre index. Le corps de votre requête HTTP POST doit contenir un seul objet JSON qui définit votre index Azure Search.

1. La première propriété de cet objet JSON correspond au nom de l’index.
2. La deuxième propriété de cet objet JSON est un tableau JSON nommé `fields`, qui contient un objet JSON distinct pour chaque champ de votre index. Chacun de ces objets JSON contient plusieurs paires nom/valeur pour chacun des attributs de champ, à savoir « nom », « type », etc.

Il est important de ne perdre de vue ni votre expérience de recherche ni vos besoins métiers lorsque vous concevez votre index, chaque champ devant être associé à des [attributs corrects](https://msdn.microsoft.com/library/azure/dn798941.aspx). Ces attributs déterminent les fonctionnalités de recherche (filtrage, facettes, tri de recherche en texte intégral, etc.) qui s’appliqueront à chaque champ. Si vous ne spécifiez pas d’attribut, le paramètre par défaut consistera à activer la fonctionnalité de recherche correspondante à moins que vous ne la désactiviez spécifiquement.

Dans notre exemple, nous avons nommé notre index « hotels » et défini ses champs de la manière suivante :

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Nous avons soigneusement choisi les attributs d’index pour chaque champ en fonction de la manière dont ils seront vraisemblablement utilisés dans une application. Par exemple, `hotelId` est une clé unique qui sera vraisemblablement méconnue des utilisateurs effectuant une recherche d’hôtels. Nous allons donc désactiver la recherche en texte intégral pour ce champ en définissant le paramètre `searchable` sur `false`, afin d’économiser de l’espace au niveau de l’index.

Notez que, dans votre index, un seul champ de type `Edm.String` doit être désigné en tant que « clé ».

La définition d’index ci-dessus utilise un analyseur de langue personnalisé pour le champ `description_fr` dans la mesure où il est destiné à stocker du texte en français. Pour plus d’informations sur les analyseurs de langue, consultez la [rubrique relative à la prise en charge linguistique sur MSDN](https://msdn.microsoft.com/library/azure/dn879793.aspx) ainsi que le [billet de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) correspondant.

## III. Envoyer la requête HTTP
1. En utilisant votre définition d’index dans le corps de votre requête, envoyez une requête HTTP POST vers l’URL de point de terminaison de votre service Azure Search. Dans l’URL, veillez à utiliser le nom de votre service en tant que nom d’hôte et placez l’attribut `api-version` approprié comme paramètre de chaîne de requête (à la date publication de ce document, l’API `2015-02-28` correspond à la version la plus récente).
2. Dans les en-têtes de requête, spécifiez `Content-Type` comme `application/json`. Vous devrez également renseigner dans l’en-tête `api-key` la clé d’administration de votre service que vous avez identifiée à l’étape I.


    POST https://[service name].search.windows.net/indexes?api-version=2015-02-28 Content-Type: application/json api-key: [api-key]

Pour que votre requête aboutisse, vous devez voir le code d’état « 201 créé ». Pour plus d’informations sur la création d’un index via l’API REST, consultez la référence d’API sur [MSDN](https://msdn.microsoft.com/library/azure/dn798941.aspx). Pour plus d’informations sur les autres codes d’état HTTP pouvant être renvoyés en cas d’échec, consultez la page [HTTP status codes (Azure Search)](https://msdn.microsoft.com/library/azure/dn798925.aspx) (Codes d’état HTTP (Azure Search).

Pour supprimer un index, il vous suffit de générer une requête HTTP DELETE. Voici, par exemple, la requête à utiliser pour supprimer l’index « hotels » :

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2015-02-28
    api-key: [api-key]

## Suivant
Après avoir créé un index Azure Search, vous pouvez commencer à télécharger du contenu dans votre index afin d’y lancer des recherches. Pour plus d’informations, consultez la page [Importer des données dans Azure Search à l’aide de l’API REST](search-import-data-rest-api.md).

<!---HONumber=AcomDC_0309_2016-->