<properties 
   pageTitle="Création de graphiques dans Azure Automation"
   description="La création de graphiques vous permet de créer des Runbooks pour Azure Automation sans utiliser de code. Cet article propose une introduction à la création de graphiques et tous les détails nécessaires pour commencer à créer Runbook graphique."
   services="automation"   
   documentationCenter=""
   authors="mgoedtel"
   manager="stevenka"
   editor="tysonn" />
<tags 
   ms.service="automation"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="02/23/2016"
   ms.author="magoedte;bwren" />

# Création de graphiques dans Azure Automation

## Introduction

La création de graphiques vous permet de créer des Runbooks pour Azure Automation sans les complexités du code de workflow Windows PowerShell sous-jacent. Vous pouvez ajouter des activités d'une bibliothèque d'applets de commande et d'autres activités à un canevas, et les lier pour former un workflow.

Cet article propose une introduction à la création de graphiques et aux concepts dont vous avez besoin pour prendre en main la création d'un Runbook graphique.

## Runbooks graphiques

Dans Azure Automation, tous les Runbooks sont des workflows Windows PowerShell. Les Runbooks graphiques génèrent du code PowerShell qui est exécuté par les Workers Automation, mais vous ne pouvez pas l'afficher ou le modifier directement. Les Runbooks graphiques ne peuvent pas être convertis en Runbooks textuels. Par ailleurs, un Runbook textuel existant ne peut pas être importé dans l'éditeur graphique.


## Vue d'ensemble de l'éditeur graphique

Vous pouvez ouvrir l’éditeur graphique dans le portail Azure en créant ou en modifiant un Runbook graphique.

![Espace de travail graphique](media/automation-graphical-authoring-intro/graphical-editor.png)


Les sections suivantes décrivent les contrôles de l'éditeur graphique.


### Canevas
Le canevas est l'emplacement où vous concevez votre Runbook. Vous pouvez ajouter au Runbook des activités des nœuds se trouvant dans le contrôle Bibliothèque et les connecter à l'aide de liens pour définir la logique du Runbook.

Vous pouvez utiliser les commandes en bas de la zone de dessin pour effectuer un zoom avant ou arrière.

![Espace de travail graphique](media/automation-graphical-authoring-intro/canvas-zoom.png)

### Contrôle Bibliothèque

Le contrôle Bibliothèque est l'emplacement où vous sélectionnez les [activités](#activities) à ajouter à votre Runbook. Vous les ajoutez au canevas où vous les connectez à d'autres activités. Il comprend quatre sections décrites dans le tableau suivant.

