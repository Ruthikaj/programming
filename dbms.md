### **1. SQL Query to Get Total Students in Each Department**  
```sql
SELECT Department, COUNT(Student_ID) AS Total_Students  
FROM Students  
GROUP BY Department;
```
🔹 **Explanation:** This query counts the number of students in each department using `GROUP BY`.

---

### **2. What is the `static` keyword in C?**  
The `static` keyword in C modifies **variables** and **functions**:  

- **Static Variables:** Retain their value between function calls.  
  ```c
  void func() {  
      static int count = 0;  
      count++;  
      printf("%d\n", count);  
  }  
  ```
  ✅ Output remains **persistent** across function calls.

- **Static Global Variables:** Restrict access within the file.  
- **Static Functions:** Restrict function scope to the file.

---

### **3. What is DELETE in SQL?**  
The `DELETE` statement removes **rows** from a table but **retains the structure**.  
```sql
DELETE FROM Students WHERE Department = 'CS';
```

---

### **4. Difference Between DELETE and DROP**  

| Feature      | DELETE            | DROP |
|-------------|------------------|------|
| **Action**  | Removes records  | Removes table/schema |
| **Can be Rolled Back?** | ✅ Yes (with `ROLLBACK`) | ❌ No |
| **Affects Structure?** | ❌ No | ✅ Yes |
| **Example** | `DELETE FROM Students WHERE id=1;` | `DROP TABLE Students;` |

---

### **5. SQL Query to Drop a Column from a Table**  
```sql
ALTER TABLE Students DROP COLUMN Address;
```
🔹 **Explanation:** Removes `Address` column from `Students` table.

---

### **6. What is Normalization in SQL?**  
Normalization **removes redundancy and ensures data integrity** by organizing data into **normal forms (1NF, 2NF, 3NF, BCNF, etc.)**.

Example of **Normalization:**
- **Before:**  
  ```plaintext
  Employee(ID, Name, Department, Department_Location)
  ```
- **After (Using BCNF):**
  ```plaintext
  Employee(ID, Name, Department_ID)
  Department(Department_ID, Department_Name, Location)
  ```
✅ **Removes redundancy & improves performance.**

---

### **7. SQL Views**  
A **View** is a **virtual table** that provides a custom query result without storing data.  
```sql
CREATE VIEW CS_Students AS  
SELECT Name, Department FROM Students WHERE Department = 'CS';
```
🔹 **Benefits:** Security, Simplicity, and Abstraction.

---

### **8. SQL Indexes**  
An **Index** speeds up searches in a table by reducing the number of scanned rows.  
```sql
CREATE INDEX idx_student ON Students(Name);
```
🔹 **Types:**  
- **Clustered Index** (Modifies physical order of rows).  
- **Non-Clustered Index** (Creates a separate structure for faster searches).  
Here are the SQL queries for your questions:

### **1. Query to Find the Maximum Salary in an Employee Table**
```sql
SELECT MAX(Salary) AS Highest_Salary FROM Employee;
```
🔹 **Explanation:**  
- `MAX(Salary)`: Finds the highest salary in the `Employee` table.  
- `AS Highest_Salary`: Gives an alias to the result.

---

### **2. Query to Get the Current Date**
```sql
SELECT CURRENT_DATE;
```
OR (in MySQL & SQL Server):
```sql
SELECT GETDATE();
```
🔹 **Explanation:**  
- `CURRENT_DATE`: Returns today’s date.  
- `GETDATE()`: Returns **current date and time** (SQL Server, MySQL).

---

### **3. Query to Select Employees Whose First Name Starts with ‘J’**
```sql
SELECT * FROM Employee WHERE First_Name LIKE 'J%';
```
🔹 **Explanation:**  
- `LIKE 'J%'`: Matches names that **start with ‘J’** (`%` is a wildcard for any characters after ‘J’).

### **Database Schema for a Photo-Sharing App**
A **simplified relational database schema** for storing users and their uploaded photos:  

#### **Tables:**
1. **Users** – Stores user information  
2. **Photos** – Stores photo details  
3. **Likes** – Tracks which user liked which photo  
4. **Comments** – Stores comments on photos  

#### **Schema Design:**
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE Photos (
    photo_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    photo_url VARCHAR(255) NOT NULL,
    caption TEXT,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE
);

