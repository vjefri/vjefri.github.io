# Keeping it DRY

Today I got to explore and think about how to keep code dry. 

![](http://dingo.care2.com/pictures/greenliving/1326/1325643.large.jpg)

The way you keep things DRY is by using functions. Functions are the only way to abstract functionality that can be used in other parts of your application. The power of functions is that they can be invoked any place that has access to that function. 

There are many ways to structure a program. I could never do justice to all the JavaScript patterns. Thus, here is a great deal of excellent resources. 

* 
http://addyosmani.com/resources/essentialjsdesignpatterns/book/
* 
http://chimera.labs.oreilly.com/books/1234000000262/index.html
* 
http://www.dofactory.com/javascript/design-patterns

What I will talk about is how we can use functions to do what its name says and nothing else. 

```
// Lets say we have this function
function getApple() {

}
```
What does that function do? No I am not trying to insult your intelligence. But I am highlighting an important issue. How much functionality should we include within that function. Well, as the developer it is up to us to decide how much is enough. And an important thing to keep in mind is that if it does more than the name of the function we need to remove code. 

I understand that you will have code that is not being repeated within the function. However, as your application grows you will forget what `getApple()` does. It might just get an apple. Or it might get an apple, color the apple red and eat the apple. If we don't stick to that functions purpose we will complicate our code and our lives. 

#### I am not just a function, I am a utility
You will notice that some functions can be abstracted to do a variety of tasks. They can work on different types of data, or ever within other functions. You might know them as higher order functions. And I have to say that these functions are special because you might use them more than once. In fact, you might use them a lot. So much that there are libraries that do just that. Here are a few. 
* 
http://underscorejs.org/
* 
http://ramdajs.com/
* 
https://lodash.com/

These functions are in a class of their own because they might not be specific to a task. If you want to build a calculator program you will have specific function as well as general ones. There are functions that you can make more general, but not always.

The most important lesson is to always be thinking about how to refactor your code to make it more readable. But at the same time, do not refactor to the extent that it is unreadable. It is important to keep a good balance. 

![](http://www.ben-morris.com/wp-content/library/refactoring-vs-rewriting.gif)




