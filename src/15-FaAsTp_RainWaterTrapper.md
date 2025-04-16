# ForgeAlgo - Two Pointers

Estimated Time: 15–20 min
Tech Stack: Java
Keywords: Two Pointers, Arrays, Dynamic Programming, Stack, Monotonic Stack
Experience Level: Intermediate to Advanced

# Rain Water Trapper

Given that `n` non-negative integers represent an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

### ✅ **Goal**:
Given an array `height[]` representing the elevation of bars `(width = 1)`, compute how much rain water can be trapped between them after it rains.

## Example 1:

![image](https://github.com/user-attachments/assets/106f903d-d84e-453e-8ee7-9f8a27fc06b3)

Each bar represents a wall.
Where there's a dip or valley between two taller walls, `water can collect`.
The amount of water that gets trapped at a position depends on which of the tallest walls on both sides is shorter.

## 📥 Input
An array of non-negative integers: height.
(e.g. [0,1,0,2,1,0,1,3,2,1,2,1])

At index 0, `there’s no wall on the left` → no water can be held.

At index 1, there’s a small wall (1).

At index 2, it's a dip (0) — and index 3 has a taller wall (2)
→ So `index 2 can trap water` — 1 unit, between the bars at 1 and 3.

We repeat this check across the entire elevation map:

"Is this position lower than both sides?"

"If so, how much water can it hold?"

## 💡 Visual Rule:
Water gets trapped when a bar is lower than both neighbors, and the amount depends on how much space is between the walls.

## 📤 Output
A **single integer** — the total amount of water trapped.
(e.g. 6 for the example above)

## 📌 Rules & Constraints

| Rule                                | Explanation                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
| 1 <= height.length <= 20,000       | The elevation map must contain at least 1 bar and no more than 20,000 bars. |
| 0 <= height[i] <= 100,000           | Each bar's height is a non-negative integer, up to 100,000 units high.     |
| Each bar is `1` unit wide           | The width of each bar is uniform, which simplifies the area calculation.   |
| Water is trapped between taller bars | Water can only be stored in "valleys" formed by taller bars on both sides. |


## 🧠 Your Job
Build a function that:

1. Uses two pointers to walk from both sides.
2. Calculates the trapped water one step at a time.
3. Keeps track of the maximum heights seen so far from left and right.

## 🔁 Bonus Insight:
You only need to know:

- The highest wall to the left
- The highest wall to the right

- → The smaller of those two decides how high water can rise at that spot.

```java

package twoPointers; // This line declares the package name
// 🗣️ Say it: "This file belongs to the twoPointers package."

public class RainWaterTrapper { // Declares the class
// 🗣️ Say it: "This is the class called RainWaterTrapper."

    public static int trap(int[] height) { // Defines the method that takes an array and returns total water
        // 🗣️ Say it: "Define a public static method named trap that takes an integer array called height and returns an integer — the total amount of water trapped."

        if (height == null || height.length == 0) return 0;
        // 🧠 Check if the array is empty or null
        // 🗣️ Say it: "If the height array is null or empty, return zero immediately - there's nothing to process."

        int left = 0, right = height.length - 1;
        // 🧠 Set up two pointers at the edges of the array
        // 🗣️ Say it: "Create two pointers — left at 0 and right at the last index."

        int leftMax = 0, rightMax = 0;
        // 🧠 These track the max height seen so far from each side
        // 🗣️ Say it: "Initialize two auxiliary variables — leftMax and rightMax — to track the maximum 
        //    height encountered from the left and right as we traverse inward."
        // 🌟 These aren't pointers! Pointers are variables that store a memory address or index position in a data structure.

        int totalWater = 0;
        // 🧠 This will accumulate the trapped water
        // 🗣️ Say it: "Create a counter called totalWater to store the result."

        while (left < right) {
            // 🧠 Loop until the two pointers meet
            // 🗣️ Say it: "While left is less than right, keep going."

            if (height[left] < height[right]) {
                // 🧠 Choose the shorter side to process
                // 🗣️ Say it: "If the left bar is shorter than the right bar..."

                if (height[left] >= leftMax) {
                    // 🧠 Update leftMax if needed
                    // 🗣️ Say it: "If the current left bar is taller than leftMax, update leftMax."

                    leftMax = height[left];
                } else {
                    totalWater += leftMax - height[left];
                    // 🧠 Otherwise, trap water = leftMax - current height
                    // 🗣️ Say it: "Trap water at this index and add it to totalWater. 
                    // Add to totalWater the difference between leftMax and the current bar height at left"
                }

                left++;
                // 🧠 Move the left pointer inward
                // 🗣️ Say it: "Move the left pointer one step to the right."
            } else {
                // 🧠 Same logic for the right side if it's the shorter bar
                // 🗣️ Say it: "Otherwise, do the same logic for the right side."

                if (height[right] >= rightMax) {
                    rightMax = height[right];
                    // 🗣️ Say it: "If the current right bar is taller than rightMax, update rightMax."
                } else {
                    totalWater += rightMax - height[right];
                    // 🗣️ Say it: "Trap water at the right index and add it to totalWater."
                }

                right--;
                // 🧠 Move the right pointer inward
                // 🗣️ Say it: "Move the right pointer one step to the left."
            }
        }

        return totalWater;
        // 🧠 After the loop, return the total amount of trapped water
        // 🗣️ Say it: "Return the total amount of trapped rainwater."
    }

    public static void main(String[] args) {
        // 🧠 Entry point for running tests
        // 🗣️ Say it: "This is the main method where we run our tests."

        int[] elevation1 = {0,1,0,2,1,0,1,3,2,1,2,1};
        // 🧠 First test input
        // 🗣️ Say it: "Create an array representing elevation heights."

        int[] elevation2 = {4,2,0,3,2,5};
        // 🧠 Second test input
        // 🗣️ Say it: "Create another elevation map for a second test case."

        System.out.println("Trapped water: " + trap(elevation1));
        // 🧠 Run the function and print result
        // 🗣️ Say it: "Print how much water is trapped for the first test."

        System.out.println("Trapped water: " + trap(elevation2));
        // 🧠 Same for the second test
        // 🗣️ Say it: "Print how much water is trapped for the second test."
    }
}
```



