# Basics in React
Notes I took while reading "The Road to React".


## Questions/Topics Covered:
- [What is local component state?](#local-component-state)
- [What is an object initializer (ES6)?](#es6-object-initializer)


<h4 id="local-component-state">
  What is local component state?
</h4>
Local component state, aka "internal component state", allows you to save, modify, and delete properties stored in your component. An ES6 class component uses a constructor to initilaize local component state:

```Javascript
class App extends Component {
  constructor(props) {
    super(props); // sets this.props in your constructor
  }
  ...
}
```

<h4 id="es6-object-initializer">
  What is an object initializer?
</h4>
An object initializer is an expression that describes the intialization of an Object. Objects consist of properties which are used to describe an object. To initialize an object, you can create a comma-delimited list of zero or more pairs of properties, names, and values enclosed in curly braces. 

```Javascript
const user = {
  name: 'Janessa',
  email: 'janessa@email.com'
}
```

You can access properties with dot or backet notation:
```javascript
user.name; // 'Janessa'
user['email']; // 'janessa@email.com'
```
