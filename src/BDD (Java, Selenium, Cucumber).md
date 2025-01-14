![Image](images/young-adult-businessman-working-late-night-computer-technology-generated-by-artificial-intelligence.jpg)

# ForgeGuard
2 hours

# Objective
Create automated test cases using Selenium, Java, and Cucumber to verify the login page's functionality.
"https://practice.expandtesting.com/login"
These tests will:

- Test login with valid credentials.
- Test login with invalid credentials.
- Validate error messages for incorrect input.
- Verify successful redirection after a valid login.

# Table Of Contents
1. Step 01 Understanding Test Automation Workflow
2. Step 02 Environment Set Up
3. Step 03 IDE and Plugin Configuration Set Up
4. Step 04 Project Initialization Set Up
5. Step 05 Core Library Installation Set Up
6. Step 06 Basic Selenium Test Set up
7. Step 07 Basic Cucumber Set Up

# Step 01 Understanding Automation Workflow(Java, Selenium,Cucumber)
Imagine you're automating how someone interacts with a website—Java, Selenium, and Cucumber each play a unique role
in making this happen. Java is the programming language you use to write instructions for the automation. Selenium acts
as the "robot" that opens a browser, clicks buttons, fills out forms and verifies things on the webpage as per your
Java code. Cucumber lets you write those instructions in plain English (called feature files) using a style called
Behavior-Driven Development (BDD). 

For example, instead of writing complex code for `"login with valid credentials,"`
you can write it as `Given I am on the login page`, `When I enter valid credentials`, `Then I should see the dashboard`.
Cucumber links this plain English text to your Java code (called `step definitions`) that uses Selenium to perform the
actual actions in the browser. Together, they make testing clear, readable, and efficient!

- Here's a workflow diagram that illustrates the whole process.
```
  [Feature File (Cucumber)]
  ↓
  Plain English Scenarios (e.g., "Given I am on the login page")

  ↓
  [Cucumber Step Definitions (Java)]
  ↓
  Links scenarios to Java code (e.g., an actual method like navigateToLoginPage())

  ↓
  [Selenium WebDriver (Java)]
  ↓
  Automates browser actions (e.g., open the login page, fills forms, clicks buttons)

  ↓
  [Browser]
  ↓
  Executes the actions (e.g., logs in, verifies output)

  ↓
  [Test Results]
  ↓
  Reports success or failure of scenarios (e.g., "Login successful")
```
# Set Up
After understanding the stack workflow, it's time to set up all these technologies in our local environment.
The setup involves several moving parts and depending on experience can take between 1-15 days to complete. That is why
it's helpful to split it into steps such as:

1. Environment Set Up
2. IDE and Plugin Configuration Set Up
3. Project Initialization Set Up
4. Core Library Installation Set Up
5. Basic Selenium Test Set up
6. Basic Cucumber Set Up

# Step 01 Environment Set Up

Objective: Install and verify foundational tools.
Tasks:
- Install Java and ensure it’s properly configured with `java -version`. 
**Without this**: You won't be able to write or execute any Java code, as Java is the foundation of
  the entire project.
- Install the JDK and confirm its functionality `javac -version`.

- Install Maven and verify it `mvn -v`.
**Without this**: You’ll need to manually download and manage all dependencies (like Selenium, JUnit, and Cucumber)
which is time-consuming and error-prone.

> `POM` stands for `"Project Object Model"`. It is an XML representation of a Maven project held in a file named
> pom. xml. pom. It describes the project, configures plugins, and declares dependencies. 
> Check the pom.xml file in this project for reference. FYI Every time the `pom.xml` changes `mvn install` must be 
> executed to reinstall dependencies.

# Step 02 IDE and Plugin Configuration
Objective: Set up the development environment.
Tasks:
- Install IntelliJ IDEA or your preferred IDE.
**Without this**: You’ll lack a professional development environment to write, debug, and run your code efficiently,
  making development harder and slower.
- Add the Cucumber for Java Plugin to enable Gherkin and Cucumber support.

> Note: Intellij comes with Java and Maven installed, however, their system wise installation is needed to be
> able to execute mvn commands from the terminal.

- **Cucumber-java**:
**Without this**: Step definitions written in Java won’t be supported, breaking the connection between feature
files and the automation logic.
- Configure the project JDK in the IDE. This is automatically done by Intellij.

