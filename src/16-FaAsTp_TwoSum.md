# ForgeAlgo - Two Pointers
Estimated Time: 5 min

Tech Stack: Java

Keywords: Data Structure - Algorithms

Experience Level: Beginner - Advanced

# Problem Statement:

### ✅ **Goal**
Given an array of integers `nums` and an integer `target`, find **two different numbers** in the array that **add up to the target**, and **return their original indexes**.

---

### 📥 **Input**
- An array of integers: `nums`  
  (e.g. `[2, 7, 11, 15]`)
- An integer `target`  
  (e.g. `9`)

---

### 📤 **Output**
- An array of two integers representing the **indexes** of the two numbers that sum to the target  
  (e.g. `[0, 1]` for `2 + 7 = 9`)

---

### 📌 **Rules & Constraints**
| Rule | Description |
|------|-------------|
| Only **one valid solution** will always exist |
| You **cannot use the same element twice** (no reusing the same index) |
| You can return the answer **in any order** |
| Array size: `2 ≤ nums.length ≤ 10⁴` |
| Number range: `-10⁹ ≤ nums[i] ≤ 10⁹` |
| Target range: `-10⁹ ≤ target ≤ 10⁹` |

---

### 🧠 **Your Job**
Build a function that:
- Loops through the array
- Finds the **two values that sum to `target`**
- Returns their **original indexes**

---

# Solution:

```java
package twoPointers; // Define the directory containing the class.

import java.util.*; // Import all java utils to use arrays.

public class TwoSum { // Define the class that will contain the algorithm logic.
    public int[] findTwoSum(int[] nums, int target) { // Define method that takes an int array and a target. 
    
    
        int[][] indexedNums = new int[nums.length][2]; 
        /* Stores the value of the number and its original index in the array,
        * if the problem asks us to return their original position.
        * This line says: 'I want to store one row per element in the array ([nums.length]). Each row will store two pieces of information ([2]).
        */


        for (int i = 0; i < nums.length; i++) { //Loops through each index in the array, starting at 0 and stopping before the end.
            indexedNums[i][0] = nums[i];  // Stores the value being passed - [i] is the current row, [0] is the column where the value will be stored
            indexedNums[i][1] = i;        // Stores the original index before the array is sorted
        }

        Arrays.sort(indexedNums, Comparator.comparingInt(a -> a[0])); //SortS the array indexedNums in ascending order based on the value stored in the first column of each row.
    
        int left = 0, right = nums.length - 1; // Declare the two pointers

        while (left < right) { //Declares a loop that the block below should happen while left is before right
            int sum = indexedNums[left][0] + indexedNums[right][0]; // Adds the VALUE from the two pointers
            if (sum == target) { 
                return new int[] { indexedNums[left][1], indexedNums[right][1] }; // If the summed values equal the target, it returns their indexes stored at column 01.
            } else if (sum < target) { //Moves the pointer from left to right if the sum value is less than the target
                left++;
            } else { //Moves the pointer from right to left if the sum value is larger than the target
                right--;
            }
        }

        return new int[0]; // Should never reach here if one solution is guaranteed
    }

    public static void main(String[] args) { //The starting point of the program, which takes an array of strings called 'args'
        TwoSum solver = new TwoSum(); //Makes a new instance of the TwoSum class and stores it in a variable called 'solver'.

        int[] nums = {2, 7, 11, 15};
        System.out.println("Output: " + Arrays.toString(solver.findTwoSum(nums, 9))); // [0, 1]

    }
}
```
