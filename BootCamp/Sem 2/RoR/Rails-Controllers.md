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

The prefix shows what exact path you want to follow



#### Private

The private keyword can but put at any point in a controller and basically says any function below it can only be used in that controller and can not be used by any other controller

# LOST ALL NOTES DUE TO BSOD BELOW IS CODE



#### routes.rb

```ruby
Rails.application.routes.draw do
  # localhost:3000/projects
  get "/projects", to: "projects#index"
  # localhost:3000/projects
  post "/projects", to: "projects#create"
  # localhost:3000/projects/5
  get "/projects/:id", to: "projects#show"
end
```



#### projects_controller.rb

```ruby
class ProjectsController < ApplicationController
  before_action :read_projects
  skip_before_action :verify_authenticity_token

  def index
    # send back all of the resources to the client
    render json: @projects
  end
  
  def create
    new_project = { 
      id: params[:id].to_i, 
      name: params[:name], 
      github_status: is_true?(params[:github_status]) 
    }
    @projects << new_project
    write_projects(@projects)
    redirect_to projects_path
  end

  def show
    # show is for sending back only 1 resource
    found_project = @projects.find do |project|
      project["id"] == params[:id].to_i
    end
    render json: found_project
  end

  private

  def is_true?(bool)
    bool == "true"
  end

  def write_projects(projects)
    File.write(Rails.public_path.join("projects.json"), JSON.generate(projects))
  end

  def read_projects
    @projects = JSON.parse(File.read(Rails.public_path.join("projects.json")))
  end
end

```



#### projects.json

```ruby
[{"id":1,"name":"rails project","github_status":false},{"id":2,"name":"terminal app","github_status":true},{"id":3,"name":"react app","github_status":false},{"id":4,"name":"portfolio","github_status":true},{"id":5,"name":"full stack app","github_status":false}]
```





#### POSTMAN post request

`localhost:3000/projects?id=3&name=portfolio app&github_status=true`