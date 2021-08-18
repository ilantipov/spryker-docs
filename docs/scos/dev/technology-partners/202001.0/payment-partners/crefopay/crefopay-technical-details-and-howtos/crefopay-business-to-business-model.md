---
title: CrefoPay - Business to Business Model
description: CrefoPay module provides B2B strategy in payments.
originalLink: https://documentation.spryker.com/v4/docs/crefopay-business-to-business-model
originalArticleId: 82a4e156-a3be-46cc-ad2d-f6f6f6b48c7c
redirect_from:
  - /v4/docs/crefopay-business-to-business-model
  - /v4/docs/en/crefopay-business-to-business-model
---

CrefoPay module enables B2B strategy in payments.

To enable the B2B business model for CrefoPay:

1. Set `$config[CrefoPayConstants::IS_BUSINESS_TO_BUSINESS]` to true.
2. Add company data into `QuoteTransfer` on project level. It should be done before customer goes to checkout payment step.

**Company Data**

```php
$quoteTransfer->setCrefoPayCompany(
    (new CrefoPayApiCompanyTransfer())
        ->setCompanyName('Company Name')
        ->setCompanyRegisterType('UNKNOWN')
        ->setCompanyRegistrationID('registration-id')
        ->setCompanyTaxID('tax-id')
        ->setCompanyVatID('vat-id')
        ->setEmail('business.email@company.com')
);
```