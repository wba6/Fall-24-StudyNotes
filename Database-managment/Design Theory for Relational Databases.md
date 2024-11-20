
---

### **1. Database Design Theory**
- **Goal**: The primary objective of database design theory is to systematically improve the database schema to ensure efficiency, minimize redundancy, and prevent data anomalies. Effective design facilitates accurate data representation, supports data integrity, and optimizes query performance.

- **Normalization**: Normalization is a fundamental process in database design aimed at organizing data to reduce redundancy and dependency. It involves decomposing a database into multiple related tables without losing data integrity. The process ensures that each table represents one entity or concept, thereby enhancing data consistency and simplifying maintenance.

  - **Key Properties of Normalization**:
    - **Elimination of Anomalies**: Prevents insertion, deletion, and update anomalies that can lead to inconsistent data.
    - **Data Consistency**: Ensures that data remains consistent across the database by minimizing redundancy.
    - **Minimal Redundancy**: Reduces duplicate data, which saves storage space and simplifies data management.

  - **Common Normal Forms**:
    - **First Normal Form (1NF)**: Ensures that the table has a primary key and that each column contains atomic (indivisible) values.
    - **Second Normal Form (2NF)**: Achieved when the table is in 1NF and all non-key attributes are fully functionally dependent on the primary key.
    - **Third Normal Form (3NF)**: Achieved when the table is in 2NF and all the attributes are functionally independent of any other non-key attribute.
    - **Boyce-Codd Normal Form (BCNF)**: A stricter version of 3NF where every determinant is a candidate key.

---

### **2. Functional Dependencies (FDs)**
- **Definition**: A Functional Dependency (FD) is a relationship that exists when one attribute uniquely determines another attribute within a relation. Formally, for attributes \(X\) and \(Y\) in a relation \(R\), \(X → Y\) means that if two tuples have the same value for \(X\), they must have the same value for \(Y\).

- **Formal Definition**:
  - Given a relation \(R\), \(X → Y\) holds if, for any two tuples \(t_1\) and \(t_2\) in \(R\), whenever \(t_1[X] = t_2[X]\), then \(t_1[Y] = t_2[Y]\).

- **Example**:
  - **Relation**: Books(ISBN, Title, Author, Publisher, Price).
  - **Functional Dependencies**:
    - ISBN → Title, Author, Publisher, Price.
      - **Explanation**: Each ISBN uniquely identifies a book's title, author, publisher, and price.
    - Publisher → Address.
      - **Explanation**: Each publisher has a unique address.

- **Additional Example**:
  - **Relation**: Employees(EmpID, Name, Department, Manager).
  - **Functional Dependencies**:
    - EmpID → Name, Department, Manager.
    - Department → Manager.
      - **Explanation**: Each employee ID uniquely determines the employee's name, department, and manager. Additionally, each department has one manager.

- **FD's Purpose**:
  - **Identify Relationships Among Attributes**: Understanding how attributes relate helps in structuring the database efficiently.
  - **Enable Schema Design Optimization**: By identifying dependencies, designers can normalize the schema to eliminate redundancy and prevent anomalies.
  - **Determine Keys**: Functional dependencies are crucial in identifying candidate keys and superkeys for the relation.

---

### **3. Goals of Logical Design**
1. **Develop Good Relational Schemas**:
   - Create schemas that accurately represent the real-world entities and their relationships.
   - Ensure that each table captures a single entity or relationship to maintain clarity and simplicity.

2. **Avoid Redundant Data and Modification Anomalies**:
   - **Redundancy**: Duplicate data can lead to inconsistencies and inefficient storage usage.
   - **Modification Anomalies**:
     - **Insertion Anomaly**: Difficulty in adding data due to missing information.
     - **Deletion Anomaly**: Unintended loss of data when deleting records.
     - **Update Anomaly**: Inconsistencies arising from updating redundant data in multiple places.

3. **Represent Relationships Among Attributes Accurately**:
   - Ensure that the relationships (one-to-one, one-to-many, many-to-many) between different entities are correctly modeled.
   - Use foreign keys and associative tables where necessary to maintain referential integrity.

---

### **4. Closure and Keys**
- **Closure**: The closure of a set of attributes \(X\) (denoted as \(X^+\)) is the set of all attributes that can be functionally determined by \(X\) using the given functional dependencies. It is used to find all attributes that are implied by \(X\).

  - **Example**:
    - **Relation**: \(R(A, B, C, D)\)
    - **Functional Dependencies**: AB → C, C → D, D → A
    - **Closure Calculation**:
      - Start with \( \{A, B\} \).
      - From AB → C, add C.
      - From C → D, add D.
      - From D → A, A is already in the set.
      - Final Closure: \( \{A, B, C, D\} \).

