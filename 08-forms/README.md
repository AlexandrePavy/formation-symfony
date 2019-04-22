Form
====

[Symfony form documentation](https://symfony.com/doc/current/forms.html)

1. `composer require form`
2. `composer require validator`
3. `php bin/console make:form` 

Création d'un form symfony avec maker bundle (ArticleType sur l'entité Article), observer la classe `App\Form\ArticleFormType`.

Création d'une nouvelle route de création d'un article :

```php
    use App\Form\ArticleFormType;
    use Symfony\Component\HttpFoundation\Request;

    /**
     * @Route("/new", name="article_new")
     */
    public function new(Request $request)
    {
        // Create form
        $form = $this->createForm(ArticleFormType::class);

        // Handle Request (Récupère les params de la Request HTTP et les envoit dans le $form)
        $form->handleRequest($request);

        // Dans le cas ou le form est valide et pousser en POST
        if ($form->isSubmitted() && $form->isValid()) {
            // On récupère l'article depuis le form (on sait qu'il est valide maintenant (enfin presque => voir Symfony Validator))

            /** @var Article $article */
            $article = $form->getData();

            $entityManager = $this->getDoctrine()->getManager();

            $entityManager->persist($article);
            $entityManager->flush();

            // On redirige vers la homepage
            return $this->redirectToRoute('homepage');
        }

        return $this->render('homepage/new.html.twig', [
            'form' => $form->createView(),
        ]);
    }
```

Add bootstrap template dans la config twig `config/packages/twig.yaml`.
```yaml
twig:
    form_themes:
        - bootstrap_4_layout.html.twig
```


Bonus : 

* Ajouter un message flash : [Flash Message](https://symfony.com/doc/current/controller.html#flash-messages)
* Jouer avec `php bin/console make:crud` - génére Create / Read / Update / Delete pour une entité
* Symfony Validator
* Symfony repository custom
* Doctrine relation
* Essayer des bundles : 
    * https://symfony.com/doc/current/bundles/FOSCKEditorBundle/installation.html
