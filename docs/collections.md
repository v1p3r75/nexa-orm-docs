# **Collections**

## Introduction

Collections are fundamental components in NexaORM, representing a group of entities retrieved from the database. They provide a convenient way to work with multiple entities at once and offer various methods for manipulating and iterating through the data.

## The `Collection` Class

NexaORM provides a built-in `Collection` class that implements the `Countable` and `ArrayAccess` interfaces. This class offers a set of methods for working with collections of entities:

- **`__construct(array $items)`:** Initializes the collection with an array of entities.
- **`count()`:** Returns the number of entities in the collection.
- **`get(string $key)`:** Retrieves the entity with the specified key (usually the entity's primary key).
- **`all(?callable $callback = null)`:** Returns an array containing all entities in the collection. Optionally applies a callback function to each entity.
- **`__get($name)`:** Magic method that allows accessing entities by property name (equivalent to `get($name)`).
- **`random()`:** Selects and returns a random entity from the collection.
- **`offsetExists(mixed $offset)`:** Checks if a specific offset exists in the collection (similar to array access).
- **`offsetGet(mixed $offset)`:** Retrieves the entity at the specified offset.
- **`offsetSet(mixed $offset, mixed $value)`:** Sets the entity at the specified offset.
- **`offsetUnset(mixed $offset)`:** Removes the entity at the specified offset.
- **`first()`:** Returns the first entity in the collection.
- **`last()`:** Returns the last entity in the collection.
- **`filter(callable $callback)`:** Creates a new collection containing entities that pass the provided callback function.
- **`map(callable $callback)`:** Applies the callback function to each entity in the collection and returns a new collection with the modified entities.
- **`has(string $key)`:** Checks if the collection contains an entity with the specified key.
- **`values()`:** Returns an array containing the values (entities) from the collection.
- **`keys()`:** Returns an array containing the keys (usually primary keys) from the collection.
- **`isEmpty()`:** Checks if the collection is empty.

## Benefits of Collections

- **Efficient Data Handling:** Collections provide a streamlined way to manage and manipulate multiple entities retrieved from database queries.
- **Simplified Iterations:** Collection methods like `all()`, `filter()`, and `map()` allow you to easily iterate through entities and perform operations on them.
- **Improved Code Readability:** Using collections keeps your code clean and focused on data processing rather than low-level array manipulations.

## Example Usage

```php
<?php

$users = User::findAll(); // Retrieve all users as Collection

if ($users->isEmpty()) {
  // Handle empty collection
} else {
  foreach ($users as $user) {
    echo $user->username . PHP_EOL;
  }

  $activeUsers = $users->filter(fn ($user) => $user->isActive); // Filter active users

  $usernames = $users->map(fn ($user) => $user->username); // Extract usernames
}
```

By understanding and effectively utilizing NexaORM collections, you can enhance the efficiency and clarity of your database interactions within your NexaORM projects.