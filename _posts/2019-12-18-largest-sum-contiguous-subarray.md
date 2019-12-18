---
title: Largest Sum Contiguous Subarray
layout: post
date: '2019-12-18 19:13:00'
image: "/assets/images/leetcode/leetcode.png"
headerImage: true
tag:
- leetcode
- competitive-programming
- codergals
- opensource
- tech-interviews
category: blog
author: AlbionaHoti
description: LeetCode Challenges
---

## Largest Sum Contiguous Subarray

<p>We are going to have a series of articles on LeetCode problems, everyday a post on a problem on LeetCode.

The first post will tacke an Array problem, which is:  </p> 

[Maximum SubArray](https://leetcode.com/problems/maximum-subarray/)

### Description

<p>Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.</p>

Example:
```

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

Follow up:

<p> If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

You will probably have experienced solving different competitive programming
tasks related to contigous subarrays.

Well, I myself when I first encountered the Maximum Sum contigous array challenge
in LeetCode, I had no idea that a Kadane's algorithm was existing first of all.

I searched on google "maxsubarray leetcode 100% javascript" and one of
the result links was: </p>

[largest-sum-contiguous-subarray](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

<p>Found out that there is an Algorithm and it's called Kadan's Algo, using
the dynamic programming paradigm to find the Maximum Sub Array.</p>

### Below you will find the short cut to the largest sum contiguous subarray solutions.

First, we will solve the problem using the paradigm Dynamic Programming and then we continue using the divide and conquer approach. 

The Algorithmic Paradigm is Dynamic Programming and the Time Complexity is O(n)

### Dynamic Programming

[Dynamic Programming](https://www.geeksforgeeks.org/dynamic-programming/) is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming. 

We will write a pseudo code, allowing ourselves to represent the implementation of the algorithm we are going to use, the Kadan's Algorithm. After the pseudo code, we will continue to add the real code of the algorithm which we will run it in the LeetCode Idle. 


```
Initialize:
  max_so_far = 0
  curr_max = 0

Loop for each element of the array
  (a) max_so_far = array[0]
  (b) curr_max = array[0]

  (c) for each element of the array
          curr_max = max of element and sum of curr_max and element
          max_so_far = max of max_so_far and curr_max
          
return max_so_far
```


<p>The solution with Dynamic Programming</p>

{% highlight js %} 

const maxSubArray = (nums) => {
  let max_so_far = nums[0];
  let curr_max = nums[0];

  for (let i = 1; i < nums.length; i++) {
    curr_max = Math.max(nums[i], curr_max + nums[i]);
    max_so_far = Math.max(max_so_far, curr_max);
  }
  return max_so_far;
};

{% endhighlight %}


<p>
Divide and Conquer Approach
</p>

{% highlight js %} 

var maxSubArray = function (nums) {

  // Return the results of the recursive function
  return findMaxSumInArr(nums);
    
  // Recursive function that will divide and conquer to find the maximum sum from a subarray of the array provided as a parameter
  function findMaxSumInArr(arr) {
    // BASE CASES: 

    // if there is only one arr item, then you can simply return that value
    if (arr.length === 1) {
      return arr[0];
    }
		
    /* 
      if there isn't an arr item, then return -Infinity 
      (we need a valid number for the calculations below. 
      Since JS can only store numbers > -Infinity, -Infinity will never be the max) */
    if (arr.length === 0) {
      return -Infinity;
    }
        
    // Declare zero-indexed length and midpoint
    let length = arr.length - 1;
    let mid = Math.floor(length / 2);
        
    // DIVIDE: Recursively find max sum in the left and right sub arrays
    let lMaxSumInSubArr = findMaxSumInArr(arr.slice(0, mid));
    let rMaxSumInSubArr = findMaxSumInArr(arr.slice(mid + 1, length + 1));
        
    /*
       MERGE: The divide step gave use the max sum on the left and right side,
       but we still need to account for the possibility of a contiguous
       array that goes from left to right through the midpoint
      
    */
		
    // Declare variables to record the maximum contiguous sums for each side
    let lMaxContiguousSum = 0,
      rMaxContiguousSum = 0;
        
    // On the left side, find sum of contiguous array and keep an updated record 
    // of the maximum
    /* 
      (NOTE: in order to account for contiguous arrays that traverse the midpoint,
       start the search from the midpoint - 1 index and traverse leftwards 
       towards index 0. This directionality guarantees that a contiguous array
       traversing the midpoint will be able to add the midpoint itself and the 
       right side's contiguous arr [this is exactly what is checked in the 
       final return statement below]) 
    */
    for (let i = mid - 1, currContiguousSum = 0; i >= 0; i--) {
      currContiguousSum += arr[i];
      lMaxContiguousSum = Math.max(lMaxContiguousSum, currContiguousSum);
    }
       
    // On the left side, find sum of contiguous array and keep an updated 
    // record of the maximum
    /* 
      (NOTE: in accordance with the last note, to account for sub arrays 
      that traverse the midpoint, start the search from the midpoint + 1 
      index and traverse rightwards 
      
    */
    for (let i = mid + 1, currContiguousSum = 0; i <= length; i++) {
      currContiguousSum += arr[i];
      rMaxContiguousSum = Math.max(rMaxContiguousSum, currContiguousSum);
    }
        
    /* 
        RETURN the max sum from the current array: either from the left side,
        right side, or a contiguous sub arrary traversing from left to 
        right through the midpoint 
    */
    return Math.max(
      // The maximum sum from a contiguous subarray that traverses the midpoint
      lMaxContiguousSum + arr[mid] + rMaxContiguousSum,
      // The max sum from each side (whether it was a single value or a contiguous sum) 
      lMaxSumInSubArr,
      rMaxSumInSubArr
    );
  }
};

var nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
console.log(maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4]));

{% endhighlight %}