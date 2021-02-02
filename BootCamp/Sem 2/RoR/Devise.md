# Devise

https://github.com/heartcombo/devise

There are a lot of authorization services which we can pay to use but may as well save money for smaller applications. Due to us using Ruby and Rails we can use a common gem known as Devise for authorisation.

## To install & Set up Devise 

1. Add `gem 'devise'` to the gem file

2. In terminal use `rails g devise:install`

3. Follow steps given in terminal

4. Then in terminal `rails g device modelname`

5. Check the model you just created and add any symbol you'd like to use for login

6. Check the migration file

7. To create a user name instead of email to the login run in terminal `rails g migration AddUsernameToUser username:string`

8. To then add the Username param to devise you must add the below to the Application controller (read more in docs):

   ```ruby
     before_action :configure_permitted_parameters, if: :devise_controller?
   
     protected
   
     def configure_permitted_parameters
       devise_parameter_sanitizer.permit(:sign_up, keys: [:username])
     end
   ```

9. Then update the views/devise/registration/new to include the new paramater

   ```erb
     <div class="field">
       <%= f.label :username %><br />
       <%= f.text_field :username, autofocus: true %>
     </div>
   ```



### Add Helper Methods

To add some helper methods you want to find some settings first in `config/initializers/devise.rb`

This is where you can change a lot of default settings like how long timout will take.



### Basic Navbar

In `app/views` create a `/shared` directory and then a `_navbar.html.erb` partial

```erb
<nav>
  <% if user_signed_in? %>
    <span class="nav-greeting"><%= "Welcome back, #{current_user.username}" %></span>
    <%= link_to "Sign Out" destroy_user_session_path, method: "delete" %>
  <% else %>
    <%= link_to "Sign In" new_user_session_path %>
    <%= link_to "Sign Up" new_user_registration_path %>
  <% end %>
</nav>
```

Then add `<%= render "shared/navbar" %>` to the `application.html.erb` or similar file