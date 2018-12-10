# Codeignter Gen CLI
Codeigniter Gen is a PHP CLI script that allows you to write controllers, models and views faster.

# Setup

To verify if you have php cli installed, type into terminal/command prompt.
```sh
php -v
```
If you receive the php version number, then you are good to go.

Go to your *config.php* file inside the *application/config* and make sure the following line looks like below:

```php
$config['uri_protocol'] = 'AUTO';
```
After that line, add:

```php
$config['uri_protocol'] = isset($_SERVER['REQUEST_URI']) ? 'PATH_INFO' : 'CLI';
```

Save the file...

Put *Gen.php* (or *gen.php* if you have a lesser than v.3 Codeigniter) inside the controllers directory. Put *config/gen.php* inside your app config folder. Also, put *gen_templates* folder inside the views folder.
From terminal or command prompt go to the application's index.php and type:

```php
php index.php gen
```

If everything went well, you should be greeted by Gen.

# Usage

## Application

To create MVC stack (controller, model, view) you can use create:app.

Usage example

```php
// Create an MVC stack
php index.php gen create:app users
```

## Controllers

### `create:controller name_of_controller`

You can use Gen to create a Controller file. The command will need at leas a parameter which represents the name of the controller.

You can put the controller inside a directory. Directories are delimited with ".". So, if you want to create the controller inside controllers/admin, you can do create:controller admin.name_of_controller.

Usage examples

```php
// Create a Welcome controller that extends MY_Controller
php index.php gen create:controller welcome e:my

// Create a User controller inside admin directory that will extend Admin_Controller
php index.php gen create:controller admin.user extend:admin
```

## Models

### `create:model name_of_model`

Creates a model having name_of_model as name. You can put the model inside a directory. Directories are delimited with ".". So, if you want to create the model inside models/admin, you can do create model admin.name_of_model.

Usage examples

```php
// Create a user_model model that extends MY_Model
php index.php gen create:model user_model e:my

// Create a User model inside admin directory that will extend MY_Model
php index.php gen create:model admin.user extend:my
```

## Views

### `create:view name_of_view`

Creates a view having name_of_view as file name. You can put the view inside a directory. Directories are delimited with ".". So, if you want to create the view inside views/admin, you can do create view admin.name_of_view.

Usage examples

```php
// Create an index_view.php
php index.php gen create:view user_view

// Create an index_view.php inside users directory
php index.php gen create:view users.index_view
```

## Migrations

CodeIgniter Gen helps you create, do, undo, and reset migrations.

### `create:migration`

To create a migration you can call create:migration. As a result, a migration will be created in the migrations directory prefixed with version as file name. You can also pass a table name as parameter. If no table name is given, you will have to put the name of the table in the migration file. Below are usage examples:

Usage examples

```php
// Create a migration
php index.php gen create:migration create_users_table

// Create a migration with a table inside it
php index.php gen create:migration create_users_table table:users

// Create a migration with a table inside it
php index.php gen create:migration create_users_table t:users

// Create a migration and name the table like the migration
// -> The table name will be 'users' in this exmaple
php index.php gen create:migration t:%inherit% create_users_table
```

### `do:migration`

do:migration executes the migrations' up() methods. If you pass the version of the migration a parameter, it will stop at that version of the migration.

Usage examples:

```php
// Execute all migrations until the last one
php index.php gen do:migration

// Execute all migrations until a certain version of migration
php index.php gen do:migration 20181210
```

### `undo:migration`

undo:migration returns you to the previous migration version. This one also can accept a migration version as parameter to return to a migration.

Usage examples:
```php
// Undo last migration
php index.php gen undo:migration

// Undo the migrations until a specified migration version
php index.php gen undo:migration 20181210
```

### `reset:migration`

reset:migration will reset the migrations until the migration mentioned in $config['migration_version'] (in the migration configuration file).

Usage example:

```php
// Reset the migrations
php index.php gen reset:migration
```

## encryption_key

`encryption_key string_to_hash-(OPTIONAL)` - creates an encryption key inside all config.php's found in config folder. If `$config['encryption_key'] = '';` doesn't exist or has a value, the encryption key won't be written.
