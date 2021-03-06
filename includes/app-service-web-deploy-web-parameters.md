Azure Resource Manager vous permet de définir des paramètres pour les valeurs que vous voulez spécifier lorsque le modèle est déployé. Ce modèle inclut une section appelée Paramètres, qui contient toutes les valeurs de paramètres. Vous devez définir un paramètre pour les valeurs qui varient selon le projet que vous déployez, ou de l’environnement dans lequel vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui restent identiques. Chaque valeur de paramètre est utilisée dans le modèle pour définir les ressources déployées.

Lorsque vous définissez les paramètres, utilisez le champ **allowedValues** pour spécifier les valeurs qu'un utilisateur peut fournir au cours du déploiement. Utilisez le champ **defaultValue** pour affecter une valeur au paramètre, si aucune valeur n'est fournie pendant le déploiement.

Nous allons décrire chaque paramètre du modèle.

### siteName

Le nom de l'application web que vous souhaitez créer.

    "siteName":{
      "type":"string"
    }

### hostingPlanName

Le nom du plan App Service à utiliser pour héberger l'application web.
    
    "hostingPlanName":{
      "type":"string"
    }

### siteLocation

L'emplacement à utiliser pour créer l'application web et le plan d'hébergement. Il doit s'agir d'un des emplacements Azure qui prennent en charge les applications web.

    "siteLocation":{
      "type":"string"
    }

### sku

Le niveau de tarification du plan d'hébergement.

    "sku":{
      "type":"string",
      "allowedValues":[
        "Free",
        "Shared",
        "Basic",
        "Standard"
      ],
      "defaultValue":"Free"
    }

Le modèle définit les valeurs autorisées pour ce paramètre (Gratuit, Partagé, De base ou Standard) et affecte une valeur par défaut (Gratuit) si aucune valeur n'est spécifiée.

### workerSize

La taille d'instance du plan d'hébergement (petite, moyenne ou grande).

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }
    
Le modèle définit les valeurs autorisées pour ce paramètre (0, 1 ou 2) et affecte une valeur par défaut (0) si aucune valeur n'est spécifiée. Les valeurs correspondent à une taille petite, moyenne et grande.

<!---HONumber=Oct15_HO3-->