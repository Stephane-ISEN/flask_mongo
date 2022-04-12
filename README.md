# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 3 : des méthodes pour manipuler MongoDB

La classe **DataAccess** étant en place, nous pouvons la compléter avec de nouvelles méthodes :
- **get_etudiants()** : qui retourne la liste complètes des étudiants, sous la forme d'une liste de documents JSON.
- **get_etudiant()** : qui prend en paramètre un id et retourne le document JSON de l'étudiant correspondant.
- **set_etudiant()** : qui prend en paramètre les données d'un étudiant pour créer un document JSON dans la base MongoDB.

Toutes ces méthodes sont des méthodes de classe.

### la méthode set_étudiant
Elle permet de créer un nouveau document *etudiant* dans la base MongoDB.
Voici le bébut de la fonction, que vous pouvez recopier :
```
    @classmethod
    def set_etudiant(cls, nom, prenom, age, classe):
        #récupère la taille de la liste de documents pour les compter à partir de 1
        taille = cls.etudiants.count_documents({})
        taille = taille+1
```

Il faut, ensuite, ajouter une variable qui contient un dictionnaire Python. La structure du dictionnaire étant la même que le JSON, ça permet de créer des documents facilement dans le code : `etudiant = {"_id":taille,...}`

Ici, on force l'**_id** pour les numérotes à partir de 1. Ainsi, le premier *etudiant* à l'**_id** 1, le deuxième l'**_id** 2 et ainsi de suite.
Vous devez, évidement, remplacer les 3 ... par le code qu'il faut pour créer un document complet à partir des paramètres de la méthode.

La dernière ligne que vous allez écrire, pour ajouter le document en base, va utiliser la méthode [insert_one()](https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html#pymongo.collection.Collection.insert_one). Consultez la documentation pour voir comment elle fonctionne. Pour l'appel de la collection, qui est une variable de classe, inspirez vous de ce qui a été fait au-dessus dans la fonction : `cls.etudiants.count_documents({})`.

### la méthode get_etudiants
Cette fonction retourne donc la liste complète des étudiants, lue en base MongoDB, sous forme de document JSON.

Créez une variable, `etudiant`par exemple, qui va contenir la liste lue en base grâce à la méthode [find()](https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html#pymongo.collection.Collection.find). Pour trouver tous les documents, vous pouvez passer en argument un dictionnaire vide **{}**. Rappelez vous que la collection est une variable de classe.

Pour le retour de la fonction, utilisez le code suivant : `return list(etudiants)`.

### la méthode get_etudiant
Cette fonction retourne le document d'un seul étudiant, sous forme JSON, trouvé à partir de son **_id**.

Pour ce faire, vous pouvez passer par la méthode [find_one()](https://api.mongodb.com/python/3.3.1/tutorial.html#getting-a-single-document-with-find-one).

### Tester les méthodes
Pour tester vos nouvelles méthodes, appelez les dans le fichier *test.py*. Vous pouvez, par exemple : 
- ajouter un nouvel étudiant avec la méthode **set_etudiant**,
- afficher la liste de tous les étudiants avec **get_etudiant**,
- aficher l'étudiant ayant 1 pour **_id** .

Pensez à vous connecter et vous déconnecter de la base, avant et après toutes ces méthodes.

Vous pouvez utiliser la méthode **pprint** (pour pretty print) de la manière suivante : `pprint.pprint(da.get_etudiants())`. Dans ce cas, pensez à importer la bibliothèque correspondante.

## La suite

Maintenant que la classe **DataAccess** fonctionne comme voulu, [nous allons l'utiliser pour un site web](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape04).
