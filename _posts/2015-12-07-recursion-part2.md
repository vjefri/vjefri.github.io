# Recursion and Trees

Recursion is an approach of solving problems that takes advantage of the call stack. When we invoke a function, a new stack of the actively running function is created on the call stack. A call stack is a data structure used by the program to store information about the active subroutine. The call stack keep tracks of where a subroutine should return control once it finishes executing. 

![](http://i.stack.imgur.com/uiCRx.png)

Certain problems have solution structures that lend themselves to be solved recursively. One of these structures are trees. 

![](http://i.stack.imgur.com/jRFp8.png)

A tree can have many branches. Branches are similar in structure to other branches. A tree in the end is composed of branches that might have different leaves. But at the end of the day the branches are the same.

Lets say this is a branch: 

{% highlight javascript %}
{
    right: null,
    left: null
}

// We then create another branch within the right property. 
// Another branch meaning another object
{
  right: {
    right: null,
    left: null
  },
  left: null
}
{% endhighlight %}

When you repeat this process, sooner or later you will have a tree structure. Not all trees are the same. Some have more children then others. Others, allow a max of two children.
![](http://nathanielclaiborne.com/wp-content/uploads/2011/04/Inception-Top-Wallpaper-Sohan-Surag.jpg)

This can become a complicated structure to keep in your mind. In fact, unless you are a genius there is no way to hold the whole tree on your mind. The same reasoning goes with recursion. You might be able to solve 3 execution contexts deep, but more than that and you will start to lose track of the current values. Thus, with recursion it is important to solve two-three stack levels. 

## Base Cases
Base cases are one of the most important parts of a recursive solution. Base cases live within the function that you will invoke. They usually start with if statements, but not always. 

{% highlight javascript %}
var recursion = function() {
    if(basecase) {
    return;
    }
    if(basecase) {
    return;
    } else {
        recursion();
    }
};
{% endhighlight %}
Base cases serve to end the running function. But remember that in a recursive solution, there may be many functions waiting to be returned. Thus, the base case has to work for all functions on the stack. If it doesn't work for all, then your function will never return, until it overflows the stack. All functions must return for recursion to work. 

## Techniques
**Use a for loop to traverse the tree from left to right. **

{% highlight javascript %}
var recursion = function() {
    if(basecase) {
    return;
    }
    if(basecase) {
    return;
    } else {
    for (var i = 0; i < children.length; i++) {
        recursion();
        }
    }
};
{% endhighlight %}
That will traverse down the tree, until it returns and we are back in the loop. Remember that each recusive call has its own loop. Use this technique if you want to move across the children at each level on the tree. 
![](https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcRrCJvw4eFxX9hq208r9owmZR70na-EoQGv9YGmTX2qNOuT6_2u)

**Keeping track of values.**

{% highlight javascript %}
var mainFunc = function() {
    var countTracker;
    var arrayTracker;
    var ObjTracker;
    
    // Closure Recursive Function
    var recursion = function() {
        if(basecase) {
        return;
        } else {
            recursion();
        }
    };
}
{% endhighlight %}
Because of the nature of recursion, anything within the recursive function will reset. It will reset to the way it was during the first invocation. Only the arguments that are passed in change at each level. A function within a function is a great way to keep track of values while having the benefits of recursion. The recursive function will be able to work on the variables outside its function at its deepest levels. 

![](https://s3-us-west-2.amazonaws.com/sfmomaopenspace/wp-content/uploads/2011/07/seashells2.jpg)

**After recursion has returned**

After the recursive function has returned, you can do more work. We may be going up the levels, but we can still do work while this happens. That is the purpose of placing lines of code after the recursive call.  

```
var mainFunc = function() {
    var varTracker;
    var arrayTracker;
    var ObjTracker;
    
    // Closure Recursive Function
    var recursion = function() {
        if(basecase) {
        return;
        } else {
            recursion();
            // There is work to be done!
            // I am working here. 
            return; // Bye!
        }
    };
}
```

Once that returns there is no coming back. Bye Bye!
