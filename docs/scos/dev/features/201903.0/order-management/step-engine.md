---
title: Step Engine
description: Using Step Engine, you can define Steps and additionally, you can link forms to interact with the user
originalLink: https://documentation.spryker.com/v2/docs/step-engine
originalArticleId: 17034b08-6d33-4c74-b8ed-e490f7470ffe
redirect_from:
  - /v2/docs/step-engine
  - /v2/docs/en/step-engine
---

The StepEngine module provides an easy way to define multi-step pages with forms.

Using this module you can define `Steps` and additionally you can link forms to interact with the user.

This is useful in handling the checkout process where you can define multiple steps, such as:

* select payment method;
* select shipment method;
* enter voucher code;
* view order summary.

Every form can have its own. The transfer object of a particular step is injected into the main transfer object by the StepEngine, after it is filled with the user data from its corresponding form.

 <!-- these files are not displayed in the Flare TOC
**See also:**

* Step Engine Workflow
* Defining a Step - Step Engine
* Use Case Scenario - Step Engine
* Breadcrumb Navigation - Step Engine
-->