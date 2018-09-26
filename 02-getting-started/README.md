# Getting Starting with Symfony 4

Les liens :
* [Site officiel de Symfony](https://symfony.com/)
* [Documentation de Symfony](https://symfony.com/doc/4.1/index.html)
* [Symfony Roadmap](https://symfony.com/roadmap)
* [Quick tour](https://symfony.com/doc/4.1/quick_tour/the_big_picture.html)
* [Getting Started with Symfony 4](https://symfony.com/doc/4.1/getting_started/index.html)

Les étapes de l'installation de Symfony sont disponible dans la [Documentation - Setup Symfony](https://symfony.com/doc/4.1/setup.html).

## Installation simple grâce à composer :

### Création d'un projet Symfony

`composer create-project symfony/website-skeleton sf4-website`

`composer create-project symfony/skeleton sf4-skeleton`

### Lancement du Serveur

1. Déplacez vous dans le dossier du projet avec `cd symfony4-skeleton`.
2. Exécutez la commande `php -S 127.0.0.1:8000 -t public` pour lancer le serveur interne de PHP.
3. Lancer sur votre navigateur la page [localhost:8000](http://localhost:8000/)
4. Un meilleur serveur de développement avec la commande `composer require server --dev` puis `php bin/console server:run`

### Création de notre première page

1. [Documentation Symfony](https://symfony.com/doc/4.1/page_creation.html)

### Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://symfony.sh/)
3. [Recettes officiel](https://github.com/symfony/recipes)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib)

### Debug Bar

Observez la barre de debug. Au fur et à mesure que nous installerons de nouveaux packages, nous verrons de nouvelles options apparaître.

> Petit tour de découverte des options de la barre.

### Installation et Configuration du Plugin Symfony pour PHPStorm

Le plugin symfony pour PHPStorm permettra à notre IDE de reconnaître toutes les fonctionnalités de Symfony. 

Plugin Symfony, mettre src pour App Directory et public pour Web Directory

### Découvrir l'Architecture de SF4
> Doc de Référence : https://symfony.com/doc/4.1/page_creation.html#checking-out-the-project-structure
