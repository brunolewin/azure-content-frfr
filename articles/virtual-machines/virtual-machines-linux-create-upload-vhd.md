<properties
	pageTitle="Création et téléchargement d'un VHD Linux | Microsoft Azure"
	description="Création et téléchargement d’un disque dur virtuel (VHD) Azure avec le modèle de déploiement classique contenant le système d'exploitation Linux."
	services="virtual-machines"
	documentationCenter=""
	authors="dsk-2015"
	manager="timlt"
	editor="tysonn"
	tags="azure-service-management"/>

<tags
	ms.service="virtual-machines"
	ms.workload="infrastructure-services"
	ms.tgt_pltfrm="vm-linux"
	ms.devlang="na"
	ms.topic="article"
	ms.date="01/22/2016"
	ms.author="dkshir"/>

# Création et téléchargement d'un disque dur virtuel contenant le système d'exploitation Linux

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)]Modèle Resource Manager


Cet article vous montre comment créer et télécharger un disque dur virtuel pour que vous puissiez l'utiliser comme image personnelle pour créer des machines virtuelles dans Azure. Vous apprendrez comment préparer le système d'exploitation pour créer plusieurs machines virtuelles basées sur cette image.

[AZURE.INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Une machine virtuelle Azure exécute le système d’exploitation basé sur l’image que vous choisissez pendant la création. Ces images sont conservées au format VHD, dans des fichiers .vhd au sein de votre compte de stockage. Pour plus d'informations, consultez les pages relatives aux [disques dans Azure](virtual-machines-disks-vhds.md) et aux [images dans Azure](virtual-machines-images.md).

Lors de la création de la machine virtuelle, vous pouvez personnaliser certains paramètres du système d'exploitation pour qu'ils correspondent à l'application que vous souhaitez exécuter. Pour obtenir des instructions, consultez le guide [Création d'une machine virtuelle personnalisée](virtual-machines-create-custom.md).

**Important** : l'accord de niveau de service de la plateforme Azure s'applique aux machines virtuelles exécutant le système d'exploitation Linux uniquement lorsqu'une des distributions reconnues est utilisée avec les détails de configuration définis sous « Versions prises en charge » dans [Linux dans les distributions approuvées par Azure](virtual-machines-linux-endorsed-distributions.md). Toutes les distributions Linux de la galerie d'images Azure sont des distributions reconnues répondant à la configuration requise.


## Conditions préalables
Cet article part du principe que vous disposez des éléments suivants :

- **Un certificat de gestion** : vous avez créé un certificat de gestion pour l'abonnement pour lequel vous souhaitez télécharger un disque dur virtuel, puis exporté ce certificat vers un fichier .cer. Pour plus d'informations sur la création de certificats, consultez la page [Vue d’ensemble des certificats pour Azure](../cloud-services/cloud-services-certs-create.md).

- **Un système d'exploitation Linux installé dans un fichier .vhd** : vous avez installé un système d'exploitation Linux pris en charge dans un disque dur virtuel. Il existe de nombreux outils de création de fichiers .vhd. Par exemple, vous pouvez utiliser une solution de virtualisation telle que Hyper-V pour créer le fichier .vhd et installer le système d'exploitation. Pour obtenir des instructions, consultez la page [Installation du rôle Hyper-V et configuration d'une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).

	**Important** : Azure ne prend pas en charge le nouveau format VHDX. Vous pouvez convertir le disque au format VHD à l'aide de Hyper-V Manager ou de l’applet de commande convert-vhd.

	Pour accéder à la liste des distributions approuvées, consultez la page [Linux dans les distributions approuvées par Azure](virtual-machines-linux-endorsed-distributions.md). Pour accéder à la liste générale des distributions Linux, consultez [Informations concernant les distributions non approuvées](virtual-machines-linux-create-upload-vhd-generic.md).

- **Interface de ligne de commande Azure** : si vous utilisez un système d'exploitation Linux pour créer votre image, utilisez l’[interface de ligne de commande Azure](virtual-machines-command-line-tools.md) pour charger le fichier VHD.

