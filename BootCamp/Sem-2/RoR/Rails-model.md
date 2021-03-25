# Model

* Represents data in our application
* Allows us to access our database using Ruby methods
* Represents models and their data
* Represent associations between these models
* Validate models before they get persisted to the database
* Perform database operations in an object-oriented fashion

## Syntax

`rails g model <model name (singular pascal case)> <column_name:data_type{size} | {size,precision}>`

* `g` or `generate`
* Model name can be PascalCase or snake_case
* Model name must be singular
* Multiple columns can be added separated by a space
* Size and precision are optional
* If you don't set a type the default is string

##### Example

`rails g model User name:string{30} age:integer`



# In Code

#### Migrate

To find where the migration file is it can be found in `db>migrate`

To use the migration file use `rails db:migrate`

This tells rails to create the database and migrate



#### Class

To find the class you use `app > models > name.rb`



# CRUD

#### Create

```ruby
user = User.create (name: 'Eddie', age: 31)

user = User.new
user.name = 'Eddie'
user.save
```

* Create will call new and save
* New will instantiate an object without saving
* Can be created from a hash
* Methods named after columns are added for you
* Save will save the model to the database



#### Read

```ruby
users = User.all

user = User.first
second = User.find(2)
eddie = User.find_by(name: 'Eddie')
```

* All will load every row in the users table
* Array like collection returned
* First will load the first entry (.last will work to)
* Find by index
* Find by attribute/ column



#### Update

```ruby
user = User.find_by(name: 'Eddie')
user.name = 'Ed'
user.save

user = User.find_by(name: 'Eddie')
user.update(name: 'Ed')
```

* attr_writer for each column
* Need to call save to change the database
* Shorthand version with update
* Can also use a hash to update multiple values



#### Delete

```ruby
user = User.find_by(name: 'Eddie')
user.destroy

User.destroy_by(name: 'Eddie')
User.destroy_all
```

* Removes a value from the database
* You can delete records in bulk



# ActiveRecord Associations

### Has One Relationship

#### belongs_to:

* Must be singular
* Is on the model with the foreign key
* Associated through `supplier_id`

#### has_one:

* Naming is singular
* One to One
* Associated through `supplier_id` on Accounts table

![has_one](C:\Users\New\Desktop\Coder-Academy\coding-notes\BootCamp\Sem 2\Database\img\has_one.JPG)



### Has Many Relationship

#### belongs_to:

* Must be singular
* Is on the model with the foreign key
* Associated through `author_id`

#### has_many:

* Naming is plural
* One to many
* Associated through `author_id` on Books table

(THE IMAGE ABOVE BUT has_one is changed to has_many)



```ruby
a = Author.create(name:'Stephen King')
b = Book.create(title:'it', author: a)
a.books.create(title:'saloms lot')
```



### Has Many Through Relationship

* Uses another table

#### appointments

* Many to Many
* Doctor can query Patients with `patient_id`
* Patient can query Doctor with `doctor_id`

#### through:

* Must be declared after has many
* Creates a reference through another table

<img src="C:\Users\New\Desktop\Coder-Academy\coding-notes\BootCamp\Sem 2\Database\img\has-many-through.JPG" alt="has-many-through" style="zoom:50%;" />

```ruby
doctor = Doctor.create(name: 'Dr Suess')
patient_one = Patient.create(name: 'Ted')
appoint = Appointment.create(doctor: doctor, patient: patient_one)

doctor.patients.create(name:'Greg')
```



### Polymorphic Relationship

#### polymorphic

* Many Forms
* Can belong to multiple models

#### Reviewable

* Uses `able` suffix as convention
* as: reference the polymorphic name
* References a row through `reviewable_id`
* References a table through `reviewable_type`

<img src="C:\Users\New\Desktop\Coder-Academy\coding-notes\BootCamp\Sem 2\Database\img\polymorphic.JPG" alt="has-many-through" style="zoom:50%;" />

##### Creating a polymorphic book

```ruby
rails g model review reviewable:references{polymorphic} comment:string
```



```ruby
b = Book.first
b.reviews.create(comment: 'it''s pretty good')

a = Author.first
a.reviews.create(comment: 'Meh')

Review.all
pp Review.all
```



# ActiveRecord Migrations

`rails db:rollback` to rollback changes from a migrations

`rails generate migration AddPriceToBooks price:integer` to update the current migration (add a new column)

`rails generate migration AddDetailsToBooks rating:integer description:text` it is okay to add multiple columns

`rails generate migration AddAuthorRefToBooks author:references` creates a reference

`rails g migration RemoveRatingFromBooks rating:integer` removes a column

##### Schema

Represents the current version of the rules to create a database. All changes should be done through migration and not touched.



#### Change Methods

* add_column
* add_foreign_key
* add_index
* add_reference
* add_timestamps
* change_column_default (must supply a `:from` and `:to` option)
* change_column_null
* create_join_table
* create_table
* disable_extension
* drop_join_table
* drop_table (must supply a block)
* enable_extension
* remove_column (must supply a type)
* remove_foreign_key (must supply a second table)
* remove_index
* remove_reference
* remove_timestamps
* rename_column
* rename_index
* rename_table



# Rails Model Methods

## Validation

To check a validation we open up the model and create a validation.

To find the model it can be found in `app > models`

Then we can create the validates method

To find an error we use `name.errors.full_messages`



##### Below validates that a title is required

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
end
```



##### Below validates length

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
   validates :description, length: {minimum: 10, 
       too_short: "%{count} is the minimum number of characters"}
end
```

or

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
   validates :description, length: { in: 10..100 }
end
```



##### Below validates numbers

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
   validates :description, length: { in: 10..100 }
   validates :price, numericality: { only_integer: true }
end
```

or

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
   validates :description, length: { in: 10..100 }
   validates :price, numericality: { greater_than_or_equal_to: 0 }
end
```



## Scopes

Specify commonly used queries

```ruby
class Book < ApplicationRecord
   validates :title, presence: true 
   validates :description, length: { in: 10..100 }
   validates :price, numericality: { greater_than_or_equal_to: 0 }
   scope :bargain, -> { where(price: 0..500) }
end
```



This allows you to search for books that are cheap for example

```ruby
Book.where(price: 0..500)
Book.bargain
Book.where(sold:false).bargain
```

