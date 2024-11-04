# Java Script for React

When using React we can, and should, use the latest features of JavaScript

Here are some common things we will use frequently: 

## Functions


There are (at least) 3 ways to define  a function in JavaScript. 
Each function below does the same thing: It takes one parameter and returns it with some text. 


### `function`
This type of function delaration is the oldest one. It has 2 things the arrow functions don't have: 

- These functions are hoisted, which means that we can call the function before it is declared. 
- These functions has its access to a `this`, which either refferst to the global object (window in Browser), or to the object, if we use this `function` keyword to declare a method in an object. 
- In these functions we can access `arguments` to see all the parameters passed to the function 

``` js
function myFunction (name){
  return 'Hi from a function' + name
}
```

### `=>(){}` Arrow function with body
- These functions are not hoisted, which means that we can must declare the function before we can use it (or import it form an other file before using). 
- These functions do not have  access to a `this`, but `this` is an empty object. 
- No `arguments` in the function.

``` js
const myArrowFunction = (name) => {
  return 'Hi from an arrow function' + name
}
```


### Arrow function in one line
When the function only has a return value, we can skip the curly brackets for the body and return the value in one line. 

``` js
const short = (name) => 'Hi' + name
```


They are all called the same way:
``` js
let result1 = myFunction('Ann')
let result2 =myArrowFunction('Ben')
let result3 =short('Cory')

console.log(result1);
console.log(result2);
console.log(result3); 
```

### Declating default values of parameters in functions: 

```js
const myFunc = ( a = 10, b = 'default value') => {
  // a will be 10 and b 'default value' if there is no value passed in. 
}

```
## Arrays

Working with arrays in React, we must always ue methods that do not change the original array (state must not be changed), but create a copy of the array with the changes we want to make. 
Thes means taht we rarly use `push`, `pop`, `shift` and `unshift` or loops like `forEach` in React.
Two very usefull methods are `map` and `filter`. 

### Map and filter

When we want to access each element in the array we use map: 

``` js
myArray = [1, 2, 3, 4]


let mynewArray = myArray.map((number, index) => { return number * 2
})

```

When we want to remove some elements from an  array we use filter: 

``` js
let myFilteredArray = myArray.filter((number, index) => {
  return number === 2
})
console.log('filtered', myFilteredArray);
console.log('new array', mynewArray);
```

### Spread Operator with arrays
To aviod changing the original array, we can also use the spread operator when we need to copy an array: 

``` js 
let werktage = ['Montag', 'Dienstag', 'Mittwoch', 'Donnerstag', 'Freitag']
let wochenende = ['Samstag', 'Sonntag']

let woche = [...werktage, ...wochenende]
console.log(woche);

// wir können auch hier kopien erstellen: 
let neueWoche = [...woche]
// Die Kopien sind nicht die selben wie die ursprünglichen Objekte. 

```

### Rest operator with arrays
With the rest operator, we can create a new array containg parts of an existing array. In the example below we create a new array `food` containg ["bread", "cakes", "pizza"]. 


 ``` js
let [fruit, vegetable, ...food] = ["banana", "cucumber", "bread", "cakes", "pizza"];
console.log(fruit, vegetable, food);
```
## Objects
### Accessing properties of objects
``` js
let person = {
  name: 'Diana',
  age: 45,
  city: 'Berlin'
}

console.log(person.city);
console.log(person["city"]);

```
Using a loop to access all properties: 

``` js
for (let prop in person) {
  console.log( 'for in', prop);
}
```

And using the `[]` notation to find the value: 
``` js
for (let eig in person) {
  console.log(person[eig]);
}
```


### Optional chaining: 
With optional caining, we can avoid getting errors in the code if a property is missing: If it is not there, we just get `undefined`. Without optional chaining we get an error. 

``` js
let hausNummer = person.adresse.nummer

let nichtdaNummer = person.telefon?.nummer
console.log(hausNummer, nichtdaNummer);
```

In an array of objects this looks like this: Example data from this API call: `https://api.dictionaryapi.dev/api/v2/entries/en/${word}`
```js
  const { word, meanings } = data[0];
          const explanation = meanings[0]?.definitions[0]?.definition;

```
### Spread Operator with Objects
When we work with object in React, we always create a copy and work on this. 

There are 2 usefull operators for this: the Spread and the rest operator: 

#### spread

``` js
let person1 = {
  name: 'Arne', 
  alter: 55
}

let personKopie = {...person1}

console.log(person1, personKopie);
```
This is the same as working with the older method `Object.assign`
``` js
let altePerson = Object.assign({}, person1)
console.log('alte art', altePerson);
```
We can also use the spread operator to combine 2 objects. 
``` js
let neueEigenschaften = {
  hobby: 'angeln', 
  sternzeichen: 'fisch' 
}

let neuePerson = {...person1, ...neueEigenschaften}
console.log({neuePerson});
```

### Rest in objects
``` js
let {g, d, ...ubrig} = {g: 10, d: 20, e: 30, f: 40}
g; // 10 
d; // 20 
ubrig; // { e: 30, f: 40 }
console.log(ubrig);
``` 

### Destructuring Objects

Sometimes we only want a part of an object, a given property. We can use distructuring to extract the property we are interested in. In the example below, city is copied from the original object, and name is also copied but given an new name `personName`. 


``` js
let { city, name : personName } = person
console.log('destructured city', city, personName);
```

This also works with  nested properties: 

```js
const hero = {
    name: 'Batman',
    realName: 'Bruce Wayne',
    address: {
      city: 'Gotham'
    }
  };
  
  // Object destructuring: Geife auf dem city in hero.address zu:
  const { address: { city } } = hero;
  
  city; // => 'Gotham'

```

Often we use destructuring when we pass an object to a function, but only want a part of the object. 

``` js 
const getName = ({name, realName}) => {
  return `${name}'s real name is ${realName}.`
}
```

This also works in call back functions of map or filter: 
``` js
  const names = heroes.map(({ name }) => {
      return name;
    }
  );
  
```

## Template strings

Template strings allow us to mix text and varibales (or other js) in a string. 

```js 
let variable = 'already declared variable'
let myTemplate = `Here is some Text and some content from a ${variable}.`

```

This can also be used when creating elements like so: 
``` js
  document.getElementById('myTag').innerHTML = `<p> ${text.name} </p>`
```
