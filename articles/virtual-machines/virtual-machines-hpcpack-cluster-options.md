<properties
 pageTitle="Options de cluster HPC Pack dans le cloud | Microsoft Azure"
 description="Découvrez les options de Microsoft HPC Pack pour créer et gérer un cluster HPC (High Performance Computing) dans le cloud Azure."
 services="virtual-machines,cloud-services,batch"
 documentationCenter=""
 authors="dlepow"
 manager="timlt"
 editor=""
 tags="azure-resource-manager,azure-service-management,hpc-pack"/>
<tags
ms.service="virtual-machines"
 ms.devlang="na"
 ms.topic="article"
 ms.tgt_pltfrm="vm-multiple"
 ms.workload="big-compute"
 ms.date="02/04/2016"
 ms.author="danlep"/>

# Options pour créer et gérer un cluster HPC (calcul haute performance) dans Azure avec Microsoft HPC Pack

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]


Tirez parti de Microsoft HPC Pack et des services de calcul et d’infrastructure Azure pour créer et gérer un cluster HPC sur le cloud. [HPC Pack](https://technet.microsoft.com/library/jj899572.aspx) est la solution HPC gratuite de Microsoft construite autour des technologies Microsoft Azure et Windows Server, prenant en charge des charges de travail HPC Windows et Linux. Un cluster HPC Pack cloud fournit à un administrateur de cluster ou un éditeur de logiciels indépendant (ISV) une plateforme flexible et évolutive pour exécuter des applications exigeantes tout en réduisant l’investissement dans une infrastructure de cluster de calcul locale.


## Configuration d’un cluster HPC Pack dans Azure

### Modèles Azure

* (Marketplace) [Cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)

* (Marketplace) [Cluster HPC Pack pour les charges de travail Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)

* (Marketplace) [Cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)

* (Démarrage rapide) [Création d'un cluster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)

* (Démarrage rapide) [Création d'un cluster HPC avec des nœuds de calcul Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

* (Démarrage rapide) [Création d'un cluster HPC avec une image de nœud de calcul personnalisée](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)

### Images d’ordinateur virtuel Azure

* [HPC Pack sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)

* [Nœud de calcul de HPC Pack sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)

* [Nœud de calcul de HPC Pack avec Excel sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)



### Script de déploiement PowerShell

* [Créer un cluster HPC avec le script de déploiement HPC Pack IaaS](virtual-machines-hpcpack-cluster-powershell-script.md)

### Didacticiels

* [Didacticiel : prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](virtual-machines-linux-cluster-hpcpack.md)

* [Didacticiel : exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](virtual-machines-linux-cluster-hpcpack-namd.md)

* [Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure](virtual-machines-linux-cluster-hpcpack-openfoam.md)

* [Didacticiel : prise en main d’un cluster HPC Pack dans Azure pour exécuter des charges de travail Excel et SOA](virtual-machines-excel-cluster-hpcpack.md)



### Déploiement manuel avec le portail Azure

* [Configurer le nœud principal d’un cluster HPC Pack dans une machine virtuelle Azure](virtual-machines-hpcpack-cluster-headnode.md)

### Gestion de cluster

* [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](virtual-machines-hpcpack-cluster-node-manage.md)


* [Agrandir et réduire les ressources de calcul Azure dans un cluster HPC Pack](virtual-machines-hpcpack-cluster-node-autogrowshrink.md)

* [Envoyer des travaux à un cluster HPC Pack dans Azure](virtual-machines-hpcpack-cluster-submit-jobs.md)


## Ajouter des nœuds de rôle de travail à un cluster HPC Pack


* [Intégration à des instances de travail Azure avec HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)

* [Didacticiel : configurer un cluster hybride avec HPC Pack dans Azure](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)

* [Ajouter des nœuds « en rafale » Azure à un nœud principal HPC Pack dans Azure](virtual-machines-hpcpack-cluster-node-burst.md)

* [Agrandir et réduire les ressources de calcul Azure dans un cluster HPC Pack](virtual-machines-hpcpack-cluster-node-autogrowshrink.md)

## Bénéficiez d'une intégration avec Azure Batch 

* [Intégration à Azure Batch avec HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## Créer des clusters RDMA pour des charges de travail MPI

* [Configuration d’un cluster Windows RDMA avec HPC Pack pour exécuter des applications MPI](virtual-machines-windows-hpcpack-cluster-rdma.md)

* [Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure](virtual-machines-linux-cluster-hpcpack-openfoam.md)

* [Configuration d’un cluster Linux RDMA pour exécuter des applications MPI](virtual-machines-linux-cluster-rdma.md)

<!---HONumber=AcomDC_0211_2016-->