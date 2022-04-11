# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 4 : Flask avec une page d'accueil

La classe **DataAccess** étant en place, nous pouvons développer notre site web qui va afficher les données sous format HTML.

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
