---
layout: default
title:  "Magento 2.x"
categories: Ecommerce-Plugins
order: 2
---

# Ematic.js module for Magento 2.x

## Installation

### Manually

To install the module manually, follow these steps:

1.  Connect to your website via SSH
2.  Go to the root folder of your Magento 2 web site
3.  Execute the commands in the box below
4.  Login to you Magento 2 admin panel
5.  Proceed to module configuration

Commands (step 3):

    wget http://api.ematicsolutions.com/v1/plugins/dist/ematicsolutions_ematicjs_v1.0.2-mage2.zip
    mkdir -p ./app/code/Ematicsolutions/Ematicjs
    unzip ematicsolutions_ematicjs_v1.0.2-mage2.zip -d ./app/code/Ematicsolutions/Ematicjs
    ./bin/magento setup:upgrade
    ./bin/magento cache:flush
    rm ematicsolutions_ematicjs_v1.0.2-mage2.zip

If `./bin/magento` does not run, try executing `chmod +x ./bin/magento` to make it executable.

## Uninstallation

### Manually

To uninstall the module manually, follow these steps:

1.  Connect to your website via SSH
2.  Go to the root folder of your Magento 2 web site
3.  Execute the commands below

    rm -rf ./app/code/Ematicsolutions/Ematicjs
    ./bin/magento setup:upgrade
    ./bin/magento cache:flush

If `./bin/magento` does not run, try executing `chmod +x ./bin/magento` to make it executable.

## Configuration

To configure the module, login to the Magento admin panel and go to _Stores -> Configuration_, then choose _Ematic Solutions -> Ematic.js Options_ on the left.

### Ematic.js Options

#### **API Key**

Here, you should enter your API key that you should have received from Ematic Solutions.

#### **Use long description**

Change this to Yes if short descriptions of your products have less than few words.

### Advanced options

> These options are used in case that your Magento shop uses 3rd party modules for shopping cart or checkout process, or some custom solution. **These options require inspecting the website and requests it sends via web browser's developer tools, such as Firebug or Chrome Developer Tools. If you are not sure how to do this, contact Ematic Solutions for assistance.**

Both of these options have default values set up for Magento 2 without 3rd party modules for checkout or shopping cart. Every page that should trigger one of the events should be in a separate text line within the field. You can also use asterisk (*) to match pages that can have optional parameters.

Matching is performed by checking if a page URL ends with any of the text lines entered in the settings. If there is an asterisk at the end of the line, it will check if that text appears anywhere in the URL. Website domain is **not** checked.

#### **Checkout URL match**

If you're not using default Magento checkout module, please enter your checkout page(s) here. For exampe, if the URL of your checkout page is _https://www.mywebshop.com/**onepage/**,_ then **onepage/** is the value you should add here.

Defaults to:

    checkout/
    multishipping/checkout/

#### **Cart URL match**

This value is used in order for plugin to detect dynamic cart updates. Examine your URLs when you add/remove/update items in the shopping cart. Find some part that is the same for all URLs and add it here.

Defaults to:

    checkout/sidebar/*
    checkout/cart/add/*