- **Superkey**: A superkey is a set of one or more attributes that can uniquely identify a tuple in a relation. It may contain additional attributes that are not necessary for unique identification.

  - **Example**:
    - In the relation \(R(A, B, C, D)\), both \( \{A, B\} \) and \( \{A, B, C\} \) are superkeys since they can uniquely identify tuples.

- **Key**: A key is a minimal superkey, meaning it has no unnecessary attributes. It is the smallest subset of attributes that can uniquely identify a tuple.

  - **Example**:
    - In the relation \(R(A, B, C, D)\), if \( \{A, B\} \) uniquely identifies tuples and removing either \(A\) or \(B\) causes it to no longer uniquely identify tuples, then \( \{A, B\} \) is a key.

- **Determining Keys**:
  - **Candidate Keys**: All possible minimal superkeys. A relation can have multiple candidate keys.
  - **Primary Key**: A selected candidate key used to uniquely identify tuples within the table.

- **Additional Example**:
  - **Relation**: Students(StudentID, Name, Email, Major)
  - **Functional Dependencies**:
    - StudentID → Name, Email, Major
    - Email → Name, Major
  - **Keys**:
    - \( \{StudentID\} \) is a key since it uniquely identifies each student.
    - \( \{Email\} \) is also a key if emails are unique to each student.

---

### **5. Normalization**
Normalization organizes the attributes and tables of a relational database to minimize redundancy and dependency. Below are detailed explanations of BCNF and 3NF, including their definitions and examples.

#### **Boyce-Codd Normal Form (BCNF)**
- **Definition**: A relation is in BCNF if, for every non-trivial functional dependency \(X → Y\), \(X\) is a superkey. This ensures that all determinants are candidate keys, eliminating redundancy caused by dependencies.

  - **Non-Trivial FD**: An FD \(X → Y\) is non-trivial if \(Y\) is not a subset of \(X\).

- **Purpose**: BCNF is designed to eliminate all forms of redundancy and prevent anomalies by ensuring that every determinant is a superkey.

- **Example**:
  - **Relation**: Students(ID, Email, Course, Term, Grade, Prof)
  - **Functional Dependencies**:
    - ID → Email
    - Course, Term → Prof
    - ID, Course, Term → Grade

  - **Analysis**:
    - **ID → Email**: \(ID\) is a key for the student’s email.
    - **Course, Term → Prof**: \(Course\) and \(Term\) determine the professor.
    - **ID, Course, Term → Grade**: Composite key determining the grade.

  - **BCNF Violation**:
    - The FD \(Course, Term → Prof\) does not have \(Course, Term\) as a superkey for the entire relation, violating BCNF.

  - **Decomposition into BCNF**:
    - **Relation 1**: Courses(Course, Term, Prof)
    - **Relation 2**: Students(ID, Email, Course, Term, Grade)

#### **Third Normal Form (3NF)**
- **Definition**: A relation is in Third Normal Form (3NF) if it is in Second Normal Form (2NF) and no transitive dependencies exist. Formally, for every non-trivial functional dependency \(X → Y\), either \(X\) is a superkey, or \(Y\) is a prime attribute (part of some candidate key).

- **Purpose**: 3NF eliminates transitive dependencies, thereby reducing redundancy while allowing some controlled redundancy to maintain dependencies.

- **Example**:
  - **Relation**: R(A, B, C)
  - **Functional Dependencies**:
    - AB → C
    - C → B

  - **Analysis**:
    - **AB → C**: \(AB\) is a key.
    - **C → B**: \(C\) is not a superkey, and \(B\) is not a prime attribute.

  - **Conclusion**: The relation violates BCNF because \(C\) is not a superkey. However, if \(B\) is part of a candidate key, the relation can still satisfy 3NF.

- **Additional Example**:
  - **Relation**: Employee(EmpID, Name, Department, DeptHead)
  - **Functional Dependencies**:
    - EmpID → Name, Department
    - Department → DeptHead

  - **Analysis**:
    - **EmpID → Name, Department**: \(EmpID\) is a key.
    - **Department → DeptHead**: \(Department\) is not a superkey, and \(DeptHead\) is not a prime attribute.

  - **3NF Compliance**:
    - If \(DeptHead\) is considered a prime attribute (part of a candidate key), the relation can be in 3NF.
    - Otherwise, to achieve 3NF, decompose the relation:
      - **Relation 1**: Employee(EmpID, Name, Department)
      - **Relation 2**: Department(Department, DeptHead)

---

### **6. Decomposition**
Decomposition is the process of breaking down a large relation into smaller, well-structured relations without losing any information. The goal is to eliminate redundancy and ensure data integrity.

- **Key Objectives**:
  - **Eliminate Anomalies**: Remove insertion, deletion, and update anomalies by decomposing relations.
  - **Ensure Lossless Joins**: Guarantee that the original relation can be perfectly reconstructed by joining the decomposed relations.
  - **Preserve Dependencies**: Maintain all functional dependencies to ensure data integrity.

