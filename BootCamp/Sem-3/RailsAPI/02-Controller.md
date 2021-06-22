# Rails API Controller

## Controller

#### Show all Jokes

First thing we need to do is create the cointroller using `rails g controller Jokes`

```ruby
class JokesController < ApplicationController
   def index
       @jokes = Joke.all # Good in thise case to have a jokes variable
   end
end
```

They key thing to remember is with an API we don't need to render a view we simply need to return a JSON file.

```ruby
class JokesController < ApplicationController
   def index
       @jokes = Joke.all
       render json: @jokes
   end
end
```

## Test Data

You can test that this is working my running `rails s ` and then going to `localhost:3000/api/jokes` - Using a browser is not the best way to be testing this as we wouldn't be receiving this info simply on a browser we would be receiving this information use HTTP requests. We are going to use postman.

In postman you can send a get request to the same URL and receive the same information without any favicon loading issues.

You can also do the above using a VSCode extension called Rest Client. The way this works is by creating a file that describes what the API does. You create the file in the root level with a new file called `client.http`

```
### Index method
GET http://localhost:3000/api/jokes
```

After typing the above you receive a link that says Send Request which gives you all the information you need without using postman.

## Controller

#### Creeate one joke

```ruby
class JokesController < ApplicationController
   def index
       @jokes = Joke.all
       render json: @jokes
   end
    
    def create
        @joke = Joke.create(joke_params)
        if @joke.errors.any?
            render json: @joke.errors, status: :unprocessable_entity
        else
            render json: @joke, status: 201
        end
    end
    
    private
    def joke_params	# parse the data types
    	params.require(:joke).permit(:category_id, :body) 
    end
end
```

To test the above we use postman and pass in the body of a post request

```json
{
    "category_id": 2,
    "body": "Why do programmers give you a gift on Halloween? Because OCT 30 == DEC 25"
}
```

and then again in Rest Client

```
### Index method
GET http://localhost:3000/api/jokes

### Succesfully posts a joke
POST http://localhost:3000/api/jokes
Content-Type: application/json	### Tell it what type of data and leave a space below

{
	"category_id": 1,
	"body": "The furniture store keeps calling me to come back, but all I wanted was one 	  night stand"
}
```

Although this works we also want to make an unsuccesfully posted joke is handled well. We should receive a 422 with a JSON object that says "Category does not exist"

```
### Unsuccesfully posts a joke
POST http://localhost:3000/api/jokes
Content-Type: application/json

{
	"body": "The furniture store keeps calling me to come back, but all I wanted was one 	  night stand"
}
```

#### Show one Joke

```ruby
class JokesController < ApplicationController
   before_action :set_joke, only: [:show]
    ### Removed above for readability
    def show
    	render json: @joke
    end
    
    private
	### removed above for readability
    def set_joke
    	@joke = Joke.find(params[:id])
    end
end
```

Then to test it this time only with the Rest Client. (You don't need to use both)

```
### show joke id: 1
GET http://localhost:3000/api/jokes/1

### unsucessfuly show joke id: 1000 (THIS will currently be html but we change that)
GET http://localhost:3000/api/jokes/1000
```

To catch the error of a joke not found we can change the set_joke

```ruby
def set_joke
	begin
    	@joke = Joke.find(params[:id])
    rescue
        render json: {error: "Joke not found"}, status 404
end
```

#### Update one Joke

```ruby
class JokesController < ApplicationController
   before_action :set_joke, only: [:show, :update] # Included update
    ### Removed above for readability
	def update
		@joke.update(joke_params)

        if @joke.errors.any?
            render json: @joke.errors, status: :unprocessable_entity
        else
            render json: @joke, status: 201
        end
    end
    
    private
	### removed above for readability
	def set_joke
		begin
    		@joke = Joke.find(params[:id])
    	rescue
  	      render json: {error: "Joke not found"}, status 404
	end
end
```

Then to test

```
### succesfully update joke id: 1
PUT http://localhost:3000/api/jokes/1
Content-Type: application/json

{
	"category_id": 2,
	"body": "A programming joke"
}
```

#### Delete one Joke

```ruby
class JokesController < ApplicationController
   before_action :set_joke, only: [:show, :update, :destroy] # Included destroy
    ### Removed above for readability
	def destroy
		@joke.delete
        render json: 204 #no content
    end
    
    private
	### removed above for readability
	def set_joke
		begin
    		@joke = Joke.find(params[:id])
    	rescue
  	      render json: {error: "Joke not found"}, status 404
	end
end
```

Then to test

```
### succesfully delete joke id: 1
DELETE http://localhost:3000/api/jokes/1

### unsuccesfully delete joke id: 1000
DELETE http://localhost:3000/api/jokes/1000
```

