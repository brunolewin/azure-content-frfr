<properties
   pageTitle="Vue d’ensemble de la configuration Azure Service Fabric Reliable Actors ReliableDictionaryActorStateProvider | Microsoft Azure"
   description="Découvrez comment configurer les acteurs avec état Azure Service Fabric de type ReliableDictionaryActorStateProvider."
   services="Service-Fabric"
   documentationCenter=".net"
   authors="sumukhs"
   manager="timlt"
   editor=""/>

<tags
   ms.service="Service-Fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="01/26/2016"
   ms.author="sumukhs"/>

# Configuration de Reliable Actors - ReliableDictionaryActorStateProvider
Vous pouvez modifier la configuration par défaut de ReliableDictionaryActorStateProvider en modifiant le fichier settings.xml généré dans la racine du package Visual Studio sous le dossier Config de l’acteur spécifié.

Le runtime Azure Service Fabric recherche des noms de sections prédéfinis dans le fichier settings.xml et utilise les valeurs de configuration pendant la création des composants runtime sous-jacents.

>[AZURE.NOTE] Veillez à **ne pas** supprimer ou modifier les noms de sections des configurations suivantes dans le fichier settings.xml généré dans la solution Visual Studio.

## Configuration de la sécurité du réplicateur
Les configurations de sécurité du réplicateur sont utilisées pour sécuriser le canal de communication utilisé pendant la réplication. Un service ne peut donc pas afficher le trafic de réplication d’un autre service, ce qui garantit la sécurité des données rendues hautement disponibles. Par défaut, une section de configuration de sécurité vide empêche de sécuriser la réplication.

### Nom de la section
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## Configuration du réplicateur
Les configurations de réplicateur servent à configurer le réplicateur en charge de la haute fiabilité de l’état du fournisseur d’état d’acteur par la réplication et la persistance de l’état au niveau local. La configuration par défaut est générée par le modèle Visual Studio et devrait suffire. Cette section décrit les configurations supplémentaires disponibles pour paramétrer le réplicateur.

### Nom de la section
&lt;ActorName&gt;ServiceReplicatorConfig

### Noms des configurations

|Nom|Unité|Valeur par défaut|Remarques|
|----|----|-------------|-------|
|BatchAcknowledgementInterval|Secondes|0,05|Durée d'attente du réplicateur secondaire après la réception d'une opération et avant de renvoyer un accusé de réception au réplicateur principal. Tous les autres accusés de réception à envoyer pour les opérations traitées durant cet intervalle sont envoyés sous la forme d'une réponse.||
|ReplicatorEndpoint|N/A|Aucune valeur par défaut (paramètre obligatoire)|Adresse IP et port que le réplicateur principal/secondaire utilise pour communiquer avec d'autres réplicateurs dans le jeu de réplicas. Doit faire référence à un point de terminaison de ressource TCP dans le manifeste de service. Pour en savoir plus sur la définition de ressources de point de terminaison dans le manifeste de service, consultez [Ressources du manifeste de service](service-fabric-service-manifest-resources.md). |
|MaxReplicationMessageSize|Octets|50 Mo|Taille maximale des données de réplication pouvant être transmises dans un même message.|
|MaxPrimaryReplicationQueueSize|Nombre d'opérations|8 192|Nombre maximal d'opérations dans la file d'attente principale. Une opération est libérée quand le réplicateur principal reçoit un accusé de réception de tous les réplicateurs secondaires. Cette valeur doit être supérieure à 64 et être une puissance de 2.|
|MaxSecondaryReplicationQueueSize|Nombre d'opérations|16 384|Nombre maximal d'opérations dans la file d'attente secondaire. Une opération est libérée une fois son état devenu hautement disponible grâce à la persistance. Cette valeur doit être supérieure à 64 et être une puissance de 2.|
|CheckpointThresholdInMB|Mo|200|Quantité d'espace du fichier journal après lequel l'état est vérifié.|
|MaxRecordSizeInKB|Ko|1024|Taille maximale de l'enregistrement que le réplicateur peut écrire dans le journal. Cette valeur doit être un multiple de 4 et supérieure à 16.|
|OptimizeLogForLowerDiskUsage|Boolean|true|Si la valeur est true, le journal est configuré de sorte que le fichier journal dédié au réplica est créé à l’aide d’un fichier partiellement alloué NTFS. Cela réduit l'utilisation d'espace disque réel du fichier. Si la valeur est false, le fichier est créé avec des allocations fixes qui offrent les meilleures performances en écriture.|
|SharedLogId|guid|""|Spécifie une valeur guid unique à utiliser pour identifier le fichier journal partagé utilisé avec ce réplica. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogId est spécifié, SharedLogPath doit l'être aussi.|
|SharedLogPath|Nom de chemin complet|""|Spécifie le chemin d'accès complet où sera créé le fichier journal partagé pour ce réplica. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogPath est spécifié, SharedLogId doit l’être aussi.|


