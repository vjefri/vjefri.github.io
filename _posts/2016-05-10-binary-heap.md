---
layout: post
title:  "Binary Heap"
date:   2016-05-10 21:28:15 +0700
categories: [problems]
---
```js
function searchArray(array, target, low, high) {
  low = low || 0
  high = high || array.length - 1
  var mid = Math.floor((low + high) / 2)

  if (low > high) { // target is not in array
    return -1
  }

  if (array[mid] === target) { // if match found
    return mid
  }

  if (array[low] <= array[mid]) { // left side is sorted
    if (array[low] <= target && array[mid] >= target) { // target in left half
      return searchArray(array, target, low, mid - 1) // search left
    } else {
      return searchArray(array, target, mid + 1, high) // search right 
    }
  } else { // right half is sorted
    if (array[mid] <= target && array[high] >= target) { // target in right half
      return searchArray(array, target, mid + 1, high) // search right
    } else {
      return searchArray(array, target, low, mid - 1) // search left
    }
  }
}

// Solution # 2

function searchArray(array, target) {
  var l = 0;
  var h = array.length - 1;

  while (l <= h) { // low is smaller or equal to high index
    var m = (l + h) / 2; // get middle index

    if (array[m] === target) { // if curr middle value equals target
      return m
    }
    if (array[m] >= array[l]) { // mid value is greater or equal to low value
     
      if (array[l] <= target && target < array[m]) { // target is between low and mid val
        h = m - 1; // decrease high index by 1
      } else {
        l = m + 1; // increase low index by 1
      }
    } else { // mid value is smaller than low value
      if (array[m] < target && target <= array[h]) { // target is between mid and high val
        l = m + 1; // increase low index by 1
      } else {
        h = m - 1; // decrease low index by 1
      }
    }
  }
  return -1; // if no match found, return -1
}
```