# OOPS in JavaScript

## Objects

1. Creating Objects:

```
// Using literal notation:
const myObject = {};

// Using the Object() constructor function:
const myObject = new Object();

//using object literal 

const circle = {
    radius:1,
    location:{
        x:1,
        y:1
    },
    draw:function(){
        console.log('draw');
    }
}
circle.draw();
```
2. Adding Properties

- Properties can be added to objects simply by specifying the property name, then giving it a value. - Let's start off with a blank object, then add two properties:
```
const printer = {};
printer.on = true;
printer.mode = 'black and white';
```
The above example uses dot notation to add properties, but keep in mind that square bracket notation works just as well:
```
printer['remainingSheets'] = 168;
```
Likewise, we can add a method to the printer object in a similar manner. This time, the value of the property is an anonymous (i.e., unnamed) function:
```
printer.print = function () {
  console.log('The printer is printing!');
};
```
3. Removing Properties
Recall that since objects are mutable, not only can we modify existing properties (or even add new ones) -- we can also delete properties from objects.

Say that the printer object above actually doesn't have any modes (i.e., 'black and white', 'color', etc.). We can go ahead and remove that property from printer using the delete operator.
```
delete printer.mode;
```
Note that delete directly mutates the object at hand. If we try to access a deleted property, the JavaScript interpreter will no longer be able to find the mode property because the mode key (along with its value, true) have been deleted:
```
printer.mode;

// undefined
```
4. Passing Arguments

- Passing a Primitive
In JavaScript, a primitive (e.g., a string, number, boolean, etc.) is immutable. In other words, any changes made to an argument inside a function effectively creates a copy local to that function, and does not affect the primitive outside of that function. Check out the following example:
```
function changeToEight(n) {
  n = 8; // whatever n was, it is now 8... but only in this function!
}

let n = 7;

changeToEight(n);

console.log(n);
// 7

```
- Passing an Object
On the other hand, objects in JavaScript are mutable. If you pass an object into a function, Javascript passes a reference to that object. Let's see what happens if we pass an object into a function and then modify a property:
```
let originalObject = {
  favoriteColor: 'red'
};

function setToBlue(object) {
  object.favoriteColor = 'blue';
}

setToBlue(originalObject);

originalObject.favoriteColor;
// 'blue'
```
5. Comparing an Object with Another Object

As object are pass by reference if two objects e.g objectB is copy of objectA then
objectA===objectB // true
else
objectA === ObjectC //false


6. Functions vs. Methods

Now, say that we also have a developer object with a single property, name:
```
const developer = {
  name: 'Andrew'
};
```
If we want to add the sayHello() function into the developer object, we can add the same way as we add other new properties: by providing property name, then giving it a value. This time, the value of the property is a function!
```
developer.sayHello = function () {
  console.log('Hi there!');
};
```
To Invoke
```
developer.sayHello();
// 'Hi there!'

developer['sayHello']();
// 'Hi there!'
```
Passing Arguments Into Methods
If the method takes arguments, you can proceed the same way, too:
```
const developer = {
  name: 'Andrew',
  sayHello: function () {
    console.log('Hi there!');
  },
  favoriteLanguage: function (language) {
    console.log(`My favorite programming language is ${language}`);
  }
};

developer.favoriteLanguage('JavaScript');
// My favorite programming language is JavaScript'

```
💡 Call Methods by Property Name 💡
We've been using anonymous functions (i.e., functions without a name) for object methods. However, naming those functions is still valid JavaScript syntax. Consider the following object, greeter:
```
const greeter = {
  greet: function sayHello() {
    console.log('Hello!');
  }
};
```
Note that the greet property points to a function with a name: sayHello. Whether this function is named or not, greet is invoked the same way:
```
greeter.greet();

// 'Hello!'
```
Named functions are great for a smoother debugging experience, since those functions will have a useful name to display in stack traces. They're completely optional, however, and you'll often read code written by developers who prefer one way or the other.

