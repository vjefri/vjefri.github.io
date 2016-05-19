---
layout: post
title:  "Subclasses and Superclasses"
date:   2015-12-18 21:28:15 +0700
categories: [JavaScript]
---

## Inheritance and the prototype chain

First checkout [this](http://www.ryanatkinson.io/javascript-instantiation-patterns/) cool posting by Ryan Atkinson. For your convenience here is the awesome image he created. Please checkout his blog [here](http://www.ryanatkinson.io/javascript-instantiation-patterns/). 
![Ryan's image](http://imageshack.com/a/img911/5519/fxn2D3.png)

Here I go into much more detail of what is happening in pseudoclassical super and sub classes. Please read the comments and try it out in your console. 

```
var Planet = function(water, life) {
	// the following is done behind the scenes:
	// -------------------Start-------------------
	// this = Object.create(Planet.prototype)
	// -------------------End -----------------

	// this delegates failed lookups to its prototype
	// its prototype has the method rotationSpeed
	// console.log(this); => { prototype: {rotationSpeed: function(){this.speed++}}}
	// this is an Object, so we add properties to it

	// Suppose we instantiate the object as var x = new Planet(true, true)
	this.water = water; // {water: true, prototype: {rotationSpeed: function(){this.speed++}}}
	this.life = life; // {water: true, life: true, prototype: {rotationSpeed: function(){this.speed++}}}
	this.speed = 0; // You can guess what this would be.

	// the following is done behind the scenes:
	// -------------------Start-------------------
	// return this; 
	// -------------------End-------------------

	// this is an Object, so we are returning {water: true, life: true, prototype: {rotationSpeed: function(){this.speed++}}}
};

// We assign functions to Planet's prototype 
Planet.prototype.rotationSpeed = function() { 
	// use case: earth.rotationSpeed(100);
	// this refers to the Object that invoked rotationSpeed function, which is earth in this example
	// so `this.speed` is the same as `earth.speed`. 
	// so we increment the property speed within earth
	this.speed++;
};

// Since Mars is also a planet, it can reuse the template we made for Planet

var Mars = function(water, life) {
	// ------------Behind Scenes Start-------------------
	// this = Object.create(Mars.prototype);
	// -------------------End-------------------
	// The problem: How do we reuse the properties and functions we created within Planet?
	// Reuse Properties: // 
	// Remember(VERY IMPORTANT): this is an Object therefore it is passed by Reference. 
	// Therefore even though we pass this as an argument into the Planet function
	// inside the Planet function it will still modify the this within the Mars function
	// a new copy of this is not created within the Planet function
	// that is the reason why we don't have to save the return value to a variable
	Planet.call(this, water, life); // here this refers to the mars object which is {}
	// Note that this = Object.create(Planet.prototype) is only added when we use the keyword `new`
	// therefore that line will not run which lets this keep the Mars.prototype
	// you can also do:
	Planet.apply(this, arguments);

	// this is passed like any other argument.
	// within the Planet function, it sets the water and life to the mars object

	// ------------Behind Scenes Start-------------------
	// return this;
	// -------------------End-------------------};
};

////// Reuse Methods /////

// We overwrite the Mars prototype with a delegation to Planet.prototype
Mars.prototype = Object.create(Planet.prototype);
// Since we overweite the prototype, we also overwrite any properties within that
// And important one is the constructor, which points to the Mars function
// to put it back we just assign the function to that constructor. 
Mars.prototype.constructor = Mars;


// Reusing Prototypal Methods // 

```