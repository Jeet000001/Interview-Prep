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

# 3. Functions

## 16. Difference between function declaration and function expression

#### Function declaration:

A function declaration defines a named function directly and is fully hoisted, so it can be called before its definition. Function declarations are generally used for reusable utility functions.

##### Example :

```js
sayHello(); // Hello

function sayHello() {
  console.log("Hello");
}
```

#### Function expression:

A function expression stores a function inside a variable, and only the variable declaration is hoisted, not the function assignment. Function expressions are commonly used for callbacks, closures, and dynamic behavior.

##### Example:

```js
sayHi(); // ReferenceError

const sayHi = function () {
  console.log("Hi");
};
```

Because:

- sayHi exists in TDZ (const)
- function is not initialized yet

## 16. Difference between normal function and arrow function

#### Normal function:

Normal functions have their own this, support the arguments object, can be used as constructors, and have a prototype property.

#### arrow function:

Arrow functions are a shorter way to write functions introduced in ES6, but the main difference is that they do not have their own this. Instead, they inherit this from the surrounding lexical scope.

## 17. What is callback function?

A callback function is a function passed as an argument to another function and executed later after a task is completed. Callbacks are commonly used in asynchronous JavaScript, event handling, timers, and array methods.

##### Example :

```js
function greet(name, callback) {
  console.log(`Hello ${name}`);

  callback();
}

function sayBye() {
  console.log("Goodbye");
}

greet("Jeet", sayBye);
// Hello Jeet
// Goodbye
```

## 18. What are higher-order functions?

A higher-order function is a function that either accepts another function as an argument or returns a function. JavaScript supports higher-order functions because functions are first-class citizens. Common examples include map, filter, reduce, and setTimeout. Higher-order functions help create reusable, flexible, and cleaner code, and they are a core concept in functional programming.

##### Example :

###### Function Taking Another Function

```js
function greet(name) {
  return `Hello ${name}`;
}

function processUser(callback) {
  console.log(callback("Jeet"));
}

processUser(greet); // Hello Jeet
```

###### Function Returning Another Function

```js
function multiply(x) {
  return function (y) {
    return x * y;
  };
}

const double = multiply(2);

console.log(double(5)); // 10
```

## 19. What is a pure function?

A pure function is a function that always returns the same output for the same input and does not modify external state.

##### Example :

```js
function add(a, b) {
  return a + b;
}

console.log(add(2, 3)); // 5
console.log(add(2, 3)); // 5
```

Same input always gives same output.

##### Example of Impure Function

```js
let count = 0;

function increment() {
  count++;
}
```

## 20. What is recursion?

Recursion is a programming technique where a function calls itself repeatedly until a base condition is met. A recursive function typically contains a base case to stop execution and a recursive call to continue the process. Recursion is commonly used for problems like factorials, tree traversal, nested data structures, and divide-and-conquer algorithms.

##### Example:

```js
function countdown(n) {
  if (n === 0) {
    console.log("Done");
    return;
  }

  console.log(n);

  countdown(n - 1);
}

countdown(5);
// 5
// 4
// 3
// 2
// 1
// Done
```

## 21. What is currying?

A technique where a function with multiple arguments is transformed into a sequence of functions, each taking one argument at a time.

##### Example:

```js
function add(a, b, c) {
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
```

## 22. What is memoization?

An optimization technique where the result of an expensive function call is cached so that future calls with the same input can return the stored result instead of recalculating.

##### Example :

```js
function memoizedSquare() {
  let cache = {};

  return function (n) {
    if (cache[n]) {
      console.log("From Cache");

      return cache[n];
    }

    console.log("Calculating...");

    let result = n * n;

    cache[n] = result;

    return result;
  };
}

const square = memoizedSquare();

console.log(square(5));
console.log(square(5));
```

# 4. this Keyword

## 23. What is this keyword?

this is a special keyword that refers to the object that is currently executing the function. Its value depends on how the function is called. In object methods, this refers to the object itself, while in regular functions it refers to the global object or undefined in strict mode. Arrow functions do not have their own this; they inherit it lexically from the surrounding scope.

##### Example:

```js
console.log(this); // window
```

global this refers to the window object.

```js
const user = {
  name: "Jeet",

  greet() {
    console.log(this.name);
  },
};

user.greet(); // Jeet
```

Because this refers to user.

```js
function test() {
  console.log(this);
}

test(); // window
```

```js
"use strict";

function test() {
  console.log(this);
}

test(); // undefine
```

##### this Inside Arrow Function

Arrow functions do NOT have their own this.
They inherit this from surrounding lexical scope.
This is called Lexical this

```js
const user = {
  name: "Jeet",

  greet: () => {
    console.log(this.name);
  },
};

user.greet(); // undefined
```

## 24. Difference between: call, apply bind ?

Normally, this depends on how a function is called.

But sometimes we want to explicitly decide what this should refer to.

That’s where: call, apply, bind are used.

call, apply, and bind are methods used to explicitly control the value of this in JavaScript functions.

#### call() :-

call() executes the function immediately and accepts arguments separately.

###### Syntax:

```js
functionName.call(thisValue, arg1, arg2);
```

###### Example:

```js
const user = {
  name: "Jeet",
};

function greet(city) {
  console.log(`Hello ${this.name} from ${city}`);
}

greet.call(user, "Kolkata"); // Hello Jeet from Kolkata
```