- **Types of Decomposition**:
  - **Dependency-Preserving Decomposition**: Ensures that all functional dependencies are maintained in the decomposed relations.
  - **Non-Dependency-Preserving Decomposition**: Some functional dependencies may not be preserved, potentially requiring additional mechanisms to enforce them.

- **Example of BCNF Decomposition**:
  - **Relation**: Drinkers(Name, Addr, BeersLiked, Manf, FavBeer)
  - **Functional Dependencies**:
    - Name → Addr, FavBeer
    - BeersLiked → Manf

  - **Decomposition Steps**:
    1. **Identify Violations**:
       - \( BeersLiked → Manf \): \( BeersLiked \) is not a superkey.
    2. **Decompose Based on FD**:
       - **Relation 1**: Drinkers1(Name, Addr, FavBeer)
       - **Relation 2**: Drinkers2(BeersLiked, Manf)
       - **Relation 3**: Drinkers3(Name, BeersLiked) *(to maintain the original relationship)*
    3. **Resulting Relations**:
       - **Drinkers1(Name, Addr, FavBeer)**
       - **Drinkers2(BeersLiked, Manf)**
       - **Drinkers3(Name, BeersLiked)**

- **Additional Example**:
  - **Relation**: Orders(OrderID, ProductID, Quantity, ProductPrice, CustomerID)
  - **Functional Dependencies**:
    - OrderID, ProductID → Quantity, ProductPrice
    - ProductID → ProductPrice

  - **Decomposition into BCNF**:
    1. **Identify Violations**:
       - \( ProductID → ProductPrice \): \( ProductID \) is not a superkey.
    2. **Decompose**:
       - **Relation 1**: Orders1(OrderID, ProductID, Quantity)
       - **Relation 2**: Products(ProductID, ProductPrice)
    3. **Resulting Relations**:
       - **Orders1(OrderID, ProductID, Quantity)**
       - **Products(ProductID, ProductPrice)**

---

### **7. Exercises**
**Exercise 1: Closure Computation**
- **Given**:
  - **Relation**: \(R(A, B, C, D, E)\)
  - **Functional Dependencies**: 
    - AB → C
    - C → D
    - D → B
    - D → E

- **Task**: Compute the closure of \( \{A, B\} \).

- **Solution**:
  1. Start with \( \{A, B\} \).
  2. Apply \( AB → C \): Add \( C \). Now \( \{A, B, C\} \).
  3. Apply \( C → D \): Add \( D \). Now \( \{A, B, C, D\} \).
  4. Apply \( D → B \): \( B \) is already in the set.
  5. Apply \( D → E \): Add \( E \). Now \( \{A, B, C, D, E\} \).

- **Closure**: \( \{A, B\}^+ = \{A, B, C, D, E\} \)

- **Conclusion**: Since the closure of \( \{A, B\} \) includes all attributes, \( \{A, B\} \) is a candidate key for \(R\).

**Exercise 2: Is R in BCNF?**
- **Given**:
  - **Relation**: \(R(A, B, C, D, E)\)
  - **Functional Dependencies**: 
    - AB → C
    - C → D
    - D → B
    - D → E

- **Task**: Determine if \(R\) is in BCNF and, if not, decompose it.

- **Solution**:
  1. **Identify Candidate Keys**:
     - From the closure computation, \( \{A, B\} \) is a candidate key.
  2. **Check Each FD**:
     - **AB → C**: \( AB \) is a superkey. **No Violation**.
     - **C → D**: \( C \) is not a superkey. **Violation**.
     - **D → B**: \( D \) is not a superkey. **Violation**.
     - **D → E**: \( D \) is not a superkey. **Violation**.

  3. **Decompose Based on Violations**:
     - **First Decomposition**:
       - **Relation 1**: \(R1(C, D, B, E)\) based on \( C → D \), \( D → B \), \( D → E \).
       - **Relation 2**: \(R2(A, B, C)\).
     - **Check BCNF for \(R1\)**:
       - \( C → D \): \( C \) is not a superkey for \(R1\). **Violation**.
       - Decompose \(R1\) further:
         - **Relation 1a**: \(R1a(D, B, E)\) based on \( D → B \), \( D → E \).
         - **Relation 1b**: \(R1b(C, D)\).

     - **Final Decomposed Relations**:
       - \(R2(A, B, C)\)
       - \(R1a(D, B, E)\)
       - \(R1b(C, D)\)

  4. **Result**: All decomposed relations are now in BCNF.

---

### **8. Minimal Basis and Synthesis**
- **Minimal Basis**: A minimal basis for a set of functional dependencies is a minimal set of dependencies that preserves the original dependencies, where:
  - Each functional dependency has a single attribute on the right-hand side.
  - The left-hand side of each dependency is minimal (no extraneous attributes).
  - No dependency can be removed without altering the closure.

