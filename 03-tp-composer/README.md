# TP Composer

L'objectif est de prendre en main composer, installer un composant symfony en dehors de symfony et utiliser une
librairie PHP.

Documentation :

* [Composer](https://getcomposer.org/)
* [Packagist](https://packagist.org/)
* [Documentation de symfony/console](https://symfony.com/doc/6.3/components/console.html)
* [Documentation de monolog/monolog](https://github.com/Seldaek/monolog#monolog---logging-for-php-)
* [Composer Cheat Sheet](http://composer.json.jolicode.com/)

Composer est le gestionnaire de dépendances de PHP. Il peut être comparé à `npm` ou `yarn` pour Javascript ou `pip`
pour Python.

Créez un nouveau dossier `tp-composer` et déplacez-vous y avec votre terminal.

Pour initialiser un projet avec Composer, vous pouvez exécuter la commande `composer init` (⚠️ Cela va créer le projet
dans le dossier courant de votre terminal).

La commande est intéractive, vous pouvez vous référer au bloc ci-dessous pour les valeurs à fournir.

1. `composer init` - Initialise un projet composer
    - name: `formation/tp-composer`
    - type: `project`
    - author: `Prenom NOM <email@domain.tld>`

Vous devriez avoir un comportement similaire à :

```
bash-5.1$ composer init


  Welcome to the Composer config generator  

This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [foo/app]: nomprenom/tp-composer
Description []: Ceci est le premier tp avec composer
Author [n to skip]: Prenom NOM <email@domain.tld>
Minimum Stability []: 
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []: 

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? no
Would you like to define your dev dependencies (require-dev) interactively [yes]? no
Add PSR-4 autoload mapping? Maps namespace "Nomprenom\TpComposer" to the entered relative path. [src/, n to skip]: src/

{
    "name": "nomprenom/tp-composer",
    "description": "Ceci est le premier tp avec composer",
    "type": "project",
    "autoload": {
        "psr-4": {
            "Nomprenom\\TpComposer\\": "src/"
        }
    },
    "authors": [
        {
            "name": "Prenom NOM",
            "email": "email@domain.tld"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? 
Generating autoload files
Generated autoload files
PSR-4 autoloading configured. Use "namespace Nomprenom\TpComposer;" in src/
Include the Composer autoloader with: require 'vendor/autoload.php';
```

Analysez le contenu du fichier `composer.json` qui a été généré.

Pour fonctionner correctement, vous devez modifier ou ajouter quelques lignes de configuration dans votre
fichier `composer.json`.

Repérez la partie autoload de votre fichier: `composer.json`

```
"autoload": {
    "psr-4": {
        "App\\": "src/"
    }
}
```

Puis lancer la commande suivante pour régénérer les fichiers composer :

```bash
composer dump-autoload
```

Cela indique à composer que le dossier `src` correspond à l’espace de nom (namespace) `App`

## Exercice

L'objectif : Écrire une commande PHP (en console/CLI pour Command Line Interface) hello world à l'aide de
[symfony/console](https://packagist.org/packages/symfony/console) avec un fichier de log (journal) à
l'aide de [monolog/monolog](https://packagist.org/packages/monolog/monolog).

1. Créé votre projet avec `composer init`
2. Veuillez suivre la documentation pour ajouter le composant `symfony/console` à votre projet fraichement créé.
3. Toujours avec l'aide de la documentation, vous devez créer une `application` à la racine du projet
   (fichier `application.php` comme décrit dans la documentation).
    - Créé votre application grâce à `symfony/console`.
    - Pour exécuter votre application, faites `php application.php`, vous devriez voir un message apparaître.
4. Création de votre première commande
    - Ajoutez à votre application une première commande (fichier `HelloWorldCommand.php` dans le dossier `src/Command`).
    - Cette commande doit afficher "Hello World!" lorsque vous l'exécuter.
      [Cette documentation peut vous aider ;)](https://symfony.com/doc/current/console.html).
    - Le nom de votre commande doit être : `app:hello-world`.
5. Modifier de votre commande pour recevoir un argument d'entrée `name` à votre commande.
    - L'objectif est d'afficher "Hello `<name>`!" à la place de "Hello World!" lorsque l'argument `name` est passé à
      la commande.
    - Si l'argument `name` n'est pas passé dans ce cas, on doit afficher "Hello World!".
6. Ajout d'une librairie
    - Ajoutez ensuite le paquet/librarie `monolog/monolog` à votre projet et utilisez ce package pour écrire des logs
      dans le fichier `logs/console.log`.
    - Écrire un log lorsque `application.php` démarre.
    - Écrire un log lorsque vous exécutez votre commande `app:hello-world` démarre.
    - (Bonus) Écrire un log de type ERROR lorsque l'argument `name` est `AZERTY`
7. Bonus en vrac
    - Documentation et commentaire dans le code.
    - Pour approfondir, regardez les possibilités de style offertes par le composant Console (progress bar, couleurs,
      sections, tableaux, etc).
