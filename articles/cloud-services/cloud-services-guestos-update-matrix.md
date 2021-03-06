<properties 
   pageTitle="En savoir plus sur les dernières publications du SE invité de Microsoft Azure | Microsoft Azure" 
   description="Dernières informations de publication et de compatibilité du Kit de développement logiciel (SDK) pour le SE invité de Microsoft Azure Cloud Services." 
   services="cloud-services" 
   documentationCenter="na" 
   authors="yuemlu" 
   manager="timlt" 
   editor=""/>

<tags
   ms.service="cloud-services"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="tbd" 
   ms.date="02/22/2016"
   ms.author="yuemlu"/>

# Versions du SE invité et matrice de compatibilité du Kit de développement logiciel (SDK) Azure
Fournit des informations récentes sur les dernières publications du SE (système d’exploitation) invité de Microsoft Azure pour Cloud Services. Ces informations vous aideront à planifier votre mise à niveau avant la désactivation d’un SE invité.

> [AZURE.IMPORTANT] Le contenu de cette page s’applique aux rôles web et de travail Cloud Services, qui s’exécutent sur un SE invité. Il ne s’applique pas aux machines virtuelles IaaS. Si vous configurez vos rôles pour utiliser les mises à jour automatiques d’un SE invité comme cela est décrit dans [Paramètres de mise à jour du système d’exploitation invité Azure][], il n’est pas indispensable que vous lisiez cette page.

<!-- -->
<br />

> [AZURE.TIP] Abonnez-vous au [Flux RSS de mise à jour du SE invité][rss] pour recevoir en temps voulu les notifications relatives à toutes les modifications de SE invités. Les modifications indiquées dans ce flux seront intégrées dans cette page environ toutes les semaines.



## Nouvelles mises à jour

###### **22 février 2016**
Le déploiement du SE invité du mois de février commence le 22 février 2016, et devrait être publié le 9 mars 2016.

###### **18 janvier 2016**
Le déploiement du SE invité du mois de janvier commence le 18 janvier 2016, et devrait être publié le 12 février 2016.

###### **4 janvier 2016**
Le déploiement du système d’exploitation invité de 201511-02 de novembre a été publié le 4 janvier 2016. Cette version du système d'exploitation n'étant pas définie comme système d'exploitation par défaut pour la mise à jour automatique, le délai d’approvisionnement du déploiement du système d’exploitation invité de 201511-02 de novembre devrait être légèrement plus long.

###### **18 décembre 2015**
La date de publication du système d’exploitation invité de 201511-02 de novembre a été différée du 16 décembre 2015 au 4 janvier 2016.

###### **9 décembre 2015**
Le déploiement du SE invité du mois de décembre commence le 10 décembre 2015, et devrait être publié le 8 janvier 2016.

###### **12 novembre 2015**  
Le 7 août 2014, Microsoft a annoncé la fin de la prise en charge de .NET Framework 4, 4.5 et 4.5.1 le 12 janvier 2016. Nous recommandons aux clients et développeurs d’effectuer la mise à jour sur place pour .NET Framework 4.5.2 avant le 12 janvier 2016 afin de continuer à recevoir des mises à jour de sécurité et à bénéficier du support technique. Pour plus d’informations, consultez la politique de support Microsoft .NET Framework.

Le 27 octobre, nous avons annoncé la mise à jour par Azure de .NET Framework dans le système d’exploitation invité Azure (familles 2.x, 3.x et 4.x) vers .NET Framework 4.5.2 lors de la publication de la prochaine version du système d’exploitation invité en novembre. Depuis, nous avons reçu des commentaires des clients demandant de reporter la mise à jour automatique vers une version de système d’exploitation avec .NET 4.5.2 et de fournir une image avec .NET 4.5.2 pour la validation des tests.

Pour répondre aux demandes des clients et fournir une mise à niveau fluide vers .NET 4.5.2, Azure mettra à jour .NET Framework dans le système d’exploitation invité Azure (familles 2.x, 3.x et 4.x) vers .NET Framework 4.5.2 lors de la publication du système d’exploitation invité de janvier 2016. Les services cloud exécutant la famille de systèmes d’exploitation invités 2.x, 3.x et 4.x avec des mises à jour automatiques activées seront mis à jour vers la version de janvier 2016 du système d’exploitation invité avec .NET Framework 4.5.2. En novembre, la version de .NET Framework installée dans le système d’exploitation par défaut ne sera pas modifiée. Pour aider les clients à valider leur service cloud avec .NET 4.5.2, Azure fournira en novembre un second jeu de versions de système d’exploitation 201511-02 avec .NET 4.5.2 pour un déploiement manuel.

Le tableau suivant présente les modifications qui seront appliquées.
 
