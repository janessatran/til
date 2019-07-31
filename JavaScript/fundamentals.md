# Fundamentals of JavaScript 
Questions from The [The Odin Project](https://www.theodinproject.com/courses/web-development-101/lessons/fundamentals-part-1)
This is a good resource for JavaScript [javascript.info](http://javascript.info).

## Questions/Topics Covered:
- [How do you declare a variable?](#How-do-you-declare-a-variable?)
- [What are three different ways to declare a variable?](#three-ways-declare-a-variable)
- [What are the rules for naming variables?](#naming-variables)
- [What are operators, operands, and operations?... and other operator questions](#operators)
- [What is concatenation and what happens when you add numbers and strings together?](#concat)
- [What are the seven data types of javascript?](#data-types)
- [What is the difference between single, double, and backtick quotes for strings?... and other string questions](#strings)
- [What are methods?](#functions)
- [What is nesting?](#nesting)
- [What are truthy and falsy values?.. and other things about conditionals/switch statements](#conditionals)


## Questions and Answers:
<h3 id="How-do-you-declare-a-variable?">
    How do you declare a variable?
</h3>

Declare a variable using the `let` keyword. The old way is to use `var`. 
```javascript
let message = 'Hello!';

// can also declare multiple vars at once
let user = 'Janessa', 
    age = 99, 
    message = 'Hello';
```
<br>

<h3 id="three-ways-declare-a-variable">
    What are three different ways to declare a variable?
</h3>
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

### Which one should you use when?
- `var`: when you don't need block scope; also the old school variable declaration.
- `let`: when you want to constrain the scope; the modern variable declaration.
- `const`: when the value you are assigning will not be redeclared; const also has limited scope.
<br>

<h3 id="naming-variables">
    What are the rules for naming variables?
</h3>
1. The name must contain only letters, digits, or the symbols $ and _.
2. The first character must not be a digit.
<br>

<h3 id="operators">
    What are operators, operands, and operations?
</h3>
- **operators**: things like addition, multiplication, subtraction, etc
- **operands**: what operators are applied to (in `5 * 2 ` there are two operands, 5 and 2)


### What is the difference between == and ===?
- `===` is a strict comparison (only true if the operands are of the same type and the contents match).
- `==`: converts the operands to the same type before making the comparison. 

### What are operator precedence values?
Operator precendence is the execution order of an expression with more than one operator.

### What are the increment/decrement operators?
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


### What is the difference between prefixing and post-fixing them?
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

### What is the “Unary +” Operator?
An operator is **unary** if it has a single operand. For example, the unary negation `-` reverses the sign of a number. The **Unary +** operator in JavaScript is useful to convert anything to a number (such as `+length`). If it's a number, the value doesn't change and the comparison returns true. If it's not a number, the assertion is false.


### What are the three logical operators and what do they stand for?
`||` OR, `&&` AND, and `!` NOT.

### What are the comparison operators?
They return a boolean value (operators like `>, <, ==, >=, <=`. Things to note about comparison operators:
- Strings are compared letter-by-letter in the "dictionary" order.
- When values of different types are compared, they get converted to numbers (with exclusion of a strict equlity check which is done with `===`).
- The values `null` and `undefined` equal `==` each other and do not equal any other value.
- Be careful when comparing things to `null/undefined` because there is weird behavior (so it's good to check if a value is null or undefined first).
```javascript
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
/*
The last value returns true because null is converted to a number and being treated as 0. On the other hand, null == 0 returns false because null == undefined. 
*/

// undefined values should be compared to other values at all
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```

<h3 id="concat">
    What is concatenation and what happens when you add numbers and strings together?
</h3>
**Concatenation** is sticking different things together to make a unit (for example, you could stick strings and variables together to make a sentence using the + operator). If you add numbers and strings together, it will concatenate the number to the string:
```javascript
let x = "2";
console.log(x + 3); // results in 23
```

<h3 id="data-types">
    What are the seven data types of javascript?
</h3>
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

### Which data type is NOT primitive?
Objects

<h3 id="strings">
    What is the difference between single, double, and backtick quotes for strings?
</h3>
There is no difference between single and double quotes ("Hello" vs 'Hello'), but backtick quotes are "extended functionality" quotes. They allow us to embed variables and expressions into a string by wrapping them in `${...}`.
```javascript
// Example of backtick quotes expression
let name = "Janessa";

// embed a variable
alert(`Hello, ${name}!`); // Hello, Janessa!

// embed an expression
alert(`the result is ${1+1}`); // the result is 2

```

### How do you escape characters in a string?
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


### What is the difference between slice/substring/substr?
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

<h3 id="functions">
    What are methods?
</h3>
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


<h3 id="nesting">
    What is nesting?
</h3>
A function is called a **nested** function when it is created inside another function. 
```javascript
function sayHiBye(firstName, lastName) {
  
  // helper nested function to use below
  function getFullName() {
    return firstName + " " + lastName;
  }
  
  alwert("Hello, " + getFullName());
  alert("Bye, " + getFullName());
  
}

```
A nested function can be returned as either a property of a new object or as a result by itself. 

```javascript
// Here, the nested function is assigned to the new object by the constructor function
function User(name) {
  // the object method is created as a nested function
  this.sayHi = function() {
    alert(name);
  };
}

let user = new User("Janessa");
user.sayHi(); // the method "sayHi" has access to the outer "name"

// here we just return the nested function
function makeCounter() {
  let count = 0;
  
  return function() {
    return count++; // has accees to the outer "count"
  };
}

let counter = makeCounter();
alert( counter() ); // 0
alert( counter() ); // 1
```

<h3 id="conditionals">
    What are truthy and falsy values?.. and other things about conditionals/switch statements.
</h3>
- **truthy value**: evaluates to `true` in a Boolean context
- **falsy value**: evalutes to `false` in a Boolean context

### What are the falsy values in Javascript?
undefined, null, NaN, 0, and "" (empty string)... and `false`.

### What is the syntax for an if/else if/else conditional?
```javascript
let timeOfDay = "midnight"

if (timeOfDay == "morning") {
  alert("What a great time for a cup of coffee!");
} else if (timeOfDay == "afternoon") {
  alert("Hmm... it's a toss up about whether I should drink some coffee now.");
} else {
  alert("It's too late for coffee, I should sleep!");
}
```

### What is the syntax for a switch statement?
```javascript
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small...' );
    break;
  case 4:
    alert( 'Exactly!' );
    break;
  case 5:
    alert( 'Too large...' );
    break;
  default:
 1   alert( 'I don't know such values." );
}
```

### What is the syntax for a ternary operator?
`let result = condition ? value1 : value2`

### What is the relationship between null and undefined?
`null == undefined // true` -> This is because they are both falsy values. In JavaScript, `undefined` means a variable has been declared but has not yet been assigned. `null` is an assignment value that has no value such as `let tempVar = null`.

### What are conditionals?
`if`, `else`, the ternary operator `?`.
