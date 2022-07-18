---
layout: post
title:  "Scope in JavaScript"
toc: true
date:   2022-06-21 18:05:19 +0200
categories: jekyll update
---

# Scope

Before ES6 there was only **Global scope** and **Function scope**. ES6 introduced **Block scope**.

Basically, Scope is a set of rules that determine how the program organizes variables, where they are stored and how are they fetched.

## Global Scope

Global variables are declared outside functions and are accessible to all scripts and functions.
They can be declared with `var`, `const`or `let`
[[Const, Let and Var]]. But they can also be initialized without being declared.

```javascript
var globalVariable = "global variable" // Global scope
const anotherGlobal = "this time with const"  // Global scope
let yetAnother = "and another"  // Global scope

function myFunction() {
        // code here can access all of the above declared variables
    }

```

If you assign a value to an undeclared variable it becomes global when the assignment is executed:

```javascript
myFunction();

// code here can accessed globalVariable

function myFunction() {
        globalVariable = "no declaration, no var const or let used"
    }

```

## Function scope

Variables defined within a function can only be accessed within that same function. This is the same for `const`, `let` or `var`.

```javascript
// Code here cannot access any of the variables declared in myFunction

function myFunction() {
        var varVariable = "declared with var";
        const constVariable = "declared with const";
        let letVariable = "declared with let";
    }

```

## Block scope

[[Block]]
Block scope was provided in ES6 with the `let` and `const` keywords.

Variables declared inside a { } block cannot be accessed outside of the block.

Variables declared with the `var` keyword cannot have block scope.

```javascript
{
    const first = 1;
    let second = 2;
    var third = 3;
}

var sumOf = first + second; // ERROR neither one nor two can be accessed outside the block 
var sumOf = third // three can be accessed

```
