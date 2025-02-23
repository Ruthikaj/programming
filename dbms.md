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


### **📌 SQL vs NoSQL Databases**  
| Feature        | SQL (Relational) | NoSQL (Non-Relational) |
|---------------|-----------------|------------------------|
| **Structure** | Table-based (Rows & Columns) | Key-Value, Document, Column, Graph-based |
| **Schema** | Fixed, predefined schema | Flexible, dynamic schema |
| **Scalability** | Vertical (Scaling up) | Horizontal (Scaling out) |
| **Transactions** | ACID-compliant | BASE (Basically Available, Soft state, Eventually consistent) |
| **Best For** | Structured data, complex queries | Large-scale, high-speed, unstructured data |
| **Examples** | MySQL, PostgreSQL, SQL Server | MongoDB, Cassandra, Redis, Firebase |

### **📌 Which Database for Transactions?**
**For transactions**, SQL databases are the **preferred choice** because they ensure **data consistency, integrity, and reliability** through **ACID properties** (Atomicity, Consistency, Isolation, Durability).  

🔹 **Example:** Banking applications, financial systems, and inventory management require strict transactions where data must remain **consistent at all times**.  

✅ **Why SQL for transactions?**
- Supports **multi-step transactions** (e.g., transferring money between accounts).
- Ensures **data integrity** with foreign keys and constraints.
- Maintains **reliability** even during failures (rollback, recovery).

---

### **📌 ACID Principles in Databases**  
ACID ensures **reliable transactions** in SQL databases.

| ACID Property | Explanation | Example in Project |
|--------------|------------|--------------------|
| **Atomicity** (All or Nothing) | Ensures that a transaction is either fully completed or fully rolled back. | In an **e-commerce** app, if a payment fails, the order is not placed. |
| **Consistency** (Valid State) | Ensures that database remains in a valid state before and after transactions. | In a **banking app**, balance updates must follow rules (no overdraft). |
| **Isolation** (Concurrent Transactions) | Prevents **race conditions**, ensuring transactions do not interfere with each other. | Two users booking the **last available ticket** won’t cause double booking. |
| **Durability** (Permanent Storage) | Once committed, a transaction remains **even after power failure or crash**. | Order history in an **e-commerce app** remains even after a server restart. |

---

### **📌 Applying ACID to My Project**
🚀 **Project: Online Payment System**
1️⃣ **Atomicity** – If money is debited from **User A**, it must be credited to **User B**, or both steps rollback.  
2️⃣ **Consistency** – Database rules ensure a **negative balance is never allowed**.  
3️⃣ **Isolation** – Two users **cannot modify the same account balance** at the same time.  
4️⃣ **Durability** – Transaction logs ensure **data is recoverable** even after a crash.  

✅ **SQL (PostgreSQL/MySQL) is the best choice for transactional systems due to ACID compliance.**

### **📌 Meaning of Consistency in ACID**  

**Consistency** in ACID (Atomicity, Consistency, Isolation, Durability) ensures that **the database remains in a valid state before and after a transaction**. This means:  

1. **Every transaction must take the database from one valid state to another.**  
2. **No transaction should leave the database in an inconsistent state.**  
3. **All integrity constraints (like foreign keys, unique constraints, and business rules) must be maintained.**  

---

### **📌 Example of Consistency in a Banking System**  
#### Scenario: Transferring ₹1000 from Account A to Account B  

- Before transaction:  
  - Account A balance = ₹5000  
  - Account B balance = ₹3000  

- Transaction Process:  
  1. Deduct ₹1000 from Account A  
  2. Add ₹1000 to Account B  

- If the transaction succeeds:  
  - **Account A = ₹4000**  
  - **Account B = ₹4000**  
  - ✅ Database remains **consistent**  

- If the transaction **fails halfway** (e.g., deducted from A but not added to B), **the system must rollback** to maintain consistency.  

---

### **📌 How Consistency Works in Databases?**  
✔ **Foreign Key Constraints** – Prevents orphan records.  
✔ **Unique Constraints** – Ensures no duplicate data (e.g., unique email IDs).  
✔ **Check Constraints** – Enforces rules (e.g., balance cannot be negative).  

---

### **📌 Key Takeaway**  
**Consistency ensures that database rules and constraints are always met, preventing corruption or invalid states.** 🚀

### **📌 Meaning of Isolation in ACID**  

**Isolation** ensures that **multiple transactions can execute concurrently without interfering with each other**, preventing **race conditions** and **dirty reads**.  

