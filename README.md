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

### la page index.html
dans le répertoire `\templates`, ajoutez la page *etudiant.html*, dont voici un exemple :

![Fiche d'un étudiant](/ressources/flaskmongo_fiche.png)

Pour que la page s'affiche bien, il faut faire attention à :
- lui passer une variable, `contenu`par exemple, qui contient le document JSON de l'étudiant,
- insérer les données sur la page à partir de cette variable. En faisant, pour le prénom, par exemple : `{{contenu["prenom"]}}`,
- ajouter un lien vers la fiche JSON : `<a href="{{url_for('json_etudiant', id=contenu['_id'])}}" id="json" target="_blank">format JSON</a>`,
- rendre cliquable les noms des étudiants de la page d'accueil, en vous inspirant du code donné au-dessus,
- et un lien vers la page d'accueil.

Vous pouvez faire un peu de CSS si vous voulez améliorer le rendu de la page.

### La fonction json_etudiant()
Fonction appelée par l'url `/etudiant/json/<id>`, lors du clique sur le lien *Format JSON*.

Dans *app.py*, ajoutez la fonction suivante :

```
@app.route("/etudiant/json/<int:id>")
def json_etudiant(id):
    da.connexion()
    etudiant = da.get_etudiant(id)
    da.deconnexion()

    return jsonify(etudiant), 200 
```

Cette fonction récupère l'id de l'étudiant dans l'url, typé **int**, se connecte à la base, retrouve le document de l'étudiant, ferme la base et affiche les données sous forme JSON grâce à la fontion **jsonify**. Pour que tout marche bien, il faut importer cette dernière fonction à partir de Flask.

Lorsque le code est en place, il est possible d'afficher le JSON dans le navigateur :

![fiche JSON](/ressources/flaskmongo_json.png)

### la fonction get_etudiant()
Fonction appelée par l'url `/etudiant/<id>`, lors du clique sur le nom d'un étudiant de la page d'accueil.

En vous inspirant du code de **json_etudiant()** codez la fonction **get_etudiant**, dans *app.py*. Cette fonction : 
- récupère l'id de l'étudiant dans l'url,
- se connecte à la base de donnée pour trouver le document correspondant à l'id,
- retourne la page *etudiant.html* et lui passe le document en paramètre.

## La suite

Il ne reste plus qu'à [ajouter un formulaire](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape06) au site web.
