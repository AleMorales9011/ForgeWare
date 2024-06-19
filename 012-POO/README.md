![Banner](https://github.com/AleMorales9011/ForgeWare/blob/44b1d40c5e502ddb50204e92f0f6eeeb90133772/src/images/futurism-perspective-digital-nomads-lifestyle%20(1).jpg)
# POO with Java

1 hour

POO (Object-oriented programming) allows developers to model software in a very similar fashion to the way we think. In terms of Classes( a category of something), objects (an element inside that category), attributes ( a characteristic of the component), and methods(something the element does). 

# Class:

```Java
public class ClassName {
  // Class body containing attributes and methods
}
```
`public:` This is an access modifier, in this case, making the class accessible from anywhere in the program.
`ClassName:` This is the name you choose for your class, following Java naming conventions (starts with an uppercase letter).
`// Class body:` This is where you define the attributes and methods of the class.

# Object:

```java
ClassName objectName = new ClassName();
```
1. `ClassName:` Replace this with the actual name of your class.
2. `objectName:` This is the name you choose for your object (reference variable).
3. `new ClassName():` This creates a new instance (object) of the ClassName class using the new keyword and the class constructor (which will be discussed later).

# Attribute:

```Java
private dataType attributeName;
```
1. `private:` This is an access modifier, in this case, restricting access to the attribute within the class. Other access modifiers like public and protected are also available.
2. `dataType:` This specifies the data type of the attribute (e.g., int, String, double).
3. `attributeName:` This is your name for your attribute.

# Method:

```Java
public void methodName(dataType parameter) {
  // Method body containing statements
}
```
1. `public:` Similar to the class, this makes the method accessible from anywhere. Other access modifiers exist as well.
2. `void:` This specifies the method's return type. void means it doesn't return any value. Methods can also return other data types.
3. `methodName:` This is the name you choose for your method.
4. `dataType parameter:` This defines an optional parameter the method can receive. Methods can have multiple parameters with different data types.
5. `// Method body:` This is where you write the code the method executes when called.

# Example:

Let's model a new Tesla Model S car with a turn-on engine. 

```Java
public class Car {  // declare class name Car
  private String model;  // with a model Attribute
  
  public void startEngine() {  // And a Start Engine Method
    System.out.println("Engine started!");
  }
}

public class Main {  // Defines the entry point for the program. The execution starts.
  public static void main(String[] args) {  //
    Car myCar = new Car();  // Create object
    myCar.model = "Tesla Model S";  // Set attribute value
    myCar.startEngine();  // Call method
  }
}
```
# Static Methods

Static methods in Java are a special type of method that belongs to the class itself, rather than to an object of the class. This is useful when you want to call a method straight from the class without having to instantiate ( create) an object to do that. While static methods offer convenience, they can also lead to tight coupling between classes if overused. Favor non-static methods when dealing with object-specific data or behavior.

```java
public class MathUtils {

  public static int add(int a, int b) { // declare static method add
    return a + b;
  }

  public static double calculateArea(double radius) { //declare static method calculateArea
    return Math.PI * radius * radius;  // Accessing a static member of Math class
  }

  public static final double PI = 3.14159;  // Static final variable (constant)
}

public class Main {
  public static void main(String[] args) {
    int sum = MathUtils.add(5, 3);  // Calling static methods without object
    System.out.println("Sum: " + sum);
    
    double circleArea = MathUtils.calculateArea(10.0);
    System.out.println("Circle Area: " + circleArea);
  }
}
```

# Constructor Methods

The primary purpose of constructors is to initialize the object's attributes with starting values. Classes and objects start with some default values (0 for numbers, false for boolean, and null for objects). If you don't want the class or object initialized like this,  you use a constructor.

```java
public class Car {
  private String model;
  private int year;

  // Default constructor (no-arg)
  public Car() {
    // Assigning default values (optional)
    this.model = "Unknown";
    this.year = 2000;
  }

  // Parameterized constructor
  public Car(String model, int year) {
    this.model = model;
    this.year = year;
  }
}

public class Main {
  public static void main(String[] args) {
    // Using default constructor
    Car car1 = new Car();
    System.out.println("Car 1: Model - " + car1.model + ", Year - " + car1.year);

    // Using parameterized constructor
    Car car2 = new Car("Tesla Model S", 2023);
    System.out.println("Car 2: Model - " + car2.model + ", Year - " + car2.year);
  }
}
```
# Overloading Methods

Sometimes you need a method to behave slightly differently according to the number and data types of parameters. By overloading methods, you can provide methods with the same name but specific functionalities based on the arguments provided. This makes code easier to understand and reduces the need for multiple methods with slightly different purposes.

```java
public class Calculator {

  // Add two integers
  public int add(int a, int b) {
    return a + b;
  }

  // Add two doubles
  public double add(double a, double b) {
    return a + b;
  }

  // Add three integers (optional)
  public int add(int a, int b, int c) {
    return a + b + c;
  }
}

public class Main {
  public static void main(String[] args) {
    Calculator calc = new Calculator();
    int sumInt = calc.add(5, 3); // Calls the first add method (int, int)
    double sumDouble = calc.add(2.5, 1.7); // Calls the second add method (double, double)
    System.out.println("Integer sum: " + sumInt);
    System.out.println("Double sum: "  + sumDouble);
  }
}
```

# Overriding Methods

Subclasses can redefine inherited methods from their parent classes. By overriding methods, you can create more specialized classes that inherit core functionality from parent classes but customize specific behaviors.

```java
public class Animal {
  public void makeSound() {
    System.out.println("Generic animal sound");
  }
}

public class Dog extends Animal {
  @Override
  public void makeSound() {
    System.out.println("Woof!");
  }
}

public class Cat extends Animal {
  @Override
  public void makeSound() {
    System.out.println("Meow!");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal animal1 = new Animal();
    animal1.makeSound(); // Generic sound

    Animal animal2 = new Dog();  // Upcasting (treated as Animal at compile time)
    animal2.makeSound(); // Overridden sound (Woof!) due to polymorphism at runtime

    Cat cat = new Cat();
    cat.makeSound(); // Meow!
  }
}
```
# Decision Structures

 Allow your Java programs to make choices and execute different code blocks based on certain conditions.

## If Statement
```java

int age = 20;
if (age >= 18) {
  System.out.println("You are eligible to vote.");
}
```
## If Else 

```java
int number = 10;
if (number > 0) {
  System.out.println("The number is positive.");
} else {
  System.out.println("The number is non-positive.");
}
```
## If Else If Statement

```java
char grade = 'A';
if (grade == 'A') {
  System.out.println("Excellent!");
} else if (grade == 'B') {
  System.out.println("Well done!");
} else {
  System.out.println("Keep practicing!");
}
```
## Switch Statement

1. Used for multi-way branching based on the value of an expression.
2. Each `case` label checks for a specific value of the expression.
3. An optional `break` statement prevents fall-through to the next case.
4. A default `case` can handle situations where none of the other cases match.

```java
String day = "Monday";
switch (day) {
  case "Monday":
  case "Tuesday":
  case "Wednesday":
  case "Thursday":
  case "Friday":
    System.out.println("It's a weekday!");
    break;
  case "Saturday":
  case "Sunday":
    System.out.println("It's a weekend!");
    break;
}

```
# Conclussion
Learning OOP with Java equips you with a powerful and adaptable approach to software development, preparing you for success in a wide range of programming endeavors.

# Next
We will discuss more advanced topics such as operators, data types, and repetition structures. 









