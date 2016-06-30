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

```js
/*
  Pseudoclassical Instantiation Pattern
*/

var Planet = function(water, life) {
  // this = Object.create(Planet.prototype)(NOTE: done behind the scenes in Pseudoclassical)

  // the keyword this delegates failed lookups to its prototype
  // its prototype has the method rotationSpeed
  // console.log(this); // => { prototype: {rotationSpeed: function(){this.speed++}}}
  // this is an Object, so we add properties to it

  this.water = water;
  // this is just an object so we can add properties to it
  // {water: true, prototype: {rotationSpeed: function(){this.speed++}}}
  this.life = life;
  this.speed = 0;

  // return this; (NOTE: done behind the scenes in Pseudoclassical)
  // which is {water: true, life: true, prototype: {rotationSpeed: function(){this.speed++}}}
};

// add a method called rotationSpeed to Planet
// we add it to the prototype because we are using Pseudoclassical pattern
Planet.prototype.rotationSpeed = function() {
  this.speed++;
};

// Let's reuse Planet's functionality

var Mars = function(water, life) {
  // NOTE: objects are passed by reference
  // the keyword this refers to the mars object
  Planet.call(this, water, life);

  // another way to write the same thing as above
  Planet.apply(this, arguments);
};

Mars.prototype = Object.create(Planet.prototype);
// overwrite the protoype property on Mars with Planet.prototype
// doing so will also remove the constructor that points to the Mars function
// we don't want that, so we have the constructor point to the Mars function again
Mars.prototype.constructor = Mars;
```