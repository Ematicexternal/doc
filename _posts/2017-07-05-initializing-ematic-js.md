---
layout: default
title:  "Initializing Ematic.js"
categories: Quick-Start
order: 1
---

# Initializing Ematic.js

If your website is using requireJS, move to the requireJS part in this page that is built specifically for it.

To use Bye-iQ, copy and paste the following JavaScript snippet into your website templates so that it appears __before the closing__ ```</head>``` tag:


```js
<script>
    (function(i,s,o,g,r,a,m){i['EmaticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//api.ematicsolutions.com/v1/ematic.min.js','ematics');
    
    //initialize
    ematics("create", ematicApikey, null);
</script>
```

When the code runs, it asynchronously loads the __ematic.min.js__ library onto the page, and then creates a tracker object for the __Ematic API Key__ you have specified.

### Adding email address into the script

Once the user logs in, you need to pass the email with this method in order to track accurately:

```js
ematics("set", "email", "<email of the user logged in if applicable>")
```
---
# Initializing Ematic.js on RequireJS:

If your website is using requireJS, use the following configuration in order to initialize the object properly:

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
> __Important Note:__ Cookies are used to track unique visitors and to limit the display of the popups. Cookies must be cleared in order to re-test the display of the popups.

## onAfterSubscribe Event
---
Alternately, you can trigger your custom code when a visitor subscribes using Bye-iQ by defining an event as shown below as part of the "opt" object that is passed on when you initialize the library.

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