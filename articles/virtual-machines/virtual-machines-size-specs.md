<properties
 pageTitle="Tailles des machines virtuelles | Microsoft Azure"
 description="Répertorie les différentes tailles de machines virtuelles et leurs capacités."
 services="virtual-machines"
 documentationCenter=""
 authors="cynthn"
 manager="timlt"
 editor=""
 tags="azure-resource-manager,azure-service-management"/>

<tags
ms.service="virtual-machines"
 ms.devlang="na"
 ms.topic="article"
 ms.tgt_pltfrm="vm-multiple"
 ms.workload="infrastructure-services"
 ms.date="01/05/2016"
 ms.author="cynthn"/>

# Tailles de machines virtuelles

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## Vue d'ensemble

Cet article décrit les tailles et options disponibles pour les ressources de calcul des machines virtuelles que vous pouvez utiliser pour exécuter vos applications et charges de travail. Il expose également les points à prendre en considération pour le déploiement quand vous planifiez l’utilisation de ces ressources. Pour plus d'informations sur la tarification des différentes tailles, consultez [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).

Pour connaître les limites générales des machines virtuelles Azure, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).

Les tailles standard sont constituées de plusieurs séries : A, D, DS, G et GS. Voici des considérations quant à certaines de ces tailles :

*   Les machines virtuelles de la série D sont conçues pour exécuter des applications qui nécessitent une puissance de calcul et des performances de disque temporaire supérieures. Ces machines virtuelles se caractérisent par des processeurs plus rapides, un rapport mémoire-cœur plus élevé et un disque SSD pour le disque temporaire. Pour plus d’informations, voir l’annonce suivante sur le blog Azure : [Nouvelles tailles de machines virtuelles de la série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/) (en anglais).

*   La série Dv2, suite de la série D d’origine, comprend un processeur plus puissant. Le processeur de la série Dv2 est environ 35 % plus rapide que le processeur de la série D. Il est basé sur la dernière génération de processeur 2,4 GHz Intel Xeon® E5-2673 v3 (Haswell) et comporte la technologie 2.0 Intel Turbo Boost, et peut atteindre 3,2 GHz. La série Dv2 a les mêmes configurations de disque et de mémoire que la série D.

*   Les machines virtuelles de la série G offrent le plus de mémoire et s’exécutent sur des hôtes équipés de processeurs de la famille Intel Xeon E5 V3.

*   Les machines virtuelles de la série DS et GS peuvent utiliser un stockage Premium, qui offre un stockage hautes performances à faible latence pour les charges de travail impliquant des E/S intensives. Ces machines virtuelles utilisent des disques SSD pour héberger les disques de la machine virtuelle et offrent également un cache de disque SSD local. Le stockage Premium est disponible dans certaines régions. Pour plus d’informations, consultez l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../storage/storage-premium-storage.md).

*   Les machines virtuelles de la série A peuvent être déployées sur différents types de matériels et processeurs. La taille est limitée, en fonction du matériel, pour offrir des performances de processeur cohérentes pour l’instance en cours d’exécution, quel que soit le matériel sur lequel elle est déployée. Pour déterminer le matériel physique sur lequel cette taille est déployée, interrogez le matériel virtuel à partir de la machine virtuelle.

*   La taille A0 est trop sollicitée sur le matériel physique. Pour cette taille spécifique uniquement, les autres déploiements de clients peuvent affecter les performances de la charge de travail en cours d’exécution. Les performances relatives sont décrites ci-dessous comme référence attendue, soumises à une variation approximative de 15 pour cent.

