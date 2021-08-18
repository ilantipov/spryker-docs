---
title: Tax Schema
originalLink: https://documentation.spryker.com/v3/docs/db-schema-tax
originalArticleId: 2c00bb3f-7a61-46cb-81b8-2f8358bd40e1
redirect_from:
  - /v3/docs/db-schema-tax
  - /v3/docs/en/db-schema-tax
---

## Tax

### Tax Set and Rate

{% info_block infoBox %}
Each product can be related to a tax set which contains the tax rates for each destination country.
{% endinfo_block %}
![Tax set rate](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Database+Schema+Guide/Tax+Schema/tax-set-rate.png){height="" width=""}

**Structure**:

* A Tax Set has a name (e.g. "Food") It represents a group of products which have the same tax rates
* The Rate (e.g. 19%) is stored in `spy_tax_rate`. There is one Rate per Country which allows tax conversions for cross-border shipments.