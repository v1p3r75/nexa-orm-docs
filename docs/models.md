## NexaORM: Models

**Introduction**

NexaORM models act as a bridge between your entities and the database. They encapsulate the logic for interacting with entities, including data retrieval, creation, modification, and deletion. Models simplify database operations and provide a layer of abstraction between your application logic and the underlying persistence layer.

**Model Structure**

A typical NexaORM model inherits from the `Nexa\Models\Model` class and defines the following properties to customize its behavior:

**Required Property:**

- `protected $entity`: (Required) Specifies the entity class associated with the model. This class represents the database table structure.

**Optional Properties:**

- `protected $hidden`: (Optional) An array listing entity properties that should be excluded from serialization (e.g., JSON encoding).
- `protected $fillable`: (Optional) An array listing the entity properties that can be mass-assigned during data operations (e.g., creation, update). By default, all properties are fillable.
- `protected $timestamp`: (Optional) A boolean value indicating whether timestamps (`created_at` and `updated_at`) should be automatically managed for the entity. Defaults to `true`.
- `protected $soft_delete`: (Optional) A boolean value indicating whether soft delete functionality should be enabled. When enabled, deleted entities are not physically removed from the database but marked as deleted with a `deleted_at` timestamp. Defaults to `false`.
- `protected $primaryKey`: (Optional) Specifies the name of the primary key column in the database table. Defaults to `"id"`.
- `protected $date_format`: (Optional) Defines the format used for storing and retrieving date and time values in the database. Defaults to `"Y-m-d H:i:s"` (year-month-day hour:minute:second).
- `protected $created_at`: (Optional) Specifies the name of the property in the entity that holds the creation timestamp. Defaults to `"created_at"`.
- `protected $updated_at`: (Optional) Specifies the name of the property in the entity that holds the update timestamp. Defaults to `"updated_at"`.
- `protected $deleted_at`: (Optional) Specifies the name of the property in the entity that holds the soft delete timestamp (if enabled). Defaults to `"deleted_at"`.

**Example Model:**

```php
namespace Nexa\Test\Models;

use Nexa\Models\Model;
use Nexa\Test\Entities\UserEntity;

class User extends Model
{

  protected $entity = UserEntity::class;

  protected $hidden = ['password']; // Exclude password from serialization

  protected $fillable = ['username', 'email']; // Allow mass assignment of specific properties

  protected $timestamp = false; // Disable automatic timestamps

  protected $soft_delete = true; // Enable soft delete functionality

  // Other properties can be set as needed
}
```

**Explanation:**

- This model inherits from `Model` and associates itself with the `UserEntity` class.
- It excludes the `password` property from serialization for security reasons.
- It allows mass assignment only for `username` and `email` properties during creation or update.
- It disables automatic timestamp management and enables soft delete functionality.

**Benefits of Models**

- **Simplified Database Interactions:** Models provide methods for common database operations, reducing the need for manual SQL queries.
- **Data Validation and Security:** Models can enforce data validation rules and control which properties can be modified, enhancing data integrity and security.
- **Improved Code Readability:** Models encapsulate database logic, making code cleaner and easier to maintain.

**Additional Considerations**

- Consider using data validation techniques within models to ensure data integrity before saving entities.
- Explore other features offered by NexaORM models, such as eager loading and relationships.

By effectively utilizing models with various properties, you can customize database interactions, manage data visibility, enforce security, and streamline database operations in your NexaORM projects.