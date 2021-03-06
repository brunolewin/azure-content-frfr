<properties
	pageTitle="Ajout de l’authentification à Apache Cordova à l’aide de Mobile Apps | Azure App Service"
	description="Découvrez comment utiliser Mobile Apps dans Azure App Service pour authentifier les utilisateurs de votre application Apache Cordova via divers fournisseurs d’identité, notamment Google, Facebook, Twitter et Microsoft."
	services="app-service\mobile"
	documentationCenter="javascript"
	authors="adrianhall"
	manager="ggailey777"
	editor=""/>

<tags
	ms.service="app-service-mobile"
	ms.workload="na"
	ms.tgt_pltfrm="mobile-html"
	ms.devlang="javascript"
	ms.topic="article"
	ms.date="02/11/2016"
	ms.author="adrianha"/>

# Ajout de l’authentification à votre application Apache Cordova

[AZURE.INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## Résumé

Dans ce didacticiel, vous allez ajouter l’authentification au projet de démarrage rapide todolist sur Apache Cordova en faisant appel à un fournisseur d’identité pris en charge. Ce didacticiel est basé sur le didacticiel [Prise en main de Mobile Apps], que vous devez effectuer en premier.

##<a name="register"></a>Inscription de votre application pour l’authentification et configuration d’App Service

[AZURE.INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

##<a name="permissions"></a>Restriction des autorisations pour les utilisateurs authentifiés

[AZURE.INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

+ Dans Visual Studio, ouvrez le projet créé durant le didacticiel [Prise en main des applications mobiles], puis exécutez votre application dans l’**Émulateur Google Android** et vérifiez qu’un problème de connexion inattendue est indiqué après le démarrage de l’application.

    Cela se produit car l’application tente d’accéder au serveur principal en tant qu’utilisateur non authentifié. Le serveur principal redirige l’utilisateur vers une page d’authentification à l’aide d’OAuth. Toutefois, l’application n’approuve pas le point de terminaison OAuth.

Ensuite, vous allez mettre à jour l’application pour authentifier les utilisateurs avant de demander des ressources à partir du serveur principal d’applications mobiles.

##<a name="add-authentication"></a>Ajout de l’authentification à l’application

1. Ouvrez votre projet dans **Visual Studio**, puis ouvrez le fichier `www/index.html` pour modification.

2. Localisez la balise META `Content-Security-Policy` dans la section d’en-tête. Vous devez ajouter l’hôte OAuth à la liste des ressources autorisées.

    | Fournisseur | Nom du fournisseur du Kit de développement logiciel. | Hôte OAuth |
    | :--------------------- | :---------------- | :-------------------------- |
    | Azure Active Directory | aad | https://login.windows.net |
    | Facebook | facebook | https://www.facebook.com |
    | Google | google | https://accounts.google.com |
    | Microsoft | microsoftaccount | https://login.live.com |
    | Twitter | twitter | https://api.twitter.com |

    Voici un exemple Content-Security-Policy (implémenté pour Azure Active Directory) :

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' 
			data: gap: https://login.windows.net https://yourapp.azurewebsites.net; style-src 'self'">

    Vous devez remplacer `https://login.windows.net` par l’hôte OAuth du tableau ci-dessus. Consultez la [documentation Content-Security-Policy] pour en savoir plus sur cette balise META.

    Notez que certains fournisseurs d’authentification ne requièrent aucune modification Content-Security-Policy avec des appareils mobiles appropriés. Par exemple, aucune modification de l’approche Content-Security-Policy n’est nécessaire lorsque vous recourez à l’authentification Google sur un appareil Android.

3. Ouvrez le fichier `www/js/index.js` pour modification, recherchez la méthode `onDeviceReady()` et, sous le code de création du client, ajoutez le code suivant :

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Notez que ce code remplace le code existant qui crée la référence de table et actualise l'interface utilisateur.

    La méthode login() lance l'authentification auprès du fournisseur. La méthode login() est une méthode asynchrone qui renvoie une promesse JavaScript. Le reste de l’initialisation est placé au sein de la réponse de promesse, de manière à ce qu’aucune exécution n’intervienne avant la fin de la méthode login().

4. Dans le code que vous venez d'ajouter, remplacez `SDK_Provider_Name` par le nom de votre fournisseur de connexion. Par exemple, pour Azure Active Directory, utilisez `client.login('aad')`.

4. Exécutez votre projet. Une fois que le projet a terminé l’initialisation, votre application affiche la page de connexion OAuth du fournisseur d’authentification choisi.

##<a name="next-steps"></a>Étapes suivantes

* En savoir plus [À propos de l’authentification] avec Azure App Service.
* Poursuivez le didacticiel en ajoutant les [Notifications Push] à votre application Apache Cordova.

<!-- URLs. -->
[Prise en main de Mobile Apps]: app-service-mobile-cordova-get-started.md
[Prise en main des applications mobiles]: app-service-mobile-cordova-get-started.md
[documentation Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Notifications Push]: app-service-mobile-cordova-get-started-push.md
[À propos de l’authentification]: app-service-mobile-auth.md

<!---HONumber=AcomDC_0302_2016-->