---
layout: default
title:  "Magento 1.x"
categories: Ecommerce-Plugins
order: 1
---

# Ematic.js module for Magento 1.x

## Manual Installation

Do the following steps to install the module manually:

1.  Download the module archive from [this link](http://api.ematicsolutions.com/v1/plugins/dist/ematicsolutions_ematicjs_v1.0.9-mage1.zip)
2.  Upload it to the root folder of your Magento website, and then extract the contents.
3.  Log in to the Magento back-end, and then refresh the cache in _System > Cache Management_.
4.  Log out, and then login again.
5.  Proceed to configuring your module.

## Manual Uninstallation

To uninstall the module manually, do the following:

1.  Remove the _app/etc/modules/Ematicsolutions_Ematicjs.xml_ file.
2.  Remove folders:
    1.  app/code/community/Ematicsolutions/Ematicjs
    2.  js/ematic
3.  Log in to the Magento back-end, and then refresh the cache in _System > Cache Management_.

## Configuration

To configure the module, login to the Magento admin panel and go to _System -> Configuration_, then choose _Ematic Solutions -> Ematic.js Options_ on the left.

### Ematic.js Options

#### **API Key**

Enter the API key that you should have received from Ematic Solutions.

#### **Use long description**

Change this to **Yes** if the description of your product is less than a few words.

### Advanced options

> These options are used in case that your Magento shop uses 3rd party modules for shopping cart or checkout process, or some custom solution. **These options require inspecting the website and requests it sends via the web browser's developer tools, such as Firebug or Chrome Developer Tools. 
Note: If you are not sure how to do this, contact Ematic Solutions for assistance.**

Both of these options have default values set up for Magento without 3rd party modules for checkout or shopping cart. Every page that triggers one of the events should be in a separate text line within the field. You can also use an asterisk (*) to match pages that can have optional parameters.

Matching is performed by checking if a page URL ends with any of the text lines entered in the settings. If there is an asterisk at the end of the line, it will check if that text appears anywhere in the URL. Website domain is **not** checked.

#### **Checkout URL match**

Enter your checkout page address here if you are not using the default Magento checkout module. For example, if the URL of your checkout page is _https://www.mywebshop.com/**onepage/**,_ then **onepage/** is the value you should add here.

Depending on the used module(s), possible values could be **onepage/** , **fancycheckout/offcanvascheckout/stepshipping**, and so on.

Default value:

    checkout/onepage/

#### **Cart URL match**

This value is used in order for a plugin to detect dynamic cart updates. Examine your URLs when you visit or update the shopping cart. If it contains the word **cart**, then you're good to go. But if not, find some parts that are the same for all URLs. It must not be identical to the _Checkout URL match_ option. For example, if you're using the Fancycheckout module, you should enter **offcanvascheckout*** as the value.

Default value:

    cart/*