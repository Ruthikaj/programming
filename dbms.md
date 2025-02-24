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

### **1. Hypothetical Situation: Joint Account Withdrawals & Concurrency Control**  
When **two users try to withdraw from a joint account at the same time from different ATMs**, **concurrency control mechanisms** in databases handle this scenario.

✅ **Possible Issues:**  
- **Race Condition**: Both transactions might read the same balance before updating, leading to over-withdrawal.  
- **Deadlock**: If both transactions hold partial locks, they may block each other indefinitely.  

✅ **How Concurrency Control Solves This:**  
- **Locks (Pessimistic Concurrency Control)**: A **write lock** ensures one transaction updates the balance before the other.  
- **Optimistic Concurrency Control**: Transactions proceed and **validate** balance before committing.  
- **ACID Properties (Isolation Level: Serializable or Repeatable Read)**: Prevents inconsistent reads and updates.

---

### **2. Normalization Concepts with Example Tables**  

#### **Unnormalized Table (UNF)**
| Student_ID | Name  | Subject  | Marks | Department |  
|-----------|------|---------|------|------------|  
| 101       | John | Math    | 85   | Science    |  
| 101       | John | Physics | 78   | Science    |  
| 102       | Alice | Math    | 90   | Science    |  
| 102       | Alice | English | 82   | Arts       |  

#### **First Normal Form (1NF)**
- No **repeating groups**; each column has atomic values.
```sql
CREATE TABLE Students (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Department VARCHAR(50)
);
CREATE TABLE Marks (
    Student_ID INT,
    Subject VARCHAR(50),
    Marks INT,
    FOREIGN KEY (Student_ID) REFERENCES Students(Student_ID)
);
```

#### **Second Normal Form (2NF)**
- No **partial dependency** on a composite key.
- If (Student_ID, Subject) is the **composite key**, remove non-key dependency **Department**.
```sql
CREATE TABLE Departments (
    Department_ID INT PRIMARY KEY,
    Department_Name VARCHAR(50)
);
CREATE TABLE Students (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Department_ID INT,
    FOREIGN KEY (Department_ID) REFERENCES Departments(Department_ID)
);
```

#### **Third Normal Form (3NF)**
- Remove **transitive dependency** (e.g., Student_ID → Department_ID → Department_Name).
```sql
CREATE TABLE Students (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50)
);
CREATE TABLE Enrollments (
    Student_ID INT,
    Department_ID INT,
    PRIMARY KEY (Student_ID, Department_ID),
    FOREIGN KEY (Student_ID) REFERENCES Students(Student_ID),
    FOREIGN KEY (Department_ID) REFERENCES Departments(Department_ID)
);
```
✅ **Now, queries on these tables can be optimized.**

---

### **3. SQL Query to Fetch Top 3 Scores from Student Table**  
#### **Table: Students**
| Student_ID | Name  | Score |
|-----------|------|------|
| 101       | John | 95   |
| 102       | Alice | 89   |
| 103       | Bob  | 92   |
| 104       | Charlie | 85   |
| 105       | Dave  | 97   |

#### **Query Using `LIMIT` (MySQL, PostgreSQL)**
```sql
SELECT Name, Score 
FROM Students 
ORDER BY Score DESC 
LIMIT 3;
```

#### **Query Using `TOP` (SQL Server)**
```sql
SELECT TOP 3 Name, Score 
FROM Students 
ORDER BY Score DESC;
```

#### **Query Using `DENSE_RANK()` (Works for All SQL)**
```sql
SELECT Name, Score 
FROM (
    SELECT Name, Score, DENSE_RANK() OVER (ORDER BY Score DESC) AS rnk
    FROM Students
) Ranked
WHERE rnk <= 3;
```

✅ **`DENSE_RANK()` ensures ties are handled correctly.**  

---

### **4. Display Third Highest Marks from Student Table**  
#### **Using `LIMIT` with `OFFSET`**
```sql
SELECT Name, Score 
FROM Students 
ORDER BY Score DESC 
LIMIT 1 OFFSET 2;
```

#### **Using `DENSE_RANK()`**
```sql
SELECT Name, Score 
FROM (
    SELECT Name, Score, DENSE_RANK() OVER (ORDER BY Score DESC) AS rnk
    FROM Students
) Ranked
WHERE rnk = 3;
```
✅ **Handles duplicate scores correctly.**  

---

