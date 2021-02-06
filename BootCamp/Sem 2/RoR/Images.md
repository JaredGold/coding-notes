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
