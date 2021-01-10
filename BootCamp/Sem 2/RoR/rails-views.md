# Rails Views

The views stores all of the visual information and is controlled and shown via the controller.

When you generate a controller you create a directory in views called the name of the controller. Here is where you store the views for that controller.

The convention for naming a html file in your view folder is the same name as the function (index).



#### Render HTML file

To render the html file you use render and then the path. e.g.  `render "projects/index"`