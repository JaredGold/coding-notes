# Intro to Databases

#### Data

A collection of facts.

* Raw
* Unfiltered
* Unrelated
* Material that can be any format
  * text
  * images
  * numbers
* meaningless

#### Information

* Consists of collected and related data that has been analyzed
* Delivers meaning

#### Relational Databases

* Relational databases organize data in tables with rows and columns

* The <u>table</u> represents a **relation** because it defines the ways that the data relates as information

* The <u>columns</u>  indicate **attributes** (also known as domains or types) for the data

* The <u>rows</u> (also called **tuples**) represent individual records in the table

  

  ​															**Products**

| name  | description      | price |
| ----- | ---------------- | ----- |
| ducky | Rubber duck      | 5.00  |
| kitty | Small cat statue | 8.00  |

#### Nonrelational databases

* Data is organized as a collections of documents
* Compared to relational databases, collections are like tables and documents are like rows
* Attributes for data are defined (like columns for relational databases), but are loosely structured

```ruby
{
    name: 'ducky',
    description: 'Rubber duck',
    price: 4.00
},
{
	name: 'kitty',
    description: 'Small cat statue',
    price: 8.00,
    discount: .10
}
```



# Relational databases

* PostgreSQL
* MySQL
* Microsoft SQL server
* Oracle Database Cloud

#### PostgreSQL

We use this in the course because it is free and open source as well as well documented and supported by many platforms. It is also the industry standard for rails



#### Database design

First step when modeling data is 

* Define entities
* Define attributes
* Define relationships between entities



#### Entities and attributes

When we model a problem or a situation, we have to define the entities and their attributes.

A good example for this would be store.

* Items *(entity)*
  * Name *(attribute)*
  * Description
  * Price
* Customers
  * Name
  * Email
  * Address
* Orders
  * Date
  * Customer
  * Items with quantities
  * Total price



#### Primary Key

One or more columns (attributes) that uniquely identify a record in the table

* Items
  * Item name
* Customers
  * Email
* Orders
  * Unique id



#### How does this look in a relational database?

* Each entity has a table
* Each attribute is a column in the table
* Instance of each entity are rows in the table

You underscore the category that has the primary key

##### Items

| <u>name</u> | description      | price |
| ----------- | ---------------- | ----- |
| ducky       | rubber ducky5.00 |       |

##### customers

| name   | <u>email</u>    | address         |
| ------ | --------------- | --------------- |
| Shazza | shazz@gmail.com | 123 fake street |

##### orders

| <u>id</u> | date     | customer | items   | total_price |
| --------- | -------- | -------- | ------- | ----------- |
| 1001      | 4/1/2021 | shazz    | 2 ducky | 10.00       |



## Refinement of the data model

* Once an initial data model is designed, it is refined to remove any anomalies and to improve query efficiency (normalization)
* For example, consider these questions:
  * What would happen if we deleted a customer from the customers table and there were orders for that customer in the order table?
  * How would you edit the items in an existing order?
  * How would you make sure the addresses have all of the required information?
  * Should the customer addresses be stored with the orders for shipping purposes?
* Answers later -



# Database design

Database design is a whole heap of skills all about accessing data efficiently, and without errors.

One of the key processes in database design is normalization.



#### Goals of normalization

* Minimize duplication (same data in two tables or two columns)
* Maintain data integrity by avoiding modification anomalies
  * Update anomaly occurs when an attribute is updated in one table but not all tables
  * Delete anomaly occurs when only part of an entity is deleted
  * Insert anomaly occurs when we try to insert data into a missing record
* Simplify queries



#### Normal forms

We normalize our table schema (our table structure) so that our tables become less prone to modification anomalies, separate concerns by purpose or topic, and to make it easier for us to query the data

There are 3 basic normal forms, and each one is built on the previous



### 1. First Normal Form (1NF) Rules 

* Column names must be unique
* Order of records does not matter
* **Records in one column must be of same type**
* **Must have atomic values in columns (single values)**

##### Customers (BAD)

| name        | email          | address                           |
| ----------- | -------------- | --------------------------------- |
| Sharon Teel | sharon@abc.com | 5 Simpson Way, Brisbane, QLD 4000 |

##### Customers (GOOD)

| name        | email          | street_number | street_name | suburb   | state | postcode |
| ----------- | -------------- | ------------- | ----------- | -------- | ----- | -------- |
| Sharon Teel | sharon@abc.com | 5             | Simpson Way | Brisbane | QLD   | 4000     |



<u>**Another Example**</u>

| date      | customer    | items            | total_price |
| --------- | ----------- | ---------------- | ----------- |
| 4/15/2020 | Sharon Teel | 2 ducky, 1 kitty | 20.00       |

Too many changes if you must tweak one item

|   date    |  customer   | quantity | item_name | item_price |
| :-------: | :---------: | :------: | :-------: | :--------: |
| 4/15/2020 | Sharon Teel |    2     |   ducky   |    5.00    |
| 4/15/2020 | Sharon Teel |    1     |   kitty   |   10.00    |



### 2. Second Normal Form (2NF) Rules

* Table is in 1NF
* All columns depend on the table's primary key

Ask the question: Does this column describe what the primary key identifies? If no, it belongs in another table.

*Using the above Customer table*

##### Addresses

|  id  | street_number | street_name |  suburb  | state | postcode | customer_id |
| :--: | :-----------: | :---------: | :------: | :---: | :------: | :---------: |
| 1001 |       5       | Simpson Way | Brisbane |  QLD  |   4000   |      1      |

##### Customers

| customer_id |    name     |     email      |
| :---------: | :---------: | :------------: |
|      1      | Sharon Teel | sharon@abc.com |

Each table has a single purpose.



### 3. Third Normal Form (3NF) Rules

* Table is in 2NF
* Contains only columns that are non-transitively dependent on the primary key

Here, state depends on postcode, and postcode depends on the primary key (address id)

3NF reduces the chances for update anomalies.

##### addresses

| id   | street_number | street_name | suburb   | postcode | customer_id |
| ---- | ------------- | ----------- | -------- | -------- | ----------- |
| 1001 | 5             | Simpson Way | Brisbane | 4000     | 1           |

##### postcodes

| postcode | state |
| -------- | ----- |
| 4000     | QLD   |



## Too much normalisation?

There can always be too much normalisation

* Identify areas of risk of anomalies considering your use of the data and use normalisation to eliminate them
* Consider how you will query and use the data, and use normalisation to make it easier and faster
* Going overboard can lead to unnecessary tables and complicated relationships that make queries time consuming.