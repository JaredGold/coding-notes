## Relational Database Model

# What is the relational database model?

A common model used to represent data in a database as a collection of relations.

The **table** defines the **structure** of each relation.

The data is stored as **rows** (called tuples) in the tables, and each row of data represents a real world entity or relationship.

This model was formally defined by E.F. Codd and published in 1969.

# Relational database features

There are three features of the relational model:

1. Structural - How is data actually stored?
2. Integrity - How is the integrity of the data enforced?
3. Manipulative - How can the data be manipulated?

## Structural features - tables, columns, and rows

Data is stored in a table that depicts an n-ary relation, where n is the number of columns.

The columns represent attributes (also called domains or types) of the relation described by the table .

The rows are the data records or tuples that represent the entities stored in the table.

## Keys

Each tuple or record in a table has constraints that must be met for instances of the relation to be valid

Every row has a **candidate key**, which is just a unique identifier for the tuple (all tuples must be uniquely identifiable)

A **primary key** is typically declared and can consist of one or more attributes (columns)

A **foreign key** is an attribute (column) in one relation (table) that serves as a candidate key in another relation (table)

##  Integrity features - entity and referential integrity rules

**Entity integrity rule**

Every tuple (record or row) in a table must have a non-null, unique identifier

- Primary keys cannot be NULL
- Primary keys must be unique

If you try to insert a record into a table with a null primary key, you will get a not-null constraint violation error.

If you try to insert a record with a primary key that matches an existing record, you will get a unique constraint error.

**Referential integrity rule**

If a relation refers to a key attribute of another (or the same) relation, that key element must exist.

In other words - if a row contains a foreign key for another record, that other record must exist.

If you try to add a record with a foreign key that cannot be found, or try to delete a record with a foreign key used in another table, you will get a foreign key constraint error.

**Why do you care?**

As a programmer, you should do your best to communicate how the data of your application can be used

- Guide the user to provide valid data
- Prevent the user from performing invalid operations on data
- The database will stop you from breaking the basic constraints with errors, but the errors will not make sense to the user
- Be prepared to handle constraint errors in your applications

## Manipulative features - select, insert, update, delete

The manipulative features of relational databases provide the ways we access and modify the data.

**Select**

Returns a relation containing all tuples (records) that meet some condition. In PostgreSQL, we use the SELECT statement for this, with optional clauses to limit the results.

Examples:

- SELECT * from items WHERE name = ‘ducky’;
- SELECT * from items WHERE price < 10.00 LIMIT 10;
- SELECT name from items;
- SELECT quantity, item from orders;

**Insert**

Add rows to a table with INSERT.

Example: 

INSERT into items
values (‘frog’, ‘great jumper’, 5.00);

**Delete**

Remove rows from a table with DELETE.

Example:

DELETE from items
WHERE name = ‘ducky’;

**Update**

Update rows in a table with UPDATE.

Example: 

UPDATE items
SET price = 4.50 WHERE name = ‘frog’;