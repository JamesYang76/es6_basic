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
