# 1. Two Sum

## Link
https://leetcode.com/problems/two-sum/

## Description

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 3:
```
Input: nums = [3,3], target = 6
Output: [0,1]
```
 
### Constraints:
```
2 <= nums.length <= 10^4
10^9 <= nums[i] <= 10^9
10^9 <= target <= 10^9
Only one valid answer exists.
```

## Solutions

### Solution 1: Nested Loops - O(n^2)

The obvious solution here is to loop through the array twice, finding every combination of two numbers and checking whether they add up to the target.

This solution is trivial to implement but slow, as it loops through the array twice, giving it a time complexity of O(n^2).

```
public class Solution 
{
    public int[] TwoSum(int[] nums, int target) 
    {
        for (var i = 0; i < nums.Length - 1; i++)
        {
            for (var j = i + 1; j < nums.Length; j++)
            {
                if (nums[i] + nums[j] == target)
                {
                    return new int[] { i, j };
                }
            }
        }

        return null;
    }
}
```

### Solution 2: Hash Table - O(n)

Initialize a dictionary with integers as keys and integers as values. 

Loop through the array a single time. For each element:
- first check whether the element's value exists as a key in the dictionary
- if it doesn't, then add a new entry into the dictionary, with the key being the complement of the element (target - element) and the value of the entry being the current index
- if it does, then return an array with the current index and the element in the dictionary

Note the initialization of the dictionary using the length of the nums array. This makes the memory complexity O(n), but it prevents unnecessary re-sizing of the array.

```
public class Solution 
{
    public int[] TwoSum(int[] nums, int target) 
    {
        var dictionary = new Dictionary<int, int>(nums.Length);
        for (var i = 0; i < nums.Length; i++)
        {
            if (dictionary.ContainsKey(nums[i]))
            {
                return new int[] { dictionary[nums[i]], i };
            }

            dictionary[target - nums[i]] = i;
        }

        return null;
    }
}
```