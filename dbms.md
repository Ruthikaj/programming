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

Would you like more SQL queries? 😊
