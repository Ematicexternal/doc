---
layout: default
title:  "Theo dõi dữ liệu và sự kiện"
categories: Quick-Start
order: 4
---

# Theo dõi dữ liệu và sự kiện

## Chuẩn bị dữ liệu sản phẩm của bạn
---
Để sử dụng Retry-iQ, theo dõi dữ liệu và sự kiện phải được triển khai.

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

Mảng sản phẩm là ảnh chụp nhanh tất cả các mặt hàng trong giỏ hàng, tất cả các mặt hàng cần thanh toán hoặc tất cả các mặt hàng đang được chuyển đổi.

## Theo dõi sự kiện Ematic
---
Có 4 sự kiện (duyệt, giỏ hàng, thanh toán, chuyển đổi) cần được thực hiện trên trang web của bạn. Xin lưu ý rằng tất cả các phương thức này cần phải có sau khi đối tượng theo dõi Ematic được tạo.

### Khi khách hàng xem chi tiết sản phẩm
Call api gửi thông tin products **mảng**:

```js
//track items browsed
ematics("log", "product", "browse", products);
```
### Khi khách hàng click “Mua ngay” để thêm sản phẩm vào giỏ hàng
Call api gửi thông tin thêm sản phẩm vào giỏ hàng:

```js
//track items in cart to enable pre-abandonded cart overlays
ematics("log", "product", "cart", products);
```
> __Lưu ý:__ Nếu khách hàng cập nhật thông tin đơn hàng như số lượng, hay xóa sản phẩm thì phải gọi lại api này.

### Khi khách hàng click vào “Thanh toán” từ page Giỏ hàng
Call api gửi thông tin giỏ hàng:

```js
//track checkout
ematics("log", "product", "checkout", products);
```
### Khi khách hàng đặt hàng thành công
Sau khi khách hàng đặt hàng thành công, gọi api dưới đây:

```js
//track conversion
ematics("log", "product", "convert", products);
```
Bước này sẽ giúp khách hàng không nhận được email nếu họ đã đặt hành thành công


## Kịch bản ví dụ
---
Dưới đây là một chuỗi ví dụ về các hoạt động giỏ hàng và nhật ký kết quả từ chúng.

#### 1. Thêm mục A vào giỏ hàng
```js
products = [A];
ematics("log", "product", "cart", products);
```
#### 2. Thêm mục B vào giỏ hàng
```js
products = [A, B];
ematics("log", "product", "cart", products);
```
#### 3. Thêm mục C vào giỏ hàng
```js
products = [A, B, C];
ematics("log", "product", "cart", products);
```
#### 4. Xóa mục B khỏi giỏ hàng
```js
products = [A, C];
ematics("log", "product", "cart", products);
```
#### 5. Thêm mục C vào giỏ hàng
```js
products = [A, C, D];
ematics("log", "product", "cart", products);
```
#### 6. Bắt đầu quá trình thanh toán
```js
products = [A, C, D];
ematics("log", "product", "checkout", products);
```
#### 7. Hoàn tất thanh toán
```js
products = [A, C, D];
ematics("log", "product", "convert", products);
```