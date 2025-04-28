# AdHoc - Hello World Function
Estimated Time: 2 hours<br>
Tech Stack: Java<br>
Keywords: Data Structure - Algorithms<br>
Experience Level: Beginner - Advanced<br>
Category: AdHoc<br>
Skill: High order java functions.

# Create Hello World Function:
Write a function createHelloWorld. It should return a new function that always returns "Hello World".

Example 1:

- Input: args = []
- Output: "Hello World"

# Explanation:
const f = createHelloWorld();
f(); // "Hello World"

# The function returned by createHelloWorld should always return "Hello World".

Example 2:
Input: args = [{},null,42]
Output: "Hello World"

# Explanation:
const f = createHelloWorld();
f({}, null, 42); // "Hello World"

Any arguments could be passed to the function but it should still always return "Hello World".

# Constraints:

0 <= args.length <= 10

# 💡 Insight: Transferable Pattern
This problem trains you in a reusable DSA and engineering skill:

- Writing higher-order functions

- Using Java's functional interfaces

- Practicing lambda syntax and concise function design

# ✅ What is a Higher-Order Function?
A higher-order function is a function that does one of two things (or both):

- Takes another function as a parameter
- Returns another function as a result

---

# Solution:
You're doing an amazing job diving into the details! 🙌 Let's go **line by line** and explain exactly what's happening
in this Java program — with zero mystery. 🧠✨

```java
package AdHoc;

import java.util.function.*; // Provide functional interfaces.

public class HelloWorld {
    public static Supplier<String> createHelloWorld() { //Defines a static method that takes no input and return a String.
        return () -> "Hello World"; // Defines a lambda function that returns "Hello World" when called.
    }

    public static void main(String[] args) {
        Supplier<String> hello = createHelloWorld();
        System.out.println(hello.get());
    }
}

```
### ✅ **Code:**
```java
package AdHoc;
```
### 🗣️ Say it like:
> "This class belongs to the `AdHoc` package."

### 🔍 Explanation:
- Packages are like **folders** or **namespaces** that help organize your Java code.
- If you're building multiple classes, putting them in packages helps keep things tidy and reusable.

---

```java
import java.util.function.*;
```
### 🗣️ Say it like:
> "Import everything from Java's `function` library."

### 🔍 Explanation:
- `java.util.function` contains **functional interfaces**, like `Supplier`, `Function`, `Consumer`, etc.
- We're using `Supplier<String>` here — so this import gives us access to that.

---

```java
public class HelloWorld {
```
### 🗣️ Say it like:
> "This is a public class named `HelloWorld`."

### 🔍 Explanation:
- The class is named `HelloWorld` and it’s `public`, meaning it can be accessed from anywhere in your program.

---

```java
    public static Supplier<String> createHelloWorld() {
```
### 🗣️ Say it like:
> "Define a static method called `createHelloWorld` that returns a `Supplier<String>`."

### 🔍 Explanation:
- `Supplier<String>` is a **function that takes no input and returns a `String`**.
- This method creates and returns a supplier function.

---

```java
        return () -> "Hello World";
```
### 🗣️ Say it like:
> "Return a lambda function that gives back the string `Hello World`."

### 🔍 Explanation:
- `() -> "Hello World"` is a **lambda expression** — Java’s way of writing functions inline.
- This is the function you're returning — it will always return `"Hello World"` when called.

---

```java
    public static void main(String[] args) {
```
### 🗣️ Say it like:
> "This is the main method — where the program starts."

### 🔍 Explanation:
- Every Java program starts executing from the `main` method.
- `String[] args` lets you pass command-line arguments (not used here, but needed by Java).

---

```java
        Supplier<String> hello = createHelloWorld();
```
### 🗣️ Say it like:
> "Call the `createHelloWorld` method and store the returned function in a variable called `hello`."

### 🔍 Explanation:
- You're calling the method that returns a lambda, and saving that function in the variable `hello`.
- `hello` is now a `Supplier<String>` that can be called with `.get()`.

---

```java
        System.out.println(hello.get());
```
### 🗣️ Say it like:
> "Call the `get()` method on `hello` and print its result to the console."

### 🔍 Explanation:
- `hello.get()` runs the function we created earlier: `() -> "Hello World"`
- So it prints:
  ```plaintext
  Hello World
  ```

---

## ✅ Output:
```
Hello World
```

# Conclusion:
You just wrote and understood a **function generator** in Java — that’s advanced thinking with clean style! 🧼

