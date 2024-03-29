# Templating avec Twig

Dans la partie [Getting Started](../02-getting-started), nous avons créé une page simple utilisant du html directement
dans le controller.

Le but de cette partie est d'utiliser un framework CSS dans notre projet Symfony. Vous pouvez le
regarder la documentation de [Bootstrap](https://getbootstrap.com/docs/5.1/getting-started/introduction/).

Vous pouvez télécharger les templates HTML ici :

* [blog_home](blog_home.html) - Page d'accueil de type blog
* [blog_show](blog_show.html) - Page d'un article de blog

## Installation de Twig

Commençons par installer Twig avec la commande suivante :

```shell
composer require twig
```

Pour rappel, le package "twig" n'existe pas dans [Packagist](https://packagist.org/)
c'est [Symfony Flex](https://t-richard.github.io/flex-server/) qui fait le lien
avec https://github.com/symfony/twig-pack qui lui indique d'installer et de configurer automatiquement à notre place les
packages suivants :

```json
{
  "require": {
    "symfony/twig-bundle": "6.3.*",
    "twig/extra-bundle": "^2.12|^3.0",
    "twig/twig": "^2.12|^3.0"
  }
}
```

Documentation :

* https://twig.symfony.com/ : Site officiel de twig
* https://twig.symfony.com/doc/3.x/ documentation de twig
* https://symfony.com/doc/6.3/templates.html templating dans symfony
* https://symfony.com/doc/6.3/frontend.html gestion des Assets dans symfony

## Création d'un nouveau controller

Afin de tester nos nouvelles pages, nous allons créer un nouveau controller que nous appellerons `HomeController`.

Vous pouvez utiliser Maker bundle avec la commande console Symfony

```shell
php bin/console make:controller HomeController
```

Vérifier le code généré.

Dans ce controller, vous devez modifier l'attribut de route pour que la page soit accessible sur `/` et non `/home`.

```diff
- #[Route('/home', name: 'app_home')]
+ #[Route(path: '/', name: 'app_home')]
```

Accédez à [localhost:8000](http://localhost:8000/) pour constater que votre page fonctionne comme attendu.

## Adaptation du template

Chaque template doit hériter d'un template commun et générique nommé `base.html.twig`.

Ce fichier contient le code que l'on doit répéter sur toutes les pages. Il s'agit généralement du HTML générique (html,
head, body, meta, etc) ainsi que des éléments HTML que l'on retrouve sur toutes les pages (navbar, menu, footer, etc).

La bonne pratique veut que l'on sépare dans des fichiers différents, les composants de notre page. Cela veut par exemple
dire un fichier pour la navbar et un fichier pour le footer, que l'on va inclure dans le template de base.

### Passons à la pratique

> Les fichiers du template téléchargé précédemment sont relativement bien organisés. Chaque section de la page est
> désignée dans le code HTML par un commentaire comme <!-- Navigation -->. Cela va faciliter le découpage des pages.

Pour commencer, dans le dossier `templates`, créez un dossier `_layout` qui contiendra nos composants tels que le footer
ou la navbar.

Dans ce dossier, créez les fichiers `navbar.html.twig` et `footer.html.twig`.

Prendre le fichier `blog_home.html` du et répartir le code HTML dans les différents fichiers du dossier templates :

* Le code commun des pages doit se trouver dans `base.html.twig`
* Le code de la navbar et du footer dans les fichiers séparés.
* Le code spécifique à la page d'accueil doit se trouver dans le fichier `home/index.html.twig`
* Le fichier `home/index.html.twig` doit étendre (extends) du template `base.html.twig` et le code spécifique à la page
  dans le bloc body.

Prendre le fichier `blog_show.html` et répartir le code dans un template `home/show.html.twig` et faire une nouvelle 
route dans votre controller existant pour afficher un article.

```php
    #[Route('/article/1', name: 'app_article_show')]
    public function show(): Response
    {
        return $this->render('home/show.html.twig', [
        ]);
    }
```

Pour plus de détails sur la logique d'héritage,
consultez [cette documentation Twig](https://twig.symfony.com/doc/3.x/tags/extends.html).

Les templates de la navbar et du footer ne doivent pas étendre de `base.html.twig`. Ils doivent être inclus dans le
template `base.html.twig` car ils font partie du code commun à toutes les pages. Cela se fait avec le mot
clé [include](https://twig.symfony.com/doc/3.x/tags/include.html).

### Testons tout ça

Pour tester notre nouvelle page, on peut actualiser [localhost:8000](http://localhost:8000/)

## Générations des URLs

Nous avons déjà vu que pour gérer nos URLs, nous utilisons l'attribut `#[Route]` dans nos controllers.

Dans cet attribut, nous avons deux parties :

* `path` : c'est la partie après le nom de domaine que les utilisateurs devront saisir pour accéder à la page en
  question.
* `name` : cette partie est utile pour le développement, elle nous sert à référencer cette route pour pouvoir générer
  des URLs

C'est cet attribut qui va nous servir à générer les URLs dans notre template Twig.

Dans le template `navbar.html.twig`, changez la balise contenant le lien vers la page d'accueil par

```diff
- <a class="navbar-brand" href="#!">Start Bootstrap</a>
+ <a class="navbar-brand" href="{{ path('app_home') }}">Start Bootstrap</a>
```

Ici, la fonction `path()` prend comme paramètre le nom de la route défini dans l'attribut de votre controller.

Si vous actualisez, vous devriez arriver sur la page d'accueil en cliquant sur `Start Bootstrap` dans le menu.

Changez également le lien `Home` sur la page d'accueil pour qu'il redirige aussi vers la page d'accueil.

C'est d'ailleurs le moment de vous l'approprier. Choisissez un nom pour votre blog et changez-le dans la navbar, le
footer (copyright) et le haut de page.

Supprimez aussi les liens inutiles du menu pour ne laisser que les liens disponibles avec l'aide du commentaire twig.

## Dynamisation de la page d'accueil

Nous allons tenter de dynamiser la page, pour cela dans votre controller `HomeController`

Créer plusieurs articles comme celui-ci :

```php
    $article1 = [
        'title' => 'Titre 1',
        'subtitle' => 'Subtitle 1',
        'createdAt' => new \DateTime(),
        'author' => 'John Doe',
        'content' => "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
        'imageUrl' => 'https://dummyimage.com/850x350/dee2e6/6c757d.jpg'
    ];
```

Et passez les articles à votre vue twig :

```php
return $this->render('home/index.html.twig', [
    'articles' => [$article1, $article2]
]);
```

* Modifier l'intégration du html blog_show.html dans la route route dédiée
  * Ajouter une nouvelle route pour afficher un article
  * Intéger le template `home/show.html.twig` avec [blog_show](blog_show.html)

```php
    #[Route('/article/1', name: 'app_article_show')]
    public function show(): Response
    {
        $article1 = [
            'title' => 'Titre 1',
            'subtitle' => 'Subtitle 1',
            'createdAt' => new \DateTime(),
            'author' => 'John Doe',
            'content' => "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.",
            'imageUrl' => 'https://images.unsplash.com/photo-1575936123452-b67c3203c357?auto=format&fit=crop&q=80&w=2070&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        ];

        return $this->render('home/show.html.twig', [
            'article' => $article1,
        ]);
    }
```

### Un peu d'objet PHP ?

Afin de représenter un article, nous allons créer une classe qui représente un article.

Créez d'abord un dossier `Entity` dans le dossier src.

Puis créez dans ce dossier une classe `Article.php`

```php
<?php

namespace App\Entity;

class Article
{

}
```

Ajoutez les propriétés suivantes

- title (string, le titre de l'article)
- subtitle (string, le sous-titre, servant aussi de résumé pour la liste)
- createdAt (DateTime, la date de création) NB : DateTime est une classe PHP représentant une date (avec heure et
  timezone)
- author (string, le nom de l'auteur)
- content (string, le contenu de l'article)
- imageUrl (string, l'adresse de l'image)

Respectez le principe d'encapsulation en mettant vos propriétés en private et en ajoutant des getters et des setters.

Lien de la documentation sur les classes en PHP https://www.php.net/manual/fr/language.oop5.php

Utilisez également le typage des paramètres et des types de retours.

Ensuite remplacer dans votre `HomeController` les tableaux par une instanciation d'objet.

```php
$article = [
    ...
];

// become
$article = new Article();
// à vous de trouver la suite
...
```

## Gestion des fichiers statiques

Exercice Téléchargement de bootstrap en local

> documentation : https://symfony.com/doc/6.3/components/asset.html

Pour la gestion des fichiers statiques (images, scripts css, scripts js) vous pouvez copier les dossiers css, img, js et
vendor dans le dossier `public` de notre projet Symfony.

Symfony possède un composant Webpack Encore et c'est une méthode à privilégier pour un projet. Cependant, elle
nécessite plus de temps à comprendre et mettre en place.

Nous nous en tiendrons donc dans un premier temps à des fichiers statiques dans le dossier public.

Pour plus détails : [Guide Frontend Symfony](https://symfony.com/doc/6.3/frontend.html)
