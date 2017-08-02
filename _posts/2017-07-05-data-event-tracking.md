---
layout: default
title:  "Data & Events Tracking"
categories: Quick-Start
order: 2
---

# Data & Events Tracking

## Preparing your product data
---
In order to use Retry-iQ, this data & events tracking must be implemented.

Firstly, prepare the _products array_, a snapshot of all the items in the cart, all the items to be checked-out or all items that are being converted.

```js
// prepare the products array and issue the API call
  var products = [{
      id: "<id>", //required
      categoryId: <category id>,
      transactionId: <transaction id>,
      price: "<unit price with currency>", //required
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
      quantity: <quantity>, //required
      name: "<name>", //required
      brandName: "<brandname>", //required
      desc: "<description>",
      imageUrl: "<image url>", //required
      link: "<web link>" //required
  }];
```

## Ematic Events Tracking
---
Basically there are 4 events (browse, cart, checkout, conversion) that need to be implemented on your website. Please note that all these methods need to come after ematic tracker object is created.

### Browse
Include the following snippet of code to track items that are being browsed.
Keep in mind that "products" is an **array**, even if you are logging a single product browse.

```js
//track items browsed
ematics("log", "product", "browse", products);
```
### Cart
Include the following snippet of code to __track items that are being added, updated and removed__ from the cart (which will also enable pre-abandonded cart overlays on appropriate triggers).

```js
//track items in cart to enable pre-abandonded cart overlays
ematics("log", "product", "cart", products);
```
### Checkout
Include the following snippet of code to __track items that are being checked out__.

```js
//track checkout
ematics("log", "product", "checkout", products);
```
### Conversion
Include the following snippet of code to __track items that are being converted__.

```js
//track conversion
ematics("log", "product", "convert", products);
```

## onAfterSubscribe Event
---
Optionally, you can have __your custom code triggered when a visitor subscribes using Bye-IQ__, by defining an event as follows as part of the "opt" object that gets passed in when you initialize the library.

```js
<script>
    ...
    
    //define the event before initializing
    opt.events = {
        onAfterSubscribe: function(email) {
            //execute your code
        }
    };
    
    //then initialize
    ematics("create", ematicApikey, opt);
</script>
```
## Example Scenarios
---
Below is a example sequence of cart activities and the loggings that results from them.

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