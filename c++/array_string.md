# Contents
- [Contents](#contents)
  - [1. Merge Sorted Array](#1-merge-sorted-array)
  - [2. Remove Element](#2-remove-element)
  - [3. Remove Duplicates from Sorted Array](#3-remove-duplicates-from-sorted-array)
  - [4. Remove Duplicates from Sorted Array II](#4-remove-duplicates-from-sorted-array-ii)
  - [5. Majority Element](#5-majority-element)
  - [6. Rotate Array](#6-rotate-array)

## 1. Merge Sorted Array

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].

Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

Constraints:

    nums1.length == m + n
    nums2.length == n
    0 <= m, n <= 200
    1 <= m + n <= 200
    -10^9 <= nums1[i], nums2[j] <= 10^9

Follow up: Can you come up with an algorithm that runs in O(m + n) time?

---

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        // Fill the array from the last element
        int p1 = m - 1;
        int p2 = n - 1;
        int p = m + n - 1;
        while (p1 >= 0 && p2 >= 0) {
            if (nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1];
                p1--;
            } else {
                nums1[p] = nums2[p2];
                p2--;
            }
            p--;
        }
        // Copy remaining elements from array2
        while (p2 >= 0) {
            nums1[p] = nums2[p2];
            p2--;
            p--;
        }
    }
};
```
## 2. Remove Element
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

    Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
    Return k.

Example 1:

Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:

    0 <= nums.length <= 100
    0 <= nums[i] <= 50
    0 <= val <= 100
---
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        // Keep track of valid element to keep using a pointer k
        int k = 0;
        for(int i = 0; i < nums.size(); i++){
            if (nums[i] != val){
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
}
```

## 3. Remove Duplicates from Sorted Array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

    Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
    Return k.

Example 1:

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:

    1 <= nums.length <= 3 * 10^4
    -100 <= nums[i] <= 100
    nums is sorted in non-decreasing order.
---

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int total_elems = nums.size();
        if (total_elems <= 1) {
            return total_elems;
        }
        int prev = nums[0];
        int k = 1; // Keep track of where valid elements should be placed
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] != prev) {
                nums[k] = nums[i];
                prev = nums[i];
                k++;
            }
        }
        return k;
    }
};
```

## 4. Remove Duplicates from Sorted Array II

Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.
Example 1:

Input: nums = [1,1,1,2,2,3]
Output: 5, nums = [1,1,2,2,3,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3,_,_]
Explanation: Your function should return k = 7, with the first seven elements of nums being 0, 0, 1, 1, 2, 3 and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:

    1 <= nums.length <= 3 * 10^4
    -10^4 <= nums[i] <= 10^4
    nums is sorted in non-decreasing order.
---

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 0; // pointer to valid elements

        // Check if 2nd neighbour from left has the same value
        for (int i = 0; i < nums.size(); i++){
            if (k < 2 || nums[i] != nums[k - 2]){
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
};
```

## 5. Majority Element

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Example 1:

Input: nums = [3,2,3]
Output: 3

Example 2:

Input: nums = [2,2,1,1,1,2,2]
Output: 2

Constraints:

    n == nums.length
    1 <= n <= 5 * 10^4
    -10^9 <= nums[i] <= 10^9

---
```cpp

// Using Hashmap, Time: O(n), Space: O(N)
class Solution1 {
public:
    int majorityElement(vector<int>& nums) {
        int maj_count = nums.size() / 2;
        unordered_map<int, int> hash_map;
        int max_count = 0;
        int majority_num = 0;

        for (int i = 0; i < nums.size(); i++) {
            hash_map[nums[i]]++;
            if (hash_map[nums[i]] > max_count) {
                max_count = hash_map[nums[i]];
                majority_num = nums[i];
            }
            if (max_count > maj_count) {
                return majority_num;
            }
        }
        return majority_num;
    }
     
};

// Using Boyer-Moore Voting Algorithm, Time: O(n), Space: O(1)
class Solution2 {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = nums[0];
        int count = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (count == 0) {
                candidate = nums[i];
            }
            count += (candidate == nums[i]) ? 1 : -1;
        }
        return candidate;
    }
};
```

## 6. Rotate Array

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:

Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]

 

Constraints:

    1 <= nums.length <= 10^5
    -2^{31} <= nums[i] <= 2^{31} - 1
    0 <= k <= 10^5

Follow up:

    Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.
    Could you do it in-place with O(1) extra space?
---

```cpp
// In-place soultion, by reversing arrays
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int N = nums.size();
        k %= N; // To handle cases where k > N
        int temp = 0;

        // Reverse entire array
        for (int i = 0; i < N / 2; i++) {
            temp = nums[i];
            nums[i] = nums[N - i - 1];
            nums[N - i - 1] = temp;
        }
        // Reverse first k elements
        for (int i = 0; i < k / 2; i++) {
            temp = nums[i];
            nums[i] = nums[k - i - 1];
            nums[k - i - 1] = temp;
        }
        // Reverse remaining n-k elements
        for (int i = 0; i < (N - k) / 2; i++) {
            temp = nums[i + k];
            nums[i + k] = nums[N - i - 1];
            nums[N - i - 1] = temp;
        }
    }
};
```