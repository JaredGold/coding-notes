# Complete Rails Dev Guide - DONE LAZy
1. Generate the rails file `rails new name -d postgres`
2. Create the database `rails db:create`
3. Migrate the databse `rails db:migrate`
4. Create tests `rake db:setup`
5. Create a home page controller `rails g controller home page` home is the name of the controller and page is a function.
6. Change root to home page `root: 'home#page'`
7. Install current gems `$ bundle`
8. Install key gems (bootstrap-sass, simple_form, devise) **Read** How to install these.
9. Read components of bootstrap docs (navbar) (copy a navbar)
10. Create a folder called partials in views and create a navbar partial `_navbar.html.erb`
11. Add `<%= render "partials/navbar" %>` to `application.html.erb`
12. Customise the `_navbar` by changing the name and removing unneeded links
13. Add the below to the nav bar to stop log out from appearing when already logged out
```erb
<% if user_signed_in?  %>
  <%= link_to "Log Out", destroy_user_session_path, method: :delete, class: "nav-link" %>
<% end %>
```
14. Wrap everything in the body of `application.html.erb` in a div with the class container
read https://getbootstrap.com/docs/4.0/layout/grid/
15. Using above split into home page into columns
16. Using Jumbotron (search on bootstrap site.) to encompas the columns.
17. Add a home page image to the `app/assets/images` folder
18. Add an `image_tag` linking to the newly uploaded image
Complete code
```erb
<div class="jumbotron">
  <div class="row">
    <div class="col-md-6">
      <h1 class="display-4">Hello, world!</h1>
      <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to
        featured content or information.</p>
      <hr class="my-4">
      <p class="lead">
        <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
      </p>
    </div>

    <div class="col-md-6">
      <%= image_tag "temp-image" %>
    </div>

  </div>
</div>
```
19. Add a class to the `image_tag` given `class: "home-image"` or similar.
20. Customise the image in `application.scss` or `home.scss`
21. Add a scaffold `rails g scaffold Name options`
22. Delete the scaffold.scss file
23. Change the link on the home page to link to the create page ` <%= link_to "Add Update", new_post_path, class: "btn btn-primary btn-lg" %>`
24. Delete items in the form you want to be hidden
25. In the form create of the scaffold_controller add `@menu.user_id = current_user.id` or similar to the hidden field you want auto populated
#### We then need to add an active storage
26. Run `$ rails active_storage:install`
27. `$ rails db:migrate`
28. In the model you want to add an image field add `has_one_attached :picture`
29. Add Picture to the controller in `post_params` add `:picture`
30. Add `<%= f.file_field :picture %>` To the `_form.html.erb`
---
#### A lot after this is styling
- Adding `class="table"` to the `index.html.erb` file instantly makes tables look much better

