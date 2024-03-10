# **Entities**

## Introduction

Entities are the foundation of object-relational mapping (ORM) in NexaORM. They represent database tables and map their columns to properties within your PHP classes. This approach simplifies database interactions by allowing you to work with objects instead of raw SQL.

## Creating Entities

**Define an Entity Class:**

Create a PHP class and decorate it with the `#[Entity]` attribute to mark it as an entity.

**Properties:**

   1. Declare properties within the class to represent database table columns.
   2. Use appropriate NexaORM attributes to define data types, constraints, relationships, and other aspects.

## Common NexaORM Attributes for Entities

- **`#[PrimaryKey]`:** Marks a property as the primary key of the table (can be used only once per entity).
- **`#[AutoIncrement(true)]` (with `#[PrimaryKey]`):** Enables auto-incrementing for the primary key.
- **`#[Strings]`:** Defines a string type for a property.
- **`#[Number]`:** Defines a numeric type for a property.
- **`#[SmallInt]`:** Specifies a small integer type (usually 2 bytes).
- **`#[DefaultValue(...)]`:** Sets a default value for a property.
- **`#[ForeignKey(targetEntityClass, targetProperty, onDelete = Nexa::CASCADE, onUpdate = Nexa::CASCADE)]`:** Defines a foreign key relationship to another entity.
       - `targetEntityClass`: The class of the related entity.
       - `targetProperty`: The property in the related entity that this property references.
       - `onDelete`: Action to take when a row in the referenced table is deleted (defaults to `Nexa::SET_NULL`).
       - `onUpdate`: Action to take when a row in the referenced table is updated (defaults to `Nexa::NO_ACTION`).
- **`#[Comment('...')]`:** Adds a comment to a property (visible in database schema).
- **`#[Nullable]`:** Allows a property to be null.
- **`#[DateAndTime]`:** Defines a property to hold a date and time value.
- **`#[DefaultValue(Nexa::DATETIME_NOW)]`:** Sets the default value of a `#[DateAndTime]` property to the current date and time.

## Example Entity

```php
namespace Nexa\Test\Entities;

use DateTime;
use Nexa\Attributes\Common\AutoIncrement;
use Nexa\Attributes\Common\Comment;
use Nexa\Attributes\Common\DefaultValue;
use Nexa\Attributes\Common\ForeignKey;
use Nexa\Attributes\Common\Nullable;
use Nexa\Attributes\Common\PrimaryKey;
use Nexa\Attributes\Dates\DateAndTime;
use Nexa\Attributes\Entities\Entity;
use Nexa\Attributes\Numbers\Number;
use Nexa\Attributes\Numbers\SmallInt;
use Nexa\Attributes\Strings\Strings;
use Nexa\Nexa;

#[Entity]
class UserEntity
{

  #[PrimaryKey]
  #[SmallInt]
  #[AutoIncrement(true)]
  public int $id;

  #[Strings]
  #[DefaultValue('John')]
  public string $username;

  #[Number]
  #[ForeignKey(ProfileEntity::class, 'id', [Nexa::ON_DELETE => Nexa::CASCADE, Nexa::ON_UPDATE => Nexa::CASCADE])]
  #[Comment('user profile')]
  #[Nullable]
  public int $profile;

  #[DateAndTime]
  #[DefaultValue(Nexa::DATETIME_NOW)]
  public DateTime $created_at;
}
```

## Benefits of Using Entities

- **Simplified Database Interactions:** Work with objects instead of raw SQL queries.
- **Improved Code Readability:** Code becomes more self-documenting due to descriptive properties and attributes.
- **Reduced Errors:** Type checking and constraints help prevent errors and maintain data integrity.

## Additional Considerations

- Refer to the NexaORM documentation for a complete list of [available attributes](attributes.md).
- Consider using data validation techniques to ensure data integrity before saving entities.

By effectively utilizing entities in your NexaORM projects, you'll enhance database interaction clarity, maintainability, and data integrity.