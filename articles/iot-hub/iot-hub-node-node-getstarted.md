<properties
	pageTitle="Prise en main avec Azure IoT Hub pour Node.js | Microsoft Azure"
	description="Suivez ce didacticiel pour commencer à utiliser Azure IoT Hub avec Node.js."
	services="iot-hub"
	documentationCenter="nodejs"
	authors="dominicbetts"
	manager="timlt"
	editor=""/>

<tags
     ms.service="iot-hub"
     ms.devlang="javascript"
     ms.topic="hero-article"
     ms.tgt_pltfrm="na"
     ms.workload="na"
     ms.date="01/19/2016"
     ms.author="dobett"/>

# Prise en main d’Azure IoT Hub pour Node.js

[AZURE.INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

## Introduction

Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils IoT et un serveur principal de solution. L’une des plus grandes difficultés des projets IoT consiste à connecter des appareils au serveur principal de la solution de manière fiable et sécurisée. Pour relever ce défi, IoT Hub :

- Offre une messagerie évolutive Appareil vers cloud et Cloud vers appareil fiable.
- Assure la sécurité des communications grâce aux informations d’identification de sécurité par appareil et au contrôle d’accès.
- Inclut des bibliothèques d’appareils pour les langages et les plateformes les plus courants.

Ce didacticiel vous explique les procédures suivantes :

- Utilisez le portail Azure pour créer un hub IoT.
- Créer une identité de l’appareil dans votre hub IoT.
- Créer un périphérique simulé qui envoie les données de télémétrie au serveur back-end de votre service cloud.

À la fin de ce didacticiel, vous disposerez de trois applications de console Node.js :

* **CreateDeviceIdentity**, qui crée une identité d’appareil et une clé de sécurité associée pour connecter votre appareil simulé ;
* **ReadDEviceToCloudMessages.js**, qui affiche les données de télémétrie envoyées par votre périphérique simulé ;
* **SimulatedDevice.js**, qui se connecte à votre hub IoT avec l’identité d’appareil créée précédemment et envoie un message de télémétrie chaque seconde.

> [AZURE.NOTE] L’article [kit de développement logiciel IoT Hub][lnk-hub-sdks] fournit des informations sur les différents kits de développement logiciels que vous pouvez utiliser pour générer les deux applications qui s’exécutent sur les appareils et sur le serveur de solution principal.

Pour réaliser ce didacticiel, vous aurez besoin des éléments suivants :

+ Node.js version 0.12.x ou version ultérieure. <br/> [Préparer votre environnement de développement][lnk-dev-setup] décrit comment installer Node.js pour ce didacticiel sous Windows ou sous Linux.

+ Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure][lnk-free-trial].

## Créer un hub IoT

Pour que votre périphérique simulé puisse se connecter, vous devez créer un Hub IoT Hub. Les étapes suivantes vous montrent comment exécuter cette tâche à l’aide du portail Azure.

1. Connectez-vous au [portail Azure][lnk-portal].

2. Dans la barre de lancement, cliquez sur **Nouveau**, sur **Internet des objets**, puis sur **IoT Hub Azure**.

    ![][1]

3. Dans le panneau **IoT hub**, choisissez la configuration de votre concentrateur IoT.

    ![][2]

    * Dans la zone **Nom**, saisissez un nom pour identifier votre hub IoT. Une fois le **Nom** validé et disponible, une coche verte apparaît dans la case **Nom**.
    * Sélectionnez une **tarification et un niveau de mise à l’échelle**. Ce didacticiel ne nécessite pas un niveau spécifique.
    * Dans **Groupe de ressources**, créez un groupe de ressources Azure ou sélectionnez un groupe existant. Pour plus d’informations, consultez [Utilisation des groupes de ressources pour gérer vos ressources Azure][lnk-resource-groups].
    * Dans **Emplacement**, sélectionnez l’emplacement destiné à héberger votre concentrateur IoT.  

