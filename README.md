# 🏨 Hostel Management System

[![Java](https://img.shields.io/badge/Java-17+-orange.svg)](https://www.oracle.com/java/)
[![Swing](https://img.shields.io/badge/GUI-Java%20Swing-blue.svg)](https://docs.oracle.com/javase/tutorial/uiswing/)
[![MySQL](https://img.shields.io/badge/Database-MySQL-blue.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A comprehensive desktop application for managing hostel operations, including student registration, room allocation, fee management, and user authentication. Built with Java Swing for an intuitive graphical interface and MySQL for robust data persistence.

---

## 📋 Table of Contents

- [Features](#-features)
- [Technologies Used](#-technologies-used)
- [System Architecture](#-system-architecture)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Database Setup](#-database-setup)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Screenshots](#-screenshots)
- [Database Schema](#-database-schema)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)
- [Contact](#-contact)

---

## ✨ Features

### 🔐 User Authentication
- **Secure Login System**: Username and password authentication with database validation
- **User Registration**: New student signup with auto-generated unique student IDs (S001, S002, etc.)
- **Password Management**: 
  - Password masking for security
  - Show/hide password toggle
  - Password confirmation validation
- **Forgot Password**: Password recovery option

### 🏠 Room Management
- **Add Rooms**: Create new room entries with room numbers and active status
- **Update Rooms**: Modify existing room information
- **Delete Rooms**: Remove rooms from the system
- **Search Functionality**: Quick room lookup by room number
- **Room Status**: Track room availability (Active/Inactive)
- **Real-time Data Display**: Table view showing all rooms with current status

### 👨‍🎓 Student Management
- **New Student Registration**: Comprehensive student information capture
  - Full name
  - Mobile number
  - Email address
  - Guardian name
  - Guardian telephone
  - Room number assignment
- **Data Validation**: Ensures all required fields are completed
- **Database Integration**: Automatic storage in MySQL database

### 💰 Student Fees Management
- **Fee Search**: Look up student fee details by mobile number
- **Fee Recording**: Track monthly fee payments
- **Student Information**: View complete student details including:
  - Name
  - Email
  - Room number
  - Month
  - Amount to be paid
- **Payment Tracking**: Record and manage fee payments

### 🎨 User Interface
- **Custom GUI Design**: Beautiful background images for each page
- **Intuitive Navigation**: Easy-to-use buttons and forms
- **Consistent Styling**: Uniform color scheme (#DA6E6E, #B04040, #9C8F85)
- **Responsive Layout**: Fixed-size windows optimized for 1300x800 resolution
- **Loading Screen**: Professional application startup with MVC pattern

---

## 🛠 Technologies Used

| Technology | Purpose | Version |
|------------|---------|---------|
| **Java** | Core programming language | 17+ |
| **Java Swing** | GUI framework | Built-in |
| **JDBC** | Database connectivity | Built-in |
| **MySQL** | Database management system | 8.0+ |
| **MVC Pattern** | Application architecture | - |

### Key Libraries
- `javax.swing.*` - GUI components
- `java.awt.*` - Graphics and layout
- `java.sql.*` - Database operations

---

## 🏗 System Architecture

The application follows the **Model-View-Controller (MVC)** architectural pattern:

```
┌─────────────────────────────────────────────────┐
│                    VIEW LAYER                    │
│  (FirstPage, LoginPage, Homepage, etc.)         │
└────────────────┬────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────┐
│                CONTROLLER LAYER                  │
│           (FirstPageController)                  │
└────────────────┬────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────┐
│                  MODEL LAYER                     │
│         (Database Operations via JDBC)           │
└────────────────┬────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────┐
│               DATABASE (MySQL)                   │
│    (studentmanagementsystem database)           │
└─────────────────────────────────────────────────┘
```

---

## 📦 Prerequisites

Before installing the Hostel Management System, ensure you have the following:

### Required Software
1. **Java Development Kit (JDK)**
   - Version: 17 or higher
   - Download: [Oracle JDK](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://openjdk.org/)

2. **MySQL Server**
   - Version: 8.0 or higher
   - Download: [MySQL Community Server](https://dev.mysql.com/downloads/mysql/)

3. **MySQL Connector/J (JDBC Driver)**
   - Version: 8.0+
   - Download: [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)

### Optional Tools
- **IDE**: Eclipse, IntelliJ IDEA, or NetBeans
- **MySQL Workbench**: For database management
- **Git**: For version control

---

## 🚀 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/Hostel-Management-System.git
cd Hostel-Management-System
```

### Step 2: Set Up MySQL JDBC Driver

1. Download the MySQL Connector/J JAR file
2. Add it to your project classpath:
   - **Eclipse**: Right-click project → Build Path → Add External Archives
   - **IntelliJ**: File → Project Structure → Libraries → Add
   - **Command Line**: Add to `CLASSPATH` environment variable

### Step 3: Configure Database Connection

Update the database connection details in the following files:
- `LoginPage.java`
- `Signuppage.java`
- `Manageroompage.java`
- `Newstudentpage.java`

```java
String url = "jdbc:mysql://localhost:3306/studentmanagementsystem";
String user = "root";
String password = "your_password"; // Update this
```

### Step 4: Update Image Paths

Update the image file paths in all view classes to match your system:

```java
// Example in FirstPage.java
backgroundImage = new ImageIcon("C:\\path\\to\\your\\images\\signup.jpg").getImage();
```

Or use relative paths:
```java
backgroundImage = new ImageIcon("images/signup.jpg").getImage();
```

### Step 5: Compile and Run

#### Using Command Line:
```bash
# Navigate to the src directory
cd EAD_CourseWork/src

# Compile all Java files
javac -d ../bin main/Main.java

# Run the application
java -cp ../bin main.Main
```

#### Using IDE:
1. Import the project into your IDE
2. Configure the build path
3. Run `Main.java` as Java Application

---

## 🗄 Database Setup

### Step 1: Create Database

Open MySQL command line or MySQL Workbench and execute:

```sql
CREATE DATABASE studentmanagementsystem;
USE studentmanagementsystem;
```

### Step 2: Create Tables

#### Students Table (Authentication)
```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id VARCHAR(10) UNIQUE NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Students1 Table (Student Information)
```sql
CREATE TABLE students1 (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    mobile_number VARCHAR(15) NOT NULL,
    email VARCHAR(100),
    guardian_name VARCHAR(100),
    guardian_tel VARCHAR(15),
    room_number VARCHAR(10),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Rooms Table
```sql
CREATE TABLE rooms (
    id INT AUTO_INCREMENT PRIMARY KEY,
    room_number VARCHAR(10) UNIQUE NOT NULL,
    active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

#### Fees Table (Optional Enhancement)
```sql
CREATE TABLE fees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    mobile_number VARCHAR(15),
    month VARCHAR(20),
    amount DECIMAL(10, 2),
    payment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (student_id) REFERENCES students1(id)
);
```

### Step 3: Insert Sample Data

```sql
-- Sample rooms
INSERT INTO rooms (room_number, active) VALUES 
('101', TRUE),
('102', TRUE),
('103', FALSE),
('201', TRUE),
('202', TRUE);

-- Sample admin user
INSERT INTO students (student_id, username, password) 
VALUES ('S001', 'admin', 'admin123');
```

---

## ⚙️ Configuration

### Database Configuration

Create a configuration file `config.properties` in the project root:

```properties
# Database Configuration
db.url=jdbc:mysql://localhost:3306/studentmanagementsystem
db.username=root
db.password=your_password
db.driver=com.mysql.cj.jdbc.Driver

# Application Settings
app.title=Hostel Management System
app.version=1.0.0
```

### Application Settings

Modify window dimensions and colors in respective view classes:

```java
// Window size
setSize(1300, 800);

// Button colors
Color primaryColor = new Color(0xDA6E6E);
Color secondaryColor = new Color(0xB04040);
Color tertiaryColor = new Color(0x9C8F85);
```

---

## 📖 Usage

### Starting the Application

1. **Launch**: Run `Main.java` from the `main` package
2. **Loading Screen**: Wait for the application to initialize
3. **Welcome Page**: Choose between Login or Sign Up

### User Registration (Sign Up)

1. Click **SIGN UP** button
2. System generates unique Student ID automatically (e.g., S001)
3. Enter username
4. Enter password
5. Confirm password
6. Click **NEXT >** to complete registration
7. You'll be redirected to Login page

### User Login

1. Click **LOGIN** button
2. Enter username
3. Enter password
4. Optional: Check "Show" to view password
5. Click **Login** button
6. Upon successful authentication, access the main dashboard

### Managing Rooms

1. From Homepage, click **Manage Room**
2. **Add New Room**:
   - Enter room number
   - Check "Active" if room is available
   - Click **Save**
3. **Update/Delete Room**:
   - Enter room number
   - Click **Search** to find the room
   - Modify active status
   - Click **Update** or **Delete**

### Adding New Students

1. From Homepage, click **New Student**
2. Fill in all required fields:
   - Name
   - Mobile Number
   - Email
   - Guardian Name
   - Guardian Telephone
   - Room Number
3. Click **Save**
4. Confirmation message appears on success

### Managing Student Fees

1. From Homepage, click **Student Fees**
2. Enter student's mobile number
3. Click **Search** to retrieve student details
4. Enter fee details:
   - Month
   - Amount to be paid
5. Click **Save** to record the payment

---

## 📁 Project Structure

```
Hostel-Management-System/
│
├── EAD_CourseWork/
│   ├── src/
│   │   ├── main/
│   │   │   └── Main.java                    # Application entry point
│   │   │
│   │   ├── controller/
│   │   │   └── FirstPageController.java     # MVC Controller
│   │   │
│   │   ├── view/
│   │   │   ├── FirstPage.java               # Welcome screen
│   │   │   ├── FirstPageView.java           # MVC View for first page
│   │   │   ├── LoginPage.java               # Login interface
│   │   │   ├── Loginpage2.java              # Alternative login view
│   │   │   ├── Signuppage.java              # Registration interface
│   │   │   ├── Homepage.java                # Main dashboard
│   │   │   ├── Manageroompage.java          # Room management
│   │   │   ├── Newstudentpage.java          # Student registration
│   │   │   └── Studentfeespage.java         # Fee management
│   │   │
│   │   ├── model/
│   │   │   └── PlaceholderModel.java        # Data models
│   │   │
│   │   ├── LoadingScreen/
│   │   │   ├── MainClass.java               # Loading screen entry
│   │   │   ├── LoadingControl.java          # Loading controller
│   │   │   ├── LoadingModel.java            # Loading model
│   │   │   └── LoadingView.java             # Loading view
│   │   │
│   │   └── module-info.java                 # Java module descriptor
│   │
│   ├── bin/                                  # Compiled classes
│   │   ├── controller/
│   │   ├── view/
│   │   ├── model/
│   │   ├── main/
│   │   └── LoadingScreen/
│   │
│   └── images/                               # Application images
│       ├── Home Page.png
│       ├── Login Page.png
│       ├── Manage Room.png
│       ├── New Student.png
│       ├── Sign Up.png
│       ├── signup.jpg
│       ├── student fee.png
│       └── Student Fees.png
│
├── README.md                                 # This file
├── LICENSE                                   # License information
└── .gitignore                                # Git ignore file
```

### Package Description

| Package | Description |
|---------|-------------|
| `main` | Application entry point |
| `controller` | MVC controllers for handling user actions |
| `view` | All GUI components and pages |
| `model` | Data models and business logic |
| `LoadingScreen` | Startup loading screen with MVC pattern |

---

## 🖼 Screenshots

### Welcome Screen
The first page where users can choose to login or sign up.

### Login Page
Secure authentication with password visibility toggle.

### Sign Up Page
User registration with auto-generated student IDs and password confirmation.

### Homepage Dashboard
Main navigation hub with three primary functions:
- Manage Room
- New Student
- Student Fees

### Manage Room Page
Comprehensive room management with CRUD operations and table display.

### New Student Page
Student registration form with all necessary fields for enrollment.

### Student Fees Page
Fee management interface for searching students and recording payments.

---

## 📊 Database Schema

### Entity Relationship Diagram

```
┌──────────────────┐         ┌──────────────────┐
│    students      │         │    students1     │
├──────────────────┤         ├──────────────────┤
│ id (PK)          │         │ id (PK)          │
│ student_id       │         │ name             │
│ username         │         │ mobile_number    │
│ password         │         │ email            │
│ created_at       │         │ guardian_name    │
└──────────────────┘         │ guardian_tel     │
                             │ room_number (FK) │
                             │ created_at       │
                             └──────────────────┘
                                      │
                                      │
                             ┌────────▼─────────┐
                             │      rooms       │
                             ├──────────────────┤
                             │ id (PK)          │
                             │ room_number      │
                             │ active           │
                             │ created_at       │
                             │ updated_at       │
                             └──────────────────┘
```

### Table Relationships
- `students1.room_number` references `rooms.room_number` (conceptual FK)
- Separate `students` table for authentication
- `students1` table for detailed student information

---

## 🤝 Contributing

We welcome contributions to improve the Hostel Management System! Here's how you can help:

### How to Contribute

1. **Fork the Repository**
   ```bash
   git clone https://github.com/yourusername/Hostel-Management-System.git
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```

3. **Make Your Changes**
   - Write clean, documented code
   - Follow existing code style
   - Add comments where necessary

4. **Commit Your Changes**
   ```bash
   git commit -m "Add some AmazingFeature"
   ```

5. **Push to the Branch**
   ```bash
   git push origin feature/AmazingFeature
   ```

6. **Open a Pull Request**
   - Describe your changes
   - Reference any related issues

### Contribution Guidelines

- Follow Java naming conventions
- Maintain MVC architecture pattern
- Test all database operations
- Update documentation as needed
- Ensure code compiles without errors
- Add comments for complex logic

### Areas for Contribution

- 🐛 Bug fixes
- ✨ New features
- 📝 Documentation improvements
- 🎨 UI/UX enhancements
- 🔒 Security improvements
- ⚡ Performance optimization

---

## 🔧 Troubleshooting

### Common Issues and Solutions

#### 1. Database Connection Error

**Problem**: `SQLException: Access denied for user 'root'@'localhost'`

**Solution**:
- Verify MySQL server is running
- Check username and password in code
- Ensure database exists: `SHOW DATABASES;`
- Grant privileges: `GRANT ALL PRIVILEGES ON studentmanagementsystem.* TO 'root'@'localhost';`

#### 2. JDBC Driver Not Found

**Problem**: `ClassNotFoundException: com.mysql.cj.jdbc.Driver`

**Solution**:
- Download MySQL Connector/J
- Add JAR to classpath
- Verify JAR is in build path

#### 3. Images Not Loading

**Problem**: Background images don't appear

**Solution**:
- Check image file paths
- Use absolute paths or place images in accessible location
- Verify image file names match code
- Use forward slashes or double backslashes in paths:
  ```java
  "C:\\Users\\...\\images\\image.png"
  // or
  "C:/Users/.../images/image.png"
  ```

#### 4. Table Not Found Error

**Problem**: `SQLException: Table 'studentmanagementsystem.students' doesn't exist`

**Solution**:
- Run all CREATE TABLE statements
- Verify correct database is selected: `USE studentmanagementsystem;`
- Check table names match code exactly (case-sensitive on Linux)

#### 5. Window Too Large/Small

**Problem**: Application window doesn't fit screen

**Solution**:
- Modify `setSize()` in each view class
- Adjust component positions proportionally
- Consider making layout responsive

#### 6. Duplicate Entry Error

**Problem**: `SQLException: Duplicate entry for key 'username'`

**Solution**:
- Usernames must be unique
- Check if username already exists before signup
- Add validation in signup form

---

## 🚀 Future Enhancements

### Planned Features

#### Version 2.0
- [ ] **Password Encryption**: Implement BCrypt or SHA-256 hashing
- [ ] **Session Management**: Track logged-in users and timeout
- [ ] **Role-Based Access**: Admin, Manager, and Student roles
- [ ] **Search and Filter**: Advanced search across all modules
- [ ] **Reports Generation**: PDF reports for fees, occupancy, etc.

#### Version 2.5
- [ ] **Email Notifications**: Automated reminders for fee payments
- [ ] **Payment Gateway Integration**: Online fee payment
- [ ] **Backup and Restore**: Database backup functionality
- [ ] **Audit Logs**: Track all system changes
- [ ] **Dashboard Analytics**: Charts and statistics

#### Version 3.0
- [ ] **Mobile App**: Android/iOS companion app
- [ ] **Cloud Integration**: Cloud database support (AWS RDS, Azure)
- [ ] **Multi-hostel Support**: Manage multiple hostels
- [ ] **Biometric Integration**: Fingerprint authentication
- [ ] **QR Code Generation**: For student identification

### Technical Improvements
- [ ] Migrate to JavaFX for modern UI
- [ ] Implement DAO pattern for database operations
- [ ] Add unit tests (JUnit)
- [ ] Configuration file support
- [ ] Logging framework (Log4j)
- [ ] Connection pooling (HikariCP)
- [ ] Input validation framework
- [ ] Internationalization (i18n)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Hostel Management System Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 📞 Contact

### Project Maintainer

**Project Link**: [https://github.com/sadinsa07/Hostel-Management-System](https://github.com/sadinsa07/Hostel-Management-System)

### Support

For issues, questions, or suggestions:
- 📧 **Email**: sadinsawarangani@gmail.com
- 🐛 **Bug Reports**: [GitHub Issues](https://github.com/sadinsa07/Hostel-Management-System/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/sadinsa07/Hostel-Management-System/discussions)
- 📖 **Documentation**: [Wiki](https://github.com/sadinsa07/Hostel-Management-System/wiki)



---

## 🙏 Acknowledgments

- **Java Documentation**: Oracle Java tutorials and documentation
- **MySQL**: For providing excellent database management system
- **Community**: Thanks to all contributors and users
- **Stack Overflow**: For troubleshooting assistance
- **GitHub**: For hosting and version control

---

## 📚 Additional Resources

### Learning Resources
- [Java Swing Tutorial](https://docs.oracle.com/javase/tutorial/uiswing/)
- [JDBC Tutorial](https://docs.oracle.com/javase/tutorial/jdbc/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [MVC Pattern](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)

### Related Projects
- [Student Management System](https://github.com/topics/student-management)
- [Hostel Management](https://github.com/topics/hostel-management)
- [Java Desktop Applications](https://github.com/topics/java-swing)

---

## 📊 Project Statistics

- **Language**: Java
- **GUI Framework**: Swing
- **Database**: MySQL
- **Architecture**: MVC
- **Lines of Code**: ~2000+
- **Classes**: 15+
- **Database Tables**: 3+

---

## 🎯 Project Status

![Status](https://img.shields.io/badge/Status-Active-success)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![Maintenance](https://img.shields.io/badge/Maintained-Yes-green)

**Current Version**: 1.0.0  
**Last Updated**: December 2025  
**Status**: Active Development

---

<div align="center">

### ⭐ Star this repository if you find it helpful!

**Made with ❤️ for better hostel management**

[⬆ Back to Top](#-hostel-management-system)

</div>
