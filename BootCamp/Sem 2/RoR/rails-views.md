# Rails Views

The views stores all of the visual information and is controlled and shown via the controller.

When you generate a controller you create a directory in views called the name of the controller. Here is where you store the views for that controller.

The convention for naming a html file in your view folder is the same name as the function (index).



#### Render HTML file

- To render the html file you use render and then the path. e.g.  `render "projects/index"`
- You can also pass a symbol if the file is stored in the correct folder `render :index`
- Finally you can implicitly render by having the view by simply having the same corresponding name as the function. Implicit rendering is the best practice



#### Naming conventions

index = *show all of the resources*

show = *showing 1 of the resources*

new = *to have a form that allows you to create a new resource*



#### Running ruby in erb

In order to run ruby commands using the erb file *(index.html.erb)* we use `<% %>` to execute ruby.

To execute ruby and display on the page we use `<%= %>`



#### link_to

`link_to` allows you to create an `<a>` to the specific item passed after.

A `link_to` has a specific format. It looks as is `link_to TEXT, DESTINATION`

In an example it could look like this `<%= link_to project[:name], project_path(project[:id]) %>`