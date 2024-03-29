# 3. Tables and keys
Created Tue Mar 19, 2024 at 9:10 AM

The "relation" word in "Relational databases" is related to "sets and relations" in math. There's a whole algebra called "Relational algebra" that deals with relations.

There are many kinds of databases, including non-relational ones, like graph databases.

## Table
- A table has columns and rows.
- A table is also called a *relation*.
- A column is also called a *attribute/field*.
- A row is also called a *tuple/record*.

An actual instance (i.e. contains data) of a table = set of tuple/rows + a table structure


## Key
A key is a *minimal set* of attributes to uniquely identify a row.

Example: In the customers table, customerId is a key. But \[customerId, customerName] is not a key, because it is not "minimum" even if it's still unique. Something like \[CustomerName, CustomerAddress] is most likely a key, since people with the same names usually don't live at the same place.

Some terms:
- Simple key - a key with only one attribute. Example: customerId
- Compound key - a key with multiple attributes. Example: \[CustomerName, CustomerAddress]
- Candidate key - the set of *all unique* keys that are *possible* for the table.
- Primary key - one of the candidate key that the DB-designer/DBA/dev *chooses* to maintain uniqueness. 
	- Very often a simple key is chosen as the primary key. 
	- It is ensured that PK is not null and unique, reasonably so since it is like an identifier.
	- There should be at-most one PK.
- Entity integrity constraint - the fact that the above three conditions are satisfied.

A subtle detail - PK cannot be null, but other candidate keys may have a null value. So this is the primary diff between PK and candidate keys.

- Alternative/secondary keys - candidate keys that are not PKs.
- Relational schema - info about structure about all tables and integrity constraints that tables have to satisfy.
- Super key - a candidate key U (union) any other attribute. A set. mAID superset. Super key cannot be a null set.
- Foreign key - an attribute that is a primary key in some other table. The other table may be the current table too (self referential).
	- Concept wise, it acts as a pointer to a row in the other table. Example: customer and purchases table, where purchases table has customerId as a attribute.
	- All foreign key values have to exist in the other table, this is checked during row creation in current table. 
	- Advantages of having foreign key:
		- Avoid redundancy
		- Avoid edit inconsistencies, i.e. the row in other table can be changed without worrying about the current table.
	- Self referential foreign keys. Example: a employees table with employeeId, employeeName and managerId. Here managerId is a FK to the employeeId attribute, of the same table, with the CEO having null as managerId.
	- Foreign keys may be null.