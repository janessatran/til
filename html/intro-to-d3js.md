## Notes on Intro to D3.js

- *html*: hypertext markup language; text format that most web pages are written in 

Basic outline of HTML page is something like:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>TITLE GOES HERE</title>
  </head>
  <body>
    MAIN CONTENT GOES HERE
  </body>
</html>
```

- *css*: cascading stylesheets; langugage for styling html pages. Also known as selectors and are applied to HTML tags based on their name, class, or ID

Applying some simple CSS rules looks like:
```html
<div>
  <p>Normal paragraph</p>

  <p class="red">Red paragraph</p>
</div>

<ol>
  <li id="some-id">Unique element</li>
  <li>Another list element</li>
  <li>
    <p>Paragraph inside list element</p>
    <p>Second paragraph</p>
  </li>
</ol>

/* Applied to all <p> tags */
p {
  color: blue;
}

/* Applied to all tags with the class "red" */
.red {
  background: red;
}

/* Applied to the tag with the id "some-id" */
#some-id {
  font-style: italic;
}

/* Applied only to <p> tags that are inside <li> tags */
li p {
  color: #0C0;
}
```

- *document object model (DOM)*: interactive object graph created by the tag hierarchy of HTML
  - handles tracking elements as they are rendered 
  - can also track events like mouse movements
  - you can attach listeners to these events to add various levels of interactivity to your page
  
```html
<div>
  <p>Normal paragraph</p>

  <p class="red">Red paragraph</p>
</div>

<ol>
  <li id="some-id">Unique element</li>
  <li>Another list element</li>
  <li>
    <p>Paragraph inside list element</p>
    <p>Second paragraph</p>
  </li>
</ol>

    
// DOM API
document.getElementById('some-id');
// <li id="some-id">Unique element</li>
document.getElementsByTagName('p').length;
// 4
var reds = document.getElementsByClassName('red');
// [<p class="red">Red paragraph</p>]
reds[0].innerText
// "Red paragraph"
    
// D3 Selection API
d3.select('p').size(); // select() only finds one
// 1
d3.selectAll('p').size(); // selectAll() finds all
// 4
var reds = d3.selectAll('.red');
// [ > Array[1] ]
reds.text();
// "Red paragraph"
    
```
- *scalable vector graphics (SVG)*: an XML format used for drawing; can apply mouse/touch listeners, CSS styles and selectors
  - CSS attributre names for SVG come from the SVG defintion, so they are sometimes different from HTML
    - to change the background color to red, you would set `background-color: red` in CSS
    - to get same effect on an SVG rectangle, you would instead use the attribute `fill: red`
    
```html
<svg width="300" height="180">
  <circle cx="30"  cy="50" r="25" />
  <circle cx="90"  cy="50" r="25" class="red" />
  <circle cx="150" cy="50" r="25" class="fancy" />

  <rect x="10"  y="80" width="40" height="40"
    fill="steelBlue" />
  <rect x="70"  y="80" width="40" height="40"
    style="fill: steelBlue" />
  <rect x="130" y="80" width="40" height="40"
    class="fancy" />
</svg>

.red {
  fill: red; /* not background-color! */
}

.fancy {
  fill: none;
  stroke: black; /* similar to border-color */
  stroke-width: 3pt; /* similar to border-width */
  stroke-dasharray: 3,5,10;
}
```
- SVG has the `<g>` tag for an arbitrary group (HTML has `<div>` and `<span>` tags)
- can use `<text>` tag for simple labels
- `<path>` tag can be used for either lines or arbitrary filled-in shapes depending on the styling
```html
<svg width="300" height="180">
  <g transform="translate(5, 15)">
    <text x="0" y="0">Howdy!</text>
  </g>

  <g transform="translate(5, 55)">
    <!-- M: move to (jump)
         L: line to
         Q: curve to (quadratic) -->
    <path d="M0,50 L50,0 Q100,0 100,50"
      fill="none" stroke-width="3" stroke="black" />
  </g>

  <g transform="translate(5, 105)">
    <!-- C: curve to (cubic)
         Z: close shape -->
    <path d="M0,100 C0,0 25,0 125,100 Z" fill="black" />
  </g>
</svg>
```
