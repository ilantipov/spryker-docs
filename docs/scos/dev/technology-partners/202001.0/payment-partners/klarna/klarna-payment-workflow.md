---
title: Klarna - Payment Workflow
description: In this article, you will find part payment request flow with Klarna.
originalLink: https://documentation.spryker.com/v4/docs/klarna-payment-workflow
originalArticleId: c6db9ec4-75d0-469f-8e64-cda0ece7ded5
redirect_from:
  - /v4/docs/klarna-payment-workflow
  - /v4/docs/en/klarna-payment-workflow
---

Both `Part Payment` and `Invoice` payment methods have the same request flow. It basically consists of the following steps:

* Pre-check: reserves the amount of the purchase
* Check order status: checks if the order status is `pending accepted`. If it's not, OMS waits for 2 hours and then calls again `KlarnaApi` to retrieve the status of the order. In case the status is `denied` the order is canceled.
* Capture payment: activates the reservation that corresponds to the given reference number
* Update payment: if activation fails, we need to update the reservation that corresponds to the given reference number
* Refund: performs a partial refund.
* Cancel: cancels a reservation.