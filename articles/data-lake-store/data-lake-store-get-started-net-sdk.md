<properties
   pageTitle="Utiliser le Kit de développement logiciel (SDK) .NET Data Lake Store pour développer des applications | Azure"
   description="Utiliser le Kit de développement logiciel (SDK) .NET Azure Data Lake Store pour développer des applications"
   services="data-lake-store"
   documentationCenter=""
   authors="nitinme"
   manager="paulettm"
   editor="cgronlun"/>

<tags
   ms.service="data-lake-store"
   ms.devlang="na"
   ms.topic="hero-article"
   ms.tgt_pltfrm="na"
   ms.workload="big-data"
   ms.date="03/07/2016"
   ms.author="nitinme"/>

# Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET

> [AZURE.SELECTOR]
- [Utilisation du portail](data-lake-store-get-started-portal.md)
- [Utiliser PowerShell](data-lake-store-get-started-powershell.md)
- [Utilisation du kit de développement logiciel (SDK) .NET](data-lake-store-get-started-net-sdk.md)
- [Utilisation de l’interface de ligne de commande Azure](data-lake-store-get-started-cli.md)
- [Utilisation de Node.js](data-lake-store-manage-use-nodejs.md)

Apprenez à utiliser le Kit de développement logiciel (SDK) .NET Azure Data Lake Store pour créer un compte Azure Data Lake et effectuer des opérations de base comme créer des dossiers, télécharger des fichiers de données, supprimer votre compte, etc. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).

## Configuration requise

* Visual Studio 2013 ou 2015. Les instructions ci-dessous utilisent Visual Studio 2015.
* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Activez votre abonnement Azure** pour la version d'évaluation publique de Data Lake Store. Consultez les [instructions](data-lake-store-get-started-portal.md#signup).
* Créer une application Azure Active Directory (AAD) et récupérer son **ID client** et l’**URI de réponse**. Pour plus d’informations sur les applications AAD et des instructions sur la façon d’obtenir un ID client, consultez [Création de l’application Active Directory et du principal du service à l’aide du portail](../resource-group-create-service-principal-portal.md). L’URI de réponse sera également disponible sur le portail une fois l’application créée.

## Comment s’authentifier à l’aide d’Azure Active Directory ?

L’extrait de code ci-dessous fournit deux méthodes d’authentification :

* **Interactive**, où un utilisateur s’inscrit à l’aide de l’application. Ceci est implémenté dans la méthode `AuthenticateUser` dans l’extrait de code ci-dessous.

* **Non interactive**, où l’application fournit ses propres informations d’identification. Ceci est implémenté dans la méthode `AuthenticateAppliaction` dans l’extrait de code ci-dessous.

Bien que l’extrait de code ci-dessous fournit des méthodes pour les deux approches, cet article utilise la méthode `AuthenticateUser`. Pour cette méthode, vous devez fournir l’ID client de l’application AAD et l’URI de réponse. Le lien fournit dans les conditions préalables donne accès à des instructions sur la façon d’obtenir ces données.

>[AZURE.NOTE] Si vous souhaitez modifier l’extrait de code et utiliser la méthode `AuthenticateApplication`, vous devez également fournir la clé d’authentification client, en plus de l’ID client et de l’URI de réponse client, en tant qu’entrées pour la méthode. L’article [Création de l’application Active Directory et du principal du service à l’aide du portail](../resource-group-create-service-principal-portal.md) fournit également des informations sur la génération et la récupération de la clé d’authentification client.



## Créer une application .NET

1. Ouvrez Visual Studio et créez une application console.

2. Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.

3. Dans **Nouveau projet**, entrez ou sélectionnez les valeurs suivantes :

	| Propriété | Valeur |
	|----------|-----------------------------|
	| Catégorie | Modèles/Visual C#/Windows |
	| Modèle | Application console |
	| Nom | CreateADLApplication |

4. Cliquez sur **OK** pour créer le projet.

5. Ajoutez les packages Nuget à votre projet.

	1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nom du projet, puis cliquez sur **Gérer les packages NuGet**.
	2. Dans l’onglet **Gestionnaire de package Nuget**, assurez-vous que **Source du package** a la valeur **nuget.org** et que la case **Inclure la version préliminaire** est cochée.
	3. Recherchez et installez les packages Data Lake Store suivants :

		* `Microsoft.Azure.Management.DataLake.Store`
		* `Microsoft.Azure.Management.DataLake.StoreUploader`

		![Ajouter une source Nuget](./media/data-lake-store-get-started-net-sdk/ADL.Install.Nuget.Package.png "Créer un compte Azure Data Lake")

	4. Installez également le package `Microsoft.IdentityModel.Clients.ActiveDirectory` pour l’authentification Azure Active Directory. Veillez à *décocher* la case **inclure la version préliminaire** afin de pouvoir installer une version stable de ce package.

		![Ajouter une source Nuget](./media/data-lake-store-get-started-net-sdk/adl.install.azure.auth.png "Créer un compte Azure Data Lake")


	5. Fermez le **Gestionnaire de package NuGet**.