CREATE TABLE Likes (
    like_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    photo_id INT NOT NULL,
    liked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE,
    FOREIGN KEY (photo_id) REFERENCES Photos(photo_id) ON DELETE CASCADE
);

CREATE TABLE Comments (
    comment_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    photo_id INT NOT NULL,
    comment_text TEXT NOT NULL,
    commented_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE,
    FOREIGN KEY (photo_id) REFERENCES Photos(photo_id) ON DELETE CASCADE
);
```

---

## **Query to Fetch Recent Photos of a Given User**
To fetch the most recent **photos uploaded by a specific user**, sorted by date:
```sql
SELECT photo_id, photo_url, caption, uploaded_at 
FROM Photos 
WHERE user_id = ? 
ORDER BY uploaded_at DESC 
LIMIT 10;
```
🔹 **Explanation:**  
- `WHERE user_id = ?` → Filters photos of the given user  
- `ORDER BY uploaded_at DESC` → Retrieves most recent photos first  
- `LIMIT 10` → Returns only the **10 most recent photos**  

---

## **Query to Fetch All Photos for a User Feed**
To fetch photos for a user feed (showing recent photos from all users the given user follows):
```sql
SELECT Photos.photo_id, Photos.user_id, Users.username, Photos.photo_url, Photos.caption, Photos.uploaded_at 
FROM Photos
JOIN Users ON Photos.user_id = Users.user_id
WHERE Photos.user_id IN (
    SELECT following_id FROM Followers WHERE follower_id = ? 
)
ORDER BY Photos.uploaded_at DESC
LIMIT 20;
```
🔹 **Explanation:**  
- The **`Followers`** table (not shown in schema) tracks which users a person follows.  
- **Subquery (`SELECT following_id FROM Followers WHERE follower_id = ?`)** gets the users the given user follows.  
- `ORDER BY uploaded_at DESC` → Fetches recent posts first.  
- `LIMIT 20` → Returns **latest 20 photos**.  

---

### **Bonus: Optimize Query with an Index**
To speed up fetching recent photos, add an **index** on `uploaded_at`:
```sql
CREATE INDEX idx_uploaded_at ON Photos(uploaded_at DESC);
```

### **1. What is SQL?**  
SQL (**Structured Query Language**) is used to manage and manipulate relational databases by performing operations like **insertion, retrieval, updating, and deletion** of data.

---

### **2. Types of Joins in SQL**  
Joins in SQL are used to combine rows from **two or more tables** based on a related column.

#### **Types of Joins:**
- **INNER JOIN** → Returns matching rows from both tables.  
- **LEFT JOIN** → Returns all rows from the left table and matching rows from the right.  
- **RIGHT JOIN** → Returns all rows from the right table and matching rows from the left.  
- **FULL JOIN** → Returns all rows from both tables, filling NULL where no match is found.  
- **CROSS JOIN** → Produces the Cartesian product of two tables.  
- **SELF JOIN** → A table joins itself.

#### **Example of INNER JOIN:**
```sql
SELECT Employees.name, Departments.dept_name 
FROM Employees
INNER JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

---

### **3. What is the Use of Self-Join in SQL?**  
A **SELF JOIN** is used to compare rows within the same table. It treats the table as two separate tables.

#### **Example: Finding Employee-Manager Relationship**
```sql
SELECT e1.name AS Employee, e2.name AS Manager
FROM Employees e1
JOIN Employees e2 ON e1.manager_id = e2.emp_id;
```
🔹 Here, the **Employees** table is joined with itself to get the manager's name.

---

### **4. Designing an Optimal Database for Searching with Non-Primary Attributes**  
To efficiently search on **non-primary attributes**, we can use **Indexing** and **Full-Text Search**.

#### **Example Schema:**
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    phone VARCHAR(15),
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### **Optimizations for Fast Searches:**
1. **Indexing on frequently searched columns:**
```sql
CREATE INDEX idx_name ON Users(name);
CREATE INDEX idx_email ON Users(email);
```
2. **Full-Text Search (for large text data):**
```sql
ALTER TABLE Users ADD FULLTEXT(name, address);
```
3. **Using Wildcards for Partial Matching:**
```sql
SELECT * FROM Users WHERE name LIKE 'John%';
```
4. **Denormalization (if needed for performance):**
- Storing derived values (e.g., `name_hash`) to speed up lookups.

