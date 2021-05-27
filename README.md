# BelongsTo field with dependency support for Nova

This package is an extension of Laravel Nova's existing BelongsTo field and Vue components.

Originally created by manmohanjit, the original package was abandoned. Then followed by webparking/nova-belongs-to-dependency, but I corrected some issues with large recordsets and addedd support for searchable fields.

## Installation

You can install this package on a Laravel app that uses [Nova](https://nova.laravel.com) via composer:

```bash
composer require scops/nova-belongs-to-dependency
```

## Usage

The following will list categories with `type_id` equal to the value set in the first BelongsTo field.

```php
use Scops\BelongsToDependency\BelongsToDependency;
...
return [
    ...
    BelongsTo::make('Type'),
    
    BelongsToDependency::make('User')
        ->dependsOn('type', 'type_id'),
    ...
];
```

Look at the [example](#example) below for other use cases.

## Example

Database Structure

- Type (id, name)
- Posts (id, type_id, category_id, title, body)
- Category (id, type_id, title)

We should only be able to assign categories to posts that belong to the same type.

This is how you would achieve it on the Nova category resource:

```php
use Scops\BelongsToDependency\BelongsToDependency;
...
return [
    ...
    BelongsTo::make('Type'),
    
    BelongsToDependency::make('User')
        ->dependsOn('type', 'type_id'),
    ...
];
```

This would work if you used a text/enum `type` field too.

```php
use Scops\BelongsToDependency\BelongsToDependency;
...
return [
    ...
    Select::make('Type')->options([
        'post' => 'Post',
        'page' => 'Page',
    ])>displayUsingLabels(),
    
    BelongsToDependency::make('User')
        ->dependsOn('type', 'type'),
    ...
];
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Credits

- https://github.com/webparking/nova-belongs-to-dependency
- https://github.com/manmohanjit/nova-belongs-to-dependency

- [nova-belongsto-depend](https://github.com/orlyapps/nova-belongsto-depend) (alternative)
- [nova-dependency-container](https://github.com/epartment/nova-dependency-container)

This tool extends the base Laravel Nova BelongsTo field and is inspired by Nova Dependency Container. 

## License

The MIT License (MIT). Please see License File for more information.
