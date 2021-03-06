<properties 
	pageTitle="Utilisation d’une action de script pour installer Apache Spark sur HDInsight basé sur Linux (Hadoop) | Microsoft Azure" 
	description="Découvrez comment installer Spark sur un cluster HDInsight basé sur Linux à l’aide des actions de script. Les actions de script vous permettent de personnaliser le cluster pendant la création, en modifiant la configuration du cluster ou en installant des services et des utilitaires." 
	services="hdinsight" 
	documentationCenter="" 
	authors="Blackmist" 
	manager="paulettm" 
	editor="cgronlun"/>

<tags 
	ms.service="hdinsight" 
	ms.workload="big-data" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="02/05/2016" 
	ms.author="larryfr"/>

# Installation et utilisation de Spark sur des clusters HDInsight Hadoop

Dans ce document, vous allez apprendre à installer Spark à l’aide d’une action de script. Une action de script vous permet d'exécuter des scripts pour personnaliser un cluster, uniquement au moment de sa création. Pour plus d’informations, consultez la page [Personnalisation d’un cluster HDInsight à l’aide d’une action de script][hdinsight-cluster-customize]. Vous verrez ensuite comment exécuter une requête Spark sur des clusters HDInsight.

> [AZURE.NOTE] HDInsight fournit aussi Spark comme type de cluster, ce qui signifie que vous pouvez désormais approvisionner directement un cluster Spark sans modifier de cluster Hadoop. Toutefois, ceci est actuellement limité aux clusters basés sur Windows. À l’aide du type de cluster Spark, vous obtenez un cluster basé sur Windows HDInsight version 3.2 avec Spark version 1.3.1. Pour plus d’informations, consultez [Prise en main d’Apache Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql.md).

## <a name="whatis"></a>Qu’est-ce que Spark ?

<a href="http://spark.apache.org/docs/latest/index.html" target="_blank">Apache Spark</a> est une infrastructure de traitement parallèle open source qui prend en charge le traitement en mémoire pour améliorer les performances des applications d’analyse de données volumineuses. De par ses capacités de calcul en mémoire, Spark constitue le choix idéal pour les algorithmes itératifs utilisés dans les calculs d'apprentissage machine et de graphiques.

Spark permet également d'effectuer des opérations standard de traitement des données sur disque. En évitant les écritures sur disque lors des étapes intermédiaires, Spark améliore l’infrastructure MapReduce traditionnelle. En outre, Spark est compatible avec le système HDFS (Hadoop Distributed File System) et le stockage d’objets blob Azure ; les données existantes peuvent dont être traitées facilement via Spark.

Cette rubrique contient des instructions de personnalisation d'un cluster HDInsight pour installer Spark.

## <a name="whatis"></a>Quelle version de Spark puis-je installer ?

Dans cette rubrique, nous utilisons un script personnalisé d’action de script pour installer Spark sur un cluster HDInsight. Ce script installe Spark 1.5.1.

Vous pouvez modifier ce script ou créer votre propre script pour installer d’autres versions de Spark.

## Ce que fait le script

Ce script installe Spark version 1.5.1 dans `/usr/hdp/current/spark`.

> [AZURE.WARNING] Vous pouvez constater que certains fichiers binaires Spark 1.3.1 sont installés par défaut sur votre cluster HDInsight. Ces derniers ne doivent pas être utilisés et seront supprimés de l’image de cluster HDInsight dans une mise à jour future.

## <a name="install"></a>Installer Spark à l’aide d’actions de script

