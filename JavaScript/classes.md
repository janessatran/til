# Classes(ES6)

## Questions/Topics Covered:
- [What does the basic class syntax look like? (Try to write it first on paper!!)](#class-syntax)
- [What is a class in JavaScript?](#class)
- [Why can't we just considered the `class` keyword to be syntactic sugar?](#class-syntactic-sugar)
- [How would you re-write the User class using pure functions?](#class-prototype)
- [What is a class expression?](#class-expression)
- [How would you create getters and setters in JavaScript classes?](#class-getters-setters)
- [(T/F): when creating class properties, it is placed into the prototype of the object.](#class-properties)
- [What are static methods in classes?](#static-methods)
- [What does the `extends` keyword do?](#extends)
- [What are mix-ins?](#mixins)


<h4 id="class-syntax">
  What does the basic class syntax look like?
</h4>

```javascript
class MyClass {
  prop = value; // property
  
  constructor(...) { // constructor
    // ...
  }
  
  method(...) {...} // method
  
  // getter
  get something() {
    return this._something;
  }
  
  // setter
  set something(val) {
    this._something = val;
  }
}
```
`MyClass` is technically a function (the one we provide as `constructor`), while methods, getters, and setters are written to `MyClass.prototype`.

<h4 id="class">
  What is a class in JavaScript?
</h4>
In JavaScript, a class is a kind of function that emulates object creation that can be accomplished by Object Oriented languages like Java or Ruby. ES6 introduced a syntax for object creation using the `class` keyword, but it's functionally the same as using object constructors and prototypes. 

```javascript
class User
  constructor(name) {
    this.name = name;
  }
  
  sayHi() {
    alert(this.name);
  }
}

// usage:
let user = new User("Janessa");
user.sayHi();
```

Above is an example of how to use the `class` keyword to create a "class" in JavaScript. When `new User("Janessa")` is called:
1. A new object is created with the methods in the class available to it.
2. The `constructor` runs with the given argument (Janessa) and assigns `this.name` to it.

<h4 id="class-syntactic-sugar">
  Why can't we just considered the `class` keyword to be syntactic sugar?
</h4>
1. A function created by `class` is labelled by a special internal property `[[FunctionKind]]:"classConstructor".
2. Unlike a regular function, a class constructor must be called with `new`:

```javascript
class User {
  constructor() {}
}

alert(typeof User); // function
User(); // Error: Class constructor User cannot be invoked without 'new'
```
3. Class methods are **non-enumerable.**
   - An **enumerable property** is one that can be included in and visited during `for..in` loops (or a similar iteration of properties, like Object.keys() ).
4. Classes always `use strict`. All code inside the class construct is automatically in strict mode. 
    - The purpose of "use strict" is to indicate that the code should be executed in "strict mode". With strict mode, you can not, for example, use undeclared variables.
    
<h4 id="class-prototype">
  How would you re-write the User class using pure functions?
</h4>

**Using `class` keyword:**
```javascript
class User
  constructor(name) {
    this.name = name;
  }
  
  sayHi() {
    alert(this.name);
  }
}

// usage:
let user = new User("Janessa");
user.sayHi();
```

**Using pure functions**:
```javascript
// Create constructor function
function User(name) {
  this.name = name;
}

// Add method to prototype
User.prototype.sayHi = function() {
  alert(this.name);
};

// Usage:
let user = new User("Janessa");
user.sayHi();
```

<h4 id="class-expression">
  What is a class expression?
</h4>

It is a way to define a class and assigning ito to an expression. They can be named or unnamed. If named, the name of the class is local to the class body only. Classes can be defined inside another expression, passed around, returned, assigned, etc.

Example:
```javascript

// unnamed
let User = class {
  sayHi() {
    alert("Hello");
  }
};

// named
let User = class MyClass {
  sayHi() {
    alert(MyClass); // MyClass name is visible only inside the class
  }
};

new User.sayHi(); // works, show MyClass definition
alert(MyClass); // error, MyClass isn't visisble outside the class
```

It is also possible to make classes dynamically:
```javascript
function makeClass(phrase) {
  // declare a class and return it
  return class {
    sayHi() {
      alert(phrase);
    }
  };
}

// create new class
let User = makeClass("hello");
new User().sayHi(); // hello
```

<h4 id="class-getters-setters">
  How would you create getters and setters in JavaScript classes?
</h4>

```javascript
class User {

  constructor(name) {
    this.name = name;
  }
  
  get name() {
    // We prefix the variable with an underscore so that 
    // we don't trigger an infinite loop.
    // The variable needs to have a different name that the getter/setter.
    return this._name; 
  }
  
  set name(value) {
    if(value.length < 4) {
      alert("name too short!");
      return;
    }
    this._name = value;
  }
  
}

let user = new User("James");
alert(user.name); // James

user = new User(""); // name too short!
```

<h4 id="class-properties">
  (T/F): when creating class properties, it is placed into the prototype of the object.
</h4>
False. The property of a class is created by `new` before calling the constructor and is the property of the object itself.

```javascript
class User {
  name = "Janessa";
  
  sayHi() {
    alert(`Hello, ${this.name}!`);
  }
}

new User().sayHi();
```

<h4 id="static-methods">
  What are static methods in classes?
</h4>
The `static` keyword defines a static method for a class. They can be called without instantiating the class and **cannot** be called through a class instance. They are often used to create utility functions for an application.

Example:
```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);

console.log(Point.distance(p1, p2)); // 7.0710678118654755
```
<h4 id="extends">
  What does the `extends` keyword do?
</h4>
The `extends` keyword is used in class declarations or class expressions to create a class as a child of another class.

Example:
```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  // if there is a constructor in the subclass, 
  // it needs to call super() before using "this".
  constructor(name) {
    super(name); // call the super class constructor and pass in the name parameter
  }
  
  speak() {
    console.log(`${this.name} barks.`);
  }
}

let d = new Dog('Kody');
d.speak(); // Kody barks.
```

<h4 id="mixins">
  What are mix-ins?
</h4>

**Mix-ins**, or abstract subclasses, are templates for classes. An ECMAScript class can only have a single superclass, so multiple inheritance from tooling classes it not possible. The functioanlity must be provided by the superclass. 
To implement mix-ins in ES6:
1. Create a function with a superclass as input
2. Get the subclass extending that superclass as output

Example:
```javascript
let calculatorMixin = Base => class extends Base {
  calc() {...}
};

let randomizerMixin = Base => class extends Base {
  randomize() {...}
};

// The class using these mix-ins is written like this
class Foo {}
class Bar extends calculatorMixin(randomizerMixin(Foo)) {}
```