---

### **5. What is Indexing in the Database?**  
**Indexing** improves the speed of data retrieval in large databases by creating a data structure for quick lookups.

#### **Example of Indexing:**
```sql
CREATE INDEX idx_email ON Users(email);
```
🔹 Now, searching for a user by email will be **faster**.

#### **Types of Indexes:**
- **Clustered Index** → Sorts the data based on key values (only one per table).  
- **Non-Clustered Index** → Stores pointers to data locations.  
- **Unique Index** → Ensures column values are unique.  
- **Full-Text Index** → Speeds up searches in large text fields.  

---

### **6. What are SQL Triggers?**  
A **Trigger** is an automatic action that runs **before or after** an event (INSERT, UPDATE, DELETE).

#### **Example: Trigger on INSERT**
```sql
CREATE TRIGGER before_insert_user
BEFORE INSERT ON Users
FOR EACH ROW
SET NEW.created_at = NOW();
```
🔹 This ensures `created_at` is automatically set to the current timestamp before inserting a new user.

---

### **7. What are SQL Views?**  
A **View** is a virtual table based on an SQL query.

#### **Use Cases of Views:**
- Hides complexity of queries  
- Ensures security by restricting access to certain columns  
- Helps in data abstraction  

#### **Example: Creating a View for Active Users**
```sql
CREATE VIEW ActiveUsers AS
SELECT user_id, name, email FROM Users WHERE status = 'active';
```

#### **Querying the View:**
```sql
SELECT * FROM ActiveUsers;
```
🔹 Acts like a **virtual table** without storing actual data.

---

### **Summary:**  
✅ **SQL** is used for managing databases  
✅ **Joins** help combine tables; **Self-Join** is used for intra-table relations  
✅ **Indexes** optimize queries on non-primary attributes  
✅ **Triggers** automate actions in a database  
✅ **Views** act as virtual tables for security and ease of access  
EXAMPLE 
# **SQL Joins Explained with Real-Life Scenarios**  

Joins in SQL are used to retrieve data from multiple tables by linking them through a common key. Let's explore each type of join with **real-life examples** to make it easier to understand.

---

## **1. INNER JOIN (Common Data Only)**
**📌 Scenario:**  
Imagine a company where **employees** are assigned to **departments**. We need to fetch only those employees who are assigned to a department.  

### **Tables:**
#### **Employees Table**
| emp_id | emp_name | dept_id |
|--------|----------|---------|
| 1      | Alice    | 101     |
| 2      | Bob      | 102     |
| 3      | Charlie  | 103     |
| 4      | David    | 101     |

#### **Departments Table**
| dept_id | dept_name  |
|---------|-----------|
| 101     | HR        |
| 102     | IT        |
| 104     | Finance   |

### **Query:**
```sql
SELECT Employees.emp_name, Departments.dept_name
FROM Employees
INNER JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

### **Output:**
| emp_name | dept_name |
|----------|----------|
| Alice    | HR       |
| Bob      | IT       |
| David    | HR       |

✅ **Explanation:**  
- **Only employees with a matching department** are included.  
- `Charlie` (dept_id = 103) **is not included** because there's no matching `dept_id` in `Departments`.  
- `Finance` (dept_id = 104) **is not included** because no employee belongs to it.

---

## **2. LEFT JOIN (All Left Table Data, Even If No Match)**
**📌 Scenario:**  
We want to list **all employees**, even those who are **not assigned to a department**.

### **Query:**
```sql
SELECT Employees.emp_name, Departments.dept_name
FROM Employees
LEFT JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

### **Output:**
| emp_name | dept_name |
|----------|----------|
| Alice    | HR       |
| Bob      | IT       |
| Charlie  | NULL     |
| David    | HR       |

✅ **Explanation:**  
- **All employees are included**, even those without a department (`Charlie`).  
- `Charlie` has `dept_id = 103`, which **does not exist** in `Departments`, so `dept_name` is **NULL**.

---

## **3. RIGHT JOIN (All Right Table Data, Even If No Match)**
**📌 Scenario:**  
We want to list **all departments**, even if they have **no employees assigned**.

