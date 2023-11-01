# Connexion à la base de données

Nous allons voir la partie "Model" du framework MVC Symfony.

Dans la plupart des projets Symfony, la connexion à la base de données est effectuée grâce à Doctrine.

Doctrine est un ORM [(Object-Relational Mapping)](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel).

Cela veut dire que les tables SQL ne sont pas manipulées directement (grâce à des requêtes SQL classiques), mais que
chaque table est représenté par une classe.

Dans la précédente partie du TP, nous avons créé un objet `Article` qui est la représentation d'un Article de blog dans
notre application.

Doctrine va prendre une classe comme celle-là et va la faire correspondre (mapper) à une table SQL.

Par exemple, le champ `title` de notre classe correspondra au champ `title` dans notre table SQL article.

Cette notion est assez compliquée à comprendre, nous allons essayer de comprendre par l'exemple.

## Installation

On installe Doctrine à l'aide de composer. `orm` est un alias de `symfony/orm-pack` qui installe toutes les dépendances
nécessaires à Doctrine pour fonctionner.

```bash
composer require orm
```

Symfony Flex modifie le fichier `.env` pour y ajouter une variable `DATABASE_URL` avec une valeur par défaut.

En général, les valeurs par défaut pour MySQL sont l'utilisateur root sans mots de passe.

La valeur de `db_name` n'a pas d'importance, c'est Doctrine qui va se charger de créer la DB, vous pouvez donc mettre ce
que vous souhaitez.

Enfin pour la version, vérifier que vous ayez bien la 5.7, si ce n'est pas le cas, remplacez 5.7 par votre version
actuelle

Si vous avez une base mariadb, elle est considérée par Doctrine comme mysql donc, faites comme si c'était un MySQL.

Vous devriez donc remplacer dans le fichier `.env` :

```diff
- DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=15&charset=utf8"
+ DATABASE_URL="mysql://root:@127.0.0.1:3306/my_blog?serverVersion=5.7&charset=utf8mb4"
```

NB : Doctrine possède une partie nommée DBAL (Database abstraction layer), qui fait abstraction du SGBD utilisé. Il est
donc possible d'utiliser PostgreSQL ou SQLite par exemple. Pour éviter les problèmes spécifiques à chaque plateforme,
nous allons utiliser MySQL dans le cadre de ce TP.

Commandes pour créer la base de données :

1. `php bin/console doctrine:database:drop --force --if-exists` supprime la base de données si elle existe.
2. `php bin/console doctrine:database:create` - création de la base de données.

Créer une entité `App\Entity\Article` avec l'aide de `php bin/console make:entity`.

Pour les différents champs à ajouter et leur type, référez-vous à la partie sur Twig à l'exception de body où vous
mettrez text au lieu de string.

Observez la classe `Article` créée par la commande.

Vous remarquerez l'attribut `#[ORM\Entity]` en haut de classe, qui permet de spécifier à Doctrine que cette classe est
une entité. Il y a également des attributs `#[ORM\Column]` au-dessus de chaque propriété qui servent à définir le type
et les contraintes de chaque colonne en base de données.

Cette commande a également généré une seconde classe `ArticleRepository` mais nous y reviendrons plus tard.

Voici un exemple tiré de la documentation officielle qui illustre le travail effectué par Doctrine.

