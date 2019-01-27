# Array methods in JS

## filter() 
Creates a new array with all elements that pass the test implemented by the provided callback function. 

```js
var names = ['Oscar', 'Anna', 'Leo', 'Kalyn', 'Joe', 'Jim', 'Samantha', 'Sam'];

// filter for people with names that are 3 characters long or less 
const result = names.filter(name => name.length <= 3);

console.log(result);
// expected output: Array ['Leo', 'Joe', 'Jim', 'Sam'];


```

## map() 
Creates a new array with the results of calling a provided function on every element in the calling array.

```js
var roster = {
              {firstName: "Oscar", lastName: "Tran", birthYear: 1992},
              {firstName: "Anna", lastName: "Nguyen", birthYear: 1990},
              {firstName: "Leo", lastName: "Smith", birthYear: 1999},
              {firstName: "Joe", lastName: "Schmoe", birthYear: 2001},
              {firstName: "Jim", lastName: "Jam", birthYear: 1991},
              {firstName: "Sam", lastName: "Ham", birthYear: 2002}
             }

// get first name and last names from roster
const names = roster.map(person => ( `${person.firstName} ${person.lastName}` ));
```

## sort()
Sorts the elements of an array in place and returns the array. 

```js
var names = ['Oscar', 'Anna', 'Leo', 'Kalyn', 'Joe', 'Jim', 'Samantha', 'Sam'];

// sort names in alphabetical order
const sortedNames = names.sort();

// sort roster by birthYear using ternary operator
const sortedBirth = roster.sort((a,b) a.birthYear > b.birthYear ? 1 : -1);

```
## reduce()
Executes a provided reducer function on each member of the array, resulting in a single output value.

```js
var array = [1, 2, 3, 4, 5];

// get the average age of people in roster (at the current age in year 2018)
const avgAge = roster.reduce((total, person) => { 
  return total + (2018 - person.birthYear) ;
}, 0);
```
