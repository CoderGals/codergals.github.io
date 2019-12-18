---
title: Largest Sum Contiguous Subarray
---

## Largest Sum Contiguous Subarray

We are going to have a series of articles on LeetCode problems, everyday a post on a problem on LeetCode.

The first post will tacke an Array problem, which is this: [Maximum SubArray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

You will probably have experienced solving different competitive programming
tasks related to contigous subarrays.

Well, I myself when I first encountered the Maximum Sum contigous array challenge
in LeetCode, I had no idea that a Kadane's algorithm was existing first of all.

I searched on google "maxsubarray leetcode 100% javascript" and one of
the result links was: https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/

Found out that there is an Algorithm and it's called Kadan's Algo, using
the dynamic programming paradigm to find the Maximum Sub Array.

#### Below you will find the short cut to the largest sum contiguous subarray solutions.

First, we will solve the problem using the paradigm Dynamic Programming and then we continue using the divide and conquer approach. 

The Algorithmic Paradigm is Dynamic Programming and the Time Complexity is O(n)

#### Dynamic Programming -> 

[Dynamic Programming](https://www.geeksforgeeks.org/dynamic-programming/) is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming. 


{% highlight js %} 

Initialize:
  max_so_far = 0
  curr_max = 0

Loop for each element of the array
  (a) max_so_far = array[0]
  (b) curr_max = array[0]

  (c) for each element of the array
          curr_max = Math.max(array[element], curr_max + array[element])
          max_so_far = Math.max(max_so_far, curr_max);
          
return max_so_far

}); {% endhighlight %}