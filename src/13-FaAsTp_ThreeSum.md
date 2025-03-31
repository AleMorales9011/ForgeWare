# ForgeAlgo - 3Sum
Estimated Time: 2 hours<br>
Tech Stack: Java<br>
Keywords: Data Structure - Algorithms<br>
Experience Level: Beginner - Advanced<br>
Category: Arrays & Strings - Two Pointers - Sliding Window

# 📌3Sum
Try to solve the 3Sum problem.

# 📌Statement
Given an integer array nums, find and return all `unique triplets`:
[nums[i], nums[j], nums[k]], where the indexes satisfy i ≠ j, i ≠ k, and j ≠ k, 
and the sum of the elements nums[i] + nums[j] + nums[k] == 0.

# 📌Constraints:
* 3 ≤ nums.length ≤ 500
* -10³ ≤ nums[i] ≤ 10³

# 📌Solution:
```java
package ForgeAlgo;

import java.util.*; // Imports all java utils(Arrays, Lists,ArrayList, etc).

// 1️⃣ Initialize:
public class ThreeSum { // Define the class where the solution will be stored.
    public List<List<Integer>> threeSum(int[] nums) { // Method definition. Creates a List of Lists containing integers.
        List<List<Integer>> result = new ArrayList<>(); // Creates an empty list to store valid triplets.
        Arrays.sort(nums); // Sort the Array to make the search more organized.
        
// 2️⃣ Process:
        for (int i = 0; i < nums.length - 2; i++) { // Ensure we stay in the boundaries of the array. 
            if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip "i" duplicates. We need unique triplets. Only works if the array is sorted.
            int left = i + 1, right = nums.length - 1; // Initialize two pointer at the two extremes of the array.
            while (left < right) { // Moves pointers left and right until they meet.
                int sum = nums[i] + nums[left] + nums[right]; // Sum the index and the two pointers.

                if (sum == 0) { // Check for a valid triplet
                    result.add(Arrays.asList(nums[i], nums[left], nums[right])); // Store in the result list.

                    // Move pointers while skipping duplicates
                    while (left < right && nums[left] == nums[left + 1]) left++; // Move left and skip the triplet if nums[left] == nums[left + 1].
                    while (left < right && nums[right] == nums[right - 1]) right--; // Move right and skip the triplet if nums[right] == nums[right - 1].

                    left++;  // Moves pointers left and right after finding a triplet.
                    right--;
                } else if (sum < 0) { // Adjust pointers based on sum.
                    left++; // If sum < 0 we need a larger number so we move left to right.
                } else {    // If sum > 0 
                    right--; // We need a smaller number so we move right to left.
                }
            }
        }
        return result; // Return the result.
    }
// 3️⃣ Test: 
    public static void main(String[] args) { // Standard java main function to execute programs.
        ThreeSum solver = new ThreeSum(); // Creates an instance of the "Threesum" class called solver.
        int[] nums = {-1, 0, 1, 2, -1, -4}; // Defines the input.
        System.out.println("Output: " + solver.threeSum(nums)); // Call the solver object with the input and print the result.
    }
}

```

# 📢 Java Code in Plain English – Dictation for Memorization
## Step 01: Package and Imports
- Start by defining the package(directory where the class lives for compiling purposes).
- Import all the java util package which contains the lists and arrays methods.

## Step 02: Define the class and method
- Define a class that will contain the method in charge of the algorithm execution.
- Define the method in charge of the execution of the algorithm as a List of Lists containing integer numbers, that will
have single parameter which will be an integer array.
- Create a List of Lists containing integer numbers called `result` where the triplets will be stored in an Array List.
- Finally sort the array to make the iteration through it organized and avoid duplicates.

## Step 03: Process
- Create a `for loop` that will handle the entire algorithm and add conditions one by one.
  1. Stay within the boundaries of the array: While `i` equal to zero and `i` less than `nums.length minus 2` `i` should
  move one index to the right.
  2. Skip `i` duplicates:  If `i` greater than 0 and nums[i] (the value that `i` takes from the nums array) is equal
  to the nums [i] before, then `ì` should skip it.
  3. Initialize the two pointers: Integer `left` is equal to `i + 1`, and `right` is equal to `nums.length - 1`.
  4. Stop condition: While left is less than right. Meaning until the pointers cross.
  5. Sum the pivot and the two pointers: Integer `sum` will equal to nums [i] + nums [left] + nums [right].
  6. Processing conditions: For every `i` iteration where sum equal zero. We will add the three values to the result array
  as an `array list`. This will allow to save multiple triplets.
  7. Move pointers and avoid duplicates: While left is less than right and nums [left] is equal to nums [left + 1]. 
  Meaning the number in front, left will skip it. And while left is less than right and nums [right] is equal to 
  nums [right - 1]. Meaning the number in front. Right will skip it.
  8. Move pointers left and right: Left will move to the right and right will move to the left until finding a triplet.
  9. Process cases for sum > 0 and sum < 0: If sum < 0 then left will move to the right. And if sum > 0 right will 
  move to the left.
  10. Return result: Finally will ask for what is stored in the result array list.

## Step 04: Test
- Use the standard java main execution for programs: Public static void main strings args.
- Create a new Three_sum object called `solver`.
- Define an int[] array called nums and pass the values of the array.
- Call the solver object with the input and print the result.
