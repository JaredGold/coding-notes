# Rails Routes

HTTP is a set of rules of how messages are formatted, transmitted and responded to.

---

## HTTP Methods

- GET -> Retrieve a resource (read)
- POST -> Create a resource
- PUT/PATCH -> Update a resource
- DELETE -> Delete a resource

CRUD operations.

Every time you receive a website you are doing a GET request.

Whenever you want to add more information (forms or posting) is a POST request.

PUT/PATCH is used when we edit information that is already on the server. Editing a post or changing a password.

You use DELETE to remove something from the server.

---

## Why Routes

- The content of the website should be organized in multiple URLS.

- Different URL's and different HTTP methods require different routes

- Routing is needed whenever we want to use a URL in our app

## How does Rails work?

![Rails Architecture](img\Rails Architecture.JPG)



#### Steps of the process

##### Client sends an HTTP request

- The user types the URL into the browser. The server then reads the path and looks for a route.
- The first route that matches is the on that it uses.
- Actually every time we type a URL and press enter or we click on a link, an HTTP request is sent to the server

##### Routes connects URLS to controller actions

- The rails server finds the route that matches the HTTP method and path, and directs the request to the associated **controller action** an HTTP request.
- Routes are defined in the config/routes.rb file and map HTTP verbs and paths to controller actions.
- Controller actions are another name for controller methods and they are found in the controllers source code

##### Controller executes actions and renders view

- In the controller action, the controller gets information from the model and provides the information to the view via instance variables.
- The controller renders the view with the appropriate information from the model, and that rendered content is sent to the client (the browser viewed by the user).
- By default the view it renders is in the views directory and has a name that matches the controller action.



## Defining the route

There are a few ways to define a route in config/routes.rb

This is one of the ways to specify a route.

`HTTP_verb 'path' to: 'controller_name#action_name'`

Example:

`get 'orders' to: 'orders#index'`



### Action, route and view conventions

| User Action     | Controller Action | Route                             | View                                     |
| --------------- | ----------------- | --------------------------------- | ---------------------------------------- |
| List all orders | order#index       | get 'orders' to: 'orders#index'   | views/orders/index.html.erb              |
| Show one order  | orders#show       | get 'orders/:id' to:'orders#show' | views/orders/show.html.erb               |
| New Order Form  | orders#new        | get 'orders/new' to: 'orders#new' | views/orders/new *THIS PART WAS BLOCKED* |

The route tells the rails server what to display when the user just types in the server url with no additional path - it's the home or index of the application itself.

The root route is specified in the config/routes.rb with the syntax:
`root to: 'controller#action'`

---

# Practice

- `rails g controller cafe` the `g` stands for generate. `rails generate controller cafe`

#### Embedded Ruby (erb) files

The syntax for referring to ruby code within an erb file is:

- `<% %>` Code to execute goes within these special brackets
- `<%= %>` The way we do string interpolation in erb

**<u>refer to files in folders \controllers, views\cafe,  config\routes.rb</u>**

#### routes.rb

```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  root to: 'cafe#index'
  get '/home', to: 'cafe#index'
end
```

#### cafe_controller.rb

```ruby
class CafeController < ApplicationController
  
  class MenuItem
    attr_reader :name, :price
    def initialize(name, price)
      @name = name
      @price = price
    end
  end

  def index
    @menu = [
      MenuItem.new("latte",4.00),
      MenuItem.new("espresso",2.50),
      MenuItem.new("cappucino",5.00),
      MenuItem.new("tea",2.00)
    ]
  end

end
```

#### index.html.erb

```ruby
<h1>Welcome to Coder cafe</h1>

<table>
  <tr>
    <th>Name</th>
    <th>Price</th>
  </tr>
  <% @menu.each do |item| %>
    <tr>
      <td> <%= item.name %> </td>
      <td> <%= "$%.2f" % item.price %> </td>
    </tr>
  <% end %>
</table>
```

#### application.html.erb

```ruby
<!DOCTYPE html>
<html>
  <head>
    <title>Routing Cafe</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

---

# Rails Scaffolding

`rails new scaffold_cafe -d postgresql`

`rails g scaffold Order item:string quantity:integer` - Creates a `localhost:3000/orders` which asks for an item which is a string and an amount of it.

`rails routes` shows all of the routes (GET, POST, PATCH, PUT, DELETE...)

**Scaffolding is not good during training as it does all the work for you**