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



#### Partials

A partial is a chunk of html that you only have to type once and then is shared among all the pages. For example a nav bar may be the perfect use of this.

A partial that will be used by more than one part of the project you put in a new directory in views called `shared`

To specify a file that is a partial you use an underscore before the file name. Using the nav example `_nav.html.erb`

To render the partial you do so as seen here `<%= render partial: "shared/nav" %>`

To render a partial in the same folder and pass information to it you do so as seen here 
`<%= render partial: "card", locals: {project: project} %>`

If you want the partial to affect the whole project you do this in the `application.html.erb` parent file in views/layouts.

If you want the partial to affect only one page you create the file in the views/projects directory.



#### Images/assets

Images are stored in the folder `assets/images`

to render the image we use `image_tag` this takes a path `asset_path("image.jpg")` for example: 
`<%= image_tag asset_path("cat.jpg") %>` 

to change the size you can add `width:` and the size. for example:
`<%= image_tag asset_path("cat.jpg"), width: "300px" %>`