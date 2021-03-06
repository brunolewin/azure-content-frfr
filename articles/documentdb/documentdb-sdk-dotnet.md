<properties 
	pageTitle="Kit de développement logiciel (SDK) .NET de DocumentDB | Microsoft Azure" 
	description="Découvrez le Kit de développement logiciel (SDK) .NET, y compris les dates de lancement, les dates de suppression et les modifications apportées entre chaque version du Kit de développement logiciel (SDK) .NET DocumentDB." 
	services="documentdb" 
	documentationCenter=".net" 
	authors="ryancrawcour" 
	manager="jhubbard" 
	editor="cgronlun"/>

<tags 
	ms.service="documentdb" 
	ms.workload="data-services" 
	ms.tgt_pltfrm="na" 
	ms.devlang="dotnet" 
	ms.topic="article" 
	ms.date="02/19/2016" 
	ms.author="ryancraw"/>

# Kit de développement logiciel (SDK) DocumentDB

> [AZURE.SELECTOR]
- [.NET SDK](documentdb-sdk-dotnet.md)
- [Node.js SDK](documentdb-sdk-node.md)
- [Java SDK](documentdb-sdk-java.md)
- [Python SDK](documentdb-sdk-python.md)

##Kit de développement logiciel (SDK) .NET DocumentDB

