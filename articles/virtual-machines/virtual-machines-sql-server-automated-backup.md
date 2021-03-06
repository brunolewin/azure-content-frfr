<properties
	pageTitle="Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure | Microsoft Azure"
	description="Décrit la fonctionnalité de sauvegarde automatisée pour SQL Server s'exécutant dans des machines virtuelles Azure à l'aide du modèle de déploiement Resource Manager."
	services="virtual-machines"
	documentationCenter="na"
	authors="rothja"
	manager="jeffreyg"
	editor="monicar"
	tags="azure-resource-manager" />
<tags
	ms.service="virtual-machines"
	ms.devlang="na"
	ms.topic="article"
	ms.tgt_pltfrm="vm-windows-sql-server"
	ms.workload="infrastructure-services"
	ms.date="02/03/2016"
	ms.author="jroth" />

# Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure

La sauvegarde automatisée configure automatiquement une [sauvegarde managée sur Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise. Cela vous permet de configurer des sauvegardes régulières de base de données utilisant le stockage d’objets blob Azure durable.

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)]Modèle Resource Manager

## Paramètres de sauvegarde automatisée

Le tableau suivant décrit les options qui peuvent être configurées pour une sauvegarde automatisée. Les étapes de la configuration varient selon que vous utilisez les commandes du portail Azure ou Azure Windows PowerShell.

|Paramètre|Plage (par défaut)|Description|
|---|---|---|
|**Sauvegarde automatisée**|Activer/Désactiver (désactivé)|Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise.|
|**Période de rétention**|1 à 30 jours (30 jours)|Nombre de jours durant lesquels une sauvegarde est conservée.|
|**Compte de stockage**|Compte de stockage Azure (compte de stockage créé pour la machine virtuelle spécifiée)|Compte de stockage Azure à utiliser pour stocker les fichiers de sauvegarde automatisée dans le stockage d’objets blob. Un conteneur est créé à cet emplacement pour stocker tous les fichiers de sauvegarde. La convention de dénomination des fichiers de sauvegarde inclut la date, l’heure et le nom de la machine.|
|**Chiffrement**|Activer/Désactiver (désactivé)|Active ou désactive le chiffrement. Lorsque le chiffrement est activé, les certificats utilisés pour restaurer la sauvegarde se trouvent dans le compte de stockage spécifié dans le même conteneur automaticbackup à l’aide de la même convention de dénomination. Si le mot de passe change, un nouveau certificat est généré avec ce mot de passe, mais l’ancien certificat est conservé pour restaurer les sauvegardes antérieures.|
|**Mot de passe**|Texte du mot de passe (aucun)|Mot de passe pour les clés de chiffrement. Il est uniquement requis si le chiffrement est activé. Pour restaurer une sauvegarde chiffrée, vous devez disposer du mot de passe correct et du certificat associé qui a été utilisé lorsque la sauvegarde a été effectuée.|

## Configurer une sauvegarde automatisée dans le portail Azure

Vous pouvez utiliser le portail Azure pour configurer une sauvegarde automatisée lorsque vous créez une machine virtuelle SQL Server 2014.

>[AZURE.NOTE] La sauvegarde automatisée utilise l’agent IaaS de SQL Server. Pour installer et configurer l’agent, vous devez disposer de l’agent Azure VM s’exécutant sur la machine virtuelle cible. Par défaut, cette option est activée dans les nouvelles images de galerie de machines virtuelles Azure, mais l’agent Azure VM peut être manquant sur les machines virtuelles existantes. Si vous utilisez votre propre image de machine virtuelle, vous devez également installer l’agent IaaS de SQL Server. Pour plus d'informations, consultez la page [Extensions et agent de machine virtuelle](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

La capture d’écran du portail Azure suivante présente ces options sous **CONFIGURATION FACULTATIVE** | **SAUVEGARDE AUTOMATISÉE SQL**.

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-sql-server-automated-backup/IC778483.jpg)

