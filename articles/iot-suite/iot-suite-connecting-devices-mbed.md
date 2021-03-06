<properties
   pageTitle="Connectez un périphérique à l'aide de C sur mbed | Microsoft Azure"
   description="Explique comment connecter un appareil à la solution de surveillance à distance Azure IoT Suite préconfigurée à l’aide d’une application écrite en C et exécutée sous mbed."
   services=""
   suite="iot-suite"
   documentationCenter="na"
   authors="dominicbetts"
   manager="timlt"
   editor=""/>

<tags
   ms.service="iot-suite"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="02/05/2016"
   ms.author="dobett"/>


# Connexion de votre appareil à la solution préconfigurée de surveillance à distance IoT Suite

[AZURE.INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## Générer et exécuter l'exemple de solution C sur mbed

Les instructions qui suivent décrivent les étapes permettant de connecter un appareil [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] à la solution de surveillance à distance.

### Connectez le périphérique à votre réseau et votre ordinateur de bureau

1. Connectez le périphérique mbed à votre réseau avec un câble Ethernet. Cette étape est nécessaire car l'exemple d'application requiert un accès à internet.

2. Voir [Mise en route avec mbed][lnk-mbed-getstarted] pour connecter votre périphérique mbed à votre ordinateur de bureau.

3. Si votre ordinateur de bureau exécute Windows, consultez [Configuration PC][lnk-mbed-pcconnect] pour configurer l'accès aux ports série de votre périphérique mbed.

### Créez un projet mbed et importez l’exemple de code

1. Dans votre navigateur Web, accédez [au site de développement](https://developer.mbed.org/) mbed.org. Si vous n’êtes pas inscrit, une option servant à créer un nouveau compte vous sera présentée (c’est gratuit). Autrement, connectez-vous avec les informations d’identification de votre compte. Cliquez sur **Compilateur** dans le coin supérieur droit de la page. Cela devrait vous permettre d’accéder à l’interface de gestion de l’espace de travail.

2. Assurez-vous que la plate-forme matérielle que vous utilisez figure dans le coin supérieur droit de la fenêtre, ou cliquez sur l’icône du coin droit pour sélectionner votre plateforme matérielle.

3. Cliquez sur **Importer** dans le menu principal. Cliquez ensuite sur **Cliquez ici** pour procéder à l’importation via un lien URL en regard du logo de globe mbed.

    ![][6]

4. Dans la fenêtre contextuelle, saisissez le lien vers l’exemple de code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, puis cliquez sur **Importer**.

    ![][7]

5. Vous pouvez voir dans la fenêtre du compilateur mbed que l’importation de ce projet a entraîné l’importation de différentes bibliothèques. Certaines sont fournies et gérées par l’équipe Azure IoT ([azureiot\_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub\_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub\_amqp\_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [proton-c-mbed](https://developer.mbed.org/users/AzureIoTClient/code/proton-c-mbed/)), tandis que d’autres sont des bibliothèques tierces disponibles dans le catalogue de bibliothèques mbed.

    ![][8]

6. Ouvrez le fichier remote\_monitoring\\remote\_monitoring.c et recherchez le code suivant dans le fichier :

    ```
    static const char* deviceId = "[Device Id]";
    static const char* deviceKey = "[Device Key]";
    static const char* hubName = "[IoTHub Name]";
    static const char* hubSuffix = "[IoTHub Suffix, i.e. azure-devices.net]";
    ```

7. Remplacez [Device Id], [Device Key] par les données de votre appareil. Utilisez le nom d’hôte IoT Hub pour remplacer les espaces réservés [Nom IoTHub] et [Suffixe IoTHub, c’est-à-dire azure-devices.net]. Par exemple, si votre nom d’hôte IoT Hub est contoso.azure-devices.net, contoso est le **nom du hub** et tous les éléments suivants constituent le **suffixe du hub** :

    ```
    static const char* deviceId = "mydevice";
    static const char* deviceKey = "mykey";
    static const char* hubName = "contoso";
    static const char* hubSuffix = "azure-devices.net";
    ```

    ![][9]

### Créez et exécutez le projet.

1. Cliquez sur **Compiler** pour générer le programme. Vous pouvez sans risque ignorer les avertissements, mais si le traitement génère des erreurs, corrigez-les avant de continuer.

2. Si le traitement réussit, le site web du compilateur mbed génère un fichier .bin portant le nom de votre projet et le télécharge sur votre ordinateur local. Copier le fichier .bin sur l’appareil. Lorsque le fichier .bin est enregistré sur le périphérique, ce dernier redémarre et exécute le programme contenu dans le fichier .bin. Vous pouvez redémarrer manuellement le programme à tout moment en appuyant sur le bouton de réinitialisation sur le périphérique mbed.

3. Connectez-vous à l’appareil en utilisant une application cliente SSH, tel que PuTTY. Vous pouvez déterminer le port série que votre appareil va utiliser en consultant le Gestionnaire de périphériques Windows.

    ![][11]

4. Dans PuTTY, cliquez sur le type de connexion **Série**. Comme le périphérique se connecte généralement à 115 200 bauds, entrez 115200 dans le champ **Vitesse**. Cliquez ensuite sur **Ouvrir** :

5. Le programme démarre l’exécution. Il se peut que vous deviez réinitialiser le tableau (appuyez sur CTRL + Retour ou appuyez sur le bouton de réinitialisation du tableau) si le programme ne démarre pas automatiquement à la connexion.

    ![][10]

[AZURE.INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]


[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[9]: ./media/iot-suite-connecting-devices-mbed/suite6.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration

<!---HONumber=AcomDC_0218_2016-->