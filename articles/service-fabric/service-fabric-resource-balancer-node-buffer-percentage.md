<properties
   pageTitle="Pourcentage de mémoire tampon de nœud | Microsoft Azure"
   description="Présentation du rôle du pourcentage de mémoire tampon de nœud dans l’équilibreur de ressources"
   services="service-fabric"
   documentationCenter=".net"
   authors="GaugeField"
   manager="timlt"
   editor=""/>

<tags
   ms.service="Service-Fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="09/03/2015"
   ms.author="masnider"/>

# Présentation du pourcentage de mémoire tampon de nœud

Actuellement, les clients peuvent spécifier une limite de capacité du nœud comme contrainte que l’équilibreur de ressources respecte selon la priorité de la contrainte. Si la priorité de contrainte de capacité est élevée (la capacité du nœud ne peut pas être ignorée) et si les nœuds de cluster sont très sollicités, il peut arriver que basculement ne soit pas immédiat ou que la capacité du nœud ne soit pas respectée.

Des problèmes peuvent se produire si des nœuds avec des réplicas secondaires approchent de la capacité de nœud quand un nœud avec le réplica principal tombe en panne. Dans ce cas, si la charge principale est supérieure à la charge secondaire, le réplica secondaire ne peut pas être promu immédiatement sans sollicitation excessive du nœud ou copie du réplica.

Si une logique de compression proactive est en cours d’exécution, davantage de nœuds de cluster seront proches de la limite de capacité de nœud. Le pourcentage de mémoire tampon de nœud est une fonctionnalité qui empêche l’augmentation du temps de basculement ou la sollicitation excessive du nœud pendant le basculement, en fournissant aux clients la possibilité de spécifier le pourcentage du nœud qui doit rester libre. Les réplicas des nouveaux services ne doivent pas être ajoutés à l’espace de mémoire tampon de nœud, mais l’équilibreur de ressources doit être en mesure d’utiliser la capacité totale du nœud (en tenant compte de l’espace de mémoire tampon) pour les basculements et l’ajout des réplicas manquants.

Cette fonctionnalité peut être utilisée même lorsque la fonctionnalité de compression de mesure proactive est désactivée.

L’exemple de code ci-dessous montre que les pourcentages de mémoire tampon de nœud pour les mesures sont configurés par mesure à l’aide de l’élément FabricSettings dans le manifeste de cluster.

``` xml
<FabricSettings>
  <Section Name=" NodeBufferPercentage">
    <Parameter Name="MetricName" Value="0.1"/>
  </Section>
</FabricSettings>

```

La valeur 0,1 pour la mesure nommée « MetricName » signifie que 10 % de la capacité de chaque nœud pour la mesure « MetricName » doivent rester libres.

Si la valeur n’est pas spécifiée dans cette section, 0 sera utilisé comme valeur par défaut.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## Étapes suivantes

Pour plus d’informations : [Architecture de l’équilibreur de ressources](service-fabric-resource-balancer-architecture.md)

<!---HONumber=AcomDC_1223_2015-->