#  Rails API Random Jokes

Starting this off all we need to do is create a function in our jokes_controller called random

```ruby
def random
    @joke = Joke.all.sample
    render json: @joke, status: 200
end
```

Then if we tried to test this we would get an error for `joke not found` - 404

```
### Random Joke
GET http://localhost:3000/api/jokes/random
```

The reason for this bug is because the routes for show is matching the same as the random. So what it is doing is searching for a joke with the ID of 'random'. We simply need to change the order to fix this. The order is the most important when attempting to scope in routes.

```ruby
get '/jokes/:id', to: 'jokes#show'
# More between
get '/jokes/random', to 'jokes#random'
```

```ruby
get '/jokes/random', to 'jokes#random'
get '/jokes/:id', to: 'jokes#show'
```

---

The way the code is working to get a random joke is by pulling every single joke from the SQL database into an array and then pulling a single joke from that array. This works when the databse is small but as it get's larger this would be poor practice.

The SQL command to find the length of databse you can use `Joke.count`. To get a random value in ruby we can use `rand(10)` which will get 1-9. So if we wanted to mix this up using `rand(Joke.count)`. But again this will be off by one. 

To fix this we can use `offset` like `Joke.offset(2)` which returns all jokes after the second Joke. We can combine this using `Joke.offset(rand(Joke.count)).first` which will give us a random joke.

```ruby
def random
    offset = rand(Joke.count)
    @joke = Joke.offset(offset).first
    render json: @joke, status: 200
end
```

#### Query Params

If we want to add some query paramaters to customise our randdom function we do so by changing the get request like so

```
### Random Joke
GET http://localhost:3000/api/jokes/random?name=alex
```

When this runs you won't receive anything different but passed to the server will be `Parameters: {"name" => "alex"}`. These can be accessed like so -  `params[:name]` If we wanted to use this more effectively to maybe search a category we would do so as below.

```
### Random Joke
GET http://localhost:3000/api/jokes/random?category=puns
```

and then the logic would look like

```ruby
def random
    if params[:category]
        puts "Searching for #{params[:category]}"
    end
    offset = rand(Joke.count)
    @joke = Joke.offset(offset).first
    render json: @joke, status: 200
end
```

Although this works we want to do all of this logic inside of the model as apposed to being inside of the controller. The idea is a fat model skinny controller.

Inside of the model we want to add this logic.

```ruby
class Joke < ApplicationRecord 
    belongs_to :category
    
    def self.find_by_category(input)
        category = Category.find_by(name: input.capitalize)
        return self.where(category: category)
    end
end
```

and then back in the controller.

```ruby
def random
    if params[:category]
        puts "Searching for #{params[:category]}"
        count = Joke.find_by_category(params[:category]).count
        if count == 0
            return render json: {error: "No jokes of that category"}, status: 404
        end
        @joke = Joke.find_by_category(params[:category]).offset(rand(count)).first
    else
    	offset = rand(Joke.count)
    	@joke = Joke.offset(offset).first
    end
    render json: @joke, status: 200
end
```



