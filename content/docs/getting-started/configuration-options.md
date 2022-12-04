---
title: "Configuration Options"
weight: 40
# geekdocFlatSection: false
geekdocToc: 6
geekdocHidden: false
date: 2022-12-04T10:35:15+01:00
draft: false
---

_NOTE: THIS IS SUBJECT TO CHANGE IN FUTURE VERSIONS IN FAVOR OF USING A YAML CONFIG FILE._

To overwrite default settings, you can create a `yamldocs.php` config file in the root of your application, where you have yamldocs set up as a dependency.
This file should return an array with your custom options.

This is also where you set up custom templates and custom builders.

These are the options you can overwrite:

- `debug`: (boolean) default is set to true.
- `templatesDir`: (string) default is set to the vendor yamldocs folder. You can replace this with your own directory containing custom templates.
- `builders`: (array) expects an array with `identifier` => `path` to all custom builders. The identifier is used to select this builder when running `yamldocs build`.

## Example 1: Setting up Templates Folder

```php
<?php

return [
    'templatesDir' => __DIR__ . '/templates'
];
```

## Example 2: Setting up Builders


```php
<?php

return [
    'builders' => [
        'default' => "Builders\\DefaultBuilder",
        'custom' => "MyBuilders\\MyCustomBuilder"
    ]
];
```