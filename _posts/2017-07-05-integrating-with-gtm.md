---
layout: default
title:  "Integrating with GTM"
categories: Quick-Start
order: 3
---
# Integrating with Google Tag Manager

## Steps
1. Prepare the data needed from your backend and send it as dataLayer object
2. Go to your GTM Account
3. Create new GTM tag
4. Paste the script and choose the trigger
5. Preview the tag to test it
6. Publish the tag

---
## Initializing Ematic.js With GTM

In order to use Bye-iQ, you just need to copy and paste Ematic initial script to the custom HTML tag in GTM. These are the steps:

### Go to your GTM account & create new tag
---
![alt text](http://i.imgur.com/k7F0xpY.png)


### Choose Custom HTML as a tag
---
![alt text](http://i.imgur.com/mialH1Y.png)


### Choose All Pages - DOM Ready as the trigger
---
![alt text](http://i.imgur.com/yqSb5Q9.png)


### Paste the code to the HTML box
---
![alt text](http://i.imgur.com/pXucu6P.png)

---
## Retry-iQ Implementation With GTM

In order to use Retry-iQ, you have to implement 4 events (browse, cart, checkout, conversion) to the GTM as well.

The first step is to prepare your data. Then call our methods based on how your website is structured.

### Preparing Data Layer
---
```js
dataLayer.push({
    'PageType': 'Productpage',
    'Email': 'alex.kurniawan@ematicsolutions.com',
    'ProductName': 'Sunset Credenza',
    'ProductId': '43243',
    'ProductPrice': 'Rp 2.449.300',
    'BrandName': 'Hemma',
    'ImageUrl':'https://yourimageurlcdn.imgix.net/catalog/product/cache/1/thumbnail/1200x/17f82f742ffe127f42dca9de82fb58b1/p/r/product-page_mg_0305.jpg'
});
```


### Abandoned Browse Code Example
---
{% raw %}
```js
<script>

  (function(i,s,o,g,r,a,m){i['EmaticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//api.ematicsolutions.com/v1/ematic.min.js','ematics');

    var ematicApikey = "xx91c1b3d11e5a40a0fasdc1100333-sgx";
    var opt = {
        email: "{{Email}}",
        country_iso: "id",
        currency_iso: "IDR",
        language_iso: "id"
    };

    //initialize
    ematics("create", ematicApikey, opt);
    
    var abpCall = function() {
        var product = {
          id: "{{ProductId}}", 
          price: "{{ProductPrice}}", 
          quantity: 1,
          name: "{{ProductName}}", 
          brandName: "{{BrandName}}",
          imageUrl: "{{ImageUrl}}",
          link: location.protocol + '//' + location.host + location.pathname;
        };

        if(product.name && product.imageUrl && product.link ) {
            // call the "browse" method
            ematics("log", "product", "browse", [product]);
        }
    }

    if(  {{PageType}} == "Productpage" ) {
        abpCall();
    }

</script>
```
{% endraw %}