- **Outils Azure Powershell** : l’applet de commande `Add-AzureVhd` est également utilisable pour télécharger le fichier VHD. Consultez la page [Téléchargements Azure](https://azure.microsoft.com/downloads/) pour télécharger les applets de commande Azure Powershell. Pour les informations de référence, consultez la page [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx).

<a id="prepimage"> </a>
## Étape 1 : préparation de l'image pour le téléchargement

Azure prend en charge diverses distributions de Linux (voir [Distributions Linux approuvées](virtual-machines-linux-endorsed-distributions.md)). Les articles suivants vous montrent comment préparer les diverses distributions de Linux prises en charge dans Azure :

- **[Distributions CentOS](virtual-machines-linux-create-upload-vhd-centos.md)**
- **[Debian Linux](virtual-machines-linux-create-upload-vhd-debian.md)**
- **[Oracle Linux](virtual-machines-linux-create-upload-vhd-oracle.md)**
- **[Red Hat Enterprise Linux](virtual-machines-linux-create-upload-vhd-redhat.md)**
- **[SLES et openSUSE](../virtual-machines-linux-create-upload-vhd-suse)**
- **[Ubuntu](virtual-machines-linux-create-upload-vhd-ubuntu.md)**
- **[Autres - Distributions non approuvées](virtual-machines-linux-create-upload-vhd-generic.md)**

Consultez également les **[Notes d'installation Linux](virtual-machines-linux-create-upload-vhd-generic.md#linuxinstall)** pour obtenir d’autres conseils sur la préparation d'images Linux pour Azure.

En suivant toutes les étapes indiquées dans ces guides, vous devez disposer d'un fichier VHD prêt pour le téléchargement dans Azure.

<a id="connect"> </a>
## Étape 2 : préparation de la connexion à Azure

Avant de pouvoir télécharger un fichier .vhd, vous devez établir une connexion sécurisée entre votre ordinateur et votre abonnement Azure.


### En cas d’utilisation de l’interface de ligne de commande Azure

Par défaut, l’interface de ligne de commande Azure est configurée pour le modèle de déploiement Resource Manager. Par conséquent, assurez-vous que vous êtes bien dans le modèle de déploiement classique à l'aide de cette commande :

		azure config mode asm  

Exécutez ensuite l’une des méthodes suivantes pour vous connecter à votre abonnement Azure.

Utilisez la méthode Azure AD pour vous connecter :

1. Ouvrez une fenêtre d'Azure CLI

2. Type :

	`azure login`

	Lorsque vous y êtes invité, tapez votre nom d'utilisateur et votre mot de passe.

**OU** utilisez un fichier PublishSettings à la place :

1. Ouvrez une fenêtre d'Azure CLI

2. Type :

	`azure account download`

	Cette commande ouvre une fenêtre de navigateur et télécharge automatiquement un fichier .publishsettings contenant des informations et un certificat pour votre abonnement Azure.

3. Enregistrez le fichier .publishsettings

4. Type :

	`azure account import <PathToFile>`

	Où `<PathToFile>` est le chemin d'accès complet au fichier .publishsettings.

	Pour plus d’informations, consultez [Se connecter à Azure avec la CLI Azure](../xplat-cli-connect.md).


### En cas d’utilisation d’Azure PowerShell

Utilisez la méthode Azure AD pour vous connecter :

1. Ouvrez une fenêtre Azure PowerShell.

2. Type :

	`Add-AzureAccount`

	Quand vous y êtes invité, entrez votre ID et votre mot de passe d’entreprise.

**OU**, utilisez les fichiers PublishSettings :

1. Ouvrez une fenêtre Azure PowerShell.

2. Type :

	`Get-AzurePublishSettingsFile`

	Cette commande ouvre une fenêtre de navigateur et télécharge automatiquement un fichier .publishsettings contenant des informations et un certificat pour votre abonnement Azure.

3. Enregistrez le fichier .publishsettings.

4. Type :

	`Import-AzurePublishSettingsFile <PathToFile>`

	Où `<PathToFile>` est le chemin d'accès complet au fichier .publishsettings.

	Pour plus d’informations, consultez la rubrique [Comment installer et configurer Azure PowerShell](powershell-install-configure.md).

> [AZURE.NOTE] Nous vous recommandons d’utiliser la nouvelle méthode Azure Active Directory pour vous connecter à votre abonnement Azure, à partir de l’interface CLI Azure ou d’Azure PowerShell.

<a id="upload"> </a>
## Étape 3 : chargement de l’image dans Azure

Vous aurez besoin d’un compte de stockage pour charger votre fichier de disque dur virtuel. Vous pouvez en choisir un existant ou en créer un. Pour créer un compte de stockage, consultez [Création d’un compte de stockage](../storage/storage-create-storage-account.md).

Lorsque vous téléchargez le fichier .vhd, vous pouvez le placer n’importe où dans votre stockage d’objets blob. Dans les exemples de commandes suivants, **BlobStorageURL** correspond à l'URL du compte de stockage que vous prévoyez d’utiliser ; **YourImagesFolder** est le conteneur du stockage d'objets blob où vous voulez stocker vos images. **VHDName** est l’étiquette affichée dans le [portail Azure](http://portal.azure.com) ou dans le [portail Azure Classic](http://manage.windowsazure.com) pour identifier le disque dur virtuel. **PathToVHDFile** est le chemin d’accès complet et le nom du fichier .vhd sur votre machine.


### En cas d’utilisation de l’interface de ligne de commande Azure

Utilisez l’interface de ligne de commande Azure pour charger l’image, à l’aide de la commande suivante :

		azure vm image create <ImageName> --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> --os Linux <PathToVHDFile>

Pour plus d’informations, consultez [Informations de référence sur l’interface de ligne de commande Azure pour la gestion des services Azure](virtual-machines-command-line-tools.md).


### En cas d’utilisation de PowerShell

Depuis la fenêtre Azure PowerShell utilisée lors de l’étape précédente, tapez :

		Add-AzureVhd -Destination <BlobStorageURL>/<YourImagesFolder>/<VHDName> -LocalFilePath <PathToVHDFile>

Pour plus d'informations, consultez la page [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx).


[Step 1: Prepare the image to be uploaded]: #prepimage
[Step 2: Prepare the connection to Azure]: #connect
[Step 3: Upload the image to Azure]: #upload

<!---HONumber=AcomDC_0204_2016-->