<properties 
	pageTitle="Kit de développement logiciel (SDK) Python DocumentDB | Microsoft Azure" 
	description="Découvrez le Kit de développement logiciel (SDK) Python, y compris les dates de publication, les dates de suppression et les modifications apportées entre chaque version du Kit de développement logiciel (SDK) Python DocumentDB." 
	services="documentdb" 
	documentationCenter="python" 
	authors="ryancrawcour" 
	manager="jhubbard" 
	editor="cgronlun"/>

<tags 
	ms.service="documentdb" 
	ms.workload="data-services" 
	ms.tgt_pltfrm="na" 
	ms.devlang="python" 
	ms.topic="article" 
	ms.date="01/19/2016" 
	ms.author="ryancraw"/>

# Kit de développement logiciel (SDK) DocumentDB

> [AZURE.SELECTOR]
- [.NET SDK](documentdb-sdk-dotnet.md)
- [Node.js SDK](documentdb-sdk-node.md)
- [Java SDK](documentdb-sdk-java.md)
- [Python SDK](documentdb-sdk-python.md)

##Kit de développement logiciel (SDK) Python DocumentDB

<table> <tr><td>**Télécharger**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr> <tr><td>**Contribuer**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr> <tr><td>**Documentation**</td><td>[Documentation de référence pour le Kit de développement logiciel (SDK) Python](http://azure.github.io/azure-documentdb-python/)</td></tr> <tr><td>**Prise en main**</td><td>[Prise en main du Kit de développement logiciel (SDK) Python](documentdb-python-application.md)</td></tr> <tr><td>**Plateforme actuellement prise en charge**</td><td>[Python 2.7](https://www.python.org/download/releases/2.7/)</td></tr> </table></br>

## Notes de publication

### <a name="1.5.0"/>[1\.5.0](https://pypi.python.org/pypi/pydocumentdb/1.5.0)
- Ajoutez des programmes de résolution de partitions par hachage et par spécification de plages de valeurs pour vous aider lors du partitionnement des applications sur plusieurs partitions.

### <a name="1.4.2"/>[1\.4.2](https://pypi.python.org/pypi/pydocumentdb/1.4.2)
- Implémenter l'opération Upsert. Nouvelles méthodes UpsertXXX ajoutées pour prendre en charge la fonctionnalité Upsert.
- Implémenter l'ID en fonction du routage. Aucune modification d'API publique, toutes les modifications en interne.

### <a name="1.2.0"/>[1\.2.0](https://pypi.python.org/pypi/pydocumentdb/1.2.0)
- Prise en charge de l'index géospatial.
- Valide la propriété ID pour toutes les ressources. Les ID des ressources ne peuvent pas contenir les caractères ?, /, #, \\ ou se terminer par un espace.
- Ajoute le nouvel en-tête « progression de la transformation de l'index » à ResourceResponse.

### <a name="1.1.0"/>[1\.1.0](https://pypi.python.org/pypi/pydocumentdb/1.1.0)
- Implémente la stratégie d'indexation V2

### <a name="1.0.1"/>[1\.0.1](https://pypi.python.org/pypi/pydocumentdb/1.0.1)
- Prend en charge la connexion proxy

### <a name="1.0.0"/>[1\.0.0](https://pypi.python.org/pypi/pydocumentdb/1.0.0)
- Kit de développement logiciel (SDK) GA

## Dates de lancement et de suppression
Microsoft fournira une notification au moins **12 mois** avant le retrait d’un Kit de développement logiciel (SDK) pour faciliter la transition vers une version plus récente/prise en charge.

Les nouvelles fonctionnalités et fonctions, et les optimisations sont uniquement ajoutées au Kit de développement logiciel (SDK) actuel. Par conséquent, il est recommandé de toujours passer à la dernière version du SDK dès que possible.

Toute requête à DocumentDB utilisant un Kit de développement logiciel (SDK) supprimé est rejetée par le service.

> [AZURE.WARNING]Toutes les versions du Kit de développement logiciel (SDK) Azure DocumentDB pour Python antérieures à la version **1.0.0** seront supprimées le **29 février 2016**.

<br/>

| Version | Date de lancement | Date de suppression 
| ---	  | ---	         | ---
| [1\.5.0](#1.5.0) | 3 janvier 2016 |--- 
| [1\.4.2](#1.4.2) | 6 octobre 2015 |--- 
| [1\.4.1](#1.4.1) | 6 octobre 2015 |--- 
| [1\.2.0](#1.2.0) | 6 août 2015 |--- 
| [1\.1.0](#1.1.0) | 9 juillet 2015 |--- 
| [1\.0.1](#1.0.1) | 25 mai 2015 |--- 
| [1\.0.0](#1.0.0) | 7 avril 2015 |--- 
| 0.9.4-version préliminaire | 14 janvier 2015 | 29 février 2016 
| 0.9.3-version préliminaire | 9 décembre 2014 | 29 février 2016
| 0.9.2-version préliminaire | 25 novembre 2014 | 29 février 2016 
| 0.9.1-version préliminaire | 23 septembre 2014 | 29 février 2016 
| 0.9.0-version préliminaire | 21 août 2014 | 29 février 2016

## Forum Aux Questions
[AZURE.INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## Voir aussi

Pour en savoir plus sur DocumentDB, consultez la page du service [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).

<!---HONumber=AcomDC_0121_2016-->