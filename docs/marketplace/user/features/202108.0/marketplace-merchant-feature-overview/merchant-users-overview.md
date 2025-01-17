---
title: Merchant users overview
description: This document contains concept information for the Merchant users feature in the Spryker Commerce OS.
template: concept-topic-template
---

The merchant concept presupposes having employees with access to the Merchant Portal that will perform various actions on behalf of the merchants. To allow that, the *merchant user* entity is introduced.
From the technical point of view, Merchant Portal is a subset of modules in Zed functioning separately from the Back Office application. As in the Back Office, there are users performing different types of actions (they are further on called *Back Office users*), Merchant Portal has *merchant users* that function similarly within the Merchant account.

{% info_block infoBox "Example" %}

For example, there can be a person responsible only for creating and managing the product offers, the other person takes care of shipping the merchant orders to their buyers. This means that two merchant users need to be created for these purposes.

{% endinfo_block %}


To add merchant users for the merchant, the merchant must be created first. When the merchant record exists, the Marketplace administrator can set up one or several merchant users to manage the merchant account.

The Merchant Users concept follows certain rules:

* Every merchant user has a unique email address in the system.
* A merchant user belongs to one merchant and the same merchant user can't be assigned to two or more merchants.

## Merchant user statuses

The table below explains all the statuses that may apply to a merchant user.


| STATUS | DESCRIPTION |
| --- | --- |
| Active | When the merchant user has the `Active` status, it means that the merchant is approved, the merchant user account is activated, the email with reset password instructions has been sent, and the merchant user has access to the Merchant Portal. |
| Deactivated | Access to the Merchant Portal is revoked for the deactivated merchant user. Merchant user can be deactivated when:<ul><li>Merchant or Marketplace administrator deactivated the Merchant User.</li><li>Merchant is [denied](/docs/marketplace/user/features/{{page.version}}/marketplace-merchant-feature-overview/marketplace-merchant-feature-overview.html#merchant-statuses).</li></ul> |
| Deleted | Access to the Merchant Portal is revoked for the deleted merchant user. In the current implementation, both statuses `Deactivated` and `Deleted` have the same functionality—they restrict access to the Merchant Portal. However, this can be changed and adapted on the project level. |

<!--See LINK TO BO GUIDE HOW TO ACTIVATE A MERCHANT USER for details on to change the merchant user statues in the Back Office-->

## Merchant user access
Both merchant and typical Back Office users have a common entry point but the login URLs to the Back Office and Merchant Portal are different. The exemplary login link to the Merchant Portal is `https://os.de.marketplace.demo-spryker.com/security-merchant-portal-gui/login`.

To be able to log in to the Merchant Portal, both merchant and merchant user need to be activated in the Back Office.

{% info_block infoBox "Info" %}

If a merchant got [denied](/docs/marketplace/user/features/{{page.version}}/marketplace-merchant-feature-overview/marketplace-merchant-feature-overview.html#merchant-statuses), all their merchant users get deactivated automatically. If the merchant is re-approved again, their merchant users need to be re-activated one-by-one manually.

{% endinfo_block %}

Upon entering the Merchant Portal, a separate area with different navigation menu is displayed to the merchant user.
Merchant users have access only to the information related to their organization through the Merchant Portal application (profile, products, offers, orders, etc.), i.e., merchant users have their own area and do not access the Back Office.

## Merchant user workflow

1. The Marketplace administrator creates a merchant and approves it.
2. When the Merchant is approved, the corresponding merchant user(s) can be created in **Back Office > Merchant > Users**.
3. After the merchant user is created, they need to be activated <!--LINK TO BO GUIDE HOW TO ACTIVATE A MERCHANT USER--> to be able to log in to the Merchant Portal.
4. The “Reset Password” email is sent to the activated merchant user.
5. After the password is reset, the merchant user is able to log in to the Merchant Portal.