Un exemple de script pour installer Spark sur un cluster HDInsight est disponible depuis un objet blob de stockage Azure à l’adresse [https://hdiconfigactions.blob.core.windows.net/linuxsparkconfigactionv02/spark-installer-v02.sh](https://hdiconfigactions.blob.core.windows.net/linuxsparkconfigactionv02/spark-installer-v02.sh). Cette section explique comment utiliser l’exemple de script dans le cadre de la création du cluster à l’aide du portail Azure.

> [AZURE.NOTE] Vous pouvez également utiliser Azure PowerShell ou le Kit de développement logiciel (SDK) .NET HDInsight pour créer un cluster à l’aide de ce script. Pour plus d’informations sur ces méthodes, consultez [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).

1. Démarrez la création d’un cluster à l’aide de la procédure décrite dans [Création de clusters HDInsight sous Linux](hdinsight-hadoop-create-linux-clusters-portal.md), mais ne terminez pas la création.

2. Dans le panneau **Configuration facultative**, sélectionnez **Actions de script**, puis indiquez les informations ci-dessous :

	* __NAME__ : saisissez un nom convivial pour l’action de script.
	* __SCRIPT URI__ : https://hdiconfigactions.blob.core.windows.net/linuxsparkconfigactionv02/spark-installer-v02.sh
	* __HEAD__ : cochez cette option.
	* __WORKER__ : décochez cette option.
	* __ZOOKEEPER__: décochez cette option.
	* __PARAMETERS__ : laissez ce champ vide.
    
    > [AZURE.NOTE] L’exemple de script Spark installe uniquement les composants sur les nœuds principaux ; vous pouvez donc décocher les autres types de nœuds.

3. En bas de l’écran **Actions de script**, utilisez le bouton **Sélectionner** pour enregistrer la configuration. Enfin, utilisez le bouton **Sélectionner** au bas du panneau **Configuration facultative** pour enregistrer les informations de configuration facultatives.

4. Continuez l’approvisionnement du cluster, comme décrit dans [Créer des clusters HDInsight sous Linux](hdinsight-provision-linux-clusters.md#portal).

## <a name="usespark"></a>Utilisation de Spark dans HDInsight

Spark fournit des API en Scala, Python et Java. Vous pouvez aussi utiliser l'interpréteur de commandes Spark interactif pour exécuter des requêtes Spark. Une fois votre cluster créé, utilisez les éléments suivants pour vous connecter à votre cluster HDInsight :

	ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
	
Pour plus d’informations sur l’utilisation de SSH avec HDInsight, consultez les articles suivants :

* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md)

* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](hdinsight-hadoop-linux-use-ssh-windows.md)

Une fois connecté, utilisez les sections suivantes pour connaître les étapes spécifiques sur l’utilisation de Spark :

