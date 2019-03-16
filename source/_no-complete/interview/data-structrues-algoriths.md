title: common data structrues
date: 2018-02-01 6:52:35
categories: algoriths
tags: js
---

<div><!--more--></div>


## common sort algorithm

> bubble sort

bubble sort is a simple sort algorithm,it's complex rate is O(n2)

```javascript
	//the bubble sort's mian thinking are compare every parameter and the next parameter,if the next parameter is bigger then this previous parameter,they will change they position。

	function bubbleSort(arr){
		// arr are a formal parameter，when actual parameter be used ,formal parameter will be replaceS
		for(let i=0;i<arr.length;i++){
			for(let j=0;j<arr.length-i;j++){
				if(arr[j]>=arr[j+1]){
					let temp = arr[j+1];
					arr[j+1] = arr[j];
					arr[j] = temp;
				}
			}
		}
	}
	
```

> quick sort

quick sort according to it's name,we can know this sort is most quick sort algorithms,I will show to you this function


```javascript 
	// the quick sort will use the recurrence algorithms to comple this 

	function quickSort(arr){
		// if the arr's length is small than one ,this function will be return.
		if(arr.length<=1) return arr;
		
		// find the pivot position
		let pivot = Math.floor(arr.length/2);

		// define two array
		let left=[],right=[];

		
	}
	
```









