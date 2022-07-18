---
layout: post
title:  "JavaScript functions"
toc: true
date:   2022-06-21 18:05:19 +0200
categories: jekyll update
---


# JavaScript Functions
A function is a set of statements that perform a task. It takes some input and return some output with a clear relation between them.

They are a way of performing similar actions repeatedly in the script, without the need to code them again and again.

In order to be used, functions must be declared inside the [[Scope]] they will be called from.

Functions are the *"building blocks"* of a program. Some of the most widely used ones are built-in-functions that JavaScript already comes with. Such as `promtp()` or `console`.

Of course, we can create our own functions. This is most commonly done with [[#Function Declaration]] , [[#Function Expression]], [[#Arrow Functions]] and the [[#Function Constructor]].

```JavaScript

function myFunction (arg1, arg2) {
	...body... // this function has Global Scope and takes two arguments
}

```

## Function Declaration
Function declarations (also called **function declaration** or **function statement**) in JavaScript can be done with the keyword `function`.

### Function Declaration Requirements & Example
 - the `function` keyword
 - a name
 - followed by the comma-separated parameters inside parentheses (optional)
 - and closed with the function's code between curly brackets (optional)

Functions are called using their name followed by parentheses. If any parameters are expected, they should be included inside those parentheses separated by commas. Data passed to a function this way is called *argument*.

```JavaScript

function firstFunction (param1) {
	console.log("first function has been declared!")
};

function secondFunction (param1, param2) {
	console.log("second function has been declared!")
};

function thirdFunction () {
	console.log("third function has been declared!")
};

firstFunction(arg1);

secondFunction(arg1, arg2);

thirdFunction();

```

## Function Expression
A function expression is when a function is declared inside an expression.

### Function Expression Requirements & Example
- variable declaration keyword (optional): [[Const, Let and Var]]. The keyword choice may affect [[Scope]]
- variable name
- the `function` keyword
- function name (optional): If omitted the function is anonymous. The name is only local to the function body
- parameters (optional)
- function body (optional)

````JavaScript

const variable1 = function firstFunction (arg1, arg2) {
	...body... // named function expression
};

(function () {...body...})(); // anonymous function

var variable2 = function () {
	...body... // anonymous function with no passed argumets
};

````

### Function Expression Hoisting
As seen in [[Hoisting#Variable hoisting|Variable Hoisting]], variable declarations are hoisted, variables expressions are not . 

This is why the following works:
````JavaScript

function calculator () {
  let firstResult = add()
  function add () { // function declaration gets hoisted to top of its scope
    console.log(2 + 2)
  }

  const multiply = function () { //anonymus function expression doesn't get hoisted
    console.log(3 * 3)
  }
  let secondResult = multiply()

  return (firstResult, secondResult)
}

calculator() // prints 4 and 9

````

But the following doesn't:
```JavaScript

function calculator () {
  let secondResult = multiply()

  const multiply = function () {
    console.log(3 * 3)
  }

  return secondResult
}

calculator() // ReferenceError: Cannot access 'multiply' before initialization

```

### Named functions expressions
Anonymous functions expressions are *implicitly* named with the name of the variable they are declared inside. But it is possible to *explicitly* name function expressions.

Named functions are used to refer to a function inside its own body. Therefore, their name is only accessible inside their body scope.

````JavaScript

const foo = function () { // implicitly named 'foo'
	console.log("Dog")
}

foo() // prints 'Dog'
console.log(typeof foo) // function
console.log(foo.name) // myVariable

const bar = function myFunction () {
	console.log(typeof bar) // function
	console.log(typeof myFunction) // function
	
}

myFunction() // ReferenceError: myFunction is not defined
bar() // no errors

console.log(typeof foo) // undefined
console.log(typeof bar) // function
console.log(bar.name) //myFunction

````

#### named function expressions advantages
- Not many
- They provide for cleaner more readable code
- Easier to trace errors
- (BEFORE ES6 ) Allow for recursive calls using that name (though with ES6 this can also be achieved using the implicit variable name in anonymous functions expressions)

````JavaScript

const bar = function recursion (n) {
  console.log(n)
  nextN = n - 1
  if (nextN > 0) {
    recursion(nextN)
  }
}
bar(3) // 3 2 1 

const bar = function recursion (n) {
  console.log(n)
  nextN = n - 1
  if (nextN > 0) {
    bar(nextN)
  }
}
bar(3) // aldo 3 2 1


````


## Arrow Function Expressions
*Arrow functions* are a short alternative to traditional *function expressions*, thought they do have some limitations. 

They are called arrow functions for the `=>` marker that's used to create them.

```JavaScript
let arrowFunction = (arg1, arg2, ..., argN) => expression
```

It is important to note that arrow functions are *always* expressions and *always* anonymous. They cannot be declared (in the sense function declaration works) and they cannot be named.

Arrow functions were introduced with ES6.

### Arrow Function Requirements & Examples
Arrow functions require the following elements:

- Parameters (optional): 
	- If only one argument is passed then no parenthesis are needed:
	  
	  ```JavaScript
	  let singleArgument = arg1 => expression
	  ```
	  
	- If no arguments are passed then empty parenthesis are needed:
	  
	  ```JavaScript
	  let noArguments = () => expression
	  ```

- The `=>` marker
- The function's body (optional):
	- If there is only one expression in can be placed in the same line with no curly brackets needed. Note than in this case the function has an implied `return` statement
	  ```JavaScript
	  let arrowFunction = (arg1, arg2) => a * b;
	  ```
	  
	- If there is more than one expression it needs to be encased by curly brackets. In this case the `return` statement must be explicitize like in traditional functions
	  
	  ```JavaScript
	  let arrowFunction (arg1, arg2) => {
	      console.log("function init")
	      return (arg1 / arg2)
	  }
	  ```


### Arrow Function Benefits and Limitations
Arrow functions are a bit of a disputed topic. Some people love them, some not so much. Because they have some major limitations, they should't be used indiscriminately. On the other hand, they do make a lot of things easier and even prettier. 

So let's take a look on some of the advantages and disadvantages of arrow functions.

#### Benefits
- They are a more concise and readable way of writing functions. One line arrow functions especially. The `function`,  `return` and the `{...}` can all be omitted.
- The `this` inside them is automatically bounded to the function's surrounding scope. See next subsection for more info.
- The `=>` marker is a lot easier to write than the verbose `function` keyword. Of course this is only an advantage as long as you don't use keybindings to help you code.
- They look pretty: This may sound superficial, irrelevant or even repetitive. And it's, of course, a personal preference. But I do want to emphasize how elegant arrow functions can look. To me, they are just a pleasure to write and read .And I can still remember how amazed I was the first time I came by them.

#### Limitations
- As pointed out in [You Don't Know JS](https://www.bookstack.cn/read/ES6Beyond/spilt.7.ch2.md), arrow functions may become harder to read than normal functions. Wait, isn't that the opposite of what I mentioned in their benefits? Kinda. You see, as an arrow function grows in statements, it gets harder and harder to identify the `=>` marker at a quick glance. This does not happen with the `function` keyword. Of course, this is based on the author's personal experience and may vary depending the tools used to write code.
- Again, the `this` inside them is bound to the surrounding scope. They don't have their own `this`. More about it in the next subsection.

### Arrow Functions and `this`
Arrow functions have *lexical scoping*, which means they don't bind their own `this` but rather inherit it from their parent scope. As seen in the [[#Arrow Function benefits and limitations | Benefits and Limitations]] , though they can be very helpful, they are not recommended for every escenario.

Explaining *this* is out of the scope of this note. For quick reference read [MOD's article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) and watch this video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/2mRN8FyjnE4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


