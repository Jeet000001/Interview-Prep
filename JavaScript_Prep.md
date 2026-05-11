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

## 2. Difference between == and ===

In JavaScript, both == and === are comparison operators, but they work differently.

#### == (Loose Equality) :-

== compares only values not the types, and in == JavaScript perform type coercion.
That means JavaScript tries to convert the operands into the same type automatically before comparing.

```js
console.log(5 == "5"); // true
console.log(false == 0); // true
console.log(null == undefined); // true
console.log("" == 0); // true
```

Because JavaScript converts "5" (string) into 5 (number).

#### === (Strict Equality) :-

=== compares both the value and type and it is more safer than == and in === type conversion not happens.

##### Example:

```js
console.log(5 === "5"); // true
```

## 3. Difference between null and undefined

#### undefined :-

A variable has been declared, but no value has been assigned yet.
JavaScript automatically assigns undefined.

```js
let name;

console.log(name); // undefine
```

Because the variable exists, but no value is assigned.

#### null :-

Intentional absence of value. It is assigned manually by the developer.

```js
let data = null;

console.log(data); // null
```

```js
console.log(typeof undefined); //undefine
console.log(typeof null); // object
```

## 4. What are truthy and falsy values?

#### Falsy Values :-

Falsy values are values that become false when converted to boolean.

JavaScript has only a few falsy values.

##### All Falsy Values in JavaScript

```js
false;
0 - 0;
0n;
("");
null;
undefined;
NaN;
```

##### Example:

```js
if (0) {
  console.log("Hello");
} else {
  console.log("Falsy");
} // Falsy
```

#### Truthy Values :-

Anything that is NOT falsy is truthy.

##### Examples of Truthy Values

```js
true
1
-1
"hello"
[]
{}
"0"
"false"
function(){}
```

Even empty arrays and empty objects are truthy.

## 5. What is hoisting?

Hoisting is JavaScript's default behavior where Variable and function declarations are moved to the top of their scope during the memory creation phase before code execution.

But only declarations are hoisted, not initializations.

##### Example with var :

```js
console.log(a); //undefined

var a = 10;
```

JavaScript internally treats it like this:

```js
var a;

console.log(a);

a = 10;
```

So the declaration is hoisted, but the value assignment stays in place.

Hoisting with let and const
let and const are also hoisted, but they stay inside something called the:`Temporal Dead Zone (TDZ)`
until initialization.

##### Examople :

```js
console.log(b);

let b = 20; // ReferenceError
```

#### Function Hoisting

Function Declarations

Function declarations are fully hoisted

##### Example:

```js
sayHello(); // Hello

function sayHello() {
  console.log("Hello");
}
```

##### Function Expressions

Function expressions behave differently.

##### Example:

```js
sayHi(); // TypeError

var sayHi = function () {
  console.log("Hi");
};
```

So sayHi becomes undefined, and calling it as a function causes an error.

## What is Temporal Dead Zone (TDZ)?

Temporal Dead Zone (TDZ) is the time between variable hoisting and its initialization where the variable cannot be accessed.

TDZ mainly applies to:

- let
- const

##### Example :

```js
console.log(a); // ReferenceError

let a = 10;
```

##### Why Does This Happen?

Internally, JavaScript hoists a into memory, but it does not initialize it immediately.

So before this line:

```js
let a = 10;
```

the variable stays inside the Temporal Dead Zone.

## 7. Difference between primitive and non-primitive data types.

In JavaScript, data types are mainly divided into two categories:

1. Primitive Data Types
2. Non-Primitive (Reference) Data Types

The main difference is:
Primitive values are stored by value, while non-primitive values are stored by reference.

##### Primitive Data Types :

Primitive data types store a single value directly in memory.
They are: Immutable, Compared by value

JavaScript has 7 primitive types:

```js
string;
number;
boolean;
undefined;
null;
symbol;
bigint;
```

##### Non-Primitive (Reference) Data Types :

Non-primitive types store references (memory addresses).

These include:

- Objects
- Arrays
- Functions

