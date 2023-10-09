# Routing et requête

Dans notre projet, c'est Symfony qui gère nos routes (c'est-à-dire nos "chemins URL").

Par exemple, quand on se rend sur [localhost:8000](http://localhost:8000/), c'est Symfony qui grâce à nos
attributs `#[Route()]` que c'est la méthode `index` de notre `HomeController` qui doit être exécuté.

Le but va être ici de faire une route et une méthode de controller pour nos pages d'articles de blog.

On voudrait donc une URL du type `/articles/{id de l'article}`, ainsi `/articles/1` nous emmènera sur la page de
l'article ayant l'id 1 dans la base de données et celui-ci n'existe pas, nous devrons avoir une erreur 404.

## Exemple

Dans votre `HomeController`, ajoutez la méthode suivante

```php
#[Route('/hello/{name}', name: 'hello_name')]
public function hello(string $name): Response
{
    return new Response('Hello ' . $name);
}
```

N'oubliez pas les imports sur les objets comme `use Symfony\Component\HttpFoundation\Response;`;

Essayez de vous rendre sur la page [localhost:8000/hello/john](http://localhost:8000/hello/john) cela vous amène sur la
page correspondant à la route `/hello/{name}`.

Ici, comme votre route contient un paramètre `name`, Symfony essaye de passer la valeur à un argument de la méthode qui
s'appelle `$name`.

## Appliquons ça à notre page article

Créez `ArticleController` grâce à la commande `php bin/console make:controller`

Renommez la méthode index en show et ajouter la route `/articles/{id}`

Injectez le repository des articles dans ce nouveau controller et avec la méthode `find($id)`, récupérez l'article en
base de données.

Utilisez le template `blog_show.html` du TP 04-templating. Adaptez ce template.

Passez votre article au template et afficher les données de votre article dans cette nouvelle page.

Enfin, générez les liens vers les articles dans `home/index.html.twig` avec la méthode `path()`. Cherchez dans la
documentation comment vous pouvez passer un paramètre à cette méthode pour qu'elle génère l'URL avec l'id.

Si tout va bien, vous pouvez aller sur la page d'accueil et cliquer sur un lien : vous devriez arriver sur la page de
détail d'un article !

## Le CSS ne fonctionne pas ?

À ce moment-là, il est possible que le css ne fonctionne pas sur la page de détail d'un article.

C'est parce que vos fichiers CSS sont chargés de manière relative, les URL vers les fichiers CSS, JS et les images ne
sont pas correct.

Pour résoudre ça :

```
composer require symfony/asset
```

Ce package va vous fournir une méthode Twig bien pratique :

```php
asset('path/to/my/file.css')
```

Avec cette méthode, pas besoin de se soucier de ce genre de problèmes, elle va générer des URL absolues vers vos
fichiers statiques.

Utilisez cette méthode pour tous vos fichiers CSS, JS et vos images.

Ce paquet peut faire beaucoup plus que ça, vous pouvez consulter la documentation si vous voulez en savoir plus.

