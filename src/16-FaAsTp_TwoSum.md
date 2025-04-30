# TwoPointers - Two Sum
Estimated Time: 2 hours<br>
Tech Stack: Java<br>
Keywords: Data Structure - Algorithms<br>
Experience Level: Beginner - Advanced<br>
Category: Opposite Ends

# Two Sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]


# Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.

Follow-up: *Can you come up with an algorithm that is less than O(n2) time complexity?*

# Solution:

```java
package TwoPointers; // Defines the namespace or directory that will contain the class.

import java.util.*; // Import java utils to be able to use arrays.

public class TwoSum { // Define the class that will contain the algorithm logic.
    public int[] findTwoSum(int[] nums, int target) { // Int[] Method that takes the array and the target.
        // Step 1: Store value and original index.
        int[][] indexedNums = new int[nums.length][2]; // Creates a 2D array that stores indexes and values separately.
        for (int i = 0; i < nums.length; i++) { // Loops through the array.
            indexedNums[i][0] = nums[i];  // Stores values
            indexedNums[i][1] = i;        // Stores original index
        }
        // Step 2: Sort by value
        Arrays.sort(indexedNums, Comparator.comparingInt(a -> a[0])); // Sort the arrays by value column so we can use the Two Pointers technique. 
// For each "a"(row) use "a sub-zero" (column), to sort by. 
        // Step 3: Two pointers
        int left = 0, right = nums.length - 1; // Define pointers.

        while (left < right) { // Move pointers.
            int sum = indexedNums[left][0] + indexedNums[right][0]; // Add the values to the two pointers.
            if (sum == target) { // If the sum matches.
                return new int[] { indexedNums[left][1], indexedNums[right][1] }; //Return the indexes.
            } else if (sum < target) { // If not move the indexes right and left.
                left++;
            } else {
                right--;
            }
        }

        return new int[0]; // If the condition is never met will return an empty array.
    }

    public static void main(String[] args) { // Testing. Standard entry point in java.
        TwoSum solver = new TwoSum(); // Creates a new TwoSum object solver to use his method.

        int[] nums1 = {2, 7, 11, 15}; // Defines the nums array.
        System.out.println("Output: " + Arrays.toString(solver.findTwoSum(nums1, 9))); // [0, 1] //Prints the output.
//Arrays.toString is needed to print the result properly.
    }
}

```
---

## ⚔️ **Challenges of the Two Sum (Two Pointers + Sorting) Solution**

| 🔍 Challenge                                                                                   | 💬 Why It Can Be Tricky                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1. Preserving original indexes after sorting**                                               | You need to return the original positions of the numbers, but sorting the array changes their order. You must track both the **value and original index**.                                                                              |
| **2. Creating and using a 2D array** (`indexedNums[i][0] = value; indexedNums[i][1] = index;`) | Storing values with their original indexes in a new structure is conceptually new for many beginners. Understanding the layout (`[value, index]`) and how to access it correctly is essential.                                          |
| **3. Sorting with a custom comparator**                                                        | Using `Arrays.sort()` with a lambda like `Comparator.comparingInt(a -> a[0])` requires understanding of **lambda expressions**, **functional interfaces**, and how sorting works in Java.                                               |
| **4. Writing Two Pointers logic**                                                              | Choosing when to move `left++` or `right--` based on the sum comparison (`sum < target` or `sum > target`) is a critical logic decision. It feels like math + intuition, and mistakes here lead to off-by-one errors or infinite loops. |
| **5. Understanding that it only finds the first valid pair**                                   | The problem guarantees **one solution**, but understanding why this algorithm stops at the first match and why that’s okay is important to avoid over-engineering.                                                                      |
| **6. Remembering when to use Two Pointers vs HashMap**                                         | Not every problem allows sorting (especially if original array order matters). Knowing that the two-pointer approach **only works after sorting** is a key insight.                                                                     |

---

## ✅ Summary

> The **core challenge** of the Two Pointers version of Two Sum is **managing value + index tracking correctly after
> sorting**, and using a comparator and pointer logic fluently in Java.
Once you master that, you unlock a **reusable pattern** that helps you crush a lot of classic problems 🔓🔥
