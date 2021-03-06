<properties 
   pageTitle="Mise en route avec TSQL et le chiffrement transparent des données (TDE) pour SQL Data Warehouse | Microsoft Azure" 
   description="Mise en route avec TSQL et le chiffrement transparent des données (TDE) pour SQL Data Warehouse" 
   services="sql-data-warehouse" 
   documentationCenter="" 
   authors="twounder" 
   manager="barbkess" 
   editor=""/>

<tags 
   ms.service="sql-data-warehouse" 
   ms.workload="data-management" 
   ms.tgt_pltfrm="na" 
   ms.devlang="na" 
   ms.topic="article" 
   ms.date="01/07/2016" 
   ms.author="mausher;barbkess;sonyama"/>
 
# Prise en main du chiffrement transparent des données (TDE)
> [AZURE.SELECTOR]
- [Azure Classic Portal](sql-data-warehouse-encryption-tde.md)
- [TSQL](sql-data-warehouse-encryption-tde-tsql.md)

La fonction de chiffrement transparent des données (TDE) d’Azure SQL Data Warehouse protège le système contre toute menace d’activité malveillante, en effectuant un chiffrement et un déchiffrement en temps réel de la base de données, des sauvegardes associées et des fichiers journaux de transactions au repos, sans exiger de modification de l’application.

Le chiffrement transparent des données chiffre le stockage d’une base de données entière à l’aide d’une clé symétrique appelée clé de chiffrement de base de données. Dans la base de données SQL, la clé de chiffrement de base de données est protégée par un certificat de serveur intégré. Le certificat de serveur intégré est unique pour chaque serveur de base de données SQL. Microsoft alterne automatiquement ces certificats au moins tous les 90 jours. Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].

##Activation du chiffrement

Pour activer le chiffrement transparent des données pour SQL Data Warehouse, procédez comme suit :

1. Connectez-vous à la base de données *master* sur le serveur hébergeant la base de données à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master
2. Exécutez l'instruction suivante pour chiffrer la base de données.

```
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

##Désactivation du chiffrement

Pour désactiver le chiffrement transparent des données pour SQL Data Warehouse, procédez comme suit :

1. Connectez-vous à la base de données *master* à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master
2. Exécutez l'instruction suivante pour chiffrer la base de données.

```
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

##Vérification de chiffrement

Pour vérifier l’état du chiffrement pour SQL Data Warehouse, procédez comme suit :

1. Connectez-vous à la base de données *master* ou d’instance à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master
2. Exécutez l'instruction suivante pour chiffrer la base de données.

```
SELECT
	[name],
	[is_encrypted]
FROM
	sys.databases;
```

Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.

 
<!--Anchors-->
[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->

<!---HONumber=AcomDC_0114_2016-->