| Famille de SE invité | .NET Framework installé avant la publication du système d’exploitation invité 201511-02 | .NET Framework installé lors de la publication du système d’exploitation invité 201511-02 | .NET Framework installé lors de la publication du système d’exploitation invité 201512-01 | .NET Framework installé lors de la publication du système d’exploitation invité 201601-01 ou ultérieur |
| --------------- | ---------------- | ---------------- | ---------------- | ---------------- |
| Famille 2.x du système d’exploitation basée sur Windows Server 2008 R2 | .NET 3.5, .NET 4.0 | .NET 3.5, .NET 4.5.2 | .NET 3.5, .NET 4.0 | .NET 3.5, .NET 4.5.2 |
| Famille 3.x du système d’exploitation basée sur Windows Server 2012 | .NET 4.5 | .NET 4.5.2 | .NET 4.5 | .NET 4.5.2 | 
| Famille 4.x du système d’exploitation basée sur Windows Server 2012 R2 | .NET 4.5.1 | .NET 4.5.2 | .NET 4.5.1 | .NET 4.5.2 | 
 
Si vous êtes concerné par la mise à jour manuelle du système d’exploitation invité, deux versions de système d’exploitation invité seront publiées pour toutes les familles de système d’exploitation invité en novembre.

   • WA-GUEST-OS-4.26\_201511-01, WA-GUEST-OS-3.33\_201511-01, WA-GUEST-OS-2.45\_201511-01 (par défaut)

   Sont inclus les correctifs cumulatifs Windows d’octobre et MSRC de novembre

   • WA-GUEST-OS-4.26\_201511-02, WA-GUEST-OS-3.33\_201511-02, WA-GUEST-OS-2.45\_201511-02

   Sont inclus les correctifs cumulatifs Windows d’octobre, MSRC de novembre et la mise à niveau de .NET Framework vers .NET 4.5.2



Avant la mise à niveau, voici certaines des options pour valider votre service cloud avec .NET 4.5.2 :

1. 	Déployez un rôle de service cloud de test vers la version 201511-02 et effectuez la validation de la compatibilité des applications. 

2. 	Installez .NET 4.5.2 sur un rôle de service cloud de test et effectuez la validation de la compatibilité des applications. Pour obtenir des instructions, consultez [Installer .NET sur un rôle de service cloud].

3. 	Effectuez la validation de la compatibilité des applications sur une machine virtuelle autonome, soit localement, soit sur une machine virtuelle Azure sur laquelle .NET 4.5.2 est installé.




###### **15 octobre 2015**
Le déploiement du système d’exploitation invité du mois d’octobre commence dès aujourd’hui, le 15 octobre 2015, et devrait être publié le 13 novembre 2015.

Les versions 4.24, 3.31, 2.43 du SE invité ont été publiées le 1er octobre 2015.

###### **9 septembre 2015**
Le déploiement du système d’exploitation invité du mois de septembre commence dès aujourd’hui, le 9 septembre 2015, et devrait être publié le 8 octobre 2015.

Les versions 4.23, 3.30 et 2.42 du SE invité ont été publiées le 9 septembre 2015.

###### **14 août 2015**
Le déploiement du système d’exploitation invité du mois d’août commence dès aujourd’hui, le 14 août 2015, et devrait être publié le 11 septembre 2015.

###### **7 août 2015**
Les versions 4.22, 3.29, 2.41 du SE invité ont été publiées le 7 août 2015.

###### **14 juillet 2015**
Le déploiement du système d'exploitation invité du mois de juillet commence dès aujourd'hui, le 14 juillet 2015, et devrait être publié le 14 août 2015.

Les versions 4.21, 3.28 et 2.40 du SE invité ont été publiées le 9 juillet 2015.

###### **15 juin 2015**
Le déploiement du système d'exploitation invité du mois de juin commence dès aujourd'hui, le 15 juin 2015, et devrait être publié le 9 juillet 2015.

Les versions 4.20, 3.27 et 2.39 du SE invité ont été publiées le 12 juin 2015.

###### **20 mai 2015**
Le déploiement du système d'exploitation invité du mois de mai commence dès aujourd'hui, le 20 mai 2015, et devrait être publié le 12 juin 2015.

###### **17 avril 2015**
Les versions 4.19, 3.26 et 2.38 du SE invité ont été publiées aujourd’hui.

