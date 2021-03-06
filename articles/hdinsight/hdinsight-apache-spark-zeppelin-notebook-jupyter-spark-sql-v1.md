<properties 
	pageTitle="Créer un cluster Spark sur HDInsight et utiliser Spark SQL à partir de Zeppelin et Jupyter pour effectuer une analyse interactive | Azure" 
	description="Des instructions pas à pas expliquent comment créer rapidement un cluster Apache Spark dans HDInsight, puis comment utiliser Spark SQL à partir des blocs-notes Zeppelin et Jupyter pour exécuter des requêtes interactives." 
	services="hdinsight" 
	documentationCenter="" 
	authors="nitinme" 
	manager="paulettm" 
	editor="cgronlun"/>

<tags 
	ms.service="hdinsight" 
	ms.workload="big-data" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="12/22/2015" 
	ms.author="nitinme"/>


# Démarrage rapide : Créer Apache Spark sur HDInsight et exécuter des requêtes interactives à l’aide de Spark SQL (Windows)

[AZURE.INCLUDE [portail-azure-hdinsight](../../includes/hdinsight-azure-portal.md)]

* [Créer Apache Spark sur HDInsight et exécuter des requêtes interactives à l’aide de Spark SQL](hdinsight-apache-spark-jupyter-spark-sql.md)

