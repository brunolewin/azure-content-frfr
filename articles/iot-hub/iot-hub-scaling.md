<properties
 pageTitle="Mise à l’échelle Azure IoT Hub | Microsoft Azure"
 description="Décrit comment mettre à l’échelle Azure IoT Hub."
 services="iot-hub"
 documentationCenter=""
 authors="fsautomata"
 manager="timlt"
 editor=""/>

<tags
 ms.service="iot-hub"
 ms.devlang="na"
 ms.topic="article"
 ms.tgt_pltfrm="na"
 ms.workload="na"
 ms.date="01/20/2016"
 ms.author="elioda"/>

# Mise à l’échelle IoT Hub

Azure IoT Hub peut prendre en charge jusqu’à un million d’appareils connectés simultanément, en augmentant le nombre d’unités de niveau IoT Hub S1 ou d’unités de niveau S2 jusqu’à 2 000. Pour plus d’informations, consultez la [tarification IoT Hub][lnk-pricing].

Chaque unité IoT Hub autorise un certain nombre d’appareils dans le registre. Ces appareils peuvent tous être connectés simultanément. Chaque unité autorise également un certain nombre de messages quotidiens.

Pour mettre correctement à l’échelle votre solution, étudiez votre utilisation particulière d’IoT Hub. Prenez plus particulièrement en compte le débit maximal requis pour les catégories d’opérations suivantes :

* Messages Appareil vers cloud
* Messages Cloud vers appareil
* Opérations du registre d’identité

Outre ces informations sur le débit, consultez les [quotas et limitations IoT Hub][] et concevez votre solution en conséquence.

## Débit de message Appareil vers cloud et Cloud vers appareil.

La meilleure façon de dimensionner une solution IoT Hub consiste à évaluer le trafic sur une base par unité.

Les messages Appareil vers cloud respectent les recommandations de débit soutenu.

| Niveau | Débit soutenu | Vitesse de transmission soutenue |
| ---- | -------------------- | ------------------- |
| S1 | Jusqu'à 1 111 Ko/minute par unité<br/>(1,5 Go/jour/unité) | Moyenne de 278 messages/minute par unité<br/>(400 000 messages/jour par unité) |
| S2 | Jusqu'à 16 Mo/minute par unité<br/>(22,8 Go/jour/unité) | Moyenne de 4 167 messages/minute par unité<br/>(6 millions de messages/jour par unité) |

La performance des échelles des messages Cloud vers appareil, où chaque appareil reçoit jusqu’à 5 messages par minute.

## Débit des opérations de registre d’identité

Les opérations de registre d’identité IoT Hub ne sont pas censées être des opérations d’exécution, car elles sont principalement liées à la configuration d’appareils.

Pour obtenir les pics de performances spécifiques, consultez [Quotas et limitations IoT Hub][].

## Partitionnement

Un hub IoT unique peut recevoir des millions d’appareils, mais votre solution nécessite parfois des caractéristiques de performances spécifiques qu’un seul hub IoT ne peut pas assurer. Dans ce cas, il est recommandé de partitionner vos appareils en plusieurs IoT hubs. L’utilisation de plusieurs IoT Hubs permet de simplifier les pics de trafic et d’obtenir le débit requis ou les taux d’opération requis.

## Étapes suivantes

Suivez ces liens pour en savoir plus sur Azure IoT Hub :

- [Prise en main d'IoT Hub (didacticiel)][lnk-get-started]
- [Qu’est-ce qu’Azure IoT Hub ?][]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[quotas et limitations IoT Hub]: iot-hub-devguide.md#throttling

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[Qu’est-ce qu’Azure IoT Hub ?]: iot-hub-what-is-iot-hub.md

<!---HONumber=AcomDC_0128_2016-->