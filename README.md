# ShopLite: Object-Oriented E-Commerce System

**Subject:** Object-Oriented Programming 1 (OOP)  
**Language:** Java (JDK 17+)  
**Project Type:** Console-Based Application (CLI)

---

## 📖 Project Overview

**ShopLite** is a robust console-based application designed to simulate the backend logic of a modern e-commerce platform. The system allows users to browse a catalog, perform smart searches, manage a shopping cart, and execute secure checkout transactions.

Unlike simple flat-file managers, ShopLite utilizes a hierarchical object structure to differentiate between **Physical** and **Digital** goods. It demonstrates the practical application of the four pillars of OOP, combined with persistent data storage (File Handling) and robust error management (Exception Handling).

---

## 🚀 Key Features

### User Features
*   **Dynamic Catalog:** View a live list of products with real-time stock and price updates.
*   **Smart Search Algorithm:** Users can search for products using keywords (e.g., "Gaming", "Office", "Pro"). The system supports partial matching and is case-insensitive.
*   **Shopping Cart System:** Add items to a temporary cart with automatic stock validation.
*   **Automated Checkout:** Calculates subtotals, applies shipping logic based on product type, and generates a detailed receipt.

### Technical Features
*   **Data Persistence:** Product inventory is loaded from `products.txt` on startup and updated automatically after every sale.
*   **Audit Trail:** Every successful transaction generates a unique, timestamped receipt file in the `orders/` directory.
*   **Crash Resistance:** Handles invalid inputs and missing files gracefully without crashing the program.

---

## 🏗️ Technical Architecture (OOP Concepts)

This project strictly adheres to Object-Oriented Programming principles:

### 1. Encapsulation (Data Security)
*   **Implementation:** The `Product` class declares fields (`stock`, `price`, `id`) as `private`.
*   **Why:** This prevents external classes from directly modifying sensitive data. Inventory can only be reduced via the `reduceStock()` method, which performs logic checks to prevent negative stock.

### 2. Inheritance (Code Reusability)
*   **Implementation:**
    *   **Parent:** `Product` (Abstract Base Class)
    *   **Children:** `PhysicalProduct` and `DigitalProduct`
*   **Why:** Common attributes (ID, Name, Price) are defined once in the parent. Child classes only contain specific unique fields (e.g., `shippingFee` for physical items).

### 3. Polymorphism (Dynamic Behavior)
*   **Implementation:** The method `calculateTotalCost()` is overridden in child classes.
    *   `PhysicalProduct`: Returns `Price + ShippingFee`.
    *   `DigitalProduct`: Returns `Price` (0 shipping).
*   **Why:** The Checkout module treats all items as `Product` objects. It calls `.calculateTotalCost()` and the specific logic is executed at runtime depending on the object type.

### 4. Abstraction (Blueprints)
*   **Implementation:** The `Product` class is `abstract` and defines abstract methods like `toCSV()`.
*   **Why:** This enforces a contract that ensures any future product types (e.g., `ServiceProduct`) must implement specific behaviors before they can be added to the system.

---

## 📂 File Handling & Storage

The system uses text-based file handling to simulate a database.

### 1. The Database (`products.txt`)
Stores inventory in CSV format: `Type,ID,Name,Price,Stock`
```text
Physical,101,Mechanical Keyboard,1500.0,15
Digital,201,Antivirus License,500.0,100