---
layout: default
title:  "Khởi tạo dịch vụ của Ematic.js"
categories: Quick-Start
order: 3
---

# Khởi tạo dịch vụ của Ematic.js

Trong trường hợp nếu website của bạn đang sử dụng requireJS thì làm theo hướng dẫn phía dưới (mục khởi tạo Ematic.js với requireJS)

Để sử dụng Bye-iQ, sao chép và dán đoạn code JavaScript dưới __đây trước thẻ__ ```</head>```


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

Khi chạy đoạn code trên, thư viện của Ematic đồng thời được load trên page và sau đó tạo ra một tracker object cho Ematic API key được chọn

### Thêm địa chỉ email vào tập lệnh

Khi người dùng đăng nhập, bạn cần chuyển email bằng phương thức này để theo dõi chính xác:

```js
ematics("set", "email", "<email of the user logged in if applicable>")
```
---
# Khởi tạo dịch vụ của Ematic.js on RequireJS:

Nếu website của bạn sử dụng requireJS, tạo configuration như dưới đây để khởi tạo dịch vụ của Ematic

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
        "ematics": "//api.ematicsolutions.com/v1/ematic.min",
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
> __Lưu ý:__ Cookies được dùng để đọc các sự Unique and để giới hạn hiển thị của popups. Cookies cần xoá trong đặt order để thử thử các hiển thị của popups.

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