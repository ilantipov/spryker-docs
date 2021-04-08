---
title: Marketplace return management feature integration
last_updated: Apr 7, 2021
summary: This document describes the process how to integrate the Marketplace return management feature into a Spryker project.
---

This document describes how to integrate the [Marketplace return management]({https://github.com/spryker-feature/marketplace-return-management}) feature into a Spryker project.

## Install feature core

Follow the steps below to install the Marketplace return management feature core.

### 1) Install required modules using Сomposer
<!--Provide one or more console commands with the exact latest version numbers of all required modules. If the composer command contains the modules that are not related to the current feature, move them to the [prerequisites](#prerequisites).-->

Install the required modules:

```bash
composer require spryker-feature/marketplace-return-management --update-with-dependencies
composer require spryker/sales-return ^1.1.0 --update-with-dependencies 
```
<!-- Have to be deleted after Return Management feature will be released with a new version-->
---

**Verification**
<!--Describe how a developer can check they have completed the step correctly.-->

Make sure that the following modules have been installed:

| MODULE  | EXPECTED DIRECTORY <!--for public Demo Shops--> |
| -------- | ------------------- |
| MerchantSalesReturn | spryker/merchant-sales-return |

---


### Set up the configuration
<!--Describe system and module configuration changes. If the default configuration is enough for a primary behavior, skip this step.-->

Add the following configuration:

| CONFIGURATION | SPECIFICATION | NAMESPACE |
| ------------- | ------------ | ------------ |
| MainMerchantStateMachine | Adjust `MainMerchantStateMachine` to have the `MarketplaceReturn` and `MarketplaceRefund` subprocesses. | config/Zed/StateMachine/Merchant/MainMerchantStateMachine.xml |
| MerchantDefaultStateMachine | Adjust `MerchantDefaultStateMachine` to have the `MarketplaceReturn` and `MarketplaceRefund` subprocesses. | config/Zed/StateMachine/Merchant/MerchantDefaultStateMachine.xml |
| MarketplaceRefund  | Add configuration for `MarketplaceRefund` subprocess in the `MarketplaceSubprocess` for the Merchant StateMachine configuration. | config/Zed/StateMachine/Merchant/MarketplaceSubprocess/MarketplaceRefund01.xml |
| MarketplaceReturn  | Add configuration for the `MarketplaceReturn` subprocess in the `MarketplaceSubprocess` for the Merchant StateMachine configuration. | config/Zed/StateMachine/Merchant/MarketplaceSubprocess/MarketplaceReturn01.xml |
| Oms  | Adjust OMS configuration for the `MarketplacePayment` to have the `MarketplaceReturn` and `MarketplaceRefund` subprocesses. | config/Zed/oms/MarketplacePayment01.xml |
| Oms  | Add configuration for the `MarketplaceRefund` subprocess in the `MarketplaceSubprocess` for the OMS configuration. | config/Zed/oms/MarketplaceSubprocess/MarketplaceRefund01.xml |
| Oms  | Add configuration for `MarketplaceReturn` subprocess in the `MarketplaceSubprocess` for the OMS configuration. | config/Zed/oms/MarketplaceSubprocess/MarketplaceReturn01.xml |

<details>
<summary markdown='span'>config/Zed/StateMachine/Merchant/MainMerchantStateMachine.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
    xmlns="spryker:state-machine-01"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="spryker:state-machine-01 http://static.spryker.com/state-machine-01.xsd">

    <process name="MainMerchantStateMachine" main="true">
        <subprocesses>
            <process>MarketplaceReturn</process>
            <process>MarketplaceRefund</process>
        </subprocesses>
    </process>

    <process name="MarketplaceReturn" file="MarketplaceSubprocess/MarketplaceReturn01"/>
    <process name="MarketplaceRefund" file="MarketplaceSubprocess/MarketplaceRefund01"/>

</statemachine>
```

</details> 

<details>
<summary markdown='span'>config/Zed/StateMachine/Merchant/MerchantDefaultStateMachine.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
    xmlns="spryker:state-machine-01"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="spryker:state-machine-01 http://static.spryker.com/state-machine-01.xsd">

    <process name="MerchantDefaultStateMachine" main="true">
        <subprocesses>
            <process>MarketplaceReturn</process>
            <process>MarketplaceRefund</process>
        </subprocesses>
    </process>

    <process name="MarketplaceReturn" file="MarketplaceSubprocess/MarketplaceReturn01"/>
    <process name="MarketplaceRefund" file="MarketplaceSubprocess/MarketplaceRefund01"/>

</statemachine>
```

</details>

<details>
<summary markdown='span'>config/Zed/StateMachine/Merchant/MarketplaceSubprocess/MarketplaceRefund01.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
        xmlns="spryker:oms-01"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd">

  <process name="DummyRefund">
    <states>
      <state name="refunded" display="oms.state.refunded"/>
    </states>

    <transitions>
      <transition>
        <source>delivered</source>
        <target>refunded</target>
        <event>refund</event>
      </transition>

      <transition>
        <source>returned</source>
        <target>refunded</target>
        <event>refund</event>
      </transition>
    </transitions>

    <events>
      <event name="refund" manual="true" command="DummyMarketplacePayment/Refund"/>
    </events>
  </process>

</statemachine>
```

</details> 

<details>
<summary markdown='span'>config/Zed/StateMachine/Merchant/MarketplaceSubprocess/MarketplaceReturn01.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
        xmlns="spryker:oms-01"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd">

  <process name="MerchantReturn">
    <states>
      <state name="waiting for return" display="oms.state.waiting-for-return"/>
      <state name="returned" display="oms.state.returned"/>
      <state name="return canceled" display="oms.state.return-canceled"/>
      <state name="shipped to customer" display="oms.state.shipped-to-customer"/>
    </states>

    <transitions>
      <transition>
        <source>shipped</source>
        <target>waiting for return</target>
        <event>start-return</event>
      </transition>

      <transition>
        <source>delivered</source>
        <target>waiting for return</target>
        <event>start-return</event>
      </transition>

      <transition>
        <source>waiting for return</source>
        <target>returned</target>
        <event>execute-return</event>
      </transition>

      <transition>
        <source>waiting for return</source>
        <target>return canceled</target>
        <event>cancel-return</event>
      </transition>

      <transition>
        <source>return canceled</source>
        <target>shipped to customer</target>
        <event>ship-return</event>
      </transition>

      <transition>
        <source>shipped to customer</source>
        <target>delivered</target>
        <event>delivery-return</event>
      </transition>
    </transitions>

    <events>
      <event name="start-return" command="MarketplaceReturn/StartReturn"/>
      <event name="execute-return" manual="true"/>
      <event name="cancel-return" manual="true"/>
      <event name="ship-return" manual="true"/>
      <event name="delivery-return" manual="true"/>
    </events>
  </process>

</statemachine>
```

</details> 

<details>
<summary markdown='span'>config/Zed/oms/MarketplacePayment01.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
    xmlns="spryker:oms-01"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd">

    <process name="MarketplacePayment01" main="true">
        <subprocesses>
            <process>MarketplaceReturn</process>
            <process>MarketplaceRefund</process>
        </subprocesses>
    </process>

    <process name="MarketplaceReturn" file="MarketplaceSubprocess/MarketplaceReturn01"/>
    <process name="MarketplaceRefund" file="MarketplaceSubprocess/MarketplaceRefund01"/>

</statemachine>
```

</details> 

<details>
<summary markdown='span'>config/Zed/oms/MarketplaceSubprocess/MarketplaceRefund01.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
        xmlns="spryker:oms-01"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd">

    <process name="DummyRefund">
        <states>
            <state name="refunded" display="oms.state.refunded"/>
        </states>

        <transitions>
            <transition>
                <source>delivered</source>
                <target>refunded</target>
                <event>refund</event>
            </transition>

            <transition>
                <source>returned</source>
                <target>refunded</target>
                <event>refund</event>
            </transition>
        </transitions>

        <events>
            <event name="refund" manual="true" command="DummyPayment/Refund"/>
        </events>
    </process>

</statemachine>
```

</details> 

<details>
<summary markdown='span'>config/Zed/oms/MarketplaceSubprocess/MarketplaceReturn01.xml</summary>

```xml
<?xml version="1.0"?>
<statemachine
        xmlns="spryker:oms-01"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="spryker:oms-01 http://static.spryker.com/oms-01.xsd">

  <process name="MerchantReturn">
    <states>
      <state name="waiting for return" display="oms.state.waiting-for-return"/>
      <state name="returned" display="oms.state.returned"/>
      <state name="return canceled" display="oms.state.return-canceled"/>
      <state name="shipped to customer" display="oms.state.shipped-to-customer"/>
    </states>

    <transitions>
      <transition>
        <source>shipped by merchant</source>
        <target>waiting for return</target>
        <event>start-return</event>
      </transition>

      <transition>
        <source>delivered</source>
        <target>waiting for return</target>
        <event>start-return</event>
      </transition>

      <transition>
        <source>waiting for return</source>
        <target>returned</target>
        <event>execute-return</event>
      </transition>

      <transition>
        <source>waiting for return</source>
        <target>return canceled</target>
        <event>cancel-return</event>
      </transition>

      <transition>
        <source>return canceled</source>
        <target>shipped to customer</target>
        <event>ship-return</event>
      </transition>

      <transition>
        <source>shipped to customer</source>
        <target>delivered</target>
        <event>delivery-return</event>
      </transition>
    </transitions>

    <events>
      <event name="start-return" command="Return/StartReturn"/>
      <event name="execute-return" manual="true"/>
      <event name="cancel-return" manual="true"/>
      <event name="ship-return" manual="true"/>
      <event name="delivery-return" manual="true"/>
    </events>
  </process>

</statemachine>
```

</details> 

### Set up database schema and transfer objects
<!--Provide the following with a description before each item:
* Code snippets with DB schema changes.
* Code snippets with transfer schema changes.
* The console command to apply the changes in project and core. -->

Run the following commands to apply database changes and to generate entity and transfer changes:

```bash
console transfer:generate
console propel:install
console transfer:generate
```

---

**Verification**
<!--Describe how a developer can check they have completed the step correctly.-->

Make sure that the following changes have been applied by checking your database:

| DATABASE ENTITY | TYPE | EVENT |
| --------------- | ---- | ------ |
| spy_sales_return.merchant_sales_order_reference | column | created |

Make sure that the following changes have been triggered in transfer objects:

| TRANSFER | TYPE | EVENT  | PATH  |
| --------- | ------- | ----- | ------------- |
| MerchantOrderCriteria.orderItemUuid | attribute | created | src/Generated/Shared/Transfer/MerchantOrderCriteria |
| Return | class | created | src/Generated/Shared/Transfer/Return |
| Item | class | created | src/Generated/Shared/Transfer/Item |
| ReturnItem | class | created | src/Generated/Shared/Transfer/ReturnItem |
| ReturnResponse | class | created | src/Generated/Shared/Transfer/ReturnResponse |
| Message | class | created | src/Generated/Shared/Transfer/Message |
| ReturnCreateRequest | class | created | src/Generated/Shared/Transfer/ReturnCreateRequest |
| MerchantOrder | class | created | src/Generated/Shared/Transfer/MerchantOrder |
| MerchantOrderCriteria | class | created | src/Generated/Shared/Transfer/MerchantOrderCriteria |
| ReturnCreateRequest | class | created | src/Generated/Shared/Transfer/ReturnCreateRequest |

---

### Add translations
<!--Provide glossary keys for `DE` and `EN` of your feature as a code snippet. When a glossary key is dynamically generated, describe how to construct the key.-->

Add translations as follows:

1. Append glossary for the feature:

<details>
<summary markdown='span'>data/import/common/common/glossary.csv</summary>

``` 
merchant_sales_return.message.items_from_different_merchant_detected,"There are products from different merchants in your order. You can only return products from one merchant at a time.",en_US
merchant_sales_return.message.items_from_different_merchant_detected,"Diese Bestellung enthält Artikel von verschiedenen Händlern. Sie können nur Artikel von einem Händler zur selben Zeit zurückschicken.",de_DE
merchant_sales_return_widget.create_form.different_merchants_info,There are products from different merchants in your order. You can only return products from one merchant at a time.,en_US
merchant_sales_return_widget.create_form.different_merchants_info,Diese Bestellung enthält Artikel von verschiedenen Händlern. Sie können nur Artikel von einem Händler zur selben Zeit zurückschicken.,de_DE
```

</details>


1. Import data:

```bash
console data:import glossary
```

---

**Verification**
<!--Describe how a developer can check they have completed the step correctly.-->

Make sure that the configured data has been added to the `spy_glossary` table.

---

### Set up behavior
<!--This is a comment, it will not be included -->
Enable the following behaviors by adding and registering the plugins:

| Plugin  | Specification | Prerequisites | Namespace |
| ------------ | ----------- | ----- | ------------ |
| MerchantReturnPreCreatePlugin | Provides merchant order reference for the return transfer. | none |   Pyz\Zed\MerchantOms\Communication\Plugin\Oms |
| MerchantReturnCreateRequestValidatorPlugin | Checks if each item in the `itemTransfers` has the same merchant reference. | none |   Pyz\Zed\MerchantOms\Communication\Plugin\Oms |
| MarketplaceRefundCommandPlugin | Triggers 'refund' event on a marketplace order item. | none |   Pyz\Zed\MerchantOms\Communication\Plugin\Oms |
| MarketplaceStartReturnCommandPlugin | Triggers 'return' event on a marketplace order item. | none |   Pyz\Zed\MerchantOms\Communication\Plugin\Oms |

<details>
<summary markdown='span'>src/Pyz/Zed/SalesReturn/SalesReturnDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Zed\SalesReturn;

use Spryker\Zed\MerchantSalesReturn\Communication\Plugin\MerchantReturnCreateRequestValidatorPlugin;
use Spryker\Zed\MerchantSalesReturn\Communication\Plugin\MerchantReturnPreCreatePlugin;
use Spryker\Zed\SalesReturn\SalesReturnDependencyProvider as SprykerSalesReturnDependencyProvider;

class SalesReturnDependencyProvider extends SprykerSalesReturnDependencyProvider
{
    protected function getReturnPreCreatePlugins(): array
    {
        return [
            new MerchantReturnPreCreatePlugin(),
        ];
    }

    protected function getReturnCreateRequestValidatorPlugins(): array
    {
        return [
            new MerchantReturnCreateRequestValidatorPlugin(),
        ];
    }
}
```

</details> 

<details>
<summary markdown='span'>src/Pyz/Zed/MerchantOms/Communication/Plugin/Oms/MarketplaceStartRefundCommandPlugin.php</summary>

```php
<?php

namespace Pyz\Zed\MerchantOms\Communication\Plugin\Oms;

use Generated\Shared\Transfer\MerchantOrderItemCriteriaTransfer;
use Generated\Shared\Transfer\StateMachineItemTransfer;
use LogicException;
use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\StateMachine\Dependency\Plugin\CommandPluginInterface;

/**
 * @method \Pyz\Zed\MerchantOms\Communication\MerchantOmsCommunicationFactory getFactory()
 * @method \Pyz\Zed\MerchantOms\MerchantOmsConfig getConfig()
 */
class MarketplaceRefundCommandPlugin extends AbstractPlugin implements CommandPluginInterface
{
    protected const EVENT_REFUND = 'refund';

    /**
     * {@inheritDoc}
     * - Triggers 'refund' event on a marketplace order item.
     *
     * @api
     *
     * @param \Generated\Shared\Transfer\StateMachineItemTransfer $stateMachineItemTransfer
     *
     * @return void
     */
    public function run(StateMachineItemTransfer $stateMachineItemTransfer)
    {
        $merchantOrderItemTransfer = $this->getFactory()->getMerchantSalesOrderFacade()->findMerchantOrderItem(
            (new MerchantOrderItemCriteriaTransfer())
                ->setIdMerchantOrderItem($stateMachineItemTransfer->getIdentifier())
        );

        if (!$merchantOrderItemTransfer) {
            return;
        }

        $result = $this->getFactory()->getOmsFacade()->triggerEventForOneOrderItem(static::EVENT_REFUND, $merchantOrderItemTransfer->getIdOrderItem());

        if ($result === null) {
            throw new LogicException(sprintf(
                'Sales Order Item #%s transition for event "%s" has not happened.',
                $merchantOrderItemTransfer->getIdOrderItem(),
                static::EVENT_REFUND
            ));
        }
    }
}
```

</details> 

<details>
<summary markdown='span'>src/Pyz/Zed/MerchantOms/Communication/Plugin/Oms/MarketplaceStartReturnCommandPlugin.php</summary>

```php
<?php

namespace Pyz\Zed\MerchantOms\Communication\Plugin\Oms;

use Generated\Shared\Transfer\MerchantOrderItemCriteriaTransfer;
use Generated\Shared\Transfer\StateMachineItemTransfer;
use LogicException;
use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\StateMachine\Dependency\Plugin\CommandPluginInterface;

/**
 * @method \Pyz\Zed\MerchantOms\Communication\MerchantOmsCommunicationFactory getFactory()
 * @method \Pyz\Zed\MerchantOms\MerchantOmsConfig getConfig()
 */
class MarketplaceStartReturnCommandPlugin extends AbstractPlugin implements CommandPluginInterface
{
    protected const EVENT_START_RETURN = 'start-return';

    /**
     * {@inheritDoc}
     * - Triggers 'return' event on a marketplace order item.
     *
     * @api
     *
     * @param \Generated\Shared\Transfer\StateMachineItemTransfer $stateMachineItemTransfer
     *
     * @return void
     */
    public function run(StateMachineItemTransfer $stateMachineItemTransfer)
    {
        $merchantOrderItemTransfer = $this->getFactory()->getMerchantSalesOrderFacade()->findMerchantOrderItem(
            (new MerchantOrderItemCriteriaTransfer())
                ->setIdMerchantOrderItem($stateMachineItemTransfer->getIdentifier())
        );

        if (!$merchantOrderItemTransfer) {
            return;
        }

        $result = $this->getFactory()->getOmsFacade()->triggerEventForOneOrderItem(static::EVENT_START_RETURN, $merchantOrderItemTransfer->getIdOrderItem());

        if ($result === null) {
            throw new LogicException(sprintf(
                'Sales Order Item #%s transition for event "%s" has not happened.',
                $merchantOrderItemTransfer->getIdOrderItem(),
                static::EVENT_START_RETURN
            ));
        }
    }
}
```

</details> 

<details>
<summary markdown='span'>src/Pyz/Zed/MerchantOms/MerchantOmsDependencyProvider.php</summary>

```php
<?php

namespace Pyz\Zed\MerchantOms;

use Pyz\Zed\MerchantOms\Communication\Plugin\Oms\MarketplaceRefundCommandPlugin;
use Pyz\Zed\MerchantOms\Communication\Plugin\Oms\MarketplaceStartReturnCommandPlugin;

class MerchantOmsDependencyProvider extends SprykerMerchantOmsDependencyProvider
{
    protected function getStateMachineCommandPlugins(): array
    {
        return [
            'DummyMarketplacePayment/Refund' => new MarketplaceRefundCommandPlugin(),
            'MarketplaceReturn/StartReturn' => new MarketplaceStartReturnCommandPlugin(),
        ];
    }
}
```

</details> 


Add config for the `SalesReturn`:

<details>
<summary markdown='span'>src/Pyz/Zed/SalesReturn/SalesReturnConfig.php</summary>

```php
<?php

namespace Pyz\Zed\SalesReturn;

use Spryker\Zed\SalesReturn\SalesReturnConfig as SprykerSalesReturnConfig;

class SalesReturnConfig extends SprykerSalesReturnConfig
{
    protected const RETURNABLE_STATE_NAMES = [
        'shipped',
        'delivered',
        'shipped by merchant',
    ];
}
```

</details> 


## Install feature front end

Follow the steps below to install the Marketplace return management feature front end.

### Prerequisites
<!--Describe the features the project must have before the current feature can be integrated.-->

To start feature integration, integrate the required features:
<!--See feature mapping at [Features](https://release.spryker.com/features).-->

| NAME | VERSION |
| --------- | ------ |
| {Feature Name} | {feature version} |

### 1) Install required modules using Сomposer
<!--Provide the console command\(s\) with the exact latest version numbers of all required modules. If the composer command contains the modules that are not related to the current feature, move them to the [prerequisites](#prerequisites).-->

Install the required modules:

```bash
composer require spryker-shop/merchant-sales-return-widget ^0.1.0 --update-with-dependencies
```

---

**Verification**
<!--Describe how a developer can check they have completed the step correctly.-->

Make sure that the following modules have been installed:

| MODULE  | EXPECTED DIRECTORY <!--for public Demo Shops--> |
| -------- | ------------------- |
| MerchantSalesReturnWidget | spryker-shop/merchant-sales-return-widget |

---

### Set up widgets
<!--Provide a list of plugins and global widgets to enable widgets. Add descriptions for complex javascript code snippets. Provide a console command for generating front-end code.-->

Set up widgets as follows:

1. Register the following plugins to enable widgets:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE   |
| --------------- | -------------- | ------ | -------------- |
| MerchantSalesReturnCreateFormWidgetCacheKeyGeneratorStrategyPlugin  | Disables widget cache for for the `MerchantSalesReturnCreateFormWidget` | none |  SprykerShop\Yves\MerchantSalesReturnWidget\Plugin |
| MerchantSalesReturnCreateFormWidget |  Provides "Create Return" only with the items of one merchant order at a time and only for the returnable items. | none |  SprykerShop\Yves\MerchantSalesReturnWidget\Widget |


```php
<?php

namespace Pyz\Yves\ShopApplication;

use SprykerShop\Yves\MerchantSalesReturnWidget\Plugin\MerchantSalesReturnCreateFormWidgetCacheKeyGeneratorStrategyPlugin;
use SprykerShop\Yves\MerchantSalesReturnWidget\Widget\MerchantSalesReturnCreateFormWidget;

class ShopApplicationDependencyProvider extends SprykerShopApplicationDependencyProvider
{
    /**
     * @return string[]
     */
    protected function getGlobalWidgets(): array
    {
        return [
              MerchantSalesReturnCreateFormWidget::class,
        ];
    }
    
    /**
     * @return \SprykerShop\Yves\ShopApplicationExtension\Dependency\Plugin\WidgetCacheKeyGeneratorStrategyPluginInterface[]
     */
    protected function getWidgetCacheKeyGeneratorStrategyPlugins(): array
    {
        return [
            new MerchantSalesReturnCreateFormWidgetCacheKeyGeneratorStrategyPlugin(),
        ];
    }
}
```

---

**Verification**
<!--Describe how a developer can check they have completed the step correctly.-->

Make sure that the following widgets have been registered by adding the respective code snippets to a Twig template:

| WIDGET | VERIFICATION |
| ---------------- | ----------------- |
| MerchantSalesReturnCreateFormWidget | Go through the  Return flow in the same way as now by clicking the "Create Return" button on the top of the Order Details page. Go on the "Create Return Page", and create a return only with the items of one merchant order at a time and only for returnable items.  |

---

1. Enable Javascript and CSS changes:

```bash
console frontend:yves:build
```