# Intro to SQP - psql

psql is postgreSQL for terminal.

There are 3 commands you need to know once PostgreSQL is installed:

- `sudo service postgresql status` for checking the status of your database.
- `sudo service postgresql start` to start running your database.
- `sudo service postgresql stop` to stop running your database.

Alternatively, you can open the psql shell by switching to the postgres user with: `su - postgres` and then entering the command: `psql`.

To exit postgres=# enter: `\q` or use the shortcut key: Ctrl+D

---

## Commands

*https://www.postgresqltutorial.com/postgresql-select/*

* `\l` lists the databases you are connected to
* `\q` or `ctrl+d` exits psql
* `\c` then the name of another database lets you change between databases
* `\dt` lists all tables
* `\d` then the table name shows the column structure of the table (db) *(describe)*
* `drop database name` deletes a database (CAREFUL)
* `\i` then the path to a `.sql` file to load the table/command from a file

## Conventions

* naming must be snake_case
* names must be plural
* column names are snake_case and typically singular

## Create a database

In order to create a database you do so as below. You do not have to list all of these options.

Below is all the options *(default blank)* you can use when creating a new database

```sql
CREATE DATABASE database_name
WITH
	[OWNER = role_name]
	[TEMPLATE = template]
	[ENCODING = encoding]
	[LC_COLLATE = collate]
	[LC_CTYPE = ctype]
	[TABLESPACE = tablespace_name]
	[ALLOW_CONNECTIONS = true | false]
	[CONNECTION LIMIT = max_concurrent_connection]
	[IS_TEMPLATE = true | false]
```

**It is important to end every statement/command with a semicolon**`;`

`create database name;` is how you create a database

### Create Table

The syntax for creating a table is similar with database.

Below `column1` is the name of that column.

https://www.postgresqltutorial.com/postgresql-data-types/ - All the data types

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
	column1 datatype(length) column_constraint,
    column2 datatype(length) column_constraint,
    column3 datatype(length) column_constraint,
    table_constraints
);
```

used version

```sql
create table categories(
	id serial primary key,
    name varchar(100) not null,
    description varchar(1000)
);
```

To reference another table in that table

```sql
create table if not exists items(
	id serial primary key,
    name varchar(100) not null,
    description varchar(1000) not null,
    category_id int,
    foreign key (category_id) references categories(id)
);
```



### Alter table

If you ever want to add, remove or change a column or constraint you need to alter the table structure

* Add a column
* Drop a column
* Change the data type of a column
* Rename a column
* Set a default value for the column
* Add a constraint to a column
* Rename a table

```sql
alter table items
add column price decimal not null;
```

If there is already an item in the table and you have said `not null` it will not let you create that unless you set a default.

```sql
alter table items
add column price decimal not null default 0.00;
```



### Inserting data

* Specify column names in any order and match order of values
* Error if required (not null, primary key) column values are missing

```sql
INSERT INTO <table_name> (COLUMNS)
VALUES
```

```sql
INSERT INTO categories (name, description)
VALUES
	('toys', 'Playthings'),
	('crafts', 'Craft Supplies'),
	('clothes', 'Beautiful things to wear'),
	('electronics', 'Gadgets for living');
```

```sql
INSERT INTO items (name, description, category_id, price)
VALUES
	('doll', 'sweet friend', 1, 0.00),
	('toy car', 'goes fast', 1, 0.00),
	('watercolor paints', 'make beauty', 2, 0.00),
	('dress', 'free fitting', 3, 0.00),
	('headphones', 'noise cancelling', 4, 0.00);
```

You can use `\i` to load it from a file.



### View items in table

Below will show all items from the the item table

```sql
select * from items;
```

Below is more examples

```sql
select name from items;
select name, price from items;
select price, name from items;
```

If you want to filter only items from the toys category or both cat's

```sql
select * from items
where category_id = 1;

select * from items
where category_id in (1,2);
```

You can search stuff similar (fuzzy match). A `%` is saying anything can be before or after that.

```sql
select * from items
where description like '%friend';
```

#### SELECT statement

The `SELECT` statement is used to query a database table. The simplest format of `SELECT` statement is:

`SELECT <list of columns> FROM <table>`

Where `<list of columns>` is either a comma separated list of columns or `*` to select all columns

* Select distinct rows using `DISTINCT` operator
* Sort rows using `ORDER BY` clause
* Filter rows using `WHERE` clause
* Select a subset of rows from a table using `LIMIT` or `FETCH`

`LIMIT 1` will show the first item in that category. `LIMIT 2` Will show the first 2 items...

`WHERE` is used in rails to filter results of a query based on some condition.

#### DELETE statement

```sql
DELETE from table
WHERE <condition>;

DELETE FROM items
WHERE name = 'dress';
```

* It is important to use **single quotes** for string literals in `WHERE` and `INSERT` statements
* All statements must end in a semi-colon