### **5. Primary Key vs. Foreign Key**
| Feature | Primary Key | Foreign Key |
|---------|------------|-------------|
| **Definition** | Uniquely identifies a record in a table | Refers to a primary key in another table |
| **Uniqueness** | Always unique | Can have duplicates |
| **Nullability** | Cannot be NULL | Can be NULL |
| **Example** | `Student_ID` in `Students` table | `Student_ID` in `Marks` table references `Students` |

```sql
CREATE TABLE Students (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50)
);

CREATE TABLE Marks (
    Student_ID INT,
    Subject VARCHAR(50),
    Marks INT,
    FOREIGN KEY (Student_ID) REFERENCES Students(Student_ID)
);
```

---

### **6. SQL Joins (Optimization Using `JOIN` Instead of `WHERE`)**  
#### **Example Tables**
| Employee_ID | Name  | Dept_ID |
|------------|------|--------|
| 1          | Alice | 10     |
| 2          | Bob  | 20     |

| Dept_ID | Dept_Name |
|--------|----------|
| 10     | HR       |
| 20     | IT       |

#### **Incorrect: Using `WHERE` (Overhead Due to Cartesian Product)**
```sql
SELECT e.Name, d.Dept_Name 
FROM Employees e, Departments d 
WHERE e.Dept_ID = d.Dept_ID;
```
🚨 **Issue:** Creates a Cartesian product before filtering.

#### **Optimized: Using `INNER JOIN`**
```sql
SELECT e.Name, d.Dept_Name 
FROM Employees e
INNER JOIN Departments d ON e.Dept_ID = d.Dept_ID;
```
✅ **Better performance without unnecessary computations.**  

---

### **7. Normalization (Key Concept Summary)**  
| Normal Form | Condition |
|------------|-----------|
| **1NF** | No repeating groups; Atomic values. |
| **2NF** | No partial dependency (All non-key attributes depend on the whole primary key). |
| **3NF** | No transitive dependency (Non-key attributes depend only on the primary key). |
| **BCNF** | Every functional dependency’s left side must be a super key. |

---

### **Final Thoughts**
- **Concurrency Control** ensures correct transaction handling.
- **Normalization** optimizes database design and prevents anomalies.
- **SQL Joins** improve query performance compared to `WHERE` filters.
- **Rank Queries** (`LIMIT`, `OFFSET`, `DENSE_RANK()`) help in fetching top scores.

### **1. ACID Properties in Database**  
**ACID** is an acronym representing four key properties of database transactions to ensure reliable processing:
- **A - Atomicity**: A transaction is **all or nothing**. It either completes fully or does not happen at all.
- **C - Consistency**: A transaction must bring the database from one valid state to another, maintaining all rules and constraints.
- **I - Isolation**: Multiple transactions can run concurrently without affecting each other, preserving intermediate states.
- **D - Durability**: Once a transaction is committed, its result is permanent, even in case of system failure.

---

### **2. Normalization in Databases**  
**Normalization** is the process of structuring a database to reduce redundancy and improve data integrity. It divides larger tables into smaller, related tables and enforces relationships using keys.
  
#### **Types of Normalization**  
1. **1NF (First Normal Form)**: Ensures **atomicity** (no multi-valued attributes) and no repeating groups.
2. **2NF (Second Normal Form)**: Ensures no **partial dependency**, where non-key attributes are dependent on part of a composite key.
3. **3NF (Third Normal Form)**: Ensures no **transitive dependency**, where non-key attributes depend on other non-key attributes.
4. **BCNF (Boyce-Codd Normal Form)**: A stricter form of 3NF, ensuring all functional dependencies have superkeys as determinants.
  
---

### **3. Difference Between Recovery and Restoration in a Database**  
- **Recovery**: Refers to the process of restoring the database to a **consistent state** after a failure. This could involve rolling back incomplete transactions or replaying committed ones from logs.
- **Restoration**: Involves restoring the entire database from a previous **backup**. This occurs after severe failure (e.g., hardware crash), and after restoration, the database needs to be recovered to the current state using logs.

---

### **4. SQL Queries: `ORDER BY` and `GROUP BY`**  

- **`ORDER BY`**: Sorts the result set based on one or more columns.
```sql
SELECT Name, Salary 
FROM Employees 
ORDER BY Salary DESC;
```

- **`GROUP BY`**: Groups rows that share a value in one or more columns.
```sql
SELECT Department, COUNT(*) 
FROM Employees 
GROUP BY Department;
```

---

### **5. Data Storage in a Database**  
Data is typically stored in databases in **tables** composed of **rows (records)** and **columns (fields)**. These tables store relational data where rows represent individual entries, and columns represent attributes.

