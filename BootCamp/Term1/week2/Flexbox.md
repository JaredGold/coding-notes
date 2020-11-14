# Flexbox

*Relatively new to CSS*

Flexbox is a system for design as well as a display type given to an element.

```css
.container{
    display: flex;
}
```

Flex makes everything responsive no matter how small the window is. The items inside get smaller with the size.

#### Direction

Default flexbox makes the main axis the horizontal axis so it stacks to the right horizontally. You can change this using `flex-direction`. For example the below

```css
p{
flex-direction: column;
flex-direction: row; /* Default option */
}
```

#### Wrap

If you don't want the elements inside to squeeze together you can use `flex-wrap: wrap` to wrap around until it absolutely can't.

#### Justify Content

`justify-content` changes if the content is more stuck to the left or right hand side.

```css
justify-content: flex-start;
justify-content: flex-end;
justify-content: center;
justify-content: space-around;
justify-content: space-between;
```

#### Align Items

`align-items` is how we align the items on the vertical axis. The codes they accept are the same as justify content.

#### Order

This let's you change the order in which the individual (Not the parent) is. By default order is set to 0 but you can change it to a positive or negative integer.

`order: 2;` 

#### Align-Self

`align-self` is similar to align-items but can move the individual item that you are writing the code on.

#### Flex Flow

`flex-flow` is used to give `flex-direction` and `flex-wrap` in one line. it looks like:

```css
.item{
    display: flex;
    flex-flow: row wrap;
}
```

#### Align-Content

`align-content` is used to set how many lines are space apart from each other. They take the same values as align-items but also include `stretch`.