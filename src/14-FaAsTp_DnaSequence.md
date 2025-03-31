# ForgeAlgo - DNA Sequence
Estimated Time: 2 hours<br>
Tech Stack: Java<br>
Keywords: Data Structure - Algorithms<br>
Experience Level: Beginner - Advanced<br>
Category: Arrays & Strings - Two Pointers - Sliding Window
 
# Find Repeated DNA Subsequences
📌 Problem:
Given a string dna representing a DNA sequence (composed of A, C, G, T) and an integer k, return all substrings of 
length k that appear more than once. The order of the returned substrings does not matter.

📌 Example:
```
Input: dna = "ACGAATTCCGGAACGAATTCCG", k = 10  
Output: {"ACGAATTCCG"}
```
📌 Constraints:

- 1 ≤ dna.length ≤ 10³
- 1 ≤ k ≤ 10
- dna[i] ∈ {'A', 'C', 'G', 'T'}

# Solution in plain English:
Create a package called ForgeAlgo. Import HashSet and Set from Java utilities. Define a public class named 
`RepeatedDnaSequences`. Inside the class, create a method called `findRepeatedDnaSequences` that takes a DNA string and an 
integer `k` as input. Initialize two HashSets—one for tracking seen substrings and another for storing repeated sequences.

Use a `while loop` to extract  substrings of length k and check if they have been seen before. If so, add them to the 
result set. Otherwise, add them to the seen set. Move the sliding window forward by incrementing left. Once all 
substrings are processed, return the result set. In the main method, create an instance of DnaTests, call 
find_sequences with a test DNA string, and print the output.

# Solution:
```java
package ForgeAlgo;

import java.util.HashSet; // A java collection that stores key-value pairs with array indexes.
import java.util.Set; // A collection that stores unique elements only. Commonly used in combo with HashSet.

// 1️⃣ Initialize:
public class RepeatedDnaSequences {
    public Set<String> findRepeatedDnaSequences(String dna, int k) { //Find repeated substrings of length k.
        Set<String> seen = new HashSet<>(); // Stores unique substrings while scanning.
        Set<String> result = new HashSet<>(); // Stores repeated substrings
        int left = 0; // Starting index of the window.
        
// 2️⃣ Process:
        while (left + k <= dna.length()) { //Ensure we stay in the boundaries of the string.  
            String substring = dna.substring(left, left + k); //Extracts a substring of length k starting at left.
            if (seen.contains(substring)) { // If it's a duplicate add to result.
                result.add(substring); 
            } else {
                seen.add(substring); // If it's unique add to "seen".
            }
            left++; // Move a step forward after completing the operation.
        }
        return result; // Return all repeated DNA Sequences found.
    }
    
// 3️⃣ Test: 
    // The block below will test the program.
    public static void main(String[] args) { // Main entry for execution. Static removes the need to create a new class.
        RepeatedDnaSequences solver = new RepeatedDnaSequences(); // Creates an object of the class to call it.
        // Call the class with test data. Stores the output in result.
        Set<String> result = solver.findRepeatedDnaSequences("ACGAATTCCGGAACGAATTCCG", 10);
        System.out.println("Output: " + result); // Prints the result.
    }
}

```
# Executing From Terminal:
- Compile
```bash
javac RepeatedDnaSequences.java
```
- Execute
```bash
java RepeatedDnaSequnces.java
```
# Output
Output: [ACGAATTCCG]

# 📢 Java Code in Plain English – Dictation for Memorization
## Step 1: Define the Package and Imports
- Start by creating a package named ForgeAlgo.
- Import two essential Java utilities:
  - HashSet (which allows storing unique substrings).
  - Set (which is the interface for the HashSet).
  
## Step 2: Create the Class
- Define a public class called DnaTests: This class will contain the logic to find repeated DNA sequences.

## Step 3: Define the find_sequences Method
Inside the class, create a public method called find_sequences.
It takes two parameters:
  - A string named dna, representing the DNA sequence.
  - An integer named k, representing the length of the sequence we are looking for. 
The method returns a Set<String>, which will store the repeated sequences.
  
## Step 4: Initialize Data Structures
- Create a HashSet called seen, which will store all substrings we encounter while scanning the DNA sequence.
- Create another HashSet called result, which will store only the substrings that appear more than once. 

## Step 5: Iterate Through the DNA Sequence
- Initialize an integer variable called left and set it to 0. This will serve as the starting index for extracting
substrings.
- Start a while loop, which will continue as long as (left + k) <= dna.length(). This ensures we do not go beyond the 
bounds of the string.

## Step 6: Extract and Process Each Substring
- Inside the loop, extract a substring of length k, starting at index left.
- Check if the substring already exists in the seen set:
- If it does, add it to the result set (since it has appeared more than once).
- If it does not, add it to the seen set (to track that we have encountered it).

## Step 7: Move the Sliding Window
- After checking the substring, increment left by 1 to shift the sliding window forward.

## Step 8: Return the Result
- Once the loop is done, return the result set, which contains all repeated sequences.

## Step 9: Implement the main Method
- Inside the main method, create an instance of DnaTests called solver.
- Call the find_sequences method with the DNA string "ACGAATTCCGGAACGAATTCCG" and k = 10.
- Store the result in a Set of Strings named result.
- Print "output:" followed by the result set.
