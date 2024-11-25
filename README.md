Create the database
CREATE DATABASE MultiVendorECommerce;
USE MultiVendorECommerce;

Table for users (customers)
CREATE TABLE Users (
    UserID INT AUTO_INCREMENT PRIMARY KEY,
    Username VARCHAR(50) NOT NULL UNIQUE,
    Email VARCHAR(100) NOT NULL UNIQUE,
    PasswordHash VARCHAR(255) NOT NULL,
    FullName VARCHAR(100),
    PhoneNumber VARCHAR(15),
    Address TEXT,
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Table for sellers
CREATE TABLE Sellers (
    SellerID INT AUTO_INCREMENT PRIMARY KEY,
    SellerName VARCHAR(100) NOT NULL,
    Email VARCHAR(100) NOT NULL UNIQUE,
    PasswordHash VARCHAR(255) NOT NULL,
    ContactNumber VARCHAR(15),
    StoreName VARCHAR(100) UNIQUE,
    StoreAddress TEXT,
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Table for product categories
CREATE TABLE Categories (
    CategoryID INT AUTO_INCREMENT PRIMARY KEY,
    CategoryName VARCHAR(100) NOT NULL UNIQUE,
    Description TEXT
);

Table for products
CREATE TABLE Products (
    ProductID INT AUTO_INCREMENT PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Description TEXT,
    Price DECIMAL(10, 2) NOT NULL,
    QuantityAvailable INT DEFAULT 0,
    SellerID INT,
    CategoryID INT,
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (SellerID) REFERENCES Sellers(SellerID) ON DELETE CASCADE,
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID) ON DELETE SET NULL
);

Table for orders
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    UserID INT,
    OrderDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    TotalAmount DECIMAL(10, 2) NOT NULL,
    Status ENUM('Pending', 'Processing', 'Shipped', 'Delivered', 'Cancelled') DEFAULT 'Pending',
    FOREIGN KEY (UserID) REFERENCES Users(UserID) ON DELETE CASCADE
);

Table for order items
CREATE TABLE OrderItems (
    OrderItemID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT NOT NULL,
    Price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE CASCADE,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID) ON DELETE CASCADE
);

Table for product reviews
CREATE TABLE Reviews (
    ReviewID INT AUTO_INCREMENT PRIMARY KEY,
    ProductID INT,
    UserID INT,
    Rating INT CHECK (Rating BETWEEN 1 AND 5),
    Comment TEXT,
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID) ON DELETE CASCADE,
    FOREIGN KEY (UserID) REFERENCES Users(UserID) ON DELETE CASCADE
);

Table for payments
CREATE TABLE Payments (
    PaymentID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT,
    PaymentMethod ENUM('Credit Card', 'Debit Card', 'PayPal', 'Net Banking', 'COD') NOT NULL,
    PaymentStatus ENUM('Pending', 'Completed', 'Failed') DEFAULT 'Pending',
    PaymentDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) ON DELETE CASCADE
);

Sample data insertion for testing
INSERT INTO Categories (CategoryName, Description)
VALUES 
    ('Electronics', 'Devices and gadgets'),
    ('Books', 'Printed and digital books'),
    ('Clothing', 'Men and Women apparel');

INSERT INTO Sellers (SellerName, Email, PasswordHash, ContactNumber, StoreName, StoreAddress)
VALUES 
    ('TechMart', 'techmart@example.com', 'hashed_password1', '1234567890', 'TechMart Store', '123 Tech Street'),
    ('BookWorld', 'bookworld@example.com', 'hashed_password2', '0987654321', 'BookWorld Store', '456 Book Lane');

INSERT INTO Products (ProductName, Description, Price, QuantityAvailable, SellerID, CategoryID)
VALUES 
    ('Smartphone', 'Latest Android smartphone', 699.99, 50, 1, 1),
    ('Laptop', 'Lightweight laptop for productivity', 1299.99, 20, 1, 1),
    ('Fiction Book', 'Bestselling fiction novel', 19.99, 100, 2, 2);
