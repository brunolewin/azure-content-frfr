<properties
   pageTitle="Vue d'ensemble technique de Service Fabric | Microsoft Azure"
   description="Une vue d’ensemble technique de Service Fabric. Traite des concepts clés et présente l'architecture."
   services="service-fabric"
   documentationCenter=".net"
   authors="msfussell"
   manager="timlt"
   editor="chackdan;subramar"/>

<tags
   ms.service="service-fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="02/12/2016"
   ms.author="mfussell"/>

# Vue d'ensemble technique de Service Fabric

Service Fabric est une plateforme de systèmes distribués qui facilite le packaging, le déploiement et la gestion de microservices évolutifs et fiables.

## Principaux concepts en termes de terminologie
Cette section décrit en détail la terminologie utilisée dans Service Fabric afin que vous compreniez les termes utilisés dans la suite de la documentation.

**Cluster**: ensemble connecté de machines virtuelles ou physiques dans lequel les microservices sont déployés et gérés. Les clusters peuvent accepter des milliers de machines.

**Nœud**: machine ou machine virtuelle faisant partie d’un cluster. Un nom (chaîne) est affecté à chaque nœud. Les nœuds présentent des caractéristiques, telles que des propriétés de placement. Chaque machine ou machine virtuelle possède un service Windows à démarrage automatique, `FabricHost.exe`, qui commence à s’exécuter dès le démarrage, puis ce service démarre deux exécutables : `Fabric.exe` et `FabricGateway.exe`. Ces deux exécutables constituent le nœud. Pour les scénarios de test, vous pouvez héberger plusieurs nœuds sur un seul et même PC ou sur une seule et même machine virtuelle en exécutant plusieurs instances de `Fabric.exe` et `FabricGateway.exe`.

**Type d’application**: nom/version affectés à une collection de types de service. Ces informations sont définies dans un fichier `ApplicationManifest.xml`, incorporé à un répertoire de package d’application, qui est ensuite copié dans le magasin d’images du cluster Service Fabric. Vous pouvez ensuite créer une application nommée à partir de ce type d’application au sein du cluster.

Pour plus d’informations, consultez l’article [Modèle d’application](service-fabric-application-model.md).

**Package d’application**: répertoire de disque contenant le fichier `ApplicationManifest.xml` du type d’application. Ce fichier référence les packages de services pour chaque type de service qui constitue le type d’application. Les fichiers du répertoire de package d’application sont copiés dans le magasin d’images du cluster Service Fabric. Par exemple, un package d’un type d’application de messagerie peut contenir des références à un package de services de File d’attente, un package de services frontaux et un package de services de base de données.

**Application nommée**: une fois qu’un package d’application a été copié dans le magasin d’images, vous pouvez créer une instance de l’application au sein du cluster en spécifiant le type d’application du package d’application (à l’aide de son nom/version). Un nom d’URI est affecté à chaque instance de type d’application, qui ressemble à ceci : `"fabric:/MyNamedApp"`. Dans un cluster, vous pouvez créer plusieurs applications nommées à partir d’un seul type d’application. Vous pouvez également en créer à partir de différents types d’application. Chaque application nommée est gérée, et sa version est gérée indépendamment.

**Type de service**: nom/version affectés aux packages de code, packages de données et packages de configuration d’un service. Ces informations sont définies dans un fichier `ServiceManifest.xml`, incorporé à un répertoire de package de services, lequel est ensuite référencé par le fichier `ApplicationManifest.xml` d’un package d’application. Au sein du cluster, après avoir créé une application nommée, vous pouvez créer un service nommé à partir d’un des types de service du type d’application. Le fichier `ServiceManifest.xml` du type de service décrit le service.

Pour plus d’informations, consultez l’article [Modèle d’application](service-fabric-application-model.md).

Il existe deux types de service :

