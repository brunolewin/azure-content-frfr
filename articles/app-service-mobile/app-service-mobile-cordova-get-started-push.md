<properties
	pageTitle="Ajouter des notifications Push à l’application Apache Cordova à l’aide d’Azure Mobile Apps | Azure App Service"
	description="Découvrez comment utiliser Azure Mobile Apps pour envoyer des notifications Push à votre application Apache Cordova."
	services="app-service\mobile"
	documentationCenter="javascript"
	manager="ggailey777"
	editor=""
	authors="adrianhall"/>

<tags
	ms.service="app-service-mobile"
	ms.workload="mobile"
	ms.tgt_pltfrm="mobile-html"
	ms.devlang="javascript"
	ms.topic="article"
	ms.date="02/11/2016"
	ms.author="adrianha"/>

# Ajout de notifications Push à votre application Apache Cordova

[AZURE.INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## Vue d'ensemble

Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide Apache Cordova] afin qu’une notification Push soit envoyée chaque fois qu’un enregistrement est inséré. Ce didacticiel est basé sur le didacticiel [Démarrage rapide Apache Cordova], que vous devez effectuer en premier. Si vous disposez d’un serveur principal ASP.NET et n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devez ajouter le package d’extension de notification Push à votre projet. Pour plus d'informations sur les packages d'extension de serveur, consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps].

##<a name="prerequisites"></a>Configuration requise

Ce didacticiel est dédié aux applications Apache Cordova développées dans Visual Studio 2015 et exécutées sur l’Émulateur Google Android. Par ailleurs, vous pouvez suivre ce didacticiel sur d’autres émulateurs ou appareils, et sur différentes plates-formes de développement.

Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :

* Un [compte Google] avec une adresse électronique vérifiée.
* Un PC avec [Visual Studio Community 2015] ou version ultérieure.
* [Visual Studio Tools pour Apache Cordova].
* Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).
* Un projet [Démarrage rapide Apache Cordova]. Vous pouvez suivre d’autres didacticiels (comme l’[authentification]) au préalable, mais ce n’est pas obligatoire.
* Un appareil Android.

Bien que les notifications Push soient prises en charge sur les émulateurs Android, nous avons constaté leur instabilité. Nous vous déconseillons de tester les notifications Push sur les émulateurs.

##<a name="create-hub"></a>Créer un hub de notification

[AZURE.INCLUDE [app-service-mobile-create-notification-hub](../../includes/app-service-mobile-create-notification-hub.md)]

##<a name="enable-gcm"></a>Activation de Google Cloud Messaging

Dans la mesure où nous ciblons la plate-forme Google Android, vous devez activer Google Cloud Messaging. Si vous cibliez les appareils Apple iOS, vous activeriez la prise en charge APNS. De la même manière, si vous cibliez les appareils Microsoft Windows, vous activeriez la prise en charge WNS ou MPNS.