- [Utilisation de l’interpréteur de commandes Spark pour exécuter des requêtes interactives](#sparkshell)
- [Utilisation de l’interpréteur de commandes Spark pour exécuter des requêtes Spark SQL](#sparksql) 
- [Utilisation d’un programme Scala autonome](#standalone)

###<a name="sparkshell"></a>Utilisation de l’interpréteur de commandes Spark pour exécuter des requêtes interactives

1. Exécutez la commande suivante pour démarrer l’interpréteur de commandes Spark :

		 /usr/hdp/current/spark/bin/spark-shell --master yarn

	Une fois la commande terminée, vous devez obtenir une invite Scala :

		 scala>

5. À l'invite Scala, entrez la requête Spark indiquée ci-dessous. Cette requête compte les occurrences de chaque mot dans le fichier davinci.txt disponible à l’emplacement /example/data/gutenberg/ sur le stockage d’objets blob Azure associé au cluster.

		val file = sc.textFile("/example/data/gutenberg/davinci.txt")
		val counts = file.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_ + _)
		counts.toArray().foreach(println)

6. La sortie doit ressembler à ce qui suit :

		(felt,,1)
		(axle-tree,1)
		(deals,9)
		(virtuous,4)

7. Entrez :q pour quitter l'invite Scala.

		:q

###<a name="sparksql"></a>Utilisation de l’interpréteur de commandes Spark pour exécuter des requêtes Spark SQL

Spark SQL vous permet d’utiliser Spark pour exécuter des requêtes relationnelles exprimées en langage SQL (Structured Query), HiveQL ou Scala. Dans cette section, nous allons examiner l’utilisation de Spark pour exécuter une requête Hive sur un exemple de table Hive. La table Hive utilisée dans cette section (appelée **hivesampletable**) est disponible par défaut quand vous créez un cluster.

1. Exécutez la commande suivante pour démarrer l’interpréteur de commandes Spark :

		 /usr/hdp/current/spark/bin/spark-shell --master yarn

	Une fois la commande terminée, vous devez obtenir une invite Scala :

		 scala>

2. À l’invite Scala, définissez le contexte Hive. Cela est nécessaire pour travailler avec des requêtes Hive en utilisant Spark.

		val hiveContext = new org.apache.spark.sql.hive.HiveContext(sc)

	> [AZURE.NOTE]  Dans cette instruction, `sc` est le contexte Spark par défaut qui est défini quand vous démarrez l’interpréteur de commandes Spark.

5. Exécutez une requête Hive en utilisant le contexte Hive et imprimez le résultat sur la console. La requête extrait des données sur des appareils d’une marque spécifique et limite le nombre d’enregistrements récupérés à 20.

		hiveContext.sql("""SELECT * FROM hivesampletable WHERE devicemake LIKE "HTC%" LIMIT 20""").collect().foreach(println)

6. Un résultat similaire à ce qui suit s’affiche normalement :

		[820,11:35:17,fr-FR,Android,HTC,Inspire 4G,Louisiana,UnitedStates, 2.7383836,0,1]
		[1055,17:24:08,fr-FR,Android,HTC,Incredible,Ohio,United States,18.0894738,0,0]
		[1067,03:42:29,fr-FR,Windows Phone,HTC,HD7,District Of Columbia,United States,null,0,0]

7. Entrez :q pour quitter l'invite Scala.

		:q

### <a name="standalone"></a>Utilisation d’un programme Scala autonome

Dans cette section, vous allez écrire une application Scala qui compte le nombre de lignes contenant les lettres « a » et « b » dans un exemple de fichier de données (/example/data/gutenberg/davinci.txt).

1. Utilisez les commandes suivantes pour installer Scala Build Tool :

		echo "deb http://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
		sudo apt-get update
		sudo apt-get install sbt
		
	Quand vous y êtes invité, sélectionnez __Y__ pour continuer.

2. Créez la structure de répertoire du projet Scala :

		mkdir -p SimpleScalaApp/src/main/scala
		
3. Créez un fichier nommé __simple.sbt__ contenant les informations de configuration pour ce projet.

		cd SimpleScalaApp
		nano simple.sbt
		
	Utilisez les données suivantes comme contenu du fichier :

		name := "SimpleApp"
	
		version := "1.0"
	
		scalaVersion := "2.10.4"
	
		libraryDependencies += "org.apache.spark" %% "spark-core" % "1.2.0"


	> [AZURE.NOTE] Veillez à conserver les lignes vides entre chaque entrée.
	
	Utilisez __Ctrl+X__, puis __Y__ et __Entrée__ pour enregistrer le fichier.

4. Utilisez la commande suivante pour créer un fichier nommé __SimpleApp.scala__ dans le répertoire __SimpleScalaApp/src/main/scala__ :

		nano src/main/scala/SimpleApp.scala

	Utilisez les données suivantes comme contenu du fichier :

		/* SimpleApp.scala */
		import org.apache.spark.SparkContext
		import org.apache.spark.SparkContext._
		import org.apache.spark.SparkConf
		
		object SimpleApp {
		  def main(args: Array[String]) {
		    val logFile = "/example/data/gutenberg/davinci.txt"			//Location of the sample data file on Azure Blob storage
		    val conf = new SparkConf().setAppName("SimpleApplication")
		    val sc = new SparkContext(conf)
		    val logData = sc.textFile(logFile, 2).cache()
		    val numAs = logData.filter(line => line.contains("a")).count()
		    val numBs = logData.filter(line => line.contains("b")).count()
		    println("Lines with a: %s, Lines with b: %s".format(numAs, numBs))
		  }
		}

	Utilisez __Ctrl+X__, puis __Y__ et __Entrée__ pour enregistrer le fichier.

5. À partir du répertoire __SimpleScalaApp__, utilisez la commande suivante pour générer l’application et la stocker dans un fichier jar :

		sbt package

	Une fois l’application compilée, le fichier **simpleapp\_2.10-1.0.jar** est créé dans le répertoire \_\_SimpleScalaApp/target/scala-2.10**.

6. Utilisez la commande suivante pour exécuter le programme SimpleApp.scala :


		/usr/hdp/current/spark/bin/spark-submit --class "SimpleApp" --master yarn target/scala-2.10/simpleapp_2.10-1.0.jar

4. Une fois l'exécution du programme terminée, la sortie s'affiche dans la console.

		Lines with a: 21374, Lines with b: 11430

## Étapes suivantes

- [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md). Hue est une interface utilisateur web qui permet de facilement créer, exécuter et enregistrer des tâches Pig et Hive, ainsi que de parcourir le stockage par défaut pour votre cluster HDInsight.

- [Installation de R sur des clusters HDInsight][hdinsight-install-r] fournit des instructions sur l’utilisation de la personnalisation des clusters pour installer et utiliser R sur des clusters HDInsight Hadoop. R se compose d'un langage et d'un environnement open source destinés au calcul de statistiques. Il intègre des centaines de fonctions statistiques et possède son propre langage de programmation qui regroupe des aspects de la programmation fonctionnelle et de la programmation orientée objet. Il offre également des fonctionnalités graphiques étendues.

- [Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilisez la personnalisation de clusters pour installer Giraph sur des clusters HDInsight Hadoop. Giraph permet de traiter des graphiques à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.

- [Installation de Solr sur des clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilisez la personnalisation de clusters pour installer Solr sur des clusters HDInsight Hadoop. Solr vous permet d'effectuer de puissantes opérations de recherche sur des données stockées.

- [Installer Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md). Utilisez la personnalisation de clusters pour installer Hue sur des clusters HDInsight Hadoop. Hue est un ensemble d’applications web permettant d’interagir avec un cluster Hadoop.



[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
 

<!---HONumber=AcomDC_0211_2016-->