7. Ouvrez **Program.cs** et remplacez le bloc de code existant par le code suivant : Renseignez également les valeurs des paramètres inclus dans l’extrait de code, tels que **\_adlsAccountName**, **\_resourceGroupName** et remplacez les espaces réservés pour **APPLICATION-CLIENT-ID**, **APPLICATION-REPLY-URI** et **SUBSCRIPTION-ID**.

	Ce code déroule le processus de création d’un compte Data Lake Store, de création de dossiers dans le magasin, de téléchargement de fichiers et enfin de suppression du compte. Si vous recherchez des exemples de données à charger, vous pouvez récupérer le dossier **Données Ambulance** dans le [Référentiel Git Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        using System;
        using System.IO;
        using System.Security;
        using System.Text;
        using System.Collections.Generic;
        using System.Linq;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.Azure.Management.DataLake.StoreUploader;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name for a NEW Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value. This resource group should already exist.
                    _location = "East US 2";

                    string localFolderPath = @"C:\local_path"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = @"C:\local_path\file.txt"; // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = remoteFolderPath + "file.txt";

                    // Authenticate the user
                    var tokenCreds = AuthenticateUser("common", "https://management.core.windows.net/",
                        "<APPLICATION-CLIENT-ID>", new Uri("https://<APPLICATION-REPLY-URI>")); // TODO: Replace bracketed values.

                    SetupClients(tokenCreds, "<SUBSCRIPTION-ID>"); // TODO: Replace bracketed value.

                    // Run sample scenarios
                    WaitForNewline("Authenticated.", "Creating NEW account.");
                    CreateAccount();
                    WaitForNewline("Account created.", "Creating a directory.");

                    // Create a directory in the Data Lake Store
                    CreateDirectory(remoteFolderPath);
                    WaitForNewline("Directory created.", "Showing directory info.");

                    // Get info about the directory in the Data Lake Store
                    var itemInfo = GetItemInfo(remoteFolderPath);
                    Console.WriteLine("Type: " + itemInfo.Type);
                    Console.WriteLine("Last modified (UTC): " +
                                      new DateTime(1970, 1, 1, 0, 0, 0, 0, DateTimeKind.Utc).AddMilliseconds(
                                          itemInfo.ModificationTime.Value));
                    WaitForNewline("Directory info shown.", "Uploading a file.");

                    // Upload a file to the Data Lake Store
                    UploadFile(localFilePath, remoteFilePath);
                    WaitForNewline("File uploaded.", "Listing files and directories.");

                    // List the files in the Data Lake Store
                    var itemList = ListItems(remoteFolderPath);
                    var fileMenuItems = itemList.Select(a => String.Format("{0,15} {1}", a.Type, a.PathSuffix));
                    Console.WriteLine(String.Join("\r\n", fileMenuItems));
                    WaitForNewline("Files and directories listed.", "Appending content to a file.");

                    // Append to a file in the Data Lake Store
                    AppendToFile(remoteFilePath, "123");
                    WaitForNewline("Content appended.", "Downloading a file.");

                    // Download a file from the Data Lake Store
                    DownloadFile(remoteFilePath, localFilePath);
                    WaitForNewline("File downloaded.", "Deleting account.");

                    // Delete account
                    DeleteAccount();
                    WaitForNewline("Account deleted. You can now exit.");
                }

                // Helper function to show status and wait for user input
                public static void WaitForNewline(string reason, string nextAction = "")
                {
                    if (!String.IsNullOrWhiteSpace(nextAction))
                    {
                        Console.WriteLine(reason + "\r\nPress ENTER to continue...");
                        Console.ReadLine();
                        Console.WriteLine(nextAction);
                    }
                    else
                    {
                        Console.WriteLine(reason + "\r\nPress ENTER to continue...");
                        Console.ReadLine();
                    }
                }

                // Authenticate the user with AAD through an interactive popup.
                // You need to have an application registered with AAD in order to authenticate.
                //   For more information and instructions on how to register your application with AAD, see:
                //   https://azure.microsoft.com/fr-FR/documentation/articles/resource-group-create-service-principal-portal/
                public static TokenCredentials AuthenticateUser(string tenantId, string resource, string appClientId, Uri appRedirectUri, string userId = "")
                {
                    var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenantId);

                    var tokenAuthResult = authContext.AcquireToken(resource, appClientId, appRedirectUri,
                        PromptBehavior.Auto, UserIdentifier.AnyUser);

                    return new TokenCredentials(tokenAuthResult.AccessToken);
                }

                // Authenticate the application with AAD through the application's secret key.
                // You need to have an application registered with AAD in order to authenticate.
                //   For more information and instructions on how to register your application with AAD, see:
                //   https://azure.microsoft.com/fr-FR/documentation/articles/resource-group-create-service-principal-portal/
                public static TokenCredentials AuthenticateApplication(string tenantId, string resource, string appClientId, Uri appRedirectUri, SecureString clientSecret)
                {
                    var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenantId);
                    var credential = new ClientCredential(appClientId, clientSecret);

                    var tokenAuthResult = authContext.AcquireToken(resource, credential);

                    return new TokenCredentials(tokenAuthResult.AccessToken);
                }

                //Set up clients
                public static void SetupClients(TokenCredentials tokenCreds, string subscriptionId)
                {
                    _adlsClient = new DataLakeStoreAccountManagementClient(tokenCreds);
                    _adlsClient.SubscriptionId = subscriptionId;

                    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(tokenCreds);
                    _adlsFileSystemClient.SubscriptionId = subscriptionId;
                }

                // Create account
                public static void CreateAccount()
                {
                    // Create ADLS account
                    var adlsParameters = new DataLakeStoreAccount(location: _location);
                    _adlsClient.Account.Create(_resourceGroupName, _adlsAccountName, adlsParameters);
                }

                // Delete account
                public static void DeleteAccount()
                {
                    _adlsClient.Account.Delete(_resourceGroupName, _adlsAccountName);
                }

                // List all ADLS accounts within the subscription
                public static List<DataLakeStoreAccount> ListAdlStoreAccounts()
                {
                    var response = _adlsClient.Account.List(_adlsAccountName);
                    var accounts = new List<DataLakeStoreAccount>(response);

                    while (response.NextPageLink != null)
                    {
                        response = _adlsClient.Account.ListNext(response.NextPageLink);
                        accounts.AddRange(response);
                    }

                    return accounts;
                }

                // Upload a file
                public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
                {
                    var parameters = new UploadParameters(srcFilePath, destFilePath, _adlsAccountName, isOverwrite: force);
                    var frontend = new DataLakeStoreFrontEndAdapter(_adlsAccountName, _adlsFileSystemClient);
                    var uploader = new DataLakeStoreUploader(parameters, frontend);
                    uploader.Execute();
                }

                // Concatenate files
                public static void ConcatenateFiles(string[] srcFilePaths, string destFilePath)
                {
                    _adlsFileSystemClient.FileSystem.Concat(destFilePath, srcFilePaths, _adlsAccountName);
                }

                // Get file or directory info
                public static FileStatusProperties GetItemInfo(string path)
                {
                    return _adlsFileSystemClient.FileSystem.GetFileStatus(path, _adlsAccountName).FileStatus;
                }

                // List files and directories
                public static List<FileStatusProperties> ListItems(string directoryPath)
                {
                    return _adlsFileSystemClient.FileSystem.ListFileStatus(directoryPath, _adlsAccountName).FileStatuses.FileStatus.ToList();
                }

                // Download file
                public static void DownloadFile(string srcPath, string destPath)
                {
                    var stream = _adlsFileSystemClient.FileSystem.Open(srcPath, _adlsAccountName);
                    var fileStream = new FileStream(destPath, FileMode.Create);

                    stream.CopyTo(fileStream);
                    fileStream.Close();
                    stream.Close();
                }

                // Append to file
                public static void AppendToFile(string path, string content)
                {
                    var stream = new MemoryStream(Encoding.UTF8.GetBytes(content));

                    _adlsFileSystemClient.FileSystem.Append(path, stream, _adlsAccountName);
                }

                // Create a directory
                public static void CreateDirectory(string path)
                {
                    _adlsFileSystemClient.FileSystem.Mkdirs(path, _adlsAccountName);
                }
            }
        }


8. Générez et exécutez l’application. Suivez les invites pour exécuter et terminer l’application.

## Autres méthodes de création d’un compte Data Lake Store

- [Prise en main de Data Lake Store avec le portail](data-lake-store-get-started-portal.md)
- [Prise en main de Data Lake Store avec PowerShell](data-lake-store-get-started-powershell.md)
- [Prise en main de Data Lake Store avec l’interface de ligne de commande Azure](data-lake-store-get-started-cli.md)


## Étapes suivantes

- [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
- [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

<!---HONumber=AcomDC_0309_2016-->