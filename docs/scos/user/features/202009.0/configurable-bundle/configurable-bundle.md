---
title: Configurable Bundle
description: A configurable bundle helps shoppers to purchase complex products that have complicated configuration and require expert knowledge for purchase.
originalLink: https://documentation.spryker.com/v6/docs/configurable-bundle
originalArticleId: 931d1264-30cf-45b7-b251-9913aa958877
redirect_from:
  - /v6/docs/configurable-bundle
  - /v6/docs/en/configurable-bundle
---

For B2B customers, being able to purchase a compound product is very important. Shoppers want to select and buy complicated sets of products in one place at once. This is where the *Configurable Bundle* feature best suits the needs.

Configurable bundle allows your customers to select components of a compound product. From a provided list of options with properties like color or size, they can select what suits them best. For example, if you are a car dealer, your customer may select heated seats instead of the regular ones or an automatic start.


Configurable Bundles feature is useful when you want to:

* Allow your customers to create custom product bundles.
* Increase conversion rate by offering diverse product combinations.

## If you are:

<div class="mr-container">
    <div class="mr-list-container">
        <!-- col1 -->
        <div class="mr-col">
            <ul class="mr-list mr-list-green">
                <li class="mr-title">Developer</li>
                <li><a href="docs\scos\user\features\202009.0\configurable-bundle\configurable-bundle-feature-overview.md" class="mr-link">Get a general idea of the Configurable Bundle feature</a></li>
                <li><a href="docs\scos\user\features\202009.0\configurable-bundle\configurable-bundle-module-relations.md" class="mr-link">Familiarize yourself with the module schema for the Configurable Bundle feature</a></li>
                <li><a href="docs\scos\dev\tutorials-and-howtos\howtos\feature-howtos\howto-render-configurable-bundle-templates-in-the-storefront.md" class="mr-link">Render Configurable Bundle Templates in the Storefront</a></li>
                 <li><a href="docs\scos\dev\module-migration-guides\202009.0\migration-guide-configurablebundle.md" class="mr-link">Migrate ConfigurableBundle module from version 1.* to  version 2.*</a></li>
                  <li><a href="docs\scos\dev\module-migration-guides\202009.0\migration-guide-configurablebundlestorage.md" class="mr-link">Migrate ConfigurableBundleStorage module from version 1.* to  version 2.*</a></li>
                <li><a href="docs\scos\dev\module-migration-guides\202009.0\migration-guide-productlistgui.md" class="mr-link">Migrate ProductListGui module from version 1.* to  version 2.*</a></li>
                 <li><a href="docs\scos\dev\module-migration-guides\202009.0\migration-guide-merchantrelationshipproductlistgui.md" class="mr-link">Migrate MerchantRelationshipProductListGui module from version 1.* to  version 2.*</a></li>
                <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\configurable-bundle-feature-integration.md" class="mr-link">Integrate the Configurable Bundle feature into your project</a></li>
                <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\merchant-product-restrictions-feature-integration.md" class="mr-link">Integrate the Merchant Product Restrictions feature into your project</a></li>
                 <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\cms-product-lists-catalog-feature-integration.md" class="mr-link">Integrate the Product Lists + Catalog feature into your project</a></li>
                 <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\prices-feature-integration.md" class="mr-link">Integrate the Prices feature into your project</a></li>
                 <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\product-feature-integration.md" class="mr-link">Integrate the Product feature into your project</a></li>
                 <li><a href="docs\scos\dev\migration-and-integration\202009.0\feature-integration-guides\product-images-configurable-bundle-feature-integration.md" class="mr-link">Integrate the Product Images + Configurable Bundle into your project</a></li>
              </ul>
        </div>
        <!-- col2 -->
        <div class="mr-col">
            <ul class="mr-list mr-list-blue">
                <li class="mr-title"> Back Office User</li>
                <li><a href="docs\scos\user\features\202009.0\configurable-bundle\configurable-bundle-feature-overview.md" class="mr-link">Get a general idea of the Configurable Bundle Templates</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\creating-configurable-bundle-templates.md" class="mr-link">Create a Configurable Bundle Template</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\managing-configurable-bundle-templates.md#editing-configurable-bundle-template" class="mr-link">Edit a Configurable Bundle Template</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\managing-configurable-bundle-templates.md#creating-a-slot-for-a-configurable-bundle-template" class="mr-link">Create a Slot for a Configurable Bundle Template</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\managing-configurable-bundle-templates.md#editing-the-slot-for-a-configurable-bundle-template" class="mr-link">Edit the Slot for a Configurable Bundle Template</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\managing-configurable-bundle-templates.md#-de-activating-configurable-bundle-template" class="mr-link">(De)Activate a Configurable Bundle Template</a></li>
                  <li><a href="https://documentation.spryker.com/docs/docs\scos\user\user-guides\202009.0\back-office-user-guide\merchandising\configurable-bundle-templates\managing-configurable-bundle-templates.md#deleting-configurable-bundle-templates" class="mr-link">Delete Configurable Bundle Templates</a></li>
            </ul>
        </div>
        <!-- col3 -->
        <div class="mr-col">
            <ul class="mr-list mr-list-red">
                <li class="mr-title">Storefront User</li>
                <li><a href="docs\scos\user\user-guides\202009.0\shop-user-guide\shop-guide-configurator\shop-guide-configurator.md" class="mr-link">Familiarize yourself with the Configurator page in the Storefront</a></li>
                <li><a href="docs\scos\user\user-guides\202009.0\shop-user-guide\shop-guide-configurator\shop-guide-managing-configurable-bundles.md#accessing-the-configurator-page" class="mr-link">Access the Configurator Page</a></li>
                <li><a href="https://documentation.spryker.com/docs/docs\scos\user\user-guides\202009.0\shop-user-guide\shop-guide-configurator\shop-guide-managing-configurable-bundles.md#setting-up-the-configurable-bundle-in-the-storefront" class="mr-link">Set up the Configurable Bundle in the Storefront</a></li>
            </ul>
        </div>
    </div>
</div>