# Step 03 Project Initialization
Objective: Create and configure the project.
Tasks:
- Use Maven archetypes to create an empty cucumber project.
```pwsh
mvn archetype:generate `
  "-DarchetypeGroupId=io.cucumber" `
  "-DarchetypeArtifactId=cucumber-archetype" `
  "-DarchetypeVersion=7.20.1" `
  "-DgroupId=<project-name>" `
  "-DartifactId=<project-name>" `
  "-Dpackage=<project-name>" `
  "-Dversion=1.0.0-SNAPSHOT" `
  "-DinteractiveMode=false"
```
- Structure the project directories. After executing the commands above the project structure should look like the 
example below.
```
src/
├── main/
│   └── java/       # Application code (if applicable)
└── test/
└── java/
├── features/       # Cucumber feature files
│   └── login.feature
├── steps/          # Step definition files
│   └── LoginSteps.java
└── TestRunner.java # Test runner class
```
- Add dependencies to the pom.xml (e.g., Selenium, Cucumber, JUnit). Check this project `pom.xml` file for an example.
**Pom Dependencies**:
**Cucumber**:
**Without this**: You won’t be able to use Cucumber’s BDD framework, and feature files won’t work with step
definitions.

**JUnit**:
**Without this**: Your tests won’t execute, as JUnit is the test runner that integrates with Maven to run
Cucumber and Selenium tests.

**Selenium-java**:
**Without this**: Browser automation won’t work, as Selenium provides the essential tools to interact with web
pages.

**Pom Plugins**:
**Surefire**:
**Without this**: Maven won’t execute tests during the build process, and you’ll lose automated test running
capabilities.

**Maven Compiler**:
**Without this**: Your Java code won’t compile to the correct version, potentially causing runtime issues and
incompatibility with modern Java features.

# Step 04 Core Library Installation
Objective: Manage and download required libraries.
Tasks:
- Add and test the WebDriverManager dependency for browser driver setup.
**WebDriverManager**:
**Without this**: You’ll need to manually download and configure browser drivers like ChromeDriver, increasing
setup complexity and risking mismatched versions.
- Configure Cucumber and JUnit dependencies in the pom.xml.
**Cucumber-junit-platform-engine**:
**Without this**: You won’t be able to run Cucumber tests using JUnit 5, which is critical for modern test
execution.

**JUnit-platform-suite**:
**Without this**: Running multiple test engines (like JUnit and Cucumber) together won’t be possible, limiting
test execution flexibility.

**JUnit Jupiter**:
**Without this**: You’ll miss the benefits of JUnit 5 (like annotations and test execution) needed for modern,
efficient test writing.

- Verify all dependencies using Maven `mvn compile`.

# Step 05 Basic Selenium Test Setup
Objective: Write and execute initial tests to verify the setup.
Tasks:
- Create a simple Selenium test to open a browser and validate functionality. 
Inside the java directory a directory with the project name(not mandatory, it can have any name) should exist. This is 
the folder where the `BasicTest.java` will be created to test the setup work as expected.

```
<your-project-name>/
├── .idea/
├── <your-project-name>/
│   ├── src/
│   │   ├── test/
│   │   │   ├── java/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   ├── BasicTest.java

```
After the file is created paste the code below to test the setup is properly configured.
```
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.junit.jupiter.api.Test;

public class BasicTest {

    @Test
    public void testGooglePageTitle() {
        // WebDriver setup
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();

        // Open Google and print title
        driver.get("https://google.com");
        System.out.println("Page Title: " + driver.getTitle());

        // Quit browser
        driver.quit();
    }
}
```
To execute the `BasicTest.java` file the code below should be pasted in a new terminal.
```
mvn -Dtest=BasicTest test
```
The output should show something under the lines of "Build Success". It means Selenium work correctly.