- **Sans état**: utilisez un service sans état si l’état persistant du service est stocké dans un service de stockage externe, par exemple Azure Storage, Base de données SQL Azure ou Azure DocumentDB. Vous devez également utiliser un service sans état si le service est totalement dépourvu de stockage persistant. Par exemple, pour un service de calculatrice où des valeurs sont transmises au service, un calcul est effectué à l’aide de ces valeurs, et un résultat est retourné.

- **Avec état **: utilisez un service avec état si vous souhaitez que Service Fabric gère l’état de votre service via ses modèles de programmation Collections fiables ou Reliable Actors. Lorsque vous créez un service nommé, vous spécifiez le nombre de partitions sur lesquelles vous souhaitez propager votre état (pour l’évolutivité) et vous indiquez le nombre de réplications de l’état dans les nœuds (pour la fiabilité). Chaque service nommé possède un seul réplica principal et plusieurs réplicas secondaires. Vous modifiez l’état du service nommé en écrivant dans le réplica principal. Service Fabric réplique ensuite cet état vers tous les réplicas secondaires conservant ainsi la synchronisation de l’état. En cas d’échec d’un réplica principal, Service Fabric le détecte automatiquement, promeut un réplica secondaire existant en réplica principal, puis crée un nouveau réplica secondaire.

**Package de services**: répertoire de disque contenant le fichier `ServiceManifest.xml` du type de service. Ce fichier référence le code, les données statiques et les packages de configuration correspondant au type de service. Les fichiers contenus dans le répertoire de package de services sont référencés par le fichier `ApplicationManifest.xml` du type d’application. Par exemple, un package de services peut faire référence au code, aux données statiques et aux packages de configuration qui composent un service de base de données.

**Service nommé**: après avoir créé une application nommée, vous pouvez créer une instance de l’un de ses types de service au sein du cluster en spécifiant le type de service (à l’aide de son nom/version). Chaque instance du type de service reçoit un nom d’URI inclus dans l’étendue de l’URI de son application nommée. Par exemple, si vous créez un service nommé « MyDatabase » dans une application nommée « MyNamedApp », l’URI ressemble à ceci : `"fabric:/MyNamedApp/MyDatabase"`. Dans une application nommée, vous pouvez créer plusieurs services nommés. Chaque service nommé peut posséder son propre schéma de partition et son propre nombre d’instances/réplicas.

**Package de code**: répertoire de disque contenant les fichiers exécutables du type de service (généralement des fichiers DLL/EXE). Les fichiers contenus dans le répertoire de package de code sont référencés par le fichier `ServiceManifest.xml` du type de service. Lorsqu’un service nommé est créé, les fichiers du package de code sont copiés vers les nœuds sélectionnés par Service Fabric pour exécuter le service nommé, puis l’exécution du code commence. Il existe deux types d’exécutable de code de package :

- **Exécutables invités**: exécutables qui s’exécutent tels quels sur le système d’exploitation hôte (Windows ou Linux). Autrement dit, ces exécutables ne sont pas liés ou ne font pas référence aux fichiers exécutables de Service Fabric. Par conséquent, ils n’utilisent pas les modèles de programmation de Service Fabric. Ces exécutables ne peuvent pas tirer parti de certaines fonctionnalités de Service Fabric telles que le service d’affectation de noms pour la découverte de point de terminaison et ils ne peuvent pas indiquer les mesures de chargement propres à chaque instance de service.

- **Exécutables d’hôte de service**: exécutables qui utilisent les modèles de programmation de Service Fabric en les liant aux fichiers exécutables de Service Fabric. Ce faisant, des parties du code de l’exécutable sont liées à Service Fabric, ce qui active des fonctionnalités supplémentaires. Par exemple, une instance de service nommé peut inscrire les points de terminaison avec le service d’affectation de noms de Service Fabric et indiquer les mesures de chargement.

