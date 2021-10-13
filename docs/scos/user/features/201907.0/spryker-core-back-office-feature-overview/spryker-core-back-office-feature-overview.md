---
title: Spryker Core Back Office feature overview
description: The article provides general information about the actions you can perform in Spryker Back Office.
template: concept-topic-template
originalLink: https://documentation.spryker.com/v3/docs/back-office
originalArticleId: 6b9ff84f-ad06-4f1b-9c95-6b9105d0232c
redirect_from:
  - /v3/docs/the-back-office-overview
  - /v3/docs/en/the-back-office-overview
  - /v3/docs/back-office-login-overview
  - /v3/docs/en/back-office-login-overview
  - /v3/docs/back-office
  - /v3/docs/en/back-office
  - /v3/docs/spryker-core-back-office
  - /v3/docs/en/spryker-core-back-office
  - /v3/docs/back-office-management
  - /v3/docs/en/back-office-management
  - /v3/docs/customer-management
  - /v3/docs/en/customer-management
  - /v3/docs/data-protection
  - /v3/docs/en/data-protection
---

A Spryker-based shop ships with a comprehensive, intuitive administration area comprised of numerous features that give you a strong hold over the customization of your store. Here you can tailor features to your specific needs, manage orders, products, customers, modify look & feel of your store by, for example, designing the eye-catching marketing campaigns and promotions, and much more.

The Spryker Back Office provides you with a variety of sections that are logically connected to each other.

{% info_block infoBox "Spryker Back Office" %}

It provides the product and content management capabilities, categories and navigation building blocks, search and filter customizations, barcode generator, order handling, company structure creation (_for B2B users_), merchant-buyer contracts' setup.

{% endinfo_block %}

With Spryker Back Office, you can:
* Manage orders placed by your customers as well as create orders for customers
* Create and manage customers
* Build and manage product categories
* Create and manage CMS blocks and pages
* Handle translations
* Manage products and all elements related to them (availability, labels, options, types, etc.)
* Customize search and filters for the online store
* Create and manage discounts
* Build and manage the main navigation of your online store
* Create new carrier companies and shipment methods as well as manage those
* Create admin users, add roles and user groups

Depending on the roles and teams in your project, you can limit the access of different Back Office users to specific Back Office areas.

**Back Office provides both, B2B and B2C capabilities.**

{% info_block infoBox "Info" %}

The following diagram shows what features are used for both **B2B and B2C**, and which are **B2B specific**.

{% endinfo_block %}

![B2B and B2C Features\(2\)](https://cdn.document360.io/9fafa0d5-d76f-40c5-8b02-ab9515d3e879/Images/Documentation/B2B%20and%20B2C%20Features%282%29.png)

You can always define what exactly is going to be needed for your specific project.


## Current constraints

Currently, the feature has the following functional constraint:

Each of the Identity Managers is an ECO module that should be developed separately. After the module development, the Identity Manager’s roles and permissions should be mapped to the roles and permissions in Spryker. The mapping is always implemented at the project level.


## Related Business User articles

|BACK OFFICE USER GUIDES|
|---|
| [Get a general idea of the Back Office Translations](/docs/scos/user/features/{{page.version}}/spryker-core-back-office/spryker-core-back-office-feature-overview/back-office-translations-overview.html) |
| **Work with the Back Office**: |
| [Log in to the Back Office](/docs/scos/user/back-office-user-guides/{{page.version}}/logging-in-to-the-back-office.html) |
| [View Dashboard](/docs/scos/user/back-office-user-guides/{{page.version}}/dashboard/viewing-dashboard.html) |
| [Mange Punch Out](/docs/scos/user/back-office-user-guides/{{page.version}}/punch-out/managing-punch-out-connections.html) |
| [View Order Matrix](/docs/scos/user/back-office-user-guides/{{page.version}}/sales/order-matrix/viewing-the-order-matrix.html) |
| [Manage customers](/docs/scos/user/back-office-user-guides/{{page.version}}/customer/customer-customer-access-customer-groups/managing-customers.html) |
| [Create an abstract product and product bundles](/docs/scos/user/back-office-user-guides/{{page.version}}/catalog/products/abstract-products/creating-abstract-products-and-product-bundles.html) |
| [Create content items](/docs/scos/user/back-office-user-guides/{{page.version}}/content/content-items/creating-content-items.html) |
| [Create a voucher](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/discount/creating-vouchers.html) |
| [Manage users](/docs/scos/user/back-office-user-guides/{{page.version}}/users/roles-groups-and-users/managing-users.html) |
| [Manage merchants](/docs/scos/user/back-office-user-guides/{{page.version}}/marketplace/merchants-and-merchant-relations/managing-merchants.html) |
| [Create a warehouse](/docs/scos/user/back-office-user-guides/{{page.version}}/administration/warehouses/creating-warehouses.html) |

{% info_block warningBox "Developer guides" %}

Are you a developer? See [Spryker Core back Office feature walkthrough](/docs/scos/dev/feature-walkthroughs/{{page.version}}/spryker-core-back-office-feature-walkthrough/spryker-core-back-office-feature-walkthrough.html) for developers.

{% endinfo_block %}