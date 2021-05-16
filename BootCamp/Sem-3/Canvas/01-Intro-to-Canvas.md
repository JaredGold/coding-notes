# Canvas Intro

Canvas is an interactive HTML element that can be modified and edited inside of JavaScript.

### Canvas Element

To create a canvas it is as simple as opening and closing tags in html `<canvas></canvas>`.

By default the canvas will be white with no borders so it may be hard to see. If you want to visualise it you can customise the visuals in CSS.

### Canvas Size

You can change the height and width in the css although it won't be as accurate as doing so in JavaScript (best to do it in javascript).

After linking the javascript file we then declare a canvas variable in the file:
`const canvas = document.querySelector('canvas')`

You then can play arround with the width and height of the canvas by typing:
`canvas.width = window.innerWidth` // This makes the width the entire window's width
You can do the same for height.

### Drawing

There are many objects we can draw:

- rectangles
- lines
- Arcs (circles)
- Bezier curves
- images
- text

The most common are rectangles, lines and arcs.

#### Canvas

We first need to create a context variable. Context is just a way for us to create a container full of methods that will draw to the canvas.
`var c = canvas.getContext('2d');`

#### Rectangle

By creating this we have the ability to draw to the actual canvas using 2d elements. One of these elements is a rectangle.

You create a rectangle by using `fillRect`

```js
// draw rectangle
c.fillRect(x, y, width, height)
// change color of rectangle (note needs to be above rect)
c.fillStyle = "rgba()" //#FFF red rgba
```

#### Line

To draw a line you need to draw a path first as below

```js
c.beginPath();
// starting point
c.moveTo(x,y);
// end point
c.lineTo(x,y);
// add color
c.strokeStyle = "rgba()" //#FFF red rgba
// draw line
c.stroke();
```

You can continue adding more `.lineTo()` to add more lines

#### Circle / Arc

Create a code as below

```js
c.beginPath() // always begin on new object
c.arc(x, y, radius, startAngle, endAngle, drawCounterClockwise(BOOL)) // start angle is what angle do we start the arc and end angle is how long do we want the arc to go on for.
c.stroke() // draw outline

c.beginPath();
c.arc(300,300,50,0, Math.PI * 2, false)
c.stroke();
```

