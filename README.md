# ActionableList

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This is a package for **Laravel 5.4** that lets you easily create catalogs of items and show them as tables, especially for administration panels.

## Postcardware

This package is [MIT-licensed](LICENSE.md), but if it makes it to your production environment we'd appreciate if you send us a postcard from your hometown. Our address is:
```
GaspariLab
via Minghetti, 18
40057 Cadriano di Granarolo E. (BO)
ITALY
```

## Install

You can easily install this package via `composer`:
``` bash
composer require gasparilab/actionablelist
```

Don't forget to put this package service provider into the `providers` array, inside of your `config/app.php`:
```
'providers' => [
    // ...
    GaspariLab\ActionableList\ActionableListServiceProvider::class,
]
```

If you want to customize the tables HTML code (you probably will!), you can publish the included views with the following Artisan command:
``` bash
php artisan vendor:publish --tag=actionablelist --force
```

This will copy the views to the `resources/views/vendor/actionablelist` folder of you app, so you can customize them and keep them versioned. The `--force` parameter overwrites any existing view with the same name, it's useful if you're updating this package from an old version.

## Usage

### Complete syntax for creating a Catalog
``` php
// Instantiate a new Catalog
$catalog = new Catalog();

// Add columns
$itemlist->setColumns(['Quantity', 'Color', 'Animal']);

// Set the items (rows)
$itemlist->setItems([
    ['one', 'red', 'cat'],
    ['two', 'green', 'bird'],
    ['three', 'blue', 'dog'],
]);
```

### Quickly creating a Catalog
You can also quickly create a new Catalog using the static `make()` function. The first parameter is an array of the columns, the second parameters is an array with the items of the table nested as arrays.

Example: creating a table with three columns and two items inside.
``` php
$catalog = Catalog::make([
    'id' => 'ID',
    'title' => 'Title',
    'created_by' => 'Author',
], [
    [1, 'Lorem Ipsum', 'John Doe'],
    [2, 'Dolor Sit', 'Pippo Pluto'],
    // ...
]);
```

The Catalog also has a fluent interface which lets you to append methods, like the Laravel Query Builder.
``` php
Catalog::setColumns($columns)->setItems($items)->addItem($item); // ...and so on
```

### Printing the table inside the view

In you Blade view you can print the Catalog this way:
``` php
{{ $catalog->getHtml() }}
```

`getHtml()` returns an `HtmlString` object, which is not escaped by Laravel, so there's no need to use the `{{!! !!}}` Blade syntax. **Beware** that **you need to manually escape** every user-provided input that will be printed inside of your table. This will probably be fixed in a next version to make it automatic.

## Testing

``` bash
vendor/bin/phpunit vendor/gasparilab/actionablelist/tests
```

## Credits

A package made by *Luca Andrea Rossi* for GaspariLab S.r.l.