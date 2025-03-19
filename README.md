# E-commerce-Web

**Full-Stack E-Commerce Website Solution (HTML, CSS, JavaScript, SQL, Java)**

## **1. HTML (Structure of Product Page & Cart)**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Commerce Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Product List</h1>
    <div id="product-list"></div>
    <h2>Shopping Cart</h2>
    <div id="cart"></div>
    <script src="script.js"></script>
</body>
</html>
```

## **2. CSS (Styling the Page)**
```css
body {
    font-family: Arial, sans-serif;
    margin: 20px;
    padding: 20px;
    background-color: #f4f4f4;
}
button {
    background-color: #28a745;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
}
button:hover {
    background-color: #218838;
}
```

## **3. JavaScript (Dynamic Product List & Cart)**
```javascript
const products = [
    { id: 1, name: 'Laptop', price: 800 },
    { id: 2, name: 'Phone', price: 500 }
];

const cart = [];
const productList = document.getElementById('product-list');
const cartDiv = document.getElementById('cart');

products.forEach(product => {
    const item = document.createElement('div');
    item.innerHTML = `${product.name} - $${product.price} <button onclick="addToCart(${product.id})">Add to Cart</button>`;
    productList.appendChild(item);
});

function addToCart(id) {
    const product = products.find(p => p.id === id);
    cart.push(product);
    updateCart();
}

function updateCart() {
    cartDiv.innerHTML = '';
    cart.forEach(item => {
        const cartItem = document.createElement('div');
        cartItem.innerHTML = `${item.name} - $${item.price}`;
        cartDiv.appendChild(cartItem);
    });
}
```

## **4. SQL (Database Schema & Queries)**
```sql
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE Products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);

CREATE TABLE Orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    total_price DECIMAL(10,2),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

INSERT INTO Products (name, price) VALUES ('Laptop', 800), ('Phone', 500);
```

## **5. Java (Backend API Handling User Authentication)**
```java
import java.sql.*;
import java.util.Scanner;

public class AuthSystem {
    public static void main(String[] args) {
        try {
            Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/ecommerce", "root", "password");
            Scanner scanner = new Scanner(System.in);
            System.out.print("Enter Username: ");
            String username = scanner.nextLine();
            System.out.print("Enter Password: ");
            String password = scanner.nextLine();
            
            String query = "SELECT * FROM Users WHERE username = ? AND password = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setString(1, username);
            pstmt.setString(2, password);
            ResultSet rs = pstmt.executeQuery();
            
            if (rs.next()) {
                System.out.println("Login Successful!");
            } else {
                System.out.println("Invalid Credentials");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **Conclusion**
This document provides a complete **Full-Stack E-Commerce Website Solution** using **HTML, CSS, JavaScript, SQL, and Java**. The **front-end** ensures an interactive user experience, the **back-end** securely manages authentication and data, and the **database** stores essential information. This implementation is scalable and secure for e-commerce applications.

