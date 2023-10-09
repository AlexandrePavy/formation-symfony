# Getting Starting with Symfony 6 🚀

Les liens :

* [Site officiel de Symfony](https://symfony.com/)
* [Documentation de Symfony](https://symfony.com/doc/6.3/index.html)
* [Versions de Symfony](https://symfony.com/releases)
* [Visite rapide](https://symfony.com/doc/6.3/quick_tour/the_big_picture.html)
* [Commencer avec Symfony 6](https://symfony.com/doc/6.3/getting_started/index.html)

Pour les étapes d'installation de Symfony, consultez
la [Documentation - Configuration de Symfony](https://symfony.com/doc/6.3/setup.html).

## Installation simple avec Composer :

### Création d'un projet Symfony

1. Utilisez la commande `composer create-project symfony/website-skeleton sf-website`
   ou avec Symfony CLI : `symfony new --webapp sf-website`
2. Utilisez la commande `composer create-project symfony/skeleton sf-skeleton` ou avec Symfony CLI :
   `symfony new sf-skeleton`.

### Démarrage du serveur web intégré PHP

1. Accédez au répertoire de votre projet avec  `cd sf-skeleton`.
2. Exécutez la commande `php -S 127.0.0.1:8000 -t public` pour lancer le serveur web interne de PHP.
3. Ouvrez votre navigateur et accédez à [localhost:8000](http://localhost:8000/)

## Création de votre première page

1. Suivez la [Documentation Symfony](https://symfony.com/doc/6.3/page_creation.html)

### Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://t-richard.github.io/flex-server/)
3. [Recettes officiel](https://github.com/symfony/recipes/blob/flex/main/RECIPES.md)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib/blob/flex/main/RECIPES.md)

### Découvrir l'Architecture de Symfony

Pour découvrir l'architecture de Symfony, consultez
la [Documentation](https://symfony.com/doc/6.3/page_creation.html#checking-out-the-project-structure).

### Création de votre première page

Créez une page simple affichant un nombre aléatoire. Créez le fichier `src/Controller/LuckyController.php` avec ce
contenu :

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

Cette fonction génère un nombre aléatoire entre 0 et 100 et renvoie une réponse contenant du HTML.

Pour rendre cette fonction accessible depuis votre navigateur, ajoutez le code suivant dans `config/routes.yaml` :

```yaml
# config/routes.yaml

app_lucky_number:
  path: /lucky_number
  controller: App\Controller\LuckyController::number
```

Vous pouvez maintenant accéder à votre page à l'adresse http://localhost:8000/lucky_number !

On vient ici de créer une route nommée app_lucky_number, qui associe le chemin /lucky_number à la méthode number de la
classe `App\Controller\LuckyController`.

### Attributs

Au lieu de définir votre route en YAML, Symfony vous permet d'utiliser des routes en annotation ou en attribut PHP.

Les attributs sont intégrés à PHP à partir de la version 8 de PHP. Dans les versions antérieures de PHP, vous pouvez
utiliser des annotations.

Pour Symfony 6, utilisez les attributs. Supprimez ce que vous avez ajouté dans `config/routes.yaml` :

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

+       #[Route('/lucky_number', name: 'app_lucky_number')]
        public function number(): Response
        {
            $number = random_int(0, 100);
    
            return new Response(
                "<html><body><p>Lucky number: $number</p></body></html>"
            );
        }
    }
```

Actualisez la page. Normalement, rien n'a changé. L'avantage des annotations ou des attributs PHP est que la
configuration de la route est directement associée au code.

## Définition

1. [Flex](https://github.com/symfony/flex)
2. [Liste des recettes](https://t-richard.github.io/flex-server/)
3. [Recettes officiel](https://github.com/symfony/recipes/blob/flex/main/RECIPES.md)
4. [Recettes contrib](https://github.com/symfony/recipes-contrib/blob/flex/main/RECIPES.md)

Symfony Flex est un plugin Composer qui simplifie l'installation des paquets. Lorsqu'un paquet a une recette Flex,
Symfony Flex gère automatiquement l'installation et la configuration.

Pour en savoir plus, consultez [Symfony Flex](https://github.com/symfony/flex).

Cela permet d'exécuter automatiquement l'installation ou la désinstallation d'un paquet, pas besoin d'écrire la
configuration par défaut nous-même.

## Debug Bar

Installez le Profiler Symfony. C’est un outil permettant d’avoir des informations supplémentaires lors du
développement afin de comprendre ce qu'il se passe et de voir les performances.

Pour l'installer, utilisez la commande suivante :

```shell
composer require debug
# ou sans flex 
composer require --dev symfony/debug-bundle symfony/web-profiler-bundle
```

> Explorez les fonctionnalités de la barre de débogage et découvrez la méthode dump() pour afficher des informations
> de débogage.

Actualiser la page. Une nouvelle barre devrait maintenant apparaître en bas de la page avec différentes informations
(temps d’exécution, temps de rendu, logs, etc)

En cliquant sur un élément de la barre, on arrive sur la page de détails du Profiler.

Observez la barre de debug et naviguez dans les différents onglets du Profiler. Au fur et à mesure que nous installerons
de nouveaux packages, nous verrons de nouvelles options apparaître.

Une fonction utile pour le debug est `dump()`, elle est fournie avec le debug pack installé précédemment.

Dans votre controller ajoutez

```php
$user = [
    'firstName' => 'John',
    'lastName' => 'Doe',
];

dump($user);
```

En actualisant la page, un symbole "Cible" devrait apparaître dans la barre et en passant le curseur dessus,
vous devriez voir le contenu de la variable `$user`.

## Installation et Configuration du Plugin Symfony pour PHPStorm

Le plugin Symfony pour PHPStorm permet à notre IDE de reconnaître les fonctionnalités de Symfony. Pour l'installer :

1. Accédez à Settings > Plugins, puis recherchez le plugin Symfony Support et installez-le.
2. Dans File > Settings > PHP > Symfony, activez-le pour le projet et définissez src comme répertoire de l'application
   et public comme répertoire web.

Cocher la case Enable for this project et mettre src pour App Directory et public pour Web Directory.

## L’objet Request

Découvrez comment récupérer des informations de la requête HTTP en utilisant l'objet Request. Modifiez la signature de
votre méthode pour inclure l'objet Request.

```diff
+   use Symfony\Component\HttpFoundation\Request;
    use Symfony\Component\HttpFoundation\Response;
    use Symfony\Component\Routing\Annotation\Route;
```

Puis changez la signature de la méthode lucky

```diff
-        public function number(): Response
+        public function number(Request $request): Response
```

Symfony va automatiquement comprendre que vous souhaitez récupérer la requête et vous la donner.

Par exemple, avec l'URL suivante http://localhost:8000/lucky_number?name=John, on aimerait pouvoir récupérer le
paramètre name présent dans la Query String

Avec Request, il est possible de le faire comme ceci `$name = $request->query->get('name')`.

Modifiez votre code pour afficher le paramètre name sur la page.

## Symfony Console

Utilisez la console Symfony pour exécuter des commandes.

```shell
php bin/console
```

## Maker Bundle

Découvrez [Symfony Maker Bundle](https://symfony.com/bundles/SymfonyMakerBundle/current/index.html). Installez-le
et essayez de comprendre son utilité.

## Liens utiles

Votre plus grande alliée est la [documentation officielle de Symfony](https://symfony.com/doc/6.3/index.html)

Pour approfondir :

* https://symfonycasts.com/ Tutoriels vidéo de qualité sur la programmation orientée objet, JavaScript, Symfony, PHP (
  gratuits et payants, en anglais).
* https://www.grafikart.fr/formations/php Formation vidéo gratuite sur PHP (en français).
* https://www.grafikart.fr/formations/git Formation vidéo sur Git (gratuite, en français).
* https://www.grafikart.fr/tutoriels/composer-480 Tutoriel vidéo sur Composer (gratuit, en français).
* https://github.com/symfony/demo Projet Symfony de démonstration (en anglais)