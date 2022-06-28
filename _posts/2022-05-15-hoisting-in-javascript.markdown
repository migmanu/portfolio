---
title: Hoisting in JavaScript
layout: post
date: '2022-06-21 18:05:19 +0200'
categories: jekyll update
---

# Hoisting

To understand #hoisting it's important to know that not all code is interpreted exactly at the same time nor from top to bottom. In fact **all declarations, both variables and functions, are processed first** by the compiler, before any code is executed.

## What does hoisting mean?

A metaphorical way of understanding how the compiler interprets code is that function and variables declarations are "moved" to the top of the code. This is called hoisting (to raise or haul up).

Hoisting emphasizes that it is in fact "the order in which code is executed that matters, not the order in which it is written in the source file." [MDN](the order in which code is executed that matters, not the order in which it is written in the source file.)

## What about scope?

[[Scope]]
**Hoisting is per-scope**. This means that hoisted functions and variables are "moved" to the top of their respective scope:


```javascript
function foo() {
    // myVariable has been "moved" here
    var myVariable;
}

```

**But there are some differences on how variable and function hoisting work.**

## Variable hoisting

But it is most **IMPORTANT** to distinguish between a declaration and an assignment (initialization). In JavaScript `var a = 2;`  is actually two statements:
    1. `var a;`
    2. `a = 2;`

**Variable declarations are hoisted, variables assignments (initialization) are not.**

That is why the following is correct:

```javascript
a = 2; // assignment (initialization)

var a; // declaration

console.log( a ) // prints 2

```

But this would result in `undefined`:

```javascript
console.log( a ); // undefined

var a = 2;

```

The above example would be the same as:

```javascript
 var a;
 
 console.log( a );
 
 a = 2;
 
```

But hoisting doesn't behave exactly the same for [[Const, Let and Var]] declared variables.

### `var` hoisting

The default initialization of `var` us `undefined`. Here are some examples from [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting):

```javascript
console.log(num); // Returns 'undefined' from hoisted var declaration (not 6)
var num; // Declaration
num = 6; // Initialization
console.log(num); // Returns 6 after the line with initialization is executed.
```

The same would happen if the variable declaration and initialization were made in the same line (`var num = 6;`) as only the declaration gets hoisted.

But, what happens if we don't use any declaration at all?

### un-declared variable hoisting

Variables that are only initialized but not declared do not get hoisted. That is why trying to access them before they are initialized results in a ReferenceError.
MND example:

```javascript
console.log(num); // Throws ReferenceError exception - the interpreter doesn't know about `num`.
num = 6; // Initialization
```

### `let` and `const` hoisting

`let` and `const` variables are also hoisted, but whereas `var` variables are initialized with a default value (`undefined`), these are not.

This means that calling them before initialization results in a ReferenceError exception.
MDN example:

```javascript
console.log(num); // Throws ReferenceError exception as the variable value is uninitialized
let num = 6; // Initialization
```

## Function hoisting

**Functions declarations are hoisted, function expressions are not**.

```javascript
foo(); // TypeError
bar(); //ReferenceError, bar is not available out of its attached scope

var foo = function bar() {
        //...
};

```

In the previous case, the variable identifier `foo` is hoisted inside its attached scope (global). But it's yet been assigned no value when called. That is why the program throws a `TypeError` and not a `ReferenceError`, as it does when `bar` is called.

### Functions are hoisted before variables

Functions are hoisted first. This can be seen when "duplicate" declarations are used:

{% highlight javascript %}
foo(); // 1

var foo;

function foo() {
    console.log(1);
};

foo = function() {
    console.log(2);
};

{% endhighlight %}

`var foo;` is ignored in the previous example as it is hoisted after `function foo()`. Subsequent function declarations do override previous ones:

```javascript
foo(); // 2

function foo() {
    console.log(1);
};

function foo() {
    console.log(2);
};

```

## Sources

- [https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/scope%20%26%20closures/ch4.md]
- [https://developer.mozilla.org/en-US/docs/Glossary/Hoisting]
- [https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/]

#
