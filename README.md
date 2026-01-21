# Bank Management System

A secure and user-friendly Bank Management System built with Java and MySQL, featuring a modern graphical user interface for seamless banking operations.

## Features

- **User Authentication**
  - Secure login with card number and PIN
  - Multi-step account signup process
  - PIN management system

- **Account Management**
  - Balance inquiry
  - Cash deposits and withdrawals
  - Fast cash transactions
  - Mini statements

- **Security**
  - Secure PIN-based authentication
  - Protected database connections
  - Input validation

## Technologies Used

- **Frontend**: Java Swing (AWT)
- **Backend**: Java
- **Database**: MySQL
- **Development Tools**: IntelliJ IDEA (or any Java IDE)

## Prerequisites

- Java Development Kit (JDK) 8 or later
- MySQL Server 5.7 or later
- MySQL Connector/J (JDBC driver)
- Git (optional, for version control)

## Database Schema

The system uses a relational database with the following tables:

### 1. `login` - User Authentication
```sql
CREATE TABLE login (
    formno VARCHAR(20) PRIMARY KEY,
    card_number VARCHAR(16) NOT NULL UNIQUE,
    pin VARCHAR(4) NOT NULL
);
```

### 2. `signup` - User Personal Information
```sql
CREATE TABLE signup (
    formno VARCHAR(20) PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    father_name VARCHAR(100) NOT NULL,
    dob DATE NOT NULL,
    gender VARCHAR(10) NOT NULL,
    email VARCHAR(100) NOT NULL,
    marital_status VARCHAR(20) NOT NULL,
    address TEXT NOT NULL,
    city VARCHAR(50) NOT NULL,
    pincode VARCHAR(10) NOT NULL,
    state VARCHAR(50) NOT NULL
);
```

### 3. `signuptwo` - Additional User Information
```sql
CREATE TABLE signuptwo (
    formno VARCHAR(20) PRIMARY KEY,
    religion VARCHAR(50) NOT NULL,
    category VARCHAR(50) NOT NULL,
    income VARCHAR(50) NOT NULL,
    education VARCHAR(100) NOT NULL,
    occupation VARCHAR(100) NOT NULL,
    pan VARCHAR(20) NOT NULL,
    aadhar VARCHAR(20) NOT NULL,
    senior_citizen BOOLEAN NOT NULL,
    existing_account BOOLEAN NOT NULL
);
```

### 4. `signupthree` - Account Details
```sql
CREATE TABLE signupthree (
    formno VARCHAR(20) PRIMARY KEY,
    account_type VARCHAR(50) NOT NULL,
    card_number VARCHAR(16) NOT NULL,
    pin VARCHAR(4) NOT NULL,
    facility VARCHAR(255) NOT NULL
);
```

### 5. `bank` - Transaction Records
```sql
CREATE TABLE bank (
    pin VARCHAR(4) NOT NULL,
    date DATETIME NOT NULL,
    type VARCHAR(50) NOT NULL,
    amount DECIMAL(15, 2) NOT NULL,
    FOREIGN KEY (pin) REFERENCES login(pin)
);
```

## Setup Instructions

### 1. Database Setup

1. Install MySQL Server if not already installed
2. Create a new database and user:
   ```sql
   CREATE DATABASE bankmanagementsystem;
   USE bankmanagementsystem;
   CREATE USER 'bankuser'@'localhost' IDENTIFIED BY 'your_secure_password';
   GRANT ALL PRIVILEGES ON bankmanagementsystem.* TO 'bankuser'@'localhost';
   FLUSH PRIVILEGES;
   ```
3. Create the tables using the schema provided above

### 2. Project Setup

1. Clone the repository:
   ```bash
   git clone [your-repository-url]
   cd Bank-Management-System
   ```

2. Import the project into your Java IDE (IntelliJ IDEA recommended)

3. Add MySQL Connector/J to your project:
   - Download the latest MySQL Connector/J from [MySQL website](https://dev.mysql.com/downloads/connector/j/)
   - Add the JAR file to your project's build path

4. Configure the database connection in `Connn.java`:
   ```java
   // Update this line in Connn.java
   connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/bankmanagementsystem", "bankuser", "your_secure_password");
   ```

### 3. Running the Application

1. Compile and run the `main_Class.java` file
2. The application will launch with a login screen
3. New users can register through the signup process

## Project Structure

```
src/
└── bank/
    └── management/
        └── system/
            ├── BalanceEnquriy.java    # Balance inquiry functionality
            ├── Connn.java             # Database connection handler
            ├── Deposit.java           # Deposit transaction handling
            ├── FastCash.java          # Fast cash withdrawal
            ├── Login.java             # Login screen
            ├── Pin.java               # PIN management
            ├── Signup.java            # Signup process (part 1)
            ├── Signup2.java           # Signup process (part 2)
            ├── Signup3.java           # Signup process (part 3)
            ├── Withdrawl.java         # Withdrawal functionality
            ├── main_Class.java        # Main application window
            └── mini.java              # Mini statement generation
```

## OOP Concepts Implemented

1. **Encapsulation**
   - Private class members with public getters/setters
   - Data hiding through access modifiers

2. **Inheritance**
   - Classes extend JFrame for GUI components
   - Implementation of ActionListener for event handling

3. **Polymorphism**
   - Method overriding in event handling
   - Interface implementation (ActionListener)

4. **Abstraction**
   - Abstract classes for common functionality
   - Interface usage for event handling

