---
tags:
  - PostgresSQL
  - database
  - RDBMS
---
## PostgreSQL RDBMs

- PostgreSQL is an open-source object-relational database management system
- Reliable and flexible
- Supports relational and non relational data types
- Uses include
	- OLTP
	- Data analytics
	- Geographic information systems
### PostgreSQL Options

Download and install on:
- macOS
- UNIX, UNIX-based, and UNIX-like systems 
- Windows

Cloud
- VM images or containers
- Managed services
### PostGresSQL Tools
- psql command line
- pgAdmin
- Navicat, DBeaver
- Cloud vendor tools and APIs
## Creating Databases and loading data in PostgreSQL

The following command create a database using psql

```
CREATE DATABASE employees:
\connect employees;
CREATE TABLE employee_details (firstname VARCHAR(20)),
lastname VARCHAR(20), startdate DATE, salary DECIMAL);
```

To restore data previously backed up

```
psql restored_employees < employeesbackup.sql
```

This recreates
- Tables, other data objects and Data

To backup a data base  you can use the following command

```
pd_dump employees > employeesbackup.sql
```

By default it backs up:
- Schema
- Data
## Views
- Is an alternative way of representing data from one or more tables or other views
- Can interact with views in the same way as you interact with tables
- Use to:
	- Limit access to sensitive data
	- Simplify data retrieval
	- reduce access to underlying tables

## Materialized views
- Behave differently to regular views
- Result set is materializes or saved for future use
- Cannot insert update or delete rows
- can improve perfomance
