---
layout: default
title:  "Initializing Ematic.js"
categories: Quick-Start
order: 1
---

# Ematic Platform - Main Part
* Paste the following JavaScript snippet into your website templates so that it appears __before the closing__ ```</head>``` tag.
* When this code runs, it asynchronously loads the __ematic.min.js__ library onto the page, creates a tracker object for the __Ematic APIKey__ you've specified.

```js
<script>
    (function(i,s,o,g,r,a,m){i['EmaticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//api.ematicsolutions.com/v1/ematic.min.js','ematics');

    var ematicApikey = "<Environment specific Ematic APIKey>";
    var opt = {
        email: "<email of the user logged in if applicable>",
        country_iso: "<current country iso code>",
        currency_iso: "<current currency iso code>",
        language_iso: "<current language iso code>"
    };
    
    //initialize
    ematics("create", ematicApikey, opt);
</script>
```
## Require.js Initialization
```js
require.config({
    config: {
        'ematics': {
            'apikey' : "<environment specific ematic apikey",
            'opt' : {
                country_iso: "<country>",
                currency_iso: "<currency>",
                language_iso: "<language>"
            }
        }
    },
    paths: {
        "ematics": "//api.ematicsolutions.com/v1/ematic.require.min",
        "jquery": "https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min" //or your local jquery path
    },
    shim: {
        'ematics': ['jquery']
    }
});

require(["ematics"], function() {
    ematics("set", "email", "<email of the user logged in if applicable>");

    //execute your code
});
```
> __Important Note:__ Cookies are used to track unique visitors and to limit the display of the popups. In order to re-test the display of the popups, __cookies will have to be cleared__.