La taille de la machine virtuelle a une incidence sur la tarification. La taille influe également sur les capacités de traitement, de mémoire et de stockage de la machine virtuelle. Les coûts de stockage sont calculés séparément en fonction des pages utilisées dans le compte de stockage. Pour plus d’informations, voir les pages [Machines virtuelles Tarification](https://azure.microsoft.com/pricing/details/virtual-machines/) et [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/). Pour plus d’informations sur le stockage pour les machines virtuelles, consultez [À propos des disques et des disques durs virtuels pour les machines virtuelles](virtual-machines-disks-vhds.md).

Les considérations ci-dessous peuvent vous aider à choisir une taille :


* Les tailles A8 à A11 sont également connues comme étant des *instances nécessitant beaucoup de ressources système*. Le matériel qui exécute ces tailles a été conçu et optimisé pour les applications nécessitant beaucoup de ressources système et réseau, notamment les applications en cluster pour des calculs complexes, la modélisation et les simulations. Pour plus d’informations et pour connaître les éléments à prendre en considération sur l’utilisation de ces tailles, consultez l’article [À propos des instances de calcul intensif A8, A9, A10 et A11](virtual-machines-a8-a9-a10-a11-specs.md).


*	Les séries Dv2, D, G et DS/GS sont idéales pour les applications qui exigent des processeurs plus rapides, de meilleures performances de disque local, ou qui ont des exigences de mémoire plus élevées. Elles offrent une combinaison puissante pour de nombreuses applications professionnelles.

*   Certains hôtes physiques des centres de données Azure ne prennent pas en charge les tailles de machines virtuelles élevées, comme A5 à A11. Ainsi, vous pouvez obtenir le message d’erreur **Échec de la configuration de la machine virtuelle <machine name>** ou **Échec de la création de la machine virtuelle <machine name>** pendant le redimensionnement d’une machine virtuelle existante, la création d’une machine virtuelle dans un réseau virtuel créé avant le 16 avril 2013 ou l’ajout d’une machine virtuelle à un service cloud existant. Pour découvrir les solutions de contournement pour chaque scénario de déploiement, consultez [Erreur : « Échec de la configuration de la machine virtuelle »](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) (en anglais) sur le forum d'assistance.


## Considérations relatives aux performances

Nous avons créé le concept d’unité de calcul Azure (ACU) pour permettre de comparer les performances de calcul (UC) des références Azure. Cela vous aidera à identifier facilement la référence la plus à même de répondre à vos besoins en termes de performances. L’unité ACU est actuellement normalisée sur une machine virtuelle de petite taille (Standard\_A1) correspondant à 100, et toutes les autres références représentent ensuite approximativement la rapidité avec laquelle la référence en question peut exécuter un test d’évaluation.

>[AZURE.IMPORTANT] Cette unité ACU est fournie uniquement à titre indicatif. Les résultats de votre charge de travail peuvent varier.

<br>

|Famille de références |ACU/Cœur |
|---|---|
|[Standard\_A0 (très petite)](#standard-tier-a-series) |50 |
|[Standard\_A1-4 (petite à grande)](#standard-tier-a-series) |100 |
|[Standard\_A5-7](#standard-tier-a-series) |100 |
|[A8-A11](#standard-tier-a-series) |225 *|
|[D1-14](#standard-tier-d-series) |160 |
|[D1-14v2](#standard-tier-dv2-series) |210 - 250 *|
|[DS1-14](#standard-tier-ds-series) |160 |
|[G1-5](#standard-tier-g-series) |180 - 240 *|
|[GS1-5](#standard-tier-gs-series) |180 - 240 *|


Les unités ACU signalées par un astérisque (*) utilisent la technologie Intel ® Turbo pour augmenter la fréquence du processeur et améliorer les performances. Cette amélioration des performances peut varier en fonction de la taille et de la charge de travail de la machine virtuelle, et des autres charges de travail en cours d’exécution sur le même hôte.



## Tableaux des tailles

Les tableaux ci-après indiquent les tailles et les capacités qu’elles offrent.

>[AZURE.NOTE] La capacité de stockage est représentée avec 1024^3 octets comme unité de mesure pour les Go. Cette unité est parfois appelée gibioctet ou définition en base 2. Quand vous comparez des tailles qui utilisent des systèmes en base différente, n’oubliez pas que les tailles en base 2 peuvent paraître plus petites que celles en base 10, mais que pour une taille spécifique (par exemple, 1 Go), un système en base 2 offre une capacité plus élevée qu’un système en base 10, car 1 024^3 est supérieur à 1 000^3.

<br>



## Niveau standard : série A

Dans le modèle de déploiement classique, certaines tailles de machines virtuelles sont légèrement différentes dans Powershell et l'interface de ligne de commande.

* Standard\_A0 est ExtraSmall (Très petit) 
* Standard\_A1 est Small (Petit)
* Standard\_A2 est Medium (Moyen)
* Standard\_A3 est Large (Grand)
* Standard\_A4 est ExtraLarge (Très grand)

<br>

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (500 par disque)|
|---|---|---|---|---|---|---|
|Standard\_A0\\ExtraSmall |1|768 Mo|1| Temporaire = 20 Go |1|1 x 500|
|Standard\_A1\\Small|1|1,75 Go|1|Temporaire = 70 Go |2|2 x 500|
|Standard\_A2\\Medium|2|3,5 Go|1|Temporaire = 135 Go |4|4 x 500|
|Standard\_A3\\Large|4|7 Go|2|Temporaire = 285 Go |8|8 x 500|
|Standard\_A4\\ExtraLarge|8|14 Go|4|Temporaire = 605 Go |16|16 x 500|
|Standard\_A5|2|14 Go|1|Temporaire = 135 Go |4|4 x 500|
|Standard\_A6|4|28 Go|2|Temporaire = 285 Go |8|8 x 500|
|Standard\_A7|8|56 Go|4|Temporaire = 605 Go |16|16 x 500|


## Niveau standard : série A : instances nécessitant beaucoup de ressources système

Remarque : pour plus d’informations et pour connaître les éléments à prendre en considération sur l’utilisation de ces tailles, consultez l’article [À propos des instances de calcul intensif A8, A9, A10 et A11](virtual-machines-a8-a9-a10-a11-specs.md).

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (500 par disque)|
|---|---|---|---|---|---|---|
|Standard\_A8|8|56 Go|2| Temporaire = 382 Go |16|16 x 500|
|Standard\_A9|16|112 Go|4| Temporaire = 382 Go |16|16 x 500|
|Standard\_A10|8|56 Go|2| Temporaire = 382 Go |16|16 x 500|
|Standard\_A11|16|112 Go|4| Temporaire = 382 Go |16|16 x 500|

## Niveau standard : série D

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (500 par disque)|
|---|---|---|---|---|---|---|
|D1 standard |1|3,5 Go|1|Temporaire (SSD) = 50 Go |2|2 x 500|
|D2 standard |2|7 Go|2|Temporaire (SSD) = 100 Go |4|4 x 500|
|D3 standard |4|14 Go|4|Temporaire (SSD) = 200 Go |8|8 x 500|
|D4 standard |8|28 Go|8|Temporaire (SSD) = 400 Go |16|16 x 500|
|D11 standard |2|14 Go|2|Temporaire (SSD) = 100 Go |4|4 x 500|
|D12 standard |4|28 Go|4|Temporaire (SSD) = 200 Go |8|8 x 500|
|D13 standard |8|56 Go|8|Temporaire (SSD) = 400 Go |16|16 x 500|
|D14 standard |16|112 Go|8|Temporaire (SSD) = 800 Go |32|32 x 500|

## Niveau standard : série Dv2

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (500 par disque)|
|---|---|---|---|---|---|---|
|Standard\_D1\_v2 |1|3,5 Go|1|Temporaire (SSD) = 50 Go |2|2 x 500|
|Standard\_D2\_v2 |2|7 Go|2|Temporaire (SSD) = 100 Go |4|4 x 500|
|Standard\_D3\_v2 |4|14 Go|4|Temporaire (SSD) = 200 Go |8|8 x 500|
|Standard\_D4\_v2 |8|28 Go|8|Temporaire (SSD) = 400 Go |16|16 x 500|
|Standard\_D5\_v2 |16|56 Go|8|Temporaire (SSD) = 800 Go |32|32 x 500|
|Standard\_D11\_v2 |2|14 Go|2|Temporaire (SSD) = 100 Go |4|4 x 500|
|Standard\_D12\_v2 |4|28 Go|4|Temporaire (SSD) = 200 Go |8|8 x 500|
|Standard\_D13\_v2 |8|56 Go|8|Temporaire (SSD) = 400 Go |16|16 x 500|
|Standard\_D14\_v2 |16|112 Go|8|Temporaire (SSD) = 800 Go |32|32 x 500|

## Niveau standard : série DS*

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Taille de cache (Go)|Nombre maximal d’opérations d’E/S par seconde du disque et bande passante|
|---|---|---|---|---|---|---|---|
|Standard\_DS1 |1|3,5|1|Disque SSD local = 7 Go |2|43| 3 200 32 Mo par seconde |
|Standard\_DS2 |2|7|2|Disque SSD local = 14 Go |4|86| 6 400 64 Mo par seconde |
|Standard\_DS3 |4|14|4|Disque SSD local = 28 Go |8|172| 12 800 128 Mo par seconde |
|Standard\_DS4 |8|28|8|Disque SSD local = 56 Go |16|344| 25 600 256 Mo par seconde |
|Standard\_DS11 |2|14|2|Disque SSD local = 28 Go |4|72| 6 400 64 Mo par seconde |
|Standard\_DS12 |4|28|4|Disque SSD local = 56 Go |8|144| 12 800 128 Mo par seconde |
|Standard\_DS13 |8|56|8|Disque SSD local = 112 Go |16|288| 25 600 256 Mo par seconde |
|Standard\_DS14 |16|112|8|Disque SSD local = 224 Go |32|576| 50 000 512 Mo par seconde |

** Le nombre maximal d’opérations d’entrée/sortie par seconde (IOPS) et le débit (bande passante) possibles avec une machine virtuelle de la série DS sont affectés par la taille du disque. Pour plus d'informations, consultez [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../storage/storage-premium-storage.md).

## Niveau standard : série G

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (500 par disque)|
|---|---|---|---|---|---|---|
|Standard\_G1 |2|28 Go|1|Disque SSD local = 384 Go |4|4 x 500|
|Standard\_G2 |4|56 Go|2|Disque SSD local = 768 Go |8|8 x 500|
|Standard\_G3 |8|112 Go|4|Disque SSD local = 1 536 Go |16|16 x 500|
|Standard\_G4 |16|224 Go|8|Disque SSD local = 3 072 Go |32|32 x 500|
|Standard\_G5 |32|448 Go|8|Disque SSD local = 6 144 Go |64| 64 x 500 |

## Niveau standard : série GS

|Taille |Cœurs d’unité centrale|Mémoire|Cartes réseau (max)|Taille maximale du disque|Nombre maximal de disques de données (1 023 Go chacun)|Taille de cache (Go)|Nombre maximal d’opérations d’E/S par seconde du disque et bande passante|
|---|---|---|---|---|---|---|---|
|Standard\_GS1|2|28|1|Disque SSD local = 56 Go |4|264| 5 000 125 Mo par seconde |
|Standard\_GS2|4|56|2|Disque SSD local = 112 Go |8|528| 10 000 250 Mo par seconde |
|Standard\_GS3|8|112|4|Disque SSD local = 224 Go |16|1 056| 20 000 500 Mo par seconde |
|Standard\_GS4|16|224|8|Disque SSD local = 448 Go |32|2 112| 40 000 1 000 Mo par seconde |
|Standard\_GS5|32|448|8|Disque SSD local = 896 Go |64|4 224| 80 000 2 000 Mo par seconde |


### Voir aussi

[Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md)

[À propos des instances de calcul intensif A8, A9, A10 et A11](virtual-machines-a8-a9-a10-a11-specs.md)

<!---HONumber=AcomDC_0302_2016-->