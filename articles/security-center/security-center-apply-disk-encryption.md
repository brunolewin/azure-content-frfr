<properties
   pageTitle="Appliquer le chiffrement de disque dans Azure Security Center | Microsoft Azure"
   description="Ce document vous montre comment implémenter la recommandation du Centre de sécurité Azure **Apply disk encryption** (Appliquer le chiffrement de disque Azure Disk Encryption)."
   services="security-center"
   documentationCenter="na"
   authors="TerryLanfear"
   manager="StevenPo"
   editor=""/>

<tags
   ms.service="security-center"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="02/23/2016"
   ms.author="terrylan"/>

# Appliquer le chiffrement de disque dans Azure Security Center

Le Centre de sécurité Azure vous recommande d’appliquer le chiffrement de disques si vous avez des disques de machines virtuelles Windows ou Linux qui ne sont pas chiffrés à l’aide d’Azure Disk Encryption. Disk Encryption vous permet de chiffrer vos disques de machines virtuelles IaaS Windows et Linux. Le chiffrement est recommandé pour les systèmes d’exploitation et les volumes de données de votre machine virtuelle.


Disk Encryption s’appuie sur les fonctionnalités standard de l’industrie [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) de Windows et [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) de Linux pour fournir le chiffrement des données et du système d’exploitation, afin de protéger vos données et de respecter les engagements de sécurité et de conformité de votre organisation. Disk Encryption est intégré au [coffre de clés Azure](https://azure.microsoft.com/documentation/services/key-vault/) pour vous aider à contrôler et à gérer les clés de chiffrement de disque ainsi que les secrets de votre abonnement au coffre de clés, tout en vous assurant que toutes les données des disques virtuels sont chiffrées au repos dans votre [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

> [AZURE.NOTE] Azure Disk Encryption est pris en charge sur les systèmes d’exploitation Windows Server suivants : Windows Server 2008 R2, Windows Server 2012, et Windows Server 2012 R2. Disk Encryption est pris en charge sur les systèmes d’exploitation Linux suivants : Ubuntu, CentOS, SUSE et SUSE Linux Enterprise Server (SLES).

## Implémenter la recommandation

1. Dans le panneau **Recommandations**, sélectionnez **Apply disk encryption**.
2. Dans le panneau **Apply disk encryption**, vous verrez une liste des machines virtuelles pour lesquelles Disk Encryption est recommandé.
3. Suivez les instructions pour appliquer le chiffrement à ces machines virtuelles.

![][1]

## Étapes suivantes

Ce document vous a montré comment implémenter la recommandation du Centre de sécurité « Apply disk encryption ». Pour plus d’informations sur le chiffrement de disque, consultez les rubriques suivantes :

- [Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (Chiffrement et gestion de clés avec Azure Key Vault) (vidéo, 36 min 39 secondes) – Découvrez comment utiliser la gestion de chiffrement de disque pour des machines virtuelles IaaS et Azure Key Vault afin de protéger vos données.
- [Azure disk encryption](../azure-security-disk-encryption.md) (document) – Découvrez comment activer le chiffrement de disque pour des machines virtuelles Windows et Linux.

Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :

- [Définition des stratégies de sécurité dans le Centre de sécurité Azure](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité.
- [Surveillance de l’intégrité de la sécurité dans le Centre de sécurité Azure](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.
- [Gestion et résolution des alertes de sécurité dans le Centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.
- [Gestion des recommandations de sécurité dans le Centre de sécurité Azure](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
- [FAQ du Centre de sécurité Azure](security-center-faq.md) : FAQ concernant l’utilisation de ce service.
- [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.



<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png

<!---HONumber=AcomDC_0224_2016-->