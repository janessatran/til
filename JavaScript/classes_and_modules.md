# Classes and Modules (ES6)

## Questions/Topics Covered:
- [What is a class in JavaScript?](#class)

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
