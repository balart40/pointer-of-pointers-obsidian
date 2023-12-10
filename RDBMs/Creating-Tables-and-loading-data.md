---
tags:
  - RDBMS
  - database
---

At this point in the course, you know:

- DDL statements, including CREATE, ALTER, TRUNCATE, and DROP, are used for defining objects like tables in a database.
    
- DML statements, including INSERT, SELECT, UPDATE, and DELETE, are used for manipulating data in tables.
    
- Many Relational Database Management Systems (RDBMS) have schemas that contain tables, views, functions, and other database objects.
    
- Most RDBMS provide a GUI through which you can create and alter the structure of tables.
    

You can also create and alter tables by using DDL SQL statements:

- CREATE TABLE. Creates entities (tables) in a relational database and sets the attributes (columns) in a table, including the names of columns, the data types of columns, and constraints (for example, the Primary Key.)
    
- ALTER TABLE. Changes the structure of a table by adding or removing columns, modifying the data type of columns, and adding or removing keys and constraints.
    
- DROP TABLE. Deletes a table from a database.
    
- TRUNCATE TABLE. Removes all rows in a table.
    

There are utilities that help you to manage the movement of data:

- You use the BACKUP and RESTORE utilities to create and recover copies of entire databases, including all objects like tables, views, constraints, and data.
    
- You use the IMPORT utility to insert data into a specific table from different formats, such as DEL/CSV, ASC and IXF, and the EXPORT utility to save data from a specific table into various formats, such as CSV.
    
- You can use the LOAD utilities, instead of INSERT statements, to quickly insert large amounts of data a variety of different data sources into tables.
    
- The Load Data utility is a simple to use interface in the Db2 Web Console.