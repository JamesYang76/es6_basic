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
