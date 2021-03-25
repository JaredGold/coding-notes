# Responsive Design

## What is Responsive Design

Responsive design answers the fact that screens are all different sizes. 

1. Phones
2. Tablets
3. Laptops
4. Desktops
5. Projectors
6. Watches

Websites need to accommodate all platforms.



#### Tools

* Viewport Optimization
* Percentages
* Media Breakpoints
* Flexbox & Frameworks



#### Mobile First

It is important to design a website first for a Mobile and then scale our way up.



#### Meta Tag Viewport

Giving a meta tag of viewport so it informs the browser that it should optimize the page to the viewport the user is looking it at.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```



#### Percentages

A solution to using pixels as a sizing it means if a device gets smaller it doesn't change the size. A better way to change width and height would be using `%`

```css
.box{
    width: 70%;
    height: 45%;
}
```



#### Media Breakpoints

If you want to  change a property if it is being used on a screen of a smaller or larger size we use something called a media breakpoint.

```css
@media screen and (max-width: 600px){
    p{
        font-size: 30px
    }
}
```

The code above is saying if screen the page is being viewed on is smaller than 600px's wide use that font size. If it is larger it would use whatever font size you determined before.

There can be multiple breakpoints.

