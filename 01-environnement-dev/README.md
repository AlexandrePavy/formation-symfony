# Installation des outils

## Objectifs

Mettre en place les outils nécessaires au développment d'application web avec Symfony.

## Les outils

### Git

 1.  Rendez-vous sur le [site officiel de GIT](https://git-scm.com/) pour télécharger et installer la dernière version de Git.
 2. Vérifiez votre installation en ouvrant le terminal de votre choix avec la commande `git --version`, la commande doit vous afficher la version de Git.
 3. Configurez Git avec les commandes suivantes :
	 1. `git config --global user.name "PRENOM NOM"` 
	 2. `git config --global user.email "EMAIL@DOMAINE"`
	 3. `git config --global core.editor nano`
 4. (Optionnel) Vous pouvez installer une application graphique pour faciliter l'utilisation de Git.
	 1. [Github Desktop](https://desktop.github.com/) Windows/macOS
	 2. [Git Kraken](https://www.gitkraken.com/) Windows/macOS/Linux
5. [Aide-mémoire](https://services.github.com/on-demand/downloads/fr/github-git-cheat-sheet.pdf) pour Git et Github en français.

### AMP Stack 

Il existe pleins d'outils pour installer Apache ou Nginx, Mysql et PHP. 
* [Wamp](http://www.wampserver.com/) - Windows
* [Xampp](https://www.apachefriends.org/fr/index.html) - Windows/Linux/macOS

Dans ce cours je recommande l'utilisation de [Laragon](https://laragon.org/) disponible sur Windows. Ce logiciel apporte non seulement Apache/Nginx, Mysql, PHP mais aussi une gestion automatique des hôtes virtuels en https, le terminal [Cmder](http://cmder.net/) et le logiciel de gestion de base de données [HeidiSQL](https://www.heidisql.com/).

1. Rendez-vous sur le site de [Laragon](https://laragon.org/) dans la section téléchargement, puis télécharger et installer Laragon.