### **Query:**
```sql
SELECT Employees.emp_name, Departments.dept_name
FROM Employees
RIGHT JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

### **Output:**
| emp_name | dept_name |
|----------|----------|
| Alice    | HR       |
| Bob      | IT       |
| David    | HR       |
| NULL     | Finance  |

✅ **Explanation:**  
- **All departments are included**, even if they have **no employees** (`Finance`).  
- `Finance` (dept_id = 104) **does not have any employees**, so `emp_name` is **NULL**.

---

## **4. FULL JOIN (Everything, Fill NULLs for Missing Matches)**
**📌 Scenario:**  
We want a **complete report** that shows **all employees and all departments**, even if some do not have matches.

### **Query:**
```sql
SELECT Employees.emp_name, Departments.dept_name
FROM Employees
FULL JOIN Departments ON Employees.dept_id = Departments.dept_id;
```

### **Output:**
| emp_name | dept_name |
|----------|----------|
| Alice    | HR       |
| Bob      | IT       |
| Charlie  | NULL     |
| David    | HR       |
| NULL     | Finance  |

✅ **Explanation:**  
- **All employees** and **all departments** are included.  
- `Charlie` (dept_id = 103) **does not match any department**, so `dept_name = NULL`.  
- `Finance` (dept_id = 104) **has no employees**, so `emp_name = NULL`.

---

## **5. CROSS JOIN (Every Combination of Two Tables)**
**📌 Scenario:**  
A **restaurant** has different **menu items** and different **tables** for customers. We want to pair every **menu item** with every **table number** to prepare a bill structure.

#### **Menu Table**
| menu_id | item_name |
|---------|----------|
| 1       | Pizza    |
| 2       | Burger   |
| 3       | Pasta    |

#### **Tables Table**
| table_id | table_no |
|---------|----------|
| 1       | 101      |
| 2       | 102      |

### **Query:**
```sql
SELECT Menu.item_name, Tables.table_no
FROM Menu
CROSS JOIN Tables;
```

### **Output:**
| item_name | table_no |
|----------|---------|
| Pizza    | 101     |
| Pizza    | 102     |
| Burger   | 101     |
| Burger   | 102     |
| Pasta    | 101     |
| Pasta    | 102     |

✅ **Explanation:**  
- Each **menu item is paired with every table number**, regardless of any relationship.

---

## **6. SELF JOIN (Table Joins Itself)**
**📌 Scenario:**  
An **organization** has employees who report to **managers**. We want to list each **employee along with their manager**.

#### **Employees Table**
| emp_id | emp_name | manager_id |
|--------|----------|------------|
| 1      | Alice    | NULL       |
| 2      | Bob      | 1          |
| 3      | Charlie  | 1          |
| 4      | David    | 2          |

### **Query:**
```sql
SELECT e1.emp_name AS Employee, e2.emp_name AS Manager
FROM Employees e1
LEFT JOIN Employees e2 ON e1.manager_id = e2.emp_id;
```

### **Output:**
| Employee | Manager |
|----------|---------|
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |
| David    | Bob     |

✅ **Explanation:**  
- The **Employees table joins itself** to show the **manager of each employee**.

---

## **Comparison of Joins**
| **Join Type**  | **Real-Life Example** | **Matching Rows?** | **Unmatched Rows?** |
|--------------|----------------|----------------|----------------|
| **INNER JOIN** | Employees with a department | ✅ Yes | ❌ Excluded |
| **LEFT JOIN**  | Employees list (even if no department) | ✅ Yes | ✅ Left table retained |
| **RIGHT JOIN** | Departments list (even if no employee) | ✅ Yes | ✅ Right table retained |
| **FULL JOIN**  | Full report of employees & departments | ✅ Yes | ✅ Both tables retained |
| **CROSS JOIN** | Pairing menu items with tables | ❌ No condition | ✅ Cartesian product |
| **SELF JOIN**  | Employees reporting to managers | ✅ Yes | ✅ Used for hierarchical data |

---

## **Summary**
💡 **INNER JOIN** → Only matches   
💡 **LEFT JOIN** → All left + matches  
💡 **RIGHT JOIN** → All right + matches  
💡 **FULL JOIN** → Everything (fill missing values with NULL)  
💡 **CROSS JOIN** → Every possible combination  
💡 **SELF JOIN** → A table joins itself  


