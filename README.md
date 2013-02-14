ZendSkeletonApplication
=======================

Introduction
------------
This is a simple, skeleton application using the ZF2 MVC layer and module
systems. This application is meant to be used as a starting place for those
looking to get their feet wet with ZF2.


Installation
------------

Using Composer (recommended)
----------------------------
The recommended way to get a working copy of this project is to clone the repository
and use `composer` to install dependencies using the `create-project` command:

    curl -s https://getcomposer.org/installer | php --
    php composer.phar create-project --repository-url="http://packages.zendframework.com" zendframework/skeleton-application path/to/install

Alternately, clone the repository and manually invoke `composer` using the shipped
`composer.phar`:

    cd my/project/dir
    git clone git://github.com/zendframework/ZendSkeletonApplication.git
    cd ZendSkeletonApplication
    php composer.phar self-update
    php composer.phar install

(The `self-update` directive is to ensure you have an up-to-date `composer.phar`
available.)

Another alternative for downloading the project is to grab it via `curl`, and
then pass it to `tar`:

    cd my/project/dir
    curl -#L https://github.com/zendframework/ZendSkeletonApplication/tarball/master | tar xz --strip-components=1

You would then invoke `composer` to install dependencies per the previous
example.

Using Git submodules
--------------------
Alternatively, you can install using native git submodules:

    git clone git://github.com/zendframework/ZendSkeletonApplication.git --recursive

Virtual Host
------------
Afterwards, set up a virtual host to point to the public/ directory of the
project and you should be ready to go!

Using Doctrine ORM
------------------
### Configurations

```
cp config/autoload/database.local.php.dist config/autoload/database.local.php
```

Edit the file `database.local.php` with your settings.

### Entities

[Doctrine ORM Getting Started](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/tutorials/getting-started.html)

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

After updating your entity class, generate and execute the update SQL:

```
php vendor/bin/doctrine-module orm:schema-tool:update --dump-sql
```

### Migrations

You can also generate database migrations for incremental database development:

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
