<properties
   pageTitle="Déploiement de StorSimple Virtual Array 3 - Configuration de l’appareil virtuel en tant que serveur de fichiers"
   description="Ce troisième didacticiel du déploiement StorSimple Virtual Array vous explique comment configurer un appareil virtuel en tant que serveur de fichiers."
   services="storsimple"
   documentationCenter="NA"
   authors="alkohli"
   manager="carmonm"
   editor=""/>

<tags
   ms.service="storsimple"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="03/01/2016"
   ms.author="alkohli"/>

# Déploiement de StorSimple Virtual Array - Configuration en tant que serveur de fichiers

![](./media/storsimple-ova-deploy3-fs-setup/fileserver4.png)

## Introduction 

Cet article s'applique à Microsoft Azure StorSimple Virtual Array (également appelé appareil virtuel StorSimple local ou appareil virtuel StorSimple) exécutant la version de mise à la disposition générale (mars 2016). Cet article décrit comment effectuer la configuration initiale, inscrire votre serveur de fichiers StorSimple, finaliser la configuration de l’appareil, créer des partages SMB et s’y connecter. Il s’agit du dernier article de la série de didacticiels sur le déploiement nécessaires pour déployer complètement votre tableau virtuel en tant que serveur de fichiers ou serveur iSCSI.

Le processus d’installation et de configuration peut prendre jusqu’à 10 minutes.


## Configuration requise

Avant de configurer votre appareil virtuel StorSimple, assurez-vous que :

-   Vous avez configuré un appareil virtuel et vous y êtes connecté comme indiqué dans la rubrique [Configuration de StorSimple Virtual Array dans Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) ou [Configuration de StorSimple Virtual Array dans VMware](storsimple-ova-deploy2-provision-vmware.md).

