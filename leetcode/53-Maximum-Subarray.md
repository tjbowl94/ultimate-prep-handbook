# 53. Maximum Subarray

## Link
https://leetcode.com/problems/maximum-subarray/description/

## Description

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

### Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

### Example 2:
```
Input: nums = [1]
Output: 1
```

### Example 3:
```
Input: nums = [5,4,-1,7,8]
Output: 23
```
 
### Constraints:
```
1 <= nums.length <= 10^5
-10^4 <= nums[i] <= 10^4
```

## Solutions

### Solution 1: Nested Loops - O(n^2)

Write nested loops, with the first loop starting at the start of the array and the second array ending at the end of the array.

With these nested loops, you can create every possible subarray, storing only the largest sum.

Converting the array to a list before iterating through it is easiest, because the List class has the GetRange() method to easily get a subarray. 

```
public class Solution 
{
    public int MaxSubArray(int[] nums) 
    {
        var numList = nums.ToList();
        var maxSubArraySum = int.MinValue;

        for (var i = 0; i < numList.Count; i++)
        {
            for (var j = 1; j <= numList.Count - i; j++)
            {
                var subArraySum = numList
                    .GetRange(i, j)
                    .Sum();

                if (subArraySum > maxSubArraySum)
                {
                    maxSubArraySum = subArraySum;
                }
            }
        }

        return maxSubArraySum;
    }
}
```

### Solution 2: Kadane's Algorithm - O(n)

Kadane's algorithm is a dynamic programming algorithm that is essentially solving this exact problem.

The basis of Kadane's algorithm is that for any element at position i in the array, the local maximum is the max value between:
1. the local maximum at `i-1` + `A[i]`
2. `A[i]`

This makes the code very simple to write.

Simply initialize two variables, `localMaximum` and `globalMaximum`, initialized with the value of the first element of the array.

Then loop through the array, setting the values of the `localMaximum` and `globalMaximum` variables.

Follow the outline above to set `localMaximum` on each iteration of the loop. Set `globalMaximum` if the current `localMaximum` is greater than the value of `globalMaximum`.

```
public class Solution 
{
    public int MaxSubArray(int[] nums) 
    {
        var globalMaximum = nums[0];
        var localMaximum = nums[0];

        for (var i = 1; i < nums.Length; i++)
        {
            localMaximum = Math.Max(nums[i], localMaximum + nums[i]);

            if (localMaximum > globalMaximum)
            {
                globalMaximum = localMaximum;
            }
        }

        return globalMaximum;
    }
}
```