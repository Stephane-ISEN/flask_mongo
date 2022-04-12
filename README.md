# Exercice Flask et Mongo

Ce petit exercice à pour but d'afficher sur des pages web, générées par Flask, des données issues d'une base MongoDB.

## Etape 1 : préparer la base MongoDB

Connectez vous à votre base Mongo dans votre conteneur.

Affichez toutes les bases avec la commande : `show dbs`

Si il a déjà une base nommée *ecole*, supprimez la de la façon suivante :
```
use ecole;
db.dropDatabase();
```

Créez une nouvelles base : `use ecole`

ajouter un document : `db.etudiants.insert({_id:1, nom:"Granger", prenom:"Hermione", age:16, classe:"première"});`

Comme vous le savez déjà, cette commande génère la collection **etudiants** et le document passé en argument.

Vous pouvez quitter la base.

### la forme du document
Même si Mongo est shemaless, nous allons respecter ce format de document pour nos étudiants :
```
{
    _id : 1,
    nom : "",
    prenom : "",
    age : 0,
    classe : ""
}
```

## La suite

[On attaque le code Python](https://github.com/Stephane-ISEN/flask_mongo/tree/Etape02).
