---
title: RatePay - How to Disable Address Updates from the Backend Application
description: Disable address updates from the backend application for Ratepay.
originalLink: https://documentation.spryker.com/v1/docs/ratepay-disable-address-updates
originalArticleId: 6dae0972-c651-4cf4-998f-779ba71387c9
redirect_from:
  - /v1/docs/ratepay-disable-address-updates
  - /v1/docs/en/ratepay-disable-address-updates
---

To disable updates on addresses from the backend application, follow the steps described below:

**Step 1**:

* Overwrite on project side
`/vendor/spryker/spryker/Bundles/Sales/src/Spryker/<br>Zed/Sales/Presentation/Detail/boxes/addresses.twig`
* Remove ' `Edit`' button

**Step 2**:

* Overwrite on project side
`/vendor/spryker/spryker/Bundles/Sales/src/Spryker/<br>Zed/Sales/Communication/Controller/EditController.php`
* Disable ' `addressAction`'