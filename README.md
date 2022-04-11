# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 4 : Flask avec une page d'accueil

La classe **DataAccess** étant en place, nous pouvons développer notre site web qui va afficher les données sous format HTML.

Commencez par étoffer le projet pour qu'il ressemble à ça : 

![Projet](/ressources/flaskmongo_projet.png)

Pour mémoire : 
- le répertoire *static* est destiné à recevoir les fichiers statiques comme le css, les iamges...
- le répertoire *templates* est destiné à recevoir les fichiers HTML et
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

Pour que la page s'affiche bien, il faut faire attention à :
- lui passer une variable, `contenu`par exemple, qui contient le document JSON de l'étudiant,
- insérer les données sur la page à partir de cette variable. En faisant, pour le prénom, par exemple : `{{contenu["prenom"]}}`,
- ajouter un lien vers la fiche JSON : `<a href="{{url_for('json_etudiant', id=contenu['_id'])}}" id="json" target="_blank">format JSON</a>`,
- rendre cliquable les noms des étudiants de la page d'accueil, en vous inspirant du code donné au-dessus,
- et un lien vers la page d'accueil.

Vous pouvez faire un peu de CSS si vous voulez améliorer le rendu de la page.

## La suite

Il ne reste plus qu'à [ajouter un formulaire](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape06) au site web.