Using this, methods can directly access the object that it is called on. Consider the following object, triangle:
```
const triangle = {
  type: 'scalene',
  identify: function () {
    console.log(`This is a ${this.type} triangle.`);
  }
};
```
Note that inside the identify() method, the value this is used. When you say this, what you're really saying is "this object" or "the object at hand." this is what gives the identify() method direct access to the triangle object's properties:
```
triangle.identify();

// 'This is a scalene triangle.'
```
When the identify() method is called, the value of this is set to the object it was called on: triangle. As a result, the identify() method can access and use triangle's type property, as seen in the above console.log() expression.

Note that this is a reserved word in JavaScript, and cannot be used as an identifier (e.g. variable names, function names, etc.).

- Exercise
```
/*
Create an object called `chameleon` with two properties:

1. `color`, whose value is initially set to 'green' or 'pink'
2. `changeColor`, a function which changes `chameleon`'s `color` to 'pink'
    if it is 'green', or to 'green' if it is 'pink'

*/
const chameleon ={
    color : 'green',
    changeColor: function(){
        this.color === 'green' ? this.color = 'pink': this.color ='pink';
    }
}
```

7. Factories and Constructors
- Suppose we want to create another Circle for that we need to duplicate the circle and if some method of circle have bug in it then we need to change all the methods.
```
const circle = {
    radius:1,
    location:{
        x:1,
        y:1
    },
    draw:function(){
        console.log('draw');
    }
}
circle.draw();

const circle = {
    radius:1,
    location:{
        x:1,
        y:1
    },
    draw:function(){
        console.log('draw');
    }
}
circle.draw();
```
So object literal syntax is not a good way to create and to duplicate if this object has atleast one method,  if an object have more than one method then we will say that object has behavior like a person that do different things.

if we delete the draw method and duplicate it then there is no probem to duplicate using object literal but for method the problem occurs.
```
const circle = {
    radius:1,
    location:{
        x:1,
        y:1
    }
}

const circle = {
    radius:1,
    location:{
        x:1,
        y:1
    }
}

circle.draw();
```
So the solution is to use factory or constructor function
```
//using factory function
function createCircle (radius){
return {
    radius,
     draw:function(){
        console.log('draw');
    }
};
}
const circle =  createCircle(10);
circle.draw();

//using constructor function
function createCircle (radius){
    this.radius =radius;
    this.draw:function(){
        console.log('draw');
    }
};
}
const circle =  new createCircle(10);
circle.draw();
//the new keyword hereit create an empty object then it will set 'this' to point to that object.
when new added -> 'this' refers to cirle object,
if new removes-> 'this' refers to windows object.

```
Every object has constructor property and 
object.constructor returns the function who create that object.

So even if we create a function then how why it have constructor property?
This is because internally JS will do like this:
```
const circle = new function createCircle ('radius',' this.radius =radius;
    this.draw:function(){
        console.log('draw');
    }
    ');
```
methods avialable in objects
.call()
e.g circle.call({},1)
This is for invocation here the first parameter is object which is referenced to 'this'.i,e the target of 'this'.
This is same as using new operator where new operator create the object and reference it to 'this'.

.apply() is same as .call() but the arguments are in array.

8. Primitive and Reference Types

Value type:

a. Number

b. String

c. Boolean

d. Symbol

e. undefined

f. null

Reference type:
a. Object

b. Function

c. Array

Primitives are copy by value, reference type are copied by reference.

8. Working with properties

circle.location = {x:1}
circle[location] ={x:1}

use case:1. when we want dunamic access then

const propertyname = "location";
circle[propertyname]

case 2: when there is special character in the property name
const propertyname = "center-location";
circle[propertyname]

to iterate we have for-in loop

