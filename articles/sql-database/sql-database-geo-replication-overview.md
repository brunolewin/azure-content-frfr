<properties
	pageTitle="Géo-réplication active pour la base de données SQL Azure"
	description="Cette rubrique explique la géo-réplication active pour la base de données SQL et comment l’utiliser."
	services="sql-database"
	documentationCenter="na"
	authors="rothja"
	manager="jeffreyg"
	editor="monicar" />


<tags
	ms.service="sql-database"
	ms.devlang="na"
	ms.topic="article"
	ms.tgt_pltfrm="na"
	ms.workload="data-management"
	ms.date="10/21/2015"
	ms.author="jroth" />

# Géo-réplication active pour la base de données SQL Azure

## Vue d'ensemble
La fonctionnalité de géo-réplication active implémente un mécanisme pour assurer la redondance de base de données dans une même région Microsoft Azure ou dans différentes régions (géo-redondance). La géo-réplication active réplique de manière asynchrone les transactions validées à partir d’une base de données sur jusqu’à quatre copies de la base de données sur des serveurs différents. La base de données d’origine devient la base de données primaire de la copie continue. Chaque copie continue est désignée sous le terme de base de données secondaire en ligne. La base de données primaire réplique de manière asynchrone les transactions validées sur chaque base de données secondaire en ligne. À un moment donné, les données secondaires en ligne peuvent être légèrement retardées derrière la base de données primaire, mais la cohérence transactionnelle des données secondaires en ligne avec les modifications apportées à la base de données primaire est garantie. La géo-réplication active prend en charge jusqu’à quatre bases secondaires en ligne, ou trois bases secondaires en ligne et une base secondaire hors ligne.

L’un des principaux avantages de la géo-réplication active, c’est qu’elle fournit une solution de récupération d’urgence au niveau de la base de données. Grâce à la géo-réplication active, vous pouvez configurer une base de données utilisateur dans le niveau de service Premium pour répliquer des transactions sur des bases de données résidant sur différents serveurs de base de données SQL Microsoft Azure dans des régions identiques ou différentes. Grâce à la redondance entre régions, les applications peuvent récupérer d’une perte permanente d’un centre de données provoquée par des catastrophes naturelles, de graves erreurs humaines ou des actes de malveillance.

Autre avantage clé : les bases de données secondaires en ligne sont lisibles. Par conséquent, une base de données secondaire en ligne peut agir en tant qu’équilibreur de charge pour les charges de travail de lecture, comme les rapports. Vous pouvez créer une base de données secondaire en ligne dans une région différente pour une récupération d’urgence, mais vous pouvez aussi disposer d’une base de données secondaire en ligne dans la même région ou sur un autre serveur. Les deux bases de données secondaires en ligne peuvent servir à équilibrer les charges de travail en lecture seule servant des clients répartis entre plusieurs régions.

Autres scénarios dans lesquels la géo-réplication active peut être utilisée :

- **Migration de base de données** : la géo-réplication active permet de migrer une base de données d’un serveur à un autre serveur en ligne avec un temps d’arrêt minimal.
- **Mises à niveau d’applications** : vous pouvez utiliser la base de données secondaire en ligne comme option de restauration automatique.

