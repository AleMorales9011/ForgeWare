# Data Structure and Algorithms

### Objective

This repository aims to simplify DSA specifically for job interview purposes, focusing on practice rather than only theory.

## Pattern 01: Two Pointers

A pattern where two indices/pointers traverse a data structure.

It optimizes time complexity in problems like searching, partitioning, or comparing elements.

**Data structures:**
The two pointers pattern is most commonly applied to **_arrays and strings_**.
It also adapts well to linked lists, matrices, and other **linear-like** structures. 

**Types of problems it solves:**
It’s particularly effective for problems requiring comparisons, traversals, or conditional element selections.

# Step 01 Define MVS
Define the components of the solution that are common for all challenges.

### Two Pointers Algorithm Components

| Nº  | **Component**             | **Description** |
|-----|---------------------------|----------------|
| 01  | **Class & Methods**       | Implements the algorithm inside a class with: <br> - **Core Algorithm Method** (contains the two pointers logic). <br> - **Main Method** (defines test cases and calls the algorithm). |
| 02  | **Data Structure**        | Works with **arrays, strings, or linked lists** for linear traversal. |
| 03  | **Two Pointers Initialization** | Define two pointers: <br> - `low = 0` (**left pointer**). <br> - `high = length - 1` (**right pointer**). |
| 04  | **Loop Execution & Termination** | Run a **loop** while `low < high`. <br> - Compare values at `low` and `high` to determine movement. <br> - Adjust pointers: `low++` (right) or `high--` (left). <br> - Loop **stops when pointers meet or cross**. |
| 05  | **Processing & Output**   | Store valid results (if needed). <br> Return or print the processed result. |


# TWO POINTERS - STRUCTURE MEMORIZATION

### Mnemonic: "PLACE → CLEAN → MATCH → MOVE → DONE → TEST"

| **Step**  | **Mnemonic**  | **What You Do**                                                                 | **Where It Happens**  |
|-----------|--------------|---------------------------------------------------------------------------------|----------------------|
| **1. Place the pointers**  | **PLACE**  | Set `low = 0` (**left pointer**) and `high = length - 1` (**right pointer**).   | `low` → **first character**, `high` → **last character**. |
| **2. Clean the string**  | **CLEAN**  | Ignore non-alphanumeric characters and convert to lowercase. Not always needed. | Adjust `low` and `high` if needed. |
| **3. Compare characters**  | **MATCH**  | Check if `s[low] == s[high]`. If not, return `false`.                           | `low` and `high` are pointing at characters being compared. |
| **4. Move pointers**  | **MOVE**  | Shift `low++` (**move right**) and `high--` (**move left**).                    | `low` moves toward the center, `high` moves toward the center. |
| **5. Stop when pointers meet**  | **DONE**  | If the loop finishes, return `true` (it's a palindrome).                        | Pointers **meet or cross**. |
| **6. Run the test cases**  | **TEST**  | The main method defines test cases and calls the algorithm.                     | **Main method (`public static void main`)**. |


# Component
```java

// Boolean - the method only returns true or false
public static boolean isPalindrome(String s) {
  
    //MNEMONIC STEP: PLACE
    //First pointer - starts on the left (beginning) of the string
    // Second pointer - points to the index of the last character in the string
        int left = 0, right = s.length() - 1;
        
        //MNEMONIC STEP: MATCH
    //Ensures the loop should continue while the left pointer is less than/before the right pointer.     
        while (left < right) {
       
            // If chart at left is different than chart at right, it returns false, meaning the string isn't a palindrome.
            if (s.charAt(left) != s.charAt(right))
            {
                return false;
            }
            
            //MNEMONIC STEP: MOVE
            //Moves the pointer one step to the left
            left = left + 1;
            
            //Moves the pointer one step to the right
            right = right - 1;
        }
        
        //MNEMONIC STEP: DONE
        //If the loop completes without finding any mismatched characters, it returns 'true'.
        return true;
    }
```

3. Step 03: Create the main method - which serves as an entry point for your code. It tests the `isPalindrome` method with different test cases.

```java
public static void main(String[] arg) {
    //MNEMONIC STEP: TEST
    // The array of strings to test the method as it iterates through test cases
    String[] testCase = {
        "RACEACAR",
        "A",
        "ABCDEFGFEDCBA",
        "ABC",
        "ABCBA",
        "ABBA",
        "RACEACAR"
    };

    //The 'for' loop iterates through each string in the array
    //While 'k' is less than the length of the array of strings, the iteration will continue
    for (int k = 0; k < testCase.length; k++) {
  
        //Prints the iteration
        System.out.println("Test Case #" + (k + 1));
        
        //Prints the dotted lines
        System.out.println(new String(new char[100]).replace('\0', '-'));
        
        //Prints the string being tested and its length
        System.out.println("The input string is '" + testCase[k] + "' and the length of the string is " + testCase[k].length() + ".");
        
        //Returns 'true' or 'false' based on the method 'isPalindrome'
        System.out.println("\nIs it a palindrome? " + isPalindrome(testCase[k]));
        System.out.println(new String(new char[100]).replace('\0', '-'));
    }
}
