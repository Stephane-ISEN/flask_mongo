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

### la méthode get_étudiants
Cette fonction retourne donc la liste complète des étudiants, lue en base MongoDB, sous forme de document JSON.

Créez une variable, `etudiant`par exemple, qui va contenir la liste lue en base grâce à la méthode [find()](https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html#pymongo.collection.Collection.find). Pour trouver tous les documents, vous pouvez passer en argument un dictionnaire vide **{}**. Rappelez vous que la collection est une variable de classe.

Pour le retour de la fonction, utilisez le code suivant : `return list(etudiants)`.





Commencez par étoffer le projet pour qu'il ressemble à ça : 

![Projet](/ressources/flaskmongo_projet.png)

Pour mémoire : 
- le répertoire */static* est destiné à recevoir les fichiers statiques comme le css, les iamges...
- le répertoire */templates* est destiné à recevoir les fichiers HTML et
- le fichier *app.py* contient le code du serveur web,
- le fichier *data.py*, que vous avez déjà codé, contient la classe de connexion à MongoDB **DataAccess*,
- le ficher *test.py*, n'est plus utile à partir de cette étape.

### le fichier app.py
Voici la structure de votre fichier *app.py* :
```
from flask import Flask, render_template

#création d'un serveur web Python
app = Flask(__name__)

#a compléter pour afficher la page d'accueil
@app.route("/")
def index():

    return render_template()

#démarre automatiquement le serveur
if __name__ == "__main__" :
    app.run(debug=True)
```


### La fonction index()
Cette fonction doit aller lire en base Mongo les documents de tous les étudiants et afficher la page *index.html*.

Il faut donc la compléter pour :
- ouvrir la connexion à la base Mongo grâce à la classe **DataAccess**,
- appeler la méthode **get_etudiants()** de la classe **DataAccess** et récupérer la liste des documents dans une variable,
- fermer la connexion en utilisant encore la classe **DataAccess**,
- compléter le **render_template()** pour retourner la page *index.html* et lui passer en paramètre la variable qui contient la liste des documents.

[La documentation de Flask](https://flask.palletsprojects.com/en/2.1.x/quickstart/#rendering-templates) devrait vous aider pour ce dernier point.

Pour l'utilisation de la classe **DataAccess**, inspirez-vous du fichier *test.py*.

Inutile de démarrer le serveur tant qu'on a pas ajouter la page *index.html*.

### la page index.html
dans le répertoire `\templates`, ajoutez la page *etudiant.html*, dont voici un exemple :

![Accueil](/ressources/flaskmongo_index.png)

La liste des étudiants, apparaissant sur cette page, est générée dynamiquement à partir de la liste de documents passé en paramètre par le **render_template()** de la fonction **index()**.

Pour parcourir une liste en Python, il faut faire une boucle **FOR**. Elle est décrire dans [cette documentation](https://jinja.palletsprojects.com/en/3.1.x/templates/#for).

Les liens seront complétés au fur et mesure des étapes suivantes.

Vous pouvez faire un peu de CSS si vous voulez améliorer le rendu de la page. Le fichier doit alors être placé dans le répertoire */static*.
Pour que le style soit appliqué à la page, ajoutez la ligne suivante dans la balise **HEAD** : `<link rel="stylesheet" href="{{???}}">`

Il faut, évidement, écrire le bon code à la place des ???. [La doc officielle devrait vous aider](https://flask.palletsprojects.com/en/2.1.x/quickstart/#static-files).

## La suite

Nous allons ajouter [la fiche des étudiants](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape05) au site web.
