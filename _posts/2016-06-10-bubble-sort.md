---
layout: post
title:  "Bubble Sort"
date:   2016-06-10 21:28:15 +0700
categories: [problems]
---

```js
function bubbleSort(array) {
  //create a flag is values are swapped start with false
  var flag = false
  //create num1 index = 0
  var index = 0
  var counter = 0;

  while(true) {
    if (index === array.length - 1 && flag === false) {
      return array
    }

    if (index === array.length - 1 && flag === true) {
      index = 0
      flag = false
    }

    if (array[index] > array[index + 1]) {
      var temp = array[index]
      array[index] = array[index + 1]
      array[index + 1] = temp
      flag = true
    }

    index += 1
  }
}

// Solution #2 

function bubbleSort(arr){
   var len = arr.length;
   for (var i = len-1; i>=0; i--){
     for(var j = 1; j<=i; j++){
       if(arr[j-1]>arr[j]){
           var temp = arr[j-1];
           arr[j-1] = arr[j];
           arr[j] = temp;
        }
     }
   }
   return arr;
}
```