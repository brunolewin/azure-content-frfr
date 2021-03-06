<properties
 pageTitle="Tailles de services cloud"
 description="Répertorie les différentes tailles des rôles web et de travail des services cloud Azure."
 services="cloud-services"
 documentationCenter=""
 authors="Thraka"
 manager="timlt"
 editor=""/>
<tags
 ms.service="cloud-services"
 ms.devlang="na"
 ms.topic="article"
 ms.tgt_pltfrm="na"
 ms.workload="tbd"
 ms.date="09/14/2015"
 ms.author="adegeo"/>

# Tailles de services cloud

Cette rubrique décrit les tailles et options disponibles pour les instances de rôle de Cloud Services (rôles web et rôles de travail). Il expose également les points à prendre en considération pour le déploiement quand vous planifiez l'utilisation de ces ressources.

Azure Virtual Machines et Azure Cloud Services sont deux des nombreux types de ressource de calcul proposés par Azure. Pour plus de détails, consultez l'article [Modèles d'exécution Azure](fundamentals-application-models.md).

> [AZURE.NOTE]Pour connaître les limites d'Azure associées, consultez l'article [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).

## Tailles pour les instances de rôle web et de travail

Les considérations ci-dessous peuvent vous aider à choisir une taille :

* Les instances de machines virtuelles de la série D sont conçues pour exécuter des applications qui nécessitent une puissance de calcul et des performances de disque temporaire supérieures. Ces machines virtuelles se caractérisent par des processeurs plus rapides, un rapport mémoire-cœur plus élevé et un disque SSD pour le disque temporaire. Pour plus d’informations, voir l’annonce suivante sur le blog Azure : [Nouvelles tailles de machines virtuelles de la série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/) (en anglais).  

*   La série Dv2, suite de la série D d’origine, comprend un processeur plus puissant. Le processeur de la série Dv2 est environ 35 % plus rapide que le processeur de la série D. Il est basé sur la dernière génération de processeur 2,4 GHz Intel Xeon® E5-2673 v3 (Haswell) et comporte la technologie 2.0 Intel Turbo Boost, et peut atteindre 3,2 GHz. La série Dv2 a les mêmes configurations de disque et de mémoire que la série D.

    La série Dv2 sera disponible régionalement selon le calendrier suivant : octobre 2015 : Est des États-Unis 2, Centre des États-Unis, Nord-Centre des États-Unis, Ouest des États-Unis Novembre 2015 : Est des États-Unis, Europe septentrionale, Europe occidentale Janvier 2016 : Sud-Centre des États-Unis, Est de l’Asie-Pacifique, Sud-est de l’Asie-Pacifique, Est du Japon, Ouest du Japon, Est de l’Australie, Sud-est de l’Australie, Sud du Brésil

* Les rôles web et de travail nécessitent davantage d'espace disque temporaire qu'Azure Virtual Machines en raison de la configuration système requise. Les fichiers système réservent 4 Go d'espace pour le fichier d'échange de Windows et 2 Go d'espace pour le fichier de vidage de Windows.

* Le disque du système d'exploitation contient le système d'exploitation invité de Windows et inclut le dossier Program Files (y compris les installations effectuées via les tâches de démarrage, sauf si vous spécifiez un autre disque), les modifications du Registre, le dossier System32 et le .NET Framework.

* Le disque de ressources locales contient les journaux et les fichiers de configuration Azure, les diagnostics Microsoft Azure (qui incluent les journaux IIS) et les ressources de stockage locales que vous définissez.

* Le disque des applications contient votre .cspkg extrait et inclut votre site web, fichiers binaires, processus hôte de rôle, tâches de démarrage, web.config, etc.

* Les tailles de machine virtuelle A8/A10 et A9/A11 présentent les mêmes capacités. Les instances de machine virtuelle A8 et A9 intègrent une carte réseau supplémentaire qui est connectée à un réseau RDMA pour accélérer la communication entre les machines virtuelles. Les instances A8 et A9 sont conçues pour les applications de calcul hautes performances qui nécessitent une communication constante et à faible latence entre les nœuds pendant l'exécution, comme les applications qui utilisent l'interface MPI (Message Passing Interface). Les instances de machine virtuelle A10 et A11 ne sont pas équipées de cette carte réseau supplémentaire. Ces instances sont conçues pour les applications de calcul hautes performances qui n'ont pas besoin d'une communication constante et à faible latence entre les nœuds, également appelées applications paramétriques ou massivement parallèles.

