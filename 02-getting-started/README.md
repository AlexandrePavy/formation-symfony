# Getting Starting with Symfony 4

Les liens :
* [Site officiel de Symfony](https://symfony.com/)
* [Documentation de Symfony](https://symfony.com/doc/4.0/index.html)
* [Symfony Roadmap](https://symfony.com/roadmap)
* [Quick tour](https://symfony.com/doc/4.O/quick_tour/the_big_picture.html)
* [Getting Started with Symfony 4](https://symfony.com/doc/4.0/getting_started/index.html)


Les étapes de l'installation de Symfony sont disponible dans la [Documentation - Setup Symfony](https://symfony.com/doc/4.0/setup.html).
## Installation simple grâce à composer :

### Création du Projet

`composer create-project symfony/website-skeleton symfony4-website`

`composer create-project symfony/skeleton symfony4-skeleton` - 

### Lancement du Serveur

1. Déplacez vous dans le dossier du projet avec `cd symfony4-skeleton`.
2. Executez la commange `php -S 127.0.0.1:8000 -t public` pour lancer le serveur interne de PHP.
3. Lancer sur votre navigateur la page [localhost:8000](http://localhost:8000/)
4. Un meilleur serveur de développement avec la commande `composer require server --dev` puis `php bin/console server:run`


### Création de notre première page

1. [Documentation Symfony](https://symfony.com/doc/4.0/page_creation.html)

### Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://symfony.sh/)
3. [Recettes officiel](https://github.com/symfony/recipes)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib)

### Barre de Débogage

Observez la barre de débogage. Au fur et à mesure que nous installerons de nouveaux packages, nous verrons de nouvelles options apparaître.

> Petit tour de découverte des options de la barre.

### Installation et Configuration du Plugin Symfony pour PHPStorm

Le plugin symfony pour PHPStorm permettra à notre IDE de reconnaître toutes les fonctionnalités de Symfony. 

Plugin Symfony, mettre src pour App Directory et public pour Web Directory

### Configuration de PSR-0 PHP Storm

Nous allons enfin, configurer PHPStorm pour résoudre correctement les espaces de noms de notre projet.

> Code / Detecter PSR-0 Namespace Roots

### Découvrir l'Architecture de SF4
> Doc de Référence : https://symfony.com/doc/current/page_creation.html#checking-out-the-project-structure
