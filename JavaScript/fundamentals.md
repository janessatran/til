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
- `var`: when you don't need block scope; also the old school variable declaration.
- `let`: when you want to constrain the scope; the modern variable declaration.
- `const`: when the value you are assigning will not be redeclared; const also has limited scope.
<br>

#### What are the rules for naming variables?
1. The name must contain only letters, digits, or the symbols $ and _.
2. The first character must not be a digit.
<br>

#### What are operators, operands, and operations?
- **operators**: things like addition, multiplication, subtraction, etc
- **operands**: what operators are applied to (in `5 * 2 ` there are two operands, 5 and 2)

#### What is concatenation and what happens when you add numbers and strings together?
**Concatenation** is sticking different things together to make a unit (for example, you could stick strings and variables together to make a sentence using the + operator). If you add numbers and strings together, it will concatenate the number to the string:
```javascript
let x = "2";
console.log(x + 3); // results in 23
```
#### What is the difference between == and ===?
- `===` is a strict comparison (only true if the operands are of the same type and the contents match).
- `==`: converts the operands to the same type before making the comparison. 

#### What are operator precedence values?
Operator precendence is the execution order of an expression with more than one operator.

#### What are the increment/decrement operators?
- **increment (++)**: increases a variable by 1
```javascript
let counter = 2;
counter++;
alert(counter); // 3
```
- **decrement (--)**: decreases a variable by 1
```javascript
let counter = 2;
counter--;
alert(counter); // 1
```


#### What is the difference between prefixing and post-fixing them?
When the operator goes after the variable, it is in **postfix** form, and the update is made to the variable after the expression is complete. When the operator goes before the variable, it is in **prefix** form, and the update is made to the variable before the expression is complete.

Example:
```javascript
// if we'd like to increase a value and immediately use the result, we would need the prefix form
let counter = 0;
alert(++counter); // 1

let counter = 0;
alert(counter++); // 0
alert(counter++); // 1
```


#### What is the “Unary +” Operator?
An operator is **unary** if it has a single operand. For example, the unary negation `-` reverses the sign of a number. The **Unary +** operator in JavaScript is useful to convert anything to a number (such as `+length`). If it's a number, the value doesn't change and the comparison returns true. If it's not a number, the assertion is false.

#### What are the seven data types of javascript?
1. Number
2. String
3. Boolean (`true` and `false`)
4. `null` value - represents nothing or value unknown.
5. `undefined` value - represents a value that is unassigned.
6. Objects - store collections of data.
7. Symbols - used to create unique identifiers for objects.

You can use the `typeof` operator to determine the type of the argument. There are two forms of syntax it supports:
1. `typeof x` as an operator
2. `typeof(x)` as a function
```javascript
typeof undefined // "undefined"

typeof 0 // "number"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"
```


#### Which data type is NOT primitive?
Objects

#### What is the difference between single, double, and backtick quotes for strings?
There is no difference between single and double quotes ("Hello" vs 'Hello'), but backtick quotes are "extended functionality" quotes. They allow us to embed variables and expressions into a string by wrapping them in `${...}`.
```javascript
// Example of backtick quotes expression
let name = "Janessa";

// embed a variable
alert(`Hello, ${name}!`); // Hello, Janessa!

// embed an expression
alert(`the result is ${1+1}`); // the result is 2

```

#### How do you escape characters in a string?
- Horizontal Tab is replaced with \t
- Vertical Tab is replaced with \v
- Null  is replaced with \0
- Backspace is replaced with \b
- Form feed is replaced with \f
- Newline is replaced with \n
- Carriage return is replaced with \r
- Single quote is replaced with \'
- Double quote is replaced with \"
- Backslash is replaced with \\


#### What is the difference between slice/substring/substr?
There are 3 methods in JavaScript to get a substring (slice, substrings, and substr).
- **slice**: returns the part of the string from start to end (exclusive of end). If there is no second argument, then slice goes til the end of the string.
```javascript
let str = 'hello';
alert(str.slice(0, 2)); //'he', the substring from 0 to 2 not including 2
alert(str.slice(0, 1)); // 'h'

let str = 'stringify';
alert(str.slice(2)); // ringify, from 2nd position to the end
```
- **substring**: returns the part of the string between the start and end. You can also have the start be greater than the end.
```javascript
let str = 'stringify';

// these are the same for substring
alert(str.substring(2, 5)); // "rin"
alert(str.substring(5, 2)); // "rin"

// doesn't work for slice
alert(str.substring(2, 5)); // "rin"
alert(str.substring(5, 2)); // "" empty string 
```

#### What are methods?
Blocks of code we can re-use by calling the function. Function declaration in JavaScript looks like this:
```javascript
function showMessage() {
  alert("hello, world!");
}

function showMessageWithParams(from, text) { // arguments: from, text
  alert(from + ': ' + text);
}

showMessageWithParams('Ann', 'Hello!'); // Ann: Hello! (*)
showMessageWithParams('Ann', "What's up?"); // Ann: What's up? (**)
```

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