4. Une fois que vous avez choisi les options de configuration de votre hub IoT, cliquez sur **Créer**. La création du hub IoT par Azure peut prendre plusieurs minutes. Pour vérifier l’état d’avancement de l’opération, vous pouvez consulter le tableau d’accueil ou le panneau Notifications.

    ![][3]

5. Une fois le hub IoT créé, ouvrez le panneau du nouveau hub IoT, prenez note du **nom d’hôte**, puis cliquez sur l’icône **Clés**.

    ![][4]

6. Cliquez sur la stratégie **iothubowner**, puis copiez et prenez note de la chaîne de connexion dans le panneau **iothubowner**.

    ![][5]

7. Cliquez sur **Paramètres** dans le panneau IoT Hub, puis sur **Messagerie** dans le panneau **Paramètres**. Sur le panneau **Messagerie**, notez le **Nom compatible Event Hub** et **Point de terminaison compatible Event Hub**. Ces valeurs sont nécessaires lorsque vous créez votre application **read-d2c-messages**.

    ![][6]

Maintenant, vous avez créé votre concentrateur IoT et vous disposez d’un nom d’hôte IoT Hub, de la chaîne de connexion IoT Hub, du nom compatible Event Hub et des valeurs de point de terminaison compatible Event Hub pour suivre le reste de ce didacticiel.

[AZURE.INCLUDE [iot-hub-get-started-cloud-node](../../includes/iot-hub-get-started-cloud-node.md)]


[AZURE.INCLUDE [iot-hub-get-started-device-node](../../includes/iot-hub-get-started-device-node.md)]

## Exécution des applications

Vous êtes maintenant prêt à exécuter les applications.

1. À l’invite de commandes du dossier **readdevicetocloudmessages**, exécutez la commande suivante pour commencer à analyser votre IoT hub :

    ```
    node ReadDeviceToCloudMessages.js 
    ```

    ![][7]

2. À l’invite de commandes du dossier **simulateddevice**, exécutez la commande suivante pour commencer à analyser votre IoT hub :

    ```
    node SimulatedDevice.js
    ```

    ![][8]

## Étapes suivantes

Dans ce didacticiel, vous avez configuré un nouveau concentrateur IoT dans le portail, puis créé une identité d’appareil dans le registre d’identités du concentrateur. Vous avez utilisé cette identité d’appareil dans un appareil simulé qui envoie des messages de l’appareil vers le cloud au concentrateur et créé une autre application qui affiche les messages reçus par le concentrateur. Vous pouvez continuer à explorer les fonctionnalités d’IoT Hub et d’autres scénarios IoT dans les didacticiels suivants :

- [Envoyer des messages du cloud vers des appareils avec IoT Hub][lnk-c2d-tutorial] montre comment envoyer des messages aux appareils et traiter les informations de remise générées par IoT Hub.
- [Traiter les messages des appareils vers le cloud][lnk-process-d2c-tutorial] montre comment traiter de manière fiable des messages interactifs et de télémétrie provenant d’appareils.
- [Téléchargement de fichiers à partir d’appareils][lnk-upload-tutorial], qui décrit un modèle qui utilise les messages du cloud vers les appareils pour faciliter les téléchargements de fichiers à partir d’appareils.

<!-- Images. -->
[1]: ./media/iot-hub-node-node-getstarted/create-iot-hub1.png
[2]: ./media/iot-hub-node-node-getstarted/create-iot-hub2.png
[3]: ./media/iot-hub-node-node-getstarted/create-iot-hub3.png
[4]: ./media/iot-hub-node-node-getstarted/create-iot-hub4.png
[5]: ./media/iot-hub-node-node-getstarted/create-iot-hub5.png
[6]: ./media/iot-hub-node-node-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdks/blob/master/node/device/doc/devbox_setup.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-upload-tutorial]: iot-hub-csharp-csharp-file-upload.md

[lnk-hub-sdks]: iot-hub-sdks-summary.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-resource-groups]: resource-group-portal.md
[lnk-portal]: https://portal.azure.com/

<!---HONumber=AcomDC_0204_2016-->