**Package de données**: répertoire de disque contenant les fichiers de données en lecture seule, statiques du type de service (en général, des fichiers audio et vidéo et des fichiers de photos). Les fichiers contenus dans le répertoire de package de données sont référencés par le fichier `ServiceManifest.xml` du type de service. Lorsqu’un service nommé est créé, les fichiers du package de données sont copiés vers les nœuds sélectionnés par Service Fabric pour exécuter le service nommé, puis l’exécution du code commence. Le code peut maintenant accéder aux fichiers de données.

**Package de configuration**: répertoire de disque contenant les fichiers de configuration en lecture seule, statiques du type de service (en général, des fichiers texte). Les fichiers contenus dans le répertoire de package de configuration sont référencés par le fichier `ServiceManifest.xml` du type de service. Lorsqu’un service nommé est créé, les fichiers du package de configuration sont copiés vers les nœuds sélectionnés par Service Fabric pour exécuter le service nommé, puis l’exécution du code commence. Le code peut maintenant accéder aux fichiers de configuration.

**Magasin d’images**: chaque cluster Service Fabric gère un magasin d’images. Vous devez copier le contenu d’un package d’application dans le magasin d’images, puis inscrire le type d’application dans ce package d’application. Une fois le type d’application configuré, vous pouvez créer des applications nommées à partir de celui-ci. Vous pouvez annuler l’inscription d’un type d’application dans le magasin d’images uniquement après que toutes ses applications nommées ont été supprimées.

Pour plus d’informations sur le déploiement vers le magasin d’images, consultez l’article [Déployer une application](service-fabric-deploy-remove-applications.md).

**Schéma de partition**: lors de la création d’un service nommé, vous devez spécifier un schéma de partition. Les services comportant de grandes quantités d’état fractionnent les données entre les partitions, ce qui les répartit entre les nœuds du cluster. Cela permet l’évolutivité de l’état de votre service nommé. Dans une partition, les services nommés sans état disposent d’instances tandis que les services nommés avec état possèdent des réplicas. En règle générale, les services nommés sans état ne possèdent qu’une partition, car ils sont dépourvus d’état interne. Les instances de partition assurent la disponibilité. En cas d’échec d’une instance, les autres instances continuent de fonctionner normalement, puis Service Fabric en crée une. Les services nommés avec état conservent leur état dans les réplicas, et chaque partition possède son propre jeu de réplicas avec tous les états synchronisés. En cas d’échec d’un réplica, Service Fabric en génère un nouveau à partir des réplicas existants.

Pour plus d’informations, consultez l’article [Partitionnement des services fiables Service Fabric](service-fabric-concepts-partitioning.md).

**Modèles de programmation**: deux modèles de programmation .NET Framework vous permettent de générer des services Service Fabric :

- Reliable Services : API permettant de générer des services avec et sans état. Les services avec état stockent leur état dans Collections fiables (par exemple, un dictionnaire ou une file d’attente). Vous pouvez également accéder à diverses piles de communication comme l’API web et WCF (Windows Communication Foundation).

- Reliable Actors : API permettant de générer des objets avec et sans état via le modèle de programmation Actor virtuel. Ce modèle peut être utile si vous avez un grand nombre d’unités indépendantes d’état/de calcul. Comme ce modèle utilise un modèle de thread en alternance, il convient d’éviter un code qui appelle d’autres acteurs ou services dans la mesure où un acteur individuel ne peut pas traiter les autres demandes entrantes tant que toutes ses demandes sortantes ne sont pas terminées.

Pour plus d’informations, consultez l’article [Choisir un modèle de programmation pour votre service](service-fabric-choose-framework.md).

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## Étapes suivantes
Pour en savoir plus sur Service Fabric

- [Vue d'ensemble de Service Fabric](service-fabric-overview.md)
- [Pourquoi une approche de microservices pour la conception d’applications ?](service-fabric-overview-microservices.md)
- [Scénarios d’application](service-fabric-application-scenarios.md)

<!---HONumber=AcomDC_0224_2016-->