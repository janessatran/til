## Design Patterns


## Questions/Topics Covered:
- [What is a factory function?](#factory-functions)
- [What is the scope of functions created inside a function?](#factory-functions-scope)
- [What is closure?](#closures)
- [In the context of Factory Functions, what do closures enable us to do?](#factory-functions-closures)
- [How do we accomplish prototypal inheritance with factory functions?](#factory-functions-inheritance)
- [What is an Immediately Invoked Function Expression (IIFE)?](#IIFE)
- [How are Modules different from Factory Functions?](#modules-and-factories)
- [What is a useful side-effect of encapsulating the inner-workings of our programs?](#encapsulation)
- [If you need one of something, should you use a factory or a module?](#module-or-factory)
<h4 id="factory-functions">
  What is a factory function?
</h4>

When a function returns an object, we call it a **factory function**. For example:

```javascript
function personFactory = (name, age) => {
  const sayHello = () => console.log('hello!');
  return { name, age, sayHello };
};

const janessa = personFactory('janessa', 99);
console.log(janessa.name); // 'janessa'

janessa.sayHello(); // calls the function and logs 'hello!'
```

The same thing created using the Constructor pattern would look like this:
```javascript
const Person = function(name, age) {
  this.sayHello = () => console.log('hello!');
  this.name = name;
  this.age = age;
};

const janessa = new Person('janessa', 99);
```

**note**: In 2015, JS was updated so that you could shorthand return the object. Before you'd have to do something like `return {name: name, age: age, sayHello: sayHello}`.
With this update, we can turn our variables into objects with brackets (which helps us decipher the output).

```javascript
const name = "Janessa"
const color = "green"
const number = 8
const food = "pizza"

console.log(name, color, number, food) // Janessa green 8 pizza
console.log({name, color, number, food}) // {name: 'Janessa', color: 'green', number: 8, food: 'pizza'}
```

<h4 id="factory-functions-scope">
  What is the scope of functions created inside a function?
</h4>
Only functions that are returned can be accessed outside of the function itself. For example:

```javascript
const FactoryFunction = string => {
  const capitalizeString = () => string.toUpperCase();
  const printString = () => console.log(`---${capitalizeString()}---`);
  return { printString };
}

const temp = FactoryFunction('hello');
printString(); // ERROR
capitalizeString(); // ERROR
temp.capitalizeString(); // ERROR
temp.printString(); // prints "---HELLO---"
```

<h4 id="closures">
  What is closure?
</h4>
The idea that functions retain their scope even if they are passed around and called oustide of that scope. This is what enables the `printString()` function in the example above to be able to access the `capitalizeString()` function, even if it gets called outside of `FactoryFunction`.

<h4 id="factory-functions-closures">
  In the context of Factory Functions, what do closures enable us to do?
</h4>
Closures allow us to create private variables and functions in the context of Factory Functions. In our example above, `printString` would be considered public (accessible outside the function), while `capitalizeString` would be considered private. 

<h4 id="factory-functions-inheritance">
  How do we accomplish prototypal inheritance with factory functions?
</h4>
We can pull out the function we want from another Object and assign it to our own Object. The advantages include being able to pick and choose which functions you want to include in your new object. For example:

```javascript
const Human = (name) => {
  const sayName = () => console.log(`my name is ${name}`)
  return {sayName}
}

const Dwarf = (name) => {
  const {sayName} = Person(name)
  const laugh = () => console.log('hahaha!')
  return { sayName, laugh }
}

const rurik = Dward('Rurik')
rurik.sayName() // my name is Rurik
rurik.laugh() // hahaha
```

It is also possible to lump all of another object into your new object using `Object.assign`:

```javascript
const Dwarf = (name) => {
  const prototype = Person(name)
  const laugh = () => console.log('hahaha!')
  return Object.assign({}, prototype, {laugh})
}
```

<h4 id="IIFE">
  What is an Immediately Invoked Function Expression (IIFE)?
</h4>
It is when you wrap a function in paraenthesis and immediately call the function by adding `()` to the end of it.

<h4 id="modules-and-factories">
  How are Modules different from Factory Functions?
</h4>

The concepts are exactly the same, but instead of creating a factory that we re-use to create multiple objects, **module pattern** wraps the factory in an IIFE. 

This is what the module pattern looks like: 
```javascript
const calculator = (() => {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return { add, sub, mul, div, };
})();

calculator.add(3, 5) // 8
calculator.sub(6, 2) // 4
calculator.mul(3, 4) // 12
```

In our example above, the function inside the Immediately Invoked Function Expression (IIFE) is a simple factory function, but we can go ahead and assign the object to the variable `calculator` since we aren't going to making several calculator objects. 

<h4 id="encapsulation">
  What is a useful side-effect of encapsulating the inner-workings of our programs?
</h4>

**Namespacing** which helps us avoid naming collisions in our programs.

<h4 id="module-or-factory">
  If you need one of something, should you use a factory or a module?
</h4>

If you only need one of something, you should use a module. If you need multiple instances of that thing, use a factory.