📌 **Key Idea:** Each transaction **must be executed as if it’s the only one running**, even if multiple transactions are happening simultaneously.

---

### **📌 Example of Isolation in a Banking System**  
#### Scenario: Two Users Withdrawing Money from the Same Account  

1️⃣ **Account Balance: ₹5000**  
2️⃣ **User A withdraws ₹2000**, and **User B withdraws ₹4000** at the same time.  
3️⃣ If transactions are not properly **isolated**, both might read the old balance and withdraw, leading to an **incorrect final balance**.  

💡 **Without Isolation:**  
- Both A & B see ₹5000 balance  
- A withdraws ₹2000 → balance should be ₹3000  
- B withdraws ₹4000 → balance should be **-₹1000** ❌ (Incorrect!)  

✅ **With Isolation:**  
- A's transaction **locks** the account → B has to wait.  
- A's transaction completes (new balance ₹3000).  
- B’s transaction starts, sees the correct balance, and only withdraws if valid.  

---

### **📌 Isolation Levels in SQL**  

| Isolation Level | Prevents Dirty Reads? | Prevents Non-Repeatable Reads? | Prevents Phantom Reads? | Use Case |
|----------------|-----------------------|------------------------------|------------------------|----------|
| **Read Uncommitted** | ❌ No | ❌ No | ❌ No | Fast but unsafe (e.g., logging) |
| **Read Committed** | ✅ Yes | ❌ No | ❌ No | General-purpose transactions |
| **Repeatable Read** | ✅ Yes | ✅ Yes | ❌ No | Banking, inventory management |
| **Serializable** | ✅ Yes | ✅ Yes | ✅ Yes | Highest safety, used in financial apps |

---

### **📌 Why Isolation is Important?**  
1. **Prevents Dirty Reads** – Ensures transactions **don’t read uncommitted data**.  
2. **Prevents Non-Repeatable Reads** – Ensures **data remains stable** during a transaction.  
3. **Prevents Phantom Reads** – Ensures **new records aren’t added** while reading a dataset.  

✅ **Isolation guarantees that transactions do not interfere with each other, ensuring database accuracy in multi-user environments.** 🚀

### **📌 Meaning of Durability in ACID**  

**Durability** ensures that once a transaction is **successfully committed**, its changes are permanently saved in the database—even in the case of system crashes, power failures, or hardware failures.  

📌 **Key Idea:** **Committed data must never be lost!**  

---

### **📌 Example of Durability in a Banking System**  
#### Scenario: Money Transfer  

1️⃣ **User transfers ₹5000 from Account A to Account B**.  
2️⃣ The database **updates balances** and **commits the transaction**.  
3️⃣ **Power failure occurs right after the commit**.  
4️⃣ When the system restarts, the **transaction must still be recorded** (₹5000 should not disappear!).  

✅ **With Durability:**  
- The database uses **logs, backups, and transaction journals** to ensure the data is saved permanently.  
- After a crash, the system **recovers the committed transaction** and maintains data integrity.  

❌ **Without Durability:**  
- A crash might **erase committed data**, leading to **inconsistent financial records**.  

---

### **📌 How Durability is Achieved in Databases?**  

✔ **Write-Ahead Logging (WAL)** – Changes are first written to a log before updating the database.  
✔ **Commit Logs & Checkpoints** – Ensure the latest committed state is saved.  
✔ **RAID & Replication** – Data is stored in multiple locations for reliability.  
✔ **Crash Recovery Mechanisms** – On restart, the system **replays logs** to restore transactions.  

---

### **📌 Why Durability is Important?**  
✅ Ensures **data is never lost** after a successful transaction.  
✅ Protects against **system crashes, power failures, and unexpected shutdowns**.  
✅ Essential for **banking, e-commerce, and financial applications** where **data loss is unacceptable**.  

🚀 **Durability guarantees that committed transactions remain permanent, ensuring database reliability and trust.**


### **SQL Query to Get the Highest Salary in Each Department**  

```sql
SELECT Department, MAX(Salary) AS Highest_Salary
FROM Employee
GROUP BY Department;
```

### **Explanation:**  
✔ `GROUP BY Department` → Groups employees based on their department.  
✔ `MAX(Salary)` → Fetches the highest salary for each department.  

### **Example Data: Employee Table**  

| Employee_ID | Name  | Department | Salary  |
|------------|-------|------------|---------|
| 101        | Alice  | HR         | 50000   |
| 102        | Bob    | IT         | 70000   |
| 103        | Charlie | HR         | 60000   |
| 104        | David  | IT         | 90000   |
| 105        | Eve    | Finance    | 75000   |

