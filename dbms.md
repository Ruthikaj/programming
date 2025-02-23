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