---

### **6. DDL, DML, DCL, and TCL**  
1. **DDL (Data Definition Language)**: Commands that define and modify database structure.
   - **CREATE**: To create a new table or database.
   - **ALTER**: To modify an existing database object.
   - **DROP**: To delete an object like a table.
   - **TRUNCATE**: To remove all rows from a table without logging individual row deletions.

2. **DML (Data Manipulation Language)**: Commands for data manipulation.
   - **SELECT**: To retrieve data.
   - **INSERT**: To add data.
   - **UPDATE**: To modify data.
   - **DELETE**: To remove data.

3. **DCL (Data Control Language)**: Commands to manage permissions.
   - **GRANT**: To give access to users.
   - **REVOKE**: To remove access.

4. **TCL (Transaction Control Language)**: Commands to manage transactions.
   - **COMMIT**: To save the work.
   - **ROLLBACK**: To undo the work.
   - **SAVEPOINT**: To set a point within a transaction to rollback to.

---

### **7. Concurrency Control & Serializability**  
Concurrency control ensures that multiple transactions can run simultaneously without causing data inconsistency.  

- **Serializability**: The concept that the result of concurrently executing transactions should be the same as if they were executed sequentially.

Concurrency is handled using techniques like:
- **Locks** (Shared and Exclusive locks).
- **Timestamps** (Oldest transactions get priority).
- **Optimistic Concurrency Control** (Validation before commit).

---

### **8. SQL Keys Explanation with Student Database Example**

- **Primary Key**: Uniquely identifies each record.  
  ```sql
  CREATE TABLE Students (
      Student_ID INT PRIMARY KEY,
      Name VARCHAR(50)
  );
  ```

- **Foreign Key**: Establishes a relationship between two tables.
  ```sql
  CREATE TABLE Marks (
      Student_ID INT,
      Subject VARCHAR(50),
      FOREIGN KEY (Student_ID) REFERENCES Students(Student_ID)
  );
  ```

- **Candidate Key**: Any column(s) that can uniquely identify a record.
- **Composite Key**: A combination of two or more columns to uniquely identify a record.
  
- **Unique Key**: Similar to primary key, but can contain a NULL value.
  
- **Super Key**: Any set of attributes that can uniquely identify a tuple.

---

### **9. SQL Query for Employee Table**  
#### **Table: Employees**  
| Emp_id | Grade | Salary |
|--------|-------|--------|
| 1      | 3     | 6000   |
| 2      | 3     | 7500   |
| 3      | 3     | 8500   |
| 4      | 2     | 5000   |

#### **Query to Find Count of Employees with Grade '3' and Second Highest Salary**
```sql
SELECT COUNT(*) AS Count, MAX(Salary) AS Second_Highest_Salary
FROM Employees
WHERE Grade = 3
AND Salary < (SELECT MAX(Salary) FROM Employees WHERE Grade = 3);
```

---

### **10. ER Diagram for Attendance Management System**  
An ER Diagram for an **Attendance Management System** could include entities such as **Students**, **Classes**, **Attendance Records**, and **Courses**. Key attributes might be:

- **Students (Student_ID, Name, Email)**.
- **Courses (Course_ID, Course_Name)**.
- **Classes (Class_ID, Course_ID, Teacher_ID)**.
- **Attendance (Attendance_ID, Class_ID, Student_ID, Status)**.

The relationships include:
- **Students** attend **Classes**.
- **Classes** are conducted for **Courses**.
- **Attendance Records** track student participation in each class.

---

### **11. SQL Query to Delete Duplicate Entries from a Table**  
Assume the table **Employees** with duplicate entries based on **Emp_id**:
```sql
WITH CTE AS (
    SELECT Emp_id, ROW_NUMBER() OVER (PARTITION BY Emp_id ORDER BY Emp_id) AS RowNum
    FROM Employees
)
DELETE FROM CTE WHERE RowNum > 1;
```

✅ **Explanation**: The `CTE` (Common Table Expression) ranks the rows and deletes any row with a rank greater than 1, effectively removing duplicates.

### **1. Deleting Duplicate Entries from a Table**
When dealing with duplicate records in a SQL table, the goal is to keep only one occurrence and remove the rest.

