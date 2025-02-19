# Data Structure and Algorithms


# Principle 01 Engineering Mindset
DSA is a fully academic topic used by organizations to measure software engineering competence. To be able to solve 
their challenges I will use an engineering approach. Min information I need to solve the problem. 

# Step 01 Lean Approach
Apply Pareto's law to learn the least amount of solutions that solve the most amount of problems.

- Who are they
- How I will sort them
  
 ## 🔥 Most Common (Almost Always Asked)
  Two Pointers
  Sliding Window
  Hash Maps
  Modified Binary Search
  Dynamic Programming
  Backtracking
  Tree Depth-First Search (DFS)
  Tree Breadth-First Search (BFS)
  Graphs
  Heaps
  These are high-priority topics. You’ll almost certainly see them in interviews at companies like Google, Amazon, Facebook, and Microsoft.

## ⚡ Very Common (Frequently Asked)
Fast and Slow Pointers
Sort and Search
Stacks
Greedy Techniques
Subsets (Power Set Problems)
Top K Elements
Union Find
Merge Intervals
These are important but secondary. They often appear in medium-to-hard difficulty problems but are less fundamental than the first category.

## 🧐 Occasionally Asked (Advanced Problems)
Topological Sort
Trie (Prefix Tree)
Bitwise Manipulation
K-way Merge
Cyclic Sort
Matrices
In-Place Manipulation of a Linked List
These topics appear occasionally in specialized problems, usually in system design interviews or hard problems.

# Step 02 Reuse not Redo
I will reuse solutions and work to fit those into problems.
- Learn the solution
  - Mnemonics
  - Rhythm
- Try to solve similar challenges with it.
Treat problems like algebra where there are variables(data structures), and formulas (algorithms).
  - Understand variables
  - Substitute variables into solution

# Step 03 Simulation (Test)
- Step 01 Learn - Define MVS
- Step 02 Measure - Memorize
- Step 03 Build - Implement


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


# Memorize
- Mnemonics
- Rhythm

# TWO POINTERS - STRUCTURE MEMORIZATION

### Mnemonic: "CLEAN → PLACE → MATCH → MOVE → DONE → TEST"

| **Step**                       | **Mnemonic**  | **What You Do**                                                                 | **Where It Happens**  |
|--------------------------------|--------------|---------------------------------------------------------------------------------|----------------------|
| **1. Clean the string**        | **CLEAN**  | Ignore non-alphanumeric characters and convert to lowercase. Not always needed. | Adjust `low` and `high` if needed. |
| **2. Place the pointers**      | **PLACE**  | Set `low = 0` (**left pointer**) and `high = length - 1` (**right pointer**).   | `low` → **first character**, `high` → **last character**. |
| **3. Compare characters**      | **MATCH**  | Check if `s[low] == s[high]`. If not, return `false`.                           | `low` and `high` are pointing at characters being compared. |
| **4. Move pointers**           | **MOVE**  | Shift `low++` (**move right**) and `high--` (**move left**).                    | `low` moves toward the center, `high` moves toward the center. |
| **5. Stop when pointers meet** | **DONE**  | If the loop finishes, return `true` (it's a palindrome).                        | Pointers **meet or cross**. |
| **6. Run the test cases**      | **TEST**  | The main method defines test cases and calls the algorithm.                     | **Main method (`public static void main`)**. |



# Component
```java

// Boolean - the method only returns true or false
public static boolean isPalindrome(String s) {
    //CLEAN
    s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
    
    //PLACE
    //First pointer - starts on the left (beginning) of the string
    // Second pointer - points to the index of the last character in the string
    int left = 0, right = s.length() -1;
        
        //MATCH
    //Ensures the loop should continue while the left pointer is less than/before the right pointer.     
    while (left < right) {
       
            // If the character at left is different from the character at right, it returns false, meaning the string isn't a palindrome.
            if (s.charAt(left) != s.charAt(right))
            {
                return false;
            }
            
            //MOVE
            //Moves the pointer one step to the left
            left += 1;
            
            //Moves the pointer one step to the right
             right -= 1;
        }
        
        //DONE
        //If the loop completes without finding any mismatched characters, it returns 'true'.
        return true;
    }
```

3. Step 03: Create the main method - which serves as an entry point for your code. It tests the `isPalindrome` method with different test cases.

```java
public static void main(String[] arg) {
    //TEST
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
    for(String test : testCase) {
        System.out.println("Input \n" + test);
        System.out.println("\nIs it Palindrome...? \n" + isPalindrome(test));
    }
}

```