```js
let user1 = {
  name: "Jeet",
};

let user2 = user1;

user2.name = "Paul";

console.log(user1.name); // Paul
```

Because both variables point to the same object in memory.

## 8. Difference between pass by value and pass by reference

#### Pass by Value:

In pass by value:
A copy of the actual value is passed.
So changing the copied value does NOT affect the original value.

Primitive data types work this way.

```js
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

Because b gets a separate copy of a.

#### Pass by Reference :

In pass by reference:
The memory reference (address) is copied instead of the actual value.

Non-primitive data types work this way.

##### Example :

```js
let user1 = {
  name: "Jeet",
};

let user2 = user1;

user2.name = "Paul";

console.log(user1.name); // Paul
```

Because both variables point to the same object in memory.

# Scope & Closures

## 9. What is scope?

Scope in JavaScript defines where variables can be accessed in the program. JavaScript mainly has global scope, function scope, and block scope. Variables declared with var are function scoped, while let and const are block scoped. JavaScript also supports lexical scoping, where inner functions can access variables from their parent scope through the scope chain.

##### Function Scope Example:

```js
function test() {
  var age = 22;

  console.log(age);
}

test(); // 22

console.log(age); // ReferenceError
```

Because age exists only inside the function.

##### Block Scope Example :

```js
if (true) {
  let city = "Kolkata";
}

console.log(city); // ReferenceError
```

Because city exists only inside the block.

##### Lexical Scope Example :

```js
function outer() {
  let name = "Jeet";

  function inner() {
    console.log(name);
  }

  inner();
}

outer(); // Jeet
```

## Difference between: global scope, function scope, block scope

#### Global Scope

A variable declared outside all functions and blocks belongs to the global scope.

It can be accessed from anywhere in the program.

##### Example:

```js
let name = "Jeet";

function show() {
  console.log(name);
}

show(); // Jeet

console.log(name); // Jeet
```

Because name is globally available.

#### Function Scope

Variables declared with var inside a function are accessible only within that function.

##### Example :

```js
function test() {
  var age = 22;

  console.log(age);
}

test(); // 22

console.log(age); // ReferenceError
```

Because age exists only inside test().

#### Block Scope

Variables declared using:

- let
- const
  inside {} are block scoped.

A block can be:

- if
- for
- while
- {}

##### Example:

```js
if (true) {
  let city = "Kolkata";
}

console.log(city); // ReferenceError
```

Because city exists only inside the block.

#### Why Scope Is Important

Scope helps:

- avoid variable conflicts
- improve memory management
- make code secure and maintainable
- support closures and encapsulation

## 11. What is lexical scope?

Lexical scope means a function can access variables from its parent scope because scope in JavaScript is determined by where functions are written in the code. Inner functions can access variables from outer functions through the scope chain. JavaScript uses lexical scoping, which is also the foundation of closures.

##### Example :

```js
function outer() {
  let name = "Jeet";

  function inner() {
    console.log(name);
  }

  inner();
}

outer(); // Jeet
```

Because inner() is lexically inside outer(),
so it can access variables from outer().

#### Scope Chain in Lexical Scope

JavaScript searches variables in this order:

1. Current scope
2. Parent scope
3. Global scope

This process is called:`Scope Chain`

## 12. What is closure?

A function that remembers and can access variables from its outer scope even after the outer function has finished execution.

##### Example :

```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const counter = outer();

counter(); // 1
counter(); // 2
counter(); // 3
```

## 13. Why are closures useful?

Closures are useful because they allow functions to:
remember and access variables from their outer scope even after the outer function has finished execution.

They are one of the most powerful features of JavaScript and are widely used in real-world applications.

#### Main Uses of Closures

Closures are mainly useful for:

- Data Privacy / Encapsulation
- Maintaining State
- Function Factories
- Callbacks & Event Handlers
- Memoization
- Module Pattern
- React Hooks and Async Operations

## 14. How can closures cause memory leaks?

Closures can cause memory leaks when: a function unnecessarily keeps references to variables or large objects that are no longer needed.

Because closures preserve outer variables in memory,
JavaScript’s garbage collector cannot remove them until all references are gone.
