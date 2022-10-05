# 217. Contains Duplicate

## Link
https://leetcode.com/problems/contains-duplicate/description/

## Description

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

### Example 1:
```
Input: nums = [1,2,3,1]
Output: true
```

### Example 2:
```
Input: nums = [1,2,3,4]
Output: false
```

### Example 3:
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```
 
### Constraints:
```
1 <= nums.length <= 105
-10^9 <= nums[i] <= 10^9
```

## Solutions

### Solution 1: Hash Set - O(n)

This problem is a perfect fit for a hash set. 

Iterate through the array. 

For each element, check if it already exists in the set. 
- if it does, there's a duplicate 
- if it doesn't, add it to the set and move on

Return false after exiting the loop.

```
public class Solution 
{
    public bool ContainsDuplicate(int[] nums) 
    {
        var hashSet = new HashSet<int>(nums.Length);
        
        for (var i = 0; i < nums.Length; i++)
        {
            if (hashSet.Contains(nums[i]))
            {
                return true;
            }

            hashSet.Add(nums[i]);
        }

        return false;
    }
}
```