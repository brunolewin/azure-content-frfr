<properties 
   pageTitle="Créer un équilibreur de charge interne dans Resource Manager à l’aide de l’interface de ligne de commande (CLI) Azure | Microsoft Azure"
   description="Découvrez comment créer un équilibreur de charge interne dans Resource Manager à l’aide de l’interface de ligne de commande (CLI) Azure"
   services="load-balancer"
   documentationCenter="na"
   authors="joaoma"
   manager="carolz"
   editor=""
   tags="azure-resource-manager"
/>
<tags  
   ms.service="load-balancer"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="02/09/2016"
   ms.author="joaoma" />

# Créer un équilibreur de charge interne à l’aide de l’interface de ligne de commande (CLI) Azure

[AZURE.INCLUDE [load-balancer-get-started-ilb-arm-selectors-include.md](../../includes/load-balancer-get-started-ilb-arm-selectors-include.md)]<BR>[AZURE.INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

[AZURE.INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)] [Modèle de déploiement classique](load-balancer-get-started-ilb-classic-cli.md).

[AZURE.INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## Ce qui est nécessaire pour créer un équilibrage de charge interne

Vous devez créer et configurer les objets suivants pour déployer un équilibreur de charge :

- Configuration d’adresses IP frontales : configure l'adresse IP privée pour le trafic réseau entrant. 

- Pool d’adresses principales : contient des interfaces réseau (NIC) pour recevoir le trafic de l’équilibreur de charge.

- Règles d'équilibrage de charge - contient des règles de mappage d'un port de trafic réseau entrant vers un port recevant le trafic réseau dans le pool principal.

- Règles NAT entrantes : contient des règles de mappage d’un port public situé sur l’équilibreur de charge vers le port d’une machine virtuelle spécifique située dans le pool d’adresses principales.

- Sondes : contient les sondes d’intégrité utilisées pour vérifier la disponibilité des machines virtuelles associées au pool d’adresses principales.

Pour obtenir plus d’informations sur les composants de l’équilibrage de charge avec Azure Resource Manager, consultez la page [Support Azure Resource Manager pour l’équilibrage de charge](load-balancer-arm.md).

## Configurer l’interface de ligne de commande pour utiliser le gestionnaire de ressources

1. Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installation et configuration de l’interface de ligne de commande Azure](xplat-cli.md) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.

2. Exécutez la commande **azure config mode** pour passer en mode Resource Manager, comme illustré ci-dessous.

		azure config mode arm

	Sortie attendue :

		info:    New mode is arm

## Créer par étapes un équilibreur de charge interne 

Les étapes suivantes créeront un équilibreur de charge interne selon le scénario ci-dessus :

### Étape 1 

