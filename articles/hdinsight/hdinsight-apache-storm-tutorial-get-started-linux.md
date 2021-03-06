<properties
	pageTitle="Didacticiel Apache Storm : prise en main de Storm sur HDInsight basé sur Linux | Microsoft Azure"
	description="Prise en main de l’analyse Big Data avec Apache Storm et des exemples Starter Storm sur HDInsight basé sur HDInsight. Découvrez comment utiliser Storm pour traiter les données en temps réel."
	keywords="apache storm,didacticiel apache storm,analyses big data,prise en main storm"
	services="hdinsight"
	documentationCenter=""
	authors="Blackmist"
	manager="paulettm"
	editor="cgronlun"/>

<tags
   ms.service="hdinsight"
   ms.devlang="java"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="na"
   ms.workload="big-data"
   ms.date="03/07/2016"
   ms.author="larryfr"/>


# Didacticiel Apache Storm : prise en main d'exemples Storm Starter pour l'analyse de données volumineuses (« Big Data ») sur HDInsight

Apache Storm est un système de calcul en temps réel, évolutif, distribué, à tolérance de panne, qui permet de traiter des flux de données. Avec Storm sur Azure HDInsight, vous pouvez créer un cluster Storm basé sur le cloud qui effectue l’analyse de données volumineuses en temps réel.

> [AZURE.NOTE] Les étapes décrites dans cet article créent un cluster HDInsight Linux. Pour savoir comment créer un cluster Storm Windows sur HDInsight, consultez le [Didacticiel Apache Storm : prise en main de l’exemple Storm Starter à l’aide de l’analyse de données sur HDInsight](hdinsight-apache-storm-tutorial-get-started.md)

## Avant de commencer

[AZURE.INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Vous devez disposer de ce qui suit pour suivre jusqu’au bout ce didacticiel Storm Apache :

- **Un abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

- **Des connaissances en SSH et SCP**. Pour plus d’informations sur l’utilisation de SSH et SCP avec HDInsight, consultez les articles suivants :

    - **Clients Linux, Unix ou OS X** : consultez la page [Utilisation de SSH avec Hadoop dans HDInsight sous Linux à partir de Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md)

	- **Clients Windows** : consultez la page [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows](hdinsight-hadoop-linux-use-ssh-windows.md)

## Créer un cluster Storm

Storm sur HDInsight utilise un stockage d’objet blob Azure pour stocker les fichiers journaux et les topologies envoyés au cluster. Utilisez les étapes suivantes pour créer un compte de stockage Azure à utiliser avec votre cluster :

1. Connectez-vous au [portail Azure][preview-portal].

2. Sélectionnez **NOUVEAU**, __Analyse des données__, puis __HDInsight__

	![Création d’un cluster dans le portail Azure](./media/hdinsight-apache-storm-tutorial-get-started-linux/new-cluster.png)

3. Entrez une valeur dans le champ __Nom de cluster__, puis sélectionnez __Storm__ pour le __Type de cluster__. Une coche verte apparaît en regard du __nom de cluster__ s’il est disponible.

	![Nom du cluster, type de cluster et type de système d’exploitation](./media/hdinsight-apache-storm-tutorial-get-started-linux/clustername.png)

	Sélectionnez __Ubuntu__ pour créer un cluster HDInsight Linux.
    
    > [AZURE.NOTE] Laissez le champ __Version__ à sa valeur par défaut pour exécuter les opérations décrites dans ce document.
	
4. Si vous avez plusieurs abonnements, sélectionnez l’entrée __Abonnement__ pour sélectionner l’abonnement Azure qui sera utilisé pour le cluster.

5. Pour __Groupe de ressources__, sélectionnez l’entrée de manière à afficher la liste des groupes de ressources existants, puis sélectionnez celui dans lequel créer le cluster. Vous pouvez également sélectionner __Créer un nouveau__, puis saisir le nom du nouveau groupe de ressources. Une coche verte s’affiche pour indiquer si le nouveau nom de groupe est disponible.

	> [AZURE.NOTE] Cette entrée ira par défaut dans l’un des groupes de ressources existants, si l’un d’eux est disponible.

6. Sélectionnez __Informations d’identification__, puis saisissez une valeur dans le champ __Mot de passe de connexion au cluster__ et dans le champ __Nom d’utilisateur de connexion au cluster__. Vous devez également saisir un __nom d’utilisateur SSH__ et un __MOT DE PASSE__ ou __CLÉ PUBLIQUE__, qui seront utilisés pour authentifier l’utilisateur SSH. Enfin, utilisez le bouton __Sélectionner__ pour définir les informations d’identification.

	![Panneau Informations d’identification du cluster](./media/hdinsight-administer-use-portal-linux/clustercredentials.png)

	Pour plus d'informations sur l'utilisation de SSH avec HDInsight, consultez l'un des articles suivants :

	* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md)

	* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](hdinsight-hadoop-linux-use-ssh-windows.md)