Découvrez comment créer un cluster Apache Spark dans HDInsight à l’aide de l’option Création rapide, puis comment utiliser les blocs-notes [Zeppelin](https://zeppelin.incubator.apache.org) et [Jupyter](https://jupyter.org) basés sur le web pour exécuter des requêtes interactives Spark SQL sur le cluster Spark.


   ![Prendre en main Apache Spark dans HDInsight](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.getstartedflow.png "Didacticiel de prise en main d’Apache Spark dans HDInsight. Étapes illustrées : créer un compte de stockage ; créer un cluster ; exécuter des instructions Spark SQL")

**Configuration requise :**

Avant de commencer ce didacticiel, vous devez disposer d’un abonnement Azure. Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

##<a name="storage"></a>Création d'un compte de stockage Azure

Lors de la création d’un cluster HDInsight dans HDInsight, vous devez spécifier un compte Azure Storage. Un conteneur de stockage d’objets blob spécifique de ce compte est désigné comme système de fichiers par défaut. Par défaut, le cluster HDInsight est créé dans le même centre de données que le compte de stockage que vous spécifiez. Pour plus d'informations, consultez la page [Utilisation du stockage d’objets blob Azure avec HDInsight][hdinsight-storage].


**Pour créer un compte Azure Storage**

1. Connectez-vous au [portail Azure][azure-management-portal].
2. Cliquez sur **NOUVEAU** dans l'angle inférieur gauche, puis entrez les valeurs comme indiqué dans l'image.

	![Portail Azure où vous pouvez utiliser l’option Création rapide pour configurer un nouveau compte de stockage](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.storageaccount.quickcreate.png "Portail Azure où vous pouvez utiliser l’option Création rapide pour configurer un nouveau compte de stockage")

>[AZURE.NOTE]  Veillez à créer le compte de stockage à un emplacement pris en charge pour le cluster.

Sélectionnez le nouveau compte de stockage dans la liste et cliquez sur **GÉRER LES CLÉS D'ACCÈS** au bas de la page. Notez la **CLÉ D'ACCÈS PRIMAIRE** (ou la **CLÉ D'ACCÈS SECONDAIRE**, les deux peuvent être utilisées). Vous en aurez besoin plus tard dans le didacticiel. Pour plus d'informations, consultez [Création d'un compte de stockage][azure-create-storageaccount].
	
##Créer un cluster HDInsight Spark

Dans cette section, vous allez créer un cluster HDInsight version 3.2, qui est basé sur la version 1.3.1 de Spark. Pour en savoir plus sur les différentes versions de HDInsight et leurs contrats SLA, consultez la page [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).

>[AZURE.NOTE] Les étapes décrites dans cet article permettent de créer un cluster Apache Spark dans HDInsight à l’aide des paramètres de configuration de base. Pour plus d’informations sur les autres paramètres de configuration de cluster (comme l’utilisation d’un espace de stockage supplémentaire, d’un réseau virtuel Azure ou d’un metastore pour Hive), consultez [Créer des clusters HDInsight à l’aide d’options personnalisées](hdinsight-apache-spark-provision-clusters.md).


**Pour créer un cluster Spark**

1. Connectez-vous au [portail Azure][azure-management-portal]. 

2. Cliquez sur **NOUVEAU** dans l'angle inférieur gauche, puis entrez les valeurs comme indiqué dans l'image.

	![Créer un cluster Spark dans HDInsight](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.quickcreatecluster.png "Créer un cluster Spark dans HDInsight")


##<a name="zeppelin"></a>Exécuter des requêtes Spark SQL interactives à l’aide d’un bloc-notes Zeppelin

Après avoir créé un cluster, vous pouvez utiliser un bloc-notes Zeppelin basé sur le web pour exécuter des requêtes Spark SQL interactives sur le cluster HDInsight Spark. Dans cette section, nous allons utiliser un fichier exemple de données (hvac.csv), qui est disponible par défaut sur le cluster pour exécuter des requêtes Spark SQL interactives.

>[AZURE.NOTE] Le bloc-notes que vous créez en suivant les instructions ci-dessous est également disponible par défaut sur le cluster. Une fois Zeppelin lancé, vous pouvez trouver le bloc-notes en lançant une recherche sur le nom **Zeppelin HVAC tutorial**.

1. Dans le volet gauche [Portail Azure][azure-management-portal], cliquez sur **HDInsight**, puis sur le cluster Spark que vous avez créé. Dans la page de cluster Spark, dans le volet inférieur, cliquez sur **Bloc-notes Zeppelin**. Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.

	> [AZURE.NOTE] Vous pouvez également atteindre le bloc-notes Zeppelin pour votre cluster en ouvrant l'URL suivante dans votre navigateur. Remplacez __CLUSTERNAME__ par le nom de votre cluster.
	>
	> `https://CLUSTERNAME.azurehdinsight.net/zeppelin`

2. Créer un nouveau bloc-notes. Dans le volet d'en-tête, cliquez sur **Bloc-notes**, puis sur **Créer une note**.

	![Créer un bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.createnewnote.png "Créer un nouveau bloc-notes Zeppelin")

	Dans la même page, sous le titre **Bloc-notes**, un nouveau bloc-notes dont le nom commence par **Note XXXXXXXXX** doit s’afficher. Cliquez sur le nouveau bloc-notes.

3. Sur la page web du nouveau bloc-notes, cliquez sur l'en-tête et modifiez le nom du bloc-notes si vous le souhaitez. Appuyez sur ENTRÉE pour enregistrer la modification de nom. Vérifiez également que l’en-tête du bloc-notes indique l’état **Connected** dans le coin supérieur droit.

	![État du bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.newnote.connected.png "État du bloc-notes Zeppelin")

4. Chargez un exemple de données dans une table temporaire. Lorsque vous créez un cluster Spark dans HDInsight, l’exemple de fichier de données **hvac.csv** est copié vers le compte de stockage associé dans **\\HdiSamples\\SensorSampleData\\hvac**.

	Collez l’extrait suivant dans le paragraphe vide créé par défaut dans le nouveau bloc-notes.

		// Create an RDD using the default Spark context, sc
		val hvacText = sc.textFile("wasb:///HdiSamples/SensorSampleData/hvac/HVAC.csv")
		
		// Define a schema
		case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
		
		// Map the values in the .csv file to the schema
		val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
    		s => Hvac(s(0), 
            		s(1),
            		s(2).toInt,
            		s(3).toInt,
            		s(6)
        	)
		).toDF()
		
		// Register as a temporary table called "hvac"
		hvac.registerTempTable("hvac")
		
	Appuyez sur **MAJ + ENTRÉE** ou cliquez sur le bouton **Lire** pour que le paragraphe exécute l'extrait de code. L’état indiqué dans le coin supérieur droit du paragraphe doit progresser de READY, PENDING, RUNNING à FINISHED. Le résultat s’affiche au bas du même paragraphe. La capture d’écran ressemble à ceci :

	![Créer une table temporaire à partir de données brutes](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.note.loaddataintotable.png "Créer une table temporaire à partir de données brutes")

	Vous pouvez également indiquer un titre pour chaque paragraphe. Dans le coin droit, cliquez sur l’icône **Settings**, puis sur **Show title**.

5. Vous pouvez maintenant exécuter des instructions Spark SQL dans la table **hvac**. Collez la requête suivante dans un nouveau paragraphe. La requête récupère l’ID de bâtiment et la différence entre les températures cibles et réelles pour chaque bâtiment à une date donnée. Appuyez sur **MAJ + ENTRÉE**.

		%sql
		select buildingID, (targettemp - actualtemp) as temp_diff, date 
		from hvac
		where date = "6/1/13" 

	L'instruction **%sql** du début indique au bloc-notes d'utiliser l'interpréteur Spark SQL. Vous pouvez consulter les interpréteurs définis dans l'onglet **Interpreter** dans l'en-tête du bloc-notes.

	La capture d’écran qui suit présente le résultat.

	![Exécuter une instruction Spark SQL à l’aide du bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.note.sparksqlquery1.png "Exécuter une instruction Spark SQL à l’aide du bloc-notes")

	 Cliquez sur les options d’affichage (mis en exergue dans un rectangle) pour basculer entre les différentes représentations du même résultat. Cliquez sur **Paramètres** pour choisir ce qui constitue la clé et les valeurs dans le résultat. La capture d'écran ci-dessus utilise la clé **buildingID** et la moyenne **temp\_diff** comme valeur.

	
6. Vous pouvez également exécuter des instructions Spark SQL à l’aide de variables dans la requête. L’extrait suivant montre comment définir la variable **Temp** dans la requête avec les valeurs possibles d’interrogation. Lors de la première exécution de la requête, une liste déroulante est automatiquement renseignée avec les valeurs que vous avez spécifiées pour la variable.

		%sql
		select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff
		from hvac
		where targettemp > "${Temp = 65,65|75|85}" 

	Collez cet extrait dans un nouveau paragraphe, puis appuyez sur **MAJ + ENTRÉE**. La capture d’écran qui suit présente le résultat.

	![Exécuter une instruction Spark SQL à l’aide du bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.note.sparksqlquery2.png "Exécuter une instruction Spark SQL à l’aide du bloc-notes")

	Pour les requêtes suivantes, vous pouvez sélectionner une nouvelle valeur dans la liste déroulante et réexécuter la requête. Cliquez sur **Settings** pour choisir ce qui constitue la clé et les valeurs dans le résultat. La capture d'écran ci-dessus utilise la clé **buildingID**, la moyenne **temp\_diff** comme valeur, et le groupe **targettemp**.

7. Redémarrez l’interpréteur Spark SQL pour quitter l’application. Cliquez sur l’onglet **Interpreter** en haut de l’écran et, pour l’interpréteur Spark, cliquez sur **Restart**.

	![Redémarrer l’interpréteur Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.zeppelin.restart.interpreter.png "Redémarrer l’interpréteur Zeppelin")

##<a name="jupyter"></a>Exécuter des requêtes Spark SQL à l’aide d’un bloc-notes Jupyter

Dans cette section, vous allez utiliser un bloc-notes Jupyter pour exécuter des requêtes Spark SQL sur un cluster Spark.

>[AZURE.NOTE] Le bloc-notes que vous créez en suivant les instructions ci-dessous est également disponible par défaut sur le cluster. Une fois Jupyter lancé, vous trouverez le bloc-notes en lançant une recherche sur **HVACTutorial.ipynb**.

1. Dans le volet gauche [Portail Azure][azure-management-portal], cliquez sur **HDInsight**, puis sur le cluster Spark que vous avez créé. Dans la page de cluster Spark, dans le volet inférieur, cliquez sur **Bloc-notes Zeppelin**. Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.

	> [AZURE.NOTE] Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur. Remplacez __CLUSTERNAME__ par le nom de votre cluster.
	>
	> `https://CLUSTERNAME.azurehdinsight.net/jupyter`

2. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **Python 2**.

	![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.note.jupyter.createnotebook.png "Créer un bloc-notes Jupyter")

3. Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb. Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.

	![Fournir un nom pour le bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.note.jupyter.notebook.name.png "Fournir un nom pour le bloc-notes")

4. Importez les modules requis et créez les contextes Spark et SQL. Collez l'extrait suivant dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.

		from pyspark import SparkContext
		from pyspark.sql import SQLContext
		from pyspark.sql.types import *

		# Create Spark and SQL contexts
		sc = SparkContext('spark://headnodehost:7077', 'pyspark')
		sqlContext = SQLContext(sc)

	À chaque exécution d’un travail dans Jupyter, le titre de la fenêtre du navigateur web affiche l’état **(Occupé)** ainsi que le titre du bloc-notes. Un cercle plein s’affiche également en regard du texte **Python 2** dans le coin supérieur droit. Une fois le travail terminé, ce cercle est remplacé par un cercle vide.

	 ![État d’un travail de bloc-notes Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.jupyter.job.status.png "État d’un travail de bloc-notes Jupyter")

4. Chargez un exemple de données dans une table temporaire. Lorsque vous créez un cluster Spark dans HDInsight, l’exemple de fichier de données **hvac.csv** est copié vers le compte de stockage associé dans **\\HdiSamples\\SensorSampleData\\hvac**.

	Dans une cellule vide, collez l’extrait suivant, puis appuyez sur **MAJ + ENTRÉE**. Cet extrait enregistre les données dans une table temporaire appelée **hvac**.


		# Load the data
		hvacText = sc.textFile("wasb:///HdiSamples/SensorSampleData/hvac/HVAC.csv")
		
		# Create the schema
		hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])
		
		# Parse the data in hvacText
		hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))
		
		# Create a data frame
		hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)
		
		# Register the data fram as a table to run queries against
		hvacdf.registerAsTable("hvac")
		
		# Run queries against the table and display the data
		data = sqlContext.sql("select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13"")
		data.show()

5. Une fois le travail terminé, le résultat suivant s’affiche.

		buildingID temp_diff date  
		4          8         6/1/13
		3          2         6/1/13
		7          -10       6/1/13
		12         3         6/1/13
		7          9         6/1/13
		7          5         6/1/13
		3          11        6/1/13
		8          -7        6/1/13
		17         14        6/1/13
		16         -3        6/1/13
		8          -8        6/1/13
		1          -1        6/1/13
		12         11        6/1/13
		3          14        6/1/13
		6          -4        6/1/13
		1          4         6/1/13
		19         4         6/1/13
		19         12        6/1/13
		9          -9        6/1/13
		15         -10       6/1/13

6. Redémarrez le noyau pour quitter l’application. Dans la barre de menus supérieure, cliquez successivement sur **Kernel**, **Restart** et **Restart** à nouveau lorsque vous y êtes invité.

	![Redémarrer le noyau Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql-v1/hdispark.jupyter.restart.kernel.png "Redémarrer le noyau Jupyter")


##<a name="seealso"></a>Voir aussi


* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview-v1.md)
* [Créer un cluster Spark sur HDInsight](hdinsight-apache-spark-provision-clusters.md)
* [Effectuer une analyse interactive des données à l’aide de Spark sur HDInsight avec des outils décisionnels](hdinsight-apache-spark-use-bi-tools-v1.md)
* [Utiliser Spark sur HDInsight pour créer des applications d’apprentissage automatique](hdinsight-apache-spark-ipython-notebook-machine-learning-v1.md)
* [Utiliser Spark sur HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-csharp-apache-zeppelin-eventhub-streaming.md)
* [Gérer les ressources du cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-resource-manager-v1.md)


[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md

<!---HONumber=AcomDC_0218_2016-->