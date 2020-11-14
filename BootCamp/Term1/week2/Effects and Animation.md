# Effects and Animations

A pseudo class is a special selector which is saying you have to do something for it to be active *(as a user)*. 

The below are examples using anchor tags.

`a:hover` the :hover part is a pseudo class saying when the users mouse hovers over that element.

`a:visited` is a website the user has previously visited

#### Transitions

`transition: 2s` is a trait used to make the animation between one state to the other to be more smooth over a total of 2 seconds.

#### Transform

`transform:` is an attribute used to transform to a specific amount.

`transform: rotate(90deg)` - transforms a certain amount

`transform: skew(145deg)` - skews the item

`transform: scale(2, 1)` - makes it scale `(width, height)` by an amount it multiplies by. Alternately you can use `scaleX()` or `scaleY()`

`transform: translate(left, top)` Replacing left and top transform lets you move it a certain amount of pixels from the left side and from the top side. `translate(20px, 50px)`. Sam e with scale you can also use `translateX` and `translateY`

#### Keyframing

Keyframes allows you to animate using very specific keyframed percentages.

```css
.box{
    width: 100px;
    height: 100px;
    background: salmon;
    animation-name: colorful-text;
    animation-duration: 5s;
}

@keyframes colorful-text {
    0%{
        background: salmon;
    }
    50%{
        background: yellow;
    }
    100%{
        background: blue;
    }
}
```

The way this works is when it is between 0-50% it is going to shift from salmon to yellow then from 50% to 100% it is going to shift from yellow to blue.

you can also use:

```css
@keyframes colorful-text {
    from{
        background: green:
    }
    to{
        background: orange;
    }
}
```