6. Pour __Source de données__, vous pouvez choisir une source de données existante ou en créer une.

	![Panneau Source de données](./media/hdinsight-apache-storm-tutorial-get-started-linux/datasource.png)
	
	Actuellement, vous pouvez sélectionner un compte de stockage Azure comme source de données pour un cluster HDInsight. Utilisez ce qui suit pour comprendre les saisies du panneau __Source de données__.
	
	- __Méthode de sélection__ : définissez cette propriété sur la valeur __De tous les abonnements__ pour permettre l’exploration des comptes de stockage de tous vos abonnements. Affectez-lui la valeur __Clé d’accès__ si vous souhaitez saisir le __nom de stockage__ et la __clé d’accès__ d’un compte de stockage existant.
    
    - __Sélectionnez le compte de stockage__ : si votre abonnement est déjà associé à un compte de stockage, utilisez cette option pour sélectionner le compte à utiliser pour le cluster.
	
	- __Créer un nouveau__ : utilisez cette option pour créer un autre compte de stockage. Utilisez le champ qui s’affiche pour saisir le nom du compte de stockage. Une coche verte s’affiche si le nom est disponible.
	
	- __Choisir le conteneur par défaut__ : utilisez cette option pour saisir le nom du conteneur par défaut à utiliser pour le cluster. Vous pouvez saisir n’importe quel nom, mais nous vous conseillons d’utiliser le même nom que le cluster pour pouvoir facilement reconnaître le conteneur utilisé pour ce cluster spécifique.
	
	- __Emplacement__ : zone géographique dans laquelle le compte de stockage se trouve ou dans laquelle il sera créé.
	
		> [AZURE.IMPORTANT] La sélection de l’emplacement de la source de données par défaut définira également l’emplacement du cluster HDInsight. Le cluster et la source de données par défaut doivent se trouver dans la même région.
    
    - __Identité de cluster AAD__ : permet de sélectionner une identité Azure Active Directory que le cluster utilisera pour accéder au magasin Azure Data Lake Store.
    
        > [AZURE.NOTE] Cette option n’est pas utilisée dans ce document, et vous pouvez laisser la valeur par défaut. Pour plus d’informations sur l’utilisation de cette entrée et du magasin Azure Data Lake Store, avec HDInsight, consultez la section [Créer un cluster HDInsight utilisant Azure Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).
		
	- __Sélectionner__ : utilisez cette option pour enregistrer la configuration de la source de données.
	
7. Sélectionnez __Niveaux de tarification du nœud__ pour afficher des informations sur les nœuds qui seront créés pour ce cluster. Par défaut, le nombre de nœuds de travail est fixé à __4__. Le coût estimé du cluster s’affiche au bas de ce panneau.

	![Panneau Niveaux de tarification du nœud](./media/hdinsight-apache-storm-tutorial-get-started-linux/nodepricingtiers.png)
	
    Vous pouvez sélectionner chaque type de nœud pour modifier le type de machine virtuelle utilisé pour ces nœuds dans votre cluster. Conservez les paramètres par défaut pour exécuter les opérations dans ce document.
    
	Utilisez le bouton __Sélectionner__ pour enregistrer les informations de __Niveaux de tarification de nœud__.

