---
title: Configuring Visibility of the Included Section
originalLink: https://documentation.spryker.com/v2/docs/ht-configuring-visibility-included-section-201903
originalArticleId: 989b742b-92d8-42b1-b506-6e77a85c9714
redirect_from:
  - /v2/docs/ht-configuring-visibility-included-section-201903
  - /v2/docs/en/ht-configuring-visibility-included-section-201903
---

Responses of Spryker Glue REST API can return the **included** and **relationships** sections. The sections contain additional information on the resource requested. Such information is presented in the form of related resources. For example, if you request information on products, the sections can include such additional related resources as image sets, prices, availability information etc.

{% info_block infoBox %}
For more details, see [Compound Documents](https://jsonapi.org/format/#document-compound-documents
{% endinfo_block %}.)

You can decide whether Glue REST API includes the sections in all responses by default:

* If you **enable** the option, API endpoints return all related resources by default. With the help of the _include_ query string you can filter out the unnecessary included resources and request only the information you need.
* If you **disable** the option, responses of API endpoints do not contain the _included_ and _relationships_ sections unless you specify the related resources you need via the include query string. When the string is specified, only the resources passed by it are returned.

| |Request with 'include' query string  | Request without 'include' query string |
| --- | --- | --- |
| | Example: /concrete-products/177_24867659?**include=concrete-product-image-sets** |Example: /concrete-products/177_24867659  |
|**Enabled** | The **included** and **relationships** sections contain only the resources whose names were passed in the query string (resource _concrete-product-image-sets_ per the example). | The included section contains all the included resources (if any). |
|**Disabled** | The response does not contain the included section with related resources. |  The included section contains all the included resources (if any).|

By default, the option is enabled on the Spryker Core level, but disabled on the project level in all [Spryker Demo Shops](/docs/scos/user/intro-to-spryker/{{site.version}}/master-suite.html) (B2B Demo Shop, B2C Demo Shop and Master Shop Suite).
        
{% info_block infoBox %}
For the purposes of boosting the API performance and bandwidth usage optimization, it is recommended to request only the information you need.
{% endinfo_block %}

To configure the behavior of the **included** and **relationships** sections:

## Prerequisites
To make the option possible, you need to have at least version **1.12.0** of `GlueApplication` module installed in your project. For details on how to upgrade, see the Integration Guide.

## Configuration
To configure the behavior of the sections:
        
1. Open or create the `Pyz\Glue\GlueApplication\GlueApplicationConfig.php` file on your project level.
2. Set the value of the `getIsEagerRelatedResourcesInclusionEnabled` parameter according to the desired behavior:
    * **true** - to enable related resources everywhere;
    * **false** - to return related resources per request only.

<details open>
<summary>Sample Implementation:</summary>
    
```php
<?php

namespace Pyz\Glue\GlueApplication;

use Spryker\Glue\CartsRestApi\CartsRestApiConfig;
use Spryker\Glue\GlueApplication\GlueApplicationConfig as SprykerGlueApplicationConfig;

class GlueApplicationConfig extends SprykerGlueApplicationConfig
{
    ...
    
    /**
     * @return bool
     */
    public function isEagerRelationshipsLoadingEnabled(): bool
    {
        return false;
    }
}
```

</br>
</details>
</br>
3. Save the file.

## Verification
 To verify that the configuration has been completed successfully:

1. Send a GET request as follows:
_http://mysprykershop.com/concrete-products/177_24867659?**include=concrete-product-image-sets**_

2. Make sure that the **included** and **relationships** sections of the response contain the `concrete-product-image-sets` resource only.
   
<details open>
<summary>Sample response:</summary>

```
{
  data: {
    type: concrete-products,
    id: 177_24867659,
    attributes: {...},
    links: {...},
    relationships: {
      concrete-product-image-sets: {
        data: [
          {
            type: concrete-product-image-sets,
            id: 177_24867659
          }
        ]
      }
    }
  },
  included: [
    {
      type: concrete-product-image-sets,
      id: 177_24867659,
      attributes: {
        imageSets: [
          {
            name: default,
            images: [
              {
                externalUrlLarge: //images.icecat.biz/img/norm/high/24867659-4916.jpg,
                externalUrlSmall: //images.icecat.biz/img/norm/medium/24867659-4916.jpg
              }
            ]
          }
        ]
      },
      links: {
        self: http://mysprykershop.com/concrete-products/177_24867659/concrete-product-image-sets
      }
    }
  ]
}
```

</br>
</details>
</br>

3. Send a GET request as follows:
_http://mysprykershop.com/concrete-products/177_24867659_
4. Make sure that the endpoint responds in accordance with your configuration:
    * if the `getIsEagerRelatedResourcesInclusionEnabled` parameter is set to `true`, the included section of the response contains all related resources.

<details open>
<summary>Sample response:</summary>

```
{
  data: {
    type: concrete-products,
    id: 177_24867659,
    attributes: {...},
    links: {...},
    relationships: {
      concrete-product-image-sets: {
        data: [
          {
            type: concrete-product-image-sets,
            id: 177_24867659
          }
        ]
      },
      concrete-product-availabilities: {
        data: [
          {
            type: concrete-product-availabilities,
            id: 177_24867659
          }
        ]
      },
      concrete-product-prices: {
        data: [
          {
            type: concrete-product-prices,
            id: 177_24867659
          }
        ]
      }
    }
  },
  included: [
    {
      type: concrete-product-image-sets,
      id: 177_24867659,
      attributes: {
        imageSets: [
          {
            name: default,
            images: [
              {
                externalUrlLarge: //images.icecat.biz/img/norm/high/24867659-4916.jpg,
                externalUrlSmall: //images.icecat.biz/img/norm/medium/24867659-4916.jpg
              }
            ]
          }
        ]
      },
      links: {
        self: http://mysprykershop.com/concrete-products/177_24867659/concrete-product-image-sets
      }
    },
    {
      type: concrete-product-availabilities,
      id: 177_24867659,
      attributes: {
        availability: true,
        quantity: 20,
        isNeverOutOfStock: false
      },
      links: {
        self: http://mysprykershop.com/concrete-products/177_24867659/concrete-product-availabilities
      }
    },
    {
      type: concrete-product-prices,
      id: 177_24867659,
      attributes: {
        price: 42502,
        prices: [
          {
            priceTypeName: DEFAULT,
            netAmount: null,
            grossAmount: 42502,
            currency: {
              code: EUR,
              name: Euro,
              symbol: €
            }
          }
        ]
      },
      links: {
        self: http://mysprykershop.com/concrete-products/177_24867659/concrete-product-prices
      }
    }
  ]
}
```

</br>
</details>
</br>

    * if the `getIsEagerRelatedResourcesInclusionEnabled` parameter is set to `false`, the included and relationships sections are absent.

<details open>
<summary>Sample response:</summary>

```
{
  data: {
    type: concrete-products,
    id: 177_24867659,
    attributes: {...},
    links: {...},
}
```

_Last review date: Mar 14, 2019_

<!--by Volodymyr Volkov-->