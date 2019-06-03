---
layout: default
title:  "Prestashop 1.6.x"
categories: Ecommerce-Plugins
order: 7
---

# Ematic.js module for Prestashop 1.6.x and below

## Installation

Do the following steps to install the module:

1.  Download the module archive from [this link.](http://api.ematicsolutions.com/v1/plugins/dist/ematics_v2.zip)
2.  Login to your Back Office (admin panel).
3.  Go to 'Modules and Services'.
4.  On the top-right corner press on 'Add new module' button.
5.  Upload your module as shown below:
![Screenshot](https://bye.ematicsolutions.com/img/module1.png)
6.  Install and configure the uploaded module:
![Screenshot](https://bye.ematicsolutions.com/img/module2.png)

## Configuration

Do the following steps to configure the module:

1.	Go to 'Modules and Services' and find Ematics module.
2.	Enter your Ematic API Key and Save.

![Screenshot](https://bye.ematicsolutions.com/img/module3.png)

#### **API Key**

You should receive an API Key from Ematic Solutions, if you don't have an API Key please contact your Customer Success Manager.

## Ajax Cart Logging

By default Ematics module works with a standard cart system that refreshes the page after adding product to a cart.
If your website is using Ajax cart system (no page-refresh) then you should add below code to your theme.

In your /web/themes/<your theme>/js/modules/blockcart/ajax-cart.js code you will insert a call to the following method in two places:

    ematics_blockcart_log(jsonData);

It should be inserted in the "add" method's "success" callback function at the very top, for example:

    add : function(idProduct, idCombination, addedFromProductPage, callerElement, quantity, whishlist){
    ...
    //send the ajax request to the server
    $.ajax({
      
      ...
      success: function(jsonData,textStatus,jqXHR)
      {
        //Ematics Module
        ematics_blockcart_log(jsonData);
        // add appliance to whishlist module
        if (whishlist && !jsonData.errors)
          ...

It should be inserted in the "remove" method's "success" callback function at the very top, for example:

    remove : function(idProduct, idCombination, customizationId, idAddressDelivery){
    //send the ajax request to the server
    $.ajax({
      ...
      success: function(jsonData) {
        //Ematics Module
        ematics_blockcart_log(jsonData); 
        ...
      }

## Uninstallation

To uninstall the module, do the following:

1.  In your back office go to 'Modules and Services'.
2.  Find Ematics module.
3.  On the 'Configure' drop-down press 'Uninstall' (alternatively you can just Disable the module).
4.	When prompted with an alert asking if you want to uninstall this module press 'Ok'.

## **Testing**

Cookies are used to track unique visitors and to limit the display of the popup. Cookies will need to be cleared to re-test the display of the popup, alternatively you can use Incognito Mode in Chrome.