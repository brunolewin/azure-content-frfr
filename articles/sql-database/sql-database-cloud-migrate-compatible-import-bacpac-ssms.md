<properties
   pageTitle="Migration d’une base de données SQL Server vers une base de données SQL Azure"
   description="Microsoft Azure SQL Database, déployer base de données, migration base de données, importer base de données, exporter base de données, assistant de migration"
   services="sql-database"
   documentationCenter=""
   authors="carlrabeler"
   manager="jeffreyg"
   editor=""/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-management"
   ms.date="12/17/2015"
   ms.author="carlrab"/>

# Importation depuis BACPAC vers Base de données SQL avec SSMS

> [AZURE.SELECTOR]
- [SSMS](sql-database-cloud-migrate-compatible-import-bacpac-ssms.md)
- [SqlPackage](sql-database-cloud-migrate-compatible-import-bacpac-sqlpackage.md)
- [Azure Portal](sql-database-import.md)
- [PowerShell](sql-database-import-powershell.md)

Cet article explique la procédure d’importation depuis un fichier [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) vers Base de données SQL à l’aide de l’Assistant Exportation d’une Application de couche données dans SQL Server Management Studio.

> [AZURE.NOTE]Les étapes ci-dessous supposent que vous avez déjà déployé votre instance logique SQL Azure et que vous disposez des informations de connexion.

1. Assurez-vous de disposer de la dernière version de SQL Server Management Studio. Les nouvelles versions de Management Studio sont mises à jour tous les mois afin de refléter les mises à jour publiées sur le portail Azure.

	 >[AZURE.IMPORTANT]Nous vous recommandons d’utiliser systématiquement la dernière version de Management Studio afin de rester en cohérence avec les mises à jour de Microsoft Azure et Base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).

2. Ouvrez Management Studio et connectez-vous à votre base de données source dans l’Explorateur d’objets.

	![Exporter une application de la couche Données à partir du menu Tâches](./media/sql-database-cloud-migrate/MigrateUsingBACPAC01.png)

3. Une fois le fichier BACPAC créé, connectez-vous à votre serveur de Base de données SQL Azure, cliquez avec le bouton droit de la souris sur le dossier **Bases de données**, puis cliquez sur **Importer une application de la couche Données…**

    ![Importer l’élément de menu de l’application de la couche Données](./media/sql-database-cloud-migrate/MigrateUsingBACPAC03.png)

4.	Dans l’Assistant d’importation, sélectionnez le fichier BACPAC que vous venez d’exporter pour créer la base de données dans Azure SQL Database.

    ![Paramètres d’importation](./media/sql-database-cloud-migrate/MigrateUsingBACPAC04.png)

5.	Renseignez le **Nom de la nouvelle base de données** résidant sur la Base de données SQL Azure, définissez l’**Edition de Base de données SQL Microsoft Azure** (niveau de service), la **Taille maximale de base de données** et l’**Objectif de service** (niveau de performance).

    ![Paramètres de base de données](./media/sql-database-cloud-migrate/MigrateUsingBACPAC05.png)

6.	Cliquez sur **Suivant**, puis cliquez sur **Terminer** pour importer le fichier BACPAC dans une nouvelle base de données sur le serveur Base de données SQL Azure.

7. À l’aide de l’Explorateur d’objets, connectez-vous à la base de données que vous venez de déployer sur votre serveur de base de données SQL Azure.

8.	Dans le portail Azure, vous pouvez afficher votre base de données et ses propriétés.

<!---HONumber=AcomDC_1223_2015-->