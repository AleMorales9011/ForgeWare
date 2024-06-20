![Banner](https://github.com/AleMorales9011/ForgeWare/blob/362a669ad3bbd7795a40d70e3cc18db09c065286/src/images/futurism-perspective-digital-nomads-lifestyle%20(2).jpg)
# POO with Java 2 

1 hour

# Operators

Operators are special symbols that perform specific operations on values (operands) and produce results. They are the building blocks of expressions and statements in your Java code.

# Arithmetic

| Symbol | Example  |     
|--------|----------|
|    +   |   3+5    |
|    -   |   5-3    | 
|    *   |   3*5    |
|    /   |   5/3    | 
|    %   |   5%3    |

```java
public class AreaCalculator {

  public static void main(String[] args) {
    // Declare variables to store length and width
    int length = 10;
    int width = 5;

    // Calculate area using arithmetic operator
    int area = length * width;

    // Print the calculated area
    System.out.println("The area of the rectangle is: " + area);
  }
}

```

# Relational 

|  Name                          |  Symbol  |  Example |  Value |      
|--------------------------------|----------|----------|--------|
| Equality                       |   ====   |  3===3   |  True  |
| Inequality                     |   !=     |  3!=3    |  False |
| Greater than                   |    >     |  5 > 7   |  False |
| Less than                      |    <     |  5 < 7   |  True  |
| Greater than or equal to       |    >=    |  5 >= 7  |  False |
| Less than or equal to          |    <=    |  5 <= 7  |  True  |

```java

public class RelationalOperatorExample {

  public static void main(String[] args) {
    int age = 25;
    boolean isAdult = age >= 18; // Checking if age is greater than or equal to 18

    if (isAdult) {
      System.out.println("You are an adult.");
    } else {
      System.out.println("You are not an adult.");
    }
  }
}
```

# Compound Attribution

| Example    | Use Case      |     
|------------|---------------|
|   x+=3     |   x = x + 3   |
|   x-=3     |   x = x - 3   | 
|   x*=3     |   x = x * 3   |
|   x/=3     |   x = x / 3   | 
|   x%=3     |   x = x % 3   |

```java
int count = 10;

// Increment count by 1 (same as count = count + 1)
count += 1;

// Decrement count by 2 (same as count = count - 2)
count -= 2;

// Multiply count by 5 (same as count = count * 5)
count *= 5;

```

# Increment and Decrement

| Example    | Use Case                    |     
|------------|-----------------------------|
|   ++x      |  Add 1 before using x       |
|   x++      |  Use x and then adds 1      | 
|   --x      |  Subtract 1 before using x  |
|   x--      |  Use x and then substract 1 | 

```java
public class IncrementDecrementExample {

  public static void main(String[] args) {
    int count = 5;

    // Pre-increment: increment count by 1 and then assign the new value to result
    int result = ++count;  // result becomes 6, count becomes 6

    System.out.println("After pre-increment, count = " + count);  // Output: After pre-increment, count = 6

    int anotherResult = count--;  // anotherResult gets the current value of count (6), then count is decremented to 5

    System.out.println("After post-decrement, anotherResult = " + anotherResult);  // Output: After post-decrement, anotherResult = 6
    System.out.println("After post-decrement, count = " + count);  // Output: After post-decrement, count = 5

  }
}

```

# Logical

| Name  | Example        |  Value     |     
|-------|----------------|------------|
|  And  |  True&&False   |  False     |
|  Or   |  True||False   |  True      | 
|  Not  |   !True        |  False     |

```java
public class AgeChecker {

  public static void main(String[] args) {
    int age = 25;
    boolean isAdult = age >= 18 && age < 65; // Combining conditions with AND

    if (isAdult) {
      System.out.println("You are an adult.");
    } else {
      System.out.println("You are not an adult.");
    }
  }
}
```
# Data Types

Here are the most used data types. 

# Primitive 

| Data Type | Description            |  Example        |     
|-----------|------------------------|-----------------| 
|  int      | interger values        |  1;45;465       |
|  float    | decimal numbers        |  1,34F;4,56F    |
|  double   | precise decimal numbers|  4,54;6,42      |
|  char     | single characters      |  '1';'%'        |
|  boolean  | logical values         |  true, value    |

```java

public class AreaCalculator {

  public static void main(String[] args) {
    // Declare variables with appropriate data types
    int length = 10; // int for whole number (width)
    double width = 5.2;  // double for decimal number (height)
    double area;  // double to store the calculated area (decimal)

    // Calculate the area
    area = length * width;

    // Print the result with descriptive message
    System.out.println("The area of the rectangle is: " + area);
  }
}

```
# Non-Primitive

| Data Type   | Description                      |  Example                        |     
|-------------|----------------------------------|---------------------------------| 
|  String     | Sequence of characers            |  "Hello World"                  |
|  Array      | Ordered items(same data type)    |  int[] numbers = {1,2,3,4};     |
|  Class      | Object blueprint                 |  public class  Classname {}     |
|  Interface  | Specifies methods for a class    |  public interface Interfacename |

```java

public interface Drawable {
  // Declare an abstract method without implementation
  void draw();
}

public class Main {

  public static void main(String[] args) {
    // Create an object of a class implementing the interface
    Drawable drawable = new Square();
    
    // Call the draw method through the interface reference
    drawable.draw();
  }
}

```
# Repetition Structures/ Loops

Allow you to execute a block of code multiple times based on a certain condition

# While loop 

This is the most basic loop construct. It repeatedly executes a code block as long as a specified condition is evaluated as true. 

```java
while (condition) {
  // code to be executed
}
```
# Do-while loop 

Similar to the while loop, it guarantees that the code block is executed at least once, even if the condition is initially false.

```java
do {
  // code to be executed
} while (condition);

```
# For loop

This loop combines initialization, condition checking, and increment/decrement in a concise syntax. It's often preferred for iterating a fixed number of times

```java
for (initialization; condition; increment/decrement) {
  // code to be executed
}
```

# Package Structure

Packages provide a logical way to group related classes, while directories on your disk reflect this structure.

```ruby
com
  - yourcompany.ecommerce
    - model
      - Product.java
      - Order.java
      - Customer.java
    - service
      - ProductService.java
      - OrderService.java
      - CustomerService.java
    - controller
      - ProductController.java
      - OrderController.java
      - CustomerController.java
```
# Directory Structure

Map directly to the package structure on disk. A package named `com.example.myapp` would have a corresponding directory structure like `com/example/myapp`. Each directory can contain Java source files (.java) and potentially subdirectories for sub-packages.

```ruby

src
  - com
    - yourcompany
      - ecommerce
        - model
          - Product.java
          - Order.java
          - Customer.java
        - service
          - ProductService.java
          - OrderService.java
          - CustomerService.java
        - controller
          - ProductController.java
          - OrderController.java
          - CustomerController.java

```

# Conclusion

Operators are the essential tools that let you perform operations on data in your Java programs. Without them, you wouldn't be able to do basic things like calculations (addition, subtraction, etc.) or comparisons.

# Next
