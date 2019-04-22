Database
========

Commandes :

1. php bin/console doctrine:database:drop --force
2. php bin/console doctrine:database:create
3. php bin/console make:entity
4. php bin/console doctrine:schema:validate
5. php bin/console doctrine:migration:diff
6. php bin/console doctrine:migration:migrate
7. php bin/console doctrine:fixtures:load

Créer une entité `App\Entity\Article` avec l'aide de `make:entity`. 

Liste des propriétés :
* title (string, 255)
* content (text)
* nbLikes (int, default : 0)

Une fois votre entité complète, il faut créer et exécuter une migration. (cf: doctrine:migration)

Essayer de connecter votre base de données et saisir des données manuellement.

Création des données de développement : [Documentation fixtures](https://symfony.com/doc/master/bundles/DoctrineFixturesBundle/index.html)
Bonus : générer des données aléatoire lisibiles : [Librairie Faker](https://github.com/fzaninotto/Faker) pour rappel via `composer require`.

Corriger votre controller `App\Controller\HomeController` pour recupèrer `App\Repository\ArticleRepository` via 
l'injection de dépendances ([Fetching and using Services](https://symfony.com/doc/current/service_container.html)).