# Step 06 Basic Cucumber Test Setup
- Add a sample Cucumber feature file and step definitions to validate Cucumber works properly.
Navigate to resources/<your-project-name>.
```
<your-project-name>/
├── .idea/
├── <your-project-name>/
│   ├── src/
│   │   ├── test/
│   │   │   ├── java/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   ├── BasicTest.java
│   │   │   │   │   ├── StepDefinitions.java
│   │   │   │   │   └── TestRunner.java
│   │   │   ├── resources/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   └── is_it_friday_yet.feature

```
Add the following scenario
```
Feature: Is it Friday yet?                 # Feature name
  Everybody wants to know when it's Friday # Description
@sunday                                    # Tags for indentifying scenarios. Multiple scenatios can exist in a file.
  Scenario: Sunday isn't Friday            # Scenario name to de able to identify it.
    Given today is Sunday                  # Steps that will be defined in the "Step Definition" file.
    When I ask whether it's Friday yet
    Then I should be told "Nope"
```
Then navigate to 
```
<your-project-name>/
├── .idea/
├── <your-project-name>/
│   ├── src/
│   │   ├── test/
│   │   │   ├── java/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   ├── BasicTest.java
│   │   │   │   │   ├── StepDefinitions.java
│   │   │   │   │   └── TestRunner.java
```
The following code adds the logic to test the previously created scenario.
```
package ForgeGuard;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static org.junit.jupiter.api.Assertions.*;

class IsItFriday {
    static String isItFriday(String today) {
        return "Nope";
    }
}

public class StepDefinitions {
    private String today;
    private String actualAnswer;

    @Given("today is Sunday")
    public void today_is_Sunday() {
        today = "Sunday";
    }

    @When("I ask whether it's Friday yet")
    public void i_ask_whether_it_s_Friday_yet() {
        actualAnswer = IsItFriday.isItFriday(today);
    }

    @Then("I should be told {string}")
    public void i_should_be_told(String expectedAnswer) {
        assertEquals(expectedAnswer, actualAnswer);
    }
}
```
To execute the test there are several choices:
1. Run scenarios by name:
```
mvn test -Dcucumber.filter.name="Sunday isn't Friday"
```
2. Run all scenarios in a file:
```
mvn test -Dcucumber.features=src/test/resources/ForgeGuard/is_it_friday_yet.feature
```
3. Run scenarios by tag:
```
mvn test -Dcucumber.filter.tags="@WeekendCheck"
```

# Congratulations! Set Up Completed
Now, the setup is completed and is time start testing.


# Step 07 Automation Logic: Selenium
Selenium is widely for automation logic because it is a robust, versatile, and open-source tool that supports c
ross-browser testing, automation of web applications, and integration with various programming languages and testing 
frameworks. while Selenium is versatile and widely used, you can absolutely use other languages, frameworks, or 
libraries in your step definitions depending on your project requirements and the type of testing you want to perform.

## Understanding Selenium
Selenium is an open source project dedicated to browser automation with several products under its brand, however for 
web browser testing purposes the product used is Selenium WebDriver.

## Selenium Web driver
- Definition: WebDriver is a `high-level Selenium API` that provides a programming interface to interact with web 
- browsers.
- Role: It defines how commands are sent to the browser and manages the communication between your test scripts and the 
- browser-specific driver.



## **1. Browser Specific Drivers**
- Refers to the browser-specific executables (e.g., `ChromeDriver`, `GeckoDriver`) that Selenium uses to communicate
- with web browsers.
- **Purpose**: Translates WebDriver commands into actions the browser can execute.

## Driver Components
1. Options: Define browser-specific configurations.
2. HTTP Client: Facilitates communication between Selenium and the browser driver.
3. Service: Starts/stops the browser driver executable.
4. Remote WebDriver: Sends commands to a remote WebDriver server.

## **3. Waits**
- Mechanisms to synchronize test execution with the application's state.
- **Types**:
    - **Implicit Waits**: Wait for a specific duration before throwing an error.
    - **Explicit Waits**: Wait for a specific condition (e.g., element visibility) to be met.
    - **Fluent Waits**: Poll for a condition at regular intervals with a timeout.

## **4. Elements**
- Refers to the web elements (e.g., buttons, input fields, links) on a webpage that Selenium interacts with.
- **Purpose**: Elements are located using locators such as ID, XPath, CSS Selector, etc.
- Example: `driver.findElement(By.id("username"));`

## 4.1 Element Components
Elements are critical because they enable Selenium to replicate user actions, validate UI behavior, and ensure the web
application works as intended. Without elements, automation would be infeasible.

## **4.2. File Upload**
- Refers to the automation of file upload functionality on web pages.
- **How it works**: Selenium interacts with `<input type="file">` elements by sending the file path directly.
- **Example**:
```java
  WebElement uploadElement = driver.findElement(By.id("fileUpload"));
  uploadElement.sendKeys("C:\\path\\to\\file.txt");
```

---

## **4.3 Locators**
- These are methods used to identify and locate web elements on a webpage.
- **Common Locators**:
    - **ID**: Locate by element ID.
    - **Name**: Locate by element name.
    - **XPath**: Flexible but slower, allows precise identification.
    - **CSS Selector**: Fast and powerful for locating elements by style rules.
    - **Class Name**, **Tag Name**, **Link Text**, **Partial Link Text**.
- **Example**:
  ```java
  WebElement element = driver.findElement(By.cssSelector(".className"));
  ```

---