|Taille|Cœurs<br>processeur|Mémoire|Tailles du disque|
|---|---|---|---|
|Très petite|1|768 Mo|Système d'exploitation = taille du SE invité<br/>Ressources locales = 15384 Go<br/>Applications = environ 1,5 Go|
|Petite|1|1,75 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 225304 Mo<br/>Applications = environ 1,5 Go|
|Moyenne|2|3,5 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 496664 Mo<br/>Applications = environ 1,5 Go|
|Grande|4|7 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1018904 Mo<br/>Applications = environ 1,5 Go|
|Très grande|8|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 2083864 Mo<br/>Applications = environ 1,5 Go|
|A5|2|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 496664 Mo<br/>Applications = environ 1,5 Go|
|A6|4|28 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1018904 Mo<br/>Applications = environ 1,5 Go|
|A7|8|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 2083864 Mo<br/>Applications = environ 1,5 Go
|A8|8|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1 856 172 Mo<br/>Applications = environ 1,5 Go<blockquote> Remarque : pour plus d’informations sur l’utilisation de cette taille et pour connaître les éléments à prendre en considération, consultez <a href="http://go.microsoft.com/fwlink/p/?linkid=328042">À propos des instances de calcul intensif A8, A9, A10 et A11</a>.</blockquote>|
|A9|16|112 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1 856 172 Mo<br/>Applications = environ 1,5 Go<blockquote> Remarque : pour plus d’informations sur l’utilisation de cette taille et pour connaître les éléments à prendre en considération, consultez <a href="http://go.microsoft.com/fwlink/p/?linkid=328042">À propos des instances de calcul intensif A8, A9, A10 et A11</a>.</blockquote>|
|A10|8|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1 856 172 Mo<br/>Applications = environ 1,5 Go<blockquote> Remarque : pour plus d’informations sur l’utilisation de cette taille et pour connaître les éléments à prendre en considération, consultez <a href="http://go.microsoft.com/fwlink/p/?linkid=328042">À propos des instances de calcul intensif A8, A9, A10 et A11</a>.</blockquote>|
|A11|16|112 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 1 856 172 Mo<br/>Applications = environ 1,5 Go<blockquote> Remarque : pour plus d’informations sur l’utilisation de cette taille et pour connaître les éléments à prendre en considération, consultez <a href="http://go.microsoft.com/fwlink/p/?linkid=328042">À propos des instances de calcul intensif A8, A9, A10 et A11</a>.</blockquote>|
|D1 standard|1|3,5 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 46 104 Mo<br/>Applications = environ 1,5 Go|
|D2 standard|2|7 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 97304 Mo<br/>Applications = environ 1,5 Go|
|D3 standard|4|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 199704 Mo<br/>Applications = environ 1,5 Go|
|D4 standard|8|28 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 404 504 Mo<br/>Applications = environ 1,5 Go|
|D11 standard|2|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 97304 Mo<br/>Applications = environ 1,5 Go|
|D12 standard|4|28 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 199704 Mo<br/>Applications = environ 1,5 Go|
|D13 standard|8|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 404 504 Mo<br/>Applications = environ 1,5 Go|
|D14 standard|16|112 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 814104 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D1\_v2|1|3,5 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 46104 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D2\_v2|2|7 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 97304 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D3\_v2|4|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 199704 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D4\_v2|8|28 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 404 504 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D5\_v2|16|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 814104 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D11\_v2|2|14 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 97304 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D12\_v2|4|28 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 199704 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D13\_v2|8|56 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 404 504 Mo<br/>Applications = environ 1,5 Go|
|Standard\_D14\_v2|16|112 Go|Système d’exploitation = taille du SE invité<br/>Ressources locales = 814 104 Mo<br/>Applications = environ 1,5 Go|
## Configurer les tailles pour les Cloud Services

Vous pouvez spécifier la taille de l’ordinateur virtuel d'une instance de rôle dans le cadre du modèle de service décrit par le fichier de définition de service. La taille du rôle détermine le nombre de cœurs du processeur, la capacité de mémoire et la taille du système de fichiers local qui lui est allouée. Choisissez la taille du rôle en fonction des besoins en ressources de votre application.

Voici un exemple qui montre comment configurer un rôle de petite taille pour une instance de rôle Web :


    <WebRole name="WebRole1" vmsize="Small">
    …
    </WebRole>

Assurez-vous que la taille de ressources locales spécifiée est inférieure ou égale à la taille de ressources locales maximale indiquée dans le tableau ci-dessus.
## Étapes suivantes

[Configuration d'un service cloud pour Azure](https://msdn.microsoft.com/library/hh124108)

<!---HONumber=AcomDC_0128_2016-->