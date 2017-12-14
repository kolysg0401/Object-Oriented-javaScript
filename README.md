OOjs
=================

Objects
----------
•	Creating objects

•	Function execution & this reference

•	Object follows blueprint of code

Object Basics
-----------------
It is the collection of multiple values
•	`Var myObj = {};` - empty object
•	In javascript whenever we want to create properties, can create no restrictions and no data type restrictions.
•	Bracket and dot notation access to the object properties. `myObj.foo or myObj[“foo”]`

Creating Objects
---------------------

`Var emp1 = {}; - empty object

function createEmpObject(firstname) {
        var myObj = {};
        myObj.firstname = firstname;
        return myObj;
}
Var emp1 = new createEmpObject(“antony”);`

JS Constructors
-------------------
Constructors is a function.

Calling in constructor mode.

`function createEmpObject(firstname) {
        //var this = {};
        this.firstname = firstname;
        //return this;
} // this defined and returned in hidden mode
Var emp2 = new createEmpObject(“antony”);`

Diff regular function & constructor function?
-------------------------------------------------
`Function Createemployee() {}`

Switching function types & calls
-------------------------------------
•	Calling constructor fn without new keyword
•	won’t return anything explicity
•	if nothing returned, js automatically return “undefined”.



Function Execution Types
-----------------------------
4 - ways to call functions

1.	`foo()`
2.	`obj.foo()`
3.	`new foo()`
4.	`foo.call({})`

#Method: 1 – Calling standalone function directly this reference: the global object
`function foo(){
     console.log(this) – o/p – window(global object)
}`
#Method: 2 – Calling functions as property of an object reference this reference: the object reference
`var obj = {};
obj.foo = function(){
	console.log(this) – o/p – object{ foo:obj.foo() }
};`
#Method: 3 – Calling standalone functions using ‘new’ keyword this reference: the newly created object. This => pointed to newly created object.
`new foo(); - creating empty object – o/p - object {}`

#Method: 4 -  using the call function
`function foo(){ this.abc = def; }
foo.call({})`

this arguments values
--------------------------
There are two default arguments to every function call:
 i.	arguments
 ii.	this – implicit variable

Working on object with this reference
-----------------------------------------
Function meant to be called in constructor mode.

`function Bicycle(gear){
	this.gear = gear;
}
Var bicycle1 = new Bicycle(4);`

	this reference in inner function diff from outer function.

Using the call function
----------------------------
`foo() === foo.call();`

Constructor
----------------





Prototypes
--------------
`foo.prototype === newobj.__proto__ (true)`



Property lookup with prototype
----------------------------------
`newObj.hello = “test from obj”;
newObj.__proto__.hello = “test from prototype”;`

	Add object property through prototype at runtime

Object behaviors using prototypes
-------------------------------------
`function foo(){}
var proto = foo.prototype;
proto.constructor === foo(); //true
        var b = new a.__proto__.constructor();`
        b returns an object
The double-underscores are referred to as “dunder” as in “Dunder Mifflin”. So, this property is called “dunder-proto”.

The Object Function
------------------------
window – global object and function are object


Prototype Object
--------------------
The automatically created prototype object is actually created using ‘new Object()’

`emp.test` – checks in the hierarchy
`emp.prop = “employee”`
`emp.__proto__.parentProp = “parent of employee”`
`emp.__proto__.__proto__ == Object.prototype` (global object- access to all object)
`Object.prototype.grandParentProp = “Grand Parent”;`
`emp.grandParentProp` [o/p – “Grand Parent”]


Inheritance in Javascript
------------------------------
`Mgr.__proto__.__proto__ = Employee.prototype`



7 ways to create objects in JavaScript:
========================================
1. Object constructor
The simplest way to create an object is to use the Object constructor: view plainprint?
var person = new Object();  
person.name = "Diego";  
person.getName = function(){  
    return this.name;  
};

2. Literal notation
view plainprint?
var person = {  
    person.name : "Diego",  
    person.getName : function(){  
        return this.name;  
    }  
}

3. Factory function
The Factory function allows to encapsulate and re-use the logic for creating similar objects. It leverages any of the previous constructs for this. Either: view plainprint?
var newPerson=function(name){  
    var result = new Object();  
    result.name = name;  
    result.getName = function(){  
        return this.name;  
    };  
    return result;  
};  
var personOne = newPerson("Diego");  
var personTwo = newPerson("Gangelo");  
console.log(personOne.getName()); // prints Diego  
console.log(personTwo.getName()); // prints Gangelo
Or:
view plainprint?
var newPerson=function(name){  
    return {  
        person.name : name,  
        person.getName : function(){  
            return this.name;  
        };  
};  
var personOne = newPerson("Diego");  
var personTwo = newPerson("Gangelo");  
console.log(personOne.getName()); // prints Diego  
console.log(personTwo.getName()); // prints Gangelo  

4. Function Constructor
In Javascript it is possible to call any function with the new operator in front of it. Given a function F, for new F(): a new empty object X is created. X is set as context for F meaning throughout F this points to X. X is returned as result of F view plainprint?
function Person(name){  
        this.name = name;  
        this.getName = function(){  
            return this.name;  
        };  
};  
var personOne = new Person("Diego");  
console.log(personOne.getName()); // prints Diego  
console.log(personOne instanceOf Person); // prints true  
console.log(personOne.constructor === Person); // prints true  
console.log(personOne instanceOf Object); // prints true  

5. Prototype
Functions are very special in Javascript. They are objects, they can create other objects and they automatically get a field called prototype. A prototype is a plain object with a single field, called constructor, pointing to the function itself. What makes it special is that every object created through a function inherits the function's prototype. view plainprint?
function Person(){};  
Person.prototype.name = "Diego";  
var personOne = new Person();  
var personTwo = new Person();  
console.log(personOne.constructor == Person); // prints true  
console.log(personOne.name); // prints Diego  
console.log(personTwo.constructor == Person); // prints true  
console.log(personTwo.name); // prints Diego  

6. Function/Prototype combination
The function/prototype combination, as you would imagine, takes advantage of both approaches :) view plainprint?
function Person(name){  
        this.name = name;  
};  
Person.prototype.getName = function(){  
            return this.name;  
        };  
var personOne = new Person("Diego");  
var personTwo = new Person("Filippo");  
console.log(personOne.getName()); // prints Diego  
console.log(personTwo.getName()); // prints Filippo  
console.log(personOne.getName === personTwo.getName) //prints true

7. Singleton
Sometimes, you may want to make sure that only a single instance of a certain class exists. To get a Singleton in Javascript is as simple as defining and invoking the constructor at the same time: view plainprint?
var singleton = new function(){  
    this.name = "ApplicationName";  
};  
