# OOPS in JavaScript

## Objects
1. Creating Objects:

```
// Using literal notation:

const myObject = {};

// Using the Object() constructor function:

const myObject = new Object();

```
2. Adding Properties

Properties can be added to objects simply by specifying the property name, then giving it a value. Let's start off with a blank object, then add two properties:
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

As object are pass by reference if two a objectB is copy of objectA then
objectA===objectB // true
else
objectA === ObjectC //false






- We are using object literal for that
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
```
2. Factories and Constructors
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

3. Primitive and Reference Types

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

4. Working with properties

circle.location = {x:1}
circle[location] ={x:1}

use case:1. when we want dunamic access then

const propertyname = "location";
circle[propertyname]

case 2: when there is special character in the property name
const propertyname = "center-location";
circle[propertyname]

to iterate we have for-in loop

5. Private Properties
6. Getters/ Setters
7. Prototype

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

⚠️ Dot Notation Limitations ⚠️

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