#### apply() :-

apply() also executes immediately but accepts arguments as an array.

###### Syntax

```js
functionName.apply(thisValue, [args]);
```

###### Example:

```js
const user = {
  name: "Jeet",
};

function greet(city, country) {
  console.log(`Hello ${this.name} from ${city}, ${country}`);
}

greet.apply(user, ["Kolkata", "India"]); // Hello Jeet from Kolkata, India
```

#### bind() :-

bind() does not execute immediately; instead, it returns a new function with permanently bound this, which is useful for callbacks and event handlers.

###### Syntax:

```js
const newFunction = functionName.bind(thisValue);
```

###### Example:

```js
const user = {
  name: "Jeet",
};

function greet() {
  console.log(`Hello ${this.name}`);
}

const newGreet = greet.bind(user);

newGreet(); // Hello Jeet
```

## 25. Difference between shallow copy and deep copy

When copying objects or arrays in JavaScript, there are two types of copying: Shallow Copy, Deep Copy

The main difference is: how nested objects are copied.

A shallow copy copies only the top-level properties of an object, while nested objects are still shared by reference. A deep copy creates completely independent copies of all nested levels. Shallow copies are faster and commonly created using the `spread operator` or `Object.assign`, whereas deep copies can be created using `structuredClone` or other deep cloning techniques.

##### Shallow copy Example :

```js
const user1 = {
  name: "Jeet",
  address: {
    city: "Kolkata",
  },
};

const user2 = { ...user1 };

user2.name = "Paul";
user2.address.city = "Delhi";

console.log(user1.name); // Jeet
console.log(user1.address.city); // Delhi
```

###### Common Ways to Create Shallow Copy

1. Using Spread Operator

```js
const copy = { ...obj };
```

2. Using Object.assign()

```js
const copy = Object.assign({}, obj);
```

##### Deep copy Example :

```js
const user1 = {
  name: "Jeet",
  address: {
    city: "Kolkata",
  },
};

const user2 = structuredClone(user1);

user2.address.city = "Delhi";

console.log(user1.address.city); // Kolkata
```

###### Ways to Create Deep Copy

1. structuredClone()

```js
const copy = structuredClone(obj);
```

2. JSON.parse(JSON.stringify())

```js
const copy = JSON.parse(JSON.stringify(obj));
```

# Objects :

## 26. What is Destructuring?

Destructuring is an ES6 feature that allows us to: extract values from arrays or properties from objects into separate variables in a cleaner and shorter way.

###### Example:

```js
const arr = [10, 20, 30];

const a = arr[0];
const b = arr[1];

console.log(a, b); // 10, 20
```

```js
const user = {
  name: "Jeet",
  age: 22,
};

const name = user.name; // Jeet
const age = user.age; // 22
```

## 27. What is spread operator?

It was introduced in: ES6
The spread operator is represented by: `...`

It is used to: expand or unpack elements of arrays, objects, or iterable values. In simple words: spread individual values out from an array or object.

It was introduced in: ES6

###### Example :

```js
const arr1 = [1, 2, 3];

const arr2 = [...arr1];

console.log(arr2); // [1, 2, 3]
```

```js
const a = [1, 2];

const b = [3, 4];

const result = [...a, ...b];

console.log(result); // [1, 2, 3, 4]
```

```js
const user = {
  name: "Jeet",
};

const updatedUser = {
  ...user,
  age: 22,
};

console.log(updatedUser);
// {
//   name: "Jeet",
//   age: 22
// }
```

## 28. What is rest operator?

It was introduced in: ES6
The rest operator is represented by: `...`

It is used to: collect multiple values into a single array or object.
In simple words: gather remaining values together.

###### Example :

```js
function sum(...numbers) {
  console.log(numbers);
}

sum(1, 2, 3, 4); // [1, 2, 3, 4]
```

```js
const user = {
  name: "Jeet",
  age: 22,
  city: "Kolkata",
};

const { name, ...rest } = user;

console.log(rest);
// {
//   age: 22,
//   city: "Kolkata"
// }
```
## 29. What is optional chaining?
It is used to: safely access deeply nested object properties without causing errors if a value is null or undefined.

In simple words: if something does not exist, JavaScript stops and returns undefined instead of throwing an error.
###### Example : 
```js
const user = {};

console.log(user.profile?.address?.city); // undefine
```

## 30. Difference between: Object.freeze(), Object.seal()
Object.seal() prevents adding or deleting object properties but still allows modification of existing properties. Object.freeze() provides stronger protection by preventing adding, deleting, and modifying properties. Both methods are shallow, meaning nested objects can still be changed unless deep freezing is implemented.

##### Object.seal() Example :
```js
const user = {
  name: "Jeet",
  age: 22,
};

Object.seal(user);

user.age = 25;

console.log(user.age); // 25
```
###### Cannot Add or Delete Properties -
```js
user.city = "Kolkata";
console.log(user.city); // undefine

delete user.name;
console.log(user.name); // Jeet
```
##### Object.freeze() Example :
```js
const user = {
  name: "Jeet",
  age: 22,
};

Object.freeze(user);

user.age = 30;

console.log(user.age); // 22
```
Modification fails.
###### Cannot Add or Delete Properties -
```js
user.city = "Delhi";
console.log(user.city); // undefined

delete user.name;
console.log(user.name); // Jeet
```