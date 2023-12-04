---
tags:
  - MySQL
  - RDBMS
  - SQL
---
## Getting Started with MySQL

- MySQL is a popular open-source RDBMS
- MariaDB is a fork of MySQL
### MySQL Options

- Download and install using
	- **Community** Edition under a GNU License.
	- **Commercial Editions**
- Cloud
	- VM images and containers
	- Managed Service (cloud providers)
### Popular MySQL Tools

- mysql command line
- mysqladmin
- MySQL Workbench
- phpMyAdmin
#### Example of Mysql CLI

```
show databases
```

MySQL Workbench is a desktop application for designing, developing and administering MySQL databases
## Creating Databases and Tables in MySQL

To create databases you can use the `CREATE DATABASE` Command, as shown in the example below:

```
CREATE DATABASE employees;
USE employees;
CREATE TABLE employee_details (firstname VARCHAR(20)),
lastname VARCHAR(20), startdate DATE, salary DECIMAL);
```

To see the configuration of the Data Base you can use 

```
DESCRIBE database_name;
```
## Loading Data in MySQL

To backup data  you can use `mysqldump` utility

```
mysqldump -u root employees > employeesbackup.sql
```

To restore the data you can use `restore`

```
mysql -u root restored_employees < employeesbackup.sql
```

You can restore data as well using the `source`command

```
source employeesbackup.sql
```

To import data file you can use the `load data infile` statement

```
load data infile 'employeesdata.csv' into table employees_details
```

You can also use the mysqlimport utility passing the name of the database that the table resides in

```
mysqlimport employees employees_details.csv
```
## Using keys and constraints in MySQL

### Types of constraints

- Primary Keys
- Foreign Keys
- Unique constraints
- Null Constraints

### Primary Key

- One column or a combination of columns
- Not null
- Unique
- Indexed

Auto Increment
- Automatic generation of incrementing numbers
- 