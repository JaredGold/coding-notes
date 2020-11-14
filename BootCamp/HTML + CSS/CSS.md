# CSS

[TOC]



## Intro

Cascading Style Sheet also known as CSS is used to style webpages and add more of a visual profile and uniform to the websites created in HTML. It is used to modifying colors, font types, font sizes, shadows, images, element positioning and more. 

**<u>In document and Inline</u>**

You can technically use what is called inline styles which allows you to add css directly into the html file although it is strongly not recommended. What this looks like is adding `style="color: red;"` for example.

Alternatively from writing it directly inline you can also write it in a dedicated `<style>` element. You write the style tag instead the head element.

```html
<head>
  <style>
    p {
      color: red;
      font-size: 20px;
    }
  </style>
</head>
```

it is best practice to split CSS code and HTML code in separate documents. You do this by creating a file using the `.css` filename extension. `style.css` tends to the the way you write this file.

## Linking the CSS File

It is important to remember that just having a css file is not enough, you still need to link to the file. You do this by adding a `<link>` element to the head of the HTML file. This element is self closing and needs to contain the following:

1. `href` - the path to the css file
2. `type` - What type of item are you linking to. `text/css`
3. `rel` - describes the relationship between the HTML file and the CSS file. `stylesheet` 

```html
<link href="./style.css" type="text/css" rel="stylesheet">
```

## Basic Syntax + Tips

> *The below code snippets are being made smaller only using spaces between the semicolons. To do this more effectively put every line of code on a different space and end it with the closing semi colon on it's own line.*

* The syntax for selecting the `<p>` element is below. It's the same for the other elements but with their elements instead of `p`

  ```css
  p {   }
  ```

* You grab a class attribute slightly differently *(below)*. You select it by using a period ( . ) before the class' name. 

  ```css
  .classname {   }
  ```

* You can add more then one class to an attribute allowing for more customization. For example if you wanted 2 rules in a h1 it would look like the below.

  ```css
  .green {
    color: green;
  }
  
  .bold {
    font-weight: bold;
  }
  ```

  ```html
  <h1 class="green bold"> ... </h1>
  ```

  This would make the h1 attribute both green and bold due to the 2 classes.

* If you want to style a HTML element uniquely no matter the classes applied you can add an ID element. `<h1 id="ID-name">`. ID's should be used **sparingly** *(don't if you can prevent it)* and on elements that need to always appear the same.

* To select an `ID` in css it should look like below:

  ```css
  #ID-name {   }
  ```

* If you want an element to have 2 or more selectors at the same time you can combine them using <u>chaining</u>. Below is how you would look for all the h1 elements with the class of special.

  ```css
  h1.special {   }
  ```

* You can also select elements nested in other HTML elements like below.

  ```html
  <ul class='main-list'>
    <li> ... </li>
    <li> ... </li>
  </ul>
  ```

  ```css
  .main-list li {   }
  ```

* To save us from writing the same code in 2 different selectors you can choose 2 different selectors and write the code once using a comma `,` as shown below

  ```css
  h1, 
  .menu {
    font-family: Georgia;
  }
  ```

  

#### Specificity

Specificity is the order in which css code takes order. Code can take over the other depending on it's order of specificity. Below is the order from least easiest to specify over to highest of specificity order. It's best to start with the tag, then the class, then if all else fails IDs.

​								element `h1` <--------- class `class="name"` <----------- ID `id="name"`

## CSS Visual Rules

* After selecting a CSS we make a declaration which consists of a property and it's value.

  * `color: blue;`
  * The property is `color` and the value is `blue`
  * Property and value is separated by a colon `:`
  * A Semicolon `;` is used at the end of a declaration

  

* To change the typeface of text you can change the property `font-family`

  ```css
  font-family: Garamond;
  ```

* When changing font family there is a couple things to keep in mind. 

  1. In order for the font to be seen on a users webpage they must have the font installed on their computer (You can link instead)
  2. The default font is `Times New Roman`.
  3. Good Practice is to limit the typefaces used to 2-3 for faster load times.
  4. if the type face consists of more then one word enclose it in quotes `"Courier New"`

  

* To change the size of text we use the `font-size` property. The below `18px` means 18 pixels.

  ```css
  font-size: 18px;
  ```



* To change how bold, thin or normal text appears we use `font-weight`

  ```css
  font-weight: bold;
  ```

  

* By default text is always aligned to the left until we add `text-align`.

  ```css
  text-align: center;
  ```

  Text align can be used one of three ways but always stays between it's parent.

  1. `left`
  2. `center`
  3. `right`

  

* Next visual rule you can use is `color`. There is 2 aspects of color Foreground and Background.

  1. Foreground Color is the color that the element appears in.
  2. Background Color is as it is written the background of the element.

  ```css
  color: red;     						 /*Foreground*/
  background-color: blue;					 /*Background*/
  ```



* Opacity measures how transparent an element is. It's measured from 0-1

  ```css
  opacity: 0.5;
  ```

  

