<properties 
	pageTitle="Surveillance et gestion des pipelines d’Azure Data Factory" 
	description="Découvrez comment utiliser la nouvelle application de surveillance et gestion pour surveiller et gérer les fabriques de données et les pipelines Azure." 
	services="data-factory" 
	documentationCenter="" 
	authors="spelluru" 
	manager="jhubbard" 
	editor="monicar"/>

<tags 
	ms.service="data-factory" 
	ms.workload="data-services" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="02/12/2016" 
	ms.author="spelluru"/>

# Surveiller et gérer les pipelines Azure Data Factory à l’aide de la nouvelle application de surveillance et gestion.
> [AZURE.SELECTOR]
- [Using Azure Portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
- [Using Monitoring and Management App](data-factory-monitor-manage-app.md)

Cet article décrit comment surveiller, gérer et déboguer vos pipelines à l’aide de l’**application de surveillance et gestion**. Il explique également comment créer des alertes et recevoir des notifications d’échec en utilisant l’application.
      
## Lancer l’application de surveillance et gestion 
Pour lancer l’application de surveillance et gestion, cliquez sur la mosaïque **Application de surveillance** sur le panneau **DATA FACTORY** de votre fabrique de données.

![Mosaïque Surveillance sur la page d’accueil de Data Factory](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

L’application de surveillance et gestion devrait s’ouvrir dans un nouvel onglet ou une nouvelle fenêtre.

![Application de surveillance et gestion](./media/data-factory-monitor-manage-app/AppLaunched.png)

## Présentation de l’application de surveillance et gestion
Il existe trois onglets (**Explorateur de ressources**, **Vues de surveillance** et **Alertes**) sur la gauche. C’est le premier onglet (Explorateur de ressources) qui est sélectionné par défaut.

### Explorateur de ressources
Vous voyez l’**arborescence** de l’Explorateur de ressources dans le volet gauche, la **Vue schématique** en haut et la liste **Fenêtres d’activité** en bas du volet central, et les onglets **Propriétés**/**Explorateur de fenêtres d’activité** dans le volet droit.

Vous pouvez voir toutes les ressources (pipelines, groupes de données, services liés) organisées en arborescence dans la fabrique de données. Lorsque vous sélectionnez un objet dans l’Explorateur de ressources, vous remarquez les points suivants :

- L’entité Data Factory associée est mise en surbrillance dans la vue schématique.
- Les fenêtres d’activité associées (cliquez [ici](data-factory-scheduling-and-execution.md) pour en savoir plus sur les fenêtres d’activité) sont mises en surbrillance dans la liste des fenêtres d’activité en bas de la page.  
- Les propriétés de l’objet sélectionné s’affichent dans la fenêtre Propriétés dans le volet droit. 

![Explorateur de ressources](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Consultez l’article [Planification et exécution](data-factory-scheduling-and-execution.md) pour des informations conceptuelles détaillées sur les fenêtres d’activité.

### Vue de diagramme
La vue schématique d'une fabrique de données est un point unique de surveillance et de gestion de la fabrique de données et de ses ressources. Lorsque vous sélectionnez une entité Data Factory (jeu de données/pipeline) dans la vue schématique, vous remarquez les points suivants :
 
- L’entité Data Factory est sélectionnée dans l’arborescence.
- Les fenêtres d’activité associées sont mises en surbrillance dans la liste des fenêtres d’activité.
- Les propriétés de l’objet sélectionné s’affichent dans la fenêtre Propriétés.

Lorsque le pipeline est activé (c’est-à-dire lorsqu’il n’est pas en pause), la barre de sa mosaïque est verte, comme indiqué ci-dessous.

![Pipeline en cours d’exécution](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Remarquez qu’il existe trois boutons de commande pour le pipeline dans la vue schématique. Vous pouvez utiliser le deuxième bouton pour mettre en pause le pipeline. Cette action n’interrompt pas les activités en cours et les laisse se terminer. Le troisième bouton permet de mettre en pause le pipeline et d’interrompre ses activités en cours. Le premier bouton permet de relancer le pipeline, qui n’est ainsi plus en pause. Lorsque votre pipeline est en pause, vous remarquez que sa mosaïque change de couleur comme suit.

![Mettre en pause/relancer depuis la mosaïque](./media/data-factory-monitor-manage-app/SuspendResumeOnTile.png)

Vous pouvez sélectionner deux ou plusieurs pipelines (en appuyant sur la touche CTRL) et utiliser les boutons de la barre de commandes pour mettre en pause/relancer plusieurs pipelines à la fois.

![Mettre en pause/relancer depuis la barre de commandes](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

Pour voir toutes les activités dans le pipeline, cliquez sur sa mosaïque avec le bouton droit, puis cliquez sur **Ouvrir un pipeline**.

![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

Dans la vue du pipeline ouvert, vous voyez toutes les activités dans le pipeline. Dans cet exemple, le pipeline ne contient qu’une seule activité : une activité de copie. Pour revenir à la vue précédente, cliquez sur le nom de la fabrique de données dans le menu de navigation en haut de la page.

![Pipeline ouvert](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

Dans la vue du pipeline ouvert/fermé, lorsque vous cliquez sur un jeu de données de sortie ou que vous le survolez avec la souris, la fenêtre d’activité correspondante s’affiche.

![Fenêtre contextuelle des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Vous pouvez cliquer sur une fenêtre d’activité pour afficher ses détails dans la fenêtre **Propriété** dans le volet droit.

![Propriétés des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Dans le volet droit, basculez sur l’onglet **Explorateur de fenêtres d’activité** pour afficher plus de détails.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Les fenêtres d’activité s’affichent à trois emplacements différents :

- la fenêtre contextuelle des fenêtres d’activité dans la vue schématique (volet central) ;
- l’Explorateur de fenêtres d’activité dans le volet droit ;
- la liste des fenêtres d’activité dans le volet inférieur.

Dans la fenêtre contextuelle et l’Explorateur de fenêtres d’activité, vous pouvez passer à la semaine précédente ou suivante à l’aide des flèches gauche et droite.

![Flèches gauche/droite de l’Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

En bas de la vue schématique, vous voyez des boutons permettant d’effectuer un zoom avant, un zoom arrière, un zoom pour ajuster l’image à la taille de l’écran, un zoom à 100 % ou de verrouiller la disposition (ce qui vous évite de déplacer accidentellement des tables et des pipelines dans la vue schématique). L’option Verrouillez la disposition est activée par défaut. Vous pouvez la désactiver et déplacer des entités dans la vue schématique. Lorsque vous la désactivez, vous pouvez utiliser le dernier bouton pour positionner automatiquement les tables et les pipelines. Vous pouvez également effectuer un zoom avant ou arrière à l’aide de la roulette de la souris.

![Commandes de zoom de la vue schématique](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)


### Liste des fenêtres d’activité
La liste des fenêtres d’activité dans la partie inférieure du volet central affiche toutes les fenêtres d’activité du jeu de données que vous avez sélectionné dans l’Explorateur de ressources ou la vue schématique. Par défaut, la liste est en ordre décroissant, ce qui signifie que la fenêtre d’activité la plus récente s’affiche en premier.

![Liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Cette liste ne s’actualise pas automatiquement. Pour l’actualiser manuellement, utilisez le bouton d’actualisation de la barre d’outils.


Les fenêtres d’activité peuvent avoir l’un des statuts suivants :

<table>
<tr>
	<th align="left">Statut</th><th align="left">État secondaire</th><th align="left">Description</th>
</tr>
<tr>
	<td rowspan="8">En attente</td><td>ScheduleTime</td><td>L’heure d’exécution de la fenêtre d’activité n’est pas encore venue.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Les dépendances en amont ne sont pas prêtes.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Les ressources de calcul ne sont pas disponibles.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Toutes les instances d’activité sont occupées par l’exécution d’autres fenêtres d’activité.</td>
</tr>
<tr>
<td>ActivityResume</td><td>L’activité est mise en pause et ne peut pas exécuter les fenêtres d’activité jusqu’à sa reprise.</td>
</tr>
<tr>
<td>Retry</td><td>L’exécution de l’activité sera retentée.</td>
</tr>
<tr>
<td>Validation</td><td>La validation n’a pas encore démarré.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Attente d’une nouvelle tentative de validation.</td>
</tr>
<tr>
&lt;tr
<td rowspan="2">InProgress</td><td>Validation</td><td>Validation en cours.</td>
</tr>
<td></td>
<td>La fenêtre d’activité est en cours de traitement.</td>
</tr>
<tr>
<td rowspan="4">Échec</td><td>TimedOut</td><td>L'exécution a pris plus de temps que l’activité ne l’autorise.</td>
</tr>
<tr>
<td>Canceled</td><td>Annulé par l’action de l’utilisateur.</td>
</tr>
<tr>
<td>Validation</td><td>La validation a échoué.</td>
</tr>
<tr>
<td></td><td>Impossible de générer ou de valider la fenêtre d’activité.</td>
</tr>
<td>Ready</td><td></td><td>La fenêtre d’activité est prête à être consommée.</td>
</tr>
<tr>
<td>Ignoré</td><td></td><td>La fenêtre d’activité n’est pas traitée.</td>
</tr>
<tr>
<td>Aucun</td><td></td><td>Fenêtre d’activité qui a été réinitialisée alors qu’elle existait avec un statut différent.</td>
</tr>
</table>


Lorsque vous cliquez sur une fenêtre d’activité dans la liste, les détails la concernant s’affichent dans l’Explorateur de fenêtres d’activité ou la fenêtre Propriétés sur la droite.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### Actualiser les fenêtres d’activité  
Les détails ne sont pas automatiquement actualisés. Pour actualiser manuellement la liste des fenêtres d’activité, utilisez le bouton **Actualiser** (le deuxième) dans la barre de commandes.
 

### Fenêtre Propriétés
La fenêtre Propriétés se trouve dans le volet situé tout à droite de l’application de surveillance et gestion.

![Fenêtre Propriétés](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Elle affiche les propriétés de l’élément que vous avez sélectionné dans l’Explorateur de ressources (arborescence), la vue schématique ou la liste des fenêtres d’activité.

### Explorateur de fenêtres d’activité

L’Explorateur de fenêtres d’activité se trouve dans le volet situé tout à droite de l’application de surveillance et gestion. Il affiche des détails sur la fenêtre d’activité que vous avez sélectionnée dans la fenêtre contextuelle ou la liste des fenêtres d’activité.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Vous pouvez passer à une fenêtre d’activité différente en cliquant dessus dans la vue calendaire en haut de l’écran. Vous pouvez également utiliser les boutons **flèche gauche**/**flèche droite** en haut de l’écran pour afficher les fenêtres d’activité de la semaine précédente ou suivante.

Vous pouvez utiliser les boutons de la barre d’outils dans le volet inférieur pour **réexécuter** la fenêtre d’activité ou **actualiser** les détails affichés dans le volet.


## Utiliser les vues système
L’application de surveillance et gestion inclut des vues système intégrées (**Fenêtres d’activité récentes**, **Fenêtres d’activité ayant échoué**, **Fenêtres d’activité en cours**), qui vous permettent d’afficher les fenêtres d’activité récentes, ayant échoué et en cours de votre fabrique de données.

Basculez vers l’onglet **Vues de surveillance** sur la gauche en cliquant dessus.

![Onglet Vues de surveillance](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Pour l’instant, l’application prend en charge trois vues système. Sélectionnez une option pour afficher les fenêtres d’activité récentes, ayant échoué, ou en cours dans la liste des fenêtres d’activité (en bas du volet central).

Lorsque vous sélectionnez l’option **Fenêtres d’activité récentes**, toutes les fenêtres d’activité récentes s’affichent dans l’ordre décroissant en fonction de l’**heure de la dernière tentative**.

Vous pouvez utiliser la vue **Fenêtres d’activité ayant échoué** pour afficher toutes les fenêtres d’activité de la liste qui ont échoué. Dans la liste, sélectionnez une fenêtre d’activité ayant échoué pour afficher les détails la concernant dans la fenêtre **Propriétés** ou dans l’**Explorateur de fenêtres d’activité**. Vous pouvez également télécharger tous les journaux d’une fenêtre d’activité ayant échoué.


## Trier et filtrer les fenêtres d’activité
Pour filtrer les fenêtres d’activité, modifiez les paramètres d’**heure de début** et d’**heure de fin** dans la barre de commandes. Après avoir modifié les heures de début et de fin, cliquez sur le bouton en regard de l’heure de fin pour actualiser la liste des fenêtres d’activité.

![Heures de début et de fin](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [AZURE.NOTE] Pour l’instant, toutes les heures de l’application de surveillance et gestion sont au format UTC.

Dans la **liste des fenêtres d’activité**, cliquez sur le nom d’une colonne (par exemple : Statut).

![Menu déroulant de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Vous pouvez effectuer les opérations suivantes :

- Trier dans l’ordre croissant.
- Trier dans l’ordre décroissant.
- Filtrer selon une ou plusieurs valeurs (Prêt, En attente, etc.).

Lorsque vous spécifiez un filtre sur une colonne, vous voyez que le bouton de filtrage est activé pour cette colonne afin d’indiquer que les valeurs filtrées sont celles de cette colonne.

![Filtre de colonne de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Vous pouvez utiliser la même fenêtre contextuelle pour effacer les filtres. Pour effacer tous les filtres de la liste des fenêtres d’activité, cliquez sur le bouton Effacer le filtre dans la barre de commandes.

![Effacer tous les filtres de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)


## Exécuter des actions batch

### Réexécuter les fenêtres d’activité sélectionnées
Sélectionnez une fenêtre d’activité, cliquez sur la flèche vers le bas du premier bouton de la barre de commandes et sélectionnez **Réexécuter** ou **Réexécuter avec les fenêtres en amont dans le pipeline**. L’option **Réexécuter avec les fenêtres en amont dans le pipeline** permet de réexécuter également toutes les fenêtres d’activité en amont. ![Réexécuter une fenêtre d’activité](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Vous pouvez également sélectionner plusieurs fenêtres d’activité dans la liste et les réexécuter simultanément. Vous pouvez filtrer les fenêtres d’activité en fonction de leur statut (par exemple : **Ayant échoué**), puis réexécuter celles qui ont échoué après avoir corrigé le problème à l’origine de cet échec. Pour en savoir plus sur le filtrage des fenêtres d’activité dans la liste, consultez la section suivante.

### Mettre en pause/relancer plusieurs pipelines
Vous pouvez sélectionner deux ou plusieurs pipelines (en appuyant sur la touche CTRL) et utiliser les boutons de la barre de commandes (entourés d’un rectangle rouge sur l’image suivante) pour les mettre en pause/relancer simultanément.

![Suspendre/relancer depuis la barre de commandes](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## Créer des alertes 
La page Alertes vous permet de créer une nouvelle alerte et d’afficher, de modifier ou de supprimer des alertes existantes. Vous pouvez également désactiver ou activer une alerte. Cliquez sur l’onglet Alertes pour afficher la page.

![Onglet Alertes](./media/data-factory-monitor-manage-app/AlertsTab.png)

### Pour créer une alerte

1. Pour ajouter une alerte, cliquez sur **Ajouter une alerte**. La page Détails s’affiche. 

	![Créer des alertes - page Détails](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
1. Spécifiez le **nom** et la **description** de l’alerte, puis cliquez sur **Suivant**. La page **Filtres** doit s’afficher.

	![Créer des alertes - page Filtres](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)

	Vous pouvez également **regrouper** les événements d’alertes comme indiqué ci-dessous :

	![Regrouper des alertes](./media/data-factory-monitor-manage-app/AggregateAlerts.png)
2. Sélectionnez l’**événement**, le **statut** et l’**état secondaire** (facultatif) sur lequel vous souhaitez que le service Data Factory vous informe et cliquez sur **Suivant**. La page **Destinataires** doit s’afficher.

	![Créer des alertes - page Destinataires](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png) 
3. Sélectionnez l’option **Administrateurs d’abonnement par courrier électronique** et/ou entrez une **adresse de messagerie électronique d’administrateur supplémentaire**, puis cliquez sur **Terminer**. L’alerte doit apparaître dans la liste. 
	
	![Liste des alertes](./media/data-factory-monitor-manage-app/AlertsList.png)

Dans la liste des alertes, utilisez les boutons associés à l’alerte pour modifier, supprimer, désactiver ou activer une alerte.

### Événement/statut/état secondaire
Le tableau suivant dresse la liste des événements et des statuts (et états secondaires) disponibles.

Nom de l'événement | Statut | État secondaire
-------------- | ------ | ----------
Exécution de l’activité démarrée | Démarré | Démarrage en cours
Exécution de l’activité terminée | Succeeded | Succeeded 
Exécution de l’activité terminée | Échec| Échec de l’allocation des ressources<p>Échec de l’exécution</p><p>Expiré</p><p>Échec de la validation</p><p>Abandonné</p>
Création d’un cluster HDI à la demande démarrée | Démarré | &nbsp; |
Cluster HDI à la demande créé correctement | Succeeded | &nbsp; |
Cluster HDI à la demande supprimé | Succeeded | &nbsp; |
### Pour modifier, supprimer ou désactiver une alerte


![Boutons d’alertes](./media/data-factory-monitor-manage-app/AlertButtons.png)



    
 

<!---HONumber=AcomDC_0218_2016-->