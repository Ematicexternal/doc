---
layout: default
title:  "Đăng ký hành vi khác hàng"
categories: Quick-Start
order: 4
---

# Đăng ký hành vi khác hàng

## Chuẩn bị dữ liệu sản phẩm của bạn
---
Để sử dụng RetryIQ, vui lòng làm theo hướng dẫn bên dưới.

Biến thông tin mảng products kèm theo khi gọi api có cấu trúc sau:

```js
// prepare the products array and issue the API call
  var products = [{
      id: "<id>", //required
      categoryId: <category id>,
      transactionId: <transaction id>,
      price: "<unit price with currency>", //required
      priceNumber: <price number in number format>, //required
      priceCurrency: "<price currency in three letter ISO format>", //required
      quantity: <quantity>, //required
      name: "<name>", //required
      brandName: "<brandname>", //required
      desc: "<description>",
      imageUrl: "<image url>", //required
      link: "<web link>" //required
  },
  ...
  {
      id: "<id>", //required
      categoryId: <category id>,
      transactionId: <transaction id>,
      price: "<unit price with currency>", //required
      priceNumber: <price number in number format>, //required
      priceCurrency: "<price currency in three letter ISO format>", //required
      quantity: <quantity>, //required
      name: "<name>", //required
      brandName: "<brandname>", //required
      desc: "<description>",
      imageUrl: "<image url>", //required
      link: "<web link>" //required
  }];
```

Lưu ý: gửi giá khuyến mãi nếu sản phẩm đang có khuyến mãi

Mảng products chứa thông tin về những sản phẩm mà khách hàng đã xem hoặc những sản phẩm trong giỏ hàng. Những thông tin này sẽ được đính kèm vào email gởi ra cho khách hàng để tăng tăng tỉ lệ mua hàng.

## Theo dõi sự kiện Ematic
---
Có 4 sự kiện (xem sản phẩm, xem giỏ hàng, bắt đầu thanh toán, mua hàng thành công) cần được theo dõi và gởi lên Ematic. Lưu lý là những sự kiện này chỉ được gọi sau khi dịch vụ Ematic đã được khởi tạo thành công ở bước "Tích hợp Ematic.js".

### Khi khách hàng xem chi tiết sản phẩm
khi khách hàng xem một sản phẩm, hãy gọi hàm dưới đây

```js
//track items browsed
ematics("log", "product", "browse", products);
```
### Thêm sảm phẩm vào giỏ hàng
Khi khách hàng thêm sản phẩm vào giỏ hàng, hãy gọi hàm dưới dây:

```js
//track items in cart to enable pre-abandonded cart overlays
ematics("log", "product", "cart", products);
```
> __Lưu ý:__ Nếu khách hàng cập nhật thông tin đơn hàng như số lượng, hay xóa sản phẩm thì phải gọi lại api này.

### Bắt đầu thanh toán/mua hàng
Khi khách hàng bắt đầu thanh toán, hãy gọi hàm dưới đây:

```js
//track checkout
ematics("log", "product", "checkout", products);
```
### Mua hàng thành công
Sau khi khách hàng đặt hàng thành công, gọi api dưới đây:

```js
//track conversion
ematics("log", "product", "convert", products);
```


## Ví dụ
---
Dưới đây là một chuỗi ví dụ về các hoạt động giỏ hàng và nhật ký kết quả từ chúng.

#### 1. Thêm sản phẩm A vào giỏ hàng
```js
products = [A];
ematics("log", "product", "cart", products);
```
#### 2. Thêm sản phẩm B vào giỏ hàng
```js
products = [A, B];
ematics("log", "product", "cart", products);
```
#### 3. Thêm sản phẩm C vào giỏ hàng
```js
products = [A, B, C];
ematics("log", "product", "cart", products);
```
#### 4. Xóa sản phẩm B khỏi giỏ hàng
```js
products = [A, C];
ematics("log", "product", "cart", products);
```
#### 5. Thêm sản phẩm C vào giỏ hàng
```js
products = [A, C, D];
ematics("log", "product", "cart", products);
```
#### 6. Bắt đầu quá trình thanh toán/mua hàng
```js
products = [A, C, D];
ematics("log", "product", "checkout", products);
```
#### 7. Đặt hàng thành công
```js
products = [A, C, D];
ematics("log", "product", "convert", products);
```