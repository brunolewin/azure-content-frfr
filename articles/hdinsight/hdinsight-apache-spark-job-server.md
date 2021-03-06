<properties 
	pageTitle="Apache Spark Job Server sur HDInsight | Microsoft Azure" 
	description="Découvrez comment utiliser le serveur Spark Job Server pour soumettre et gérer des travaux à distance sur un cluster Spark." 
	services="hdinsight" 
	documentationCenter="" 
	authors="nitinme" 
	manager="paulettm" 
	editor="cgronlun"
	tags="azure-portal"/>

<tags 
	ms.service="hdinsight" 
	ms.workload="big-data" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="12/08/2015" 
	ms.author="nitinme"/>


# Spark Job Server sur des clusters Azure HDInsight (Windows)

> [AZURE.NOTE] HDInsight fournit désormais des clusters Spark sur Linux, qui utilise Livy à soumettre des tâches à distance à un cluster Spark. Pour plus d’informations sur l’utilisation de Livy avec des clusters HDInsight Spark sur Linux, consultez [Soumettre des tâches Spark à distance en utilisant Livy avec des clusters Spark sur HDInsight (Linux)](hdinsight-apache-spark-livy-rest-interface.md).

Le cluster Apache Spark sur Azure HDInsight package le serveur Spark Job Server dans le cadre du déploiement du cluster. Spark Job Server fournit des API REST pour créer un contexte Spark, soumettre l’application Spark au contexte, vérifiez l’état du travail, supprimer le contexte, etc. Cet article fournit quelques exemples sur l’utilisation de Curl pour effectuer certaines tâches courantes sur un cluster Spark à l’aide d’un serveur de travaux.

>[AZURE.NOTE] Pour obtenir la documentation complète de Spark Job Server, consultez [https://github.com/spark-jobserver/spark-jobserver](https://github.com/spark-jobserver/spark-jobserver).

## <a name="uploadjar"></a>Charger un fichier jar vers un cluster Spark

	curl.exe -k -u "<hdinsight user>:<user password>" --data-binary @<location of jar on the computer> https://<cluster name>.azurehdinsight.net/sparkjobserver/jars/<application name>

Exemple :
	
	curl.exe -k -u "myuser:myPass@word1" --data-binary @C:\mylocation\eventhubs-examples\target\spark-streaming-eventhubs-example-0.1.0-jar-with-dependencies.jar https://mysparkcluster.azurehdinsight.net/sparkjobserver/jars/streamingjar


##<a name="createcontext"></a>Créer un contexte persistant dans le serveur de tâches

	curl.exe -k -u "<hdinsight user>:<user password>" -d "" "https://<cluster name>.azurehdinsight.net/sparkjobserver/contexts/<context name>?num-cpu-cores=<value>&memory-per-node=<value>"

Exemple :

	curl.exe -k -u "myuser:myPass@word1" -d "" "https://mysparkcluster.azurehdinsight.net/sparkjobserver/contexts/mystreaming?num-cpu-cores=4&memory-per-node=1024m"


##<a name="submitapp"></a>Soumettre une application au cluster

	curl.exe -k -u "<hdinsight user>:<user password>" -d @<input file name> "https://<cluster name>.azurehdinsight.net/sparkjobserver/jobs?appName=<app name>&classPath=<class path>&context=<context>"

Exemple :

	curl.exe -k -u "myuser:myPass@word1" -d @mypostdata.txt "https://mysparkcluster.azurehdinsight.net/sparkjobserver/jobs?appName=streamingjar&classPath=org.apache.spark.streaming.eventhubs.example.EventCountJobServer&context=mystreaming"

où mypostdata.txt définit votre application.


##<a name="submitapp"></a>Supprimer une tâche

	curl.exe -X DELETE -k -u "<hdinsight user>:<user password>" "https://<cluster name>.azurehdinsight.net/sparkjobserver/contexts/<context>"

Exemple :

	curl.exe -X DELETE -k -u "myuser:myPass@word1" "https://mysparkcluster.azurehdinsight.net/sparkjobserver/contexts/mystreaming"


##<a name="seealso"></a>Voir aussi

* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview-v1.md)
* [Créer un cluster Spark sur HDInsight](hdinsight-apache-spark-provision-clusters.md)
* [Effectuer une analyse interactive des données à l’aide de Spark sur HDInsight avec des outils décisionnels](hdinsight-apache-spark-use-bi-tools-v1.md)
* [Utiliser Spark sur HDInsight pour créer des applications d’apprentissage automatique](hdinsight-apache-spark-ipython-notebook-machine-learning-v1.md)
* [Utiliser Spark sur HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-csharp-apache-zeppelin-eventhub-streaming.md)
* [Gérer les ressources du cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)


[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: storage-create-storage-account.md

<!---HONumber=AcomDC_0218_2016-->