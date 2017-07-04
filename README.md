# js-design-patterns
short summery of the book
## Introduction
### Object Oriented
Almost everything in JS in an object
### No Classes
To create an object you dont need a class to represent it. "Prefer object composition to class inhertiance" (GOF book)
### Prototypes
prototype is an object (not a class). Every function has a prototype property.
## Literals and Constructors
### Objects
Prefer creating object from literals.
To create from constructor:

```node
let o = new Object(); //object
let n = new Object(1); //number
let s = new Object('Hey'); //string
let b = new Object(true); //boolean
```
This behavior can lead to unexepcted results, use the literal notation instead.
### Custom Constructor Functions
It is possible to create object using your own constructor functions:
```node
let adam = new Person("Adam");
adam.say(); // "I am Adam"
```
The `new` pattern looks like creating an object in Java from a class called `Person`.
The syntax is similar, but Person is nothing more than a function.
it could be defined this way
```node
let Person = function(name){
    this.name = name;
    this.say = function(){ return "I am " + this.name}
}
```
When invoking a function using with `new` the following happens (more or less...):
```node
let Person = function (name){
   //let this = {}; new object is created (not really empty... Object.create(Person.prototype)
   this.name = '...';
   this.say = function(){};
   //return this;
  }
 ```
 now the `say` function is created with every invokation of the function. 
 A better way would be:
 ```node
 Person.prototype.say = function(){}
 ```
 This way we add the function to the prototype and unless some object defines a new `say` it will use this one.
 
 ### Array
 Array is an object. 
 ```node
 let a = [1,2,3] //array of length 3
 let a = new Array(1,2,3) //array of length 3
 let a = new Array(3) //array of length 3 (all members are undefined)
 
 (new Array(20)).join("*")) // ********************
 
 ##Primitive Wrappers
 number, string, boolean, null and undefined are primitive (not objects)
 
 They have object wrapper: Number(), String(), Boolean()
 
 ```node
 let n = 100;
 typeof n; //number
 
 let n = new Number(100);
 typeof n; //object
 ```
 The wrappers have some useful methods. Fortunatly primitive can be converted on the fly to objects/
 
 ```node
 let s = "hello";
 s.toUpperCase(); //works
 ```
 That's why you should always use the primitives as they read better.
 
 ### Error Objects
 Built-in error constructors (Error(),SyntaxError()...) have the following properties: 
 `name`: the name property of the constructor function created the object, `message`: the string passed to the constructor when creating the object.
 
 and might have more stuff depending on the host enviroment.
 
 `throw` works with any object.
 so it is possible to do for example:
 ```node
 try{
    throw{
        name: 'myError',
        message: 'oops',
        remedy: myFunc
        };
     } catch (e){
       console.log(e.message);
       e.remedy()
     }
```
Invoking error constructor with `new` is the same as without `new`
always pefer throwing literal object rather than objects created with Error()
 
