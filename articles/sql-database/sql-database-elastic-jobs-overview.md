<properties
	pageTitle="Vue d’ensemble des travaux de base de données élastiques | Microsoft Azure" 
	description="Illustre le service de tâche de base de données élastique" 
	metaKeywords="azure sql database elastic databases" 
	services="sql-database" documentationCenter=""  
	manager="jeffreyg" 
	authors="ddove"/>

<tags 
	ms.service="sql-database" 
	ms.workload="sql-database" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="02/23/2016" 
	ms.author="ddove;sidneyh" />

# Vue d’ensemble des tâches de base de données élastiques

La fonction **travaux de base de données élastique** (version préliminaire) vous permet d’exécuter un script Transact-SQL (T-SQL) fiable ou d’appliquer un DACPAC ([application de la couche Données](https://msdn.microsoft.com/library/ee210546.aspx)) dans un groupe de bases de données, notamment :

* une collection personnalisée des bases de données (voir ci-après)
* toutes les bases de données dans le [pool de base de données élastique](sql-database-elastic-pool.md)
* un ensemble de partitions (créé à l’aide d’une [bibliothèque client de base de données élastique](sql-database-elastic-database-client-library.md)). 
 
Pour obtenir des instructions sur l’installation, consultez la page [Installation des composants de tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md). Consultez également [Prise en main des travaux de base de données élastiques](sql-database-elastic-jobs-getting-started.md).

La fonctionnalité **Tâches de bases de données élastiques** est actuellement un service cloud Azure hébergé client qui permet l’exécution de tâches administratives ad hoc et planifiées, appelées **travaux**. Grâce aux travaux, vous pouvez facilement gérer, de façon fiable, de grands groupes de bases de données SQL Azure en exécutant les scripts Transact-SQL pour effectuer des opérations administratives.

![Service de tâche de base de données élastique][1]

## Avantages
* Gérez facilement les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte télémétrique du locataire (client).
* Réduire des surcharges : normalement, vous devez vous connecter indépendamment à chaque base de données pour exécuter les instructions Transact-SQL ou effectuer d’autres tâches administratives. Un travail gère la tâche de connexion à chaque base de données dans le groupe cible.
* Comptabilité : les travaux exécutent le script et enregistre l’état d’exécution pour chaque base de données. 
* Flexibilité : la définition des groupes personnalisés de bases de données SQL Azure
* Définir, gérer et conserver des scripts Transact-SQL à exécuter dans un groupe de bases de données SQL Azure 
* Déployer une application de couche Données (DACPAC)
* Nouvelle tentative automatique lors de l’exécution de scripts
* Définir des calendriers d'exécution
* Agréger des données à partir d’une collection de bases de données SQL Azure dans un tableau de destination unique

> [AZURE.NOTE] Dans le portail Azure, seul un ensemble réduit de fonctions limitées aux pools élastiques SQL Azure est disponible. Utiliser les APIs PowerShell pour accéder à l'ensemble des fonctionnalités actuelles.

## Scénarios

* Tâche administrative de performances, par exemple le déploiement d'un nouveau schéma
* Mettre à jour les données de référence, par exemple les informations de produit communes à toutes les bases de données, même à l’aide des planifications pour automatiser les mises à jour chaque jour ouvrable après plusieurs heures.
* Recréer des indexes pour améliorer les performances d’une requête. La reconstruction peut être configurée pour s'exécuter dans une collection de bases de données de façon récurrente, par exemple pendant les heures creuses.
* Collecter les résultats de la requête à partir d'un ensemble de bases de données dans une table centrale sur une base continue. Les requêtes de performances peuvent être exécutées en permanence et configurées pour déclencher des tâches supplémentaires à exécuter.
* Exécuter des requêtes de traitement de données avec un temps d’exécution plus long sur un grand ensemble de bases de données, par exemple, la collection de télémétrie de client. Les résultats sont rassemblés dans une table de destination unique pour une analyse ultérieure.

## Travaux de base de données élastique : de bout en bout 
1.	Installez les composants de **travaux de bases de données élastiques**. Pour en savoir plus, consultez [Installation des tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md). Si l'installation échoue, voir [comment désinstaller](sql-database-elastic-jobs-uninstall.md).
2.	Utilisez les APIs PowerShell pour accéder à davantage de fonctionnalités, par exemple la création de collections de bases de données personnalisées, l’ajout de planifications et/ou la collecte des ensembles de résultats. Utilisez le portail pour une installation simple et la création/la surveillance de travaux limités à l’exécution par rapport à un **pool de bases de données élastiques**. 
3.	Créez des informations d’identification chiffrées pour l’exécution d’une tâche et [ajoutez l’utilisateur (ou le rôle) à chaque base de données du groupe](sql-database-security.md).
4.	Créez un script T-SQL idempotent qui peut être exécuté sur chacune des bases de données du pool. 
5.	Procédez comme suit pour créer des travaux à l’aide du portail Azure : [Création et gestion des travaux de base de données élastiques](sql-database-elastic-jobs-create-and-manage.md) 
6.	Ou utilisez des scripts PowerShell : [Création et gestion des travaux de base de données SQL élastiques à l’aide de PowerShell (version préliminaire)](sql-database-elastic-jobs-powershell.md).

## L’importance des scripts idempotent
Les scripts doivent être [idempotent](https://en.wikipedia.org/wiki/Idempotence). En termes simples, « idempotent » signifie que si le script réussit, et est réexécuté, le résultat est le même. Un script peut échouer en raison de problèmes réseau provisoires. Dans ce cas, le travail va automatiquement refaire des tentatives d’exécution du script un nombre prédéfini de fois. Un script idempotent a le même résultat, même s’il a été correctement exécuté deux fois.

Une tactique simple consiste à tester l’existence d’un objet avant de créer ce dernier.

	IF NOT EXIST (some_object)
	-- Create the object 
	-- If it exists, drop the object before recreating it.

De même, un script doit être capable d’exécuter avec succès par une vérification logique et s’adapter aux conditions qu’il rencontre.

## Échecs et journaux

Si un script échoue après plusieurs tentatives, le travail consigne l’erreur et continue. Après la fin d’un travail (en d’autres termes, son exécution sur toutes les bases de données dans le groupe), vous pouvez vérifier la liste de tentatives ayant échoué. Les journaux fournissent des détails pour déboguer des scripts défectueux.

## Types de groupe et création

Il existe deux types de groupes :

1. Ensemble de partitions
2. Groupes personnalisés

Les groupes d’ensembles de partitions sont créés à l’aide des [outils de base de données élastique](sql-database-elastic-scale-introduction.md). Lorsque vous créez un groupe de jeu de partitions, des bases de données sont ajoutées au groupe ou supprimées de ce dernier automatiquement. Par exemple, une nouvelle partition sera automatiquement créée dans le groupe. Un travail sera exécuté sur le groupe sans ajustement.

Les groupes personnalisés, quant à eux, sont définis de façon rigide. Vous devez explicitement ajouter ou supprimer des bases de données à partir de groupes personnalisés. Si une base de données du groupe est supprimée, le travail va tenter d’exécuter le script sur la base de données, ce qui entraînera une panne éventuelle. Les groupes créés actuellement à l’aide du portail Azure sont des groupes personnalisés.


## Composants et tarification 
Les composants suivants fonctionnent en synergie pour créer un service Cloud Azure permettant l'exécution ad hoc de tâches administratives. Les composants sont installés et configurés automatiquement pendant l'installation, dans le cadre de votre abonnement. Vous pouvez identifier les services car ils portent tous le même nom généré automatiquement. Le nom est unique et se compose d'un préfixe « edj » suivi de 21 caractères générés de façon aléatoire.

* **Service Cloud Azure**: les tâches de base de données élastiques (version préliminaire) sont fournies sous forme d'un service Cloud Azure hébergé par le client pour exécuter les tâches demandées. À partir du portail, le service est déployé et hébergé dans votre abonnement Microsoft Azure. Par défaut, le service déployé s'exécute avec un minimum de deux rôles de travail pour garantir une haute disponibilité. La taille par défaut de chaque rôle de travail (ElasticDatabaseJobWorker) s'exécute sur une instance A0. Pour la tarification, voir [Tarification des services cloud](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Base de données SQL Azure**: le service utilise une base de données SQL Azure appelée **base de données de contrôle** pour stocker toutes les métadonnées de la tâche. Le niveau de service par défaut est S0. Pour en savoir plus, voir [Tarification de la base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: Azure Service Bus sert à coordonner le travail au sein du service Cloud Azure. Voir [Tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).
* **Azure Storage**: un compte Azure Storage sert à stocker la journalisation des résultats de diagnostic au cas où un problème nécessite un débogage supplémentaire (consultez [Activation de Diagnostics dans les services cloud et les machines virtuelles Azure](../cloud-services/cloud-services-dotnet-diagnostics.md)). Pour la tarification, voir[Tarification d'Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

## Fonctionnement des tâches de bases de données élastiques
1.	Une base de données SQL Azure est conçue comme une base de données de contrôle qui stocke toutes les métadonnées et les données d’état.
2.	Pour accéder à la base de données de contrôle, accédez à la fonctionnalité **Tâches de bases de données élastiques** pour lancer les tâches à exécuter et en assurer le suivi.
3.	Deux rôles communiquent avec la base de données de contrôle : 
	* Contrôleur : détermine les tâches qui nécessitent d’autres tâches pour effectuer la tâche demandée, ainsi que les tâches des nouvelles tentatives ayant échoué en créant de nouvelles tâches.
	* Exécution de tâches de travail : exécute les tâches de travail.

### Types de tâches de travail
Il existe plusieurs types de tâches qui effectuent l'exécution des tâches :

* ShardMapRefresh : interroge la carte de partitions pour déterminer toutes les bases de données utilisées en tant que partitions
* ScriptSplit : répartit le script sur l’instruction « GO » dans des lots
* ExpandJob : crée des tâches enfants pour chaque base de données à partir d'une tâche qui cible un groupe de bases de données
* ScriptExecution : exécute un script sur une base de données spécifique à l'aide des informations d'identification définies
* Dacpac : applique un DACPAC à une base de données à spécifique à l'aide des informations d'identification spécifiques

## Flux de travail de l'exécution de tâche de bout en bout
1.	Une tâche est insérée dans la **base de données de contrôle** à l’aide du portail ou de l’API PowerShell. La tâche demande l'exécution d'un script Transact-SQL sur un groupe de bases de données à l'aide des informations d'identification spécifiques.
2.	Le contrôleur identifie la nouvelle tâche. Les tâches sont créées et exécutées pour fractionner le script et pour actualiser les bases de données du groupe. Enfin, une nouvelle tâche est créée et exécutée pour développer la tâche et créer des tâches enfants où chacune de celles-ci est configurée pour exécuter le script Transact-SQL sur une base de données individuelle du groupe.
3.	Le contrôleur identifie la nouvelle tâche enfant. Pour chaque tâche, le contrôleur crée et déclenche une tâche pour exécuter le script sur une base de données. 
4.	Une fois toutes les tâches terminées, le contrôleur met à jour et définit les tâches sur l’état terminé. À tout moment pendant l'exécution de la tâche, l'API PowerShell peut être utilisée pour afficher l'état actuel de l'exécution de la tâche. Toutes les heures retournées par les APIs PowerShell sont représentées au format UTC. Si vous le souhaitez, une demande d'annulation peut être lancée pour arrêter une tâche. 

## Étapes suivantes
[Installez les composants](sql-database-elastic-jobs-service-installation.md), puis [créez et ajoutez un journal dans chaque base de données du groupe](sql-database-security.md). Pour mieux comprendre la création et la gestion de tâches, consultez la page [Création et gestion de tâches de bases de données élastiques](sql-database-elastic-jobs-create-and-manage.md). Consultez également [Prise en main des travaux de base de données élastiques](sql-database-elastic-jobs-getting-started.md).

[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->

<!---HONumber=AcomDC_0224_2016-->