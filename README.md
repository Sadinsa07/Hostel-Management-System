# Hostel Management System 

[![Java](https://img.shields.io/badge/Java-11%2B-blue.svg)](https://www.oracle.com/java/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![Swing](https://img.shields.io/badge/Swing-GUI-orange.svg)](https://docs.oracle.com/javase/8/docs/technotes/guides/swing/)
[![GUI](https://img.shields.io/badge/GUI-Swing-lightgrey.svg)](https://docs.oracle.com/javase/8/docs/technotes/guides/swing/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A feature-rich Java Swing desktop application for managing hostel students, rooms, and fees — built during the EAD coursework. 
---

## 📋 Table of Contents

- [Features](#features)
- [Screenshots](#screenshots)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Configuration](#configuration--tips)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Security & Best Practices](#security--best-practices)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact--author)

---

## 🚀 Project Overview

This application provides a GUI for hostel management including:
- Student Sign Up & Login
- Add / Manage hostel rooms
- Add and manage student details (personal & guardian contact info)
- Record / view student fee data

The UI is built using Java Swing and the app performs DB CRUD operations using `java.sql`/JDBC to a MySQL database.

---

## ✨ Key Features

- User Authentication (Login) using MySQL DB (plain-text passwords in current code; see Security section)
- Admin-styled pages: Manage room, New Student, Student Fees
- Simple MVC architecture (controllers in `controller/`, views in `view/`, models in `model/`)
- Background images for UI screens (images in `EAD_CourseWork/images/`)

---

## 🧭 Project Structure

```
Hostel-Management-System-main/
  EAD_CourseWork/
    src/
      controller/       # Controllers (action listeners)
      view/             # Swing UI screens
      model/            # Data Models (placeholder)
      main/             # Main class to start app
    images/             # Background & UI images
    bin/                # Compiled class files (if used)
```

---

## ⚙️ Requirements

- Java 11 or higher (JDK) — module-info.java is included
- MySQL Server (or compatible) — used for backend DB
- MySQL Connector/J (JDBC driver jar) added to your classpath or module path
- IDE such as IntelliJ IDEA / Eclipse / NetBeans or CLI build tools

---

## 🛠️ Database Setup

The app expects a MySQL database named `studentmanagementsystem` with the following minimal tables:

```sql
CREATE DATABASE IF NOT EXISTS studentmanagementsystem;
USE studentmanagementsystem;

CREATE TABLE IF NOT EXISTS students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  student_id VARCHAR(10),
  username VARCHAR(100),
  password VARCHAR(255)
);

CREATE TABLE IF NOT EXISTS students1 (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  mobile_number VARCHAR(50),
  email VARCHAR(255),
  guardian_name VARCHAR(255),
  guardian_tel VARCHAR(50),
  room_number VARCHAR(50)
);

CREATE TABLE IF NOT EXISTS rooms (
  id INT AUTO_INCREMENT PRIMARY KEY,
  room_number VARCHAR(50),
  active BOOLEAN DEFAULT FALSE
);
```

- Default DB connection credentials in code are: `root`/`(empty password)` connecting to `jdbc:mysql://localhost:3306/studentmanagementsystem`.
- Update the credentials in the following files to match your environment (or set environment variables and update code accordingly): `LoginPage.java`, `Signuppage.java`, `Newstudentpage.java`, and `Manageroompage.java`.

---

## 🔧 Configuration — Tips

- The SQL schema file is included at `EAD_CourseWork/db/schema.sql`. Use a MySQL client or `mysql` command-line tool to import it:

```powershell
mysql -u root -p < EAD_CourseWork\db\schema.sql
```

- Move DB settings into a `config.properties` and read them at startup (recommended) instead of hard-coding credentials in the Java files.
- Replace absolute image paths with resource loading; move images to `src/main/resources/images/` and update view code to use:

```java
new ImageIcon(getClass().getResource("/images/Login Page.png"));
```


## 🔧 Quick Setup & Run (IDE Recommended)

The easiest way to run the application is via an IDE — import the project as a Java project.

Steps (using IntelliJ/Eclipse/NetBeans):
1. Import or open the folder `EAD_CourseWork` as a Java project.
2. Add the MySQL Connector/J jar to the project's classpath or module path.
   - Download from: https://dev.mysql.com/downloads/connector/j/
   - Add as a library/dependency in your IDE.
3. Ensure Java 11+ is set as the project SDK and that module settings allow `EAD_CourseWork` to compile.
4. Update DB credentials and (optionally) image paths as described below.
5. Run `main.Main` (found at `EAD_CourseWork/src/main/Main.java`)

---

## 🏁 Build & Run (Command Line)

Note: Because `module-info.java` is present, the project uses the module system introduced in Java 9+. CLI commands below assume a simple `javac` compilation and running with correct module path references.

1. Open a terminal at the `EAD_CourseWork` folder

Windows PowerShell example (adapt the paths for your environment):

```powershell
# Create bin directory
mkdir bin

# Compile all Java files into bin (PowerShell example)
$files = Get-ChildItem -Path .\src -Recurse -Filter *.java | ForEach-Object {$_.FullName}
javac -d bin --module-source-path src @($files)

# Run (add MySQL connector to module path or classpath)
# Replace "path\to\mysql-connector-java.jar" with your jar path
$driverPath = 'C:\path\to\mysql-connector-java-8.0.xx.jar'
java --module-path "$driverPath;bin" --module EAD_CourseWork/main.Main
```

If you prefer packaging into a fat JAR, use a build tool like Gradle or Maven and include the MySQL Connector as a dependency. Instructions for packaging via Maven/Gradle are in the next section.

---

## 📦 (Optional) Maven/Gradle Setup

This repository doesn't include Maven or Gradle configs; if you prefer automation, create the following minimal setup:

- Add `mysql-connector-java` as a dependency
- Configure the main class as `main.Main`
- Include images in `resources/` and access them with `getResource()` to pack into the JAR

If you'd like, I can add a `pom.xml` or `build.gradle` for you — tell me whether you prefer Maven or Gradle.

---

## 📸 Screenshots

You can find UI images in `EAD_CourseWork/images/`. These images are used by the views for backgrounds. Consider changing to relative (project-local) paths or using classpath resource loading.

Example:
- `EAD_CourseWork/images/Login Page.png`
- `EAD_CourseWork/images/Sign Up.png`
- `EAD_CourseWork/images/Home Page.png`

To include images in a packaged JAR, move them to `src/main/resources/images/` and load them with `getResource("/images/Name.png")`.

---

## ✅ Notes, Best Practices & Suggestions

- Security: Passwords are currently stored in plaintext in the database. Use salted hashing (e.g., BCrypt) to store passwords securely, and never store raw passwords in code or in DB.
- SQL & DB: Use connection pooling for production and move DB credentials to a configuration file or environment variables.
- Code Quality: Consider refactoring to: 
  - Proper DAO/Repository layer
  - Exception handling with logging
  - Unit tests
  - Avoid absolute paths for images; use resource paths instead
- UI: Consider upgrading from Swing to JavaFX for richer UI and better resource handling.

---

## 💡 Common Troubleshooting

- ClassNotFoundException (com.mysql.cj.jdbc.Driver): Make sure mysql-connector-java jar is added to module/classpath.
- Images not loading: Replace absolute paths with relative resource loading. E.g. `new ImageIcon(getClass().getResource("/images/Your.png"))`.
- DB connection error: Ensure MySQL is running and the database `studentmanagementsystem` exists, plus username/password are correct.

---

## 🤝 Contributing

Contributions are welcome! To contribute:
1. Fork the repository
2. Create a feature branch
3. Make changes, add tests if possible, and update this README if applicable
4. Create a pull request with a clear message of what you changed and why

If you'd like help converting the project to a Maven/Gradle build or to add tests/CI, I can help implement that.

---

## 📝 License

This template README suggests a permissive license such as MIT. If you are the repository owner and would like to place a license, add a `LICENSE` file or let me know what license you prefer.

---

## 📬 Contact 

If you want more help improving this project (e.g., converting to Maven/Gradle, refactoring, modularizing, or adding tests), tell me what you'd like and I can implement the changes.

---

Thanks for building this project — it's a great starting point for a fully-featured hostel management system! ✅
