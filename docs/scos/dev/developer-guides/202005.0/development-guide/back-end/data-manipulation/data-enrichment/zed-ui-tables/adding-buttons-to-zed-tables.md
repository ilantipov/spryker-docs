---
title: Adding Buttons to Zed Tables
description: The article describes how to add buttons to Zed tables.
originalLink: https://documentation.spryker.com/v5/docs/t-add-button-table
originalArticleId: 5df9bba5-3d89-4d77-b40e-df4da19d42b7
redirect_from:
  - /v5/docs/t-add-button-table
  - /v5/docs/en/t-add-button-table
---

<!-- used to be: http://spryker.github.io/tutorials/yves/adding-buttons-to-tables/ -->

Depending on the button type that needs to be added (`Update/Create/Remove/View`), the following operations can be called:

```php
<?php
$this->generateCreateButton('destination_URL', 'Button title', array $buttonOptions);
$this->generateEditButton('destination_URL', 'Button title', array $buttonOptions);
$this->generateViewButton('destination_URL', 'Button title', array $buttonOptions);
$this->generateRemoveButton('destination_URL', 'Button title', array $buttonOptions);
```
Each generated button will have the corresponding style(color,icon) according to its type.

Usage example:

```php
<?php
$this->generateCreateButton('/category/create', 'Add new Category');
$this->generateEditButton('/category/edit/?id-category=1', 'Edit Category');
$this->generateViewButton('/category/view/?id-category=1', 'View Category');
$this->generateRemoveButton('#', 'Remove Category', [
    'id' => 'category-' . $this->getIdCategory(),
    'class' => 'remove-item',
]);
```

The third parameter (`$buttonOptions`) is an array through which extra properties can be appended to the HTML code that is generated.

Example:

```php
<?php
$buttonOptions = [
    'class' => 'my-custom-class', // will append this class to default class list
    'id' => 'my-custom-id-for-this-button', // will add id property to generated HTML link
    'icon' => 'button-icon'
];
```