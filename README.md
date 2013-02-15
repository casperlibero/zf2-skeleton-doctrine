ZendSkeletonApplication + DoctrineORMModule
===========================================

Configuração
------------

```
cp config/autoload/database.local.php.dist config/autoload/database.local.php
```

Configurar o arquivo `database.local.php`.

Entidades
---------

Exemplo:

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

Verifique se a classe da entidade está funcionando corretamente:

```
php vendor/bin/doctrine-module orm:info
```

Criar a tabela no banco de dados a partir da classe da entidade:

```
php vendor/bin/doctrine-module orm:schema-tool:create
```

Sempre que atualizar sua classe de entidade, como por exemplo, a inclusão de um novo atributo:

```php
class Product
{
    /** @ORM\Column(type="string") **/
    protected $description;
}
```

A tabela no banco de dados pode ser atualizada automaticamente:

```
php vendor/bin/doctrine-module orm:schema-tool:update
```

Migrations
----------

É recomendado que as alterações de banco de dados sejam incrementais, através de migrations:

```
php vendor/bin/doctrine-module migrations:generate
```

Edite o arquivo gerado:

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

e execute-o:

```
php vendor/bin/doctrine-module migrations:migrate
```

Referências
-----------

[Doctrine ORM Getting Started](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/tutorials/getting-started.html)
