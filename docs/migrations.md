# **Migrations**

NexaORM offers intelligent auto-generation of migrations based on your entities. This feature analyzes changes to your entities and creates the necessary migrations to update your database schema accordingly.


## Benefits of Auto-Generated Migrations

- **Save Time and Effort:** Eliminates tedious manual creation of migrations.
- **Reduced Errors:** Ensures consistency between entities and database structure.
- **Easier Change Tracking:** Provides a history of database schema modifications.

## Example of Generating Migrations

```php
<?php

// Example

require './vendor/autoload.php';

use Nexa\Nexa;

$nexa = Nexa::getInstance(__DIR__ . "/tests/database.php");

// Generate migrations for all entities
$nexa->makeAllMigrations();

// Run all generated migrations
$nexa->runAllMigrations();

```

## Intelligent Migration Execution

NexaORM goes beyond just generating migrations; it also executes them intelligently. It analyzes existing migrations and compares their structure to the current database schema. NexaORM only executes the migrations necessary to update the database based on detected changes.

## Benefits of Intelligent Migration Execution

- **Optimized Execution:** Avoids wasting resources on unnecessary migrations.
- **Change Management:** Accounts for modifications to entity structures.
- **Increased Safety:** Reduces the risk of errors during migration execution.


## Advanced Features

- **Rebuild Migrations:** Rebuild existing migrations based on current entities.
- **Selective Migration Execution:** Option to specify which migrations to execute.
- **Rollback Management:** Ability to revert to a previous database version.

## Conclusion

NexaORM's intelligent auto-generated migrations provide a powerful tool for simplifying database schema management. By automating migration creation and execution, NexaORM saves you time, reduces errors, and improves application reliability.


**By leveraging NexaORM's auto-migration features, you can ensure your database remains up-to-date and consistent with your entities, streamlining your application development process.**