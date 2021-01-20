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



