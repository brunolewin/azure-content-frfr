<properties writer="kathydav" editor="tysonn" manager="timlt" />


Lorsque vous n’avez plus besoin d’un disque de données qui est attaché à une machine virtuelle, vous pouvez le détacher facilement. Cela supprime le disque de la machine virtuelle, mais pas du stockage. Si vous souhaitez réutiliser les données du disque, vous pouvez l’attacher à la même machine virtuelle ou à une autre.

> [AZURE.NOTE] Dans Azure, une machine virtuelle utilise différents types de disque, comme le disque du système d’exploitation, un disque temporaire local et des disques de données facultatifs. Les disques de données sont le mode de stockage recommandé pour les données des machines virtuelles. Pour en savoir plus, consultez la section [À propos des disques et VHD pour machines virtuelles](virtual-machines-disks-vhds.md). Il n’est pas possible de détacher un disque de système d’exploitation, sauf si vous supprimez également la machine virtuelle.

## Recherche du disque

Avant de pouvoir détacher un disque d'un ordinateur virtuel, vous devez rechercher le nombre LUN, qui est un identificateur pour le disque à détacher. Pour ce faire, procédez comme suit :

1. 	Ouvrez l'interface de ligne de commande Azure (Azure CLI) pour Mac, Linux et Windows, puis connectez-vous à votre abonnement Azure. Pour en savoir plus, consultez la rubrique [Se connecter à Azure à partir de l'interface de ligne de commande Azure (Azure CLI)](../articles/xplat-cli-connect.md).

2.  Vérifiez que vous êtes en mode de gestion des services Azure (la valeur par défaut) en saisissant `azure config
 	mode asm`.

3. 	Recherchez les disques attachés à votre machine virtuelle à l'aide de la commande`azure vm disk list
	<virtual-machine-name>`de la manière suivante :

		$azure vm disk list ubuntuVMasm
		info:    Executing command vm disk list
		+ Fetching disk images
		+ Getting virtual machines
		+ Getting VM disks
		data:    Lun  Size(GB)  Blob-Name                         OS
		data:    ---  --------  --------------------------------  -----
		data:         30        ubuntuVMasm-2645b8030676c8f8.vhd  Linux
		data:    1    10        test.VHD
		data:    0    30        ubuntuVMasm-76f7ee1ef0f6dddc.vhd
		info:    vm disk list command OK

4. 	Notez le LUN ou le **numéro d'unité logique** pour le disque que vous souhaitez détacher.


## Détachement du disque

Après avoir trouvé le LUN du disque, vous êtes prêt à le détacher :

1. 	Détachez le disque sélectionné de la machine virtuelle en exécutant la commande `azure vm disk detach
 	<virtual-machine-name> <LUN>` de la manière suivante :

		$azure vm disk detach ubuntuVMasm 0
		info:    Executing command vm disk detach
		+ Getting virtual machines
		+ Removing Data-Disk
		info:    vm disk detach command OK

2. 	Vous pouvez vérifier si le disque est détaché en exécutant la commande suivante :

		$azure vm disk list ubuntuVMasm
		info:    Executing command vm disk list
		+ Fetching disk images
		+ Getting virtual machines
		+ Getting VM disks
		data:    Lun  Size(GB)  Blob-Name                         OS
		data:    ---  --------  --------------------------------  -----
		data:         30        ubuntuVMasm-2645b8030676c8f8.vhd  Linux
		data:    1    10        test.VHD
		info:    vm disk list command OK

Le disque détaché reste dans le stockage, mais il n'est plus attaché à une machine virtuelle.

<!---HONumber=AcomDC_0204_2016-->