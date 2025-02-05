# Data Structure and Algorithms

### Objective

This repository aims to simplify DSA specifically for job interview purposes, focusing on practice rather than only theory.

## Pattern 01: Two Pointers

A pattern where two indices/pointers traverse a data structure.

It optimizes time complexity in problems like searching, partitioning, or comparing elements.

```java
public static boolean isPalindromeWithoutTwoPointers(String s) {
    StringBuilder filtered = new StringBuilder();
    for (char c : s.toCharArray()) {
        if (Character.isLetterOrDigit(c)) {
            filtered.append(Character.toLowerCase(c));
        }
    }
    String original = filtered.toString();
    String reversed = filtered.reverse().toString();
    return original.equals(reversed);
}
```

```java
public static boolean isPalindromeWithTwoPointers(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) return false;
        left++;
        right--;
    }
    return true;
}
```

**Data structures:**
The two pointers pattern is most commonly applied to **_arrays and strings_**.
It also adapts well to linked lists, matrices, and other **linear-like** structures. 

**Types of problems it solves:**
It’s particularly effective for problems requiring comparisons, traversals, or conditional element selections.

## HOW TO USE IT:

#### 01. Exercise one - Valid Palindrome

This is one example of how to use the Two Pointers pattern to solve a common problem asked in interviews - the Valid Palindrome:
 
> A palindrome is a word, phrase, or sequence of characters that reads the same backward as forward.

1. Step 01: Create the class that will encapsulate the palindrome validation.

```java
public class ValidPalindromeForProduction {
```

2. Step 02: Create the method that checks whether the given String is a palindrome:

```java

// Boolean - the method only returns true or false
public static boolean isPalindrome(String s) {
  
    //First pointer - starts on the left (beginning) of the string
    // Second pointer - points to the index of the last character in the string
        int left = 0, right = s.length() - 1;
        
    //Ensures the loop should continue while the left pointer is less than/before the right pointer.     
        while (left < right) {
       
            // If chart at left is different than chart at right, it returns false, meaning the string isn't a palindrome.
            if (s.charAt(left) != s.charAt(right))
            {
                return false;
            }
            
            //Moves the pointer one step to the left
            left = left + 1;
            
            //Move~~~~s the pointer one step to the right
            right = right - 1;
        }
        
        //If the loop completes without finding any mismatched characters, it returns 'true'.
        return true;
    }
```

3. Step 03: Create the main method - which serves as an entry point for your code. It tests the `isPalindrome` method with different test cases.

```java
public static void main(String[] arg) {
    
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

```