- **Synthesis Algorithm**: A method to create a set of relations in 3NF from a minimal basis by ensuring that dependencies are preserved and the resulting schema is in 3NF.

- **Steps to Find Minimal Basis**:
  1. **Ensure Single Attribute on RHS**: Decompose dependencies so each FD has only one attribute on the right.
  2. **Minimize LHS**: Remove any extraneous attributes from the left-hand side.
  3. **Remove Redundant Dependencies**: Eliminate any dependencies that can be inferred from others.

- **Example**:
  - **Given**:
    - **Relation**: \(R(A, B, C, D)\)
    - **Functional Dependencies**: 
      - A → B
      - C → AD

  - **Minimal Basis**:
    - **Step 1**: Ensure single attribute on RHS:
      - A → B
      - C → A
      - C → D
    - **Step 2**: Minimize LHS:
      - \(A → B\) remains as is.
      - \(C → A\) and \(C → D\) remain as is.
    - **Step 3**: Remove redundant dependencies:
      - No redundant dependencies in this case.

    - **Final Minimal Basis**:
      - A → B
      - C → A
      - C → D

  - **Synthesis into 3NF**:
    - **Relation 1**: \(R1(A, B)\) based on \( A → B \).
    - **Relation 2**: \(R2(C, A, D)\) based on \( C → A \) and \( C → D \).

- **Additional Example**:
  - **Given**:
    - **Relation**: \(R(X, Y, Z)\)
    - **Functional Dependencies**: 
      - XZ → Y
      - Y → Z

  - **Minimal Basis**:
    - Ensure single attribute on RHS:
      - XZ → Y
      - Y → Z
    - Minimize LHS:
      - No extraneous attributes in \(XZ → Y\).
    - Remove redundant dependencies:
      - None.

    - **Final Minimal Basis**:
      - XZ → Y
      - Y → Z

  - **Synthesis into 3NF**:
    - **Relation 1**: \(R1(X, Z, Y)\) based on \( XZ → Y \).
    - **Relation 2**: \(R2(Y, Z)\) based on \( Y → Z \).

---

### **9. Comparison: BCNF vs. 3NF**
Understanding the differences between Boyce-Codd Normal Form (BCNF) and Third Normal Form (3NF) is crucial for effective database design.

- **BCNF**:
  - **Stricter**: BCNF is a stricter form of normalization compared to 3NF.
  - **Redundancy Elimination**: Completely eliminates redundancy caused by functional dependencies where determinants are not candidate keys.
  - **Dependency Preservation**: May not always preserve all functional dependencies during decomposition, which can complicate queries and updates.
  - **Use Cases**: Preferred when eliminating all redundancy is crucial, and when dependencies can be preserved through alternative mechanisms.

- **3NF**:
  - **Less Strict**: Allows some redundancy to ensure that all functional dependencies are preserved.
  - **Balanced Approach**: Balances between eliminating redundancy and preserving dependencies, making it more practical for many real-world applications.
  - **Dependency Preservation**: Ensures that all functional dependencies are maintained within the decomposed relations, simplifying query and update operations.
  - **Use Cases**: Commonly used in practical database designs where maintaining dependencies is essential for data integrity.

- **Key Differences**:
  - **Redundancy**: BCNF eliminates more redundancy than 3NF.
  - **Dependency Preservation**: 3NF ensures that all dependencies are preserved, whereas BCNF might not.
  - **Complexity**: Decomposing to BCNF can sometimes require more tables and may complicate the schema, whereas 3NF often results in a more manageable number of tables.

- **Illustrative Example**:
  - **Relation**: \(R(A, B, C)\)
  - **Functional Dependencies**:
    - A → B
    - B → C

  - **Analysis**:
    - **Candidate Keys**: \( \{A\} \) if A determines B and B determines C, so \( \{A\} \) → \( \{A, B, C\} \).
    - **3NF Compliance**:
      - All non-trivial FDs have either a superkey on the LHS or a prime attribute on the RHS.
      - \( A → B \): \( A \) is a superkey. **OK**.
      - \( B → C \): \( B \) is not a superkey, but if \( B \) is part of a candidate key, it can satisfy 3NF.
    - **BCNF Compliance**:
      - \( B → C \): \( B \) is not a superkey. **Violation**.
  
  - **Decomposition**:
    - **For 3NF**:
      - Since 3NF allows dependencies with prime attributes, the relation may already satisfy 3NF if \( B \) is part of a candidate key.
    - **For BCNF**:
      - Decompose into:
        - **Relation 1**: \( R1(A, B) \)
        - **Relation 2**: \( R2(B, C) \)
      - Both \( R1 \) and \( R2 \) are now in BCNF.

