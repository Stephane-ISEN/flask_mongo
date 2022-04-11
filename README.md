# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.


## Etape 6 : Ajout d'un formulaire

On va ajouter une dernière page, un formulaire d'inscription pour de nouveaux élèves.

Il nous faut 2 nouvelles url : 
- `/etudiant/inscription` : qui fait appel à la fonction **add_etudiant** qui affiche le formulaire,
- `/etudiant/create`: qui fait appel à la fonction **create_etudiant** reçoit toutes les infos du formulaire, par une **METHOD POST**, les sauves en base et redirige vers la page d'accueil.


### la page inscription.html
dans le répertoire `\templates`, ajoutez la page *inscription.html*, dont voici un exemple :

![page d'inscription](/ressources/flaskmongo_form.png)

Pour que le formulaire fonctionne bien, i lfaut faire attention à :
- ajouter une url dans l'**ACTION** de la balise **FORM** et **POST** comme **METHOD** : `<form id="formulaire" action="{{url_for('create_etudiant')}}" method="post">`,
- avoir un **BUTTON** de type **SUBMIT** : `<button id="bouton" type="submit">Inscrire</button>`,
- ajouter un **INPUT** pour saisir le nom, qui doit absolument avoir un paramètre **NAME** : `<input type="text" id="nom" name="nom" placeholder="Nom" required autofocus>`,
- faire de même pour les champ *prénom*, *classe* et *âge*,
- et un lien vers la page d'accueil.

Si vous avez besoin de plus d'information sur les formulaires : [le site MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Form).

Vous pouvez faire un peu de CSS si vous voulez améliorer le rendu de la page.

**Pensez à mettre à jour le lien vers l'inscription sur la page d'accueil !**


### La fonction add_etudiant()
Fonction appelée par l'url `/etudiant/inscription`.

Dans *app.py*, il faut ajouter la fonction add_etudiant() qui retourne la page *inscription.html*.


### la fonction create_etudiant()
Fonction appelée par l'url `/etudiant/create`, lors de la validation du formulaire de la page *inscription.html*.

Les données arrivant par la **METHOD POST**, il faut le préciser dans le `@app.route()` et utiliser l'objet `request`pour récupérer les saisies du formulaire. vous pouvez vous inspirez de [la doc officielle](https://flask.palletsprojects.com/en/2.1.x/quickstart/#the-request-object) pour ça.

Lorsque toutes les données sont récupérées, il faut se connecter à la base, écrire en base (voir la fonction **set_etudiant()**) et se déconnecter grâce à la classe **DataAccess**.

Puis faire une redirection vers la page d'accueil en vous inspirant de [la doc de **redirect()**](https://flask.palletsprojects.com/en/2.1.x/quickstart/#redirects-and-errors).


## Les différentes étapes

Etape 6 : Ajout d'un formulaire
