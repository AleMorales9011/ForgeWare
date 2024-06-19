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
| Less than                      |    <     |   5 < 7  |  True  |
| Greater than or equal to       |    >=    |   5 >= 7 |  False |
| Less than or equal to          |    <=    |   5 <= 7 |  True  |

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
```

# Logical

| Name  | Example        |  Value     |     
|-------|----------------|------------|
|  And  |  True&&False   |  False     |
|  Or   |  True||False   |  True      | 
|  Not  |   !True        |  False     |

```java
```

# Conclusion

# Next