## Exemple de fichier de configuration

```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## Remarques
Le paramètre BatchAcknowledgementInterval contrôle la latence de la réplication. La valeur « 0 » entraîne la latence la plus faible possible, au détriment du débit (car davantage de messages d'accusé de réception doivent être envoyés et traités, chacun contenant moins d'accusés de réception). Plus la valeur de BatchAcknowledgementInterval est élevée, plus le débit de réplication général est élevé, au détriment d'une plus grande latence de l'opération. Cela se traduit directement par une latence dans la validation des transactions.

Le paramètre CheckpointThresholdInMB contrôle la quantité d’espace disque que le réplicateur peut utiliser pour stocker des informations d’état dans le fichier journal dédié au réplica. Son augmentation pour une valeur supérieure à celle par défaut peut entraîner des temps de reconfiguration plus rapides quand un nouveau réplica est ajouté à l’ensemble. Cela est dû au transfert d'état partiel qui intervient suite à la disponibilité d'un historique des opérations plus important dans le journal. Cela peut potentiellement accroître le temps de récupération d’un réplica après un blocage.

Si vous affectez à OptimizeForLowerDiskUsage la valeur true, l’espace du fichier journal est surapprovisionné. Les réplicas actifs peuvent ainsi stocker davantage d’informations d’état dans leurs fichiers journaux, tandis que les réplicas inactifs utilisent moins d’espace disque. Il est donc possible d’héberger davantage de réplicas sur un nœud. Si vous affectez à OptimizeForLowerDiskUsage la valeur false, les informations d’état sont écrites dans les fichiers journaux plus rapidement.

Le paramètre MaxRecordSizeInKB définit la taille maximale d’un enregistrement que le réplicateur peut écrire dans le fichier journal. Dans la plupart des cas, la taille d’enregistrement par défaut de 1 024 Ko est optimale. Toutefois, si le service ajoute des données plus volumineuses aux informations d’état, cette valeur devra éventuellement être augmentée. Il n’est pas recommandé de choisir une valeur MaxRecordSizeInKB inférieure à 1 024 Ko, car des enregistrements plus petits utilisent uniquement l’espace nécessaire à l’enregistrement le plus petit. Cette valeur ne doit être modifiée qu’en de rares occasions.

Les paramètres SharedLogId et SharedLogPath sont toujours utilisés ensemble pour permettre à un service d’utiliser un journal partagé distinct du journal partagé par défaut pour le nœud. Pour plus d'efficacité, vous devriez spécifier autant de services que possible dans le même journal partagé. Les fichiers journaux partagés doivent être placés sur des disques uniquement utilisés pour le fichier journal partagé afin de réduire la contention des mouvements de la tête. Ces valeurs ne doivent être modifiées qu’en de rares occasions.

<!---HONumber=AcomDC_0204_2016-->