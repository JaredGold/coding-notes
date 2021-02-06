# Image upload with AWS
To make an image we use the image tag of erb. This looks as below
```erb
<%= image_tag "linktoimage.com", alt: "alt text for iamge", class: "class-name" %>
```
It is not best practice to request an iamge from the a seperate site every single time incase the website goes down.
Instead of using the link you can add the image to `app/assets/images` and use the `name.jpg`

#### How to in css
In the html file use a div instead with a class
```erb
<div class="hero-image">
  <h1>My Book Collection</h1>
</div>
```
Then in the style sheet
```css
.hero-image{
  display: flex;
  background-image: url("books.jpg");
  height: 100vh;
  width:100%;
}
```

## Activate storage
You activate storage by running `rails active_storage:install`
You then need to run `rails db:migrate`

The key files used for image storage is `/config/storage.yml` + `/config/environments/` (development.rb, production.rb & test.rb)

You then can add a field to your form to allow images to be uploaded

```erb
  <div class="field">
    <%= form.label :picture %>
    <%= form.file_field :picture, accept: 'image/png, image/jpg, image/jpeg' %>
  </div>
```
You still need to allow it into your paramaters. This is done in the controller. You add to the trusted params

```ruby
def book_params
   params.require(:book).permit(:title, :genre_id, :published, :picture)
end
```
We still need to teach the model what to do with the image
You add `has_one_attached picture` to the model in our case the books

In order to add the image you can do this by adding this line to your html.erb file
```erb
<%= image_tag book.picture, class: "card-img-top" if book.picture.attached? %>
```

This method of storage is **bad** as it costs a lot of money to keep up storage space. This is why we save the images in an AWS server or similar.

## AWS Storage
1. First you would log into the AWS console (they give 12 months free)
2. You then look for S3
3. Then create a bucket
4. A bucket gets a unique name similar to a url. You can also choose a region or default it. Then you choose next.
5. Then Next Again.
6. Tick Block all public acces.
7. Then create bucket

You then need to create a user which has access to that bucket, this is done through the Iam identity management.
1. Click services
2. Search Iam
It is best practice to have one login for each bucket.
3. Users, Add User
4. Give programmatic access

Then we need to give permissions
5. Attach existing policies directly
6. Search S3 (you can go through and read about each if you want)
7. AmazonS3FullAccess
8. Press Review
9. Create user

**WATCH OUT FOM THIS POINT IT IS IMPOSSIBLE TO GET ANY OF THE INFORMATION ON THIS SCREEN BACK!**
10. Download the .csv and keep it in a secure place **OR** keep the page up with the secret access key until you need it

Because rails has a great place to store keys you can use the credentials.yml file. Because it is encrypted and can only be unencrypted by your rails file you are okay.
To access the credentials file you have to follow the below.
1. In terminal `EDITOR="code --wait" rails credentials:edit
(This should open up the credentials file)
You then can store your access key and secret access key there.
It is important that you leave the files white spacing as it follows strict structre

Next thing to do is add the AWS gem.
`bundle add aws-sdk-s3`

In the storage.yml file you need to uncomment the amazon service area.
You have to change the region and the bucket name.

Then we have to change the development.rb file in the `config/environments` directory
`config.active_storage.service = :local` to `config.active_storage.service = :amazon`

You then do the same as above to the production environment

Keep the test as the local so you don't fill up the amazon server with too much.
