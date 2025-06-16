Here's a complete recap of all **ten tables** in your GPA system, including their **structure** (columns) and **sample data** (as given):

---

### **1. `cdist` – Component Distribution**

Tracks maximum marks per assessment component (like Hourly/Quiz) per course.

**Columns**:
• `id` (PK)
• `hid` (references `head.hid`)
• `total` – max marks
• `rid` (references `recap.rid`)

**Sample Rows**:

```
 id | hid | total | rid
----+-----+-------+-----
 16 |  16 |    30 |   1
 17 |  17 |    25 |   1
...
 61 |  22 |    10 |   4
```

---

### **2. `cmarks` – Component Marks**

Stores each student’s scored marks per assessment component.

**Columns**:
• `mid` (PK)
• `hid` (references `head.hid`)
• `regno` (references `student.regno`)
• `marks` – marks obtained
• `rid` (references `recap.rid`)

**Sample Rows**:

```
 mid    | hid | regno  | marks  | rid
--------+-----+--------+--------+------
922032 |  23 | '33741'| 11.0   | 2559
...
922047 |  23 | '33740'| 12.0   | 2559
```

---

### **3. `course`**

Holds course details and credit weight.

**Columns**:
• `cid` (PK)
• `code` – course code
• `title`
• `theory` (credit hours)
• `lab` (credit hours)

**Sample Rows**:

```
 cid | code    | title                           | theory | lab
-----+---------+---------------------------------+--------+-----
 1   | CE1251  | Introduction to Computers       |      2 |   1
 2   | CE1252  | Calculus and Analytical Geometry-I|    3 |   0
...
10   | CE2454  | Digital Systems                 |      3 |   0
```

---

### **4. `dist` – Distribution**

Similar to `cdist`, also tracks distribution of marks per component.

**Columns**:
• `id` (PK)
• `hid`
• `total` – max marks
• `rid`

**Sample Rows**:

```
 id | hid | total | rid
----+-----+-------+-----
 1  | 1   |    15 |   1
 2  | 2   |    15 |   1
...
 11 | 11  |     5 |   1
```

---

### **5. `faculty`**

Lists faculty teaching the courses.

**Columns**:
• `fid` (PK)
• `name`

**Sample Rows**:

```
 fid | name
-----+------------------
 1   | Marley Romero
 2   | Quinten Pope
...
 11  | Shyla Wheeler
```

---

### **6. `grade`**

Maps score ranges to grade letters and GPA values (with versions).

**Columns**:
• `gradeid` (PK)
• `start`, `end` – score range
• `grade` – letter grade
• `gpa` – numeric value (0.00–4.00)
• `version`

**Sample Rows**:

```
 gradeid | start | end  | grade | gpa  | version
---------+-------+------+-------+------+---------
       1 |    95 | 100  | A+    | 4.00 |       1
 ...
      11 |     0 | 59   | F     | 0.00 |       1
```

---

### **7. `head` – Assessment Headings**

Defines assessment types like Hourly or Quiz.

**Columns**:
• `hid` (PK)
• `head` – assessment name

**Sample Rows**:

```
 hid | head
-----+----------
 1   | Hourly 1
 2   | Hourly 2
 ...
 14  | Final Paper 1
```

---

### **8. `marks`**

Stores student marks per assessment, mirroring `cmarks` but for graded tasks.

**Columns**:
• `mid` (PK)
• `hid`
• `regno` (references `student.regno`)
• `marks`
• `rid`

**Sample Rows**:

```
 mid   | hid | regno  | marks   | rid
-------+-----+--------+---------+-----
1      | 1   | '49829'| 9.5     |   1
2      | 2   | '49829'| 9.5     |   1
... 
13     | 13  | '49829'| 5.0     |   1
```

---

### **9. `recap` – Course Recap**

Connects courses, term, class, faculty.

**Columns**:
• `rid` (PK)
• `semester`
• `year`
• `class`
• `fid`
• `cid`

**Sample Rows**:

```
 rid | semester | year | class      | fid | cid
-----+----------+------+------------+-----+-----
 1   | Fall     | 1952 | BSCS 1 A   | 1   | 1
...
 7-12| Fall     | 1952 | BSCS 3 A   | 6-11| 7-12
```

---

### **10. `student`**

Student master data.

**Columns**:
• `regno` (PK)
• `name`

**Sample Rows**:

```
 regno | name
-------+-------------------
 '30103' | Alexandria Davis
 '30109' | Nick Oconnell
 ...
 '30654' | Thomas Salazar
 '30660' | Dania Silva
```

---

### ✅ Summary

* **`cdist` & `dist`**: max marks for components.
* **`cmarks` & `marks`**: actual student marks.
* **`Head`**: types of assessments.
* **`grade`**: mapping to GPA.
* **`course`**: credits.
* **`recap`**: links courses to semester, class, year.
* **`faculty`**: instructors.
* **`student`**: student identities.

This is your complete relational structure and sample data to support your GPA computation logic. Let me know if you'd like detailed seed data for each or guidance on crafting the final GPA query!