#### **Approach 1: Using `ROW_NUMBER()` with CTE**
```sql
WITH CTE AS (
    SELECT *, 
           ROW_NUMBER() OVER (PARTITION BY column1, column2 ORDER BY id) AS row_num
    FROM table_name
)
DELETE FROM table_name 
WHERE id IN (SELECT id FROM CTE WHERE row_num > 1);
```
✅ **Explanation**:  
- `ROW_NUMBER()` assigns a unique number to each duplicate row.
- `PARTITION BY column1, column2` groups identical rows.
- `row_num > 1` identifies duplicates for deletion.

#### **Approach 2: Using `DISTINCT` and Temporary Table**
```sql
CREATE TABLE temp_table AS
SELECT DISTINCT * FROM table_name;

DROP TABLE table_name;

ALTER TABLE temp_table RENAME TO table_name;
```
✅ **Explanation**:  
- Creates a new table with distinct records.
- Drops the old table and renames the new one.

---

### **2. Transaction Concurrency in SQL**
Transaction concurrency ensures multiple transactions can execute simultaneously without conflicts.

🔹 **Concurrency Issues:**
1. **Dirty Read** – One transaction reads uncommitted changes from another.
2. **Lost Update** – Two transactions update the same row simultaneously.
3. **Non-Repeatable Read** – A transaction gets different values on repeated reads.
4. **Phantom Read** – A transaction sees new records on re-execution.

🔹 **Concurrency Control Techniques:**
- **Locking Mechanisms** (Shared & Exclusive Locks)
- **Timestamp Ordering**
- **Optimistic Concurrency Control** (Validation before commit)
- **Multiversion Concurrency Control (MVCC)** – Used in PostgreSQL & MySQL

Example using Pessimistic Locking:
```sql
BEGIN TRANSACTION;
SELECT * FROM Accounts WHERE AccountID = 101 FOR UPDATE;
UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 101;
COMMIT;
```
✅ **Explanation**:  
- `FOR UPDATE` locks the row until the transaction completes.

---

### **3. Hashing, Indexing, and Normalization**
#### **Hashing**
- Converts input data into a fixed-size key.
- Used in **password storage**, **hash joins**, and **cache lookups**.

#### **Indexing**
- Improves search performance in databases.
- Types:
  - **Clustered Index** (Data is physically sorted)
  - **Non-clustered Index** (Stores references to data)

Example:
```sql
CREATE INDEX idx_employee_salary ON Employees(Salary);
```

#### **Normalization**
- Reduces redundancy and improves data integrity.
- **1NF:** Atomic columns.
- **2NF:** No partial dependency.
- **3NF:** No transitive dependency.
- **BCNF:** Stronger form of 3NF.

---

### **4. Handling "Memory Full" in a Database**
#### **Short-Term Fixes**
- **Normalization**: Remove redundant data.
- **Check for Memory Leaks**: Identify inefficient queries.
- **Optimize Indexes**: Reduce unused indexes.
- **Partitioning**: Split large tables into smaller ones.

#### **Long-Term Fixes**
- **Move to Cloud Storage**: AWS, Azure, Google Cloud.
- **Sharding**: Distribute data across multiple databases.
- **Load Balancing**: Distribute queries across servers.

---

### **5. Fraudulent Debit Transaction Scenario**
#### **Possible Causes**
1. **Unauthorized Access**  
   - If a user’s PIN was used, it’s a **security issue** (not a software bug).  

2. **Software Bug in Transaction Processing**  
   - If multiple fraudulent transactions occur within seconds:
     - **Log Analysis**: Identify suspicious transactions.
     - **Fraud Detection Algorithm**: Flag unusual spending patterns.
     - **Modular Testing & Exception Handling**: Ensure robustness.

#### **Technical Fixes**
- Implement **Two-Factor Authentication (2FA)** for transactions.
- Monitor **transaction frequency** and **flag anomalies**.
- Use **Rate Limiting** to prevent excessive withdrawals.

---

### **6. SQL Query: Fetch the Third-Highest Marks**
```sql
SELECT DISTINCT marks 
FROM students 
ORDER BY marks DESC 
LIMIT 1 OFFSET 2;
```
✅ **Explanation**:  
- `ORDER BY marks DESC` sorts scores in descending order.
- `LIMIT 1 OFFSET 2` skips the top 2 and fetches the 3rd highest.

---

### **7. SQL Query: Second-Highest Salary for Employees with Grade 3**
```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM Employees 
WHERE grade = '3' 
AND salary < (SELECT MAX(salary) FROM Employees WHERE grade = '3');
```
✅ **Explanation**:
- The subquery finds the highest salary.
- The outer query finds the next highest.

---