Pour les machines virtuelles SQL Server 2014 existantes, sélectionnez les paramètres de **sauvegarde automatisée** dans la section **Configuration** des propriétés de la machine virtuelle. Dans la fenêtre **Sauvegarde automatisée**, vous pouvez activer la fonctionnalité, définir la période de rétention, sélectionner le compte de stockage et définir le chiffrement. Cette situation est présentée dans la capture d’écran suivante.

![Configuration d’une sauvegarde automatisée dans le portail Azure](./media/virtual-machines-sql-server-automated-backup/IC792133.jpg)

>[AZURE.NOTE] Lorsque vous activez la sauvegarde automatisée pour la première fois, Azure configure l’agent IaaS de SQL Server en arrière-plan. Pendant ce temps, le portail Azure n’indique pas que la sauvegarde automatisée est configurée. Patientez quelques minutes jusqu’à ce que l’agent soit installé et configuré. Le portail Azure reflète alors les nouveaux paramètres.

## Configurer une sauvegarde automatisée avec PowerShell

Dans l’exemple PowerShell suivant, une sauvegarde automatisée est configurée pour une machine virtuelle SQL Server 2014 existante. La commande **New-AzureVMSqlServerAutoBackupConfig** configure les paramètres de sauvegarde automatisée pour stocker les sauvegardes dans le compte de stockage Azure spécifié par la variable $storageaccount. Ces sauvegardes sont conservées pendant 10 jours. La commande **Set-AzureVMSqlServerExtension** met à jour la machine virtuelle Azure spécifiée avec ces paramètres.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

L’installation et la configuration de l’agent IaaS de SQL Server peuvent prendre plusieurs minutes.

Pour activer le chiffrement, modifiez le script précédent pour transmettre le paramètre EnableEncryption avec un mot de passe (chaîne sécurisée) pour le paramètre CertificatePassword. Le script suivant active les paramètres de sauvegarde automatisée dans l’exemple précédent et ajoute le chiffrement.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Pour désactiver la sauvegarde automatisée, exécutez le même script sans le paramètre **-Enable** pour la commande **New-AzureVMSqlServerAutoBackupConfig**. À l’instar de l’installation, la désactivation de la sauvegarde automatisée peut prendre plusieurs minutes.

## Désactivation et désinstallation de l’agent IaaS de SQL Server

Si vous voulez désactiver l’agent IaaS de SQL Server pour la sauvegarde et la mise à jour corrective automatisées, utilisez la commande suivante :

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -Disable | Update-AzureVM

Pour désinstaller l’Agent IaaS de SQL Server, utilisez la syntaxe suivante :

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension –Uninstall | Update-AzureVM

Vous pouvez également désinstaller l’extension à l’aide de la commande **Remove-AzureVMSqlServerExtension** :

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Remove-AzureVMSqlServerExtension | Update-AzureVM

>[AZURE.NOTE] La désactivation et la désinstallation de l’agent IaaS de SQL Server ne suppriment pas les paramètres de sauvegarde managée précédemment configurés. Vous devez désactiver la sauvegarde automatisée avant de désactiver ou de désinstaller l’agent IaaS de SQL Server.

## Compatibilité

Les produits suivants sont compatibles avec les fonctionnalités de l’agent IaaS de SQL Server pour la sauvegarde automatisée :

- Windows Server 2012

- Windows Server 2012 R2

- SQL Server 2014 Standard

- SQL Server 2014 Enterprise

## Étapes suivantes

La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure. Il est donc important de [lire la documentation relative à la sauvegarde gérée](https://msdn.microsoft.com/library/dn449496.aspx) pour comprendre son comportement et ses implications.

Vous trouverez des conseils supplémentaires pour la sauvegarde et la restauration de SQL Server sur les machines virtuelles Azure dans la rubrique suivante : [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](virtual-machines-sql-server-backup-and-restore.md).

La [mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure](virtual-machines-sql-server-automated-patching.md) est une fonctionnalité associée pour les machines virtuelles SQL Server dans Azure.

Passez en revue les autres [ressources liées à l'exécution de SQL Server dans des machines virtuelles Azure](virtual-machines-sql-server-infrastructure-services.md).

<!---HONumber=AcomDC_0204_2016-->