# Database Relationships

An association between entities is called a relationship

Relationships define the way that records in on table relate to records in another table

#### Store

Going off of the store example

How is a customer associated with an order

* A customer places an order

How is an item associated with an order?

* An order contains at least one item



### Relationship cardinality and ordinality

Cardinality expresses the maximum number of one entity with which an entity relates

* An order is made by one customer (one)
* An order can contain many items (many)

Ordinality expresses the minimum number of on entity with which an entity relates

* A customer can have 0 orders (options relation)
* An order contains at least one item (mandatory relation)



#### One to One

If we separate addresses from customers, into a separate address

* A customer has one address
* An address belongs to one customer

#### One to many

The relationship between customer and order is one to many

* An order has exactly one customer
* A customer can have 0 or more orders

#### Many to many

* An order can have many items (and at least one item)
* An item can belong to many orders (or no orders at all)



# Relationship Symbols

![symbols of database relationships](.\img\symbols of database relationships.JPG)

* A customer has exactly one address. An address belongs to exactly one customer
* An order belongs to exactly one customer. A customer may place 0 or more orders
* An order has at least one item. An item can belong to 0 or more orders



---

# Entity Relationship Diagrams

#### Physical ERD

The physical ERD shows the way data is physically modeled in the database and can include: 

* Attribute types
* Keys and constraints
* Relationships

It represents the **schemas** for the database tables and can be used to directly inform how the tables should be created



#### ERD Tools

* Smartdraw and Lucid chart are two licensed options

* Diagrams.net is free



## When do you create an ERD?

* Entity relationship diagrams are a part of the design process, so they are created before implementation
* Some or all optimization (including normalisation) of the data model may be done before physical ERD's are created
* In some cases, an ERD is created from a database, as when designing the refactor of an existing code base and database



#### Foreign Keys

Foreign keys are attributes from one table referenced in a related table

They create relationships between tables

* `customer_id` in addresses refers to a tuple (row) in the customers table (an address belongs to one customer)

* `postcode` in addresses refers to a row in the postcodes table (an address has exactly one postcode, and a postcode can belong to many addresses)

  ![diagram](.\img\diagram.JPG)