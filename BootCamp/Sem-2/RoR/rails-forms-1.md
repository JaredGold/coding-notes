# Rails Forms

## Add/Create a form

To create a form you can do so by following html standards.

Every form by default makes a post request.

To submit a form you need to make the action the route that you need and the method be post. For example:	`<form action= "/movies" method="POST">`
You do not want to hardcode the path and should use the `<%= movies_path %>`

In order to stop "Invalid Authenticity Token" we must add a token field to all of our forms, this look like this: 	`<input type="hidden" name="authenticity_token" value="<%=form_authenticity_token%>">`



## Save to a Session

A session is stored in the cookie or the browser but is max saved to a 4kb file. It is temporary and refreshes every server load. (good for testing)

To create a session you can do so using the example below.

```ruby
def create
    # If the sessions isn't created create and make empty array
   if session[:movies] == nil
       session[:movies] = []
   end
   	# Push the params being to the session 
    session[:movies].push(params[:movie])
    # redirect to movie/:id the id will be the last item in the array (.length)
    redirect_to movie_path(sessions[:movies].length)
end
```



## Show the current form return

To show the return you woudl do so as below

```ruby
def show
	# session[:movies] = ["Avengers", "The Dark Knight"]
    @movie = session[:movies][params[:id].to_i - 1]
end
```

you then would add it to the show.html.erb

```erb
<%= @movie %>
```

or

```erb
<h1>
    <%= @movie["title"] %>
</h1>
<p> Rating <%= @movie["rating"] %> </p>
<%= link_to "back", :back %>
```



#### Create a link to

In order to link to another page you would use a link to form code

```erb
<%= link_to "name", name_path %> # Generic Link
<%= link_to "back", :back %> # Takes the user to the previous page
<%= link_to "edit", edit_movie_path(params[:id]) %> # takes you to the edit path and passes the id param
```



#### Edit (PUT)

To edit a post or similar form you need to send a PUT request. In order to send the put request a form still is required to be sent as a POST. An example of how you should do a PUT request can be seen below.

```erb
<form action="<%= movies_path %>" method="POST">
    <input type="hidden" name="_method" method="PUT"> # This resets the above line
</form>
```



A full example replacing the default text as that of what you are editing can also be seen below

First we change the function to pass in the paramaters

```ruby
def edit
    @movie = session[:movies][params[:id].to_i - 1]
end
```

then in the edit.html.erb

```erb
<h1>Edit Movie</h1>

<form action="<%= movie_path(params[:id]) %>" method="POST">
    <input type="hidden" name="_method" method="PUT"> # This resets the above line
	<input type="hidden" name="authenticity_token" value="<%=form_authenticity_token%>">
    <label>Title</label>
    <input type="text" name="movie[title]" value="<%=@movie["title"%>">
    <br>
    <label>Rating</label>
    <input type="number" name="movie[rating]" min="1" max="10" value="<%=@movie["rating"%>">
    <br>
    <input type="submit" name="Edit Movie">
</form>
```

Then in the controller again

```ruby
def update
    session[:movies][params[:id].to_i - 1] = params[:movie] #replace old entry
    redirect_to movie_path(params[:id].to_i - 1) # Take to current movie page
```

