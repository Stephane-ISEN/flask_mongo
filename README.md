# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 6 : Ajout d'une fiche étudiante

Le site va être compléter avec une fiche étudiante, qui présente les informations d'un étudiant, sous forme HTML et sous forme JSON.

Il nous faut 2 nouvelles url : 
- `/etudiant/<id>` : qui fait appel à la fonction **get_etudiant** qui affiche la fiche étudiante HTML, à partir d'un id,
- `/etudiant/json/<id>`: qui fait appel à la fonction **json_etudiant** qui affiche la fiche étudiante JSON, à partir d'un id.

### la page etudiant.html
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
```@app.route("/etudiant/json/<int:id>")
def json_etudiant(id):
    da.connexion()
    etudiant = da.get_etudiant(id)
    da.deconnexion()

    return jsonify(etudiant), 200```

### la fonction get_etudiant()
Fonction appelée par l'url `/etudiant/<id>`, lors du clique sur le nom d'un étudiant sur la page d'accueil.

Les données arrivant par la **METHOD POST**, il faut le préciser dans le `@app.route()` et utiliser l'objet `request`pour récupérer les saisies du formulaire. vous pouvez vous inspirez de [la doc officielle](https://flask.palletsprojects.com/en/2.1.x/quickstart/#the-request-object) pour ça.

Lorsque toutes les données sont récupérées, il faut se connecter à la base, écrire en base (voir la fonction **set_etudiant()**) et se déconnecter grâce à la classe **DataAccess**.

Puis faire une redirection vers la page d'accueil en vous inspirant de [la doc de **redirect()**](https://flask.palletsprojects.com/en/2.1.x/quickstart/#redirects-and-errors).

## Les différentes étapes

Etape 6 : Ajout d'un formulaire
