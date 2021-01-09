# Rails Controllers

A controller is the middle man between the model/data and the view.

The controller manages the requests sent to application and the responses sent back to the client.

## Conventions

* `projects#index` index is used as the initial load
* `projects#show` show is for sending back a singular resource (one project)



#### Create Controller

To create a controller use `rails g controller NAMEHERE`. This will create all that you need to make a controller	

#### How Routes Work

In the routes file we are basically saying when the user sends a get request for the url ending in `/projects` run in the projects controller the function `index`. We create this function inside the controller that we used above.

`get "/projects", to: "projects#index"`

#### Render

`render` is a keyword/method that can send back a response to the client.

- `render html: "<h1>hello word</h1>".html_safe` will render the code as html
- `render plain: "hello world"` returns plain text
- `render json: { message: "hello world" }` returns json files



#### Routes for one controller

To get one controller's routes in terminal write `rails routes -c NAMEOFCONTROLLER`

# LOST ALL NOTES DUE TO BSOD BELOW IS CODE



#### routes.rb

```ruby

```



#### projects_controller.rb

```ruby

```



#### projects.json

```ruby

```





#### POSTMAN post request

`localhost:3000/projects?id=3&name=portfolio app&github_status=true`