<properties 
	pageTitle="Vue d’ensemble de la protection du contenu" 
	description="Cet article donne une vue d’ensemble de la protection du contenu avec Media Services." 
	services="media-services" 
	documentationCenter="" 
	authors="Juliako" 
	manager="dwrede" 
	editor=""/>

<tags 
	ms.service="media-services" 
	ms.workload="media" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="02/18/2016" 
	ms.author="juliako"/>

#Vue d’ensemble de la protection du contenu


Microsoft Azure Media Services vous permet de sécuriser votre contenu multimédia dès lors qu’il quitte votre ordinateur via le stockage, le traitement et la remise. Media Services permet de transmettre un contenu chiffré dynamiquement avec la norme AES (Advanced Encryption Standard) (à l’aide de clés de chiffrement 128 bits) et le chiffrement commun CENC (Common Encryption) en utilisant PlayReady et/ou Widevine DRM. Media Services fournit également un service de distribution de clés AES et licences PlayReady aux clients autorisés. Vous pouvez également utiliser les partenaires AMS suivants pour vous aider à distribuer des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

- L'image suivante montre le flux de travail « Chiffrement commun dynamique PlayReady et/ou Widevine DRM ». Pour plus de détails, consultez [Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine DRM](media-services-protect-with-drm.md).

![Protéger avec PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)


- L'image suivante montre le flux de travail « Chiffrement dynamique AES-128 ». Pour plus de détails, consultez [Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés](media-services-protect-with-aes128.md).

