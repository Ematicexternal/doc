---
layout: default
title:  "Tích hợp Ematic.js"
categories: Quick-Start
order: 3
---

# Tích hợp Ematic.js

Nếu website của bạn đang sử dụng requireJs thì làm theo hướng dẫn ở mục "Tích hợp Ematic.js với RequireJS" (bên dưới)

Để sử dụng Bye-iQ, sao chép và dán đoạn code JavaScript dưới __đây trước thẻ__ ```</head>```


```js
<script>
    (function(i,s,o,g,r,a,m){i['EmaticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//api.ematicsolutions.com/v1/ematic.min.js','ematics');
    
    var opt = {
        email: "<email of the user logged in if applicable>",
        country_iso: "<country>",
        currency_iso: "<currency>",
        language_iso: "<language>"
    }

    //initialize
    ematics("create", ematicApikey, opt);
</script>
```

Khi chạy đoạn code trên, thư viện của Ematic sẽ được tải về và sau đó tạo ra một tracker object với ematicApiKey đã khai báo

### Đăng ký email khách hàng với dịch vụ của Ematic

Khi khách hàng đăng nhập hoặc để lại email trên website, gọi hàm ematic bên dưới để đăng ký email với Ematic. Việc này sẽ giúp dịch vụ của Ematic làm việc hiệu quả:

```js
ematics("set", "email", "<email of the user logged in if applicable>")
```
---
# Tích hợp Ematic.js với requireJs:

Nếu website của bạn sử dụng requireJS, tạo cấu hình như sau để khởi tạo và sử dụng dịch vụ của Ematic

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
        "ematics": "//api.ematicsolutions.com/v1/ematic.min"
    }
});

require(["ematics"], function() {
    ematics("set", "email", "<email of the user logged in if applicable>");

    //execute your code
});
```
> __Lưu ý:__ Cookies được sử dùng để định danh người dùng và giới hạn lượt hiển thị của popups. Trong trường hợp bạn muốn kiểm tra việc hiển thị popup của ByeIQ, bạn nên sử dụng trình duyệt ẩn danh hoặc phải xóa cookies của trình duyệt.

## onAfterSubscribe Event
---
Ngoài ra, bạn có thể đăng ký sự kiện onAfterSubscribe lúc khởi tạo. Hàm này sẽ được gọi khi có khách hàng đăng ký email trên Bye-iQ popup.

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