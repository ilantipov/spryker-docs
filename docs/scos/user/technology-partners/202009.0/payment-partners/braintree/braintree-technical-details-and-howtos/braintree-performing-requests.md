---
title: Braintree - Performing Requests
description: This article contains information on the state machine commands and conditions for the Braintree module in the Spryker Commerce OS.
last_updated: Nov 4, 2020
template: concept-topic-template
originalLink: https://documentation.spryker.com/v6/docs/braintree-performing-requests
originalArticleId: c0bd64d9-a36c-4775-9ac8-d870ab044397
redirect_from:
  - /v6/docs/braintree-performing-requests
  - /v6/docs/en/braintree-performing-requests
related:
  - title: Braintree - Installation and configuration
    link: docs/scos/user/technology-partners/page.version/payment-partners/braintree/braintree-installation-and-configuration.html
  - title: Braintree - Integration into a project
    link: docs/scos/user/technology-partners/page.version/payment-partners/braintree/braintree-integration-into-a-project.html
  - title: Braintree - Workflow
    link: docs/scos/user/technology-partners/page.version/payment-partners/braintree/braintree-technical-details-and-howtos/braintree-workflow.html
---

In order to perform the necessary requests in the project based on Spryker Commerce OS or SCOS, you can easily use the implemented state machine commands and conditions. The next section gives a summary of them. You can also use the facade methods directly which, however, are invoked by the state machine.

## Braintree State Machine Commands and Conditions

### Commands

<b>Authorize</b>

* Authorize the payment by validating the given payment data
* Response:
  - Success: Payment Details accepted
  - Declined: Request format error, payment details not accepted
* Plugin: `AuthorizePlugin`

<b>Revert</b>

* Revert a previous pre-authorization call
* Always reverts the complete pre-check or authorization
* Plugin: `RevertPlugin`

<b>Capture</b>

* Capture of previous (p)re-authorization call Response:
  - Success: Previous (p)re-authorization still valid and accepted
  - Declined: Previous (p)re- authorization expired, request format error, or internal error
* Plugin: `CapturePlugin`

<b>Refund</b>

* Refund previous captured amount
* Full and partial refunds possible
* Response:
  - Success: Refund possible and accepted
  - Declined: Previous capture to far in the past, request format error, or internal
* Plugin: `RefundPlugin`

### Conditions

|Name  |Description  |Plugin  |
| --- | --- | --- |
|  `IsAuthorizationApproved` | Checks transaction status log for successful authorization response |  `IsAuthorizationApprovedPlugin` |
|  `IsReversalApproved` | Checks transaction status log for successful reversal response |  `IsReversalApprovedPlugin` |
|  `IsCaptureApproved` | Checks transaction status log for successful capture response |  `IsCaptureApprovedPlungin` |
|  `IsRefundApproved` | Checks transaction status log for successful refund response |  `IsRefundApprovedPlugin` |

## Braintree Facade

|Facade Method  | Parameter | Return | Description |
| --- | --- | --- | --- |
|  `saveOrderPayment` | `QuoteTransfer``CheckoutResponseTransfer` | void | Saves order payment method data according to quote and checkout response transfer data. |
|  `preCheckPayment` |  `QuoteTransfer` |  `BraintreeTransactionResponseTransfer` | Sends pre-authorize payment request to Braintree gateway to retrieve transaction data. Checks that form data matches transaction response data. |
|  `authorizePayment` |  `TransactionMetaTransfer` |  `BraintreeTransactionResponseTransfer` | Processes payment confirmation request to Braintree gateway. |
|  `capturePayment` |  `TransactionMetaTransfer` |  `BraintreeTransactionResponseTransfer` | Processes capture payment request to Braintree gateway. |
|  `revertPayment` |  `TransactionMetaTransfer` |  `BraintreeTransactionResponseTransfer` | Processes cancel payment request to Braintree gateway. |
|  `refundPayment` | `SpySalesOrderItem[]``SpySalesOrder` |  `BraintreeTransactionResponseTransfer` | Calculate `RefundTransfer` for given `$salesOrderItems` and `$salesOrderEntity`.Processes refund request to Braintree gateway by calculated `RefundTransfer`. |
|  `isAuthorizationApproved` |  `OrderTransfer` | bool | Checks if pre-authorization API request got success response from Braintree gateway. |
|  `isReversalApproved` |  `OrderTransfer` | bool | Checks if cancel API request got success response from Braintree gateway. |
|  `isCaptureApproved` |  `OrderTransfer` | bool | Checks if capture API request got success response from Braintree gateway. |
|  `isRefundApproved` |  `OrderTransfer` | bool | Checks if refund API request got success response from Braintree gateway. |
|  `postSaveHook` | `OrderTransfer``CheckoutResponseTransfer` |  `CheckoutResponseTransfer` | Execute post-save hook. |
