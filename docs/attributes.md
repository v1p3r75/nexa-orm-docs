# **Attributes**

## Introduction

NexaORM attributes play a vital role in defining the characteristics and behavior of entities and their properties. They provide metadata that enriches the framework and guides its interactions with the database.

## Types of Attributes

**Entity Attributes:**

   - `#[Entity]`: Designates a class as an entity that can be mapped to a database table.

**Property Attributes:**

   - **Data Types:**
      - `#[Strings]`: Designates a property as a string type.
      - `#[Number]`: Designates a property as a numeric type.
      - `#[SmallInt]`: Designates a property as a small integer type (2 bytes).
      - `#[DateAndTime]`: Designates a property as a date and time type.
      - ...

   - **Constraints and Default Values:**
      - `#[PrimaryKey]`: Designates the property as the primary key of the entity.
      - `#[AutoIncrement(true)]` (with `#[PrimaryKey]`): Enables auto-incrementing for the primary key.
      - `#[DefaultValue(...)]`: Sets a default value for a property.
      - `#[Nullable]`: Allows the property to be null.
      - ...

   - **Relationships:**
      - `#[ForeignKey(targetEntityClass, targetProperty, onDelete = Nexa::CASCADE, onUpdate = Nexa::CASCADE)]`: Defines a foreign key relationship with another entity.
         - `targetEntityClass`: Class of the related entity.
         - `targetProperty`: Property in the related entity that this property references.
         - `onDelete`: Action to take when a row in the linked table is deleted (default: `Nexa::SET_NULL`).
         - `onUpdate`: Action to take when a row in the linked table is updated (default: `Nexa::NO_ACTION`).

   - **Miscellaneous:**
      - `#[Comment('...')]`: Adds a comment to a property (visible in the database schema).
      - ...

## Example Attributes

```php
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
  #[ForeignKey(ProfileEntity::class, 'id', [Nexa::ON_DELETE => Nexa::CASCADE, onUpdate => Nexa::CASCADE])]
  #[Comment('user profile')]
  #[Nullable]
  public int $profile;

  #[DateAndTime]
  #[DefaultValue(Nexa::DATETIME_NOW)]
  public DateTime $created_at;
}
```

## Benefits of Attributes

- **Rich Metadata:** Define additional information about entities and their properties.
- **Clearer and More Precise Code:** Enhance code readability and understanding.
- **Improved Relationship Management:** Facilitate creation and management of relationships between entities.
- **Flexibility and Customization:** Allow tailoring entity behavior to specific needs.


**In summary, NexaORM attributes are an essential element for fully leveraging the framework's power and flexibility. By using them effectively, you can design robust entities and achieve more efficient database interactions.**