### **Output of the Query:**  

| Department | Highest_Salary |
|------------|---------------|
| HR         | 60000         |
| IT         | 90000         |
| Finance    | 75000         |

This ensures each department's **highest salary** is retrieved efficiently. 🚀

### **Insertion, Deletion, and Updating Anomalies in DBMS**  

When a database is **not properly normalized**, it may suffer from **data redundancy and inconsistency issues**. These issues are classified into **Insertion, Deletion, and Update Anomalies**.

Let's understand these **anomalies** using a real-life **University Database** scenario.  

---

## **1. Insertion Anomaly (Adding Data Issues)**
📌 **Problem:** Inserting data becomes difficult because some attributes depend on other attributes.  

**💡 Scenario:**  
A university maintains a table for **Students and Courses** where students enroll in different courses.

| Student_ID | Student_Name | Course_ID | Course_Name | Instructor |
|------------|--------------|------------|-------------|------------|
| 101        | Alice        | CSE101     | DBMS        | Dr. Smith  |
| 102        | Bob          | CSE102     | OS          | Dr. Brown  |

### **Issue:**  
- If a new course is introduced (e.g., **CSE103 - Computer Networks**) but **no student has enrolled yet**, we **CANNOT insert the course** because we must also insert a **Student_ID**.
- This is an **Insertion Anomaly** because inserting a course **depends on having students enrolled in it**.

✅ **Solution:**  
- **Normalize the table** by creating a separate **Courses Table** and **Students Table**.

---

## **2. Deletion Anomaly (Losing Important Data)**
📌 **Problem:** Deleting one piece of data **accidentally deletes other critical data**.  

**💡 Scenario:**  
Let's say a student **drops out** or cancels enrollment.

| Student_ID | Student_Name | Course_ID | Course_Name | Instructor |
|------------|--------------|------------|-------------|------------|
| 101        | Alice        | CSE101     | DBMS        | Dr. Smith  |
| 102        | Bob          | CSE102     | OS          | Dr. Brown  |

### **Issue:**  
- If **Bob drops out**, and we delete his row, we **also lose the course details (CSE102 - OS, Dr. Brown)**.
- This is a **Deletion Anomaly** because **course information should not depend on student enrollment**.

✅ **Solution:**  
- Store **Courses separately** so that even if a student leaves, course data **remains intact**.

---

## **3. Update Anomaly (Inconsistencies in Updating Data)**
📌 **Problem:** Updating a piece of data **leads to inconsistencies** if it appears in multiple places.  

**💡 Scenario:**  
Suppose the **Instructor for DBMS (Dr. Smith) changes**.

| Student_ID | Student_Name | Course_ID | Course_Name | Instructor |
|------------|--------------|------------|-------------|------------|
| 101        | Alice        | CSE101     | DBMS        | Dr. Smith  |
| 102        | Bob          | CSE102     | OS          | Dr. Brown  |
| 103        | Charlie      | CSE101     | DBMS        | Dr. Smith  |

### **Issue:**  
- We must update **every row** where `DBMS` is taught by `Dr. Smith`.
- If we **miss even one row**, there will be **data inconsistency** (some students may still have "Dr. Smith" instead of the new instructor).
- This is an **Update Anomaly** because **updating one value should not require updating multiple rows**.

✅ **Solution:**  
- Store **Instructor details separately** in an **Instructor Table** and link it via `Instructor_ID`.

---

## **How to Prevent These Anomalies?**
The **best way** to prevent these anomalies is by **normalizing the database** using **Normalization Forms (1NF, 2NF, 3NF, BCNF, etc.)**.

### **🔹 Recommended Normalized Tables**
1. **Students Table**
   ```
   | Student_ID | Student_Name |
   |------------|--------------|
   | 101        | Alice        |
   | 102        | Bob          |
   | 103        | Charlie      |
   ```

2. **Courses Table**
   ```
   | Course_ID | Course_Name |
   |-----------|-------------|
   | CSE101    | DBMS        |
   | CSE102    | OS          |
   | CSE103    | CN          |
   ```

3. **Instructors Table**
   ```
   | Instructor_ID | Instructor_Name |
   |--------------|-----------------|
   | 1            | Dr. Smith       |
   | 2            | Dr. Brown       |
   ```

4. **Enrollments Table (Bridge Table)**
   ```
   | Student_ID | Course_ID | Instructor_ID |
   |------------|-----------|---------------|
   | 101        | CSE101    | 1             |
   | 102        | CSE102    | 2             |
   ```