Exercise:
```
/*
Create an object called `menu` that represents the following menu item:

Salted Caramel Ice Cream
2.95
butter, ice cream, salt, sugar

The object should contain the following properties:
* name
* price
* ingredients

Hint: Which data collection can hold all the listed ingredients in order?
*/

const menu = {
    name: "Salted Caramel Ice Cream",
    price:2.95,
    ingredients: ['butter', 'ice cream', 'salt', 'sugar']
}
```

9.⚠️ Dot Notation Limitations ⚠️

```
const bicycle = {
  color: 'blue',
  type: 'mountain bike',
  wheels: {
    diameter: 18,
    width: 8
  }
};

```
Note that while dot notation may be easier to read and write, it can't be used in every situation. For example, let's say there's a key in the above bicycle object that is a number. An expression like bicycle.1; will cause a error, while bicycle[1]; returns the intended value:

bicycle.1;

// Uncaught SyntaxError: Unexpected number

bicycle[1];

// (returns the value of the `1` property)
Another issue is when variables are assigned to property names. Let's say we declare myVariable, and assign it to the string 'color':

const myVariable = 'color';
bicycle[myVariable]; returns 'blue' because the variable myVariable gets substituted with its value (the string 'color') and bicycle['color']'s value is 'blue'. However, bicycle.myVariable; returns undefined:

bicycle[myVariable];

// 'blue'

bicycle.myVariable;

// undefined

It may seem odd, but recall that all property keys in a JavaScript object are strings, even if the quotation marks are omitted. With dot notation, the JavaScript interpreter looks for a key within bicycle whose value is 'myVariable'. Since there isn't such a key defined in the object, the expression returns undefined.

10.Things that Belong to Objects

this and Invocation
How the function is invoked determines the value of this inside the function. ← That sentence is really important, so read that two more times...we'll wait!

Because .lookAround() is invoked as a method, the value of this inside of .lookAround() is whatever is left of the dot at invocation. Since the invocation looks like:
```
chameleon.lookAround();
```
The chameleon object is left of the dot. Therefore, inside the .lookAround() method, this will refer to the chameleon object!

Now let's compare that with the whoThis() function. Since it is called as a regular function (i.e., not called as an method on an object), its invocation looks like:
```
whoThis();
```
Well, there is no dot. And there is no object left of the dot. So what is the value of this inside the whoThis() function? This is an interesting part of the JavaScript language.

When a regular function is invoked, the value of this is the global window object.

11. Globals and var, let, and const
Only declaring variables with the var keyword will add them to the window object. If you declare a variable outside of a function with either let or const, it will not be added as a property to the window object.

12.Functions are First-Class Functions
In JavaScript, functions are first-class functions. This means that you can do with a function just about anything that you can do with other elements, such as numbers, strings, objects, arrays, etc. JavaScript functions can:

Be stored in variables
Be returned from a function.
Be passed as arguments into another function.
Note that while we can, say, treat a function as an object, a key difference between a function and an object is that functions can be called (i.e., invoked with ()), while regular objects cannot.

```
/*

Declare a function named `higherOrderFunction` that takes no arguments,
and returns an anonymous function.

The returned function itself takes no arguments as well, and simply
returns the number 8.

*/

const higherOrderFunction = function(){
    return function(){
        return 8;
    }
}

```
13.Callback Functions

Recall that JavaScript functions are first-class functions. We can do with functions just about everything we can do with other values -- including passing them into other functions! A function that takes other functions as arguments (and/or returns a function, as we learned in the previous section) is known as a higher-order function. A function that is passed as an argument into another function is called a callback function.

We'll be focusing on callbacks in this section. Callback functions are great because they can delegate calling functions to other functions. They allow you to build your applications with composition, leading to cleaner and more efficient code.
```
function each(array, callback) {
  for (let i = 0; i < array.length; i++) {
    if (callback(array[i])) {
      console.log(array[i]);
    }
  }
}
function isPositive(n) {
  return n > 0;
};
The following is then executed:

each([-2, 7, 11, -4, -10], isPositive);
//What is outputted to the console?
//7, 11

```
Array Methods
Where have you probably seen callback functions used? In array methods! Functions are commonly passed into array methods and called on elements within an array (i.e., the array on which the method was called).


