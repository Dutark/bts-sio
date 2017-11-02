# TodoList : (Ré-)écrire les API du projet

Le But de notre application est de créer des API Rest qui vont exposer la gestion de nos ```todos``` défini en base de données

<!-- TOC -->

- [TodoList : (Ré-)écrire les API du projet](#todolist--ré-écrire-les-api-du-projet)
    - [Introduction](#introduction)
    - [Création du projet](#création-du-projet)
    - [Installer Lumen](#installer-lumen)
    - [Créer le nouveau Projet](#créer-le-nouveau-projet)
    - [Initialisation](#initialisation)
    - [Tester votre application](#tester-votre-application)
    - [Gestion de la bose de données](#gestion-de-la-bose-de-données)
        - [Le script de création / migration](#le-script-de-création--migration)
    - [Déclarer les routes](#déclarer-les-routes)

<!-- /TOC -->

## Introduction

Dans ce TP nous allons voir la création d’API pour le projet « TodoList ». Nous allons donc créer un nouveau projet avec Laravel pour créer des API qui permettront de :

- Lister les éléments dans la TodoList.
- Créer un nouvel élément dans la TodoList.
- Marquer un élément comme ```terminer```.
- Supprimer un élément.

## Création du projet

Pour créer des API Laravel est un peu « lourd » (dans notre cas, dans certains cas se choix est complètement justifié). Nous allons donc utiliser son petit frère Lumen. Lumen est un micro-framework reprenant les concepts de Laravel (et les même briques). Mais en beaucoup plus petit et donc plus adaptés à des micro-projets comme celui-ci.

## Installer Lumen

L’installation de Lumen est similaire à celle de Laravel

```shell
composer global require "laravel/lumen-installer"
```

## Créer le nouveau Projet

Maintenat que vous avez installer Lumen nous allons pouvoir utiliser la ligne de commande pour créer un nouveau projet :

```shell
lumen new api-todo
```

✋ Attention, le projet va être créé dans le dossier api-todo dans le dossier courant.

## Initialisation

Contrairement à un projet Laravel, les dépendances ```composer``` ne sont pas installés par défaut. Il faut donc les installer via la ligne de commande en faisant :

```shell
$ composer install
```

Le projet n’étant pas initialisé nous allons devoir jouer quelques commande pour terminer l’installation :

```shell
$ mv .env.example .env
```

Contrairement à Laravel, Lumen ne contient pas l’outils permettant d’initialiser la « secret key » nécéssaire à la sécurisation de votre application. Je pous propose par exemple de passer via la commande suivante :

```shell
$ openssl rand -base64 24
```

éditer le fichier ```.env``` pour renseigner une valeur pour :

- ```APP_KEY``` (exemple ```APP_KEY="I82xtis8Tsur2"```)

## Tester votre application

Pour tester votre application avec Lumen sur votre poste, c’est un peu plus « complexe » qu’avec Laravel. Vous devez saisir la commande suivante :

```shell
$ php -S localhost:8000 -t ./public
```

Une fois lancé vous avez un serveur Web qui écoute sur [le port 8000](http://localhost:8000)

🤔 Pourquoi Lumen n’intègre pas la commande ```php artisan serve``` ? La raison est plutôt logique, Lumen étant un ```micro framework``` il n’embarque pas toutes les options de base de Laravel. Options qui peuvent d’ailleurs simplement être remplacée.

## Gestion de la bose de données

### Le script de création / migration

Contrairement à la première version de notre application, nous allons stocker les données dans une Base de données. Qui dit base de données dit « ORM » et donc mapping objet. Pour rappel un ORM :

>> Un mapping objet-relationnel (en anglais object-relational mapping ou ORM) est une technique de programmation informatique qui crée l'illusion d'une base de données orientée objet à partir d'une base de données relationnelle en définissant des correspondances entre cette base de données et les objets du langage utilisé.

Pour rappel, le But de notre application est de créer des API Rest qui vont exposer la gestion de nos ```todos``` défini en base de données. La première étape est de créer via la ligne de commande le « script » qui initialisera la structure de votre base de données. 

L’option ```--create=todos``` permet d’indiquer le nom de la table à créer

```shell
php artisan make:migration create_todos_table --create=todos
```

✋ Le contenu du fichier est fictif est la pour illustrer comment travailler. Nous allons le modifier pour mettre les informations relative à notre base de données.

La commande à créér un nouveau fichier (dans mon cas) : ```database/migration/2017_11_02_205700_create_todos_table.php```

Dans le fichier créer nous allons définir notre schéma (à savoir la table) pour ajouter les 2 colonnes qui nous sont utiles ```texte``` et ```termine```. Le fichier après modification doit ressembler à :

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateTodosTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('todos', function (Blueprint $table) {
            $table->increments('id');
            $table->string('texte');
            $table->boolean('termine');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('todos');
    }
}
```

## Déclarer les routes

Pour commencer nous allons créer les différentes « routes » (c’est à dire les chemins d’accès à votre API). Dans notre applicaton nous avons 4 routes :

- Liste (/liste)
- Création (/creation)
- Terminer (/terminer)
- Suppression (/suppression)