<properties
	pageTitle="Prise en main d’Event Hubs dans Java avec Apache Storm | Microsoft Azure"
	description="Suivez ce didacticiel pour commencer à utiliser Azure Event Hubs, à envoyer des événements en Java et à en recevoir dans un cluster Apache Storm."
	services="event-hubs"
	documentationCenter=""
	authors="fsautomata"
	manager="timlt"
	editor=""/>

<tags
	ms.service="event-hubs"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="11/05/2015"
	ms.author="sethm"/>

# Prise en main des concentrateurs d’événements

[AZURE.INCLUDE [service-bus-selector-get-started](../../includes/service-bus-selector-get-started.md)]

## Introduction

Les concentrateurs d’événements représentent un système d’ingestion à l’extensibilité élevée en mesure d’absorber des millions d’événements par seconde, ce qui permet à une application de traiter et d’analyser les quantités énormes de données produites par vos périphériques connectés et vos applications. Une fois collectés dans des concentrateurs d’événements, vous pouvez transformer et stocker des données à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.

Pour plus d'informations, consultez la [Vue d'ensemble d’Event Hubs][].

Ce didacticiel explique comment collecter des messages dans un hub d’événements à l’aide d’une application console en Java et les récupérer en parallèle à l’aide d’Apache Storm.

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

+ Un environnement de développement Java configuré pour exécuter [Maven](http://maven.apache.org/). Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).

+ Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Ffr-FR%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d’évaluation gratuite d’Azure</a>.

## Création d’un concentrateur d’événements

1. Connectez-vous au [portail Azure Classic][] et cliquez sur **NOUVEAU** en bas de l’écran.

2. Cliquez sur **Services d’application**, sur **Service Bus**, sur **Concentrateur d’événements**, puis sur **Création rapide**.

   	![][1]

3. Attribuez un nom à votre concentrateur d’événements, sélectionnez la région souhaitée, puis cliquez sur **Créer un concentrateur d’événements**.

   	![][2]

4. Cliquez sur l’espace de noms que vous venez de créer (en règle générale ***nom du hub d’événements*-ns**).

   	![][3]

5. Cliquez sur l’onglet **Hubs d’événements** en haut de la page, puis cliquez sur le concentrateur d’événements que vous venez de créer.

   	![][4]

6. Cliquez sur l’onglet **Configurer** en haut de la page, ajoutez une règle nommée **SendRule** avec les droits *Envoyer*, puis ajoutez une autre règle nommée **ReceiveRule** avec les droits *Écouter*, puis cliquez sur **Enregistrer**.

   	![][5]

7. Sur la même page, notez les clés générées pour **SendRule** et **ReceiveRule**.

   	![][6c]

Votre concentrateur d’événements est désormais créé et vous disposez des chaînes de connexion dont vous avez besoin pour envoyer et recevoir des événements.

[AZURE.INCLUDE [service-bus-event-hubs-get-started-send-java](../../includes/service-bus-event-hubs-get-started-send-java.md)]


[AZURE.INCLUDE [service-bus-event-hubs-get-started-receive-storm](../../includes/service-bus-event-hubs-get-started-receive-storm.md)]

## Exécution des applications

Vous êtes maintenant prêt à exécuter les applications.

1.	Exécutez la classe **LogTopology** dans Eclipse, puis attendez qu’elle démarre les récepteurs pour toutes les partitions.

2.	Exécutez le projet **Expéditeur,** appuyez sur **Entrée** dans la fenêtre de console. Les événements s’affichent dans la fenêtre du destinataire.

   	![][22]

> [AZURE.NOTE]Dans le cadre de ce didacticiel, utilisez exclusivement Storm en mode local destiné au développement. Reportez-vous à la [Vue d’ensemble HDInsight Storm][] et à la documentation [Apache Storm][] officielle pour plus d’informations sur les déploiements et les modèles Storm.

## Étapes suivantes

Les ressources suivantes sont disponibles pour les applications de développement intégrant des concentrateurs d’événements et Storm.

- Le didacticiel [Analyse des données de capteur avec Storm et HDInsight] est un didacticiel présentant un scénario complet qui tire parti des concentrateurs d’événements, de Storm et de HBase pour la réception des données de capteur dans un cluster Hadoop.
- Le didacticiel [Développement d’applications de traitement de données de diffusion avec SCP.NET et C# sur Storm et HDInsight][] décrit la marche à suivre pour écrire des pipelines Storm en C#.

<!-- Images. -->
[1]: ./media/event-hubs-java-storm-getstarted/create-event-hub1.png
[2]: ./media/event-hubs-java-storm-getstarted/create-event-hub2.png
[3]: ./media/event-hubs-java-storm-getstarted/create-event-hub3.png
[4]: ./media/event-hubs-java-storm-getstarted/create-event-hub4.png
[5]: ./media/event-hubs-java-storm-getstarted/create-event-hub5.png
[6]: ./media/event-hubs-getstarted/create-event-hub6.png
[6c]: ./media/event-hubs-java-storm-getstarted/create-event-hub6c.png

[22]: ./media/event-hubs-java-storm-getstarted/receive-storm2.png

<!-- Links -->
[portail Azure Classic]: https://manage.windowsazure.com/
[Event Processor Host]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Vue d'ensemble d’Event Hubs]: event-hubs-overview.md

[Apache Storm]: https://storm.incubator.apache.org
[Vue d’ensemble HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[Analyse des données de capteur avec Storm et HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md
[Développement d’applications de traitement de données de diffusion avec SCP.NET et C# sur Storm et HDInsight]: ../hdinsight/hdinsight-storm-develop-csharp-visual-studio-topology.md
 

<!---HONumber=AcomDC_1203_2015-->