## **4.4 Finders**
- These are the Selenium methods that use locators to retrieve web elements.
- **Common Methods**:
    - `findElement`: Finds a single element.
    - `findElements`: Finds multiple elements that match the locator.
- **Example**:
```java
  WebElement element = driver.findElement(By.id("username"));
  List<WebElement> elements = driver.findElements(By.className("items"));
 ```

---

### **4.5 Element Interactions**
- Refers to actions performed on elements, such as:
    - Clicking (`click()`)
    - Typing (`sendKeys()`)
    - Clearing input fields (`clear()`)
    - Submitting forms (`submit()`)
- **Example**:
- 
```java
  WebElement inputField = driver.findElement(By.name("search"));
  inputField.sendKeys("Selenium");
  inputField.submit();
```

---

### **5. Information**
- Deals with retrieving information about elements, such as:
    - Text content (`getText()`)
    - Attributes (`getAttribute()`)
    - Tag name (`getTagName()`)
    - Displayed status (`isDisplayed()`)
- **Example**:
```java
String buttonText = driver.findElement(By.id("submitButton")).getText();
boolean isEnabled = driver.findElement(By.id("submitButton")).isEnabled();
```

## **6. Browser Interactions**
- Actions that Selenium can perform on web elements, such as clicking, typing, dragging, and dropping.
- **Purpose**: Simulates user behavior for testing purposes.

## Most Important Interactions
Interactions are important in Selenium because they enable the automation of real-world user actions, making it 
possible to simulate, test, and validate the behavior of web applications as end-users would interact with them. 
Below are the most common ones.

## **6.1 Navigation**
- Refers to controlling the browser’s navigation actions, such as opening URLs, refreshing pages, and moving forward 
- or backward in the browser history.
- **Common Methods**:
    - `driver.get(url)`: Navigate to a URL.
    - `driver.navigate().back()`: Go back in history.
    - `driver.navigate().forward()`: Go forward in history.
    - `driver.navigate().refresh()`: Refresh the current page.


## **6.2 Alerts**
- Handles JavaScript alerts, confirmations, or prompts displayed on a web page.
- **Common Methods**:
    - `switchTo().alert().accept()`: Accepts the alert.
    - `switchTo().alert().dismiss()`: Dismisses the alert.
    - `switchTo().alert().getText()`: Retrieves the text of the alert.
    - `switchTo().alert().sendKeys("text")`: Sends input to a prompt alert.

## **6.4 Cookies**
- Refers to managing browser cookies, which are small data pieces stored by websites.
- **Common Use Cases**:
    - Add cookies.
    - Retrieve cookies.
    - Delete cookies.
- **Example**:
```java
driver.manage().addCookie(new Cookie("key", "value"));
Cookie cookie = driver.manage().getCookieNamed("key");
driver.manage().deleteCookie(cookie);
```

## **6.5 Windows**
- Refers to managing multiple browser windows or tabs.
- **Common Methods**:
    - `driver.getWindowHandles()`: Retrieve all open windows/tabs.
    - `driver.switchTo().window(handle)`: Switch to a specific window/tab.
    - `driver.close()`: Close the current window.
- **Use Case**: Automating workflows involving pop-ups or multi-tab scenarios.


## **6. Actions API**
- Provides advanced interactions like:
    - Hovering over elements.
    - Clicking and holding.
    - Dragging and dropping.
    - Simulating keyboard shortcuts.
- **Purpose**: Enables complex user interactions beyond simple clicks and typing.
- Example:
  ```java
  Actions actions = new Actions(driver);
  actions.moveToElement(element).click().perform();
  ```

## Selenium Script: 8 Components
When using selenium for web automation there are always 8 basic components involved:

1. Start Session: Initialize the WebDriver
`(e.g., driver = new Builder().forBrowser('chrome').build();)`.
2. Take Action on Browser: Perform browser-level actions like navigating to a URL
`(e.g., driver.get('http://example.com');)`.
3. Request Browser Information: Retrieve details like page title, URL, or cookies 
`(e.g., driver.getTitle())`.
4. Establish Waiting Strategy: Wait for elements to load or be interactable using explicit waits
`(e.g., driver.wait(until.elementLocated(locator), 5000);)`.
5. Find an Element: Locate elements on the page with locators like ID, CSS, or XPath 
`(e.g., driver.findElement(By.css('.button'));)`.
6. Take Action on Element: Interact with elements by clicking, typing, or selecting
`(e.g., element.click())`.
7. Request Element Information: Extract details like text or attributes from elements
`(e.g., element.getText())`.
8. End the Session: Close the browser and clean up resources
`(e.g., driver.quit();)`.
