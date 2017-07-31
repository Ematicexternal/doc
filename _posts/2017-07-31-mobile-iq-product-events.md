---
layout: default
title:  "Usage & Product Events"
categories: Mobile-iQ
order: 4
---
# Usage

If user was **already logged in** (before you implemented MobileIQ), you need to tell MobileIQ which email address to use. You can do this by calling `MobileIQ.submitEmailAddress` method. E.g:

    MobileIQ.submitEmailAddress("john.doe@example.com");

_Note: Although it is enough to call this only once, you can call it every time the app starts, for example, after initialization code ([Setup, Step 2](http://api.ematicsolutions.com/v1/mobileiq/#setup))._

# Product Events

To submit a product event (browse, cart, checkout, conversion), call the corresponding method with a list of products (`List<? extends ProductInterface> products`), e.g:

    MobileIQ.Events.cart(products);

There are also methods that accept only one product (`? extends ProductInterface`) for each event (browse, cart, checkout, conversion). E.g:

    MobileIQ.Events.browse(product);

_Note: You can submit events before you submit an email address to MobileIQ, but they will be ignored until they are associated with an email address, which will happen after calling `submitEmailAddress` method. After that, events will be sent to Ematic. If a user changes his email address in your app, you should call `submitEmailAddress`method again, so all the future events are associated with the new email address._

## Product Browse Event

You should submit this event in your product Activity/Fragment/Dialog `onCreate` method:

    public void onCreate(Bundle savedInstanceState) {
       ...
       if (savedInstanceState == null) { // this will make sure the event is submitted only once, when opening the activity/fragment/dialog for the first time
          MobileIQ.Events.browse(product);
       }
    }

## Product Cart Event

Call this method every time a cart state is changed (product added / removed / quantity changed):

    MobileIQ.Events.cart(productsInCart);

_Note: You must call this method when the cart is emptied too, just pass an empty products list._

## Product Checkout Event

Call this method after a successful checkout.

    MobileIQ.Events.checkout(products);

## Product Convert Event

Call this if conversion was successful. For example, you may have a callback function on successful conversion - in that case, do this:

    public void onPaymentSuccessful(...) {
       ...
       MobileIQ.Events.convert(products);
    }

# Testing

Monitor logcat for messages with `MobileIQ` tag. If anything bad happens, it will show up there.

_Note: While your app is in debug mode, exceptions will be thrown if you submit invalid data (as shown in method's`throws` clause). However, in release builds, no exceptions will be thrown and MobileIQ will just ignore invalid data (in order to to prevent app crashes)._