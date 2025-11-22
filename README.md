# Restaurant-QR-Menu-System-Java-project
 The application transforms traditional restaurant service by allowing customers to scan table-specific QR codes with their smartphones, instantly accessing a dynamic digital menu. Customers can browse items by category, add selections to their cart, and place orders directly from their device without requiring app downloads or additional software.
# Restaurant QR Code Menu System

A complete Java-based web application for restaurants to manage digital menus with QR code table access.

## Features

### Customer Features
- 📱 Scan QR code at table to view menu
- 🍔 Browse menu items by category
- 🛒 Add items to cart with quantity control
- 📝 Place orders with table number
- 📊 Responsive design for mobile and desktop

### Staff Features
- ➕ Add, edit, and delete menu items
- 🏷 Organize items by categories
- 👁 View all active orders in real-time
- ✅ Update order status (Pending → Preparing → Completed)
- 🔲 Generate QR codes for all tables
- 📋 Filter orders by table number

## Technology Stack

- *Backend*: Java 17+, Spring Boot 2.7+
- *Database*: H2 (in-memory for development)
- *QR Code*: ZXing library
- *Frontend*: HTML5, CSS3, Vanilla JavaScript
- *API*: RESTful architecture

## Project Structure


restaurant-menu-system/
├── src/
│   ├── main/
│   │   ├── java/com/restaurant/menu/
│   │   │   ├── RestaurantMenuApplication.java
│   │   │   ├── controller/
│   │   │   │   ├── MenuController.java
│   │   │   │   ├── OrderController.java
│   │   │   │   └── QRCodeController.java
│   │   │   ├── model/
│   │   │   │   ├── MenuItem.java
│   │   │   │   ├── Order.java
│   │   │   │   └── OrderItem.java
│   │   │   ├── repository/
│   │   │   │   ├── MenuItemRepository.java
│   │   │   │   └── OrderRepository.java
│   │   │   └── service/
│   │   │       ├── MenuService.java
│   │   │       ├── OrderService.java
│   │   │       └── QRCodeService.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── static/
│   │           └── index.html
│   └── test/
└── pom.xml


## Setup Instructions

### Prerequisites
- Java 17 or higher
- Maven 3.6+
- Any modern web browser

### Installation

1. *Create the project structure*:
bash
mkdir -p restaurant-menu-system/src/main/java/com/restaurant/menu/{controller,model,repository,service}
mkdir -p restaurant-menu-system/src/main/resources/static
cd restaurant-menu-system


2. *Create pom.xml*:
xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.14</version>
    </parent>
    
    <groupId>com.restaurant</groupId>
    <artifactId>menu-system</artifactId>
    <version>1.0.0</version>
    <name>Restaurant Menu System</name>
    
    <properties>
        <java.version>17</java.version>
    </properties>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>core</artifactId>
            <version>3.5.1</version>
        </dependency>
        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>javase</artifactId>
            <version>3.5.1</version>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>


3. *Copy all Java files* to their respective directories under src/main/java/com/restaurant/menu/

4. *Copy application.properties* to src/main/resources/

5. *Copy index.html* (the frontend) to src/main/resources/static/

6. *Build the project*:
bash
mvn clean install


7. *Run the application*:
bash
mvn spring-boot:run


Or run the JAR file:
bash
java -jar target/menu-system-1.0.0.jar


## Usage Guide

### Accessing the Application

1. *Main Application*: http://localhost:8080
2. *H2 Database Console*: http://localhost:8080/h2-console
   - JDBC URL: jdbc:h2:mem:restaurantdb
   - Username: sa
   - Password: (leave empty)

### Customer Flow

1. *Scan QR Code*: Customer scans the QR code at their table
2. *View Menu*: Menu opens automatically with the table number pre-filled
3. *Browse Items*: Filter by categories (Appetizers, Main Course, Desserts, etc.)
4. *Add to Cart*: Use +/- buttons to select quantities
5. *Place Order*: Click "View Cart" → Enter/confirm table number → "Place Order"

### Staff Operations

#### Managing Menu Items

1. Navigate to *"Staff - Manage Menu"* tab
2. Fill in the form:
   - Item Name
   - Description
   - Price
   - Category
3. Click *"Save Item"*
4. Existing items can be:
   - *Deleted*: Remove from menu
   - *Mark Unavailable*: Temporarily hide from customers

#### Viewing Orders

1. Navigate to *"Staff - View Orders"* tab
2. See all orders with:
   - Order ID and time
   - Table number
   - Items ordered
   - Current status
3. Update order status:
   - *Mark Preparing*: Kitchen is working on it
   - *Mark Completed*: Order ready/delivered

#### Generating QR Codes

1. Navigate to *"Staff - QR Codes"* tab
2. View QR codes for tables 1-20
3. Print or display QR codes at respective tables
4. Each QR code contains the table number

## API Endpoints

### Menu Management
- GET /api/menu - Get all menu items
- GET /api/menu/available - Get available items only
- GET /api/menu/category/{category} - Filter by category
- POST /api/menu - Create new menu item
- PUT /api/menu/{id} - Update menu item
- DELETE /api/menu/{id} - Delete menu item

### Order Management
- GET /api/orders - Get all orders
- GET /api/orders/table/{tableNumber} - Get orders by table
- GET /api/orders/status/{status} - Filter by status
- POST /api/orders - Create new order
- PUT /api/orders/{id}/status?status={status} - Update order status

### QR Code Generation
- GET /api/qrcode/generate/{tableNumber} - Generate QR code for specific table

## Sample Menu Data

You can pre-populate the menu using the API:

bash
# Add an appetizer
curl -X POST http://localhost:8080/api/menu \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Caesar Salad",
    "description": "Fresh romaine lettuce with parmesan cheese",
    "price": 8.99,
    "category": "Appetizers",
    "available": true
  }'

# Add a main course
curl -X POST http://localhost:8080/api/menu \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Grilled Salmon",
    "description": "Atlantic salmon with lemon butter sauce",
    "price": 24.99,
    "category": "Main Course",
    "available": true
  }'


## Customization

### Adding More Tables
In index.html, modify the generateQRCodes() function:
javascript
const tables = Array.from({length: 50}, (_, i) => i + 1); // Change to 50 tables


### Changing Categories
Modify the category dropdown in the frontend and ensure consistency in the backend.

### Production Database
Replace H2 with PostgreSQL or MySQL in application.properties:
properties
spring.datasource.url=jdbc:postgresql://localhost:5432/restaurantdb
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect


## Security Considerations

For production deployment:

1. *Add Authentication*: Implement Spring Security for staff pages
2. *HTTPS*: Use SSL certificates
3. *Database*: Use persistent database with backups
4. *Input Validation*: Add comprehensive validation
5. *Rate Limiting*: Prevent abuse of API endpoints

## Troubleshooting

*Port Already in Use*:
properties
# Change port in application.properties
server.port=8081


*CORS Issues*:
Already configured in the controllers with @CrossOrigin(origins = "*")

*Database Connection*:
Check H2 console to verify database is running and tables are created.

## Future Enhancements

- 📸 Image upload for menu items
- 💳 Payment integration
- 📧 Email/SMS order notifications
- 📊 Sales analytics dashboard
- 🌐 Multi-language support
- ⭐ Customer reviews and ratings
- 🎨 Theme customization per restaurant

## License

This project is open-source and available for educational and commercial use.

## Support

For issues or questions, please check:
- Spring Boot Documentation: https://spring.io/projects/spring-boot
- ZXing Documentation: https://github.com/zxing/zxing
