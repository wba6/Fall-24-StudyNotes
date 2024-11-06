# Chapter 7: Constraints

## Why Are Constraints Needed?
Constraints enforce specific relationships among data elements in a database, ensuring data integrity. For example:
- **Primary Key Constraints**: Ensure uniqueness of a row.
- **Triggers**: Execute actions when specified conditions occur, making complex constraints easier to handle.

---

## Types of Constraints
1. **Primary Keys**
   - Ensure each row in a table is unique.
   - Example:
     ```sql
     CREATE TABLE Beers (
       name CHAR(20) PRIMARY KEY,
       manf CHAR(20)
     );
     ```

2. **Foreign Keys (Referential Integrity)**
   - Ensure values in one table correspond to values in another.
   - Example:
     ```sql
     CREATE TABLE Sells (
       bar CHAR(20),
       beer CHAR(20) REFERENCES Beers(name),
       price REAL
     );
     ```

3. **Value-Based Constraints**
   - Apply rules to individual attributes (e.g., `NOT NULL`).

4. **Tuple-Based Constraints**
   - Apply rules to combinations of attributes.

---

## Foreign Keys: Handling Violations
Two possible violations:
1. Insertion/Update in one table introduces invalid references.
2. Deletion/Update in the referenced table leaves "dangling" references.

### Actions Taken:
1. **Default (Reject Modification)**: Prevents the operation.
2. **Cascade**: Propagates changes to dependent tables.
   - Example:
     - Deleting a referenced row cascades deletion in dependent rows.
     - Updating a referenced value cascades the update.
3. **Set NULL**: Sets dependent foreign key values to `NULL`.

### Policy Declaration:
Define policies for updates and deletions explicitly:
```sql
FOREIGN KEY(beer)
REFERENCES Beers(name)
ON DELETE SET NULL
ON UPDATE CASCADE;
