<properties
   pageTitle="Présentation de l’équilibrage de charge Azure | Microsoft Azure"
   description="Présentation des fonctionnalités, de l'architecture et de l'implémentation de l'équilibrage de charge Azure. Il est utile de comprendre comment fonctionne l'équilibrage de charge et d'en tirer parti sur le cloud."
   services="load-balancer"
   documentationCenter="na"
   authors="joaoma"
   manager="adinah"
   editor="tysonn" />
<tags
   ms.service="load-balancer"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="12/09/2015"
   ms.author="joaoma" />


# Qu'est-ce que l'équilibrage de charge Azure ?

L'équilibrage de charge Azure offre une haute disponibilité et des performances réseau élevées pour vos applications. Il s'agit d'un équilibrage de charge Layer-4 (TCP, UDP) qui distribue le trafic entrant parmi les instances de service saines dans les services cloud ou les machines virtuelles définis dans un jeu d'équilibrage de la charge.

Il peut être configuré pour :

- équilibrer la charge du trafic Internet entrant sur les machines virtuelles. Nous appelons cela l'[équilibrage de charge accessible sur Internet](load-balancer-internet-overview.md).
- équilibrer le trafic entre des machines virtuelles dans un réseau virtuel, entre des machines virtuelles dans les services cloud ou entre des ordinateurs locaux et des machines virtuelles dans un réseau virtuel entre différents locaux. Nous appelons cela l'[équilibrage de charge interne](load-balancer-internal-overview.md).
- transférer du trafic externe vers une instance spécifique de machine virtuelle.

## Équilibrage de charge dans les deux modèles de déploiement

Toutes les ressources du cloud ont besoin d'une adresse IP publique pour être accessibles depuis Internet. L'infrastructure de cloud dans Microsoft Azure utilise des adresses IP non routables dans ses ressources. Elle utilise la traduction d'adresses réseau (NAT) avec des adresses IP publiques pour communiquer avec Internet.

### Portail Azure Classic

Dans le modèle de déploiement d'Azure Classic, une adresse IP publique et un nom de domaine complet sont affectés à un service cloud. Les machines virtuelles qui sont déployées dans une limite de service cloud peuvent être regroupées afin d'utiliser un équilibrage de charge. L'Équilibrage de charge Azure effectue une traduction de port et équilibre la charge du trafic réseau en tirant parti de l'adresse IP publique du service cloud.

Dans le modèle de déploiement classique, la traduction de port est effectuée à l'aide de points de terminaison qui constituent une relation un-à-un entre le port public affecté de l'adresse IP publique et le port local attribué pour envoyer le trafic vers une machine virtuelle spécifique.

L'équilibrage de charge est effectué à l'aide des points de terminaison du jeu de l'Équilibrage de charge. Ces points de terminaison constituent une relation un-à-plusieurs entre l'adresse IP publique et les ports locaux affectés à toutes les machines virtuelles du jeu qui répondent au trafic réseau à charge équilibrée.

Le nom de domaine de l'adresse IP publique que l'Équilibrage de charge doit utiliser dans ce modèle de déploiement est le suivant : `<cloud service name>.cloudapp.net`.

Il s'agit d'une représentation graphique de l'Équilibrage de charge dans un modèle de déploiement classique :

