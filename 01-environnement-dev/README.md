# Installation des outils

## Objectifs
L'objectif de cette étape est de mettre en place les outils nécessaires pour le développement d'applications PHP avec 
Symfony.

## Les outils

### Git

 1. Rendez-vous sur le [site officiel de GIT](https://git-scm.com/) pour télécharger et installer la dernière version de
Git.
 2. Vérifiez votre installation en ouvrant le terminal de votre choix avec la commande `git --version`, la commande doit
vous afficher la version de Git.
 3. Configurez Git avec les commandes suivantes :
	 1. `git config --global user.name "PRÉNOM NOM"` 
	 2. `git config --global user.email "EMAIL@DOMAIN.TLD"`
	 3. `git config --global core.editor nano`
 4. (Optionnel) Vous pouvez installer une application graphique pour faciliter l'utilisation de Git.
      1. [Github Desktop](https://desktop.github.com/) pour Windows/macOS
	 2. [Git Kraken](https://www.gitkraken.com/) pour Windows/macOS/Linux
5. Consultez cet [Aide-Mémoire](https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf) pour Git et Github 
en français.

### AMP Stack

Il existe plusieurs outils pour installer Apache ou Nginx, MySQL et PHP. Vous pouvez choisir parmi les options 
suivantes :

* [Wamp](http://www.wampserver.com/) - Windows
* [Xampp](https://www.apachefriends.org/fr/index.html) - Windows/Linux/macOS

Si vous utilisez Windows, je vous recommande l'utilisation de [Laragon](https://laragon.org/). Ce logiciel apporte non seulement la 
combinaison Apache/Nginx, MySQL, PHP mais aussi une gestion automatique des hôtes virtuels en https, le terminal 
[Cmder](http://cmder.net/) ainsi que le logiciel de gestion de base de données [HeidiSQL](https://www.heidisql.com/).

1. Rendez-vous sur le site de [Laragon](https://laragon.org/) dans la section téléchargement, puis télécharger et installer 
[Laragon](https://laragon.org/).

Pour rendre disponible PHP dans votre terminal n'oubliez pas de configurer correctement votre variable d'environnement **PATH** [en suivant ce tutoriel](https://www.forevolve.com/en/articles/2016/10/27/how-to-add-your-php-runtime-directory-to-your-windows-10-path-environment-variable/).

### Composer 

Composer est le gestionnaire de dépendances PHP, il est essentiel pour une bonne utilisation de Symfony.

1. Rendez-vous sur le site de [Composer](https://getcomposer.org/) pour télécharger et installer Composer.

Composer a besoin de l'exécutable PHP, sur windows et avec [Laragon](https://laragon.org/) vous pouvez définir `C:\laragon\bin\php\php-8.1.10-Win32-VC14-x64\php.exe` comme exécutable.  

Consultez cette [Composer Cheat Sheet](http://composer.json.jolicode.com/) pour obtenir un aide-mémoire en anglais sur Composer.

### IDE

Je recommande fortement l'utilisation de [PhpStorm](https://www.jetbrains.com/phpstorm/), disponible gratuitement sur les systèmes d'exploitation 
Windows/Linux/macOS avec le [GitHub Student Developer Pack](https://education.github.com/pack).

1. Rendez-vous sur le site de [PhpStorm](https://www.jetbrains.com/phpstorm/)
2. Liste des plugins sur PhpStorm à installer dans Settings > Plugins :
    1. [Symfony Plugin](https://plugins.jetbrains.com/plugin/7219-symfony-plugin)
    2. [PHP Toolbox](https://plugins.jetbrains.com/plugin/8133-php-toolbox)
    3. [PHP Annotations](https://plugins.jetbrains.com/plugin/7320-php-annotations)
    4. [.ignore](https://plugins.jetbrains.com/plugin/7495--ignore) (Optionnel)
    5. [.env files support](https://plugins.jetbrains.com/plugin/9525--env-files-support) (Optionnel)

Si vous préférez utiliser un éditeur plus simple, vous pouvez opter pour [Visual Studio Code](https://code.visualstudio.com/) compatible avec 
Windows/Linux/macOS.

Pour Visual Studio Code, voici une liste de plugins à installer :
1. [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)
2. [PHP Namespace Resolver](https://marketplace.visualstudio.com/items?itemName=MehediDracula.php-namespace-resolver)
3. [Twig Language](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language)
4. [Twig Language 2](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language-2)

### Symfony CLI

La CLI (Command Line Interface) Symfony est un outil de développement qui vous permet de créer, exécuter et gérer vos 
applications Symfony directement depuis votre terminal.

Installation de la CLI Symfony
1. [Symfony CLI](https://symfony.com/download) - Windows/Linux/macOS

### Vérification de votre environnement

Assurez-vous que les outils sont correctement installés en exécutant les commandes suivantes dans votre terminal :

1. `php --version`
2. `composer --version`
3. `git --version`
4. `symfony version`

Votre environnement de développement PHP avec Symfony est maintenant prêt à être utilisé.