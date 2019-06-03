---
layout: default
title:  "Developer Guide"
categories: RESTful-API
order: 1
---

<h1>Core API developer guide</h1>

* TOC
{:toc}

# Introduction

Ematic Solutions Core API is a set of RESTful web services that allow product logging and other events to be recorded through a technology independent API. This document provides some guidance on using the API in addition to the official [API Reference]({% post_url 2017-11-07-core-api %})

# Creating requests

## Hitting the right server

Client accounts are distributed among several data centers. When the client account is being created, an Ematic API key is generated for that account in the format: `<hash>-<suffix>`, where suffix indicates the data center where the account is located (for example: sg1). 

For the data to be successfully sent, the API client must send it to the right server. To get the correct url:
1. Extract the suffix from Ematic API key
2. Use the suffix as a replacement to &lt;suffix&gt; in: `https://<suffix>-api.ematicsolutions.com:8084/v2`<br>
        Example:
        `https://sg1-api.ematicsolutions.com:8084/v2`

If you happen to have a "us1" suffix, swap it with sg1.

## Authorization

In order to have requests authorized, you must provide HTTP Authorization header with every request. Authorization header consists of Ematic API key and an ESP (Email Service Provider) API key in the following format:

````yaml
Authorization: ematic-apikey=xxx-x,esp-apikey=yyyy
````

**xxx-x** - Ematic API key<br>
**yyyy** - ESP API key

## Format
Core API accepts and outputs only JSON format. XML format is not available. But it is a good practice to provide content type header:

````yaml
content-type: application/json
````

Every request other than GET accepts a body as a JSON object with properties specified in the API reference.

## User identification

Unique user identification is left to the client of this API. User can be identified in two ways:

1. By **uuid** field - client's unique identifier for the user
2. By **email** field - user's email address (if available)

At least one of these fields should be provided in the request, or the request will fail. It is recommended to provide both fields whenever possible.

## Client environment
For analytical purposes, we collect some details about the user environment, such as screen size and/or device model. This is provided to the Core API as a `clientEnv` JSON object (as a property of body object) with the following format:

````javascript
"clientEnv": {
    "deviceHeight": 0,
    "deviceWidth": 0,
    "viewportHeight": 0,
    "viewportWidth": 0,
    "country": "string",            // Country ISO code
    "language": "string",           // Language ISO code
    "currency": "string",           // Currency ISO code
    "device_uid": "string",         // Device UID (mobile only)
    "device_model": "string",       // Device model, for example 'Galaxy S8' (mobile only)
    "device_os_family": "string",   // Operating system family, for example 'Android'
    "device_os_version": "string"   // Operating system version, for example '6.0'
}
````

# Product logging

## Events

Main purpose of the Core API is to allow easier integration of Retry-IQ with different e-commerce patforms. For Retry-IQ to work, certain events related to products have to be recorded. Those events are:

1. **Product browse** - when user is looking at the product page
2. **Shopping cart update** - when user's shopping cart is updated (products added, removed, or quantity change)
3. **Checkout** - when user opens the checkout page
4. **Convert** - when the user has completed the order

## Product details

For every event, array of products should be sent to the Core API. Product is a JSON object with the following properties:

````javascript
{
      "experiment_id": 0,               // Must be 0
      "client_product_id": "string",    // Product ID
      "client_category_id": "string",   // Product category ID if available
      "price": "string",                // Formatted product price with currency
      "price_number": "string",         // Product price in number format
      "price_currency": "string",       // Product currency in three letter ISO format
      "name": "string",                 // Product name
      "description": "string",          // Product description (up to 255 characters)
      "brand_name": "string",           // Product brand if available
      "image_url": "string",            // URL to the product image
      "link": "string",                 // URL to the product page
      "misc1": "string",                // Place for custom product attributes
      "misc2": "string",                // Place for custom product attributes
      "misc3": "string"                 // Place for custom product attributes
}
````

## Example log request body

````json
{
  "uuid": "11279900",
  "email": "user@example.com",
  "clientEnv": {
    "deviceHeight": 0,
    "deviceWidth": 0,
    "viewportHeight": 0,
    "viewportWidth": 0,
    "country": "SG",
    "language": "en-SG",
    "currency": "SGD",
    "device_uid": "",
    "device_model": "",
    "device_os_family": "Windows",
    "device_os_version": "10"
  },
  "products": [
    {
      "experiment_id": 0,
      "client_product_id": "223",
      "client_category_id": "1",
      "price_number": 20.5,
      "price": "$20.50",
      "name": "T-Shirt",
      "description": "Men's T-Shirt",
      "brand_name": "Acme",
      "image_url": "http://www.mywebstore.com/images/products/product_223.jpg",
      "link": "https://www.mywebstore.com/products/223",
      "misc1": "Blue",
      "misc2": "XL",
      "misc3": ""
    }
  ]
}
````

# Subscriptions

Core API can also be used to add email addresses to an ESP list, or to remove them from it. **<span style="color:red;">Doing these operations without user's consent is prohibited!</span>**

## Subscribe

Following fields are used for the signup request:

1. `subscribe_email_addr` (required) - Email address to subscribe
2. `first_name` (optional) - User's first name
3. `last_name` (optional) - User's last name

Subscribe email address doesn't have to be the same as the identification email address, but it is recommended for two to be the same.

Example request:

````json
{
  "uuid": "11279900",
  "email": "user@example.com",
  "subscribe_email_addr": "user@example.com",
  "first_name": "John",
  "last_name": "Smith",
  "clientEnv": {
    "deviceHeight": 0,
    "deviceWidth": 0,
    "viewportHeight": 0,
    "viewportWidth": 0,
    "country": "SG",
    "language": "en-SG",
    "currency": "SGD",
    "device_uid": "",
    "device_model": "",
    "device_os_family": "Windows",
    "device_os_version": "10"
  }
}
````

## Unsubscribe

Unsubscribe uses `unsubscribe_email_addr` field to unsubscribe an email address. First name and last name don't have to be provided.