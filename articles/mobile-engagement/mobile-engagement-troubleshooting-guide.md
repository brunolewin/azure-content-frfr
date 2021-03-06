<properties 
   pageTitle="Guide de résolution des problèmes d’Azure Mobile Engagement" 
   description="Guide de dépannage pour Azure Mobile Engagement" 
   services="mobile-engagement" 
   documentationCenter="" 
   authors="piyushjo" 
   manager="dwrede" 
   editor=""/>

<tags
   ms.service="mobile-engagement"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="mobile-multiple"
   ms.workload="mobile" 
   ms.date="02/26/2016"
   ms.author="piyushjo"/>

# Azure Mobile Engagement - Guide de dépannage

## Introduction
Le guide de dépannage qui suit vous aidera à comprendre les causes principales de certains problèmes couramment rencontrés et vous permettra de les résoudre vous-même.

## Généralités

En règle générale, vous devez systématiquement vérifier les éléments suivants :

1. Assurez-vous que vous avez exécuté toutes les opérations requises pour l’intégration, comme décrit dans nos [didacticiels de prise en main](mobile-engagement-windows-store-dotnet-get-started.md),
2. que vous utilisez bien la dernière version du kit de développement logiciel de la plateforme, 
3. que vous effectuez les tests sur un périphérique réel et un émulateur, car certains problèmes sont spécifiques à l’émulateur, 
4. que vous n’atteignez pas les limites/seuils d’Engagement Mobile qui sont mentionnés [ici](../azure-subscription-service-limits.md).
5. Si vous n’êtes pas en mesure de vous connecter au backend du service Engagement Mobile ou si voyez pas les données chargées en continu, assurez-vous qu’il n’y a pas d’incident de service en cours [ici](https://azure.microsoft.com/status/)

## problèmes d’« Analyse »

### Mon périphérique n’apparaît pas sous l’onglet Analyse
L’onglet Analyse affiche les périphériques connectés à votre plate-forme Mobile Engagement en temps réel. Si vous procédez à un débogage sur un émulateur et un périphérique, vous devez voir au moins une session ici. Si l’application a été distribuée, les périphériques connectés à la plate-forme en temps réel apparaîtront dans la jauge Sessions actives.

Si vous ne voyez pas votre appareil dans l’onglet Analyse, il s’agit probablement un problème d’intégration du SDK. Voici quelques opérations à effectuer pour résoudre les problèmes courants :

1. Assurez-vous que vous utilisez la chaîne de connexion correcte dans l’application mobile et qu’elle est issue de la section Clés de la section du kit de développement logiciel et non de la section des clés de l’API. La chaîne de connexion connecte votre application mobile à l’instance de l’application Engagement Mobile et votre périphérique apparaît dans l’onglet Analyse. 
2. Pour la plateforme Windows - si votre page remplace la méthode `OnNavigatedTo`, assurez-vous d’appeler `base.OnNavigatedTo(e)`.
3. Si vous intégrez Mobile Engagement à une application mobile existante, vous pouvez également vérifier que vous n’avez manqué aucune opération en regardant les étapes d’intégration avancées [ici](mobile-engagement-windows-store-integrate-engagement.md)
4. Vérifiez que vous envoyez au moins un écran/une activité en remplaçant la page par EngagementActivity selon la plateforme que vous utilisez, comme décrit dans les [didacticiels de prise en main](mobile-engagement-windows-store-dotnet-get-started.md).

### Je vois un onglet Surveiller une session, même si j’ai déconnecté ou fermé mon application/émulateur. 
Si vous êtes le seul connecté à la plate-forme à ce stade, et si vous utilisez un émulateur pour ouvrir l’application, cela est probablement dû à des particularités de l’émulateur. En général, vous devez vous assurer que vous revenez à l’écran d’accueil de l’émulateur pour que la session de l’application se déconnecte correctement. En outre, sur la plate-forme Windows, pendant le débogage avec Visual Studio, il se peut que vous deviez vous assurer que dans Visual Studio, vous pouvez accéder à la barre de menus **Événements de cycle de vie**, cliquez sur **Interrompre** pour vraiment fermer la session. Voir [Didacticiel Windows](mobile-engagement-windows-store-dotnet-get-started.md) pour plus de détails.

## Problèmes d’« Analyse »

### Je ne vois pas de données/de données actualisées sur l’onglet Analyse 
Les données d’analyse sont recalculées régulièrement et l’actualisation peut prendre jusqu’à 24 heures. Ces données ne sont pas extraites en temps réel et elles seront actualisées pendant cette période de 24 heures. Assurez-vous toutefois que vous envoyez au moins un écran ou une activité au serveur principal de plateforme soit en remplaçant au moins une page par `EngagementActivity`, soit ou en appelant explicitement `SendActivity`.

### Je vois une date/heure mal définie pour un appareil sur l’onglet Analyse
La période d’analyse est basée sur la date à partir des paramètres de périphérique de l’utilisateur. Par conséquent, vérifiez que la date du périphérique est correctement définie.

## Problèmes « Segment »

### J’ai créé un segment et il s’affiche en grisé, ou il n’affiche pas toutes les données
Actuellement, la création de segment ne se fait pas en temps réel. Elle est calculée pendant l’agrégation des données d’analyse, et donc, peut prendre jusqu’à 24 heures. Vous devez contrôler plus tard, mais dans l’intervalle, vous devez également vous assurer que vos applications mobiles envoient effectivement les données sur la base avec laquelle vous formez les segments. Par exemple, si un événement, par exemple « foo » n’est pas envoyé par un appareil mobile, il n’y aura aucune donnée correspondant à un segment créé avec EventName = foo pour critère. Vous pouvez également vérifier votre intégration de kit de développement logiciel pour vous assurer que votre application mobile envoie les données correctement.

## Problèmes de notifications Push ou « Reach »

### Mes messages Push ne sont pas remis 

1. Essayez d’envoyer des notifications à un périphérique de test avant de vous assurer que tous les composants (application mobile, kit de développement de logiciel et services) sont connectés correctement et en mesure de livrer des notifications Push. 
2. Envoyez toujours la « notification hors application » la plus simple d’abord, via une campagne non planifiée et n’ayant pas de critère d’audience spécifié. Il s’agit à nouveau de prouver que la connectivité de notification fonctionne correctement. 
3. Si vous rencontrez des problèmes de livraison des notifications dans l’application, il peut être judicieux de commencer par envoyer une notification hors application d’abord. 
4. Assurez-vous que le « Push natif » est correctement configuré pour votre application mobile. Selon la plate-forme, il fera appel à des clés (Android, Windows) ou à des certificats (iOS). Voir [Interface utilisateur - Paramètres](mobile-engagement-user-interface-settings.md)
5. Les notifications hors application peuvent également être bloquées par l’utilisateur via le système d’exploitation mobile et donc, assurez-vous que ce n’est pas le cas. 
6. Assurez-vous que vous ne définissez pas l’option *Ignorer Audience, Push sera envoyé aux utilisateurs via l’API* dans la section **Campagne** de la couverture campagne, car cela garantit que les notifications Push ne pourraient être envoyées que via des API. 
7. Assurez-vous de tester votre campagne Push avec deux périphériques connectés via un réseau WiFi et votre opérateur téléphonique pour éliminer la connexion réseau en tant que source potentielle de problèmes.
8. Assurez-vous que la date/heure système de votre périphérique/émulateur est correcte, parce que n’importe quel périphérique hors synchronisation interférera avec la possibilité de service de notification Push pour remettre des notifications. 

Vous trouverez d’autres instructions de dépannage spécifiques de plateforme ci-dessous :

1. **iOS** 

	- Assurez-vous que les certificats sont valides et non expirés pour les Notifications Push iOS. 
	- Vérifiez que vous configurez correctement un certificat de *Production* dans votre application Mobile Engagement. 
	- Assurez-vous d’effectuer le test sur un *périphérique physique réel.* Le simulateur iOS ne peut pas traiter les messages push.
	- Vérifiez que l’identificateur d’offres groupées est correctement configuré dans l’application mobile. Suivez les instructions disponibles [ici](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
	- Lors du test, utilisez la distribution « Ad Hoc » dans votre profil d’approvisionnement mobile. Vous ne pourrez pas recevoir de notification si votre application est compilée à l’aide de « Debug »

2. **Android**

	- Vérifiez que vous avez spécifié le numéro de projet correct dans les fichiers AndroidManifest.xml de votre application mobile suivie du caractère \\n. 
	
	    	<meta-data android:name="engagement:gcm:sender" android:value="************\n" />
	    
	- Assurez-vous qu’il ne manque pas une autorisation ou que l’une d’elle n’est pas mal configurée dans le fichier manifeste Android.
	- Assurez-vous que le numéro de projet que vous ajoutez à votre application cliente provient du même compte que celui où vous avez obtenu la clé du serveur GCM. Toute incompatibilité entre les deux empêchera la sortie de vos notifications push. 
	- Si vous recevez des notifications système, mais pas dans l’application, passez en revue la [section Spécifier une icône de notifications](mobile-engagement-android-get-started.md), car il est probable que vous ne spécifiez pas l’icône correcte dans le fichier manifeste Android. 
	- Si vous envoyez une notification BigPicture, assurez-vous, au cas où vous disposez de serveurs d’images externes, qu’ils sont en mesure de prendre en charge HTTP « GET » et « HEAD ».

3. **Windows**
	
	- Assurez-vous que vous avez associé l’application à une application Windows Store valide. Dans Visual Studio, vous devez cliquer avec le bouton droit sur le projet et sélectionner l’option « Associate App with Store » et sélectionnez l’application que vous avez créée dans Windows Store. Cette application Windows Store doit être identique à celle de laquelle vous avez obtenu les informations d’identification Push native pour configurer le portail Mobile Engagement.
	- Si vous recevez des notifications Push hors application, mais pas dans les applications avec l’intégration `EngagementOverlay`, assurez-vous qu’il existe un élément de grille racine dans votre page. EngagementOverlay utilise le premier élément « Grid » qu’elle trouve dans le fichier .xaml pour ajouter deux vues web à votre page. Si vous souhaitez localiser l’endroit où les vues web seront placées, vous pouvez définir une grille nommée « EngagementGrid » ainsi, tout en vous assurant cependant que la hauteur et la largeur des deux vues web qui se suivent afficheront la notification et l’annonce qui suit en tant que notification d’application :
		
			<Grid x:Name="EngagementGrid"></Grid>

### J’ai créé une notification Push/annonce/campagne et même après qu’il m’ait envoyé la notification, il est affiché en tant qu’« Actif ». Qu’est-ce que cela signifie ? 
La **campagne** que vous avez créée dans Mobile Engagement est appelée ainsi parce qu’il s’agit d’une notification Push à long terme, ce qui signifie que lorsque de nouveaux appareils se connectent à votre plate-forme d’engagement mobile, ils reçoivent automatiquement une notification que vous configurez à ce niveau, s’ils répondent aux critères que vous avez définis dans la campagne. Il ne s’agit pas d’une notification unique, émise une fois pour toutes. Vous devez cliquer manuellement sur le bouton **Terminer** pour mettre fin à la campagne afin qu’elle n’envoie pas d’autres notifications.

### J’ai créé une campagne Push et je reçois des notifications indiquant qu’elle est réussie. Toutefois chaque fois que j’ouvre l’application, j’obtiens la notification qui a motivé mon action ? 
Cette erreur est susceptible de se produire pendant le test et si vous utilisez des émulateurs ou certains frameworks tels que TestFlight. Dans ce cas précis, chaque application exécute une instance, détecte un nouvel ID de périphérique l’envoie à notre serveur principal, ce qui fait que la plateforme Mobile Engagement le traite comme nouveau périphérique et envoie la notification.

## Obtenir une assistance

Si vous ne parvenez pas à résoudre le problème vous-même, vous pouvez :

1. Recherchez votre problème dans les threads existants sur le forum StackOverflow et le [forum MSDN](https://social.msdn.microsoft.com/Forums/windows/fr-FR/home?forum=azuremobileengagement) et, s’il n’y en a pas, posez une question. 
2. Si vous trouvez une fonctionnalité manquante, ajoutez / votez pour la demande sur notre [forum UserVoice](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Si vous bénéficiez d’une assistance Microsoft, ouvrez un incident de support en fournissant les détails suivants : 
	- ID d’abonnement Azure
	- Plate-forme (par exemple, iOS, Android etc.)
	- ID d'application
	- ID de campagne (pour les problèmes de notification Push)
	- ID de périphérique
	- Version du kit de développement logiciel Mobile Engagement (par exemple, le kit de développement logiciel Android v2.1.0)
	- Détails de l’erreur avec message d’erreur exact et scénario

<!---HONumber=AcomDC_0302_2016-->