forEach()
Array's forEach() method takes in a callback function and invokes that function for each element in the array. In other words, forEach() allows you to iterate (i.e., loop) through an array, similar to using a for loop. Check out its signature:

```
array.forEach(function callback(currentValue, index, array) {
    // function code here
});

const logIfEven = function(n){
if(n % 2 === 0){
console.log(n);
}
}

[1, 5, 2, 4, 6, 3].forEach(logIfEven);
[1, 5, 2, 4, 6, 3].forEach( function(n){
  if(n % 2 === 0){
  console.log(n);
}
})
```

map()
Array's map() method is similar to forEach() in that it invokes a callback function for each element in an array. However, map() returns a new array based on what's returned from the callback function.

```
const names = ['David', 'Richard', 'Veronika'];

const nameLengths = names.map(function(name) {
  return name.length;
});

```
So nameLengths will be a new array: [5, 7, 8]. Again, it is important to understand that the map() method returns a new array; it does not modify the original array.

filter()
Array's filter() method is similar to the map() method:

It is called on an array
It takes a function as an argument
It returns a new array
The difference is that the function passed to filter() is used as a test, and only items in the array that pass the test are included in the new array.

```
/* Using filter()
 *
 * Using the musicData array and filter():
 *   - Return only album objects where the album's name is
 *     10 characters long, 25 characters long, or anywhere in between
 *   - Store the returned data in a new `results` variable
 *
 * Note:
 *   - Do not delete the musicData variable
 *   - Do not alter any of the musicData content
 */

const musicData = [
    { artist: 'Adele', name: '25', sales: 1731000 },
    { artist: 'Drake', name: 'Views', sales: 1608000 },
    { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
    { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
    { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
    { artist: 'Original Broadway Cast Recording', 
      name: 'Hamilton: An American Musical', sales: 820000 },
    { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
    { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
    { artist: 'Rihanna', name: 'Anti', sales: 603000 },
    { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
];

const results = musicData.filter(function(temp){
    return (temp.name.length === 10 || temp.name.length ===25 || temp.name.length > 10 && temp.name.length < 25 );
})

console.log(results);
```
14. Closure
```
function remember(number) {
    return function() {
        return number;
    }
}

const returnedFunction = remember(5);

console.log( returnedFunction() );
// 5
```
When the Javascript engine enters remember(), it creates a new execution scope that points back to the prior execution scope. This new scope includes a reference to the number parameter (an immutable Number with the value 5). When the engine reaches the inner function (a function expression), it attaches a link to the current execution scope.

This process of a function retaining access to its scope is called a closure. In this example, the inner function "closes over" number. A closure can capture any number of parameters and variables that it needs. MDN defines a closure as:

"the combination of a function and the lexical environment within which that function was declared."

This definition might not make a lot of sense if you don't know what the words "lexical environment" mean. The ES5 spec refers to a lexical environment as:

"the association of Identifiers to specific variables and functions based upon the lexical nesting structure of ECMAScript code."

In this case, the "lexical environment" refers the code as it was written in the JavaScript file. As such, a closure is:

The function itself, and
The code (but more importantly, the scope chain of) where the function is declared
When a function is declared, it locks onto the scope chain. You might think this is pretty straightforward since we just looked at that in the previous section. What's really interesting about a function, though, is that it will retain this scope chain -- even if it is invoked in a location other than where it was declared. This is all due to the closure!

15. IIFE

An immediately-invoked function expression (IIFE) is a function that is called immediately after it is defined. Utilizing an IIFE alongside closures allows for a private scope, which maintains privacy for variables defined within them. And since less variables are created, an IIFE will help to minimize pollution of the global environment, hindering the chances of variable name collisions.

16.OOPS
Object oriented javaScipt topics