-   Vous disposez de la clé d'inscription du service StorSimple Manager que vous avez créé pour gérer les appareils virtuels StorSimple. Pour plus d'informations, consultez l’[étape 2 : Obtention de la clé d’inscription](storsimple-ova-deploy1-portal-prep.md#step-2-get-the-service-registration-key) pour StorSimple Virtual Array.

-   S'il s'agit du deuxième appareil virtuel (ou ultérieur) que vous inscrivez auprès d’un service StorSimple Manager existant, vous devez disposer de la clé de chiffrement des données de service. Cette clé a été générée lorsque le premier appareil a été correctement inscrit auprès de ce service. Si vous avez perdu cette clé, consultez la rubrique [Obtenir la clé de chiffrement des données de service](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) pour votre StorSimple Virtual Array.

## Configuration étape par étape

Utilisez la procédure détaillée ci-dessous pour configurer et déployer votre appareil virtuel StorSimple.

## Étape 1 : Finalisation de la configuration de l'interface utilisateur web locale et inscription de votre appareil 


#### Pour finaliser l'installation et l’inscription de l'appareil

1.  Ouvrez une fenêtre de navigateur et connectez-vous à l'interface utilisateur web locale. Tapez :	

    `https://<ip-address of network interface>`

	Utilisez l'URL de connexion notée à l'étape précédente. Une erreur vous indique qu'il existe un problème avec le certificat de sécurité du site web. Cliquez sur **Poursuivre sur cette page web**.

	![](./media/storsimple-ova-deploy3-fs-setup/image2.png)

1.  Connectez-vous à l'interface utilisateur web de votre appareil virtuel en tant que **StorSimpleAdmin**. Entrez le mot de passe administrateur que vous avez modifié à l’étape 3 : démarrage de l’appareil virtuel dans [Configurer StorSimple Virtual Array dans Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) ou dans [Configurer StorSimple Virtual Array dans VMware](storsimple-ova-deploy2-provision-vmware.md).

	![](./media/storsimple-ova-deploy3-fs-setup/image3.png)

1.  Vous accéderez à la page d’**accueil**. Cette page décrit les différents paramètres requis pour configurer et inscrire l'appareil virtuel auprès du service StorSimple Manager. Notez que les **paramètres réseau**, **les paramètres du proxy web** et les **paramètres horaires** sont facultatifs. Les seuls paramètres requis sont les **paramètres de l’appareil** et les **paramètres du cloud**.

	![](./media/storsimple-ova-deploy3-fs-setup/image4.png)

1.  Dans la page **Paramètres réseau**, sous **Interfaces réseau**, DATA 0 sera automatiquement configuré pour vous. Chaque interface réseau est définie par défaut pour obtenir automatiquement l’adresse IP (DHCP). Par conséquent, une adresse IP, un sous-réseau et une passerelle seront automatiquement attribués (pour IPv4 et IPv6).

	![](./media/storsimple-ova-deploy3-fs-setup/image5.png)

	Si vous avez ajouté plusieurs interfaces réseau lors de la configuration de l'appareil, vous pouvez les configurer ici. Notez que vous pouvez configurer votre interface réseau en IPv4 uniquement ou en IPv4 et IPv6. Les configurations en IPv6 uniquement ne sont pas prises en charge.

1.  Des serveurs DNS sont requis car ils sont utilisés lorsque votre appareil tente de communiquer avec vos fournisseurs de services de stockage cloud ou pour résoudre votre appareil par nom lorsqu’il configuré comme un serveur de fichiers. Dans la page **Paramètres réseau**, sous **Serveurs DNS** :

    1.  Un serveur DNS principal et un serveur secondaire seront définis automatiquement. Si vous choisissez de configurer des adresses IP statiques, vous pouvez spécifier des serveurs DNS. Pour une haute disponibilité, nous vous recommandons de configurer un serveur DNS principal et un serveur secondaire.

    2.  Cliquez sur **Apply**. Cette opération appliquera et validera les paramètres réseau.

2.  Sur la page **Paramètres de l’appareil** :

    1.  Attribuez un **nom** unique à votre appareil. Ce nom peut contenir 1 à 15 caractères ainsi que des lettres, des chiffres et des traits d'union.

    2.  Cliquez sur l’icône **Serveur de fichiers** ![](./media/storsimple-ova-deploy3-fs-setup/image6.png) pour le **type** d’appareil que vous créez. Un serveur de fichiers vous permettra de créer des dossiers partagés.

    3.  Votre appareil étant un serveur de fichiers, vous devez l’associer à un domaine. Entrez un **nom de domaine**.

	1.  Cliquez sur **Apply**.

2.  Une boîte de dialogue s’affiche. Entrez vos informations d'identification de domaine au format spécifié. Cliquez sur l’icône en forme de coche. Les informations d'identification de domaine seront vérifiées. Un message d'erreur apparaît si les informations d'identification sont incorrectes.

	![](./media/storsimple-ova-deploy3-fs-setup/image7.png)

1.  Cliquez sur **Apply**. Cette opération appliquera et validera les paramètres de l’appareil.

	![](./media/storsimple-ova-deploy3-fs-setup/image8.png)

	> [AZURE.NOTE]
	> 
	> Assurez-vous que votre tableau virtuel est dans sa propre unité organisationnelle (UO) pour Active Directory et qu'aucun objet de stratégie de groupe (GPO) ne lui est appliqué.

1.  (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici.

	![](./media/storsimple-ova-deploy3-fs-setup/image9.png)

	Sur la page **Proxy Web** :

	1.  Indiquez l’**URL du proxy web** dans ce format : *adresse ou nom de domaine complet http://&lt;host-IP &gt;Numéro de Port*. Notez que les URL HTTPS ne sont pas prises en charge.

	2.  Définissez **Authentification** sur **De base**, **NTLM** ou **Aucune**.

	3.  Si vous utilisez une authentification, vous devrez également fournir un **nom d'utilisateur** et un **mot de passe**.

	4.  Cliquez sur **Apply**. Cette opération validera et appliquera les paramètres de proxy web configurés.

1.  (Facultatif) Configurez les paramètres d'heure de votre appareil, notamment le fuseau horaire et les serveurs NTP principal et secondaire. Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud.

	![](./media/storsimple-ova-deploy3-fs-setup/image10.png)

	Sur la page **Paramètres d’heure** :

	1.  Dans la liste déroulante, définissez le **fuseau horaire** en fonction de l'emplacement géographique de l’appareil déployé. Le fuseau horaire par défaut de votre appareil est PST. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.

	2.  Spécifiez un **serveur NTP principal** pour votre appareil ou acceptez la valeur par défaut time.windows.com. Vérifiez que votre réseau autorise le trafic NTP à passer de votre centre de données à Internet.

	3.  (Facultatif) Spécifiez un **serveur NTP secondaire** pour votre appareil.

	4.  Cliquez sur **Apply**. Cette opération validera et appliquera les paramètres d’heure configurés.

1.  Configurez les paramètres de cloud de votre appareil. Dans cette étape, vous allez finaliser la configuration de l’appareil local puis inscrire l'appareil auprès du service StorSimple Manager.

    1.  Saisissez la **clé d’inscription de service** que vous avez obtenue à l’[étape 2 : Obtention de la clé d’inscription](storsimple-ova-deploy1-portal-prep.md#step-2-get-the-service-registration-key) pour StorSimple Virtual Array.

    2.  S’il ne s’agit pas du premier appareil que vous inscrivez auprès de ce service, vous devrez fournir la **clé de chiffrement de données du service**. Cette clé et la clé d’enregistrement de service sont requises pour l’inscription d’appareils supplémentaires auprès du service StorSimple Manager. Pour plus d'informations, reportez-vous à la section permettant d’obtenir la [clé de chiffrement de données du service](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) sur votre interface utilisateur web locale.

    3.  Cliquez sur **S'inscrire**. Cette opération redémarra l’appareil. Vous devrez peut-être attendre 2 à 3 minutes avant que l'appareil soit inscrit. Une fois que l’appareil a redémarré, vous êtes redirigé vers la page de connexion.

		![](./media/storsimple-ova-deploy3-fs-setup/image13.png)
	

1.  Retournez dans le portail Azure Classic. Sur la page **Appareils**, vérifiez que l’appareil s’est bien connecté au service en vérifiant son état. L’état de l’appareil doit être **Actif**.

![](./media/storsimple-ova-deploy3-fs-setup/image12.png)

## Étape 2 : Finalisation de la configuration requise pour l’appareil

Pour finaliser la configuration minimale de votre appareil StorSimple, vous devez :

-   Sélectionner un compte de stockage à associer à votre appareil.

-   Choisir les paramètres de chiffrement pour les données envoyées vers le cloud.

Pour finaliser la configuration minimale requise, procédez comme suit dans le [portail Azure Classic](https://manage.windowsazure.com/).

#### Pour finaliser l'installation minimale de l’appareil

1.  Sur la page **Appareils**, sélectionnez l’appareil que vous venez de créer. Cet appareil apparaît en tant que **Actif**. Cliquez sur la flèche en regard du nom de l’appareil, puis sur **Démarrage rapide**.

2.  Cliquez sur **Terminer la configuration de l’appareil** pour démarrer l'Assistant Configurer l’appareil.

3.  Dans l'Assistant Configurer l’appareil, sur la page **Paramètres de base**, procédez comme suit :

	1.  Spécifiez un compte de stockage à utiliser avec votre appareil. Vous pouvez sélectionner un compte de stockage existant de cet abonnement dans la liste déroulante, ou spécifier **Ajouter** pour choisir un compte d'un autre abonnement.

	2.  Définissez les paramètres de chiffrement pour toutes les données au repos (chiffrement AES) qui seront envoyées vers le cloud. Pour chiffrer vos données, cochez la case pour **activer la clé de chiffrement de stockage cloud**. Entrez une clé de chiffrement de stockage cloud contenant 32 caractères. Entrez à nouveau la clé pour la confirmer. Une clé AES de 256 bits sera utilisée avec la clé définie par l'utilisateur pour le chiffrement.

	3.  Cliquez sur l’icône en forme de coche ![](./media/storsimple-ova-deploy3-fs-setup/image15.png).

		![](./media/storsimple-ova-deploy3-fs-setup/image16.png)

Les paramètres seront maintenant être mis à jour. Une fois les paramètres mis à jour, le bouton de finalisation de l'installation de l’appareil est grisé. Vous revenez à la page **Démarrage rapide** de l'appareil.

 ![](./media/storsimple-ova-deploy3-fs-setup/image17.png)


> [AZURE.NOTE]                                                              
>
> Vous pouvez modifier tous les autres paramètres de l’appareil à tout moment en accédant à la page **Configurer**.

## Étape 3 : Ajout d’un partage

Pour créer un partage, procédez comme suit dans le [portail Azure Classic](https://manage.windowsazure.com/).

#### Pour créer un partage

1.  Sur la page **Démarrage rapide** de l’appareil, cliquez sur **Ajouter un partage**. L’assistant Ajouter un partage se lance.

	![](./media/storsimple-ova-deploy3-fs-setup/image17.png)

1.  Dans la page **Paramètres de base**, procédez comme suit :

    1.  Spécifiez un nom unique pour votre partage. Le nom doit être une chaîne contenant entre 3 et 127 caractères.

    2.  (Facultatif) Fournissez une description du partage. La description permet d'identifier les propriétaires du partage.

    3.  Sélectionnez un type d'utilisation du partage. Le type d’utilisation peut être **À plusieurs niveaux** ou **Épinglé localement**, À plusieurs niveaux étant l’option par défaut. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un partage **épinglé localement**. Pour toutes les autres données, sélectionnez un partage **à plusieurs niveaux**.

	La configuration d’un partage épinglé localement est complète, et garantit que les données principales sur le partage sont conservées en local sur l’appareil et ne débordent pas sur le cloud. D’autre part, la configuration d’un partage à plusieurs niveaux est légère, et sa création peut être très rapide. Lorsque vous créez un partage à plusieurs niveaux, 10 % de l'espace sont configurés au niveau local et 90 % dans le cloud. Par exemple, si vous avez configuré un volume de 1 To, 100 Go résident dans l'espace local et 900 Go sont utilisés dans le cloud lorsque les données sont stockées en niveaux. Cela implique que si vous n'avez plus d'espace local sur l’appareil, vous ne pouvez pas configurer un partage à plusieurs niveaux.

1.  Indiquez la capacité allouée pour votre partage. Notez que la capacité spécifiée doit être inférieure à la capacité disponible. Si vous utilisez un partage à plusieurs niveaux, la taille du partage doit être comprise entre 500 Go et 20 To. Pour un partage épinglé localement, spécifiez une taille de partage comprise entre 50 Go et 2 To. Utilisez la capacité disponible comme guide pour configurer un partage. Si la capacité locale disponible est de 0 Go, vous ne pourrez pas configurer de partages locaux ou à plusieurs niveaux.

	![](./media/storsimple-ova-deploy3-fs-setup/image18.png)

1.  Cliquez sur l’icône en forme de flèche ![](./media/storsimple-ova-deploy3-fs-setup/image19.png) pour passer à la page suivante.

1.  Sur la page **Paramètres supplémentaires**, attribuez les autorisations à l'utilisateur ou au groupe qui aura accès à ce partage. Spécifiez le nom de l'utilisateur ou du groupe d'utilisateurs au format *<john@contoso.com>*. Nous vous recommandons d'utiliser un groupe d'utilisateurs (plutôt qu'un seul utilisateur) lorsque vous accordez des privilèges d'administrateur pour accéder à ces partages. Après avoir attribué ici les autorisations, vous pouvez ensuite utiliser l'Explorateur Windows pour modifier ces autorisations.

	![](./media/storsimple-ova-deploy3-fs-setup/image20.png)

1.  Cliquez sur l’icône en forme de coche ![](./media/storsimple-ova-deploy3-fs-setup/image21.png). Un partage est créé avec les paramètres spécifiés. Par défaut, la surveillance et la sauvegarde seront activées pour le partage.

## Étape 4 : Connexion au partage

Vous devrez maintenant vous connecter aux partages que vous avez créés à l'étape précédente. Procédez comme suit sur votre hôte Windows Server.

#### Pour vous connecter au partage

1.  Appuyez sur ![](./media/storsimple-ova-deploy3-fs-setup/image22.png) + R. Dans la fenêtre Exécuter, spécifiez *\<file server name>* comme chemin, en remplaçant *nom du serveur de fichiers* par le nom de l’appareil que vous avez affecté à votre serveur de fichiers. Cliquez sur **OK**.

	![](./media/storsimple-ova-deploy3-fs-setup/image23.png)

2.  L’Explorateur s'ouvre. Vous devriez maintenant voir les partages que vous avez créés sous forme de dossiers. Sélectionnez et double-cliquez sur un partage (dossier) pour afficher son contenu.

	![](./media/storsimple-ova-deploy3-fs-setup/image24.png)

3.  Vous pouvez maintenant ajouter des fichiers à ces partages et effectuer une sauvegarde.

![icône de vidéo](./media/storsimple-ova-deploy3-fs-setup/video_icon.png) **Vidéo disponible**

Regardez la vidéo pour découvrir comment configurer et inscrire StorSimple Virtual Array comme un serveur de fichiers.

> [AZURE.VIDEO configure-a-storsimple-virtual-array]

## Étapes suivantes

Découvrez comment utiliser l'interface utilisateur web locale pour [gérer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

<!---HONumber=AcomDC_0302_2016-->