---
layout: default
title:  "Setup"
categories: Mobile-iQ
order: 2
---
# Setup

1. Write your own `Application` class (Documentation: [Application](https://developer.android.com/reference/android/app/Application.html)). If you already did this, go to the next step:

2. Add Mobile-IQ initialization code to your application `onCreate` method:

    MobileIQ.init(getApplicationContext(), "<your_ematic_api_key>", "<your_esp_api_key>");

3. Implement `ProductInterface` (`com.ematicsolutions.mobileiq.model.ProductInterface`) in your product class, for example:

    public class Product implements ProductInterface {

        protected long id;
        protected Long categoryId;
        protected Long transactionId;
        protected double price;
        protected String currency;
        protected int quantity;
        protected String name;
        protected String brand;
        protected String desc;

        @Override
        public long getMobIqId() {
            return id;
        }

        @Override
        public Long getMobIqCategoryId() {
            return categoryId;
        }

        @Override
        public Long getMobIqTransactionId() {
            return transactionId;
        }

        @Override
        public String getMobIqPrice() {
            return String.format(Locale.US, "%s %.2f", currency, price);
        }

        @Override
        public int getMobIqQuantity() {
            return quantity;
        }

        @Override
        public String getMobIqName() {
            return name;
        }

        @Override
        public String getMobIqBrandName() {
            return brand;
        }

        @Override
        public String getMobIqDescription() {
            return desc;
        }

        @Override
        public String getMobIqImageUrl() {
            return "http://mywebsite.com/img/product_" + id + ".jpg";
        }

        @Override
        public String getMobIqLink() {
            return "http://mywebsite.com/product/" + id;
        }

        @Override
        public String getMobIqMisc1() {
            return null;
        }

        @Override
        public String getMobIqMisc2() {
            return null;
        }

        @Override
        public String getMobIqMisc3() {
            return null;
        }
    }

You are now ready to start using MobileIQ in your app.