Service Container
=================

[Service container documentation](https://symfony.com/doc/current/service_container.html)

* `php bin/console debug:autowiring`

Ajouter des logs comme l'exemple via le TP-composer dans votre HomeController : 

* Il faut utiliser `Psr\Log\LoggerInterface` pour indiquer à symfony de vous fournir une implémentation dans votre controller.

```php
use Psr\Log\LoggerInterface;

class HomeController extends AbstractController
{

    /**
     * @var \Psr\Log\LoggerInterface
     */
    private $logger;

    public function __construct(
        LoggerInterface $logger
    )
    {
        $this->logger = $logger;
    }

    ... use logger in methods
```

Ajouter un log quand on clique sur ajouter un like sur un article.