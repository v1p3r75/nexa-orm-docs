# **Models**

## Introduction

**NexaORM** models act as a bridge between your entities and the database. They encapsulate the logic for interacting with entities, including data retrieval, creation, modification, and deletion. Models simplify database operations and provide a layer of abstraction between your application logic and the underlying persistence layer.

## Model Structure

A typical NexaORM model inherits from the `Nexa\Models\Model` class and defines the following properties to customize its behavior:

**Required Property:**

  - `$entity`: (Required) Specifies the entity class associated with the model. This class represents the database table structure.

**Optional Properties:**

  - `$hidden`: (Optional) An array listing entity properties that should be excluded from serialization (e.g., JSON encoding).
  - `$fillable`: (Optional) An array listing the entity properties that can be mass-assigned during data operations (e.g., creation, update). By default, all properties are fillable.
  - `$timestamp`: (Optional) A boolean value indicating whether timestamps (`created_at` and `updated_at`) should be automatically managed for the entity. Defaults to `true`.
  - `$soft_delete`: (Optional) A boolean value indicating whether soft delete functionality should be enabled. When enabled, deleted entities are not physically removed from the database but marked as deleted with a `deleted_at` timestamp. Defaults to `false`.
  - `$primaryKey`: (Optional) Specifies the name of the primary key column in the database table. Defaults to `"id"`.
  - `$date_format`: (Optional) Defines the format used for storing and retrieving date and time values in the database. Defaults to `"Y-m-d H:i:s"` (year-month-day hour:minute:second).
  - `$created_at`: (Optional) Specifies the name of the property in the entity that holds the creation timestamp. Defaults to `"created_at"`.
  - `$updated_at`: (Optional) Specifies the name of the property in the entity that holds the update timestamp. Defaults to `"updated_at"`.
  - `$deleted_at`: (Optional) Specifies the name of the property in the entity that holds the soft delete timestamp (if enabled). Defaults to `"deleted_at"`.

## Example Model

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

## Explanation

- This model inherits from `Model` and associates itself with the `UserEntity` class.
- It excludes the `password` property from serialization for security reasons.
- It allows mass assignment only for `username` and `email` properties during creation or update.
- It disables automatic timestamp management and enables soft delete functionality.

## Available Methods on Models

NexaORM empowers you with a comprehensive set of methods to interact with your database models, streamlining data retrieval, manipulation, and management. Here's a breakdown of the essential methods you'll frequently leverage:

**Retrieving Data:**

  - **`find($id)`:** Locates a single model record based on its primary key, returning a collection or `false` if not found.
  - **`findOrFail($id)`:** Fetches a single record by its primary key, throwing a `NotFoundException` if not found.
  - **`findAll(array $columns = ["*"])`:** Retrieves all records for the model, optionally specifying columns for inclusion.
  - **`like(string $column, string $search, $columns = ['*'])`:** Searches for records based on a partial string match within a specified column.

**Creating Data:**

  - **`insert(array $data)`:** Inserts a new model record into the database.

**Updating Data:**

  - **`update(array $data, array $conditions = [])`:** Updates existing model records matching specified conditions.

**Deleting Data:**

  - **`delete($id)`:** Removes a single record by its primary key, considering soft delete configuration if enabled.
  - **`deleteWhere(array $conditions)`:** Deletes records based on given conditions.

**Additional Methods:**

  - **`beginTransaction()`:** Initiates a database transaction.
  - **`commitTransaction()`:** Commits changes within a transaction.
  - **`transactional(Closure $function)`:** Executes a function within a transaction.
  - **`random()`:** Fetches a random model record.

These robust methods equip you with the tools necessary to effectively interact with your database and manage model data within your NexaORM applications.

**Automatic Foreign Key Data Fetching**

NexaORM further simplifies your data management by automatically fetching foreign key information. This powerful feature allows you to access related data without writing additional code.

**Example:**

Imagine your `Article` model has a foreign key `category_id` referencing the `Category` model. When using `find($id)` to retrieve an article, NexaORM will automatically fetch the corresponding category information and include it in the result.

**Benefits of Automatic Foreign Key Data Fetching:**

- **Reduced Code:** Eliminates the need for manual table joins to retrieve related data.
- **Improved Code Readability:** Makes your code more concise and easier to understand.
- **Time and Effort Savings:** Streamlines the process of retrieving complex data.

**How Automatic Foreign Key Data Fetching Works:**

NexaORM analyzes the relationships defined in your models and uses that information to automatically load foreign key data. You can customize this behavior by configuring fetch options for relationships within your models.

**Conclusion:**

NexaORM's automatic foreign key data fetching is a powerful tool that simplifies and optimizes data access in your applications. By leveraging this feature, you can save time, improve code readability, and focus on your application's core business logic.

**In summary, NexaORM is committed to simplifying complex data management by automating foreign key data fetching. This powerful feature empowers you to save time, improve code readability, and focus on what matters most in your application.**

## Benefits of Models

- **Simplified Database Interactions:** Models provide methods for common database operations, reducing the need for manual SQL queries.
- **Data Validation and Security:** Models can enforce data validation rules and control which properties can be modified, enhancing data integrity and security.
- **Improved Code Readability:** Models encapsulate database logic, making code cleaner and easier to maintain.

## Additional Considerations

- Consider using data validation techniques within models to ensure data integrity before saving entities.
- Explore other features offered by NexaORM models, such as eager loading and relationships.

By effectively utilizing models with various properties, you can customize database interactions, manage data visibility, enforce security, and streamline database operations in your NexaORM projects.