# Getting Starting with Symfony 5 🚀

Les liens :
* [Site officiel de Symfony](https://symfony.com/)
* [Documentation de Symfony](https://symfony.com/doc/5.3/index.html)
* [Symfony Roadmap](https://symfony.com/roadmap)
* [Quick tour](https://symfony.com/doc/5.3/quick_tour/the_big_picture.html)
* [Getting Started with Symfony 5](https://symfony.com/doc/5.3/getting_started/index.html)

Les étapes de l'installation de Symfony sont disponible dans la [Documentation - Setup Symfony](https://symfony.com/doc/5.3/setup.html).

## Installation simple grâce à composer :

### Création d'un projet Symfony

`composer create-project symfony/website-skeleton sf-website`

`composer create-project symfony/skeleton sf5-skeleton`

### Lancement du Serveur

1. Déplacez vous dans le dossier du projet avec `cd sf5-skeleton`.
2. Exécutez la commande `php -S 127.0.0.1:8000 -t public` pour lancer le serveur interne de PHP.
3. Lancer sur votre navigateur la page [localhost:8000](http://localhost:8000/)
4. Un meilleur serveur de développement avec la commande `composer require server --dev` puis `php bin/console server:run`

## Création de notre première page

1. [Documentation Symfony](https://symfony.com/doc/5.3/page_creation.html)

### Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://symfony.sh/)
3. [Recettes officiel](https://github.com/symfony/recipes)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib)

### Découvrir l'Architecture de SF5
> Doc de Référence : https://symfony.com/doc/5.3/page_creation.html#checking-out-the-project-structure

### Création de notre première page

Nous allons créer une simple page qui affiche un nombre aléatoire.

Créez le fichier `src/Controller/LuckyController.php` avec ce contenu

```php
<?php
// src/Controller/LuckyController.php
namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;

class LuckyController
{
    public function number(): Response
    {
        $number = random_int(0, 100);

        return new Response(
            "<html><body><p>Lucky number: $number</p></body></html>"
        );
    }
}
```

Ici, nous avons une fonction qui génère un nombre entre 0 et 100 et retourne un objet Response contenant du HTML.

Le but est maintenant de faire en sorte de transformer ça en une page, accessible depuis notre navigateur.

Pour cela, ajoutez le code suivant dans `config/routes.yaml`

```yaml
# config/routes.yaml

app_lucky_number:
    path: /lucky_number
    controller: App\Controller\LuckyController::number
```

Vous pouvez maintenant accéder à votre page à l’adresse http://localhost:8000/lucky_number !

On vient ici de créer une route nommée app_lucky_number, qui associe le chemin /lucky_number à la méthode number de la classe App\Controller\LuckyController.

### Annotations

Il y a une autre façon de configurer les routes, qui est souvent préférée à la configuration en YAML.

Ce sont les annotations, pour pouvoir les utiliser, lancez la commande suivante

package flex : https://flex.symfony.com/

```shell
composer require annotations
```

Supprimez maintenant ce que vous aviez ajouté dans config/routes.yaml

```diff
# config/routes.yaml
-
- app_lucky_number:
-    path: /lucky_number
-    controller: App\Controller\LuckyController::number
```

```diff
    <?php
    // src/Controller/LuckyController.php
    namespace App\Controller;
    
    use Symfony\Component\HttpFoundation\Response;
+   use Symfony\Component\Routing\Annotation\Route;
    
    class LuckyController
    {
+       /**
+        * @Route("/lucky_number", name="app_lucky_number")
+        */
        public function number(): Response
        {
            $number = random_int(0, 100);
    
            return new Response(
                "<html><body><p>Lucky number: $number</p></body></html>"
            );
        }
    }
```
Il y a une alternative à l'annotation @Route, ce sont les attributes PHP (qui sont arrivés récemment avec PHP 8) qui devient aujourd'hui le standard pour PHP car natif (pas besoin de package externe).

Si vous avez PHP > 8 vous pouvez remplacer par :
```diff
       /**
        * @Route("/lucky_number", name="app_lucky_number")
        */
+    #[Route('/lucky_number', name: 'app_lucky_number')]
```

Maintenant, actualisez la page. Normalement rien n’a changé.

L’avantage des annotations, c’est que la configuration est près du code ce qui rend le projet plus facilement compréhensible et configurable.

## Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://flex.symfony.com/)
3. [Recettes officielles](https://github.com/symfony/recipes)
3. [Recettes contrib](https://github.com/symfony/recipes-contrib)

Symfony Flex est un plugin Composer qui s'ajoute au processus d’installation (lorsque l'on fait un composer install). Lorsqu’il détecte un paquet pour lequel une recette existe, il l’exécute.
Cela permet d'exécuter automatiquement l'installation ou la désinstallation d'un paquet, pas besoin d'écrire la configuratin de base nous-même.


## Debug Bar

Installez le Profiler Symfony. C’est un outil permettant d’avoir beaucoup de détails lors du développement afin de pouvoir facilement débugger et comprendre l’origine d’un bug ou d’une erreur.

Pour l’installer :

```shell
composer require debug
```

> Faite un petit tour de découverte des options de la barre.
> Découvrez la méthode `dump()`.

Actualiser la page. Une barre devrait maintenant apparaître en bas de la page avec différentes informations (temps d’exécution, temps de rendu, logs, etc)

En cliquant sur un élément de la barre de debug, on arrive sur la page de détails du Profiler.

Observez la barre de debug et naviguez dans les différents onglets du Profiler. Au fur et à mesure que nous installerons de nouveaux packages, nous verrons de nouvelles options apparaître.

Une fonction utile pour le debug est dump(), elle est fournie avec le debug pack installé précédemment.

Dans votre controller ajoutez

```php
$user = [
    'firstName' => 'John',
    'lastName' => 'Doe',
];

dump($user);
```

En actualisant la page, un symbole "Cible" devrait apparaître dans la barre et en passant le curseur dessus, vous devriez voir le contenu de la variable `$user`.


## Installation et Configuration du Plugin Symfony pour PHPStorm

Le plugin symfony pour PHPStorm permettra à notre IDE de reconnaître toutes les fonctionnalités de Symfony. 

Le plugin symfony pour PHPStorm permettra à notre IDE de reconnaître toutes les fonctionnalités de Symfony.

Pour l’installer, rendez-vous dans Settings > Plugins puis Marketplace et cherchez un plugin nommé Symfony Support et installez-le.

Dans File > Settings > PHP > Symfony

Cocher la case Enable for this project et mettre src pour App Directory et public pour Web Directory.

## L’objet Request

Nous allons maintenant voir comment récupérer certaines informations de la requête HTTP.

Changer le code de votre controller pour ajouter un import de l’objet Request

```diff
+   use Symfony\Component\HttpFoundation\Request;
    use Symfony\Component\HttpFoundation\Response;
    use Symfony\Component\Routing\Annotation\Route;
```

Puis changez la signature de la méthode lucky

```
-        public function number(): Response
+        public function number(Request $request): Response
```

Symfony va automatiquement comprendre que vous souhaitez récupérer la requête et vous la donner.


Par exemple, si l’utilisateur accès à l’URL http://localhost:8000/lucky_number?name=John, on aimerait pouvoir récupérer le paramètre name présent dans la Query String

Avec Request, il est possible de le faire comme ceci `$name = $request->query->get('name')`.

Modifiez votre code pour afficher le paramètre name sur la page.


## Symfony Console

Manipulation de la command symfony.

```shell
php bin/console
```

## Maker Bundle

https://symfony.com/bundles/SymfonyMakerBundle/current/index.html

Objectif : essaye de comprendre Symfony Maker Bundle
Installer Symfony Maker Bundle et l'utiliser

## Découvrir l’Architecture de Symfony 5

Doc de Référence : https://symfony.com/doc/5.3/page_creation.html#checking-out-the-project-structure

## Liens utiles

Votre plus grande alliée est la [documentation officielle de Symfony](https://symfony.com/doc/current/index.html)

Pour appronfondir : 

* https://symfonycasts.com/ tutoriel de qualité en vidéo pour POO/ Javascript / Symfony / PHP (Gratuit et Payant) (en anglais)
* https://www.grafikart.fr/formations/php formation vidéo gratuite sur PHP (Gratuit) (en français)
* https://www.grafikart.fr/formations/git Formation vidéo git (Gratuit) (en français)
* https://www.grafikart.fr/tutoriels/composer-480 Tutoriel vidéo pour composer (Gratuit) (en français)
* https://github.com/symfony/demo Projet Symfony de démonstration (anglais)