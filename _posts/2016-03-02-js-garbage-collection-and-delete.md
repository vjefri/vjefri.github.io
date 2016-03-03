# JS Garbage Collection and Delete

What is garbage collection and why do we care?
Garbage collection is a machine running inside the browser that cleans up anything that is not used. JavaScript along with other interpreted languages frees you from doing this yourself like you have to in the C language. Depending on the browser and the number of objects that are in use, this can take a small or large amount of time in ms. Obviously if it is a small program, it is not the best use of developer time to be looking for small memory leaks. There are other bottle necks that should be addressed like the DOM. However, it is important to understand how garbage collection works in JavaScript. 

####How does garbage collection work?
The V8 engine divides the heap into
* New-Space: A space where objects can be collected really quickly
* Old-Pointer Space: Objects which have pointers to other objects
* Old-data-space: Objects that have NO pointers
* Large-object-space: Large objects are never moved to garbage collector
* Code-space: Place of executable memory
* Cell-space: Contains objects that are all the same size

Memory is allocated to each space from the operating system. 

The GC has to determine data vs pointers. So the GC needs to follow the pointers to see if the objects are still alive. V8 takes the approach of reserving a bit at the end of each word to determine if it is a pointer or not. That is the tag that identifies that item as a pointer or not. That way it can be marked to be collected by GC. There is more complexity to GC, but we will leave it to the Chrome developers to figure that out. What we need to worry about is JavaScript. 

####How do you help the garbage collector?
* Stop referencing things you are not using. 
* Don't forget your *var* keyword

####How do you delete Objects?
In JavaScript you cannot use the *delete* keyword to remove objects. Objects are removed when you go out of scope. You can set the variable to `null`and let GC do its thing. 

####How do you delete properties of Objects?
```
var icecream = {flavor: 'vanilla'};
delete icecream.flavor
```
First flavor will be set to `undefined` and then marked to be garbage collected. Delete works to remove properties from objects. 

####But wait isn't everything in JavaScript an Object?

Yes, so the truth is that during property creation attributes are assigned within the object to have the right to **Delete** or **Can't Delete**. We all know about the infamous Global Object. Well, if properties are assigned there, they will be marked with **Can't Delete**. 

