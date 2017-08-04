---
layout: default
title:  "Magento 2.x"
categories: Ecommerce-Plugins
order: 2
---

# Ematic.js module for Magento 2.x

## Manual Installation

Do the following steps to install the module manually:

1.  Connect to your website via SSH.
2.  Go to the root folder of your Magento 2 web site.
3.  Execute the commands in the box below.
4.  Log in to you Magento 2 Admin panel.
5.  Proceed to configuring your module.

Commands (Step 3):

    wget http://api.ematicsolutions.com/v1/plugins/dist/ematicsolutions_ematicjs_v1.0.2-mage2.zip
    mkdir -p ./app/code/Ematicsolutions/Ematicjs
    unzip ematicsolutions_ematicjs_v1.0.2-mage2.zip -d ./app/code/Ematicsolutions/Ematicjs
    ./bin/magento setup:upgrade
    ./bin/magento cache:flush
    rm ematicsolutions_ematicjs_v1.0.2-mage2.zip

If `./bin/magento` does not run, try executing `chmod +x ./bin/magento` to make it executable.

## Manual Uninstallation

Do the following steps to install the module manually:

1.  Connect to your website via SSH.
2.  Go to the root folder of your Magento 2 website.
3.  Execute the commands below:

    rm -rf ./app/code/Ematicsolutions/Ematicjs
    ./bin/magento setup:upgrade
    ./bin/magento cache:flush

If `./bin/magento` does not run, try executing `chmod +x ./bin/magento` to make it executable.

## Configuration

To configure the module, log in to the Magento Admin panel, and then go to _Stores > Configuration_. Choose _Ematic Solutions > Ematic.js Options_ on the left.

### Ematic.js Options

#### **API Key**

Here, you should enter your API key that you should have received from Ematic Solutions.

#### **Use long description**

Change this to Yes if the descriptions of your product is less than few words.

### Advanced options

> These options are used in case that your Magento shop uses 3rd party modules for shopping cart or checkout process, or some custom solution. **These options require inspecting the website and requests it sends via the web browser's developer tools, such as Firebug or Chrome Developer Tools. 
Note: If you are not sure how to do this, contact Ematic Solutions for assistance.**

Both of these options have default values set up for Magento 2 without 3rd party modules for checkout or shopping cart. Every page that triggers one of the events should be in a separate text line within the field. You can also use an asterisk (*) to match pages that can have optional parameters.

Matching is performed by checking if a page URL ends with any of the text lines entered in the settings. If there is an asterisk at the end of the line, it will check if that text appears anywhere in the URL. Website domain is **not** checked.

#### **Checkout URL match**

Enter your checkout page address here if you are not using the default Magento checkout module.  

For example, if the URL of your checkout page is _https://www.mywebshop.com/**onepage/**,_ then **onepage/** is the value you should add here.

Defaults to:

    checkout/
    multishipping/checkout/

#### **Cart URL match**

This value is used in order for a plugin to detect dynamic cart updates. Examine your URLs when you add/remove/update items in the shopping cart. Find some parts that are the same for all URLs and add it here.

Defaults to:

    checkout/sidebar/*
    checkout/cart/add/*