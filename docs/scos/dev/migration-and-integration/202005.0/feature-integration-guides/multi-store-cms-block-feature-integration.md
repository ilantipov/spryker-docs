---
title: Multi-store CMS Block Feature Integration
description: This integration guide provides step-by-step instruction on integrating Multi-store CMS Block Feature into your project.
originalLink: https://documentation.spryker.com/v5/docs/multi-store-cms-block-feature-integration
originalArticleId: cdb8976d-0876-4c0a-8a58-fc74f913ad68
redirect_from:
  - /v5/docs/multi-store-cms-block-feature-integration
  - /v5/docs/en/multi-store-cms-block-feature-integration
---

To prepare your project to work with multi-store CMS Blocks, the following minimum module versions are required:

| Module| Version |
| --- | --- |
| `spryker/cms-block` | 2.0.0 |
| `spryker/cms-block-collector` | 2.0.0 |
| `spryker/cms-block-gui` | 2.0.0 |
| `spryker/store` | 1.2.0 |
| `spryker/kernel` | 3.13.0 |
| `spryker/collector` | 6.0.0 |
| `spryker/touch` | 4.0.0 |

To enable multi-store management within the CMS Block Zed Admin UI, override `Spryker\Zed\Store\StoreConfig::isMultiStorePerZedEnabled()` in your project to return `true`. 
This will enable the store management inside the CMS Block Zed Admin UI.

**Example override**

```php
<?php
namespace Pyz\Zed\Store;

use Spryker\Zed\Store\StoreConfig as SprykerStoreConfig;

class StoreConfig extends SprykerStoreConfig
{
    /**
     * @return bool
     */
    public function isMultiStorePerZedEnabled()
    {
        return true;
    }
}
```

You should now be able to use the CMS Block in the administration interface to manage CMS Block-store relations.
Check out our [Demoshop implementation](https://github.com/spryker/demoshop){target="_blank"} for implementation example and idea.