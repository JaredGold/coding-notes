# Rails API - User and Auth

#### Configure Knock

First thing we have to do is configure the Knock gem. To do this we open the cors.rb file in `config>initializers`. We need to uncomment the `Rails.application.config....`

We need to add more origins inside.

```ruby
Rails.application.config.midddleware.insert_before 0, Rack::Cors do
	allow do
    	origins 'localhost:3000', 'localhost:3001','127.0.0.1:5050'
        
        resource '*',
        headers: :any,
        methods: [:get, :psot, :put, :patch, :delete, :options, :head]
    end
end
```

From here it is set up and we need to start creating our user Model
`rails g model User username:string email:string password_digest:string` which will make our User model file which we then need to modify.

```ruby
class User < ApplicationRecord
	has_secure_password # Uses a secure password and requires all the below to be unique
	validates :username, presence: true, uniqueness: true
    validates :email, presence: true, uniqueness: true
end
```

`rails db:migrate` to create this user table.

To create a user it would look like this 
`User.create(username: "Jared", email: "jared@test.com", password:"password", password_confirmation:"password")`

We then need to create a controller for the users using `rails g controller Users`

Inside of the users controller we want to create a creation method.

```ruby
class UsersController < ApplicationController
	def create
		@user = User.create(user_params)
        if @user.save
            render json: @user, status: :created # or 201
        else
            render json: @user.errors, status: :unprocessable_entity
        end
	end
    
	private
    def user_params
       params.permit(:username, :email, :password, :password_confirmation) 
    end
end
```

Once this method is created we then need a route to create this.

```ruby
Rails.application.routes.draw do
    scope '/api' do # this forces everything under to be /api/...
        get '/jokes', to: 'jokes#index'
        post '/jokes', to: 'jokes#create'
        get '/jokes/:id', to: 'jokes#show'
        put '/jokes/:id', to: 'jokes#update'
        delete '/jokes/:id', to: 'jokes#destroy'
        get '/jokes/random' to: 'jokes#random'
        #Above is old content
        scope '/auth' do
           post '/sign_up', to: 'users#create' 
        end
    end
end
```

In our RestClient we can check if it works

```
### Create user
POST http://localhost:3000/api/auth/sign_up
Content-Type: application/json

{
	"username": "Jared44",
	"email": "jaredDaBomb@test.com",
	"password": "password123",
	"password_confirmation": "password123"
}
```

---

We don't want to be responding with the user json as it has the password_digest as it can still be decrypted although quite difficult. So we should change our users controller

```ruby
if @user.save
	auth_token = Knock::AuthToken.new payload: {sub: @user.id}
	render json: {username: @user.username, jwt: auth_token.token}, status: :created
```

#### Creating the sign in feature

Although we've created the sign up ability we still need a secure way to sign in. The way we do this is through the UsersController

```ruby
class UsersController < ApplicationController
	def sign_in
		@user = User.find_by_email(params[:email])
        if @user && @user.authenticate(params[:password])
            auth_token = Knock::AuthToken.new payload: {sub: @user.id}
			render json: {username: @user.username, jwt: auth_token.token}, status: 200
        else
            render json: {error: "Incorrect Username or Password"}, status: 404
        end
    end
end
```

We then need to create the route.

```ruby
scope '/auth' do
	post '/sign_up', to: 'users#create'
    post '/sign_in', to: 'users#sign_in'
end
```

Then we test it

```
### Sign in with correct details
POST http://localhost:3000/api/auth/sign_in
Content-Type: application/json

{
	"email": "jaredDaBomb@test.com",
	"password": "password123"
}

### Sign in with incorrect details
POST http://localhost:3000/api/auth/sign_in
Content-Type: application/json

{
	"email": "jaredDaBomb@test.com",
	"password": "fakePassword"
}
```

Finally we want to set up the relationship the user has to jokes. We do this by creating a migration to add the user to the jokes:
`rails g migration add_user_to_jokes user:references`
`rails db:migrate`

You may need to drop the database and recreate the database when making this link.

You also need to update the model for joke and user: the joke needs `belongs_to :user` and the user needs to `has_many :jokes`

---

### Setting up this use in the API

We need to use the jokes_controller to set up the api controller. We need the user to be logged in in order to make a joke.

```ruby
class JokesController < ApplicationController
    before_action :authenticate_user, except: [:index, :random, :show]
    before_action :check_ownership, only: [:update, :destroy]
    # We have the above because we are using Knock Authenticatable
    
    def create
        @joke = current_user.jokes.create(joke_params)
        # ...
    end
    
    def check_ownership
       if current_user.id != @joke.user.id
           render json: {error: "You don't have permission to do that"}, status: 401 
       end
    end
end
```

If we take the users JWT and we add it to the header now in the creating a joke. After Bearer wouldd be the users token.

```
### Succesfully posts a joke
POST http://localhost:3000/api/jokes
Content-Type: application/json	### Tell it what type of data and leave a space below
Authorization: Bearer aksjdhakljshgdliahsdilahsddkljhashkljdh

{
	"category_id": 1,
	"body": "The furniture store keeps calling me to come back, but all I wanted was one 	  night stand"
}
```

---

# Reformatting the responses

We want to customise what information we return to our users when they do specific requests. We do this as shown in the Jokes model.

```Ruby
class Joke < ApplicationRecord
	belongs_to :category
    belongs_to :user
    
    def self.find_by_category(input)
        category = Category.find_by(name: input.capitalize)
        return self.where(category: category)
    end
    
    def transform_joke
       return {
           author: self.user.username,
           category: self.category.name,
           body: self.body,
           posted: self.created_at,
           edited: self.updated_at
		} 
    end
end
```

Then inside of the Jokes controller

```ruby
def show
    render json: @joke.transform_joke
end
```

