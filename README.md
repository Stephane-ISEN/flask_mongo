# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 1 : préparer la base MongoDB
nous allons commencer à mettre en place le code Python pour travailler avec MongoDB. Pour ça, dans un nouveau projet, créons 2 fichiers :
- *data.py* : qui va contenir une classe pour se connecter à MongoDB,
- *test.py* : code test de la classe.

### la classe DataAccess
dans le fichier *data.py*, créez une classe de nom **DataAccess**. 

Commencez par déclarer les variables de classe suivantes : 
```    
    user = "root"
    mdp = "pass12345"
    serveur = "127.0.0.1"
    port = "27018"
    db_name = "ecole"
    collection_name = "etudiants"
```

Comme vous pouvez le voir, ce sont les paramètres de connection. Pensez à les personnaliser, suivant votre base.

Nous allons maintenant ajouter une méthode qui va permettre la connexion à la base MongoDB. Puisqu'on a besoin que d'une seule connexion dans le programme, on ne créera pas d'instance d'objet. Il est plus simple de passer par une méthode de classe, déclarée par le décorateur `@classmethod`. Il faut aussi penser à passer la classe en paramètre, grâce à la variable `cls`.

Voici la méthode de classe **connexion()** :
```
    # méthode de classe
    @classmethod
    def connexion(cls) :
        #connexion à la base mongo
        cls.client = MongoClient(f"mongodb://{cls.user}:{cls.mdp}@{cls.serveur}:{cls.port}")

        # variable de classe qui représente la BDD
        cls.db = cls.client[cls.db_name]
        # variable de classe qui représente la collection
        cls.etudiants = cls.db[cls.collection_name]
```

Sur la même idée, vous pouvez ajouter une méthode de classe pour la déconnexion :
```
    # méthode de classe
    @classmethod
    def deconnexion(cls) :
        #il suffit de fermer le client
        cls.client.close()
```

### le fichier test.py

Il ne reste plus qu'à tester la connexion en écrivant un petit code dans *test.py*.
```
from data import DataAccess as da

# méthodes de classe, pas besoin de créer d'objet
da.connexion()

da.deconnexion()
# s'il n'y a pas de message d'erreur dans la console c'est que la connexion est ok
```

Comme écrit dans le code, s'il n'y a pas de message d'erreur dans la console, c'est que la connexion est bonne.

## La suite

Il faut enrichir la classe **DataAccess** [avec des méthodes pour requêter la base MongoDB](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape03).
