# Multi-Vendor E-commerce Database

## Description
This project is a scalable **MySQL database** designed to support a multi-vendor e-commerce platform. It efficiently manages users, sellers, products, categories, orders, payments, and reviews while ensuring data integrity and relational consistency. The database is optimized for querying large datasets and supports essential e-commerce functionality such as order tracking, product reviews, and multi-payment methods.

---

## Features
- **User Management**: Stores customer details, including usernames, emails, addresses, and phone numbers.
- **Seller Management**: Manages seller profiles, store details, and product listings.
- **Product Management**: Handles product information, categories, pricing, and inventory levels.
- **Order Management**: Tracks orders, order items, and their statuses (Pending, Shipped, Delivered, etc.).
- **Payment Processing**: Supports multiple payment methods (Credit Card, PayPal, COD, etc.) and tracks payment statuses.
- **Product Reviews**: Allows customers to leave ratings and comments on products.

---

## Database Schema
The database contains the following main tables:
1. **Users**: Stores customer data.
2. **Sellers**: Manages seller details.
3. **Categories**: Organizes products into categories.
4. **Products**: Stores product details with relationships to sellers and categories.
5. **Orders**: Tracks orders and their statuses.
6. **OrderItems**: Associates products with specific orders.
7. **Reviews**: Manages customer reviews and ratings.
8. **Payments**: Tracks payment details for orders.



