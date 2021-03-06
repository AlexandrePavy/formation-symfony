# Installation des outils

## Objectifs

Mettre en place les outils nécessaires au développement d'applications web avec Symfony.

## Les outils

### Git

 1. Rendez-vous sur le [site officiel de GIT](https://git-scm.com/) pour télécharger et installer la dernière version de Git.
 2. Vérifiez votre installation en ouvrant le terminal de votre choix avec la commande `git --version`, la commande doit vous afficher la version de Git.
 3. Configurez Git avec les commandes suivantes :
	 1. `git config --global user.name "PRENOM NOM"` 
	 2. `git config --global user.email "EMAIL@DOMAINE"`
	 3. `git config --global core.editor nano`
 4. (Optionnel) Vous pouvez installer une application graphique pour faciliter l'utilisation de Git.
	 1. [Github Desktop](https://desktop.github.com/) Windows/macOS
	 2. [Git Kraken](https://www.gitkraken.com/) Windows/macOS/Linux
5. [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf) pour Git et Github en français.

### AMP Stack 

Il existe pleins d'outils pour installer Apache ou Nginx, Mysql et PHP. 
* [Wamp](http://www.wampserver.com/) - Windows
* [Xampp](https://www.apachefriends.org/fr/index.html) - Windows/Linux/macOS

Si vous êtes sur Windows, je recommande l'utilisation de [Laragon](https://laragon.org/) disponible sur Windows. Ce logiciel apporte non seulement Apache/Nginx, Mysql, PHP mais aussi une gestion automatique des hôtes virtuels en https, le terminal [Cmder](http://cmder.net/) et le logiciel de gestion de base de données [HeidiSQL](https://www.heidisql.com/).

1. Rendez-vous sur le site de [Laragon](https://laragon.org/) dans la section téléchargement, puis télécharger et installer [Laragon](https://laragon.org/).

### Composer 

Composer est le gestionnaire de dépendances PHP, il est essentiel pour une bonne utilisation de Symfony.

1. Rendez-vous sur le site de [Composer](https://getcomposer.org/) pour télécharger et installer composer.

Composer a besoin de l'exécutable PHP, sur windows et avec [Laragon](https://laragon.org/) vous pouvez définir `C:\laragon\bin\php\php-7.1.14-Win32-VC14-x64\php.exe` comme exécutable.  

[Composer Cheat Sheet](http://composer.json.jolicode.com/) - aide mémoire en anglais sur composer

### IDE

Je recommande fortement l'utilisation de [PhpStorm](https://www.jetbrains.com/phpstorm/) disponible pour Windows/Linux/macOS.

1. Rendez-vous sur le site de [PhpStorm](https://www.jetbrains.com/phpstorm/)
2. Liste des plugins sur PhpStorm :
    1. [Symfony Plugin](https://plugins.jetbrains.com/plugin/7219-symfony-plugin)
    2. [PHP Toolbox](https://plugins.jetbrains.com/plugin/8133-php-toolbox)
    3. [PHP Annotations](https://plugins.jetbrains.com/plugin/7320-php-annotations)
    4. [.ignore](https://plugins.jetbrains.com/plugin/7495--ignore) (Optionnel)
    5. [.env files support](https://plugins.jetbrains.com/plugin/9525--env-files-support) (Optionnel)

Il existe d'autres IDE ou éditeur de texte :
* [Eclipse](https://www.eclipse.org/downloads/) - Windows/Linux/macOS
* [Netbeans](https://netbeans.org/downloads/) - Windows/Linux/macOS
* [Visual Studio Code](https://code.visualstudio.com/) - Windows/Linux/macOS
