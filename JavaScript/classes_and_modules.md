# Classes and Modules (ES6)

## Questions/Topics Covered:
- [What is a class in JavaScript?](#class)
- [Why can't we just considered the `class` keyword to be syntactic sugar?](#class-syntactic-sugar)
- [How would you re-write the User class using pure functions?](#class-prototype)

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
    // We prefix the variable with an underscore so that we don't trigger an infinite loop
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
