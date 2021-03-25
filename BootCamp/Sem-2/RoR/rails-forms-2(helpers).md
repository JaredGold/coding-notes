# Rails Forms with Helpers

The previous rails forms teaches you how to create a manual form. Of course rails has a simplified way to create forms using the `form_with` code. It can look like below

```ruby
form_with(model: nil, scope: nil, url: nil, format: nil, **options)
```

Reading the apidock.com helper docs

```erb
# Using just a URL:
<%= form_with url: posts_path do |form| %>
  <%= form.text_field :title %>
<% end %>
# =>
<form action="/posts" method="post" data-remote="true">
  <input type="text" name="title">
</form>

# Adding a scope prefixes the input field names:
<%= form_with scope: :post, url: posts_path do |form| %>
  <%= form.text_field :title %>
<% end %>
# =>
<form action="/posts" method="post" data-remote="true">
  <input type="text" name="post[title]">
</form>

# Using a model infers both the URL and scope:
<%= form_with model: Post.new do |form| %>
  <%= form.text_field :title %>
<% end %>
# =>
<form action="/posts" method="post" data-remote="true">
  <input type="text" name="post[title]">
</form>

# An existing model makes an update form and fills out field values:
<%= form_with model: Post.first do |form| %>
  <%= form.text_field :title %>
<% end %>
# =>
<form action="/posts/1" method="post" data-remote="true">
  <input type="hidden" name="_method" value="patch">
  <input type="text" name="post[title]" value="<the title of the post>">
</form>

# Though the fields don't have to correspond to model attributes:
<%= form_with model: Cat.new do |form| %>
  <%= form.text_field :cats_dont_have_gills %>
  <%= form.text_field :but_in_forms_they_can %>
<% end %>
# =>
<form action="/cats" method="post" data-remote="true">
  <input type="text" name="cat[cats_dont_have_gills]">
  <input type="text" name="cat[but_in_forms_they_can]">
</form>
```

---

# Example's Using code

```erb
<h1>New Listing</h1>


```

