ZendSkeletonApplication + DoctrineORMModule
===========================================

Configuration
-------------

```
cp config/autoload/database.local.php.dist config/autoload/database.local.php
```

Edit the file `database.local.php` with your settings.

Entities
--------

Example:

```php
namespace Application\Entity;

use Doctrine\ORM\Mapping as ORM;

/**
 * module/Application/src/Application/Entity/Product.php
 * @ORM\Entity @ORM\Table(name="products")
 **/
class Product
{
    /** @ORM\Id @ORM\Column(type="integer") @ORM\GeneratedValue **/
    protected $id;
    /** @ORM\Column(type="string") **/
    protected $name;
}
```

Check your entity class:

```
php vendor/bin/doctrine-module orm:info
```

Create table from entity:

```
php vendor/bin/doctrine-module orm:schema-tool:create
```

After updating your entity class, for example, adding new attributes:

```php
class Product
{
    /** @ORM\Column(type="string") **/
    protected $description;
}
```

generate and execute the update SQL:

```
php vendor/bin/doctrine-module orm:schema-tool:update --dump-sql
```

Migrations
----------

Sometimes you will need run more advanced changes on database than simple
adding new attributes. You can generate database migrations for incremental
database development:

```
php vendor/bin/doctrine-module migrations:generate
```

Edit generated file:

```php
public function up(Schema $schema)
{
    $this->addSql('ALTER TABLE products ADD description TEXT NOT NULL');
}

public function down(Schema $schema)
{
    $this->addSql('ALTER TABLE products DROP description');
}
```

Then run:

```
php vendor/bin/doctrine-module migrations:migrate
```

References
----------

[Doctrine ORM Getting Started](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/tutorials/getting-started.html)

