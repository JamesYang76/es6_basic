# es6_basic

### let and const
#### let
The let statement declares a block scope local variable, optionally initializing it to a value
```javascript
let foo = 'bar1';
console.log(foo); // bar1
 
if (true) {
  console.log(foo); // Uncaught ReferenceError: foo is not defined
  let foo = 'bar2';
}
 
console.log(foo); //bar1
```
#### const
Constants are block-scoped, much like variables defined using the let statement\
The value of a constant cannot change through re-assignment, and it can't be redeclared.
```javascript
const number = 42;

try {
  number = 99;
} catch(err) {
  console.log(err);
  // expected output: TypeError: invalid assignment to const `number'
}
console.log(number);// expected output: 42
```

### Destructuring assignment
expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables\
#### Object destructuring
```javascript
const user = { firstname: 'Robin',lastname: 'Wieruch',};
const { firstname, lastname } = user;
```
#### Array destructuring
```javascript
var [a=5, b=7] = [1];

var [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]
```
### Template literals
Template literals are enclosed by the back-tick (` `)  character instead of double or single quotes.\
Template literals can contain placeholders. These are indicated by the dollar sign and curly braces (${expression})
```javascript
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and not ${2 * a + b}.`);

```
### Spread syntax
#### object
```javascript
const userNames = { firstname: 'Robin', lastname: 'Wieruch' };
const age = 28;
const user = { ...userNames, age };
console.log(user); // output: { firstname: 'Robin', lastname: 'Wieruch', age: 28 }

‘const userNames = { firstname: 'Robin', lastname: 'Wieruch' };
const userAge = { age: 28 };
const user = { ...userNames, ...userAge };
console.log(user); // output: { firstname: 'Robin', lastname: 'Wieruch', age: 28 }
```
#### array
```javascript
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes']; //["head", "shoulders", "knees", "and", "toes"]

var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1 = [...arr1, ...arr2];//same as arr1 = arr1.concat(arr2);
```

### function
```javascript
function sum(x, y, z) {
  return x + y + z;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers));// expected output: 6
```

### import and export
```javascript
//file1.js
const firstname = 'robin';
const lastname = 'wieruch';
export { firstname, lastname };

//file2.js
import { firstname, lastname } from './file1.js';
console.log(firstname);//output: robin

import * as person from './file1.js';
console.log(person.firstname);// output: robin

import { firstname as foo } from './file1.js';
console.log(foo);// output: robin
```
```javascript
//file1.js
const robin = {
  firstname: 'robin',
  lastname: 'wieruch',
};
export default robin;

//file2.js
import developer from './file1.js';
console.log(developer);// output: { firstname: 'robin', lastname: 'wieruch' }
```
```javascript
//file1.js
const firstname = 'robin';
const lastname = 'wieruch';
const person = { firstname, lastname,};
export { firstname,lastname,};
export default person;

//file2.js
import developer, { firstname, lastname } from './file1.js';
console.log(developer); // output: { firstname: 'robin', lastname: 'wieruch' }
console.log(firstname, lastname); // output: robin wieruch
```
```javascript
export const firstname = 'robin';
export const lastname = 'wieruch';
```

### Arrow function
#### this
An arrow function expression has a shorter syntax than a function expression and does not have its own `this, arguments, super, or new.target`.
```javascript
function Person() {
  // The Person() constructor defines `this` as an instance of itself.
  this.age = 0;

  setInterval(function growUp() {
    // In non-strict mode, the growUp() function defines `this` 
    // as the global object (because it's where growup() is executed.), 
    // which is different from the `this` defined by the Person() constructor. 
    this.age++;
  }, 1000);
}
var p = new Person();


function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}
var p = new Person();
```
#### body
In a concise body, only an expression is specified, which becomes the explicit return value.\
In a block body, you must use an explicit return statement.
```javascript
var func = x => x * x; // concise body syntax, implied "return"
var func = (x, y) => { return x + y; }; // with block body, explicit "return" needed

var func = () => { foo: 1 };// Calling func() returns undefined!
var func = () => ({foo: 1});
let callback;
callback = callback || (() => {});    // ok

item => {...};//okay
item,key => {...}; //error
(item,key)=> {...}; //okay
```
### class
#### class expressions and class declarations
```javascript
// class declaration
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

//class expression is another way to define a class.
// unnamed
var Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name); // output: "Rectangle"

// named
var Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name); // output: "Rectangle2"
```
#### Prototype methods and static methods
```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
}
const square = new Rectangle(10, 10);
console.log(square.area); // 100

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
#### extend
If there is a constructor present in subclass, it needs to first call super() before using "this".\
The super keyword is used to call corresponding methods of super class.
```javascript
class Cat { 
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Lion extends Cat {
  constructor(name) {
     super(name); // because of constructor, super is mandotary,
  }
  speak() {
    super.speak();
    console.log(this.name + ' roars.');
  }
}

var l = new Lion('Fuzzy');
l.speak(); 
```
### Object
#### initialize 
The list variable name and the state property name share the same name.
```javascript
var name = 'Robin';
var user = { name: name,};//es5

const name = 'Robin';
const user = { name,};//es6


var user = { name: 'Robin',};// ES5

// ES6
const key = 'name';
const user = { [key]: 'Robin',};
```
```javascript
// ES5
var userService = {
  getUserName: function (user) {
    return user.firstname + ' ' + user.lastname;
  },
};

// ES6
const userService = {
  getUserName(user) {
    return user.firstname + ' ' + user.lastname;
  },
};
```
#### Object.assign()
The Object.assign() method is used to copy the values of all enumerable own properties from one or more source objects to a target object.\
It will return the target object.
```javascript
//Object.assign(target, ...sources)

var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }

var o1 = { a: 1 };
var o2 = { b: 2, shallow:{d:0} };
var o3 = { c: 3 };
var obj = Object.assign(o1, o2, o3);

o1.a = 10;// also obj.a is 10
o2.b = 20;// obj.b and o1.b are 2
o2.shallow.d = 999;// does not support deep clone,so obj.shallow.d and o1.shallow.d are 999;

```
