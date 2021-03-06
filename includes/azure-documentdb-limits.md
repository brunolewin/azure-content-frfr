=======
Entité|Quota (offre standard)
---|---
Comptes de base de données*|5
Nombre de bases de données par compte de base de données|100
Nombre d'utilisateurs par compte de base de données (pour l'ensemble des bases de données)|500 000
Nombre d'autorisations par compte de base de données (pour l'ensemble des bases de données)|2 000 000
Stockage de pièces jointes par compte de base de données (fonctionnalité préliminaire)|2 Go
Nombre maximal d'unités de demande par seconde par collection|2 500
Nombre de procédures stockées, déclencheurs et fonctions définies par l'utilisateur par collection* |25 de chaque
Délai maximal d'exécution pour les procédures stockées et déclencheurs|5 secondes
Stockage/collection de documents configuré|10 Go
Nombre maximal de collections par compte de base de données*|100
Quantité maximale de stockage de documents par base de données (100 collections)* |1 To
Longueur maximale de la propriété d'ID|255 caractères
Nombre maximal d'éléments par page|Aucune limite pratique
Taille de demande maximale des documents et pièces jointes |512 Ko
Taille maximale des procédures stockées, déclencheurs et fonctions définies par l'utilisateur|100 KO
Taille de réponse maximale|1 Mo
Chaîne|Toutes les chaînes doivent être au format UTF-8. Étant donné qu'UTF-8 est un codage de largeur variable, les tailles de chaîne sont déterminées à l'aide d'octets UTF-8.
Longueur maximale de la propriété ou valeur|Aucune limite pratique
Nombre maximal de fonctions définies par l'utilisateur par requête* |2
Nombre maximal de clauses JOIN par requête* |5
Nombre maximal de clauses AND par requête* |20
Nombre maximal de clauses OR par requête* |20
Nombre maximal de valeurs par expression IN* |200
Nombre maximal de points dans un argument de polygone dans une requête ST\_WITHIN* |16
Nombre maximal de créations de collection par minute* |5
Nombre maximal d'opérations de mise à l'échelle par minute* |5

Les quotas marqués d'un astérisque (*) [peuvent être ajustés en contactant le support Azure](../articles/documentdb/documentdb-increase-limits.md).

<!---HONumber=AcomDC_0302_2016-->