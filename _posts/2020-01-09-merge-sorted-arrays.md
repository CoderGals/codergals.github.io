---
title: Merge Sorted Arrays
layout: post
date: '2020-01-09 18:03:00'
image: "/assets/images/leetcode/leetcode.png"
headerImage: true
tag:
- leetcode
- competitive-programming
- codergals
- opensource
- tech-interviews
- arrays
category: blog
author: AlbionaHoti
description: LeetCode Challenges
---

## 88. Merge Sorted Array


Given two sorted integer arrays nums1 and nums2, merge nums2
into nums1 as one sorted array.

Note:
1. The number of elements initialized in nums1 and nums2 are m and n respectively.
2. You may assume that nums1 has enough space (size that is greater or
    equal to m + n) to hold additional elements from nums2.

```
   Example:

   Input: 
   nums1 = [1,2,3,0,0,0], m = 3
   nums2 = [2,5,6],       n = 3

   Output: [1,2,2,3,5,6]

```

### 1. First Solution

 * Starting at the end of the first array -> nums1
      * compare the last initialized elements in each of the two arrays
      * which one is bigger we will put in the last element of the first array -> nums1[nums1.length-1] 
      
      1. First we start by comparing 6 and 3 -> which one is bigger? 6 -> nums1[nums1.length-1] => [1, 2, 3, 0, 0, 6]
          1.1 We continue to compare 5 and 3 -> which one is bigger? 5 -> nums1[nums1.length-2] => [1, 2, 3, 0, 5, 6]
          1.2 We continue to compare 2 and 3 -> which one is bigger? 3 -> nums1[nums1.length-3] => [1, 2, 3, 3, 5, 6]
          1.3 We continue to compare 2 and 2 -> which one is bigger? no one -> nums1[nums1.length-4] => [1, 2, 2, 3, 5, 6]


    * m is the number of the initialized variables in nums1
    * n is the number of the initialized variables in nums2 


```
    const merge = function (nums1, m, nums2, n) {
        let first = m - 1;
        let second = n - 1;

        for (let i = m + n - 1; i >= 0; i--) {
            if (second < 0) {
                break;
            }

            if (nums1[first] > nums2[second]) {
                nums1[i] = nums1[first];
                first--;
            } else { 
                nums1[i] = nums2[second];
                second--;
            }
        }
    };

```

### 2. Second Solution

Approach: 

* Start from back of nums1 and iterate through both lists
backwards, putting the larger of nums1[m] and nums2[n] into the last 
element of nums1 so far.  Starting from the back allows us to
do this in one loop. 

* Once an element is copied over, it is in it's "final spot" in the sorted
array, and will not move again. 

* The algorithm has a runtime of O(m+n) and space of O(1).

* The latter is true because even though a variable is initialized, 
it is not a function of the inputs m or n.

*  Note: This could have been done without initializing 'final' at all,
but it reads better with it.

```

    const merge = function (nums1, m, nums2, n) {
        let final = m + n - 1;
        m--;
        n--;

        while (m >= 0 || n >= 0) {
            // if no more nums2 then just copy remaining m elements
            if (n < 0 || nums1[m] > nums2[n]) {
                nums1[final] = nums1[m];
                m--;
            } else { // m < 0 || nums1[m] < nums2[n]
                nums1[final] = nums2[n];
                n--;
            }
            final--;
        }

        return nums1;
    };
```





[Merge Sorted Arrays](https://leetcode.com/problems/merge-sorted-array/)