Pour assurer vraiment la continuité des activités, l’ajout de redondance au stockage relationnel entre les centres de données n’est qu’une partie de la solution. La récupération d’une application (service) de bout en bout après un sinistre implique la récupération de tous les composants qui constituent le service et tous les services dépendants. En voici quelques exemples : logiciel client (il peut s’agir par exemple d’un navigateur avec un code JavaScript personnalisé), serveurs web frontaux, ressources de stockage et DNS. Il est essentiel que tous les composants résistent aux mêmes défaillances et redeviennent disponibles dans l’objectif de délai de récupération (RTO) de votre application. Par conséquent, vous devez identifier tous les services dépendants et comprendre les garanties et les fonctionnalités qu’ils fournissent. Ensuite, vous devez prendre les mesures appropriées pour vous assurer que votre service fonctionne pendant le basculement des services dont il dépend. Pour plus d’informations sur la conception de solutions pour la récupération d’urgence, consultez la section [Conception de solutions cloud pour la récupération d’urgence à l’aide de la géo-réplication active](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## Fonctionnalités de géo-réplication active
La fonctionnalité de géo-réplication active fournit les capacités essentielles suivantes :

- **Réplication asynchrone automatique** : après qu’une base de données secondaire en ligne a été amorcée, les mises à jour de la base de données primaire sont copiées automatiquement de manière asynchrone sur la base de données secondaire en ligne. Cela signifie que les transactions sont validées sur la base de données primaire avant qu’elles ne soient copiées dans la base de données secondaire en ligne. Toutefois, après l’amorçage, la cohérence transactionnelle de la base de données secondaire en ligne est assurée en permanence. 

	>[AZURE.NOTE]La réplication asynchrone permet la latence caractéristique des réseaux étendus via lesquels les centres de données distants sont connectés.

- **Plusieurs bases de données secondaires en ligne** : au moins deux bases de données secondaires en ligne améliorent la redondance et la protection de la base de données primaire et de l’application. Si plusieurs bases de données secondaires en ligne existent, l’application restera protégée même en cas d’échec de l’une des bases de données secondaires en ligne. En cas d’échec d’une base de données secondaire en ligne unique, l’application est exposée à un risque plus élevé jusqu’à la création d’une nouvelle base de données secondaire en ligne.

- **Bases de données secondaires en ligne lisibles** : une application peut accéder à une base de données secondaire en ligne pour les opérations en lecture seule avec les mêmes entités de sécurité que celles utilisées pour accéder à la base de données primaire. Les opérations de copie continue sur la base de données secondaire en ligne sont prioritaires sur l’accès aux applications. En outre, si les requêtes sur la base de données secondaire en ligne provoquent un verrouillage de table prolongé, les transactions pourraient finir par échouer sur la base de données primaire.

- **Arrêt contrôlé par l’utilisateur pour le basculement** : avant de pouvoir basculer une application vers une base de données secondaire en ligne, la relation de copie continue avec la base de données principale doit être interrompue. L’arrêt de la relation de copie continue nécessite une action explicite de l’application ou un script d’administration ou une opération manuelle via le portail. Après l’arrêt, la base de données secondaire en ligne devient une base de données autonome. Elle devient une base de données en lecture-écriture, sauf si la base de données principale était en lecture seule. Deux formes d’[arrêt de la relation de copie continue](#termination-of-a-continuous-copy-relationship) sont décrites plus loin dans cette rubrique.

>[AZURE.NOTE]La géo-réplication active est uniquement prise en charge pour les bases de données dans le niveau de service Premium. Cela s’applique à la fois pour la base de données primaire et pour les bases de données secondaires en ligne. La base de données secondaire en ligne doit être configurée avec un niveau de performances identique ou supérieur à celui de la base de données primaire. Les modifications apportées aux niveaux de performance dans la base de données primaire ne sont pas automatiquement répliquées sur les bases de données secondaires. Toutes les mises à niveau doivent être effectuées sur les bases de données secondaires dans un premier temps, puis sur la base de données primaire. Pour plus d’informations sur la modification des niveaux de performances, consultez la rubrique [Passage d’un niveau de performances à un autre](sql-database-scale-up.md). La base de données secondaire en ligne doit avoir une taille au moins identique à celle de la base de données primaire pour deux raisons principales. La base de données secondaire doit avoir une capacité suffisante pour traiter les transactions répliquées à la même vitesse que la base de données primaire. Si la base de données secondaire n’a pas au moins la même capacité pour traiter les transactions entrantes, elle risquerait d’être retardée et d’affecter au final la disponibilité de la base de données primaire. Si la base de données secondaire n’a pas la même capacité que la base de données primaire, le basculement risque de dégrader les performances et la disponibilité de l’application.

## Concepts de la relation de copie continue
La redondance des données en local et la récupération opérationnelle sont des fonctionnalités standard de la base de données SQL Azure. Chaque base de données possède une base de données primaire et deux bases de données réplicas en local qui résident sur le même centre de données, offrant une haute disponibilité au sein de ce centre de données. Cela signifie que les bases de données de géo-réplication active ont également des réplicas redondants. La base de données primaire comme les bases de données secondaires en ligne possèdent deux réplicas secondaires. Toutefois, le réplica principal de la base de données secondaire est mis à jour directement par le mécanisme de copie continue et ne peut pas accepter les mises à jour initiées par l’application. La figure suivante illustre comment la géo-réplication active étend la redondance de la base de données entre deux régions Azure. La région qui héberge la base de données primaire est désignée sous le terme de région primaire. La région qui héberge la base de données secondaire est désignée sous le terme de région secondaire. Dans cette figure, l’Europe du Nord est la région primaire. L’Europe de l’Ouest est la région secondaire.

![Relation de copie continue](./media/sql-database-active-geo-replication/continuous-copy-relationships.gif)

Si la base de données primaire devient indisponible, l’arrêt de la relation de copie continue sur une base de données secondaire en ligne transforme cette base secondaire en une base de données autonome. La base de données secondaire en ligne hérite du mode lecture seule/lecture-écriture de la base de données primaire non affectée par l’arrêt. Par exemple, si la base de données primaire est une base de données en lecture seule, après l’arrêt, la base de données secondaire en ligne devient une base de données en lecture seule. À ce stade, l’application peut basculer et continuer à utiliser la base de données secondaire en ligne. Pour fournir une résilience en cas de sinistre sur le centre de données ou de panne prolongée dans la région primaire, au moins une base de données secondaire en ligne doit résider dans une autre région.

## Création d’une copie continue
Vous pouvez uniquement créer une copie continue d’une base de données existante. La création d’une copie continue d’une base de données existante est utile pour l’ajout de géo-redondance. Une copie continue peut également être créée pour copier une base de données existante vers un autre serveur de base de données SQL Azure. Une fois créée, la base de données secondaire est remplie avec les données copiées à partir de la base de données primaire. Ce processus est appelé amorçage. Une fois l’amorçage terminé, chaque nouvelle transaction est répliquée après avoir été validée sur la base de données primaire.

Pour plus d’informations sur la création d’une copie d’une base de données existante, consultez la section [Activation de la géo-réplication](sql-database-business-continuity-design.md#how-to-enable-geo-replication).

## Prévention de la perte de données critiques
En raison de la latence élevée des réseaux étendus, la copie continue utilise un mécanisme de réplication asynchrone. La perte de certaines données reste donc inévitable en cas de défaillance. Or, pour certaines applications, une perte de données est inacceptable. Pour protéger ces mises à jour critiques, un développeur d’applications peut appeler la procédure système [sp\_wait\_for\_database\_copy\_sync](https://msdn.microsoft.com/library/dn467644.aspx) immédiatement après la validation de la transaction. L’appel de **sp\_wait\_for\_database\_copy\_sync** bloque le thread appelant jusqu’à ce que la dernière transaction validée ait été répliquée sur la base de données secondaire en ligne. La procédure attend que toutes les transactions en file d’attente aient été acceptées par la base de données secondaire en ligne. **sp\_wait\_for\_database\_copy\_sync** est limitée à une relation de copie continue spécifique. Tout utilisateur disposant de droits de connexion à la base de données primaire peut appeler cette procédure.

>[AZURE.NOTE]Le délai provoqué par un appel de procédure **sp\_wait\_for\_database\_copy\_sync** peut être significatif. Ce délai dépend de la longueur de la file d’attente et de la bande passante disponible. Évitez d’appeler cette procédure, sauf si cela est absolument nécessaire.

## Arrêt d’une relation de copie continue
La relation de copie continue peut être arrêtée à tout moment. L’arrêt d’une relation de copie continue ne supprime pas la base de données secondaire. Il existe deux méthodes pour arrêter une relation de copie continue :

- L’**arrêt planifié** est utile pour les opérations planifiées pour lesquelles une perte de données est inacceptable. Un arrêt planifié peut uniquement être effectué sur la base de données primaire, une fois que la base de données secondaire en ligne a été amorcée. Dans un arrêt planifié, toutes les transactions validées sur la base de données primaire sont répliquées sur la base de données secondaire en ligne dans un premier temps, puis la relation de copie continue est arrêtée. Cela évite la perte de données sur la base de données secondaire.
- L’**arrêt non planifié (forcé)** vise à répondre soit à la perte de la base de données primaire, soit à celle de l’une de ses bases de données secondaires en ligne. Un arrêt forcé peut être effectué soit sur la base de données primaire, soit sur la base de données secondaire. Il résulte de chaque arrêt forcé la perte irréversible de la relation de réplication entre la base de données primaire et la base de données secondaire en ligne associée. En outre, un arrêt forcé provoque la perte de toutes les transactions qui n’ont pas été répliquées à partir de la base de données primaire. Un arrêt forcé provoque l’arrêt immédiat de la relation de copie continue. Les transactions en cours ne sont pas répliquées sur la base de données secondaire en ligne. Par conséquent, un arrêt forcé peut entraîner la perte irréversible de toutes les transactions qui n’ont pas été répliquées à partir de la base de données primaire.

>[AZURE.NOTE]Si la base de données primaire n’a qu’une seule relation de copie continue, après l’arrêt, les mises à jour apportées à la base de données primaire ne seront plus protégées.

Pour plus d’informations sur la façon de mettre fin à une relation de copie continue, consultez la section [Récupérer une base de données SQL Azure en cas de défaillance](sql-database-disaster-recovery.md).

## Étapes suivantes
Pour plus d’informations sur les fonctionnalités de géo-réplication active et de poursuite d’activité supplémentaire de la base de données SQL, consultez [Vue d’ensemble de la continuité des activités métier](sql-database-business-continuity.md).

<!---HONumber=AcomDC_0121_2016-->