✅ **Now:**
- **New courses** can be added without requiring students (fixing Insertion Anomalies).
- **Deleting a student** won't remove course details (fixing Deletion Anomalies).
- **Updating an instructor** is done in one place (fixing Update Anomalies).

---

### **📌 Summary Table**
| **Anomaly Type**  | **Problem** | **Example Scenario** | **Solution** |
|------------------|------------|----------------------|-------------|
| **Insertion Anomaly** | Unable to add data without unrelated fields | Can't add a new course unless a student enrolls | Separate Courses Table |
| **Deletion Anomaly** | Deleting one entry removes other necessary data | Removing a student deletes course details | Separate Students & Courses |
| **Update Anomaly** | Data inconsistency when updating | Updating an instructor requires updating multiple rows | Store Instructor details separately |

---

### **🔥 Conclusion**
- **Always normalize databases** to avoid **data redundancy, inconsistency, and anomalies**.
- **Use separate tables** for related data and connect them using **foreign keys**.
- **Apply normalization techniques** to avoid **complex updates and unnecessary dependencies**.

- ### **1. SQL Query to Evaluate A - B Using Joins**  
To evaluate **A - B** (i.e., rows in table `A` that are not present in table `B`), we use the **LEFT JOIN** and filter out NULL values from `B`.

#### **Query**
```sql
SELECT A.*
FROM A
LEFT JOIN B ON A.id = B.id
WHERE B.id IS NULL;
```
#### **Explanation:**
- Performs a **LEFT JOIN** on `A` and `B` based on `id`.
- Filters rows where `B.id IS NULL`, meaning the `id` from `A` has no match in `B`.

---

### **2. Difference Between TRUNCATE and DELETE**
| Feature          | TRUNCATE                         | DELETE                          |
|-----------------|--------------------------------|--------------------------------|
| **Definition**  | Removes **all rows** from a table **without logging individual row deletions**. | Removes **specific rows** based on a **WHERE condition**. |
| **Condition**   | Cannot have a **WHERE clause**. | Can use **WHERE** to delete selective rows. |
| **Logging**     | Minimal logging, **faster**. | Logs each row deletion, **slower** for large data. |
| **Rollback**    | **Cannot be rolled back** (unless within a transaction). | **Can be rolled back**. |
| **Resets Identity** | **Yes**, resets auto-increment counter. | **No**, identity value is retained. |
| **Trigger Activation** | **No triggers** are fired. | Triggers are executed. |
| **Performance** | **Faster** for large data. | **Slower**, especially for large datasets. |

✅ **Use `TRUNCATE`** when you want to remove **all rows quickly** without logging.  
✅ **Use `DELETE`** when you need **conditional row deletion** and rollback capabilities.

---

### **3. DML vs DDL Commands in SQL**
| **Category**  | **DML (Data Manipulation Language)** | **DDL (Data Definition Language)** |
|--------------|----------------------------------|----------------------------------|
| **Purpose** | Modifies **data** in the database | Defines/modifies **structure** of the database |
| **Commands** | `INSERT`, `UPDATE`, `DELETE`, `SELECT` | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **Effect** | Affects **rows (data)** | Affects **tables (schema)** |
| **Rollback** | **Yes**, can be rolled back | **No**, cannot be rolled back in most cases |
| **Logging** | Fully logged | Partially logged |

✅ **DML Example:**  
```sql
INSERT INTO Employees (Emp_id, Name, Salary) VALUES (101, 'Alice', 50000);
```

✅ **DDL Example:**  
```sql
CREATE TABLE Employees (
    Emp_id INT PRIMARY KEY,
    Name VARCHAR(50),
    Salary INT
);
```

---

### **4. SQL Query to Find Count of Employees Having `grade = '3'` and Their Second Highest Salary**
#### **Query**
```sql
WITH RankedSalaries AS (
    SELECT Emp_id, grade, salary, 
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rank
    FROM Employee
    WHERE grade = '3'
)
SELECT COUNT(*) AS employee_count, MAX(salary) AS second_highest_salary
FROM RankedSalaries
WHERE rank = 2;
```
#### **Explanation:**
1. **`DENSE_RANK()`** assigns ranks to salaries in descending order.
2. Filters employees where **`grade = '3'`**.
3. Selects:
   - **`COUNT(*)`** → Total employees with `grade = '3'`.
   - **`MAX(salary)`** where `rank = 2` → Gets the **second highest salary**.

✅ This ensures correct ranking even when multiple employees have the same salary.
