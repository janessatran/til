# Fundamentals of JavaScript 
questions from The [The Odin Project](https://www.theodinproject.com/courses/web-development-101/lessons/fundamentals-part-1)

#### How do you declare a variable?
Declare a variable using the `let` keyword. The old way is to use `var`. 
```javascript
let message = 'Hello!';

// can also declare multiple vars at once
let user = 'Janessa', 
    age = 99, 
    message = 'Hello';
```
<br>

#### What are three different ways to declare a variable?
You can use `var`, `let`, or `const`. The main differences between `var` and `let/const` are that:
1. `var` variables have no block scope. For example:
```javascript
if (true) {
  var test = true;
}

alert(test); // true, the variable lives after the if block
```
If a code block is inside a function, then `var` becomes a function-level variable:
```javascript
function printGreeting() {
  if (true) {
    var phrase = "Hello!";
  }
  alert(phrase); // will print Hello
}

printGreeting();
alert(phrase); // Error: phrase not defined
```
2. `var` declarations are processed at function start. For example, the below code will run
```javascript
function var printGreeting() {
  if (true) {
    phrase = "Hello";
    alert(phrase);
    var phrase;
  }
}
printGreeting();
```
<br>

#### Which one should you use when?
`var`: when you don't need block scope.
`let`: when you want to constrain the scope.
`const`: when the value you are assigning will not be redeclared; const also has limited scope.
#### What are the rules for naming variables?
#### What are operators, operands, and operations?
#### What is concatenation and what happens when you add numbers and strings together?
#### What are the different type of operators in JavaScript?
#### What is the difference between == and ===?
#### What are operator precedence values?
#### What are the increment/decrement operators?
#### What is the difference between prefixing and post-fixing them?
#### What are assignment operators?
#### What is the “Unary +” Operator?

#### What are the seven data types of javascript?
#### Which data type is NOT primitive?
#### What is the difference between single, double, and backtick quotes for strings?
#### Which type of quote lets you embed variables/expressions into a string?
#### How do you embed variables/expressions into a string?
#### How do you escape characters in a string?
#### What is the difference between slice/substring/substr?
#### What are methods?
#### What are the three logical operators and what do they stand for?
#### What are the comparison operators?
#### What is nesting?
#### What are truthy and falsy values?
#### What are the falsy values in Javascript?
#### What is the syntax for an if/else if/else conditional?
#### What is the syntax for a switch statement?
#### What is the syntax for a ternary operator?
#### What is the relationship between null and undefined?
#### What are conditionals?
