Webpack
=======

[Documentation Webpack](https://symfony.com/doc/4.2/frontend.html)

L'objectif est d'ajouter un bouton html sur la page "show" d'un article pour ajouter un like à l'aide de javascript.

1. Ajouter un lien/bouton dans votre html.
2. Créer une route dans votre backend.
3. écrire du javascript sur le clique du boutton appel votre route backend pour ajouter un like.

Ajouter html qui correspond au nombre de ❤ dans votre `templates/homepage/show.html.twig`

```html
    <div>
        <span class="pl-2">
            <span class="js-like-article-count">{{ article.nbLike }}</span>
            <a
                href="javascript:"
                class="js-like-article">
                ❤
            </a>
        </span>
    </div>
```

Ajouter une nouvelle route dans votre HomeController : 

```php
    /**
     * @Route("/{id}/like", name="article_like", requirements = { "id" = "\d+" }, methods={ "POST" })
     */
    public function toggleArticleHeart(...)
    {
        // Get article

        // Add one like

        // Save in database

        // Return JSONResponse 'likes': 8
    }
```

dans votre html, il faut ajouter l'attribut `data-like-url` à votre lien pour récupérer ce lien côté javascript et faire l'appel à votre backend :

```html
            <a
                href="javascript:"
                class="js-like-article"
                data-like-url="USE TWIG url() TO GENERATE URL TO YOUR API ENDPOINT">
                ❤
            </a>
```

Dernière étape dans `assets/js/app.js` ajouter le code néccesaire pour rendre le système fonctionnel.

```js
$(document).ready(function () {
    $('.js-like-article').on('click', function (event) {
        // PreventDefault and StopPropagation

        // Get Target clicked

        // Make XHR call to your api endpoint and update like counter .js-like-article-count
    });
});
```