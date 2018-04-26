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
Constants are block-scoped, much like variables defined using the let statement.\
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
item,key => {...} //error
(item,key)=> {...} //okay
```
