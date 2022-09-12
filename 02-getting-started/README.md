# Getting Starting with Symfony 6 🚀

Les liens :
* [Site officiel de Symfony](https://symfony.com/)
* [Documentation de Symfony](https://symfony.com/doc/6.1/index.html)
* [Symfony Roadmap](https://symfony.com/roadmap)
* [Quick tour](https://symfony.com/doc/6.1/quick_tour/the_big_picture.html)
* [Getting Started with Symfony 6](https://symfony.com/doc/6.1/getting_started/index.html)

Les étapes de l'installation de Symfony sont disponible dans la [Documentation - Setup Symfony](https://symfony.com/doc/5.3/setup.html).

## Installation simple grâce à composer :

### Création d'un projet Symfony

1. `composer create-project symfony/website-skeleton sf-website`
    * Dans le cas de Symfony CLI : `symfony new --webapp sf-website`
2. `composer create-project symfony/skeleton sf-skeleton`
    * Dans le cas de Symfony CLI : `symfony new sf-skeleton`

### Lancement du Serveur

1. Déplacez vous dans le dossier du projet avec `cd sf-skeleton`.
2. Exécutez la commande `php -S 127.0.0.1:8000 -t public` pour lancer le serveur interne de PHP.
3. Lancer sur votre navigateur la page [localhost:8000](http://localhost:8000/)

## Création de notre première page

1. [Documentation Symfony](https://symfony.com/doc/6.1/page_creation.html)

### Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://t-richard.github.io/flex-server/)
3. [Recettes officiel](https://github.com/symfony/recipes/blob/flex/main/RECIPES.md)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib/blob/flex/main/RECIPES.md)

### Découvrir l'Architecture de SF
> Doc de Référence : https://symfony.com/doc/6.1/page_creation.html#checking-out-the-project-structure

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

### Attributs

Au lieu de définir votre route en YAML, Symfony vous permet également d'utiliser des routes en annotation ou en attribut PHP.

Les attributs sont intégrés à PHP à partir de PHP 8. Dans les versions antérieures de PHP, vous pouvez utiliser des annotations.

Dans le cas de Symfony 6 on utilise les attibuts :

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

+       #[Route('/test', name: 'app_test')]
        public function number(): Response
        {
            $number = random_int(0, 100);
    
            return new Response(
                "<html><body><p>Lucky number: $number</p></body></html>"
            );
        }
    }
```

Maintenant, actualisez la page. Normalement rien n’a changé.

L’avantage des annotations ou des attributs PHP, c’est que la configuration de la route se trouve au même endroit que le code pour faciliter la compréhensiton et la configuration.

## Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://t-richard.github.io/flex-server/)
3. [Recettes officiel](https://github.com/symfony/recipes/blob/flex/main/RECIPES.md)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib/blob/flex/main/RECIPES.md)


Symfony Flex est un plugin Composer qui s'ajoute au processus d’installation (lorsque l'on fait un composer install). Lorsqu’il détecte un paquet pour lequel une recette existe, il l’exécute.

Cela permet d'exécuter automatiquement l'installation ou la désinstallation d'un paquet, pas besoin d'écrire la configuratin de base nous-même.


## Debug Bar

Installez le Profiler Symfony. C’est un outil permettant d’avoir beaucoup de détails lors du développement afin de pouvoir facilement débugger et comprendre l’origine d’un bug ou d’une erreur.

Pour l’installer :

```shell
composer require profiler
# ou sans flex 
composer require --dev symfony/profiler-pack
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

## Découvrir l’Architecture de Symfony 6

Doc de Référence : https://symfony.com/doc/6.1/page_creation.html#checking-out-the-project-structure

## Liens utiles

Votre plus grande alliée est la [documentation officielle de Symfony](https://symfony.com/doc/6.1/index.html)

Pour appronfondir : 

* https://symfonycasts.com/ tutoriel de qualité en vidéo pour POO/ Javascript / Symfony / PHP (Gratuit et Payant) (en anglais)
* https://www.grafikart.fr/formations/php formation vidéo gratuite sur PHP (Gratuit) (en français)
* https://www.grafikart.fr/formations/git Formation vidéo git (Gratuit) (en français)
* https://www.grafikart.fr/tutoriels/composer-480 Tutoriel vidéo pour composer (Gratuit) (en français)
* https://github.com/symfony/demo Projet Symfony de démonstration (anglais)