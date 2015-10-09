#Object Oriented Programming with Cars!

##Summary

| Skills to practice: |
| :--- |
|  |
| summarize key features of the Object Oriented Programming paradigm |
| model real-world data and relationships with JavaScript objects |
| justify choices of which methods and attributes to include, and whether to put them on a constructor, a prototype, or a single object |

##Programming Paradigms

<!--
![XKCD goto](https://imgs.xkcd.com/comics/goto.png)
*Dev culture reference: 'goto considered harmful.' Google it LATER.*
-->

Before OOP, we'd been working with **procedural programming**, putting blocks of code in functions (aka procedures) that we call at various points in the code.

```
data <--> global or local variables

behaviors <--> procedures  (functions)

```


With **object oriented programming**, we organize data and behaviors in objects.  

```
data <--> attributes  ("class" or "instance" variables)

behaviors <--> methods (functions)

```

##OOP features

###Classes and Instances

JavaScript doesn't have classes (yet - they're being added in the next version very soon). We can instead think of "object types" or "kinds of objects" that are defined by the combination of (1) a constructor function (like `Array()`) and (2) the constructor function's prototype (`Array.prototype`).

Objects created with the `new` keyword are cloned "instances" of the "object type" of the constructor.

###Composition

Object types are built up or composed of other data types, including objects.

###Delegation

Basically, "delegating" tasks to another part of the program. In JS, think of **prototype chain** lookup.

###Inheritance

Basically, letting objects be "a kind of" other objects. The process by which, for example, we can easily create both `Employee` and `Student` object types starting from the features of a base `Person` object type. JavaScript does inheritance in an atypical way, so as a class we'll study it first with Ruby.


###Encapsulation

Encapsulation is an *overloaded* term - it can mean a few different things.  In the context of OOP, it most often refers to keeping attributes or methods "private," instead of "public" and exposed. JS doesn't have actual private object variables but can simulate them by using a scoping setup known as a **closure**.

Private variables always need *getter* and *setter* methods if they're going to be accessible from outside their scope.

```
function Person (name, realAge, feelsOld){
  this.name = name;
  this.feelsOld = feelsOld;

  var _realAge = realAge;  // this variable will be "private", not accessible
  // can also make "private" function variables if your design calls for it

  this.getAge = function(){
    if (this.feelsOld){
     return _realAge - 10
    } else {
     return _realAge;
    }
  }
}

var grandpa = new Person("Jim", 72, true);

console.log("real age: ", grandpa._realAge);  // undefined

console.log("'age': ",grandpa.getAge());  // 62 :D
```

![old man dressed as a teenager](https://38.media.tumblr.com/106e7e5598f02c6017fb6e146dea465f/tumblr_inline_nimszn3Xft1t98at1.gif)

##Constructor and Prototype Review

**Constructors**

* variables and functions are declared once for each instance
* functions have access to "private" variables declared within the constructor's scope
* when you update the constructor, previously created instances DON'T update
* data is "embedded" in each instance

**Prototypes**

* all instances share the same function and variable declarations
* when you update the prototype, previously created instances DO get the updates
* data is "referenced" from the prototype copy

**Instance variables and functions**

* adds variable or function directly to the instance
* overwrites constructor properties/methods by replacing them
* overwrites prototype properties/methods by being earlier on the lookup chain!

##Modeling with Constructors, Prototypes, Instances

| Place | How it Works | Attribute Example | Method Example |
| :-- | :--- | :--- | :--- |
| constructor | each instance gets its own copy at creation | used often, usually passed in (name), sometimes calculated | used rarely, can access "private" variables |
| prototype | all instances share a lookup copy | used less often, common features (numLegs on Dog), or shared data (numCreated) | used often, same behavior across instances |
| instance | only one copy, for this instance | changing properties (3-legged dog) or adding unique features | used rarely, for behaviors that only this instance has or for overwriting existing methods |

Remember, when possibly overwriting an existing prototype property or method (especially on built-in objects' prototypes), use `||`:

`Array.prototype.sort = Array.prototype.sort || mySort;`

##Challenges - Modeling Cars for a Dealership

For each challenge that asks you to add a variable to the Car object type, write a comment that explains why you chose to put it on the constructor, prototype, or individual car instance.

1. List important attributes and methods for a Car object type.

1. Create a constructor for the Car object type.

1. Create a "public" (normal) `location` attribute for the Car object type.  Should this be on the constructor or the prototype?

1. Create a `drive` method for the Car object that takes in a new location and changes the car's location to that place. Should this be on the constructor or the prototype?

1. Create a `numWheels` variable that says how many wheels cars should have. Should this be on the constructor or the prototype?

1. Almost all of your dealership's cars are black. Create a `color` variable that stores the color of a car. Give it a default value of `"black"`. Should this be on the constructor or the prototype?

1. Create an instance of a car, and change its `color`.

1. Create a "private" `_priceMarkup` variable for the Car object type that stores the markup above a car's actual price (don't want customers to see this!). For example, `_priceMarkup = 0.5` would mean the final price of the car is 1.5 times its actual price. Should this be on the constructor or the prototype?

1. Create a getter method and a setter for the `_priceMarkup` variable.  Should these methods be on the constructor or the prototype?

1. Create a `getFinalPrice` method that returns the calculated cost of the car (based on the `price` and `_priceMarkup`). Should this be on the constructor or the prototype?

1. Create a `carCount` variable that counts how many cars the dealership has entered into inventory.  Should this be on the constructor or the prototype?

1. Stretch: Use `carCount` to assign an `inventoryID` to each car when it's created. A car's `inventoryID` should be unique to that car. Should this be on the constructor or the prototype?

