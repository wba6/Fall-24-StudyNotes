Here is a structured summary of the lecture on **Design Theory for Relational Databases**, covering key concepts with examples:

---

### **1. Database Design Theory**
- Goal: Improve schema systematically to avoid anomalies and redundancy.
- **Normalization**: Process of converting schemas into normal forms, ensuring properties like:
  - No insertion, deletion, or update anomalies.
  - Data consistency and minimal redundancy.

---

### **2. Functional Dependencies (FDs)**
- **Definition**: A constraint between attributes in a relation. If two tuples have the same value for attributes \(X\), they must have the same value for \(Y\).
- **Example**:
  - Relation: Books(ISBN, Title, Author, Publisher).
  - FD: ISBN → Title.

- **FD's Purpose**:
  - Identify relationships among attributes.
  - Enable schema design optimization.

---

### **3. Goals of Logical Design**
1. Develop good relational schemas.
2. Avoid redundant data and modification anomalies.
3. Represent relationships among attributes accurately.

---

### **4. Closure and Keys**
- **Closure**: The set of all attributes that can be functionally determined by a given set.
- **Superkey**: A set of attributes that functionally determines all attributes in the relation.
- **Key**: A minimal superkey.
- **Example**:
  - Relation: \(R(A, B, C, D)\), FDs = \{AB → C, C → D, D → A\}.
  - \( \{A, B\}^+ = \{A, B, C, D\} \) → \( \{A, B\} \) is a key.

---

### **5. Normalization**
#### **Boyce-Codd Normal Form (BCNF)**
- A relation is in BCNF if every FD \(X → Y\) satisfies:
  - \(X\) is a superkey, and \(Y\) is not a subset of \(X\).
- **Example**:
  - Relation: Students(ID, Email, Course, Term, Grade).
  - FDs: 
    - ID → Email.
    - Course, Term → Prof.
    - ID, Course, Term → Grade.
  - Decomposition into BCNF is required.

#### **Third Normal Form (3NF)**
- Modifies BCNF to allow some redundancy if \(A\) (right-hand side of FD) is a prime attribute.
- **Example**:
  - FDs: AB → C, C → B. Relation satisfies 3NF but not BCNF.

---

### **6. Decomposition**
- Breaks a schema into smaller relations to:
  - Eliminate anomalies.
  - Ensure **lossless joins** (no data loss).
  - Preserve dependencies (not always possible with BCNF).
- **Example of BCNF Decomposition**:
  - Drinkers(Name, Addr, BeersLiked, Manf, FavBeer).
  - FDs:
    - Name → Addr, FavBeer.
    - BeersLiked → Manf.
  - Decomposition Steps:
    - Relation 1: Drinkers1(Name, Addr, FavBeer).
    - Relation 2: Drinkers2(Name, BeersLiked, Manf).

---

### **7. Exercises**
- **Closure Computation**:
  - Relation: \(R(A, B, C, D, E)\).
  - FDs: AB → C, C → D, D → B, D → E.
  - Compute closures:
    - \( \{A, B\}^+ = \{A, B, C, D, E\} \).
  
- **Is R in BCNF?**
  - No, decompose based on violations.

---

### **8. Minimal Basis and Synthesis**
- Constructing minimal FD sets to create efficient 3NF relations.
- **Example**:
  - Relation: \(R(A, B, C, D)\), FDs: A → B, C → AD.
  - Minimal Basis Decomposition:
    - Relation 1: AB.
    - Relation 2: CD.

---

### **9. Comparison: BCNF vs. 3NF**
- BCNF:
  - Eliminates redundancy.
  - May not preserve dependencies.
- 3NF:
  - Allows some redundancy to preserve dependencies.

---

This summary includes examples and key takeaways for understanding **design theory for relational databases**. Let me know if you'd like detailed examples or explanations for any specific section!