![Protéger avec AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

>[AZURE.NOTE]Pour pouvoir utiliser le chiffrement dynamique, vous devez obtenir au moins une unité réservée de diffusion en continu pour le point de terminaison de diffusion en continu à partir duquel vous prévoyez de diffuser votre contenu chiffré.

##Concepts

###Options de chiffrement d’élément multimédia

Selon le type de contenu que vous souhaitez télécharger, stocker et remettre, Media Services met à votre disposition différentes options de chiffrement.

**None**: aucun chiffrement. Il s’agit de la valeur par défaut. À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.

Si vous prévoyez de remettre du contenu MP4 via un téléchargement progressif, utilisez cette option pour télécharger votre contenu.

**StorageEncrypted**: utilisez cette option pour chiffrer votre contenu localement à l’aide du chiffrement AES 256 bits, puis chargez-le vers Azure Storage où il est stocké au repos sous forme chiffrée. Les éléments multimédias protégés par le chiffrement de stockage sont automatiquement déchiffrés et placés dans un système de fichiers chiffré avant d’être encodés, puis éventuellement rechiffrés avant d’être rechargés sous la forme d’un nouvel élément multimédia de sortie. Le principal cas d’utilisation du chiffrement de stockage concerne la sécurisation des fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.

Pour fournir un élément multimédia avec chiffrement de stockage, vous devez configurer la stratégie de remise de l'élément multimédia afin que Media Services sache comment vous souhaitez remettre votre contenu. Pour que votre élément multimédia puisse être diffusé en continu, le serveur de diffusion supprime le chiffrement de stockage et diffuse votre contenu à l'aide de la stratégie de remise spécifiée (par exemple AES, chiffrement commun ou aucun chiffrement).

**CommonEncryptionProtected**: utilisez cette option si vous souhaitez chiffrer du contenu (ou charger du contenu déjà chiffré) avec Common Encryption. PlayReady et Widewine sont chiffrés conformément à la spécification de chiffrement commun (CENC) et sont pris en charge par AMS.

**EnvelopeEncryptionProtected**: utilisez cette option si vous souhaitez protéger du contenu (ou charger du contenu déjà protégé) HTTP Live Streaming (HLS) chiffré avec AES (Advanced Encryption Standard). Notez que si vous téléchargez du contenu HLS déjà chiffré avec AES, il doit avoir été chiffré par Transform Manager.



###Chiffrement dynamique

Microsoft Azure Media Services vous permet de transmettre du contenu chiffré de manière dynamique avec la norme AES (Advanced Encryption Standard) (à l’aide de clés de chiffrement 128 bits) et la gestion des droits numériques (DRM) PlayReady et/ou Widevine.

Actuellement, vous pouvez chiffrer les formats de diffusion en continu suivants : HLS, MPEG DASH et Smooth Streaming. Vous ne pouvez pas chiffrer le format de diffusion en continu HDS ni les téléchargements progressifs.

Si vous souhaitez que Media Services chiffre un élément multimédia, vous devez associer une clé de chiffrement (CommonEncryption ou EnvelopeEncryption) à votre élément multimédia et configurer des stratégies d’autorisation pour la clé.

Vous devez également configurer la stratégie de remise de l’élément multimédia. Si vous souhaitez diffuser un élément multimédia avec chiffrement de stockage, assurez-vous de spécifier comment vous souhaitez le remettre en configurant la stratégie de remise d’élément multimédia.

Lorsqu’un lecteur demande un flux de données, Media Services utilise la clé spécifiée pour chiffrer dynamiquement votre contenu à l’aide du chiffrement AES ou du chiffrement commun. Pour déchiffrer le flux de données, le lecteur demande la clé au service de remise de clé. Pour déterminer si l’utilisateur est autorisé à obtenir la clé, le service évalue les stratégies d’autorisation que vous avez spécifiées pour la clé.

>[AZURE.NOTE]Pour tirer parti du chiffrement dynamique, vous devez d’abord obtenir au moins une unité de diffusion en continu à la demande pour le point de terminaison de diffusion en continu à partir duquel vous envisagez de distribuer votre contenu chiffré. Pour plus d’informations, voir [Mise à l’échelle de Media Services](media-services-manage-origins.md#scale_streaming_endpoints).

###Service de remise de licences et de clés

Media Services fournit un service de remise de licences DRM (PlayReady et Widevine) et de clés en clair AES aux clients autorisés. Vous pouvez utiliser le portail Azure Classic, l’API REST ou le kit de développement logiciel (SDK) Media Services pour .NET pour configurer des stratégies d’authentification et d’autorisation pour vos licences et vos clés.

Notez que si vous utilisez le portail, vous pouvez configurer une stratégie AES (qui sera appliquée à tout le contenu chiffré AES) et une stratégie PlayReady (qui sera appliquée à tout le contenu chiffré PlayReady). Utilisez le kit SDK Media Services pour .NET si vous souhaitez bénéficier d’un contrôle accru sur les configurations.

###Licence PlayReady 

Media Services fournit un service de remise de licences PlayReady. Lorsque le lecteur de l’utilisateur final (par exemple Silverlight) tente de lire votre contenu PlayReady protégé, une demande est envoyée au service de remise de licence pour obtenir une licence. Si le service de licence approuve la demande, il émet la licence, qui est envoyée au client et peut être utilisée pour déchiffrer et lire le contenu spécifié.

Les licences contiennent les droits et les restrictions que vous souhaitez pour le runtime DRM PlayReady, qui s’appliquent lorsqu’un utilisateur tente de lire du contenu protégé. Media Services propose des API qui vous permettent de configurer vos licences PlayReady. Pour plus d'informations, consultez la page [Présentation du modèle de licence PlayReady de Media Services](media-services-playready-license-template-overview.md).

###Licence Widevine

AMS vous permet également de diffuser du contenu MPEG DASH chiffré avec Widevine DRM. PlayReady et Widewine sont chiffrés conformément à la spécification de chiffrement commun (CENC). Vous pouvez utiliser [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (en commençant par la version 3.5.1) ou une API REST pour configurer votre AssetDeliveryConfiguration afin d’utiliser Widevine.

En commençant par le Kit de développement logiciel (SDK) Media Services .NET 3.5.2, Media Services vous permet de configurer le [modèle de licence Widevine](media-services-widevine-license-template-overview.md) et d’obtenir des licences Widevine. Vous pouvez également utiliser les partenaires AMS suivants pour vous aider à distribuer des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

###Restriction à jeton

La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : ouverte ou restriction à jeton. La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS). Media Services prend en charge les jetons aux formats SWT (Simple Web Tokens) et JWT (JSON Web Token). Media Services ne fournit pas de services de jeton sécurisé. Vous pouvez créer un STS personnalisé ou utiliser l’ACS Microsoft Azure pour émettre des jetons. Le STS doit être configuré pour créer un jeton signé avec la clé spécifiée et émettre les revendications spécifiées dans la configuration de restriction de jeton. Le service de remise de clé Media Services retourne la clé (ou licence) demandée au client si le jeton est valide et que les revendications du jeton correspondent à celles configurées pour la clé (ou licence).

Lorsque vous configurez la stratégie de restriction par jeton, vous devez définir les paramètres principaux de clé de vérification, émetteur et public. La clé de vérification principale contient la clé utilisée pour signer le jeton, l’émetteur est le service de jeton sécurisé qui émet le jeton. Le public (parfois appelé l’étendue) décrit l’objectif du jeton ou la ressource à laquelle le jeton autorise l’accès. Le service de remise de clé Media Services valide le fait que les valeurs du jeton correspondent aux valeurs du modèle.


##Scénarios courants

###Protéger le contenu stocké et diffuser du contenu multimédia chiffré dynamiquement en continu, utiliser le service AMS de fourniture de clé/licence.

1. Ajoutez un fichier mezzanine de haute qualité à une ressource. Appliquez l’option de chiffrement de stockage à la ressource.
2. Configurez les points de terminaison de diffusion en continu.
1. Encodez-la sous forme de jeu de fichiers MP4 à débit adaptatif. Appliquez l’option de chiffrement de stockage à la ressource de sortie.
1. Créez la clé de contenu de chiffrement pour la ressource que vous souhaitez chiffrer dynamiquement pendant la lecture.
2. Configurez la stratégie d’autorisation de clé de contenu.
1. Configurez la stratégie de remise de ressources (utilisée par l’empaquetage dynamique et le chiffrement dynamique).
1. Publiez la ressource en créant un localisateur à la demande.
1. Diffusez le contenu publié.

###Utiliser le service de remise de clés et de licences de Media Services avec vos propres services de chiffrage et de diffusion en continu

Pour plus d’informations, consultez la page [Intégration du service de remise de licences PlayReady d’Azure à votre propre chiffreur/serveur de diffusion en continu](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).

###Intégration avec des partenaires

[Utilisation de castLabs pour fournir des licences DRM à Azure Media Services](media-services-castlabs-integration.md)



##Parcours d’apprentissage de Media Services

[AZURE.INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

##Fournir des commentaires

[AZURE.INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


##Liens connexes

[Annonce de PlayReady en tant que service et du chiffrement AES dynamique avec Azure Media Services](http://mingfeiy.com/playready)

[Explication de la tarification de la remise de licences PlayReady d’Azure Media Services](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Débogage d’un flux de données chiffré utilisant le chiffrement AES dans Azure Media Services](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Authentification par jeton JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)

[Utilisation d'ACS Azure pour émettre des jetons](http://mingfeiy.com/acs-with-key-services)

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png

<!---HONumber=AcomDC_0224_2016-->