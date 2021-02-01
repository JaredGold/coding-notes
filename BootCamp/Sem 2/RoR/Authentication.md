# Authentication

## What is authentication

Authentication is the process of determining whether someone or something is, in fact, who or what it declarers itself to be.

Authentication is very important because it allows our applications to verify and serve resources to a particular user. And it is something we are all very familiar with.

##### Common authentication methods

<u>Session/cookie</u>

A session is saved in memory on the server, in an external database, or something directly on a cookie. The cookie either references the session or holds it entirely, and is sent with the request.

<u>Token</u>

A token is generated on the server, and then saved on the client side. It's sent back as part of the HTTP request from the client and is verified with a secret on the server.

<u>OAuth</u>

Outside authentication is when a third party service (Facebook, Google, Twitter, etc) is used to login. It may also use a session or token hbehind the scenes



### Session Authentication

Starts with a post request (/user/login). Usually with a user name and a password stored in a body hash. This then goes to the server.

It then sends the cookie back to the browser. Then any time the user requests a new page the cookie is sent to the server and then returns back the correct information.

**Pros:**

* Simple implementation
* Small session can be stored on the cookie
* Cookies are much more secure than they used to be

**Cons:**

* Difficult to scale (good for small applications)
* Issues with multiple domains



### Token Authentication

Starts similar to the Sessions with a post request of the /user/login with a body and password. The server then creates something with a secret key. This can be a JWT Jason Web Token. It then sends it back to the browser.

It then constantly sends the authentication request with the JWT in the header. It then checks that the signature has not been tampered with before returning the file.

**Pros:**

* Better scalability as token is stored on the client
* No issue with domains as token is stored in HTTP request header

**Cons:**

* More complex implementation
* Security issues around storing token



# Practical Code Along

https://github.com/JaredGold/rails-diy-auth

<u>**Using Session Authentication**</u>

To access the authentication you would do this in the home function or route. 

You add to them the same way you add to any hash. For example `cookies[:fave_food] = "pizza"` would push a cookie with the fave_food key and the value of pizza.

To create a counter you could use cookies like this:

```ruby
  def home
    cookies[:count] = cookies[:count] ? cookies[:count].to_i + 1 : 1
    @count = cookies[:count]
  end
```

```erb
<p>You have visted <%=@count%> times</p>
```

Even if you turn off the server the cookie remains saved to the browser.

Cookies are not good to use for important, private or critical information because java script can access it, as well as the dev tools.



#### Horrible Auth Method `(DON'T USE LITERALLY)`

*(Could be wrong about not using this is pretty secure)*

The best way to securely store a password is bcrypt

To create a good user and password first in the gem file uncomment the `gem bcrypt`
Then create the scaffold using `rails g scaffold User email:uniq password:digest`

The data type makes sure that there is only one of it's type for example you could not make 2 accounts using the same email address.

Digest creates an encrypted string for the password instead of the users password as well as creating a 2 step password confirmation when creating a login.

The model for user gets a `has_secure_password` in it.

Because the model has `has_secure_password` we are able to use `.authenticate()` as a method to authenticate.

(bit all over the place) `||=` or equals says if I have not assigned something to this assign it or move on.

<u>**routes.rb**</u>

```ruby
Rails.application.routes.draw do
  resources :users
  root 'pages#home'
  get '/signup', to: 'users#new', as: 'signup'
  get '/signin', to: 'sessions#new', as: 'signin'
  post '/signin', to: 'sessions#create', as: 'create_session'
  get '/signout', to: 'sessions#destroy', as: 'signout'
  get '/restricted', to: 'pages#restricted', as: 'restricted'
end
```

<u>**sessions_controller.rb**</u>

```ruby
class SessionsController < ApplicationController
  def new
  end

  def create
    user = User.find_by_email(params[:email])
    if user && user.authenticate(params[:password])
      session[:user_id] = user.id
      redirect_to root_url, notice: "Successfully logged in"
    else
      flash.now[:alert] = "Incorrect email or password"
      render "new"
    end
  end

  def destroy
    session[:user_id] = nil
    redirect_to root_url, notice: "Signed out!"
  end
end
```

<u>**pages_controller.rb**</u>

```ruby
class PagesController < ApplicationController
  before_action :authenticate_user, only: [:restricted]
  def home
    cookies[:count] = cookies[:count] ? cookies[:count].to_i + 1 : 1
    @count = cookies[:count]
  end

  def restricted
  end
end
```

<u>**application_controller.rb**</u>

```ruby
class ApplicationController < ActionController::Base
  helper_method :current_user, :authenticate_user
  def current_user
    if session[:user_id]
      @current_user ||= User.find(session[:user_id])
    else
      @current_user = nil
    end
  end

  def authenticate_user
    if session[:user_id]
      return true
    end

    redirect_to signin_path, alert: "You shall not pass!"
  end
end
```

**<u>home.html.erb</u>**

```erb
<% if current_user %>
  <p>Logged in as <%= current_user.email %></p>
  <%= link_to "Sign out", signout_path %>
  <% else %>
  <%= link_to "Sign In", signin_path %>
  <%= link_to "Sign Up", signup_path %>
<% end %>

<div class= 'notice'><%= notice %></div>

<h1>Welcome</h1>
<p>Welcome to my site. You have visted <%=@count%> times</p>
```

**<u>new.html.erb</u>**

```erb
<p class="alert-message"> <%=alert%> </p>

<%=form_with url: create_session_path, local: true do |form| %>
  <div class='form-field'>
    <%= label_tag :email  %>
    <%= text_field_tag :email %>
  </div>
  <div class='form-field'>
    <%= label_tag :password  %>
    <%= password_field_tag :password %>
  </div>
  <div>
    <%= submit_tag "Sign-in"  %>
  </div>
<%end%>
```

https://github.com/JaredGold/rails-diy-auth

https://github.com/JaredGold/rails-diy-auth