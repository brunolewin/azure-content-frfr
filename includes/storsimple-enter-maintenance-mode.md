<!--author=SharS last changed: 12/01/15-->

#### Pour passer en mode Maintenance

1. Dans le menu de la console série, sélectionnez l’option 1, **Ouvrir une session avec un accès total**.

2. Saisissez le mot de passe. Le mot de passe par défaut est **Password1**.

3. À l'invite de commandes, tapez

     `Enter-HcsMaintenanceMode`

4. Un message d’avertissement s’affiche pour vous indiquer que le mode Maintenance va perturber toutes les demandes d’E/S et annuler la connexion au portail Azure Classic. Vous êtes invité à confirmer l’opération. Saisissez **O** pour passer en mode Maintenance.

    Les deux contrôleurs redémarrent. Une fois le redémarrage terminé, un autre message s’affiche pour indiquer que l’appareil est en mode Maintenance.

<!---HONumber=AcomDC_1203_2015-->