8. Sélectionnez __Configuration facultative__. Ce panneau vous permet d’associer le cluster à un __réseau virtuel__, d’utiliser __Actions de script__ pour personnaliser le cluster, ou un __Metastore personnalisé__ pour conserver les données correspondant à Hive et Oozie.

	![Panneau Configuration facultative](./media/hdinsight-apache-storm-tutorial-get-started-linux/optionalconfiguration.png)
    
    Laissez ces paramètres sur __Non configuré__ pour les étapes décrites dans ce document.

9. Vérifiez que l’option __Épingler au tableau d’accueil__ est sélectionnée, puis sélectionnez __Créer__. Le cluster est créé et la vignette correspondante ajoutée au tableau d’accueil de votre portail Azure. L'icône indique que le cluster est en cours de configuration et sera modifiée pour représenter l'icône HDInsight une fois la configuration terminée.

	| Pendant l’approvisionnement | Approvisionnement terminé |
	| ------------------ | --------------------- |
	| ![Indicateur d’approvisionnement sur le tableau d’accueil](./media/hdinsight-apache-storm-tutorial-get-started-linux/provisioning.png) | ![Vignette de cluster approvisionné](./media/hdinsight-apache-storm-tutorial-get-started-linux/provisioned.png) |

	> [AZURE.NOTE] La création du cluster prend un certain temps (en règle générale, environ 15 minutes). Utilisez la vignette du tableau d’accueil ou l’entrée __Notifications__ à gauche de la page pour suivre la progression du processus d’approvisionnement.

##Exécution d’un exemple Starter Storm sur HDInsight

