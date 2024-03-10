## NexaORM: Configuration

NexaORM allows for centralized configuration of your database settings in a dedicated file, `database.php`. This approach offers several advantages:

- **Improved Readability and Maintainability:** Separates database configurations from your core application logic.
- **Simplified Environment Management:** Enables configuration of different environments (development, production, etc.) with specific files.
- **Configuration Sharing:** Facilitates sharing of database configuration across multiple applications using NexaORM.

**Sample `database.php` Configuration File:**

```php
<?php

return [

    'host' => 'localhost',
    'user' => 'root',
    'password' => '',
    'dbname' => 'floky',
    'driver' => 'pdo_mysql',

    'options' => [

        'migrations_path' => __DIR__ . "/migrations/",
        'entity_path' => __DIR__ . "/Entities/",
        'entity_namespace' => "\\Nexa\\Test\\Entities",
    ]

];
```

**Inheritance and Automatic Configuration:**

By inheriting from the `Nexa\Models\Model` class and overriding the `setConfigPath()` method, you can automatically load the configuration from `database.php`. This approach simplifies your model code and centralizes configuration.

**Sample `Model.php` Model:**

```php
<?php

namespace App\Models;

use Nexa\Models\Model as BaseModel;

class Model extends BaseModel
{

    public function __construct()
    {

        $this->setConfigPath('database.php');
        parent::__construct();

    }

}
```

**Sample `User.php` Model:**

```php
<?php

namespace App\Models;

use App\Entities\UserEntity;

class User extends Model
{

    protected $entity = UserEntity::class;

    protected $fillable = ['username', 'created_at'];

}
```

**Benefits of Inheritance:**

- **Reduced Redundant Code:** Eliminates the need to repeat database configuration in each model.
- **Improved Consistency:** Ensures all models utilize the same configuration.
- **Easier Maintenance:** Allows configuration changes in a single location.

**Conclusion:**

Leveraging a centralized configuration file and inheriting from NexaORM's `Model` class provides an efficient approach to managing database configuration within your PHP applications. This approach enhances code readability, maintainability, and consistency.

**Key Takeaways:**

- Define database connection parameters in `database.php`.
- Override the `setConfigPath()` method in your model class to load configuration from `database.php`.
- Inherit from `Nexa\Models\Model` for automatic configuration benefits.

By following these guidelines, you can effectively configure NexaORM and harness its features for streamlined database interactions in your projects.