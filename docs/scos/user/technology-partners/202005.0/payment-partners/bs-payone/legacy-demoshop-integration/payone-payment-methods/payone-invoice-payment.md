---
title: PayOne - Invoice Payment
description: Integrate invoice payment through Payone into the Spryker-based shop.
originalLink: https://documentation.spryker.com/v5/docs/payone-invoice
originalArticleId: f8bcbd3e-f499-4716-a762-231f1b2b0cc9
redirect_from:
  - /v5/docs/payone-invoice
  - /v5/docs/en/payone-invoice
---

## Front-end Integration

To adjust the frontend appearance, provide the following templates in your theme directory:
`src/<project_name>/Yves/Payone/Theme/<custom_theme_name>/invoice.twig`

## State Machine Integration

Payone module provides a demo state machine for the Invoice payment method which implements Authorization flow.

To enable the demo state machine, extend the configuration with following values:

```php
<?php
$config[SalesConstants::PAYMENT_METHOD_STATEMACHINE_MAPPING] = [
 ...
 PayoneConfig::PAYMENT_METHOD_INVOICE => 'PayoneInvoice',
];

$config[OmsConstants::ACTIVE_PROCESSES] = [
 ...
 'PayoneInvoice',
];
```