[AZURE.INCLUDE [mobile-services-enable-google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

##<a name="configure-backend"></a>Configurer le backend d’application mobile pour l’envoi de demandes de notifications Push

[AZURE.INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

##<a name="update-service"></a>Mettre à jour le projet de serveur pour l’envoi de notifications Push

[AZURE.INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

##<a name="configure-device"></a>Configurer votre appareil Android pour le débogage USB

Pour pouvoir déployer votre application sur votre appareil Android, vous devez activer le débogage USB. Sur votre téléphone Android, procédez comme suit :

1. Accédez à **Settings** > **About phone**
2. Appuyez sur le **Build number** jusqu’à l’activation du mode développeur.
3. Revenez à **Settings**.
4. Sélectionnez **Developer Options**.
5. Activez l’option **USB debugging**.
6. Connectez votre téléphone Android sur votre PC de développement à l’aide d’un câble USB.

Pour le test de ce didacticiel, nous avons utilisé un appareil Google Nexus 5X exécutant une version Android 6.0 (Marshmallow). Toutefois, les techniques sont communes à l’ensemble des versions Android modernes.

##<a name="add-push-to-app"></a>Ajout de notifications Push à votre application

Vous devez vous assurer que votre projet d’application Apache Cordova est prêt à gérer les notifications Push.

### Installer le plug-in de notification Push Apache Cordova

En mode natif, les applications Apache Cordova ne gèrent pas les fonctionnalités de réseau ou d’appareils. Ces fonctionnalités sont fournies par des plug-ins publiés sur [npm](https://www.npmjs.com/) ou sur GitHub. Le plug-in `phonegap-plugin-push` est utilisé pour gérer les notifications Push du réseau.

Vous pouvez installer le plug-in de notification Push de l’une des façons suivantes :

**À partir de l'invite de commandes :**

    cordova plugin add phonegap-plugin-push

**À partir de Visual Studio :**

1.  Ouvrez le fichier `config.xml` à partir de l’Explorateur de solutions.
2.  Cliquez sur **Plug-ins** > **Personnalisé**, sélectionnez **Git** comme source d'installation, puis entrez `https://github.com/phonegap/phonegap-plugin-push` comme source.
	
	![](./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png)
	
4.  Cliquez sur la flèche en regard de la source d’installation, puis cliquez sur **Ajouter**

Le plug-in de notification Push est maintenant installé.

### Installez les services Android Google Play.

Le plug-in de notification Push PhoneGap sollicite les services Google Play. Pour effectuer l’installation :

1.  Ouvrez **Visual Studio**
2.  Cliquez sur **Outils** > **Android** > **Gestionnaire du Kit de développement logiciel (SDK) Android**
3.  Cochez les cases en regard des kits de développement à installer du dossier Extras. Les packages suivants sont requis :
    * Bibliothèque de prise en charge Android 23 ou version ultérieure
    * Référentiel de prise en charge Android 20 ou version ultérieure
    * Services Google Play 27 ou version ultérieure
    * Référentiel Google 22 ou version ultérieure
4.  Cliquez sur **Packages d’installation**.
5.  Attendez que l’installation se termine.

Les bibliothèques actuellement requises figurent dans la [documentation d’installation phonegap-plugin-push].

### Inscrire votre appareil pour les notifications Push au démarrage

1. Ajoutez un appel à **registerForPushNotifications** durant le rappel du processus de connexion, ou en bas de la méthode **onDeviceReady** :

 
		// Login to the service.
		client.login('google')
		    .then(function () {
		        // Create a table reference
		        todoItemTable = client.getTable('todoitem');
		
		        // Refresh the todoItems
		        refreshDisplay();
		
		        // Wire up the UI Event Handler for the Add Item
		        $('#add-item').submit(addItemHandler);
		        $('#refresh').on('click', refreshDisplay);
		
				// Added to register for push notifications.
		        registerForPushNotifications();
		
		    }, handleError);

	Cet exemple illustre l'appel à **registerForPushNotifications** une fois l'authentification réussie, ce qui est recommandé lors de l'utilisation conjointe des notifications Push et de l'authentification dans votre application.

2. Ajoutez la nouvelle méthode `registerForPushNotifications()` comme suit :

	    // Register for Push Notifications.
		// Requires that phonegap-plugin-push be installed.
	    var pushRegistration = null;
	    function registerForPushNotifications() {
	        pushRegistration = PushNotification.init({
	            android: {
	                senderID: 'Your_Project_ID'
	            },
	            ios: {
	                alert: 'true',
	                badge: 'true',
	                sound: 'true'
	            },
	            wns: {
	
	            }
	        });
	
	        pushRegistration.on('registration', function (data) {
	            client.push.register('gcm', data.registrationId);
	        });
	
	        pushRegistration.on('notification', function (data, d2) {
	            alert('Push Received: ' + data.message);
	        });
	
	        pushRegistration.on('error', handleError);
	    }

3. Dans le code ci-dessus, remplacez `Your_Project_ID` par l’ID de projet numérique associé à votre application de [Google Developer Console].

## Test de l'application avec le service mobile publié

Pour tester l’application, associez directement un téléphone Android à l’aide d’un câble USB. À la place de l’**Émulateur Google Android**, sélectionnez **Appareil**. Visual Studio télécharge l’application sur l’appareil, et l’exécute. Vous interagissez alors avec l’application sur l’appareil.

Améliorez votre expérience du développement. Les applications de partage d’écran comme [Mobizen] peuvent vous aider à développer une application Android, en projetant votre écran Android sur un navigateur web, sur votre PC.

Vous pouvez également tester l'application Android sur l'émulateur Android. N'oubliez pas d’ajouter d’abord un compte Google à l'émulateur.

##<a name="next-steps"></a>Étapes suivantes

* Consultez la documentation relative à [Notification Hubs] afin d’en découvrir davantage sur les notifications Push.
* Si vous ne l’avez pas encore fait, continuez le didacticiel en [ajoutant l’authentification] à votre application Apache Cordova.

<!-- URLs -->
[ajoutant l’authentification]: app-service-mobile-cordova-get-started-users.md
[Démarrage rapide Apache Cordova]: app-service-mobile-cordova-get-started.md
[Démarrage rapide Apache Cordova]: app-service-mobile-cordova-get-started.md
[authentification]: app-service-mobile-cordova-get-started-users.md
[Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[compte Google]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[Google Developer Console]: https://console.developers.google.com/home/dashboard
[documentation d’installation phonegap-plugin-push]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[Mobizen]: https://www.mobizen.com/
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/fr-FR/features/cordova-vs.aspx
[Notification Hubs]: ../notification-hubs/notification-hubs-overview.md

<!---HONumber=AcomDC_0302_2016-->