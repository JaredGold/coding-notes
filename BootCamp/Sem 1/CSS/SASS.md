# SASS and SCSS

#### SASS What is it?

Sass is an extension language for CSS. It allows you to do more with Vanilla CSS.

#### SASS vs SCSS

SASS is a syntax extension. 
SCSS is also a syntax extension.
They do the same thing with different syntax.

All CSS is valid SCSS wheras SASS is different from SCSS.



#### SCSS Development Workflow

SCSS has to get transpiled into CSS

We need to conver it from SCSS to CSS

It tends to be apart of a complex build process.

`$ sass style.scss:style.css` - writes the css file

`sass --watch style.scss:style.css` - see the changes in the scss file and auto updates the css file that it has writte.



#### Variables

It uses variables similar to coding.

```scss
$error-color: red;

.error-text {
    color: $error-color;
}
```

This is useful because you can change on variable instead of many.



#### Mixin

```scss
@mixin fancy-box{
    border: 1px dashed black;
    font-family: "Fancy Font";
    color: gold;
}

.nav-card{
    @include fancy-box();
    box-shadow: 0px 1px 5px black;
    background: grey;
}
```

A mixin is a premade collection of variables that you can put in any bit of code without retyping.



#### Nesting

```SCSS
.box{
    color:blue
        li{
            background: red;
            font-size: 20px;
            }
}
```

This can next code in code.



#### Inheritance

```scss
.error{
    color:red;
    border:red;
}

.serious-error{
    @extend .error;
    font-weight: bold;
    font-size: 20px;
}
```

`@extend` lets you copy all that is in another selector.