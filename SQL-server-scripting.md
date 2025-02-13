## Working with SQL Servers
1. Connect to a PostgreSQL Server: `psql -U postgres -h localhost`
2. Create Login
    * Log into SQL Server: `psql postgres`
3. Create Users (After logging in)
    * `CREATE ROLE username WITH LOGIN PASSWORD 'quoted password' [OPTIONS]`
4. Create a Password
    * `\password postgres`
    * Next enter password and confirm it.
5. Create a Role with a password
    * `CREATE ROLE pedro WITH LOGIN PASSWORD 'Starter pack';`
6. Creating and Managing Databases
`CREATE DATABASE databasename;`

### SQL Semantics
* List DB's
    * `\l`
* Choose DB
    * `\c databasename`
* Create a Table
``` sql
CREATE TABLE table_name(
  id int PRIMARY KEY,
  name VARCHAR(30)
);
```

#### Show All Tables in Database
  * List all tables in Database: `\d`
  * Shows table entry structure and types: `\d tablename`
  * Shows all entries inside a table: `SELECT * FROM table;`

#### Find Server Port
``` sql
SELECT *
FROM pg_settings
WHERE name = 'port';
```
* Output: Port number

#### Check Table Schema
``` sql
SELECT table_schema, table_name, column_name, data_type
FROM information_schema.columns
WHERE table_name = 'your_table_name';
```
