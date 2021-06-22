# Rails API Intro

The way we start this API is by running `rails new name --api` you can also add `-d=postgresql` if you wanted to make it a postgresql database.

When you open the created file you can see that it is very similar to what we covered in previous projects withh rails. The way to distinguish that this is indeed in API mode is by going into 
`app > controllers > application_controller.rb` and checking that it is indeed pulling from the API action controller.

You can also check in `config > application.rb` you should see `config.api_only = true`

## Database

We use our models and migrations the exact same way we did before. The below will act like we are making an API for jokes.

`rails g model Category name:string` - will create a migration with a model file named category which takes a name of string.

`rails g model Joke body:text category:references` - this creates a model named joke which takes a body of type text and  references the category table.

It is important to remember you need to pass inside of the category model `has_many :jokes`

then `rails db:create` and `rails db:migrate`

At this point you could create some seeds

```ruby
joke_categories = ["Puns", "Programming", "Knock Knock", "Limericks"]

if Category.all.length == 0
    joke_categories.each do |category|
        Category.create(name: category)
        puts "Created #{category} category"
    end
end
```

Then you can run rails `db:seed`

It is always good to first work inside of the console so I would reccomend running a `rails c` and then create a joke using `Joke.create(category_id: 1, body: "I tried to sue the airline for losing my luggage. I lost my case")`

It may be worth while to check if it is actually working by running a `Joke.first.category.name` to make sure the relation is still working.

## Routes

This is not an API yet as we need to first create a routes.

Inside of the routes.rb we will creat the routes file.

```ruby
Rails.application.routes.draw do
    scope '/api' do # this forces everything under to be /api/...
        get '/jokes', to: 'jokes#index'
        post '/jokes', to: 'jokes#create'
        get '/jokes/:id', to: 'jokes#show'
        put '/jokes/:id', to: 'jokes#update'
        delete '/jokes/:id', to: 'jokes#destroy'
        get '/jokes/random' to: 'jokes#random'
    end
end
```

We can test these routes with `rails routes -g jokes`