![L'équilibrage de charge dans le modèle de déploiement classique](./media/load-balancer-overview/asm-lb.png)

### Azure Resource Manager

Le concept d'Équilibreur de charge est différent dans le modèle de déploiement Azure Resource Manager, car aucun service cloud n'est nécessaire pour créer un équilibrage de charge.

Dans Resource Manager, une adresse IP publique est sa propre ressource et peut être associée à un nom de domaine ou un nom DNS. Dans ce cas, l'adresse IP publique est associée à la ressource d'équilibrage de charge. Par conséquent, les règles d'équilibrage de charge et les règles NAT entrantes utilisent l'adresse IP publique comme point de terminaison Internet pour les ressources recevant le trafic réseau à charge équilibrée.

Une ressource d'interface réseau (NIC) contient la configuration d'adresse IP (publique ou privée) d'une machine virtuelle. Lorsqu'une carte réseau est ajoutée au pool d'adresses IP principales de l'équilibrage de charge, ce dernier démarre l'envoi du trafic réseau à charge équilibrée selon les règles à charge équilibrée créées.

Il s'agit d'une représentation graphique d'un équilibrage de charge dans Azure Resource Manager :

![L'équilibrage de charge dans Resource Manager](./media/load-balancer-overview/arm-lb.png)

## Fonctionnalités d’équilibrage de charge

### Distribution basée sur le hachage

L'Équilibrage de charge Azure utilise un algorithme de distribution basé sur le hachage. Par défaut, il utilise un hachage à 5 tuples (adresse IP source, port source, adresse IP de destination, port de destination, type de protocole) pour mapper le trafic vers les serveurs disponibles. Il fournit l’adhérence uniquement dans une session de transport. Les paquets de la même session TCP ou UDP sont dirigés vers la même instance IP (DIP) de centre de données derrière le point de terminaison d'équilibrage de charge. Lorsque le client ferme et rouvre la connexion ou démarre une nouvelle session à partir de la même adresse IP source, le port source change. Cela peut pousser le trafic à accéder à un autre point de terminaison DIP.


Plus d'informations, consultez [Mode de distribution de l'équilibrage de charge](load-balancer-distribution-mode.md).

Ce graphique illustre une distribution basée sur hachage :

![Distribution basée sur le hachage](./media/load-balancer-overview/load-balancer-distribution.png)

### Réacheminement de port

L'équilibrage de charge Azure vous permet de contrôler la gestion des communications entrantes. Ces communications peuvent inclure le trafic initié par des hôtes Internet ou des machines virtuelles dans d'autres services cloud ou réseaux virtuels. Ce contrôle est représenté par un point de terminaison (également appelé point de terminaison d'entrée).

Un point de terminaison écoute sur un port public et transmet le trafic vers un port interne. Vous pouvez mapper les mêmes ports pour un point de terminaison interne ou externe, ou utiliser un port différent. Par exemple : vous pouvez avoir une écoute configurée du serveur Web sur le port 81 alors que le mappage de point de terminaison public est le port 80. La création d'un point de terminaison public déclenche la création d'une instance d'équilibrage de charge Azure.

Par défaut, les points de terminaison sur une machine virtuelle que vous créez via le portail Azure sont utilisés et configurés pour le trafic RDP (Remote Desktop Protocol) et de la session Windows PowerShell distante. Vous pouvez utiliser ces points de terminaison pour administrer à distance la machine virtuelle sur Internet.


### Reconfiguration automatique

L'équilibrage de charge Azure se reconfigure instantanément lors de la mise à l'échelle d'instances vers le haut ou vers le bas. Cette reconfiguration peut se produire, par exemple, lorsque vous augmentez le nombre d'instances pour le rôle web/de travail ou lorsque vous placez des machines virtuelles supplémentaires dans le même jeu à charge équilibrée.


### Surveillance des services
L'équilibrage de charge Azure offre la possibilité de sonder l'intégrité des différentes instances de serveur. Lorsqu'une sonde ne répond pas, l'équilibrage de charge n'envoie plus de nouvelles connexions aux instances défaillantes. Les connexions existantes ne sont pas concernées.

Trois types de sondes sont pris en charge :

- Sonde d'agent invité (sur des machines virtuelles PaaS uniquement). L'équilibrage de charge Azure utilise l'agent invité dans la machine virtuelle. Il écoute et répond avec une réponse HTTP 200 OK uniquement lorsque l'instance est prête (c'est-à-dire que l'instance n'est pas dans un état de type occupé, recyclage ou arrêt). Si l'agent invité ne répond pas avec HTTP 200 OK, l'équilibrage de charge Azure marque l'instance comme ne répondant pas et arrête d'envoyer du trafic vers cette instance. L'équilibrage de charge continue d'exécuter un test ping de l'instance. Si l'agent invité répond avec HTTP 200, l'équilibrage de charge envoie à nouveau du trafic vers cette instance. Lorsque vous utilisez un rôle web, le code de votre site web s'exécute généralement dans w3wp.exe, qui n'est pas surveillé par l'agent Azure Fabric ou l'agent invité. Cela signifie que les échecs dans w3wp.exe (par exemple, les réponses HTTP 500) ne seront pas signalés à l'agent invité et l'équilibrage de charge ne saura pas qu'il doit placer cette instance hors service.

- Sonde HTTP personnalisée. La sonde d'équilibrage de charge personnalisée remplace la sonde (agent invité) par défaut. Vous pouvez l'utiliser pour créer votre propre logique personnalisée pour déterminer l'état de l'instance de rôle. L'équilibrage de charge sonde régulièrement votre point de terminaison (toutes les 15 secondes, par défaut). L'instance est considérée comme en service si elle répond avec le code de statut HTTP 200 ou un paquet TCP ACK dans le délai imparti (31 secondes par défaut). Cela peut être utile pour implémenter votre propre logique pour supprimer des instances du service d'équilibrage de charge. Vous pouvez, par exemple, configurer l'instance pour qu'elle renvoie un état autre que 200 si l'instance a une utilisation supérieure à 90 % de l'UC. Pour les rôles web utilisant w3wp.exe, vous obtenez également une analyse automatique de votre site web, dans la mesure où les erreurs dans votre code de site web renvoient un état autre que 200 à la sonde de l'équilibrage de charge.

- Sonde TCP personnalisée. Les sondes TCP s’appuient sur l’établissement réussi d’une session TCP sur un port de sonde défini.

Pour plus d'informations, consultez [Sonde d'intégrité de l'équilibrage de charge](https://msdn.microsoft.com/library/azure/jj151530.aspx).

### Source NAT


Tout le trafic sortant vers Internet à partir de votre service d'origine passe par SNAT (Source NAT) avec la même adresse IP virtuelle que pour le trafic entrant. SNAT offre des avantages importants :

- il permet une mise à niveau et une récupération d'urgence simples des services, étant donné que l'adresse IP virtuelle peut être dynamiquement mappée à une autre instance du service ;

- il facilite la gestion de l'ACL puisqu'elle peut être exprimée en termes d'adresses IP virtuelles. Par conséquent, elle ne change pas lorsque les services sont redimensionnés ou redéployés.

La configuration de l'équilibrage de charge Azure prend en charge le NAT « plein cône » pour UDP. Le NAT« plein cône » est un type de NAT où le port autorise les connexions entrantes à partir de n’importe quel hôte externe (en réponse à une requête sortante).


>[AZURE.NOTE] Pour chaque nouvelle connexion sortante initiée par une machine virtuelle, un port sortant est également alloué par l'équilibrage de charge Azure. L'hôte externe voit le trafic entrant comme un port alloué d'adresse IP virtuelle. Si vous avez besoin d'un grand nombre de connexions sortantes, nous recommandons que les machines virtuelles utilisent des adresses IP publiques de niveau d’instance afin qu'elles disposent d'une adresse IP sortante dédiée pour SNAT. Cela réduit le risque d’épuisement du port.
>
>Le nombre maximal de ports pouvant être utilisés par l'adresse IP virtuelle ou l'adresse IP publique de niveau d'instance est 64 000. Il s'agit d'une limite TCP standard.


**Prise en charge de plusieurs adresses IP à équilibrage de charge pour les machines virtuelles**

Vous pouvez obtenir plusieurs adresses IP publiques à équilibrage de charge attribuées à un jeu de machines virtuelles. Cela vous permet d'héberger plusieurs sites Web SSL et/ou plusieurs écouteurs de groupe de disponibilité SQL Server Always On sur le même jeu de machines virtuelles. Pour plus d'informations, consultez [Plusieurs adresses IP virtuelles par service cloud](load-balancer-multivip.md).

**Déploiements basés sur modèle avec Azure Resource Manager**

Azure Resource Manager est la nouvelle infrastructure de gestion des services dans Azure. L'équilibrage de charge Azure peut maintenant être géré à l'aide des outils et API de Resource Manager. Pour en savoir plus sur Resource Manager, consultez [IaaS just got easier with Azure Resource Manager](https://azure.microsoft.com/blog/2015/04/29/iaas-just-got-easier-again/).


## Étapes suivantes

[Présentation de l'équilibrage de charge accessible sur Internet](load-balancer-internet-overview.md)

[Présentation de l’équilibrage de charge interne](load-balancer-internal-overview.md)

[Prise en main de la création d'un équilibreur de charge accessible sur Internet](load-balancer-internet-getstarted.md)

<!---HONumber=AcomDC_0128_2016-->