<table> <tr><td>**Téléchargement**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr> <tr><td>**Documentation**</td><td>[Documentation de référence du Kit de développement logiciel (SDK) .NET](https://msdn.microsoft.com/library/azure/dn948556.aspx)</td></tr> <tr><td>**Échantillons**</td><td>[Échantillons de code .NET](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</td></tr> <tr><td>**Prise en main**</td><td>[Prise en main du Kit de développement logiciel (SDK) .NET DocumentDB](documentdb-get-started.md)</td></tr> <tr><td>**Framework actuellement pris en charge**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr> </table></br>

## Notes de publication

### <a name="1.5.3"/>[1\.5.3](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.5.3)
  - **[Corrigés]** L’interrogation du point de terminaison DocumentDB renvoie : System.Net.Http.HttpRequestException: Error while copying content to a stream (erreur lors de la copie du contenu vers un flux).

### <a name="1.5.2"/>[1\.5.2](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.5.2)
  - Prise en charge LINQ étendue, y compris de nouveaux opérateurs pour la pagination, les expressions conditionnelles et la comparaison de plages.
    - Opérateur Take pour activer le comportement SELECT TOP dans LINQ
    - Opérateur CompareTo pour activer les comparaisons de plages de chaînes
    - Opérateurs Conditional (?) et Coalesce (??)
  - **[Résolu]** ArgumentOutOfRangeException lors de la combinaison de projection de modèle avec Where-In dans la requête linq. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="1.5.1"/>[1\.5.1](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.5.1)
 - **[Résolu]** Si la dernière expression n’est pas Select, le fournisseur LINQ n’effectuait aucune projection et créait une expression SELECT * incorrecte. [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="1.5.0"/>[1\.5.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.5.0)
 - Mise en œuvre de l’opération Upsert, ajout des méthodes UpsertXXXAsync
 - Améliorations des performances pour toutes les requêtes
 - Prise en charge par le fournisseur LINQ des méthodes conditionnelles, de regroupement et CompareTo pour les chaînes
 - **[Résolu]** Fournisseur LINQ--> Mise en œuvre de la méthode Contains sur List pour générer le même SQL que sur IEnumerable et Array
 - **[Résolu]** BackoffRetryUtility utilise de nouveau le même HttpRequestMessage au lieu d’en créer un nouveau à chaque tentative
 - **[Obsolète]** UriFactory.CreateCollection --> doit désormais utiliser UriFactory.CreateDocumentCollection
 
### <a name="1.4.1"/>[1\.4.1](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.4.1)
 - **[Résolu]** Erreurs de localisation lors de l’utilisation d’autres langues que l’anglais, comme nl-NL, etc. 
 
### <a name="1.4.0"/>[1\.4.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.4.0)
  - Routage basé sur l’ID
    - Nouvelle application d’assistance UriFactory pour faciliter la construction de liens de ressources basés sur l’ID
    - Nouvelles surcharges sur DocumentClient pour prendre en compte l’URI
  - Ajout de IsValid() et IsValidDetailed() dans LINQ pour les données géospatiales
  - Amélioration de la prise en charge du fournisseur LINQ
    - **Mathématiques** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
    - **Chaîne** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
    - **Tableau** - Concat, Contains, Count
    - Opérateur **IN**

### <a name="1.3.0"/>[1\.3.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.3.0)
  - Ajout de la prise en charge de la modification des stratégies d’indexation
    - Nouvelle méthode ReplaceDocumentCollectionAsync dans DocumentClient
    - Nouvelle propriété IndexTransformationProgress dans ResourceResponse<T> pour le suivi de l’évolution du pourcentage de modification de la stratégie d’indexation
    - DocumentCollection.IndexingPolicy est désormais mutable
  - Ajout de la prise en charge de l’indexation et des requêtes spatiales
    - Nouvel espace de noms Microsoft.Azure.Documents.Spatial pour la sérialisation/désérialisation des types de données spatiales comme Point et Polygon
    - Nouvelle classe SpatialIndex pour l’indexation des données GeoJSON stockées dans DocumentDB
  - **[Résolu]**: requête SQL incorrecte générée à partir de l’expression linq [#38](https://github.com/Azure/azure-documentdb-net/issues/38)

### <a name="1.2.0"/>[1\.2.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.2.0)
- Dépendance de Newtonsoft.Json v5.0.7 
- Modifications pour prendre en charge la clause Order By
  - Prise en charge du fournisseur LINQ pour OrderBy() ou OrderByDescending()
  - IndexingPolicy pour prendre en charge la clause Order By 
  
		**NB : modification avec rupture possible** 
  
    	Si vous avez un code qui configure les collections avec une stratégie d'indexation personnalisée, vous devrez le mettre à jour de sorte qu'il prenne en charge la nouvelle classe IndexingPolicy.Si vous n'avez pas de stratégie d'indexation personnalisée, cette modification ne vous affecte pas.

### <a name="1.1.0"/>[1\.1.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.1.0)
- Prise en charge du partitionnement des données à l’aide des nouvelles classes HashPartitionResolver et RangePartitionResolver et de IPartitionResolver
- Sérialisation DataContract
- Prise en charge des Guid dans le fournisseur LINQ
- Prise en charge UDF dans LINQ

### <a name="1.0.0"/>[1\.0.0](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/1.0.0)
- Kit de développement logiciel (SDK) GA

> [AZURE.NOTE]
Une modification du nom du package NuGet entre l’aperçu et la disponibilité générale a eu lieu. Nous sommes passés de **Microsoft.Azure.Documents.Client** à **Microsoft.Azure.DocumentDB** <br/>


### <a name="0.9.x-preview"/>[0\.9.x-aperçu](https://www.nuget.org/packages/Microsoft.Azure.Documents.Client)
- Kits de développement logiciel (SDK) en version préliminaire [Obsolète]

## Dates de lancement et de suppression
Microsoft fournira une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.

Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit de développement logiciel (SDK) actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du SDK dès que possible.

Toute requête à DocumentDB utilisant un Kit de développement logiciel (SDK) supprimé est rejetée par le service.

> [AZURE.WARNING]
Toutes les versions du Kit de développement logiciel (SDK) Azure DocumentDB pour .NET antérieures à la version **1.0.0** seront supprimées le **29 février 2016**.
 
<br/>
 
| Version | Date de lancement | Date de suppression 
| ---	  | ---	         | ---
| [1\.5.3](#1.5.3) | 19 février 2016 |---
| [1\.5.2](#1.5.2) | 14 décembre 2015 |---
| [1\.5.1](#1.5.1) | 23 novembre 2015 |---
| [1\.5.0](#1.5.0) | 5 octobre 2015 |---
| [1\.4.1](#1.4.1) | 25 août 2015 |---
| [1\.4.0](#1.4.0) | 13 août 2015 |---
| [1\.3.0](#1.3.0) | 5 août 2015 |---
| [1\.2.0](#1.2.0) | 6 juillet 2015 |---
| [1\.1.0](#1.1.0) | 30 avril 2015 |---
| [1\.0.0](#1.0.0) | 8 avril 2015 |---
| [0\.9.3-version préliminaire](#0.9.x-preview) | 12 mars 2015 | 29 février 2016
| [0\.9.2-version préliminaire](#0.9.x-preview) | Janvier 2015 | 29 février 2016
| [.9.1-version préliminaire](#0.9.x-preview) | 13 octobre 2014 | 29 février 2016
| [0\.9.0-version préliminaire](#0.9.x-preview) | 21 février 2014 | 29 février 2016

## Forum Aux Questions
[AZURE.INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## Voir aussi

Pour en savoir plus sur DocumentDB, consultez la page du service [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).

<!---HONumber=AcomDC_0224_2016-->