Cette version contient [MS15-034](https://technet.microsoft.com/library/security/MS15-034), un correctif **critique** pour les serveurs HTTP sous Windows.

Les versions 4.17, 3.24 et 2.36 du SE invité seront désactivées le 17 mai 2015.

###### **6 avril 2015**
Les versions 4.18, 3.25 et 2.37 du SE invité ont été publiées le 2 avril 2015.

Les versions 4.16, 3.23 et 2.35 du SE invité seront désactivées le 2 mai 2015.


###### **11 mars 2015**
Les versions 4.17, 3.24 et 2.36 du SE invité ont été publiées le 9 mars 2015.

La date de désactivation des versions 4.15, 3.22 et 2.34 du SE invité a été fixée au 9 avril 2015.


###### **29 janvier 2015**
La date de désactivation des versions 4.14, 4.13, 3.21, 3.20, 2.33 et 2.32 du SE invité a été repoussée. La matrice de publication du SE invité a été mise à jour.


###### **13 janvier 2015, mise à jour le 15 janvier 2015**
Le SE invité a été publié le 14 janvier 2015.


###### **13 janvier 2015**
Le démarrage du déploiement du SE invité de janvier est prévu au plus tôt pour la mise à jour du 19 janvier 2015. Les services cloud seront mis à jour automatiquement. Le SE invité de janvier sera disponible pour le déploiement en février. Il va désactiver SSL version 3.0 par défaut comme indiqué dans la mise à jour de sécurité de janvier. Cet article sera mis à jour lorsque des informations supplémentaires seront disponibles.

Comme [précédemment annoncé][ssl3 announcement], la mise à jour de sécurité de janvier du SE invité PaaS désactivera la prise en charge SSL version 3.0 par défaut recommandée par l’[avis de sécurité Microsoft 3009008][]. Cette modification se rajoutera aux autres mises à jour de sécurité mensuelles. Les clients PaaS avec mises à jour automatiques activées peuvent valider la présence d’impact de compatibilité des applications lorsque SSL version 3.0 est désactivé par l’exécution du [script Fix it][ssl3-fixit] qui désactivera de manière proactive la prise en charge de SSL version 3.0.

###### **16 décembre 2014. Mis à jour le 7 janvier 2015**
Le démarrage de la publication du SE invité de décembre est prévu pour le 9 janvier 2015 au plus tôt.




## Informations de publication du SE invité

Cette section répertorie les versions de SE invité actuellement prises en charge. Les familles et versions de SE invité ont une date de publication, une date de désactivation et une date d’expiration. Lors de sa date de publication, une version de SE invité peut être sélectionnée manuellement dans le portail Azure Classic. Un SE invité est supprimé du portail Azure Classic au moment de sa date de désactivation ou après celle-ci. Il est alors « en transition » : il reste pris en charge mais sa capacité de mise à jour de déploiement est limitée. La date d’expiration correspond au moment où une version ou une famille est définitivement supprimée du système Azure. Les services cloud exécutés sur une version lors de son expiration sont arrêtés, supprimés ou mis à jour de force vers une version plus récente, comme cela est décrit dans la [Politique de prise en charge et de suppression du SE invité Azure][retirepolicy].

Microsoft prend en charge au moins deux versions récentes de chaque famille de SE invité pris en charge. La date de désactivation d’une version de SE invité existante peut être retardée pour garantir qu’au moins deux versions publiées restent activées pour le déploiement.

> [AZURE.WARNING] Le retrait de la famille du SE invité 1 a commencé le 1er juin 2013 et devrait s’achever bientôt. Veuillez ne pas créer d’installations, et procédez à la mise à niveau des anciennes installations utilisant cette famille de SE invité. Pour plus d’informations, consultez la page [Informations relatives à la suppression de la Famille 1 de systèmes d’exploitation invités Azure][fam1retire]


### Informations sur la famille, la version et la publication du SE invité
Les familles de SE invité sont basées sur les versions publiées de Microsoft Windows Server. Le SE invité est le système d’exploitation sous-jacent sur lequel s’exécute Azure Cloud Services. Chaque SE invité possède un numéro de famille, de version et de publication.

La **famille de SE invité** correspond à une publication de système d’exploitation Windows Server sur laquelle est basé un SE invité. Par exemple, la famille 3 est basée sur Windows Server 2012.

Une **« Version de SE invité »** est l’image du SE de la famille accompagnée des correctifs [Microsoft Security Response Center (MSRC)][msrc] adéquats disponibles à la date de production de la nouvelle version du SE invité. Il est possible que les correctifs ne soient pas tous inclus. Les numéros commencent à 0 et augmentent de 1 chaque fois qu’un nouvel ensemble de mises à jour est ajouté. Les zéros à droite sont uniquement affichés s’ils sont importants. Autrement dit, la version 2.10 est une version différente, bien plus récente, que la version 2.1.

Une **« Publication de SE invité »** correspond à une nouvelle publication d’une version de SE invité. Une nouvelle publication survient si Microsoft détecte des problèmes pendant les tests nécessitant des modifications. La publication la plus récente remplace toujours les publications précédentes, publiques ou non. Le portail Azure Classic permet uniquement aux utilisateurs de choisir la publication la plus récente pour une version donnée. Les déploiements s’exécutant sur une publication antérieure ne sont généralement pas mis à niveau de force en fonction de la gravité du bogue.

Dans l’exemple ci-dessous, 2 est la famille, 12 est la version et « rel2 » est la publication.

**Publication du SE invité** - 2.12 rel2

**Chaîne de configuration pour cette publication** - WA-GUEST-OS-2.12\_201208-02

Ces informations sont intégrées dans la chaîne de configuration d’un SE invité, ainsi qu’une date indiquant les correctifs MSRC envisagés pour cette publication. Dans cet exemple, les correctifs MSRC produits pour Windows Server 2008 R2 jusqu’à août 2012 inclus ont été envisagés pour l’inclusion. Seuls les correctifs s’appliquant spécifiquement à cette version de Windows Server sont inclus. Par exemple, si un correctif logiciel de MSRC s’applique à Microsoft Office, il ne sera pas inclus, car ce produit ne fait pas partie de l’image de base de Windows Server.

## Publications

## Publications de famille 4
**Windows Server 2012 R2**

Prend en charge .NET 4.0, 4.5, 4.5.1, 4.5.2 (Remarque 2)

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ---------------------- | ------------ | --- |
| 4\.29 | WA-GUEST-OS-4.29\_201602-01 | Prévu le 9 mars 2016 | Mise à jour lors de la publication de la version 4.31 | TBD |
| 4\.28 | WA-GUEST-OS-4.28\_201601-01 | 12 février 2016 | Mise à jour lors de la publication de la version 4.30 | TBD |
| 4\.27 | WA-GUEST-OS-4.27\_201512-01 | 12 janvier 2016 | Mise à jour à l’occasion de la publication de la version 4.29 | TBD |
| 4\.26 | WA-GUEST-OS-4.26\_201511-02 | 4 janvier 2016 | 12 mars 2016| TBD |
| 4\.26 | WA-GUEST-OS-4.26\_201511-01 | 10 décembre 2015 | 12 mars 2016| TBD |
| 4\.25 | WA-GUEST-OS-4.25\_201510-01 | 6 novembre 2015 | 12 février 2016 | TBD |
| 4\.24 | WA-GUEST-OS-4.24\_201509-01 | 1er octobre 2015 | 10 janvier 2016 | TBD |
| 4\.23 | WA-GUEST-OS-4.23\_201508-02 | 9 septembre 2015 | 6 décembre 2015 | TBD |
| 4\.22 | WA-GUEST-OS-4.22\_201507-02 | 7 août 2015 | 1 novembre 2015 | TBD |
| 4\.21 | WA-GUEST-OS-4.21\_201506-01 | 9 juillet 2015 | 9 octobre 2015 | TBD |
| 4\.20 | WA-GUEST-OS-4.20\_201505-02 | 12 juin 2015 | 7 septembre 2015 | TBD |
| 4\.19 | WA-GUEST-OS-4.19\_201504-01 | 17 avril 2015 | 9 août 2015 | TBD |
| 4\.18 | WA-GUEST-OS-4.18\_201503-01 | 2 avril 2015 | 12 juillet 2015 | 14 octobre 2015 |
| 4\.17 | WA-GUEST-OS-4.17\_201502-01 | 9 mars 2015 | 17 mai 2015 | 14 octobre 2015 |
| 4\.16 | WA-GUEST-OS-4.16\_201501-01 | 29 janvier 2015 | 2 mai 2015 | 14 octobre 2015 |
| 4\.15 | WA-GUEST-OS-4.15\_201412-01 | 14 janvier 2015 | 9 avril 2015 | 14 octobre 2015 |
| 4\.14 | WA-GUEST-OS-4.14\_201411-01 | 11 novembre 2014 | 28 février 2015 | 14 octobre 2015 |
| 4\.13 | WA-GUEST-OS-4.13\_201410-01 | 3 novembre 2014 | 14 février 2015 | 14 octobre 2015 |
| 4\.12 (Remarque 1) | WA-GUEST-OS-4.12\_201409-02 | 6 octobre 2014 | 12 octobre 2014 | 23 mars 2015 |
| 4\.11 (Remarque 1) | WA-GUEST-OS-4.11\_201408-02 | 25 août 2014 | 11 septembre 2014 | 23 mars 2015 |
| 4\.10 | WA-GUEST-OS-4.10\_201407-01 | 18 juillet 2014 | 1 décembre 2014 | 23 mars 2015 |
| 4\.9 | WA-GUEST-OS-4.9\_201406-01 | 16 juin 2014 | 10 novembre 2014 | 23 mars 2015 |
| 4\.8 | WA-GUEST-OS-4.8\_201405-01 | 1er juin 2014 | 1er août 2014 | 23 mars 2015 |

## Publications de famille 3

**Windows Server 2012**

Prend en charge .NET 4.0, 4.5

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ---------------------- | ------------ | --- |
| 3\.36 | WA-GUEST-OS-3.36\_201602-01 | Prévu le 9 mars 2016 | Mise à jour lors de la publication de la version 3.38 | TBD |
| 3\.35 | WA-GUEST-OS-3.35\_201601-01 | 12 février 2016 | Mise à jour lors de la publication de la version 3.37 | TBD |
| 3\.34 | WA-GUEST-OS-3.34\_201512-01 | 12 janvier 2016 | Mise à jour lors de la publication de la version 3.36 | TBD |
| 3\.33 | WA-GUEST-OS-3.33\_201511-02 | 4 janvier 2016 | 12 mars 2016| TBD |
| 3\.33 | WA-GUEST-OS-3.33\_201511-01 | 10 décembre 2015 | 12 mars 2016| TBD |
| 3\.32 | WA-GUEST-OS-3.32\_201510-01 | 6 novembre 2015 | 12 février 2016 | TBD |
| 3\.31 | WA-GUEST-OS-3.31\_201509-01 | 1er octobre 2015 | 10 janvier 2016 | TBD |
| 3\.30 | WA-GUEST-OS-3.30\_201508-02 | 9 septembre 2015 | 6 décembre 2015 | TBD |
| 3\.29 | WA-GUEST-OS-3.29\_201507-02 | 7 août 2015 | 1 novembre 2015 | TBD |
| 3\.28 | WA-GUEST-OS-3.28\_201506-01 | 9 juillet 2015 | 9 octobre 2015 | TBD |
| 3\.27 | WA-GUEST-OS-3.27\_201505-02 | 12 juin 2015 | 7 septembre 2015 | TBD |
| 3\.26 | WA-GUEST-OS-3.26\_201504-01 | 17 avril 2015 | 9 août 2015 | TBD |
| 3\.25 | WA-GUEST-OS-3.25\_201503-01 | 2 avril 2015 | 12 juillet 2015 | 14 octobre 2015 |
| 3\.24 | WA-GUEST-OS-3.24\_201502-01 | 9 mars 2015 | 17 mai 2015 | 14 octobre 2015 |
| 3\.23 | WA-GUEST-OS-3.23\_201501-01 | 29 janvier 2015 | 2 mai 2015 | 14 octobre 2015 |
| 3\.22 | WA-GUEST-OS-3.22\_201412-01 | 14 janvier 2015 | 9 avril 2015 | 14 octobre 2015 |
| 3\.21 | WA-GUEST-OS-3.21\_201411-01 | 11 novembre 2014 | 28 février 2015 | 14 octobre 2015 |
| 3\.20 | WA-GUEST-OS-3.20\_201410-01 | 3 novembre 2014 | 14 février 2015 | 14 octobre 2015 |
| 3\.19 (Remarque 1) | WA-GUEST-OS-3.19\_201409-02 | 6 octobre 2014 | 12 octobre 2014 | 23 mars 2015 |
| 3\.18 (Remarque 1) | WA-GUEST-OS-3.18\_201408-02 | 25 août 2014 | 11 septembre 2014 | 23 mars 2015 |
| 3\.17 | WA-GUEST-OS-3.17\_201407-01 | 18 juillet 2014 | 1 décembre 2014 | 23 mars 2015 |
| 3\.16 | WA-GUEST-OS-3.16\_201406-01 | 16 juin 2014 | 10 novembre 2014 | 23 mars 2015 |
| 3\.15 | WA-GUEST-OS-3.15\_201405-01 | 1er juin 2014 | 1er août 2014 | 23 mars 2015 |


## Publications de famille 2

**Windows Server 2008 R2 SP1**

Prend en charge .NET 3.5, 4.0

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ---------------------- | ------------ | --- |
| 2\.48 | WA-GUEST-OS-2.48\_201602-01 | Prévu le 9 mars 2016 | Mise à jour lors de la publication de la version 2.50 | TBD |
| 2\.47 | WA-GUEST-OS-2.47\_201601-01 | 12 février 2016 | Mise à jour lors de la publication de la version 2.49 | TBD |
| 2\.46 | WA-GUEST-OS-2.46\_201512-01 | 12 janvier 2016 | Mise à jour lors de la publication de la version 2.48 | TBD |
| 2\.45 | WA-GUEST-OS-2.45\_201511-02 | 4 janvier 2016 | 12 mars 2016| TBD |
| 2\.45 | WA-GUEST-OS-2.45\_201511-01 | 10 décembre 2015 | 12 mars 2016| TBD |
| 2\.44 | WA-GUEST-OS-2.44\_201510-01 | 6 novembre 2015 | 12 février 2016 | TBD |
| 2\.43 | WA-GUEST-OS-2.43\_201509-01 | 1er octobre 2015 | 10 janvier 2016 | TBD |
| 2\.42 | WA-GUEST-OS-2.42\_201508-02 | 9 septembre 2015 | 6 décembre 2015 | TBD |
| 2\.41 | WA-GUEST-OS-2.41\_201507-02 | 7 août 2015 | 1 novembre 2015 | TBD |
| 2\.40 | WA-GUEST-OS-2.40\_201506-01 | 9 juillet 2015 | 9 octobre 2015 | TBD |
| 2\.39 | WA-GUEST-OS-2.39\_201505-02 | 12 juin 2015 | 7 septembre 2015 | TBD |
| 2\.38 | WA-GUEST-OS-2.38\_201504-01 | 17 avril 2015 | 9 août 2015 | TBD |
| 2\.37 | WA-GUEST-OS-2.37\_201503-01 | 2 avril 2015 | 12 juillet 2015 | 14 octobre 2015 |
| 2\.36 | WA-GUEST-OS-2.36\_201502-01 | 9 mars 2015 | 17 mai 2015 | 14 octobre 2015 |
| 2\.35 | WA-GUEST-OS-2.35\_201501-01 | 29 janvier 2015 | 2 mai 2015 | 14 octobre 2015 |
| 2\.34 | WA-GUEST-OS-2.34\_201412-01 | 14 janvier 2015 | 9 avril 2015 | 14 octobre 2015 |
| 2\.33 | WA-GUEST-OS-2.33\_201411-01 | 11 novembre 2014 | 28 février 2015 | 14 octobre 2015 |
| 2\.32 | WA-GUEST-OS-2.32\_201410-01 | 3 novembre 2014 | 14 février 2015 | 14 octobre 2015 |
| 2\.31 (Remarque 1) | WA-GUEST-OS-2.31\_201409-02 | 6 octobre 2014 | 12 octobre 2014 | 23 mars 2015 |
| 2\.30 (Remarque 1) | WA-GUEST-OS-2.30\_201408-02 | 25 août 2014 | 11 septembre 2014 | 23 mars 2015 |
| 2\.29 | WA-GUEST-OS-2.29\_201407-01 | 18 juillet 2014 | 1 décembre 2014 | 23 mars 2015 |
| 2\.28 | WA-GUEST-OS-2.28\_201406-01 | 16 juin 2014 | 10 novembre 2014 | 23 mars 2015 |
| 2\.27 | WA-GUEST-OS-2.27\_201405-01 | 1er juin 2014 | 1er août 2014 | 23 mars 2015 |




### Publications de famille 1
La **FAMILLE 1** a été [supprimée][fam1retire].

#### Remarque 1
Les publications d’août et de septembre 2014 ont été partiellement déployées en raison de problèmes détectés avec une partie des [correctifs MSRC][MS14-046] durant la publication. Le problème empêche l’installation manuelle de .NET 3.5.1 sur les familles 3 et 4. La publication a été désactivée par mesure de précaution pour que les clients ne puissent pas la sélectionner manuellement.

#### Remarque 2
Depuis le 19 septembre 2014, .NET 4.5.2 n’a pas été testé spécifiquement sur le SE invité Azure. Mais le SE invité équivaut globalement à Windows Server. Par conséquent, les mêmes règles de compatibilité qui s’appliquent au produit Windows Server s’appliquent aux familles de SE invité équivalentes. Si vous rencontrez une exception à cette règle, veuillez contacter le [support technique Azure][azuresupport]. Microsoft s’efforcera de résoudre votre problème, dans la mesure du possible. [Installation manuelle du package pour .NET 4.5.2][net install pkg].

## Mises à jour MSRC incluses dans le SE invité
La liste des correctifs inclus dans chaque publication mensuelle du SE invité est disponible [ici][patches].

## Prise en charge du Kit de développement logiciel (SDK)

Ce tableau indique quelle famille de SE invité est compatible avec quelle version de Kit de développement logiciel (SDK) Azure. Pour en savoir plus, consultez la page [Informations relatives à la prise en charge et au retrait pour le Kit de développement logiciel Azure SDK pour .NET et les API][retire policy sdk]. Toutes les informations de cette liste remplacent les informations ci-dessous.

> [AZURE.IMPORTANT] Pour vous assurer que votre service fonctionne comme prévu, vous devez le déployer sur la publication du SE invité compatible avec la version du Kit de développement logiciel (SDK) Azure utilisée pour développer votre service. Sinon, des erreurs absentes dans l’environnement de développement pourront toucher le service déployé dans le cloud.

| Famille de SE invité | Versions du Kit de développement logiciel (SDK) prises en charge |
| --------------- | ---------------------- |
| 4 | Version 2.1 et ultérieures |
| 3 | Version 1.8 et ultérieures |
| 2 | Version 1.3 et ultérieures |
| 1 | Version 1.0 et ultérieures |


## Processus de mise à jour du SE invité
Cette page contient des informations sur les prochaines publications de SE invités. Les clients ont indiqué qu’ils souhaitent être informés lors d’une publication, car leurs rôles de service cloud redémarreront s’ils sont définis pour la mise à jour « Automatique ». Les publications de SE invités se produisent généralement au moins 5 jours après la publication de mise à jour MSRC survenant le deuxième mardi de chaque mois. Les nouvelles publications incluent tous les correctifs MSRC adéquats pour chaque famille de SE invité.

Microsoft Azure publie constamment des mises à jour. Le SE invité n’est qu’une mise à jour parmi d’autres. Une version peut être affectée par un certain nombre de facteurs trop nombreux pour être répertoriés ici. En outre, Azure s’exécute sur des centaines de milliers d’ordinateurs. Cela signifie qu’il est impossible de donner une date et une heure précises pour le redémarrage de vos rôles. Nous mettrons à jour le [Flux RSS de mise à jour du SE invité][rss] avec les dernières informations dont nous disposons, mais considérez les dates présentées comme approximatives. Nous sommes conscients que cela peut être problématique pour les clients et travaillons sur un plan pour limiter ou régler ces redémarrages.

La propagation complète sur Azure d’une nouvelle publication de SE invité peut prendre du temps. Lorsque les services sont mis à jour pour le nouveau SE invité, ils sont redémarrés en respectant les domaines de mise à jour. Les services définis pour utiliser des mises à jour « Automatiques » obtiennent une publication en premier. Après la mise à jour, la nouvelle version du SE invité est répertoriée pour votre service dans le portail Azure Classic. De nouvelles publications peuvent se produire pendant cette période. Il est possible que certaines versions soient déployées sur de longues périodes et donc que des redémarrages de mise à niveau automatiques ne se produisent pas pendant plusieurs semaines après la date officielle de la publication. Une fois qu’un SE invité est disponible, vous pouvez choisir explicitement cette version à partir du portail ou dans votre fichier de configuration.

Pour consulter un grand nombre d’informations utiles sur les redémarrages et des orientations vers d’autres informations techniques sur les mises à jour de SE invités et hôtes, consultez le blog de MSDN intitulé [Redémarrage d’instance de rôle en raison d’une mise à niveau du SE][restarts].

Si vous procédez à une mise à jour manuelle de votre SE invité, consultez la page [Stratégie de suppression du SE invité][retirepolicy].


## Prise en charge et stratégie de suppression du SE invité
La prise en charge et la stratégie de suppression du SE invité sont détaillées [ici][retirepolicy].
 
## Archive des dernières nouvelles

###### **11 novembre 2014.**

La publication de novembre (4.14, 3.21 et 2.33) a été déployée le 11 novembre. Cette mise à jour a été publiée plus tôt, car elle inclut la mise à jour MSRC [Bulletin de sécurité Microsoft MS14-066 - Critique][MS14-066]. Vos rôles web et de travail pour la mise à jour automatique doivent redémarrer une fois au cours des jours suivants pour recevoir ce correctif.

###### **10 novembre 2014**
La date de désactivation de la publication d’octobre (4.13, 3.20 et 2.32) a été mise à jour en fonction des commentaires des clients. La date de désactivation sera toujours fixée au moins deux mois après la date de publication.

###### **4 novembre 2014**
La publication d’octobre (4.13, 3.20 et 2.32) a été déployée le 4 novembre 2014. Elle inclut le correctif MSRC ayant provoqué des problèmes avec les publications d’août et de septembre. Pour contourner ce problème, .NET 3.5 et 3.5.1, qui sont inclus dans la publication d’octobre, sont pré-installés mais désactivés. Les scripts essayant d’installer .NET 3.5 ou 3.5.1 parviendront à le réactiver et signaleront la « réussite » de l’installation de .NET, tout en évitant le problème d’installation complète créé par le correctif MSRC.

**20 octobre 2014. Mise à jour le 4 novembre 2014**: la publication de septembre (4.12, 3.19, 2.31 et 1.39) est partiellement déployée en raison du même [correctif MSRC MS14-046][MS14-046] provoquant des défaillances pour les utilisateurs essayant d’installer .NET 3.5 ou 3.5.1 sur la famille 3 ou 4. .NET 3.5.x n’est PAS officiellement pris en charge sur une famille, mais Microsoft répond à cette modification de comportement, car les installations de certains clients reposent sur cette version et la modification a été annoncée. Les dates de désactivation du précédent SE invité (juin et juillet) seront retardées en conséquence pour qu’au moins deux SE invités entièrement publiés soient pris en charge et disponibles. Une solution au problème d’installation de .NET est apparue dans la publication d’octobre 2014.

La publication d’octobre inclut .NET 3.5 et 3.5.1 en pré-installation (tout en les désactivant), ainsi que les correctifs MSRC répertoriés précédemment. Les scripts essayant d’installer .NET 3.5 ou 3.5.1 parviendront à le réactiver et signaleront la « réussite » de l’installation de .NET, tout en évitant le problème d’installation créé par le correctif MSRC.

En raison du déploiement partiel des deux dernières versions, les personnes utilisant la mise à jour automatique ou ayant déployé des nouvelles installations peuvent utiliser l’une ou l’autre de ces versions de SE invité. Le tableau suivant répertorie les publications de SE invité permettant l’installation de .NET 3.5 ou 3.5.1 sur les familles 3 et 4. Pour le moment, si une publication permet l’installation, cela signifie que le correctif MSRC ms14-046 n’y est PAS installé.

| Version du SE | Peut installer .NET 3.5 | Inclut le correctif MSRC [MS14-046][] |
| --- | --- | --- |
| Toutes les versions ultérieures du SE invité | Oui | Oui |
| WA-GUEST-OS-4.13\_201410-01 | Oui | Oui |
| WA-GUEST-OS-4.12\_201409-02 | Non | Oui |
| WA-GUEST-OS-4.12\_201409-01 | Non | Oui |
| WA-GUEST-OS-4.11\_201408-02 | Oui | Non |
| WA-GUEST-OS-4.11\_201408-01 | Non | Oui |
| WA-GUEST-OS-4.10\_201407-01 | Oui | Non |

**20 octobre 2014**: comme les versions d’août et de septembre n’ont été que partiellement déployées, veuillez tenir compte des éléments suivants :

1. Les modifications de chiffrement signalées dans Différences entre un système d’exploitation invité Azure et Windows Server par défaut n’ont pas été déployées sur l’intégralité de Microsoft Azure. Les clients qui ne sont pas encore passé aux publications d’août ou de septembre recevront ces modifications dans la publication d’octobre. 

2. Les SE invités d’août et de septembre ont été désactivés dans le portail Azure Classic. Vous ne pouvez pas les choisir manuellement. Il s’agit d’une protection contre les problèmes qui pourraient survenir si vous sélectionnez cette version de SE invité.

3. Les dates désactivées de certaines publications antérieures ont été ajustées en conséquence. Il s’agit de garantir la disponibilité continue dans le portail et la prise en charge d’au moins deux versions de SE invité publiées dans chaque famille.

## Archive de publication

### Famille 4

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ------------ | ------------ | --- |
| 4\.7 | WA-GUEST-OS-4.7\_201404-01 | 2 mai 2014 | 2 juillet 2014 | 18 août 2014 |
| 4\.6 | WA-GUEST-OS-4.6\_201403-01 | 28 mars 2014 | 9 juin 2014 | 18 août 2014 |
| 4\.5 | WA-GUEST-OS-4.5\_201402-01 | 21 mars 2014 | 21 mai 2014 | 18 août 2014 |
| 4\.4 | WA-GUEST-OS-4.4\_201401-01 | 8 février 2014 | 8 avril 2014 | 14 mai 2014 |
| 4\.3 | WA-GUEST-OS-4.3\_201312-01 | 6 janvier 2014 | 6 mars 2014 | 14 mai 2014 |
| 4\.2 | WA-GUEST-OS-4.2\_201311-01 | 12 décembre 2013 | 12 février 2014 | 14 mai 2014 |
| 4\.1 | WA-GUEST-OS-4.1\_201310-01 | 29 octobre 2013 | N/A | 14 mai 2014 |
| 4\.0 rel3 | WA-GUEST-OS-4.0\_201309-03 | 9 octobre 2013. Rendue publique le 18 octobre. | N/A | 14 mai 2014 |
 


### Famille 3

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ------------ | ------------ | --- |
| 3\.14 | WA-GUEST-OS-3.14\_201404-01 | 2 mai 2014 | 2 juillet 2014 | 18 août 2014 |
| 3\.13 | WA-GUEST-OS-3.13\_201403-01 | 28 mars 2014 | 9 juin 2014 | 18 août 2014 |
| 3\.12 | WA-GUEST-OS-3.12\_201402-01 | 21 mars 2014 | 21 mai 2014 | 18 août 2014 |
| 3\.11 | WA-GUEST-OS-3.11\_201401-01 | 8 février 2014 | 8 avril 2014 | 14 mai 2014 |
| 3\.10 | WA-GUEST-OS-3.10\_201312-01 | 6 janvier 2014 | 6 mars 2014 | 14 mai 2014 |
| 3\.9 | WA-GUEST-OS-3.9\_201311-01 | 12 décembre 2013 | 12 février 2014 | 14 mai 2014 |
| 3\.8 | WA-GUEST-OS-3.8\_201310-01 | 29 octobre 2013 | N/A | 14 mai 2014 |
| 3\.7 rel3 | WA-GUEST-OS-3.7\_201309-03 | 9 octobre 2013 | N/A | 14 mai 2014 |
| 3\.7 rel1 | WA-GUEST-OS-3.7\_201309-01 | 23 septembre 2013 | N/A | 14 mai 2014 |

### Famille 2

| Version du SE invité | Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| ---------------- | -------------------------- | ------------ | ------------ | --- |
| 2\.26 | WA-GUEST-OS-2.26\_201404-01 | 2 mai 2014 | 2 juillet 2014 | 18 août 2014 |
| 2\.25 | WA-GUEST-OS-2.25\_201403-01 | 28 mars 2014 | 9 juin 2014 | 18 août 2014 |
| 2\.24 | WA-GUEST-OS-2.24\_201402-01 | 21 mars 2014 | 21 mai 2014 | 18 août 2014 |
| 2\.23 | WA-GUEST-OS-2.23\_201401-01 | 8 février 2014 | 8 avril 2014 | 14 mai 2014 |
| 2\.22 | WA-GUEST-OS-2.22\_201312-01 | 6 janvier 2014 | 6 mars 2014 | 14 mai 2014 |
| 2\.21 | WA-GUEST-OS-2.21\_201311-01 | 12 décembre 2013 | 12 février 2014 | 14 mai 2014 |
| 2\.20 | WA-GUEST-OS-2.20\_201310-01 | 29 octobre 2013 | N/A | 14 mai 2014 |
| 2\.19 rel3 | WA-GUEST-OS-2.19\_201309-03 | 9 octobre 2013 | N/A | 14 mai 2014 |
| 2\.19 rel1 | WA-GUEST-OS-2.19\_201309-01 | 23 septembre 2013 | N/A | 14 mai 2014 |

[Installer .NET sur un rôle de service cloud]: https://azure.microsoft.com/fr-FR/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Paramètres de mise à jour du système d’exploitation invité Azure]: cloud-services-how-to-configure.md
[rss]: http://sxp.microsoft.com/feeds/3.0/msdntn/WindowsAzureOSUpdates
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[avis de sécurité Microsoft 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
 

<!---HONumber=AcomDC_0224_2016-->