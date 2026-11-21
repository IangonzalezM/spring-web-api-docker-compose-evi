# Student Management System - REST API

A Spring Boot RESTful API for managing student records with full CRUD operations. Built with Spring Data JPA, Hibernate, and MySQL database.

---

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
- [Testing with Postman](#testing-with-postman)
- [Postman Setup Guide](#postman-setup-guide)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## ✨ Features

- ✅ **Create** - Add new student records
- ✅ **Read** - Retrieve all students or search by ID/Name
- ✅ **Update** - Modify student details (full & partial updates)
- ✅ **Delete** - Remove student records
- ✅ **MySQL Database** - Persistent data storage with automatic schema management
- ✅ **RESTful API** - Standard HTTP methods and status codes
- ✅ **Error Handling** - Comprehensive exception management
- ✅ **Hot Reload** - Spring DevTools for faster development
- ✅ **Postman Ready** - All endpoints Postman-tested and documented

---

## 🛠️ Tech Stack

| Component | Version | Purpose |
|-----------|---------|---------|
| **Java** | 25 | Programming language |
| **Spring Boot** | 4.0.2 | Application framework |
| **Spring Data JPA** | Latest | ORM & Database access |
| **Hibernate** | Latest | JPA implementation |
| **MySQL** | 8.0+ | Database |
| **Lombok** | Latest | Reduce boilerplate code |
| **Maven** | 3.6+ | Build tool |
| **Postman** | Latest | API Testing Tool |

---

## 📦 Prerequisites
**Before you begin, ensure you have the following installed:**
**Docker Desktop:**
- docker --version
- docker compose version

**Git:**
- git --version

**Maven**
- mvn --version
- mvn clean package -DskipTests

---

## 🚀 Installation
### Step 1: Clone the Repository
- git clone https://github.com/IangonzalezM/spring-web-api-docker-compose-evi.git
- cd spring-web-api-docker-compose-evi/sbapp11
### Step 2: Create Environment File
**Copy:**
- .env.example 
- to:
- .env 
- and customize the database credentials if required.
**Example:**
- DB_URL=jdbc:mysql://mysql:3306/EVITest
- DB_USER=root
- DB_PASSWORD=root
- MYSQL_DATABASE=EVITest
- MYSQL_ROOT_PASSWORD=root
### Step 3: Build the Application
- mvn clean package -DskipTests
### Step 4: Build Docker Image
- docker build -t evitest-api .
### Step 5: Start the Environment
- docker compose up -d
### Step 6: Verify Containers
- docker ps
**Expected containers:**
- mysql-evitest
- evitest-app
### Step 7: Access the API
http://localhost:4455/api/v1/getStudent12

---
### 🐳 Docker Environment
**The project uses Docker Compose to orchestrate:**

- Spring Boot REST API
- MySQL 8 Database
- Persistent Docker Volume
- Start
- docker compose up -d
- View Logs
- docker compose logs -f
- Stop Containers
- docker compose down
- Remove Containers and Database Volume
- docker compose down -v
- Rebuild Everything
- mvn clean package -DskipTests
- docker build --no-cache -t evitest-api .
- docker compose up -d

---

## ⚙️ Configuration

### Application Properties
File: `src/main/resources/application.properties`

```properties
**Server Configuration**
- server.port=4455

**Database Connection**
- spring.datasource.url=${DB_URL}
- spring.datasource.username=${DB_USER}
- spring.datasource.password=${DB_PASSWORD}

**JPA/Hibernate Configuration**
- spring.jpa.hibernate.ddl-auto=update
- spring.jpa.show-sql=true
```

**Options for `ddl-auto`:**
- `create` - Drop and recreate tables on startup
- `create-drop` - Drop tables on shutdown
- `update` - Update schema without dropping data *(Recommended)*
- `validate` - Validate schema without making changes

---

## 🔌 API Endpoints

**Base URL:** `http://localhost:4455/api/v1`

### 1️⃣ Get All Students
```
GET /getStudent12
```
**Description:** Retrieve all student records from the database

**Headers:**
```
Content-Type: application/json
```

**Response:** `200 OK`
```json
[
  {
    "sid": 1,
    "regdno": 123,
    "name": "John Doe",
    "contact": 9876543210
  },
  {
    "sid": 2,
    "regdno": 456,
    "name": "Jane Smith",
    "contact": 9876543211
  }
]
```

---

### 2️⃣ Get Student by ID
```
GET /getStud/{sid}
```
**Description:** Retrieve a specific student by Student ID

**URL Example:** `http://localhost:4455/api/v1/getStud/52`

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| sid | integer | Yes | Student ID |

**Response:** `200 OK`
```json
{
  "sid": 52,
  "regdno": 456,
  "name": "Jane Smith",
  "contact": 9876543211
}
```

**Error Response:** `404 Not Found`
```json
{
  "error": "Student not found",
  "status": 404
}
```

---

### 3️⃣ Get Student by Name
```
GET /getst/{name}
```
**Description:** Retrieve a student record by name

**URL Example:** `http://localhost:4455/api/v1/getst/Ashish`

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | string | Yes | Student name |

**Response:** `200 OK`
```json
{
  "sid": 10,
  "regdno": 789,
  "name": "Ashish",
  "contact": 9876543212
}
```

---

### 4️⃣ Create New Student
```
POST /insertStudent12
```
**Description:** Add a new student record to the database

**Headers:**
```
Content-Type: application/json
```

**Request Body:**
```json
{
  "regdno": 101,
  "name": "Rahul Sharma",
  "contact": 9876543213
}
```

**Response:** `201 Created`
```json
{
  "sid": 15,
  "regdno": 101,
  "name": "Rahul Sharma",
  "contact": 9876543213
}
```

---

### 5️⃣ Update Student (Complete Update)
```
POST /updateStudent12/{sid}
```
**Description:** Update all fields of an existing student

**URL Example:** `http://localhost:4455/api/v1/updateStudent12/52`

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| sid | integer | Yes | Student ID to update |

**Headers:**
```
Content-Type: application/json
```

**Request Body:**
```json
{
  "regdno": 999,
  "name": "Jane Updated",
  "contact": 9876543220
}
```

**Response:** `200 OK`
```json
{
  "sid": 52,
  "regdno": 999,
  "name": "Jane Updated",
  "contact": 9876543220
}
```

---

### 6️⃣ Update Student (Partial Update)
```
PATCH /patchStudent/{sid}
```
**Description:** Update specific fields of a student record

**URL Example:** `http://localhost:4455/api/v1/patchStudent/52`

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| sid | integer | Yes | Student ID to update |

**Headers:**
```
Content-Type: application/json
```

**Request Body:** (Only update registration number)
```json
{
  "regdno": 500
}
```

**Response:** `200 OK`
```json
{
  "sid": 52,
  "regdno": 500,
  "name": "Jane Updated",
  "contact": 9876543220
}
```

---

### 7️⃣ Delete Student
```
DELETE /deleteStudent12/{sid}
```
**Description:** Remove a student record from the database

**URL Example:** `http://localhost:4455/api/v1/deleteStudent12/4`

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| sid | integer | Yes | Student ID to delete |

**Response:** `200 OK`
```json
"Student details has been removed successsfully based on id 4"
```

---

## 🧪 Testing with Postman

### Postman Environment Setup

**Step 1: Create an Environment**
1. Open Postman
2. Click **Environments** → **Create new environment**
3. Name it: `Student API Local`
4. Add these variables:

| Variable | Value | Type |
|----------|-------|------|
| base_url | http://localhost:4455/api/v1 | string |
| sid | 52 | number |
| name | Ashish | string |

**Step 2: Save the environment**

---

## 📮 Postman Setup Guide

### Method 1: Create Requests Manually

#### Request 1: Get All Students
1. **Click** `New` → `Request`
2. **Name:** `Get All Students`
3. **Method:** `GET`
4. **URL:** `{{base_url}}/getStudent12`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Click** `Send`

#### Request 2: Get Student by ID
1. **Click** `New` → `Request`
2. **Name:** `Get Student by ID`
3. **Method:** `GET`
4. **URL:** `{{base_url}}/getStud/{{sid}}`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Click** `Send`

#### Request 3: Create Student
1. **Click** `New` → `Request`
2. **Name:** `Create Student`
3. **Method:** `POST`
4. **URL:** `{{base_url}}/insertStudent12`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Body** → `raw` → `JSON`:
```json
{
  "regdno": 102,
  "name": "Priya Singh",
  "contact": 9876543214
}
```
7. **Click** `Send`

#### Request 4: Update Student
1. **Click** `New` → `Request`
2. **Name:** `Update Student`
3. **Method:** `POST`
4. **URL:** `{{base_url}}/updateStudent12/{{sid}}`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Body** → `raw` → `JSON`:
```json
{
  "regdno": 600,
  "name": "Jane Updated",
  "contact": 9876543221
}
```
7. **Click** `Send`

#### Request 5: Partial Update Student
1. **Click** `New` → `Request`
2. **Name:** `Patch Student`
3. **Method:** `PATCH`
4. **URL:** `{{base_url}}/patchStudent/{{sid}}`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Body** → `raw` → `JSON`:
```json
{
  "regdno": 700
}
```
7. **Click** `Send`

#### Request 6: Delete Student
1. **Click** `New` → `Request`
2. **Name:** `Delete Student`
3. **Method:** `DELETE`
4. **URL:** `{{base_url}}/deleteStudent12/{{sid}}`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Click** `Send`

#### Request 7: Get Student by Name
1. **Click** `New` → `Request`
2. **Name:** `Get Student by Name`
3. **Method:** `GET`
4. **URL:** `{{base_url}}/getst/{{name}}`
5. **Headers:** 
   - `Content-Type: application/json`
6. **Click** `Send`

---

### Method 2: Create a Postman Collection

**Step 1: Create Collection**
1. Click `Collections` → `New Collection`
2. Name: `Student Management API`
3. Save

**Step 2: Add Requests to Collection**
1. Right-click collection → `Add Request`
2. Create each request as shown above
3. Save all requests

**Step 3: Run Collection**
1. Click the collection name
2. Click `Run` button
3. Select environment: `Student API Local`
4. Click `Run Student Management API`

---

### Postman Testing Workflow

**Complete Test Flow:**

```
1. GET /getStudent12
   ↓ (View all students)
   
2. POST /insertStudent12
   ↓ (Create new student, note the returned sid)
   
3. GET /getStud/{sid}
   ↓ (Verify student was created)
   
4. GET /getst/{name}
   ↓ (Search by name)
   
5. POST /updateStudent12/{sid}
   ↓ (Update student details)
   
6. PATCH /patchStudent/{sid}
   ↓ (Partial update)
   
7. GET /getStudent12
   ↓ (View all students again)
   
8. DELETE /deleteStudent12/{sid}
   ↓ (Delete the student)
   
9. GET /getStudent12
   ↓ (Verify student was deleted)
```

---

### Postman Tips & Tricks

**💡 Tip 1: Use Variables**
```
Save response value as variable:
1. In response, select JSON value
2. Right-click → Set as variable
3. Choose environment
```

**💡 Tip 2: Save Response**
```
1. After getting response
2. Click "Save response" button
3. Name it for future reference
```

**💡 Tip 3: Add Tests to Requests**
```javascript
// Go to Tests tab and add:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is valid JSON", function () {
    pm.response.to.be.json;
});
```

**💡 Tip 4: Pre-request Scripts**
```javascript
// Go to Pre-request Script tab:
pm.environment.set("timestamp", new Date().getTime());
```

---

## 📁 Project Structure

```
spring-web-api-docker-compose-evi/
│
└── sbapp11/
    ├── src/
    │   ├── main/
    │   │   ├── java/com/vcube/sbapp11/
    │   │   │   ├── Sbapp11Application.java          (Entry point)
    │   │   │   ├── Controller/
    │   │   │   │   └── StuControl.java              (REST endpoints)
    │   │   │   ├── model/
    │   │   │   │   └── Student12.java               (Entity model)
    │   │   │   └── Repo/
    │   │   │       └── StudenRepo.java              (Database interface)
    │   │   └── resources/
    │   │       └── application.properties           (Configuration)
    │   │
    │   └── test/
    │       └── java/com/vcube/sbapp11/
    │           └── Sbapp11ApplicationTests.java     (Unit tests)
    │
    ├── pom.xml                                      (Maven dependencies)
    ├── mvnw / mvnw.cmd                              (Maven wrapper)
    └── HELP.md                                      (Spring Boot help)
```

---

## 🗄️ Database Schema

### Student1 Table

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| `sid` | INT | PRIMARY KEY, AUTO_INCREMENT | Student ID |
| `regdno` | INT | - | Registration Number |
| `name` | VARCHAR(255) | - | Student Name |
| `contact` | BIGINT | - | Contact Phone Number |

### Sample Data
```sql
INSERT INTO Student1 (regdno, name, contact) VALUES
(123, 'John Doe', 9876543210),
(456, 'Jane Smith', 9876543211),
(789, 'Ashish Kumar', 9876543212);
```

---

## 🐛 Troubleshooting

### Issue 1: Connection Refused (Postman)
```
Error: Connection refused
```
**Solution:**
- Verify server is running: `docker compose up -d`
- Check port 4455 is accessible
- In Postman, confirm base URL: `http://localhost:4455/api/v1`

### Issue 2: MySQL Connection Error
- com.mysql.cj.jdbc.exceptions.CommunicationsException
**Possible Solutions**
- 1. Verify that Docker containers are running:
- docker ps
**Expected containers:**
- mysql-evitest
- evitest-app

- 2. Verify Docker Compose status:
- docker compose ps

- 3. Review application logs:
- docker compose logs -f

- 4. Verify environment variables in .env:
- DB_URL=jdbc:mysql://mysql:3306/EVITest
- DB_USER=root
- DB_PASSWORD=your_password

- 5. Restart the environment:
- docker compose down
- docker compose up -d

- 6. If the database volume became corrupted:
- docker compose down -v
- docker compose up -d
⚠️ This removes all persisted database data.

### Issue 4: Student Not Found (404)
**Solution:**
- Verify the student ID exists
- Check database: `SELECT * FROM Student1;`
- Create a student first before updating

### Issue 5: Invalid JSON in Postman
**Solution:**
- Ensure `Content-Type: application/json` header is set
- Validate JSON syntax at: https://jsonlint.com/
- Check for trailing commas or missing quotes

---

## 📝 Key Classes

### **Sbapp11Application.java**
- Spring Boot application entry point
- Starts the embedded Tomcat server on port 4455

### **StuControl.java**
- REST Controller handling all HTTP requests
- Maps endpoints to business logic
- Manages CRUD operations

### **Student12.java**
- Entity class representing Student database table
- Uses JPA annotations for ORM mapping
- Contains properties: sid, regdno, name, contact

### **StudenRepo.java**
- Data Access Object (DAO) interface
- Extends JpaRepository for CRUD operations
- Custom method: `findByname(String name)`

---

## 🔒 Security Notes
- ⚠️ Important for Production

- Change Default Credentials
- Do not use the default credentials provided in .env.example.

- Update the following values in your .env file:

- DB_PASSWORD=your_secure_password
- MYSQL_ROOT_PASSWORD=your_secure_password
- Avoid using the MySQL root user outside development environments.

### Environment Variables
- All database configuration is externalized through environment variables.

- Example:

- DB_URL=jdbc:mysql://mysql:3306/EVITest
- DB_USER=root
- DB_PASSWORD=your_secure_password

- MYSQL_DATABASE=EVITest
- MYSQL_ROOT_PASSWORD=your_secure_password
### Hibernate Configuration
- For production environments, consider changing:

- spring.jpa.hibernate.ddl-auto=update
- to:

- spring.jpa.hibernate.ddl-auto=validate
- to prevent automatic schema modifications.

### Add Spring Security (Optional)
- For production-grade deployments:

- Implement authentication and authorization
- Use JWT Bearer Tokens
- Restrict API access based on user roles
- Enable HTTPS behind a reverse proxy

---

## 📚 Additional Resources

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Spring Data JPA Guide](https://spring.io/projects/spring-data-jpa)
- [REST API Best Practices](https://restfulapi.net/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Maven Documentation](https://maven.apache.org/guides/)
- [Postman Documentation](https://learning.postman.com/)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/YourFeature`
3. Commit changes: `git commit -m 'Add YourFeature'`
4. Push to branch: `git push origin feature/YourFeature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License. See the LICENSE file for details.

---

## 👤 Author

**Developed by:** [IanGonzalezM](https://github.com/IangonzalezM)

---

## ❓ FAQ

**Q: How do I test the API without Postman?**
A: You can use cURL commands in terminal or any REST client like Insomnia, Thunder Client, etc.

**Q: Can I save my Postman requests?**
A: Yes! Create a Collection and all requests are automatically saved locally.

**Q: How do I export Postman collection?**
A: Right-click collection → Export → Choose format (JSON) → Save

**Q: What's the difference between POST and PATCH in Postman?**
A: POST updates all fields, PATCH updates only specified fields. Change Method dropdown in Postman.

**Q: How do I add authentication to Postman requests?**
A: Go to Authorization tab → Select type (API Key, Bearer Token, etc.) → Add credentials

**Q: Can I run Postman tests automatically?**
A: Yes! Use Newman (Postman CLI) or Collection Runner feature in Postman

---

## 📞 Support

For issues or questions, please:
1. Check the [Troubleshooting](#troubleshooting) section
2. Open an issue on GitHub

---

**Last Updated:** November 2026  
**Version:** 0.0.1-SNAPSHOT  
**Status:** ✅ Tested with Postman
