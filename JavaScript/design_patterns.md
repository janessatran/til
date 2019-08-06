## Design Patterns


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