Les exemples [storm-starter](https://github.com/apache/storm/tree/master/examples/storm-starter) sont inclus dans le cluster HDInsight. Dans les étapes suivantes, vous allez exécuter l’exemple WordCount.

1. Connectez-vous au cluster HDInsight à l’aide de SSH :

		ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
		
	Si vous utilisez un mot de passe pour sécuriser votre compte utilisateur SSH, vous serez invité à le saisir. Si vous utilisez une clé publique, vous devrez peut-être utiliser le paramètre `-i` pour spécifier la clé privée correspondante. Par exemple : `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.
		
	Pour plus d’informations sur l’utilisation de SSH avec HDInsight sous Linux, consultez les articles suivants :
	
	* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md)

	* [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](hdinsight-hadoop-linux-use-ssh-windows)

2. Utilisez la commande suivante pour démarrer un exemple de topologie :

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-0.9.3.2.2.4.9-1.jar storm.starter.WordCountTopology wordcount
		
	> [AZURE.NOTE] La partie `0.9.3.2.2.4.9-1` du nom de fichier peut varier si HDinsight est mis à jour avec des versions plus récentes de Storm.

    Cette opération va démarrer l’exemple de topologie WordCount sur le cluster, avec le nom convivial « wordcount ». Elle va générer de manière aléatoire des phrases et compter les occurrences de chaque mot dans les phrases.

    > [AZURE.NOTE] Pendant l’envoi de la topologie au cluster, vous devez d’abord copier le fichier jar contenant le cluster avant d’utiliser la commande `storm`. Pour ce faire, vous pouvez utiliser la commande `scp` à partir du client où se trouve le fichier. Par exemple, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > L’exemple WordCount et d’autres exemples de Storm Starter sont déjà inclus dans votre cluster sous `/usr/hdp/current/storm-client/contrib/storm-starter/`.

##Analyse de la topologie

L’interface utilisateur Storm fournit une interface web incluse dans votre cluster HDInsight pour utiliser les topologies en cours d’exécution.

Suivez la procédure ci-après pour surveiller la topologie à l’aide de l’interface utilisateur de Storm.

1. Ouvrez un navigateur web et accédez à https://CLUSTERNAME.azurehdinsight.net/stormui, où __CLUSTERNAME__ est le nom de votre cluster. L’interface utilisateur de Storm s’ouvre.

	> [AZURE.NOTE] Si vous êtes invité à fournir un nom d’utilisateur et un mot de passe, entrez l’administrateur de cluster (admin) et le mot de passe que vous avez utilisé pour la création du cluster.

2. Sous **Résumé de la topologie**, sélectionnez l’entrée **Statistiques** située dans la colonne **Nom**. Vous obtiendrez plus d’informations sur la topologie.

	![Tableau de bord Storm avec les informations sur la topologie Statistiques Storm Starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

	Cette page fournit les informations suivantes :

	* **Statistiques de topologie** : informations de base sur les performances de la topologie, organisées dans des fenêtres de temps.

		> [AZURE.NOTE] La sélection d’une fenêtre de temps spécifique modifie la fenêtre de temps pour les informations affichées dans d’autres sections de la page.

	* **Spouts** : informations de base sur les spouts, y compris la dernière erreur retournée par chaque spout.

	* **Bolts** : informations de base sur les bolts.

	* **Configuration de la topologie** : informations détaillées sur la configuration de la topologie.

	Cette page présente également les actions qui peuvent être effectuées sur la topologie :

	* **Activer** : reprend le traitement d’une topologie désactivée.

	* **Désactiver** : suspend une topologie en cours d’exécution.

	* **Rééquilibrer** : ajuste le parallélisme de la topologie. Il convient de rééquilibrer les topologies en cours d’exécution après avoir modifié le nombre de nœuds dans le cluster. Cela permet à la topologie d’ajuster le parallélisme pour compenser l’augmentation/la réduction du nombre de nœuds du cluster. Pour plus d’informations, consultez la rubrique [Présentation du parallélisme d’une topologie Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

	* **Supprimer** : met fin à une topologie Storm après expiration du délai spécifié.

3. À partir de cette page, sélectionnez une entrée dans la section **Spouts** ou **Bolts**. Vous obtiendrez des informations relatives au composant sélectionné.

	![Tableau de bord Storm avec des informations sur les composants sélectionnés.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

	Cette page affiche les informations suivantes :

	* **Statistiques du spout/bolt** : informations de base sur les performances de la topologie, organisées dans des fenêtres de temps.

		> [AZURE.NOTE] La sélection d’une fenêtre de temps spécifique modifie la fenêtre de temps pour les informations affichées dans d’autres sections de la page.

	* **Statistiques d’entrée** (bolt uniquement) : informations sur les composants qui produisent des données consommées par le bolt.

	* **Statistiques de sortie** : informations sur les données émises par ce bolt.

	* **Exécuteurs** : informations sur les instances de ce composant.

	* **Erreurs** : erreurs générées par ce composant.

4. Lorsque vous affichez les détails d’un spout ou d’un bolt, sélectionnez une entrée depuis la colonne **Port** située dans la section **Exécuteurs** pour afficher les détails d’une instance spécifique du composant.

		2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
		2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
		2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
		2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
		2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
		2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
		2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
		2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

	À partir de ces données, vous pouvez voir qu’il y a 1 493 957 occurrences du mot **seven**. C’est le nombre de fois où il a été détecté depuis le démarrage de cette topologie.

##Arrêt de la topologie

Retournez à la page **Résumé de la topologie**, puis sélectionnez le bouton **Supprimer** de la section**Actions de topologie**. Lorsque vous êtes invité à entrer le nombre de secondes à attendre avant l’arrêt de la topologie, entrez le nombre 10. Après le délai d’expiration, la topologie n’apparaîtra plus lorsque vous vous rendrez dans la section **Interface utilisateur Storm** du tableau de bord.

##Suppression du cluster

[AZURE.INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

##Résumé

Dans ce didacticiel sur Storm Apache, vous avez appris à créer un cluster Storm sur HDInsight à l’aide de Storm Starter et à déployer, surveiller et gérer des topologies Storm à l’aide du tableau de bord Storm.

##<a id="next"></a>Étapes suivantes

* Le document suivant contient une liste d’autres exemples pouvant être utilisés avec Storm sur HDInsight :

	* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[azureportal]: https://manage.windowsazure.com/
[hdinsight-provision]: hdinsight-provision-clusters.md
[preview-portal]: https://portal.azure.com/

<!---HONumber=AcomDC_0309_2016-->