* You can change the background of an element by changing it's `background-image` also requires a URL.

  ```css
  background-image: url("images/mountains.jpg");
  ```

  

* A code that should **never** really be used is `!important`. It overrides every style.

  ```css
  color: blue !important;
  ```



## The Box Model

Browsers load everything with a box by default. For example when you change the background color of an element the color changes of it and the left and right of it.

The box model has multiple elements that take up space. The Properties include:

1. Width and height — specifies the width and height of the content area.
2. Padding — specifies the amount of space between the content area and the border.
3. Border — specifies the thickness and style of the border surrounding the content area and padding.
4. Margin — specifies the amount of space between the border and the outside edge of the element.

![The Box Model](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\The Box Model.PNG)



#### Content

* An element's content has 2 dimension: `height` and `width`.

* The default size of height and width are set to hold the raw contents of the box.

  ```css
  height: 80px;
  width: 120px;
  ```



#### Border

* A `border` is a line that surrounds an element (like a frame). They can set with 3 different attributes:

  1. `width` - thickness of the border. This can be set similarly by px or using `thin`, `medium`, or `thick`
  2. `style` - The design of the borders. [Different Styles](https://developer.mozilla.org/en-US/docs/Web/CSS/border-style#Values)
  3. `color` - The color of the border. [Different Color Options](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

  ```css
  border: 3px solid coral;
  ```

* If you would like to make the border to be more rounded we do this using `border-radius`. It adds a curve to the edges. 

  ```css
  border-radius: 5px;                    /*5 pixel rounding on all corners*/
  border-radius: 100%;                   /*Creates a circle border*/
  ```



#### Padding

* The space between the contents of the box and the border is it's *padding*.

* You can use padding to expand the background color to make it feel less cramped.

  ```css
  padding: 10px;
  ```

* To customize the padding in specific sections you can use the four below.

  1. `padding-top`
  2. `padding-right`
  3. `padding-bottom`
  4. `padding-left`

  ```css
  padding-top: 20px;
  ```

* You can also decide how much padding there should be on each side using a single declaration.

  ```css
  padding: 6px /*top*/ 11px /*right*/ 4px /*bottom*/ 9px; /*left*/
  ```

* This works in a clockwise direction starting at the top.

* You can also make it only 2 if that works for you.

  ```css
  padding: 5px /*top && bottom*/ 10px; /*left && right*/
  ```



#### Margins

* Margin is the space directly outside of the box.

  ```css
  margin: 20px;
  ```

* Margin can also be used similarly to padding as below:

  1. `margin-top`
  2. `margin-right`
  3. `margin-bottom`
  4. `margin-left`

* It can also be used in the clockwise directions similar to padding above.

* You can also center content using `margin` although it requires some syntax.

  ```css
  margin: 0 auto;
  ```

  * The above code makes top and bottom margin `0px` but the `auto` value lets the browser adjust the left and right margins to be centered. This works for div's but not for elements.
  * In order to center and element you must also include a width.



#### Minimum and Maximum Height and Width

Because web pages can be viewed on multiple different display sizes there are 4 properties we use to limit how narrow, wide or tall the element's box can be sized to.

1. `min-width` — this property ensures a minimum width of an element’s box.
2. `max-width` — this property ensures a maximum width of an element’s box.
3. `min-height` — this property ensures a minimum height for an element’s box.
4. `max-height` — this property ensures a maximum height of an element’s box.

```css
min-width: 300px;
max-width: 600px;
min-height: 150px;
max-height: 300px;
```



#### Overflow

After adding all of our dimensions to the boxes we can sometimes make something larger than the parent holding it which can create a spill. We can contain the spill by using `overflow`. Overflow can be managed using 3 different values.

- `hidden` - when set to this value, any content that overflows will be hidden from view.
- `scroll` - when set to this value, a scrollbar will be added to the element’s box so that the rest of the content can be viewed by scrolling.
- `visible` - when set to this value, the overflow content will be displayed outside of the containing element. Note, this is the default value.

```css
overflow: scroll;
```

#### Resetting Browser Defaults

All web browsers come with a default stylesheet also known as *user agent stylesheets*.
Developers like to reset the values so you can truly work with a clean slate. Below is the code used often as the first rule in CSS to start clean.

```css
* {
    margin: 0;
    padding: 0;
}
```



#### Visibility

You can hide elements from view using `visibility`. There are 2 properties you can use in visibility:

1. `hidden`
2. `visible`

```css
visibility: hidden;
```

### Changing The Box Model

The box model is hard to keep track of how the dimensions of the box actually is. If the box has a height of 200px and then you had a padding of 10px and a border of 1px you may forget that the height size now of the box is actually 222 pixels.

Similarly to the browser setting defaults the box has a default value using `box-sizing` the default value of it is called `content-box`. 

Alternatively we can reset the box model to work dependently on the width and height and everything get encapsulated inside it. We do this with the following code:

```css
* {
  box-sizing: border-box;
}
```

With that it now limits the height and width and makes it fixed. So if we change the height to 200px, add a border of 10px it now will have a fixed height of 200px and a border on the inside of 10px all around.

## Display and Positioning

The browser will render a HTML document with no css from left to right, top to bottom. This is known as the *flow* of elements in HTML. CSS includes properties that change where the browser positions element. The following will be a telling of the list properties that allow us to position and view the elements on a web page.

### Position

Remembering the box model it is key to remember that boxes are a certain width and height and will always remain on the left and not side by side. The default position can be changed by setting it's `position` property. The position Property can be changed to one of 4 values.

1. `static` - the default value (it does not need to be specified)
2. `relative`
3. `absolute`
4. `fixed`

#### Relative

Relative moves the object relative to where it is meant to be when it is static. We do this using offset properties:

1. `top` - moves the element down.
2. `bottom` - moves the element up.
3. `left` - moves the element right.
4. `right` - moves the element left.

```css
.box-bottom {
  background-color: DeepSkyBlue;
  position: relative;
  top: 20px;
  left: 50px;
}
```

![Relative](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\Relative.PNG)

#### Absolute

`absolute` will make the other elements ignore the element and act like it is not present. The element will be positioned relative to it's closest positioned parent element.

``` css
.box-bottom {
  background-color: DeepSkyBlue;
  position: absolute;
  top: 20px;
  left: 50px;
}
```

The below is displacing from the top left corner top 20px and left 50px. Test this for it to make sense.

![absolute](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\absolute.jpg)

#### Fixed

We can fix an element on the page and have it not move regardless of scrolling. `fixed`. This tends to be used for navigation bars. When it changes to fixed it gets removed from the *flow* of the HTML docment.

```css
.box-bottom {
  background-color: DeepSkyBlue;
  position: fixed;
  top: 20px;
  left: 50px;
}
```

![fixed](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\fixed.gif)

### Z-Index

When boxes positions are changed they can sometimes overlap which may make the  content difficult to read. The `z-index` property controls how far "back" or "forward" the element appears in the webpage. It's the depth of the elements. Think 3D. The `z-index` property only accepts integer's (full numbers).

```css
z-index: 2;
```

### Display

Every HTML element has a `display` value that dictates whether or not it can share horizontal space with other elements. Some elements will span the entire horizontal space regardless of the size of their content. There are 3 values for the `display` property.

1. `inline`
2. `block`
3. `inline-block`

#### Inline

Tags like `<em>`, `<strong>`, and `<a>` use *inline*. This property have a box tightly around their content only taking up the space needed to display their content. You can not change the height or width of this property.

```css
display: inline;
```

#### Block

`block` fills the entire width of the page by default but their width can also be set. The elements that are block-level by default is heading elements, `<p>`, `<div>` and `<footer>`. There are more as well but those are available on the MDN docs.

```css
display: block;
```

#### Inline-Block

The final property is `inline-block`. This is a combined feature of the previous 2. It can be seen next to each other and we can change the physical dimensions of it.

```css
display: inline-block;
width: 100px;
height: 200px;
```

### Float

The `float` property allows us to move an element as far left or as far right as possible on the page. Floated elements have a specified width otherwise the float value will not yield results. Float get's 2 values. 

1. `left`
2. `right`

```css
width: 10px;
float: left;
```

#### Clear

Float can be used on multiple elements at once although when floated elements have different heights it can affect the layout of the page and elements can "bump" into each other.

We use `clear` to specify what happens when elements bump into each other. The value's it takes is:

1. `left` — the left side of the element will not touch any other element within the same containing element.
2. `right` — the right side of the element will not touch any other element within the same containing element.
3. `both` — neither side of the element will touch any other element within the same containing element.
4. `none` — the element can touch either side.

```css
float: left;
clear: left;
```

## Color

There are 2 distinctions about color. It can affect the following things.

1. Foreground - `color`
2. Background - `background-color`

```css
color: white;
background-color: black;
```

There are multiple ways to choose colors, first off being:

#### Hexadecimal

"<u>Hexadecimal</u>" (#00FFAA). 

```css
color: #9932cc;
```

#### RGB

The next is RGB. RGB represents colors between 0 to 255 (decimals are okay). It is in the order it sounds Red, Green then Blue.

```css
color: rgb(255, 0, 125);
```

#### Hue, Saturation Lightness

Another very powerful system is hue-saturation-lightness abbreviated to `hsl`.
Hue can be between 0-360, then saturation and lightness is a percentage.

```css
color: hsl(120, 60%, 70%)
```

![](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\Color-Wheel.PNG)

#### Opacity and Alpha

We can also change how transparent an image is using opacity or alpha. For the HSL color scheme we can use `hsla` instead of `hsl`. Alpha is represented in a decimal number ranging from 
0 (inv) to 1. 

```css
color: hsla(34, 100%, 50%, 0.1)
```

Similarly with RGB we use `rgba`

```css
color: rgba(234, 44, 12, 0.33);
```

Alpha can only be used with rgb and hsl although you can add keyword `transparent`

```css
color: transparent;
```



## Typography

Typography is all about how to style our text and fonts. 

### Font Family

To change the type of font that is being used we use `font-family`.

```css
font-family: Garamond;
font-family: "Courier New";
```

When setting typefaces on a web page, keep the following points in mind:

1. The font specified in a stylesheet must be installed on a user’s computer in order for that font to display when a user visit the web page. 
2. The default typeface for many browsers is [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman).
3. It’s a good practice to limit the number of typefaces used on a web page to 2 or 3.
4. When the name of a typeface consists of more than one word, it must be enclosed in double quotes.

### Font Weight

`font-weight` controls how **bold** something is.

```css
font-weight: bold;
font-weight: normal;
```

 It can also be used as a numeric scaling ranging in multiples of 100 from anywhere between 
`100` to `900`. The default weight is `400`, bold is `700` and light is `300`.

```css
font-weight: 900;
```

### Font Style

You can also italicize text using the `font-style` property.

```css
font-style: italic;
```

### Word Spacing

To increase the space between words we use `word-spacing`.

```css
word-spacing: 0.3em;
```

### Letter Spacing

Similarly to word spacing we can also change the letter spacing using `letter-spacing`.

```css
letter-spacing: 0.3em;
```

### Text Transformation

Text can also be styled to look all uppercase or lowercase using `text-transform`.

```css
text-transform: uppercase;
```

### Text Alignment

We can also text align using `text-align` our choices of alignment are `left`, `center` and `right`

```css
text-align: center;
```

### Line Height

We can also change the `line-height` which modifies the *leading* of text. Below should explain the difference. This is normally used to make text easier to read.

![Line-height](C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\Line-height.PNG)

Generally when writing `line-height` we want to use a unitless number (not px) this is so no matter if the font size changes it will change with it.

```css
line-height: 1.4;
```

### Serif & Sans Serif

1. Serif — fonts that have extra details on the ends of each letter. Examples include fonts like Times New Roman or Georgia, among others.
2. Sans-Serif — fonts that do not have extra details on the ends of each letter. Instead, letters have straight, flat edges, like Arial or Helvetica.

### Fallback Fonts

When a font is used that a user doesn't have installed the system will load a fallback font. You can tell it to use specific fonts in order of fallback by the following. Garamond would be first then times second and serif as a final solution.

```css
font-family: "Garamond", "Times", serif;
```

### Google Fonts

You can find more font family's using [Google Fonts](https://fonts.google.com/).

When you choose the fonts you want on the right you have a link for the HTML document which goes in the `<head>` section.

Then you can choose it as a font in the css.

#### non-google Font-Face

If you prefer not to use a website link you can instead use an `@font-face` property. To do this after choosing the font on Google Font's follow below.

1. Instead of using the font’s link in the HTML document, enter the link into the URL bar in the browser.
2. The browser will load the CSS rules. You will need to focus on the rules that are directly labeled as `/* latin */`. Some of the latin rules are on separate lines. You will need each of these.
3. Copy each of the CSS rules labeled latin, and paste the rules from the browser to the top of **style.css**.

You **<u>HAVE</u>** to copy `@font-face` rules to the top of the stylesheet for the font to load correctly.

```css
@font-face {
  font-family: 'Space Mono';
  font-style: normal;
  font-weight: 700;
  src: local('Space Mono Bold'), local('SpaceMono-Bold'), url(https://fonts.gstatic.com/s/spacemono/v6/i7dMIFZifjKcF5UAWdDRaPpZUFWaHg.woff2) format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}  
```

We can also link a font that we may have hosted in our website. The font path is relative instead of being a url and it has multiple formats to support multiple browsers. Although `.woff2` seems to be the future of font format.

```css
@font-face {
  font-family: "Roboto";
  src: url(fonts/Roboto.woff2) format('woff2'),
       url(fonts/Roboto.woff) format('woff'),
       url(fonts/Roboto.tff) format('truetype');
}
```

## Grid Essentials

To create a grid you need to have a *grid container* and *grid items*. The grid container is a parent element that contains all the grid items. To make a grid container we set the element's `display` property to `grid` (to create a block-level grid) or `inline-grid` (to create an inline grid).

* to create columns we use `grid-template-columns`
* We can use `px` `em` `rem`or `%` to dictate the width of each columns
* The more sizes you put the more columns it creates
* Similarly you can create rows using `grid-template-rows` the same way

```css
.grid {
  display: grid; /*Create Grid Parent*/
  width: 1000px;
  height: 500px;
  grid-template-columns: 100px 200px; /*Create 2 columns of size 100px and 200px*/
  grid-template-rows: 10% 20% 600px; /*Create 3 rows of 50px, 100px and 600px*/
}
```

* You can also use the shorthand `grid-template` to combine the two. I
* Using `grid-template` rows come first then columns separated by a slash.

The same code as above using `grid-template`.

```css
.grid {
  display: grid; /*Create Grid Parent*/
  width: 1000px;
  height: 500px;
  grid-template: 100px 200px / 10% 20% 600px;
}
```

#### Fraction

Instead of using the responsive units such as `%`, `em` and `rem` there is another unit called `fr` (fraction).

* The way this works is it uses a fraction of the grid's length and width. This prevents overflow.
* `fr` divides the available space depending on how many fractions you give it.
* `fr` can be used with other units and then it divides the available space left.

```css
grid-template: 2fr 1fr 1fr / 1fr 3fr 1fr;
```

#### Repeat

`repeat()` is a function you can use in grid's which allow you to duplicate the specifications for rows and columns a given number of times. The way this looks is below.

```css
grid-template-columns: repeat(3, 100px);
```

The above code makes 3 columns of size 100px. 
If you want to create an alternating sized columns let's say the first and third column to be 20px and the second and fourth column to be 50px wide it would look like the below.

```css
grid-template-columns: repeat(2, 20px 50px)
```

#### minmax

When creating a grid you may have items put into the grid that is larger than the grid column itself. You don't want it spilling so you would use a function called `minmax()`. 

* It takes 2 sizes and will adjust the size depending on what is inside of it. 

* For example the below has the first and third column always being 100px and the second column always being a minimum of 100px but if it has something larger inside it can expand up to 500px wide.

```css
grid-template-columns: 100px minmax(100px, 500px) 100px;
```

#### Grid Gap

If you want to create a gap between each column or row we use `grid-row-gap` or `grid-column-gap`.

* It is important to note that `grid-gap` doesn't add space at the beginning or end of the grid just between them.

```css
grid-column-gap: 10px;
grid-row-gap: 20px;
```

or similarly you could use grid-gap to do the same. Note there is no `/` between the values.

```css
grid-gap: 20px 10px;
```

----

We will now look at the following. Regarding making multiple rows and columns all look very different depending on new factors. (this makes beautiful layouts with little effort)

<img src="C:\Users\New\Google Drive\Coding Notes\BootCamp\PreWork\IMGs\Grid-example.PNG" alt="Grid-example" style="zoom: 50%;" />

---

#### Multiple Row Items

Using `grid-row-start` and `grid-row-end` we can make single grid items take up multiple rows. This is adding CSS to the elements inside the grid.

```css
.item {
  grid-row-start: 1;
  grid-row-end: 3;
}
```

The above  `item` will take up 2 rows. The way to look at it is the grid lines. It starts on the first grid line on the left of it and moves up to the third grid line on the right of it. *e.g. a 5 row item would be between 1 to 6.*

We can also use the short hand `grid-row`. For example the above in grid row.

```css
grid-row: 1 / 3;
```

**NOTE**: You can do the exact same as above using `grid-column-start`, `grid-column-end` and `grid-column`.

#### Span

Using all these properties we can also use the keyword `span`. Span is like saying 'Take up *x* amount of rows or columns'. For example the below will start at column four and take up two columns of space.

```css
.item {
  grid-column: 4 / span 2;
}
```

This can make it easier than calculating where the final grid line would be.

---

### Grid Area

We can do even more refactoring to `grid-row` and `grid-column` using the term `grid-area`. The order for this is as below:

1. `grid-row-start`
2. `grid-column-start`
3. `grid-row-end`
4. `grid-column-end`

```css
.item {
  grid-area: 2 / 3 / 4 / span 5;
}
```

Using this info the item will occupy rows two and three and columns three through eight.

---

## Advanced Grid

#### Grid Template Areas

*This was hard to explain hopefully following the copy paste may help.*

`grid-template-areas` lets you name sections of the webpage to use in our `grid-row-start`, `grid-row-end`, `grid-col-start`,`grid-col-end`, and `grid-area` properties.

```html
<div class="container">
  <header>Welcome!</header>
  <nav>Links!</nav>
  <section class="info">Info!</section>
  <section class="services">Services!</section>
  <footer>Contact us!</footer>
</div>
```

```css
.container {
  display: grid;
  max-width: 900px;
  position: relative;
  margin: auto;
  grid-template-areas: "head head"
                       "nav nav" 
                       "info services"
                       "footer footer";
  grid-template-rows: 300px 120px 800px 120px;
  grid-template-columns: 1fr 3fr; 
}

header {
  grid-area: head;
} 

nav {
  grid-area: nav;
} 

.info {
  grid-area: info;
} 

.services {
  grid-area: services;
}

footer {
  grid-area: footer;
} 
```

1. In the example above, the HTML creates a web page with five distinct parts.
2. The `grid-template-areas` declaration in the `.container` rule set creates a 2-column, 4-row layout.
3. The `grid-template-rows` declaration specifies the height of each of the four rows from top to bottom: 300 pixels, 120 pixels, 800 pixels, and 120 pixels.
4. The `grid-template-columns` declaration uses the `fr` value to cause the left column to use one fourth of the available space on the page and the right column to use three-fourths of the available space on the page.
5. In each rule set below `.container`, we use the `grid-area` property to tell that section to cover the portion of the page specified. The `header` element spans the first row and both columns. The `nav` element spans the second row and both columns. The element with class `.info` spans the third row and left column. The element with class `.services` spans the third row and right column. The `footer` element spans the bottom row and both columns.
6. That’s it! An entire page laid out in 40 lines of code.

#### Overlapping Elements

When using the grid layout we can overlap areas much easier.

```c
<div class="container">
  <div class="info">Info!</div> 
  <img src="#" />
  <div class="services">Services!</div>
</div>
```

```css
.container {
  display: grid;
  grid-template: repeat(8, 200px) / repeat(6, 100px);
}

.info {
  grid-area: 1 / 1 / 9 / 4;
}

.services {
  grid-area: 1 / 4 / 9 / 7;
}

img {
  grid-area: 2 / 3 / 5 / 5;
  z-index: 5;
}
```

In the example above, there is a grid container with eight rows and six columns. There are three grid items within the container — a `<div>` with the class `info`, a `<div>` with the class `services`, and an image.

The `info` section covers all eight rows and the first three columns. The `services` section covers all eight rows and the last three columns.

The image spans the 2nd, 3rd, and 4th rows and the 3rd and 4th columns.

The z-index property tells the browser to render the image element on top of the `services` and `info` sections so that it is visible.

---

### Justify

#### Justify Items

`justify-items` is a property that positions grid items along the inline, or row, axis. 

`justify-items` accepts these values:

- `start` — aligns grid items to the left side of the grid area
- `end` — aligns grid items to the right side of the grid area
- `center` — aligns grid items to the center of the grid area
- `stretch` — stretches all items to fill the grid area

```css
justify-items: stretch;
```

#### Justify Content

We can use `justify-content` to position the entire grid along the row axis.
It accepts these values:

- `start` — aligns the grid to the left side of the grid container
- `end` — aligns the grid to the right side of the grid container
- `center` — centers the grid horizontally in the grid container
- `stretch` — stretches the grid items to increase the size of the grid to expand horizontally across the container
- `space-around` — includes an equal amount of space on each side of a grid element, resulting in double the amount of space between elements as there is before the first and after the last element
- `space-between` — includes an equal amount of space between grid items and no space at either end
- `space-evenly` — places an even amount of space between grid items and at either end

```css
justify-content: start;
```

#### Align Items

The last 2 justify property's were regarding the left-right. This is going to be the top-bottom.
`align-items` is similar to justify items but for the top to bottom.

`align-items` accepts these values:

- `start` — aligns grid items to the top side of the grid area
- `end` — aligns grid items to the bottom side of the grid area
- `center` — aligns grid items to the center of the grid area
- `stretch` — stretches all items to fill the grid area

```css
align-items: center;
```

#### Align Content

As above `align-content` is the same for justify content but on the top to bottom.
It accepts these positional values:

- `start` — aligns the grid to the top of the grid container
- `end` — aligns the grid to the bottom of the grid container
- `center` — centers the grid vertically in the grid container
- `stretch` — stretches the grid items to increase the size of the grid to expand vertically across the container
- `space-around` — includes an equal amount of space on each side of a grid element, resulting in double the amount of space between elements as there is before the first and after the last element
- `space-between` — includes an equal amount of space between grid items and no space at either end
- `space-evenly` — places an even amount of space between grid items and at either **end**

```css
align-content: center;
```

#### Justify Self & Align Self

Justify items and align items was talking about how **all** grid items will position themselves. 

`justify-self` specifies how the individual element should position itself within the row axis and will override `justify-items`.

`align-self` specifies how the individual element should position itself within the column axis and will override `align-items`.

They both accept these four properties: 

- `start` — positions grid items on the left side/top of the grid area
- `end` — positions grid items on the right side/bottom of the grid area
- `center` — positions grid items on the center of the grid area
- `stretch` — positions grid items to fill the grid area (default)

---

### Implicit vs Explicit Grid

> Stolen from Code Cademy but worth a read and hard to paraphrase.

So far, we have been explicitly defining the dimensions and quantities of our grid elements using various properties. This works well in many cases, such as a landing page for a business that will display a specific amount of information at all times.

However, there are instances in which we don’t know how much information we’re going to display. For example, consider online shopping. Often, these web pages include the option at the bottom of the search results to display a certain quantity of results or to display ALL results on a single page. When displaying all results, the web developer can’t know in advance how many elements will be in the search results each time.

What happens if the developer has specified a 3-column, 5-row grid (for a total of 15 items), but the search results return 30?

Something called the *implicit* grid takes over. The implicit grid is an algorithm built into the specification for CSS Grid that determines default behavior for the placement of elements when there are more than fit into the grid specified by the CSS.

The default behavior of the implicit grid is as follows: items fill up rows first, adding new rows as necessary. New grid rows will only be tall enough to contain the content within them. In the next exercise, you’ll learn how to change this default behavior.

#### Grid Auto Rows & Grid Auto Columns

`grid-auto-rows` specifies the height of implicitly added grid rows.

`grid-auto-columns` specifies the width of implicitly added grid columns.

`grid-auto-rows` and `grid-auto-columns` accept the same values as their explicit counterparts, `grid-template-rows` and `grid-template-columns`:

- pixels (`px`)
- percentages (`%`)
- fractions (`fr`)
- the `repeat()` function

#### Grid Auto Flow

We can also specify the order in which the rows are rendered automatically.

`grid-auto-flow` specifies whether new elements should be added to rows or columns.

`grid-auto-flow` accepts these values:

- `row` — specifies the new elements should fill rows from left to right and create new rows when there are too many elements (default)
- `column` — specifies the new elements should fill columns from top to bottom and create new columns when there are too many elements
- `dense` — this keyword invokes an algorithm that attempts to fill holes earlier in the grid layout if smaller elements are added

You can pair `row` and `column` with `dense`, like this: 

```css
grid-auto-flow: row dense;.
```

---

## CSS Transitions

The visual appearance of elements can change for multiple reasons,

* mice moving over links (changes colors)
* changing size of the window
* Scrolling makes elements dispappear and appear.

CSS transitions can control how it happens. These are what we call a *state change*. Transitions control the timing of the change. We can control the following four aspects:

- Which CSS properties transition
- How long a transition lasts
- How much time there is before a transition begins
- How a transition accelerates

---

#### Duration

First we must specify two of those elements:

* The property to transition
* The duration of the transition

`transition-property` declares the property to be animating and `transition-duration` declares how long it will take. (properties you can transition can be found [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties))

Transition duration can be specified in **<u>seconds or milliseconds</u>** such as `3s`, `0.75s` or `500ms`

```css
a {
  transition-property: color;
  transition-duration: 1s;
}
```

---

#### Delay

The next property is `transition-delay` which specifies how long to wait before starting the transition.

```css
transition-delay: 250ms;
```

---

#### Timing Function

`transition-timing-function` is the pace of the transition.
By default the value is `ease` which is slow at the start and end and speeds up in the middle. You can use the folowing values as well:

- `ease-in` — starts slow, accelerates quickly, stops abruptly
- `ease-out` — begins abruptly, slows down, and ends slowly
- `ease-in-out` — starts slow, gets fast in the middle, and ends slowly
- `linear` — constant speed throughout

---

#### Transition Shorthand

Similarly with many css rules there is short hand to declare all of this at once. The short hand is called `transition`

`transition` must be specified in this order: `transition-property`, `transition-duration`, `transition-timing-function`, `transition-delay`.

```css
transition: color 1.5s linear 0.5s;
```

The great thing about the shorthand is that you can have multiple transitions for multiple properties in the one code. 

To combine transitions, add a comma (`,`) before the semicolon (`;`) in your rule. After the comma, use the same shorthand syntax. For example:

```css
transition: color 1s linear,
font-size 750ms ease-in 100ms;
```

---

#### All

For the `transition-property` value you can choose `all` which applies the same values to every property.

```css
transition: all 1.5s linear 0.5s;
```





----

## CodeCademy's Short notes

#### CSS Selectors

- CSS can change the look of HTML elements. In order to do this, CSS must select HTML elements, then apply styles to them.
- CSS can select HTML elements by tag, class, or ID.
- Multiple CSS classes can be applied to one HTML element.
- Classes can be reusable, while IDs can only be used once.
- IDs are more specific than classes, and classes are more specific than tags. That means IDs will override any styles from a class, and classes will override any styles from a tag selector.
- Multiple selectors can be chained together to select an element. This raises the specificity, but can be necessary.
- Nested elements can be selected by separating selectors with a space.
- Multiple unrelated selectors can receive the same styles by separating the selector names with commas.

---

#### Visual Rules

- CSS declarations are structured into property and value pairs.
- The `font-family` property defines the typeface of an element.
- `font-size` controls the size of text displayed.
- `font-weight` defines how thin or thick text is displayed.
- The `text-align` property places text in the left, right, or center of its parent container.
- Text can have two different color attributes: `color` and `background-color`. `color` defines the color of the text, while `background-color` defines the color behind the text.
- CSS can make an element transparent with the `opacity` property.
- CSS can also set the background of an element to an image with the `background-image` property.
- The `!important` flag will override any style, however it should almost never be used, as it is extremely difficult to override.

---

#### The Box Model

1. The box model comprises a set of properties used to create space around and between HTML elements.
2. The height and width of a content area can be set in pixels or percentage.
3. Borders surround the content area and padding of an element. The color, style, and thickness of a border can be set with CSS properties.
4. Padding is the space between the content area and the border. It can be set in pixels or percent.
5. Margin is the amount of spacing outside of an element’s border.
6. Horizontal margins add, so the total space between the borders of adjacent elements is equal to the sum of the right margin of one element and the left margin of the adjacent element.
7. Vertical margins collapse, so the space between vertically adjacent elements is equal to the larger margin.
8. `margin: 0 auto` horizontally centers an element inside of its parent content area, if it has a width.
9. The `overflow` property can be set to `display`, `hide`, or `scroll`, and dictates how HTML will render content that overflows its parent’s content area.
10. The `visibility` property can hide or show elements.

---

##### Box Model Resizing

1. In the default box model, box dimensions are affected by border thickness and padding.
2. The `box-sizing` property controls the box model used by the browser.
3. The default value of the `box-sizing` property is `content-box`.
4. The value for the new box model is `border-box`.
5. The `border-box` model is not affected by border thickness or padding.

---

##### Layout

1. The `position` property allows you to specify the position of an element in three different ways.
2. When set to `relative`, an element’s position is relative to its default position on the page.
3. When set to `absolute`, an element’s position is relative to its closest positioned parent element. It can be pinned to any part of the web page, but the element will still move with the rest of the document when the page is scrolled.
4. When set to `fixed`, an element’s position can be pinned to any part of the web page. The element will remain in view no matter what.
5. The `z-index` of an element specifies how far back or how far forward an element appears on the page when it overlaps other elements.
6. The `display` property allows you control how an element flows vertically and horizontally a document.
7. `inline` elements take up as little space as possible, and they cannot have manually-adjusted `width` or `height`.
8. `block` elements take up the width of their container and can have manually-adjusted `height`s.
9. `inline-block` elements can have set `width` and `height`, but they can also appear next to each other and do not take up their entire container width.
10. The `float` property can move elements as far left or as far right as possible on a web page.
11. You can clear an element’s left or right side (or both) using the `clear` property.

---

#### Color

There are four ways to represent color in CSS:

- Named colors — there are 147 named colors, which you can review [here](https://msdn.microsoft.com/en-us/library/aa358802(v=vs.85).aspx).
- Hexadecimal or hex colors
  - Hexadecimal is a number system with has sixteen digits, 0 to 9 followed by “A” to “F”.
  - Hex values always begin with `#` and specify values of red, blue and green using hexademical numbers such as `#23F41A`.
- RGB
  - RGB colors use the `rgb()` syntax with one value for red, one value for blue and one value for green.
  - RGB values range from 0 to 255 and look like this: `rgb(7, 210, 50)`.
- HSL
  - HSL stands for hue (the color itself), saturation (the intensity of the color), and lightness (how light or dark a color is).
  - Hue ranges from 0 to 360 and saturation and lightness are both represented as percentages like this: `hsl(200, 20%, 50%)`.
- You can add opacity to color in RGB and HSL by adding a fourth value, `a`, which is represented as a percentage.

---

#### Typography

- *Typography* is the art of arranging text on a page.
- Text can appear in any number of weights, with the `font-weight` property.
- Text can appear in italics with the `font-style` property.
- The vertical spacing between lines of text can be modified with the `line-height` property.
- *Serif* fonts have extra details on the ends of each letter. *Sans-Serif* fonts do not.
- *Fallback fonts* are used when a certain font is not installed on a user’s computer.
- Google Fonts provides free fonts that can be used in an HTML file with the `<link>` tag or the `@font-face` property.
- Local fonts can be added to a document with the `@font-face` property and the path to the font’s source.
- The `word-spacing` property changes how far apart individual words are.
- The `letter-spacing` property changes how far apart individual letters are.
- The `text-align` property changes the horizontal alignment of text.

---

#### Grid Essentials

- `grid-template-columns` defines the number and sizes of the columns of the grid
- `grid-template-rows` defines the number and sizes of the rows of the grid
- `grid-template` is a shorthand for defining both `grid-template-columns` and `grid-template-rows` in one line
- `grid-gap` puts blank space between rows and/or columns of the grid
- `grid-row-start` and `grid-row-end` makes elements span certain rows of the grid
- `grid-column-start` and `grid-column-end` makes elements span certain columns of the grid
- `grid-area` is a shorthand for `grid-row-start`, `grid-column-start`, `grid-row-end`, and `grid-column-end`, all in one line

---

#### Advanced CSS Grid

- `grid-template-areas` specifies grid named grid areas
- grid layouts are two-dimensional: they have a row, or inline, axis and a column, or block, axis.
- `justify-items` specifies how individual elements should spread across the row axis
- `justify-content` specifies how groups of elements should spread across the row axis
- `justify-self` specifies how a single element should position itself with respect to the row axis
- `align-items` specifies how individual elements should spread across the column axis
- `align-content` specifies how groups of elements should spread across the column axis
- `align-self` specifies how a single element should position itself with respect to the column axis
- `grid-auto-rows` specifies the height of rows added implicitly to the grid
- `grid-auto-columns` specifies the width of columns added implicitly to the grid
- `grid-auto-flow` specifies in which direction implicit elements should be created

---

#### Transitions

CSS Transitions have 4 components:

- A *property* that will transition.
- The *duration* which describes how long the transition takes.
- The *delay* to pause before the transition will take place.
- The *timing function* that describes the transition’s acceleration.

A simple transition can be described with a property and a duration, which can be written like this:

```css
transition-property: color;
transition-duration: 1s;
```

Many properties’ *state changes* can be transitioned, including color, background color, font size, width, and height. `all` is also a valid transition property that causes every changing property to transition.

The shorthand property `transition` can be used to describe all four components of a transition at once. By using the comma (`,`) operator, many transitions can be described in one CSS rule.