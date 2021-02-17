# Car Sales
1. Create a car rails project `rails _6.0.3_ new car -d postgresql -T` Don't quote me on that
2. Add rails-rspec to gemfile `gem rspec-rails`
3. Create db
4. run `rails g rspec:install`
5. If rspec is not installed you can run `bundle exec rspec` and it runs it through the project
6. Generate a scaffold `rails g scaffold Listing title description:text price:integer sold:boolean`

## Set up Heroku for deployment
- `heroku login`
- `heroku create name`
- `git push heroku main`
- `heroku rake db:create`

## Day 2
1. Carry on setting the home route to the index page
2. Follow bootstrap install guides on github
3. Going through the docs add what you want to make your website and take from templates
4. Customise the copied styles to your liking
5. Go back to main branch and merge then push to heroku `git push heroku main`

Look into Omni Auth for application to log in using FB, Google, Twitter etc...

6. Install devise using rails docs - https://github.com/heartcombo/devise
7. run `rails g devise:install`
8. Follow the notes that show up after running devise install
9. run `rails g devise User` to created the User model.
10. CHOICE add `before_action :authenticate_user!` to application controller
11. Add logic to log in and log out button
```erb
<% if user_signed_in? %>
  <li class="nav-item">
    <%= link_to "Log Out", destroy_user_session_path, method:"delete", class: "nav-link active" %>
  </li>
<% else %>
  <li class="nav-item">
    <%= link_to "Log In", new_user_session_path, class: "nav-link active" %>
  </li>
<% end %>
```
12. Add new fields for forms if required. in the `new.html.erb` in `views/devise/registration`