Le cas échéant, téléchargez la dernière version de l’[interface de ligne de commande Azure](https://azure.microsoft.com/downloads/).

### Étape 2 : 

Après l’installation, authentifiez votre compte.

	azure login

Le processus d'authentification vous demandera vos nom d’utilisateur et mot de passe pour votre abonnement Azure.

### Étape 3

Remplacez les outils de commande par le mode Azure Resource Manager.

	azure config mode arm

## Créer un groupe de ressources

Toutes les ressources d’Azure Resource Manager sont associées à un groupe de ressources. Le cas échéant, créez un groupe de ressources.

	azure group create <resource group name> <location>


## Créer un jeu d’équilibrage de charge interne 


### Étape 1 

Créez un jeu d’équilibrage de charge interne à l’aide de la commande `azure network lb create`. Dans le scénario suivant, un groupe de ressources nommé nrprg est créé dans la région Est des États-Unis.
 	
	azure network lb create -n nrprg -l westus

>[AZURE.NOTE] Toutes les ressources d'un équilibreur de charge interne, telles que le réseau virtuel et le sous-réseau du réseau virtuel doivent figurer dans le même groupe de ressources et dans la même région.


### Étape 2 

Créez une adresse IP frontale pour l'équilibrage de charge interne. L'adresse IP utilisée doit se trouver dans la plage de sous-réseau de votre réseau virtuel.

	
	azure network lb frontend-ip create -g nrprg -l ilbset -n feilb -a 10.0.0.7 -e nrpvnetsubnet -m nrpvnet

Paramètres utilisés :

**-g** - groupe de ressources **-l** - nom du jeu d’équilibrage de charge interne **-n** - nom de l’adresse IP frontale **-a** - adresse IP privée dans la plage de sous-réseau. **-e** - nom du sous-réseau **-m** - nom du réseau virtuel

### Étape 3 

Créez le pool d'adresses principales.

	azure network lb address-pool create -g nrprg -l ilbset -n beilb

Paramètres utilisés :

**-g** - groupe de ressources **-l** - nom du jeu d’équilibrage de charge interne **-n** - nom du pool d’adresses principales

Après avoir défini une adresse IP frontale et un pool d'adresses principales, vous pouvez créer des règles d'équilibreur de charge, des règles NAT entrantes et personnaliser les sondes d'intégrité.

### Étape 4


Créez une règle d'équilibrage de charge pour l'équilibrage de charge interne. Suivant le scénario ci-dessus, la commande crée une règle d'équilibrage de charge écoutant sur le port 1433 du pool frontal et envoyant le trafic de réseau à charge équilibrée au pool d'adresses principales en utilisant également le port 1433.

	azure network lb rule create -g nrprg -l ilbset -n ilbrule -p tcp -f 1433 -b 1433 -t feilb -o beilb

Paramètres utilisés :

**-g** - groupe de ressources **-l** - nom du jeu d'équilibrage de charge interne **-n** - nom de la règle d'équilibrage de charge **-p** - protocole utilisé pour la règle **-f** - port qui écoute le trafic réseau entrant dans l’équilibreur de charge frontal **-b** - port qui reçoit le trafic réseau dans le pool d'adresses principales

### Étape 5

Créez des règles NAT entrantes. Les règles NAT entrantes sont utilisées pour créer des points de terminaison dans un équilibreur de charge qui pointera vers une instance d'ordinateur virtuel spécifique. Selon l'exemple ci-dessus, les 2 règles NAT ont été créées pour l'accès Bureau à distance.

	azure network lb inbound-nat-rule create -g nrprg -l ilbset -n NATrule1 -p TCP -f 5432 -b 3389
	
	azure network lb inbound-nat-rule create -g nrprg -l ilbset -n NATrule2 -p TCP -f 5433 -b 3389

Paramètres utilisés :

**-g** - groupe de ressources **-l** - nom du jeu d'équilibrage de charge interne **-n** - nom de la règle NAT entrante **-p** - protocole utilisé pour la règle **-f** - port qui écoute le trafic réseau entrant dans l’équilibreur de charge frontal **-b** - port qui reçoit le trafic réseau dans le pool d'adresses principales

### Étape 5 

Créez des sondes d'intégrité pour l'équilibreur de charge. Une sonde d'intégrité vérifie toutes les instances de machine virtuelle pour s’assurer qu’elles peuvent transmettre le trafic réseau. L'instance de machine virtuelle présentant des contrôles de sonde défaillants est supprimée de l'équilibreur de charge jusqu'à ce qu'elle revienne en ligne et que la sonde valide son intégrité.

	azure network lb probe create -g nrprg -l ilbset -n ilbprobe -p tcp -i 300 -c 4

**-g** - groupe de ressources **-l** - nom du jeu d’équilibrage de charge interne **-n** - nom de la sonde d’intégrité **-p** - protocole utilisé par la sonde d’intégrité **-i** - intervalle de sondage, en secondes **-c** - nombre de contrôles

>[AZURE.NOTE] La plateforme Microsoft Azure utilise une adresse IPv4 statique routable publiquement pour divers scénarios d’administration. L’adresse IP est 168.63.129.16. Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu. En ce qui concerne l’équilibrage de charge Azure, cette adresse IP est utilisée par les sondes de l’équilibreur de charge, pour déterminer l’état de santé pour les machines virtuelles dans un jeu d’équilibrage de charge interne. Si un groupe de sécurité réseau est utilisé pour limiter le trafic vers les machines virtuelles Azure dans un jeu d’équilibrage de charge interne, ou est appliqué à un sous-réseau de réseau virtuel, vérifiez qu’une règle de sécurité de réseau est ajoutée pour autoriser le trafic à partir de 168.63.129.16.

## Créer des cartes réseau

Vous devez créer des cartes réseau (ou modifier des cartes existantes) et les associer à des règles NAT, des règles d’équilibreur de charge et des sondes.

### Étape 1 : 

Créez une carte réseau nommée *lb-nic1-be*, puis associez-la à la règle NAT *rdp1* et au premier (et unique) pool d’adresses principales *beilb*.
	
	azure network nic create -g nrprg -n lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet -d "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" -e "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus

Paramètres :

- **-g** - nom de groupe de ressource
- **-n** - nom de la ressource de carte réseau
- **--subnet-name** - nom du sous-réseau 
- **--subnet-vnet-name** - nom du réseau virtuel
- **-d** - ID de ressource de pool principal - commence par /subscription/ {subscriptionID/resourcegroups/<resourcegroup-name>/providers/Microsoft.Network/loadbalancers/<load-balancer-name>/backendaddresspools/<name-of-the-backend-pool> 
- **-e** - ID de la règle NAT qui sera associée à la ressource de la carte d’interface réseau - commence par /subscriptions/####################################/resourceGroups/<resourcegroup-name>/providers/Microsoft.Network/loadBalancers/<load-balancer-name>/inboundNatRules/<nat-rule-name>


Sortie attendue :

	info:    Executing command network nic create
	+ Looking up the network interface "lb-nic1-be"
	+ Looking up the subnet "nrpvnetsubnet"
	+ Creating network interface "lb-nic1-be"
	+ Looking up the network interface "lb-nic1-be"
	data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
	data:    Name                            : lb-nic1-be
	data:    Type                            : Microsoft.Network/networkInterfaces
	data:    Location                        : eastus
	data:    Provisioning state              : Succeeded
	data:    Enable IP forwarding            : false
	data:    IP configurations:
	data:      Name                          : NIC-config
	data:      Provisioning state            : Succeeded
	data:      Private IP address            : 10.0.0.4
	data:      Private IP Allocation Method  : Dynamic
	data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
	data:      Load balancer backend address pools
	data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
	data:      Load balancer inbound NAT rules:
	data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
	data:
	info:    network nic create command OK

### Étape 2

Créez une carte réseau nommée *lb-nic2-be*, puis associez-la à la règle NAT *rdp2* et au premier (et unique) pool d’adresses principales *beilb*.

 	azure network nic create -g nrprg -n lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet -d "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" -e "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus

### Étape 3 

Créez une machine virtuelle nommée *DB1*, puis associez-la à la carte réseau nommée *lb-nic1-be*. Un compte de stockage appelé *web1nrp* a été créé avant d’exécuter la commande ci-dessous.

	azure vm create --resource-group nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825

>[AZURE.IMPORTANT] Les machines virtuelles d’un équilibreur de charge doivent se trouver dans le même groupe à haute disponibilité. Utilisez `azure availset create` pour créer un groupe à haute disponibilité.

### Étape 4

Créez une machine virtuelle nommée *DB2*, puis associez-la à la carte réseau nommée *lb-nic2-be*. Un compte de stockage appelé *web1nrp* a été créé avant d’exécuter la commande ci-dessous.

	azure vm create --resource-group nrprg --name DB2 --location eastus --vnet-	name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825

## Suppression d’un équilibreur de charge 


Pour supprimer un équilibreur de charge, utilisez la commande suivante

	azure network lb delete -g nrprg -n ilbset 

Où **nrprg** correspond au groupe de ressources et **ilbset** au nom de l’équilibreur de charge interne.


## Étapes suivantes

[Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

<!----HONumber=AcomDC_0218_2016-->