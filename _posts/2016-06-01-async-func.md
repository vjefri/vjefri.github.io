---
layout: post
title:  "Create Async Function"
date:   2016-06-01 21:28:15 +0700
categories: [Problems]
---

```js

// create asyncMap func with array and callback as args
  // create empty results list
  // create counter set to 0
  
  // for func in array of functions
    // invoke func with anonymous function as arg which takes item 
    // asign item to results sub index
    // increment counter by 1
    // if last func in array
      // invoke callback with results as arg
      
function asyncMap(array, callback) {
  var results = []
  var counter = 0
  
  array.forEach(function(func, index) {
    func(function(item) { // tricky part is this anon func
      results[index] = item
      counter++
      if (counter === array.length) {
        callback(results)
      }
    })
  })
}

// Solution #2
function asyncMap(array, callback) {
  var counter = 0;

  array.reduce((result, func, index) => {
    func((item) => {
      result[index] = item;
      if (++counter === array.length) {
        return callback(result);
      }
    });
    return result;
  }, [])
}

asyncMap([
    function(cb) {
      setTimeout(function() {
        cb('one');
      }, 200);
    },
    function(cb) {
      setTimeout(function() {
        cb('two');
      }, 100);
    }
  ],
  function(results) {
    // the results array will equal ['one','two'] even though
    // the second function had a shorter timeout.
    console.log(results); // ['one', 'two']
  });

  ```
