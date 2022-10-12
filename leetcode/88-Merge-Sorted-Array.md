# 88. Merge Sorted Array

## Link
https://leetcode.com/problems/merge-sorted-array/

## Description

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers m and n, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

### Example 1:
```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```

### Example 2:
```
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
```

### Example 3:
```
Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```
 
### Constraints:
```
nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-10^9 <= nums1[i], nums2[j] <= 10^9
```

## Solutions

### Solution 1: Two Pointers - O(m + n)

This solution is basically just the same strategy as the "merge" part of "merge sort", with the added complication that we are manipulating one of the arrays directly rather than a third array.

We can solve that first complication by simply copying the existing array into another one, and then using the original array as our working array.

We then initialize a few pointers. One for each of the two arrays we're copying from, and one for the array we're copying into. We compare the elements at each of the two pointers, copy over the lower element, and then increment the pointer from the array we copied from. We also increment the pointer that's associated with the array we're copying to.

Finally, because our loop condition exits based on EITHER of the two pointers reaching the end of its respective array. This means that once we exit the loop, we still have to copy over any remaining elements from one of the source arrays.

```
public class Solution 
{
    public void Merge(int[] nums1, int m, int[] nums2, int n) 
    {
        var nums1Copy = new int[m];

        Array.Copy(nums1, nums1Copy, m);

        var i = 0;
        var j = 0;
        var k = 0;

        while (i < m && j < n)
        {
            if (nums1Copy[i] < nums2[j])
            {
                nums1[k] = nums1Copy[i];
                i++;
            }
            else
            {
                nums1[k] = nums2[j];
                j++;
            }
            k++;
        }

        Array.Copy(nums1Copy, i, nums1, k, m - i);
        Array.Copy(nums2, j, nums1, k, n - j);
    }
}
```
