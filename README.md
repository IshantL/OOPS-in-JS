# OOPS in JavaScript

## Objects
1. Creating Objects:
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