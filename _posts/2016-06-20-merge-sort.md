---
layout: post
title:  "Merge Sort"
date:   2016-06-20 21:28:15 +0700
categories: [problems]
---

![Array of 7 integer values](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Merge_sort_algorithm_diagram.svg/618px-Merge_sort_algorithm_diagram.svg.png)

Merge sort takes an array of numbers that are unsorted. Splits the array in half until we have 1 value. 

```js
/* Pseudocode */

// create mergeSort func accepts list as arg
  // if length of list is less than 2
    // return list
  // create variable that holds middle index of list
  // create left array by calling mergeSort and passing left side of array
  // create right array by calling mergeSort and passing right side of array

  // create variable results that holds sorted items

  // while left or right has items
    // if left is greater than right or left is undefined
      // push right item into results
    // else
      // push left item into results

  // return results
```

```js
function mergeSort(list) {
  if (list.length < 2) { // I am ready to be put in order
    return list
  }

  var result = []

  var middle = Math.floor(list.length / 2) // I am middle 
  var left = mergeSort(list.slice(0, middle)) // break me into pieces 
  var right = mergeSort(list.slice(middle)) // break me into pieces

  var x = 0;
  var y = 0;

  while (left[y] || right[x]) { // this is the last resort
    if (left[y] > right[x] || left[y] === undefined) {
      result.push(right[x++])
    } else {
      result.push(left[y++])
    }
  }

  return result
}
```

