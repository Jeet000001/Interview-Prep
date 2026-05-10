# 1. Variables & Basics

## 1. Difference between var, let, and const

#### var :-

var is the old way of declaring variables before ES6.

##### Features:

- Function scoped
- Can be re-declared
- Can be re-assigned
- Hoisted with undefined

##### Example:

```js
var name = "Jeet";
var name = "Paul"; // allowed

name = "Developer"; // allowed

console.log(name);
```

##### Scope Example:

```js
if (true) {
  var age = 22;
}

console.log(age); // 22
```

Because var is function scoped, it ignores block scope.

#### let :-

Introduced in ES6.

##### Features:

- Block scoped
- Cannot be re-declared in same scope
- Can be re-assigned
- Hoisted but stored in Temporal Dead Zone (TDZ)

##### Example:

```js
let city = "Kolkata";

city = "Delhi"; // allowed

console.log(city);

let a = 10;
let a = 20; // Error
```

##### Scope Example:

```js
if (true) {
  let score = 100;
}

console.log(score); // Error
```

let respects block scope.

#### const :-

Also introduced in ES6.

##### Features:

- Block scoped
- Cannot be re-declared
- Cannot be re-assigned
- Value must be initialized during declaration

##### Example:

```js
const pi = 3.14;

pi = 10; // Error
```