![Mapping single entity](https://symfony.com/doc/current/_images/mapping_single_entity.png)

Une fois votre entité complète, il faut créer et exécuter une migration. Une migration est un fichier qui est créé par
Doctrine et qui contient les requêtes SQL à exécuter pour créer, modifier ou supprimer une table.

Pour cela Doctrine compare le mapping (les attributs dans la classe `Article`) et l'état actuel de la base de données.

Comme la table `article` n'existe pas, Doctrine va la créer avec tous les champs de notre entité.

Exécuter la commande `php bin/console make:migration` ou `php bin/console doctrine:migration:diff` qui calcule la
différence entre le mapping et la DB.

Observez le fichier généré dans `src/Migrations`

Pour l'exécuter, il faut taper la commande `php bin/console doctrine:migration:migrate`

Cette commande va exécuter toutes les migrations qui n'ont pas encore été appliquées à la base de données. Ainsi, si
vous tapez cette commande à nouveau, Doctrine devrait vous dire qu'il n'y a rien à exécuter.

Il en est de même pour `php bin/console doctrine:migration:diff`, cela va générer un fichier de migration vide, car il
n'y a plus de différences entre le mapping et la DB.

## Fixtures

Afin de faciliter le développement et avant d'avoir à notre disposition un formulaire pour créer des articles, nous
allons créer des fixtures.

Ce sont des fichiers php dans lesquels nous allons créer de faux articles pour le développement.

Regardez la [documentation des fixtures](https://symfony.com/bundles/DoctrineFixturesBundle/current/index.html) pour
comprendre comment cela fonctionne. Appliquez cette logique à nos articles pour créer 10 articles avec l'aide de Faker
pour générer des données aléatoires lisibles : [Librairie Faker](https://fakerphp.github.io/) pour rappel via composer
require.

Puis chargez ces fixtures avec la commande `php bin/console doctrine:fixtures:load`

## Et si on affichait tout ça ?

Si tout s'est bien passé, vous devriez avoir 10 articles en DB.

Il faut récupérer les articles grâce à la classe `ArticleRepository` que nous avions volontairement mis de côté plus tôt
dans le TP.

Un Repository, dans Doctrine, c'est une classe qui possède des méthodes permettant de récupérer des entités.

Par défaut, un répository possède plusieurs méthodes, dont la méthode findAll() que nous allons utiliser dans notre
Controller.

### Comment récupérer un repository ?

Grâce au Dependency Injection Container (DIC).

En Symfony, chaque classe créée est considérée comme un service à l'exception des classes définies dans `Entity`
et `Migrations` ainsi que la classe Kernel.php.

Un service, c'est un objet qui a une fonction précise et qui sont gérés par le DIC.

Ce DIC nous permet d'injecter les services dans nos controllers par exemple (mais aussi dans d'autres services !),
c'est-à-dire rendre disponible le service dans le controller.

Généralement, l'injection de dépendances est réalisée dans le constructeur de notre controller et depuis Symfony 4,
nous pouvons utiliser l'autowiring pour l'injection de dépendances.

L'autowiring consiste à utiliser le typage des paramètres du constructeur pour injecter nos dépendances automatiquement.

Plus d'informations sur les services et le DIC [ici](https://symfony.com/doc/6.3/service_container.html).

Ici, en ajoutant le code ci-dessous à notre HomeController, nous avons maintenant accès à $this->articleRepository.

```php
private $articleRepository;

public function __construct(ArticleRepository $articleRepository)
{
    $this->articleRepository = $articleRepository;
}
```

⚠️ n'oubliez pas le `use` en haut de votre fichier pour importer `ArticleRepository`.

Utiliser maintenant la méthode `findAll()` du repository pour remplacer le tableau `articles` que nous passions au
template Twig.

En actualisant la page, vous devriez voir vos articles créés grâce aux fixtures !

### Débugger le SQL généré par Doctrine

Cliquez sur l'icône "doctrine" dans la debug bar.

Vous arrivez sur une page du Profiler qui vous indique quelles sont les requêtes SQL qui ont été exécutées.

On voit ici que Doctrine génère une requête SQL qui SELECT tous nos champs de la table article.

### Ok, mais là, on affiche tous les articles ?!

Oui... Si demain, on a 100, 1000, 10000 articles, ils seront tous affichés sur la page d'accueil.

Vous pouvez même tester en augmentant le nombre d'itérations dans vos fixtures pour générer des centaines ou milliers
d'articles.

C'est là qu'intervient : le repository !

Nous allons ici créer une méthode customisée `findLast` dans le repository qui va nous permettre de récupérer seulement
les derniers articles.

```php
public function findLast(int $count) {
    return $this->createQueryBuilder('article')
        ->getQuery()
        ->getResult()
    ;
}
```

Nous créons ici un `QueryBuilder`, c'est l'objet que nous allons manipuler afin de construire nos requêtes dans un
langage assez proche du SQL, le DQL (Doctrine Query Language).

Le code ci-dessus revient à exécuter la requête SQL `SELECT * FROM article`, sauf que Doctrine va automatiquement créer
des objets `Article` à partir du résultat de la requête SQL. C'est ce qu'a également fait la méthode `findAll` que nous
avons utilisé précédemment. Ce processus est appelé hydratation.

À l'aide du code ci-dessus et de
la [documentation du QueryBuilder](https://www.doctrine-project.org/projects/doctrine-orm/en/2.16/reference/query-builder.html#working-with-querybuilder),
récupérez les 4 derniers articles et affichez-les sur la page d'accueil, du plus récent au plus ancien.

À nouveau, regardez l'onglet Doctrine dans le profiler et observez la nouvelle requête générée.

## Résumons…

Dans cette partie, nous avons vu comment ajouter une connexion à la base de données grâce à Doctrine, les entités et les
repositories.

Nous avons aussi vu comment générer des tables SQL grâce aux entités et aux migrations et comment générer de fausses
données pour le développement.

Nous avons également abordé l'injection de dépendances.

Avec tout ça, nous avons maintenant presque une page d'accueil fonctionnelle à l'exception de :

Les liens sur le titre des articles doivent nous rediriger vers la vue de l'article en question, c'est ce que nous
allons voir dans le prochain tp.