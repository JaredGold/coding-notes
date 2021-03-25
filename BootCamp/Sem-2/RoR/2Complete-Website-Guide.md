# Complete Web Dev - Follow Up
- Straight out of the box `_spec` files are created. If you look into what is inside of the spec file you can use the predefined tests or customise
- When running tests it's good to use the seed file so that way the test is clean.

## Add Active Record
`rails active_storage:install` - Adds active storage to the application (for db)
- `has_one_attached :photo` - Add to listing to have one photo attached
Add the below to your form to add a field for files
```erb
  <div class="field">
    <%= form.label :photo %>
    <%= form.file_field :photo %>
  </div>
```

To then display the image you add the below to show
```ruby
<% if @listing.photo.attached? %>
  <p>
    <strong>Photo:</strong>
    <%= image_tag @listing.photo %>
  </p>
<% end %>
```

Using Cloudinary to upload images - Add gems
```ruby
# Used for cloudinary image uploading
gem 'cloudinary'
gem 'activestorage-cloudinary-service'
```

Run 
`EDITOR="code --wait" rails credentials:edit`

then add
```yml
cloudinary:
  service: Cloudinary  
  cloud_name: nameofcloud
  api_key: api key number
  api_secret: secret key
```

In `storage.yml`

```yml
cloudinary:
  service: Cloudinary
  cloud_name: <%= Rails.application.credentials.dig (:cloudinary, :cloud_name) %> 
  api_key: <%= Rails.application.credentials.dig (:cloudinary, :api_key) %> 
  api_secret: <%= Rails.application.credentials.dig (:cloudinary, :api_secret) %>
```

Add the master key to heroku
`$ heroku config:set RAILS_MASTER_KEY= ` + the key that is found in `config/master.key`

Almost complete... we just need to point specifics to what is going to point to cloudinary...
In development.rb and production.rb (will be in same bucket this method)
search for `config.active_storage` then change it from `:local` to `:cloudinary`
