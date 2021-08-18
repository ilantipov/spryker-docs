---
title: Coding Best Practices
description: In this article we outline a few common PHP coding problems and the recommended solutions.
originalLink: https://documentation.spryker.com/v5/docs/coding-best-practices
originalArticleId: 51c42e8e-e71a-42a8-9c1f-b4c187969c4a
redirect_from:
  - /v5/docs/coding-best-practices
  - /v5/docs/en/coding-best-practices
---

In this article we outline a few common PHP coding problems and the recommended solutions.

## Merging Arrays

When merging arrays, one usually uses `array_merge($defaults, $options)`. However, when working with associative arrays (keys are all string identifiers), it is recommended to use the `+` operator. This is not only a lot faster, it also yields more correct results with edge cases. Beware of the switched order in this case: `$mergedOptions = $options + $defaults;`

## Operations Per Line

To facilitate readability and debugging, it is recommended to use only one operation per line.

## Method Size

Long methods tend to have too many responsibilities, and are usually harder to understand and maintain than smaller ones. Therefore it is advisable to stick to the "single responsibility" principle, when a method is just a few lines long.

 

<!-- Last review date: Nov. 22nd, 2017--  by Mark Scherer -->