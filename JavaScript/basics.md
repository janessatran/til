# JavaScript Basics

## Variables
Variables are containers that you can store values in. You start by delcaring a variable with the `var` keyword, followed by any name you want to call it.
```javascript
var myVariable = 'Janessa';
```
*Note: JavaScript is case sensitive*

Variables may hold values that have different datatypes:

| Variable | Explanation | Example |
|----------|-------------|---------|
| String   | A sequence of text. | var myVariable = 'Janessa'; |
| Number   | A number; numbers don't have quotes around them | var myVariable = 1; |
| Boolean  | True/False. The words `true` and `false` are keywords in JS | var myVariable = true; |
| Array    | A structure that allows you to store multiple values in one single reference. | var myVariable = [1, "Bob", "AJ", 10]; |
| Object   | Basically anything... everything in JS is an object. | var myVariable = document.querySelector('h1'); |

## Conditionals
Conditionals are code structures which allow you to test if an expression returns true or not, running alternative code revelead by its results.
```javascript
var iceCream = 'strawberry'
if(iceCream === 'strawberry') {
  alert('Yay, I love strawberry ice cream!!!!');
} else {
  alert('Not my favorite... but it's still ice cream!');
}
```

## Functions
Functions are a way of packaging functionality that you wish to reuse. When you need the procedure you can call a function with the function name, instead of rewriting the entire code each time.
```javascript
function multiply(num1,num2) {
  var result = num1 * num2;
  return result;
}
```

## Events
These are code structures which listen for things happening in browser, running code in response. The most obvious example is the click event, which is fired by the broswer when you click on something with your mouse. 
```javascript
document.querySelector('html').onclick = function() {
  alert('Ouch! Stop picking me!');
}
```
## Constructor
The `constructor` method is a special method for creating and initializing an object created within a `class`.
```javascript
class Polygon {
  constructor() {
    this.name = "Polygon";
  }
}

var poly1 = new Polygon();
console.log(poly1.name);
// expected output: "Polygon"
```

```javascript
class Square extends Polygon {
  constructor(length) {
    // Here, it calls the parent class' constructor with lengths
    // provided for the Polygon's width and height
    super(length, length);
    // Note: In derived classes, super() must be called before you
    // can use "this". Leaving this out will cause a reference error.
    this.name = 'Square';
}

get area() {
  return this.height * this.width;
}

set area(value) {
    this.area = value;
  }
}
```
