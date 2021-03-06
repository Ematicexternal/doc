---
layout: default
title:  "Data and Events Tracking"
categories: Quick-Start
order: 2
---

# Data & Events Tracking

## Preparing your product data
---
In order to use Retry-iQ, data and events tracking must be implemented.

Prepare the following product array:

```js
// prepare the products array and issue the API call
  var products = [{
      id: "<id>", //required
      categoryId: <category id>,
      transactionId: <transaction id>,
      price: "<unit price with currency>", //required
      priceNumber: <price number in number format>, //required
      priceCurrency: "<price currency in three letter ISO format>", //required
      quantity: <quantity>, //required
      name: "<name>", //required
      brandName: "<brandname>", //required
      desc: "<description>",
      imageUrl: "<image url>", //required
      link: "<web link>" //required
  },
  ...
  {
      id: "<id>", //required
      categoryId: <category id>,
      transactionId: <transaction id>,
      price: "<unit price with currency>", //required
      priceNumber: <price number in number format>, //required
      priceCurrency: "<price currency in three letter ISO format>", //required
      quantity: <quantity>, //required
      name: "<name>", //required
      brandName: "<brandname>", //required
      desc: "<description>",
      imageUrl: "<image url>", //required
      link: "<web link>" //required
  }];
```

The _products array_ is a snapshot of all the items in the cart, all the items to be checked-out or all items that are being converted.

## Ematic Events Tracking
---
There are 4 events (browse, cart, checkout, conversion) that need to be implemented on your website. Please note that all these methods need to come after the Ematic tracker object is created.

### Browse
Include the following code to track items that are being browsed.
Keep in mind that "products" is an **array**, even if you are logging a single product browse.

```js
//track items browsed
ematics("log", "product", "browse", products);
```
### Cart
Include the following code to __track items that are being added, updated and removed__ from the cart (which will also enable pre-abandonded cart overlays on appropriate triggers).

```js
//track items in cart to enable pre-abandonded cart overlays
ematics("log", "product", "cart", products);
```
### Checkout
Include the following code to __track items that are being checked out__.

```js
//track checkout
ematics("log", "product", "checkout", products);
```
### Conversion
Include the following code to __track items that are being converted__.

```js
//track conversion
ematics("log", "product", "convert", products);
```


## Example Scenarios
---
Below is an example sequence of cart activities and the logs that resulted from them.

#### 1. Add item A to cart
```js
products = [A];
ematics("log", "product", "cart", products);
```
#### 2. Add item B to cart
```js
products = [A, B];
ematics("log", "product", "cart", products);
```
#### 3. Add item C to cart
```js
products = [A, B, C];
ematics("log", "product", "cart", products);
```
#### 4. Remove item B from cart
```js
products = [A, C];
ematics("log", "product", "cart", products);
```
#### 5. Add item D to cart
```js
products = [A, C, D];
ematics("log", "product", "cart", products);
```
#### 6. Begin checkout process
```js
products = [A, C, D];
ematics("log", "product", "checkout", products);
```
#### 7. Finish payment
```js
products = [A, C, D];
ematics("log", "product", "convert", products);
```