| Section | Description |
|:---|:---|
| Applets de commande | Inclut toutes les applets de commande qui peuvent être utilisées dans votre Runbook. Les applets de commande sont organisées par module. Tous les modules que vous avez installés dans votre compte Automation seront disponibles. |
| Runbooks | Inclut les Runbooks de votre compte Automation, organisés par balise. Étant donné qu'un Runbook peut avoir plusieurs balises, il peut être répertorié sous plusieurs balises. Ces Runbooks peuvent être ajoutés au canevas afin d'être utilisés comme Runbook enfant. Le Runbook en cours de modification est affiché, mais il ne peut pas être ajouté au canevas, car un Runbook ne peut pas s'appeler lui-même.
| Éléments multimédias | Inclut les [ressources Automation](http://msdn.microsoft.com/library/dn939988.aspx) de votre compte Automation qui peuvent être utilisées dans votre Runbook. Lorsque vous ajoutez une ressource à un Runbook, cela ajoute une activité de workflow qui obtient la ressource sélectionnée. Pour les ressources de type Variable, vous pouvez choisir d'ajouter une activité pour obtenir la variable ou de définir la variable.
| Contrôle de Runbook | Inclut des activités de contrôle de Runbook qui peuvent être utilisées dans votre Runbook actuel. Une *jonction* prend plusieurs entrées et attend que tout soit terminé pour poursuivre le workflow. Un *script de workflow* exécute une ou plusieurs lignes de code de workflow PowerShell. Vous pouvez utiliser cette activité pour du code personnalisé ou pour une fonctionnalité que vous ne pouvez pas obtenir avec d'autres activités.|

### Contrôle Configuration

Le contrôle Configuration est l'emplacement où vous fournissez des détails concernant un objet sélectionné sur le canevas. Les propriétés disponibles dans ce contrôle dépendent du type d'objet sélectionné. Lorsque vous sélectionnez une option dans le contrôle Configuration, des panneaux supplémentaires s'ouvrent afin de fournir des informations supplémentaires.

### Contrôle Test

Le contrôle Test n'est pas affiché lors du premier démarrage de l'éditeur graphique. Il s'ouvre lorsque vous [testez un Runbook graphique](#graphical-runbook-procedures) de manière interactive.

## Procédures relatives aux Runbooks graphiques 

### Exportation et importation d'un Runbook graphique

Vous pouvez exporter uniquement la version publiée d'un Runbook graphique. Si le Runbook n'a pas encore été publié, le bouton **Exportation publiée** est désactivé. Lorsque vous cliquez sur le bouton **Exportation publiée**, le Runbook est téléchargé sur votre ordinateur local. Le nom du fichier correspond au nom du Runbook avec une extension *graphrunbook*.

![Exportation publiée](media/automation-graphical-authoring-intro/runbook-export.png)

Vous pouvez importer un fichier de Runbook graphique en sélectionnant l’option **Importer** lors de l'ajout d'un Runbook. Lorsque vous sélectionnez le fichier à importer, vous pouvez conserver le même **nom** ou en fournir un nouveau.

![Importer un Runbook](media/automation-graphical-authoring-intro/runbook-import.png)


### Test d'un Runbook graphique

Vous pouvez tester le brouillon d’un Runbook dans le portail Azure tout en laissant la version publiée du Runbook inchangée, ou vous pouvez tester un Runbook avant sa publication. Cela vous permet de vérifier que le Runbook fonctionne correctement avant de remplacer la version publiée. Lorsque vous testez un Runbook, le Runbook brouillon est exécuté et toutes les actions qu'il effectue sont finalisées. Aucun historique des tâches n'est créé, mais la sortie est affichée dans le volet de sortie du test.

Ouvrez le contrôle Test pour un Runbook en ouvrant le Runbook en vue de sa modification, puis cliquez sur le bouton **Volet de test**.

![Bouton Volet de test](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

Le contrôle Test demande tous les paramètres d'entrée, et vous pouvez démarrer le Runbook en cliquant sur le bouton **Démarrer**.

![Boutons de contrôle Test](media/automation-graphical-authoring-intro/runbook-test-start.png)

### Publication d'un Runbook graphique

Dans Azure Automation, chaque Runbook a un brouillon et une version publiée. Seule la version publiée est disponible à l'exécution, et seul le brouillon peut être modifié. La version publiée n'est pas affectée par les modifications apportées à la version Bouillon. Lorsque le brouillon est prêt à être rendu disponible, vous le publiez, ce qui remplace la version publiée par le brouillon.

Vous pouvez publier un Runbook graphique en ouvrant le Runbook en vue de sa modification, puis en cliquant sur le bouton **Publier**.

![Bouton Publier](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Lorsqu'un Runbook n'a pas encore été publié, il a le statut **Nouveau**. Une fois publié, il a le statut **Publié**. Si vous modifiez le Runbook après qu'il a été publié, et que la version publiée et le brouillon sont différents, le Runbook a le statut **En mode Édition**.

![États du Runbook](media/automation-graphical-authoring-intro/runbook-statuses.png)

Vous avez également la possibilité de revenir à la version publiée d'un Runbook. Cela supprime toutes les modifications apportées depuis la dernière publication du Runbook et remplace le brouillon du Runbook par la version publiée.

![Bouton Revenir à la version publiée](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)


## Activités

Les activités sont les éléments essentiels d'un Runbook. Une activité peut être une applet de commande PowerShell, un Runbook enfant ou une activité de workflow. Vous ajoutez une activité au Runbook en cliquant avec le bouton droit dans le contrôle Bibliothèque, puis en sélectionnant **Ajouter au canevas**. Vous pouvez ensuite cliquer sur l'activité et la faire glisser pour la placer à l'emplacement de votre choix sur le canevas. L'emplacement de l'activité sur le canevas n'affecte en aucune façon le fonctionnement du Runbook. Vous pouvez disposer votre Runbook de la façon qui vous convient le mieux pour visualiser son fonctionnement.

![Ajouter au canevas](media/automation-graphical-authoring-intro/add-to-canvas.png)

Sélectionnez l'activité sur le canevas pour configurer ses propriétés et ses paramètres dans le panneau Configuration. Vous pouvez remplacer l'**étiquette** de l'activité par une chaîne descriptive. L'applet de commande d'origine est toujours en cours d'exécution. Vous modifiez simplement son nom d'affichage qui sera utilisé dans l'éditeur graphique. L'étiquette doit être unique dans le Runbook.

### Jeux de paramètres

Un jeu de paramètres définit les paramètres obligatoires et facultatifs qui acceptent des valeurs pour une applet de commande particulière. Toutes les applets de commande ont au moins un jeu de paramètres ; certaines en ont plusieurs. Si une applet de commande a plusieurs jeux de paramètres, vous devez sélectionner celui que vous allez utiliser avant de pouvoir configurer les paramètres. Les paramètres que vous pouvez configurer dépendent de l'ensemble de paramètres que vous choisissez. Vous pouvez changer le jeu de paramètres utilisé par une activité en sélectionnant **Jeu de paramètres**, puis en sélectionnant un autre jeu. Dans ce cas, toutes les valeurs de paramètres que vous avez configurées sont perdues.

Dans l'exemple suivant, l'applet de commande Get-AzureVM a deux jeux de paramètres. Vous ne pouvez pas configurer les valeurs de paramètres tant que vous n'avez pas sélectionné l'un des jeux de paramètres. Le jeu de paramètres ListAllVMs, qui a un seul paramètre facultatif, sert à retourner toutes les machines virtuelles. La valeur GetVMByServiceandVMName, qui a un paramètre obligatoire et deux paramètres facultatifs, sert à spécifier la machine virtuelle à retourner.

![Jeu de paramètres](media/automation-graphical-authoring-intro/parameter-set.png)

#### Valeurs de paramètres

Lorsque vous spécifiez une valeur pour un paramètre, vous sélectionnez une source de données pour déterminer la façon dont la valeur sera spécifiée. Les sources de données disponibles pour un paramètre particulier dépendent des valeurs valides pour ce paramètre. Par exemple, Null ne sera pas une option disponible pour un paramètre qui n'autorise pas les valeurs null.

| Source de données | Description |
|:---|:---|
|Valeur constante|Entrez une valeur pour le paramètre. Cette option est disponible uniquement pour les types de données suivants : Int32, Int64, String, Boolean, DateTime, Switch. |
|Sortie d'activité|Sortie d'une activité qui précède l'activité actuelle dans le workflow. Toutes les activités valides sont répertoriées. Sélectionnez simplement l'activité pour utiliser sa sortie comme valeur de paramètre. Si l'activité génère un objet ayant plusieurs propriétés, vous pouvez taper le nom de la propriété après avoir sélectionné l'activité.|
|Paramètre d'entrée de Runbook|Sélectionnez un paramètre d'entrée de Runbook en tant qu'entrée pour le paramètre de l'activité.|  
|Ressource variable Automation|Sélectionnez une variable Automation comme entrée.|  
|Ressource d'identification Automation|Sélectionnez les informations d'identification Automation comme entrée.|  
|Ressource de certificat Automation|Sélectionnez un certificat Automation comme entrée.|  
|Ressource de connexion Automation|Sélectionnez une connexion Automation comme entrée.| 
|Expression PowerShell|Spécifiez une [expression PowerShell](#powershell-expressions) simple. L'expression sera évaluée avant l'activité, et le résultat utilisé pour la valeur du paramètre. Vous pouvez utiliser des variables pour faire référence à la sortie d'une activité ou à un paramètre d'entrée de Runbook.|
|Chaîne vide|Une valeur de chaîne vide.|
|Null|Une valeur Null.|
|Désélectionner|Efface toute valeur qui a été précédemment configurée.|


#### Autres paramètres facultatifs

Toutes les applets de commande peuvent fournir des paramètres supplémentaires. Il s'agit de paramètres communs PowerShell ou d'autres paramètres personnalisés. Une zone de texte dans laquelle vous pouvez fournir des paramètres en utilisant la syntaxe PowerShell s'affiche. Par exemple, pour utiliser le paramètre commun **Verbose**, vous devez spécifier « **-Verbose:$True** ».

### Nouvelles tentatives d’activité

La fonction **Comportement des nouvelles tentatives** permet à une activité de s’exécuter plusieurs fois jusqu’à ce qu’une condition particulière soit remplie. Vous pouvez utiliser cette fonctionnalité pour les activités qui doivent s’exécuter plusieurs fois ou qui sont sujettes à des erreurs et qui peuvent nécessiter plusieurs tentatives avant d’aboutir.

Lorsque vous activez les nouvelles tentatives pour une activité, vous pouvez définir un délai et une condition. Le délai correspond au temps (exprimé en secondes ou minutes) d’attente du Runbook avant la nouvelle exécution de l’activité. Si aucun délai n’est spécifié, l’activité est immédiatement réexécutée après son exécution.

![Délai de nouvelle tentative d’activité](media/automation-graphical-authoring-intro/retry-delay.png)

La condition de nouvelle tentative est une expression PowerShell qui est évaluée après chaque exécution de l’activité. Si l’expression correspond à True, l’activité s’exécute à nouveau. Si l’expression correspond à False, l’activité n’est pas réexécutée et le Runbook passe à l’activité suivante.

![Délai de nouvelle tentative d’activité](media/automation-graphical-authoring-intro/retry-condition.png)

La condition de nouvelle tentative peut utiliser une variable appelée $RetryData qui fournit un accès aux informations sur les nouvelles tentatives d’activité. Cette variable possède les propriétés indiquées dans le tableau suivant.

| Propriété | Description |
|:--|:--|
| NumberOfAttempts | Nombre d’exécutions de l’activité. |
| Sortie | Sortie de la dernière exécution de l’activité. |
| TotalDuration | Délai écoulé depuis la première exécution de l’activité. |
| StartedAt | Heure au format UTC à laquelle l’activité a été exécutée pour la première fois. |

Voici des exemples de conditions de nouvelles tentatives d’activité.

	# Run the activity exactly 10 times.
	$RetryData.NumberOfAttempts -ge 10 

	# Run the activity repeatedly until it produces any output.
	$RetryData.Output.Count -ge 1 

	# Run the activity repeatedly until 2 minutes has elapsed. 
	$RetryData.TotalDuration.TotalMinutes -ge 2

### Contrôle Script de workflow

Un contrôle Script de workflow est une activité spéciale qui accepte du code de workflow PowerShell pour fournir des fonctionnalités qui, sans cela, ne serait peut-être pas disponibles. Il ne s'agit pas d'un workflow complet, mais il doit contenir des lignes valides de code de workflow PowerShell. Il n'accepte pas de paramètres, mais il peut utiliser des variables pour les paramètres de sortie d'activité et d'entrée de Runbook. Toute sortie de l'activité est ajoutée au bus de données, sauf si elle n'a aucun lien sortant, auquel cas elle est ajoutée à la sortie du Runbook.

Par exemple, le code suivant effectue des calculs de date à l'aide d'une variable d'entrée de Runbook appelée $NumberOfDays. Il envoie ensuite la valeur date-heure calculée en tant que sortie qui doit être utilisée par les activités suivantes dans le Runbook.

    $DateTimeNow = InlineScript{(Get-Date).ToUniversalTime()}
    $DateTimeStart = InlineScript{($using:DateTimeNow).AddDays(-$using:NumberOfDays)}
	$DateTimeStart


## Liens et workflow

Dans un Runbook graphique, un **lien** connecte deux activités. Il est affiché sur le canevas sous la forme d'une flèche pointant de l'activité source vers l'activité de destination. Les activités s'exécutent dans le sens de la flèche, l'activité de destination commençant une fois l'activité source terminée.

### Créer un lien

Créez un lien entre deux activités en sélectionnant l'activité source, puis en cliquant sur le cercle situé en bas de la forme. Faites glisser la flèche vers l'activité de destination, puis relâchez-la.

![Créer un lien](media/automation-graphical-authoring-intro/create-link.png)

Sélectionnez le lien pour configurer ses propriétés dans le panneau Configuration. Cela inclut le type du lien, qui est décrit dans le tableau suivant.

| Type de lien | Description |
|:---|:---|
| Pipeline | L'activité de destination est exécutée une fois pour chaque sortie d'objet de l'activité source. L'activité de destination n'est pas exécutée si l'activité source ne génère aucune sortie. La sortie de l'activité source est disponible sous la forme d'un objet. |
| Séquence | L'activité de destination s'exécute une seule fois. Elle reçoit un tableau d'objets de l'activité source. La sortie de l'activité source est disponible sous la forme d'un tableau d'objets. |

### Activité de départ

Un Runbook graphique commence par toute activité qui n'a pas un lien entrant. Il s'agit souvent d'une seule activité qui fait office d'activité de départ du Runbook. Si plusieurs activités n'ont pas de lien entrant, le Runbook démarre en les exécutant en parallèle. Lorsque chaque activité est terminée, il suit les liens pour exécuter les autres activités.

### Conditions

Lorsque vous spécifiez une condition sur un lien, l'activité de destination est exécutée uniquement si la condition a pour résultat la valeur true. Vous utiliserez généralement une variable $ActivityOutput dans une condition pour récupérer la sortie de l'activité source.

Pour un lien de type pipeline, vous spécifiez une condition pour un seul objet, et cette condition est évaluée pour chaque sortie d'objet par l'activité source. L'activité de destination est ensuite exécutée pour chaque objet qui remplit la condition. Par exemple, avec une activité source Get-AzureVM, la syntaxe suivante peut être utilisée pour qu'un lien pipeline conditionnel récupère uniquement les machines virtuelles en cours d'exécution.

	$ActivityOutput['Get-AzureVM'].PowerState -eq 'Started'

Pour un lien de type séquence, la condition est évaluée une seule fois, car un seul tableau contenant la sortie de tous les objets à partir de l'activité source est retourné. C'est pour cette raison qu'un lien séquence ne peut pas être utilisé pour filtrer comme un lien pipeline ; il détermine simplement si l'activité suivante est exécutée ou non. Le code suivant illustre le même exemple d'évaluation de la sortie de Get-AzureVM pour déterminer les machines virtuelles qui sont en cours d'exécution. Dans ce cas, le code parcourt chaque objet du tableau et produit la valeur true si au moins une machine virtuelle est en cours d'exécution. L'activité de destination est responsable de l'analyse de ces données.

	$test = $false
	$VMs = $ActivityOutput['Get-AzureVm']
	Foreach ($VM in VMs)
	{
		If ($VM.PowerState –eq 'Started')
			{
				$test = $true
			}
	}
	$test

Lorsque vous utilisez un lien conditionnel, les données disponibles de l'activité source vers d'autres activités dans cette branche sont filtrées par la condition. Si une activité est la source vers plusieurs liens, les données disponibles pour les activités de chaque branche dépendent de la condition spécifiée dans le lien de connexion à cette branche.

Par exemple, l'activité source du Runbook ci-dessous obtient toutes les machines virtuelles. Elle a deux liens conditionnels et un lien sans condition. Le premier lien conditionnel utilise l'expression *$ActivityOutput['Get-AzureVM'.PowerState -eq 'Started'* pour filtrer uniquement les machines virtuelles en cours d'exécution. Le deuxième lien conditionnel utilise l'expression *$ActivityOutput['Get-AzureVM'].PowerState -eq 'Stopped'* pour filtrer uniquement les machines virtuelles actuellement arrêtées.

![Exemple de lien conditionnel](media/automation-graphical-authoring-intro/conditional-links.png)

Toute activité qui suit le premier lien et qui utilise la sortie d'activité de Get-AzureVM obtient uniquement les machines virtuelles qui étaient démarrées au moment de l'exécution de Get-AzureVM. Toute activité qui suit le deuxième lien obtient uniquement les machines virtuelles qui étaient arrêtées au moment de l'exécution de Get-AzureVM. Toute activité suivant le troisième lien obtient toutes les machines virtuelles, quel que soit leur état d'exécution.

### Jonctions

Une jonction est une activité spéciale qui attend que toutes les branches entrantes aient terminé. Cela vous permet d'exécuter plusieurs activités en parallèle et de vous assurer qu'elles ont toutes terminé avant de continuer.

Alors qu'une jonction peut avoir un nombre illimité de liens entrants, un seul de ces liens peut être un pipeline. Le nombre de liens de type séquence entrants n'est pas limité. Vous êtes autorisé à créer la jonction avec plusieurs liens de type pipeline entrants et d'enregistrer le Runbook, mais il échouera lorsqu'il sera exécuté.

L'exemple ci-dessous représente une partie d'un Runbook qui démarre un ensemble de machines virtuelles tout en téléchargeant simultanément des correctifs à appliquer à ces machines. Une jonction permet de garantir que les deux processus sont terminés avant que le Runbook poursuive.

![Jonction](media/automation-graphical-authoring-intro/junction.png)

### Cycles

Un cycle se produit lorsqu'une activité de destination a un lien qui revient vers son activité source ou vers une autre activité qui, au final, revient à sa source. Les cycles ne sont actuellement pas autorisés dans la création de graphiques. Si votre Runbook a un cycle, il s'enregistrera correctement, mais il recevra une erreur lorsqu'il s'exécutera.

![Cycle](media/automation-graphical-authoring-intro/cycle.png)

### Boucles

Une boucle se produit lorsque vous répétez une activité un nombre de fois spécifié ou que vous continuez à la répéter jusqu'à ce qu'une condition particulière soit remplie. Les boucles ne sont actuellement pas prises en charge dans les Runbooks graphiques.

### Partage de données entre des activités

Toutes les données qui sont générées par une activité avec un lien sortant sont écrites dans le *bus de données* du Runbook. Toute activité du Runbook peut utiliser les données présentes dans le bus de données pour renseigner les valeurs de paramètres ou les inclure dans le code de script. Une activité peut accéder à la sortie de toute activité précédente du workflow.

La façon dont les données sont écrites dans le bus de données varie en fonction du type de lien figurant sur l'activité. Pour un **pipeline**, les données sont sorties sous la forme de plusieurs objets. Pour un lien de type **séquence**, les données sont sorties sous la forme d'un tableau. S'il n'y a qu'une seule valeur, elle sera sortie sous la forme d'un tableau à un seul élément.

Vous avez le choix entre deux méthodes pour accéder aux données présentes dans le bus de données. La première consiste à utiliser une source de données **Sortie d'activité** pour renseigner un paramètre d'une autre activité. Si la sortie est un objet, vous ne pouvez spécifier qu'une seule propriété.

![Sortie d'activité](media/automation-graphical-authoring-intro/activity-output-datasource.png)

Vous pouvez également récupérer la sortie d'une activité dans une source de données **Expression PowerShell** ou à partir d'une activité **Script de workflow** avec une variable ActivityOutput. Si la sortie est un objet, vous ne pouvez spécifier qu'une seule propriété. Les variables ActivityOutput utilisent la syntaxe suivante.

	$ActivityOutput['Activity Label']
	$ActivityOutput['Activity Label'].PropertyName 

### Points de contrôle

Vous pouvez définir des [points de contrôle](automation-powershell-workflow/#checkpoints) dans un Runbook graphique en sélectionnant *Runbook de point de contrôle* sur n’importe quelle activité. Cette option permet de définir un point de contrôle après l’exécution de l’activité.

![Point de contrôle](media/automation-graphical-authoring-intro/set-checkpoint.png)

Les recommandations relatives à la définition de points de contrôles dans votre Runbook s’appliquent également aux Runbooks graphiques. Si le Runbook utilise les applets de commande Azure, vous devez suivre toute activité soumise à des points de contrôle avec l’applet de commande Add-AzureRMAccount dans l’éventualité où le Runbook serait interrompu et redémarré sur un autre Worker à partir de ce point de contrôle.


## Authentification auprès de ressources Azure

Dans Azure Automation, la plupart des Runbooks requièrent une authentification auprès des ressources Azure. La méthode classique utilisée pour cette authentification est l'applet de commande Add-AzureAccount avec une [ressource d'informations d'identification](http://msdn.microsoft.com/library/dn940015.aspx) qui représente un utilisateur Active Directory disposant d'un accès au compte Azure. Cette procédure est décrite dans la rubrique [Configuration d'Azure Automation](automation-configuring.md).

Vous pouvez ajouter cette fonctionnalité à un Runbook graphique en ajoutant une ressource d'informations d'identification au canevas, suivie d'une activité Add-AzureAccount. Add-AzureAccount utilise l'activité d'informations d'identification pour son entrée. Cette opération est illustrée dans l'exemple suivant.

![Activités d'authentification](media/automation-graphical-authoring-intro/authentication-activities.png)

Vous devez effectuer une authentification au début du Runbook et après chaque point de contrôle. Cela signifie qu'une activité Add-AzureAccount doit être ajoutée après chaque activité Checkpoint-Workflow. Vous n'avez pas besoin d'ajouter une activité d'informations d'identification dans la mesure où vous pouvez utiliser la même.

![Sortie d'activité](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## Entrée et sortie de Runbook

### Entrée de Runbook

Un Runbook peut nécessiter une entrée d’un utilisateur lorsqu’il démarre le Runbook via le portail Azure ou à partir d’un autre Runbook si celui actuel est utilisé en tant qu’enfant. Par exemple, si vous avez un Runbook qui crée une machine virtuelle, vous devrez peut-être fournir des informations telles que le nom de la machine virtuelle et d'autres propriétés chaque fois que vous démarrez le Runbook.

Vous acceptez une entrée pour un Runbook en définissant un ou plusieurs paramètres d'entrée. Vous fournissez des valeurs pour ces paramètres chaque fois à chaque démarrage du Runbook. Lorsque vous démarrez un Runbook avec le portail Azure, il vous invite à fournir des valeurs pour chacun des paramètres d’entrée du Runbook.

Vous pouvez accéder aux paramètres d'entrée d'un Runbook en cliquant sur le bouton **Entrée et sortie** dans la barre d'outils du Runbook.

![Entrée/sortie de Runbook](media/automation-graphical-authoring-intro/runbook-edit-input-output.png)

Cela ouvre le contrôle **Entrée et sortie** où vous pouvez modifier un paramètre d'entrée existant ou en créer un nouveau en cliquant sur **Ajouter une entrée**.

![Ajouter une entrée](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Chaque paramètre d'entrée est défini par les propriétés figurant dans le tableau suivant.

|Propriété|Description|
|:---|:---|
| Nom | Nom unique du paramètre. Il ne peut contenir que des caractères alphanumériques et ne peut pas contenir d'espace. |
| Description | Description facultative du paramètre d'entrée. |
| Type | Type de données attendu pour la valeur de paramètre. Le portail Azure fournira un contrôle approprié pour le type de données de chaque paramètre lorsque vous serez invité à indiquer une entrée. |
| Obligatoire | Spécifie si une valeur doit être fournie pour le paramètre. Le Runbook ne peut pas être démarré si vous ne fournissez pas une valeur pour chaque paramètre obligatoire pour lequel aucune valeur par défaut n'est définie. |
| Valeur par défaut | Spécifie quelle valeur est utilisée pour le paramètre si aucune n'est pas fournie. Cela peut être Null ou une valeur spécifique. |


### Sortie de Runbook

Les données créées par toute activité qui ne dispose pas d'un lien sortant seront ajoutées à la [sortie du Runbook](http://msdn.microsoft.com/library/azure/dn879148.aspx). La sortie est enregistrée avec la tâche du Runbook et est disponible pour un Runbook parent lorsque le Runbook est utilisé en tant qu'enfant.


## Expressions PowerShell

Un des avantages de la création de graphiques est qu'elle vous donne la possibilité de créer un Runbook avec une connaissance de PowerShell minimale. Pour le moment, vous devez avoir quelques connaissances de base sur PowerShell pour remplir certaines [valeurs de paramètres](#activities) et définir des [conditions de lien](#links-and-workflow). Cette section propose une brève introduction aux utilisateurs qui ne connaissent pas les expressions PowerShell. La totalité des informations sur PowerShell est disponible dans [Écriture de scripts avec Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).


### Source de données d’expressions PowerShell

Vous pouvez utiliser une expression PowerShell comme source de données pour remplir la valeur d'un [paramètre d'activité](#activities) avec les résultats d'un code PowerShell. Il peut s'agir d'une seule ligne de code qui exécute une fonction simple ou de plusieurs lignes qui suivent une logique complexe. Toute sortie de commande non affectée à une variable correspond à la sortie de la valeur du paramètre.

Par exemple, la commande suivante affiche la date actuelle.

	Get-Date

Les commandes suivantes construisent une chaîne à partir de la date actuelle et l'affectent à une variable. Le contenu de la variable est ensuite envoyé à la sortie

	$string = "The current date is " + (Get-Date)
	$string

Les commandes suivantes évaluent la date actuelle et renvoient une chaîne qui indique si la date du jour est un jour de la semaine ou du week-end.

	$date = Get-Date
	if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
	else { "Weekday" }
	
 

### Sortie d'activité

Pour utiliser la sortie d'une activité précédente dans le Runbook, utilisez la variable $ActivityOutput avec la syntaxe suivante.

	$ActivityOutput['Activity Label'].PropertyName

Par exemple, si la propriété d'une activité requiert le nom d'une machine virtuelle, vous pouvez utiliser l'expression suivante.

	$ActivityOutput['Get-AzureVm'].Name

Si la propriété requiert l'objet machine virtuelle au lieu d'une simple propriété, vous devez renvoyer l'objet entier avec la syntaxe suivante.

	$ActivityOutput['Get-AzureVm']

Vous pouvez également utiliser la sortie d'une activité dans une expression plus complexe comme celle-ci, qui concatène le texte au nom de la machine virtuelle.

	"The computer name is " + $ActivityOutput['Get-AzureVm'].Name


### Conditions

Utilisez les [opérateurs de comparaison](https://technet.microsoft.com/library/hh847759.aspx) pour comparer des valeurs ou déterminer si une valeur correspond à un modèle spécifié. Une comparaison renvoie la valeur $true ou $false.

Par exemple, la condition suivante détermine si la machine virtuelle d'une activité nommée *Get-AzureVM* est actuellement *arrêtée*.

	$ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

La condition suivante détermine si la même machine virtuelle est dans un état autre qu'*arrêté*.

	$ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Vous pouvez joindre plusieurs conditions en utilisant un [opérateur logique](https://technet.microsoft.com/library/hh847789.aspx) comme **-and** ou **-or**. Par exemple, la condition suivante détermine si la machine virtuelle de l'exemple précédent est dans un état *arrêté* ou *en cours d'arrêt*.

	($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### Tables de hachage

Les [tables de hachage](http://technet.microsoft.com/library/hh847780.aspx) sont des paires nom/valeur servant à renvoyer un ensemble de valeurs. Les propriétés de certaines activités peuvent attendre une table de hachage plutôt qu'une valeur simple. Vous pouvez également voir une table de hachage appelée dictionnaire.

Une table de hachage se crée avec la syntaxe suivante. Une table de hachage peut contenir un nombre quelconque d'entrées, chacune étant définie par un nom et une valeur.

	@{ <name> = <value>; [<name> = <value> ] ...}

Par exemple, l'expression suivante crée une table de hachage à utiliser dans la source de données pour un paramètre d'activité qui attend une table de hachage avec des valeurs pour une recherche sur Internet.

	$query = "Azure Automation"
	$count = 10
	$h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
	$h

L'exemple suivant utilise la sortie d'une activité nommée *Obtenir la connexion Twitter* pour remplir une table de hachage.

	@{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
	  'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
	  'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
	  'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## Articles connexes

- [Apprentissage du workflow Windows PowerShell](automation-powershell-workflow.md)
- [Ressources Automation](http://msdn.microsoft.com/library/azure/dn939988.aspx)
- [Opérateurs](https://technet.microsoft.com/library/hh847732.aspx)
 

<!-----HONumber=AcomDC_0302_2016-->