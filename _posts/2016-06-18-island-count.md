---
layout: post
title:  "Island Count"
date:   2016-06-18 21:28:15 +0700
categories: [problems]
---

```js
function islandCount(mapStr) {
  var matrix = mapStr.split('\n').map(r => r.split(''))
  var islandCounter = 0

  matrix.forEach((row, rowIndex) => { 
    row.forEach((value, colIndex) => { 	
      if(value === '0') {
      	islandCounter++
      	markIsland(matrix, rowIndex, colIndex)
      }
    });
  });

  return islandCounter
}

const markIsland = (matrix, row, col) => {
	if (matrix[row] && matrix[row][col] === '0') {
		matrix[row][col] = '.'
		markIsland(matrix, row + 1, col)
		markIsland(matrix, row - 1, col)
		markIsland(matrix, row, col + 1)
		markIsland(matrix, row, col - 1)
	}
}

// Psuedo Code //
// Output: number of islands counted
// Input: string of letters, 1 represent water and 0 represent land
// Complex: any
// Edge: account for undefined values in the matrix

// Notes:
  // an island is defined as 1's that are surrounded by 0's

// create markIsland that accepts matrix, column, and row
  // if matrix row exists and matrix value is 0
    // change matrix value to 1
    // invoke markIsland to search left
    // invoke markIsland to search right
    // invoke markIsland to search down
    // invoke markIsland to search up

// create countIsland func that accepts map string as arg
  // convert string to matrix of numbers
  // create and set island counter to 0
  
  // for row and rowIndex in matrix
    // for val and columnIndex in row
      // if value is 0
        // increment island count by 1
        // invoke markIsland with map, columnIndex, and rowIndex as args
        
  // return island count
  
```