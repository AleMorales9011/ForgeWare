# ForgeGuard - Functionality Testing - Login
Estimated Time: 2 hours<br>
Tech Stack: Selenium - Java - Cucumber<br>
Keywords: Automation - Testing - QA - BDD<br>
Experience Level: Beginner - Advanced

# Why Web Testing
The main use case for `Web Browser Automation` is `regression testing`. Most companies today's have websites, and they 
deploy new code every day. This new code is destined to correct issues or add new functionalities. The problem is that
often times this new code mess up things that were already functioning correctly. 

`Regression testing` notifies that this not happen by verifying all the applications previous functionalities before new
code is deployed.

# Objective
Create automated test cases using `Selenium`, `Java`, and `Cucumber` to verify the login page's functionality of
"https://practice.expandtesting.com/login". Login is arguably the most used and common functionality of all web 
applications. By mastering this functionality one can ensure `~80%` of the required knowledge to perform this activity.

These tests will:

- Test login with valid credentials.
- Test login with invalid credentials.
- Validate error messages for incorrect input.
- Verify successful redirection after a valid login.

## Encouragement
Progress in automation testing requires persistence, and each effort lays a solid foundation for future success.

# Table Of Contents

1.  Functionality Testing 
2.  Step 01 Understanding Automation Workflow(Java, Selenium,Cucumber)
3.  Step 02 Environment Set Up
4.  Step 03 IDE and Plugin Configuration Set Up
5.  Step 04 Project Initialization Set Up
6.  Step 05 Core Library Installation Set Up
7.  Step 06 Basic Selenium Test Set up
8.  Step 07 Basic Cucumber Set Up
9.  Step 08 Understand Automation Logic: Selenium
10. Step 09 Scripting
11. Conclusion


# Functionality Testing
Functionality testing is the first step of the automation journey as it is the main objective of testing in general to
verify that a software application performs as intended, meeting all specified functionalities and user requirements, 
ensuring the delivered product is reliable and free from major defects by identifying and fixing issues early in the 
development cycle.

# Step 01 Understanding Automation Workflow(Java, Selenium,Cucumber)

When automating how someone interacts with a `website—Java`, `Selenium`, and `Cucumber` each play a unique role
in making this happen. 

- Java is the programming language you use to write instructions for the automation. 
- Selenium acts as the "robot" that opens a browser, clicks buttons, fills out forms and verifies things on the webpage
as per your Java code. 
- Cucumber lets you write those instructions in plain English (called feature files) using a style called
`Behavior-Driven Development (BDD)`.

Instead of writing complex code for `"login with valid credentials,"`
it can be written as `Given I am on the login page`, `When I enter valid credentials`,
`Then I should see the dashboard`. Cucumber links this plain English text to your Java code
(called `step definitions`) that uses Selenium to perform the actual actions in the browser. 
Together, they make testing clear, readable, and efficient.

# Set Up

After understanding the stack workflow, it's time to set up all these technologies in the local environment.
The setup involves several moving parts and depending on experience can take between 1-15 days to complete. That is why
it's helpful to split it into steps such as:

1. Environment Setup
2. IDE and Plugin Configuration SetUp
3. Project Initialization SetUp
4. Core Library Installation Setup
5. Basic Selenium Test Setup
6. Basic Cucumber SetUp

# Step 02 Environment Setup

Objective: Install and verify foundational tools.
Tasks:

- Install `Java` and ensure it’s properly configured with `java -version`.
  **Without this**: You won't be able to write or execute any Java code, as Java is the foundation of
  the entire project.

- Install the `JDK` and confirm its functionality `javac -version`.

- Install `Maven` and verify it `mvn -v`.
  **Without this**: You’ll need to manually download and manage all dependencies (like Selenium, JUnit, and Cucumber)
  which is time-consuming and error-prone.


# Step 03 IDE and Plugin Configuration

Objective: Set up the development environment.
Tasks:

- Install `IntelliJ IDEA` or your preferred IDE.
  **Without this**: You’ll lack a professional development environment to write, debug, and run your code efficiently,
  making development harder and slower.

> Note: Intellij comes with Java and Maven installed, however, their system-wise installation is needed to be
> able to execute mvn commands from the terminal.

- Add the `Cucumber for Java` Plugin to enable `Gherkin` and Cucumber support.
- **Cucumber-java**:
  **Without this**: Step definitions written in Java won’t be supported, breaking the connection between feature
  files and the automation logic.
- Configure the project JDK in the IDE. IntelliJ automatically does this.

# Step 04 Project Initialization

Objective: Create and configure the project.
Tasks:

- Use plain `Maven project builder` or `Maven archetypes` to create an empty cucumber project. The code below can be
used to create a ``cucumber project archetype`` from a `pwsh` terminal.

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

# Step 04.01 Project Structure 
Structure the project directories correctly is crucial for it to work. After executing the commands above the project
structure should look like the example below. This structure is mandatory for it to work properly.
```
src
├── main
│   └── java
│       └── <Project-Name>
│           └── [Production code files]
├── test
    ├── java
    │   └── <Project-Name>
    │       └── RunCucumberTest.java
    │       └── [Step definitions here]
    ├── resources
        └── <Project-Name>
            └── [Feature files]

```

# Step 05 Dependencies Set Up
The test automation environment contains several moving parts. To function properly all those moving parts needs to be
declared in the `POM.xml`file (backbone of the Automation Testing Project) for maven to build the project properly.

# Step 05.01 POM File Template
Using the `mvn archetype` above installs `cucumber dependencies` but not `Selenium dependencies` nor the Web driver
(controls the browser) or other plugins required. Failing to have all required dependencies and proper configurations
means the project will face issues. Here's a pom file template it can be used to avoid misconfigurations.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- This is a Maven POM file template for a Selenium + Cucumber test automation project -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion> <!-- Version of the POM model -->

    <!-- General project information -->
    <groupId>org.example</groupId> <!-- A unique ID for your project, usually your organization's domain in reverse -->
    <artifactId>test-automation-template</artifactId> <!-- The name of the project -->
    <version>1.0-SNAPSHOT</version> <!-- The current version of the project -->

    <properties>
        <!-- Java version for compiling the project -->
        <maven.compiler.source>17</maven.compiler.source> <!-- Java version for source code -->
        <maven.compiler.target>17</maven.compiler.target> <!-- Java version for compiled classes -->
        <project.build.sourceEncoding>UTF-8
        </project.build.sourceEncoding> <!-- Encoding to handle special characters -->

        <!-- Versions for external dependencies -->
        <cucumber.version>7.20.0</cucumber.version> <!-- Cucumber version -->
        <selenium.version>4.11.0</selenium.version> <!-- Selenium version -->
        <webdriver.version>5.5.3</webdriver.version> <!-- WebDriverManager version -->
        <junit.version>5.11.0</junit.version> <!-- JUnit version -->
    </properties>

    <!-- Project dependencies -->
    <dependencies>
        <!-- JUnit is used as the testing framework -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>${junit.version}</version> <!-- Use the JUnit version defined in properties -->
            <scope>test</scope> <!-- Indicates this dependency is only needed for tests -->
        </dependency>
        <dependency>
            <groupId>org.junit.platform</groupId>
            <artifactId>junit-platform-suite-api</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>

        <!-- Cucumber dependencies for Behavior-Driven Development (BDD) -->
        <dependency>
            <groupId>io.cucumber</groupId>
            <artifactId>cucumber-java</artifactId>
            <version>${cucumber.version}</version> <!-- Cucumber library for writing step definitions -->
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.cucumber</groupId>
            <artifactId>cucumber-junit-platform-engine</artifactId>
            <version>${cucumber.version}</version> <!-- Integrates Cucumber with JUnit -->
            <scope>test</scope>
        </dependency>

        <!-- Selenium dependencies for browser automation -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>${selenium.version}</version> <!-- Selenium Java binding -->
        </dependency>

        <!-- WebDriverManager for automatically managing browser drivers -->
        <dependency>
            <groupId>io.github.bonigarcia</groupId>
            <artifactId>webdrivermanager</artifactId>
            <version>${webdriver.version}</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Maven Compiler Plugin for Java compilation -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version> <!-- Plugin version -->
                <configuration>
                    <release>17</release> <!-- Java version for compiling -->
                </configuration>
            </plugin>

            <!-- Maven Surefire Plugin for executing tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M7</version> <!-- Plugin version -->
                <configuration>
                    <includes>
                        <include>**/*.java</include> <!-- Include all Java files in the test folder -->
                    </includes>
                    <systemPropertyVariables>
                        <!-- Pass configuration to Cucumber -->
                        <cucumber.features>src/test/resources</cucumber.features> <!-- Path to feature files -->
                        <cucumber.glue>your.step.definition.package</cucumber.glue> <!-- Step definitions package -->
                        <cucumber.plugin>pretty, json:target/cucumber.json</cucumber.plugin> <!-- Report plugins -->
                    </systemPropertyVariables>
                </configuration>
            </plugin>

            <!-- Maven Failsafe Plugin for integration tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-failsafe-plugin</artifactId>
                <version>3.0.0-M7</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>integration-test</goal> <!-- Runs integration tests -->
                            <goal>verify</goal> <!-- Verifies test results -->
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>

```
# Step 05.02 Runner Class Template
The final component of the set-up is the `runner class` which is in charge to tell junit where the feature files and 
`step definitions` are. It is also used to pass customized test execution configurations.

```bash
C:\04ForgeGuard\ForgeGuard\src\test\java\ForgeGuard\RunCucumberTest.java
```

```java
package ForgeGuard;

import org.junit.platform.suite.api.ConfigurationParameter;
import org.junit.platform.suite.api.IncludeEngines;
import org.junit.platform.suite.api.SelectDirectories;
import org.junit.platform.suite.api.Suite;

import static io.cucumber.junit.platform.engine.Constants.*;

@Suite
@IncludeEngines("cucumber") // Use the Cucumber engine
@SelectDirectories("src/test/resources/ForgeGuard") // Path to your feature files
@ConfigurationParameter(key = GLUE_PROPERTY_NAME, value = "ForgeGuard") // Package containing step definitions
@ConfigurationParameter(key = PLUGIN_PROPERTY_NAME, value = "pretty, json:target/cucumber.json") // Plugins
public class RunCucumberTest {
}
```
## Encouragement
Every project milestone brings a sense of achievement, and even challenges contribute to stronger skills and deeper
understanding.


# Step 06 Basic Selenium Test Setup
Once the project structure is set up, the pom file is correct and the runner class is implemented, it's time to test the
set-up to verify everything runs smoothly.

Objective: Write and execute initial tests to verify the setup.
Tasks:

- Create a simple `Selenium` test to open a browser and validate functionality.
  Inside the java directory, a directory with the project name(not mandatory, it can have any name) should exist. This
  is the folder where the `BasicTest.java` will be created to test the setup work as expected.

```bash
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

```java
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

```bash
mvn test -Dtest=DatabaseTest
```
> Note: For some reason mvn commands don't work sometimes in `pwsh` terminals make sure you use bash instead.

# Step 07 Basic Cucumber Test Setup
If the test above runs properly it means selenium works properly. Now it's time to test if cucumber works properly too.
Add a sample Cucumber feature file and step definitions to validate that Cucumber works properly.

Objective: Write and execute initial tests to verify the setup.
Tasks:
- Navigate to resources/<your-project-name>.

```bash
<your-project-name>/
├── .idea/
├── <your-project-name>/
│   ├── src/
│   │   ├── test/
│   │   │   ├── java/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   ├── BasicTest.java
│   │   │   │   │   ├── ForgeGuard.StepDefinitions.java
│   │   │   │   │   └── TestRunner.java
│   │   │   ├── resources/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   └── is_it_friday_yet.feature

```

Add the following scenario

```gherkin
# Feature name
Feature: Is it Friday yet?
# Description
  Everybody wants to know when it's Friday 
# Tags for identifying scenarios. Multiple scenarios can exist in a file.
  @WeekendCheck                                    
# Scenario name to be able to identify it.
  Scenario: Sunday isn't Friday 
# Steps that will be defined in the "Step Definition" file.
    Given today is Sunday                  
    When I ask whether it's Friday yet
    Then I should be told "Nope"
```

Then navigate to

```bash
<your-project-name>/
├── .idea/
├── <your-project-name>/
│   ├── src/
│   │   ├── test/
│   │   │   ├── java/
│   │   │   │   ├── <your-project-name>/
│   │   │   │   │   ├── BasicTest.java
│   │   │   │   │   ├── ForgeGuard.StepDefinitions.java
│   │   │   │   │   └── TestRunner.java
```

The following code adds the logic to test the previously created scenario.

```java
package ForgeGuard;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static org.junit.jupiter.api.Assertions.*;

class ForgeGuard.IsItFriday {
    static String isItFriday(String today) {
        return "Nope";
    }
}

public class ForgeGuard.StepDefinitions {
    private String today;
    private String actualAnswer;

    @Given("today is Sunday")
    public void today_is_Sunday() {
        today = "Sunday";
    }

    @When("I ask whether it's Friday yet")
    public void i_ask_whether_it_s_Friday_yet() {
        actualAnswer = ForgeGuard.IsItFriday.isItFriday(today);
    }

    @Then("I should be told {string}")
    public void i_should_be_told(String expectedAnswer) {
        assertEquals(expectedAnswer, actualAnswer);
    }
}
```
# Step 07.01 Basic Cucumber Test Setup: Execution
To execute the test there are several choices:
- Run scenarios by name:
```bash
mvn test -Dcucumber.filter.name="Sunday isn't Friday"
```
- Run all scenarios in a file:
```bash
mvn test -Dcucumber.features=src/test/resources/ForgeGuard/is_it_friday_yet.feature
```
- Run scenarios by tag:
```bash
mvn test -Dcucumber.filter.tags="@WeekendCheck"
```
- Re-install dependencies and compiling test code without executing tests.
```bash
mvn clean install -DskipTests
```
- Re-install dependencies without compiling and executing test code
```bash
mvn clean install -Dmaven.test.skip=true
```
# Congratulations! Set Up Completed
Now, the setup is completed and is time start testing. You're doing a `fantastic job!` Every new test you write is 
another step toward mastering automation testing. Keep building momentum—you’ve got this! 😊

# Step 08 Understand Automation Logic: Selenium
Before writing automated test a basic understanding of `Selenium` is needed. Selenium is an open source project
dedicated to `browser automation` with several products under its brand, however for web browser testing purposes the
product used is `Selenium WebDriver`.

# Selenium Web driver

- Definition: `WebDriver` is a `high-level Selenium API` that provides a programming interface to interact with web
- browsers.
- Role: It defines how commands are sent to the browser and manages the communication between your test scripts and the
- browser-specific driver.

# WebDriver Core 06 Components

The `WebDriver` is composed by 6 core components, and several subcomponents. They are the building blocks Selenium uses
to interact with the browser, and therefore they are also the building blocks of the `stepdefinitions` file needed for 
automation testing.

#### **01 Drivers**
- `Options`: Configures browser options like headless mode or window size.
- `Http Client`: Handles HTTP requests between Selenium and the browser driver.
- `Service`: Manages driver lifecycle (start, stop, port configuration).
- `Remote Web Driver`: Enables testing on remote browsers or cloud grids.

---

#### **02 Browsers**
- `Chrome`: Automates Google Chrome browser actions and interactions.
- `Firefox`: Automates Mozilla Firefox browser actions and interactions.
- `Edge`: Automates Microsoft Edge browser actions and interactions.

---

#### **03 Waits**
- `Implicit`: Global wait for element presence across all interactions.
- `Explicit`: Waits for specific conditions like visibility or click-ability.
- `Custom`: User-defined waits for unique or complex conditions.

---

#### **04 Elements**
- `4.1 Uploads`: Handles file input fields for uploading files.

**4.2 Locators** (Find elements based on attributes):
- `class`: Finds elements by `class` attribute.
- `css`: Uses CSS selectors for locating elements.
- `id`: Finds elements by unique `id` attribute.
- `name`: Finds elements by `name` attribute.
- `link text`: Finds links by exact visible text.
- `partial link text`: Finds links by partial visible text.
- `tag name`: Finds elements by HTML tag name.
- `xpath`: Uses XPath expressions to locate elements.

**4.3 Finders**: Locate elements on the page using locators.

**4.4 Interactions**:
- `Click`: Clicks a web element.
- `Send Keys`: Inputs text into fields.
- `Clear`: Clears input fields or text areas.
- `Submit`: Submits forms programmatically.
- `Select`: Selects dropdown options.

**4.5 Information**:
- `Is displayed`: Checks if an element is visible.
- `Is enabled`: Checks if an element is interactable.
- `Is selected`: Checks if an element is selected (e.g., checkbox).
- `Tag name`: Gets the HTML tag of an element.
- `Size and position`: Retrieves element size and screen position.
- `Get CSS Value`: Gets computed CSS property values of elements.
- `Text Content`: Fetches visible text from elements.
- `Fetch Properties/Attributes`: Retrieves attributes or DOM properties.

---

#### **05 Interactions**
- `Navigation`: Performs URL navigation (back, forward, refresh, etc.).
- `Alerts`: Handles JavaScript alerts and confirmation popups.
- `Cookies`: Manages cookies for sessions and authentication.
- `Frames`: Switches to or interacts with iframe content.
- `Print Pages`: Prints page to PDF or retrieves print content.
- `Windows`: Manages multiple browser windows or tabs.
- `Virtual Authenticator`: Tests WebAuthy functionality programmatically.

---

#### **06 Actions**
- `Keyboard`: Simulates keyboard inputs like typing or key combinations.
- `Mouse`: Simulates mouse actions like hover, drag, and drop.
- `Pen`: Simulates pen input for touch devices.

---

## Encouragement
The journey of learning and improvement is always worthwhile, and small steps lead to remarkable outcomes.

# Selenium Script: 8 Components

When writing a selenium script for web automation there are always 8 basic components involved. Mastering those
guarantees a step-by-step process that can be followed for writing the `stepdefinitions` file.

1. `Start Session`:              Initialize the WebDriver
2. `Take Action`:                Perform browser-level actions like navigating to a URL
3. `Request Information`:        Retrieve details like page title, URL, or cookies
4. `Waiting Strategy`:           Wait for elements to load or be interactable using explicit waits
5. `Find Element`:               Locate elements on the page with locators like ID, CSS, or XPath
6. `Interact`:                   Interact with elements by clicking, typing, or selecting
7. `Request Information`:        Extract details like text or attributes from elements
8. `End Session`:                Close the browser and clean up resources

# Step 09 Scripting
Understanding Selenium WebDriver 6 components and Selenium's script 8 components are the first steps to master
web-browser automation scripting. The next step is to write the first script. The objective of this project is to
create automated test cases using `Selenium`, `Java`, and `Cucumber` to verify the login page's functionality of
"https://practice.expandtesting.com/login".

These tests will:

- Test login with valid credentials.
- Test login with invalid credentials.
- Validate error messages for incorrect input.
- Verify successful redirection after a valid login.

# Step 09.01 Feature File
After the 6 steps from the set-up are complete to automate the tests above the first step is to write the feature file.
This file will describe all the steps to execute the test in `Gherkin` language which is very similar to plain English.

```gherkin
Feature: Login Functionality
  As a user
  I want to be able to login with valid credentials
  So that I can access the application
@valid-login
  Scenario: Valid Login
  Given I am in the login page
  When I enter the valid credentials "practice" and "SuperSecretPassword!"
  Then I should be redirected to the secure page
  And I should see a welcome message "Secure Area page for Automation Testing Practice"

@invalid-login
  Scenario: Invalid Login
  Given I am in the login page
  When I enter the invalid credentials "2" and "2"
  Then I should see an error message "Your username is invalid!"
```
# Step 09.02 StepDefinitions
The step definition file is the place where the automation instructions are written using Selenium's WebDriver and Scrip
components.

```java
package ForgeGuard;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;


import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class ValidLogin {  // Declares the main class. This is the file name that encapsulates all data and methods.
    WebDriver driver;      // Declares a WebDriver variable provided by Selenium to control the browser.
    WebDriverWait wait;    // Declares WebDriverWait instance from Selenium to implement explicit waits.

    @Given("I am in the login page")        // Cucumber annotation that links step definition with feature file.
    public void i_am_on_the_login_page() {  // Defines a method that implements the behaviour of the step.
        WebDriverManager.chromedriver().setup(); // Call the WebDriverManager library to set up the Chrome-driver.
        ChromeOptions options = new ChromeOptions(); // Object  of ChromeOptions class that customize driver behaviour.
        options.addArguments("--headless", "--disable-gpu", "--window-size=1920,1080"); // Pass arguments.
        driver = new ChromeDriver(options); // Initializes the driver object as a new class of ChromeDriver.

        driver.get("https://practice.expandtesting.com/login"); // Get method of the WebDriver

        wait = new WebDriverWait(driver, Duration.ofSeconds(10)); // Initializes the wait object.
    }

    @When("I enter the valid credentials {string} and {string}")
    public void i_enter_the_valid_credentials(String username, String password) {
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//*[@id=\"username\"]")));
        WebElement passwordField = driver.findElement(By.xpath("//*[@id=\"password\"]"));
        WebElement loginButton = driver.findElement(By.xpath("//*[@id=\"login\"]/button"));
            usernameField.sendKeys(username);
            passwordField.sendKeys(password);
            loginButton.click();
    }

    @Then("I should be redirected to the secure page")
    public void i_should_be_redirected_to_the_secure_page(){
        String currentUrl = wait.until(ExpectedConditions.urlContains("secure")) ? driver.getCurrentUrl() :"";
        assertTrue(currentUrl.contains("secure"), "The user is not redirected to the secure page.");

    }

    @Then("I should see a welcome message {string}")
    public void i_should_see_a_welcome_message(String expectedMessage){
        WebElement welcomeMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("/html/body/main/div[4]/div/h1")));
        assertTrue(welcomeMessage.isDisplayed(),"Welcome message is not displayed");
        assertEquals(expectedMessage, welcomeMessage.getText(), "The message does not match");

        driver.quit();
    }

    @When("I enter the invalid credentials {string} and {string}")
    public void i_enter_the_invalid_credentials(String username, String password){
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//*[@id=\"username\"]")));
        WebElement passwordField = driver.findElement(By.xpath("//*[@id=\"password\"]"));
        WebElement loginButton = driver.findElement(By.xpath("//*[@id=\"login\"]/button"));
        usernameField.sendKeys(username);
        passwordField.sendKeys(password);
        loginButton.click();
    }

    @Then("I should see an error message {string}")
    public void i_should_see_an_error_message(String expectedMessage){
        WebElement errorMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("flash")));
        assertTrue(errorMessage.isDisplayed(),"Error message is not displayed");
        assertEquals(expectedMessage, errorMessage.getText(),"Text does not match");

        driver.quit();
    }
}



```

# Congratulations - Functionality Test Completed!🚀✨
You're making steady progress toward building a robust test automation framework! Every refinement you make brings you 
closer to a more polished and professional setup. Stay focused, and don't forget to celebrate your wins—no 
matter how small! 🚀✨ Keep up the great momentum! This project is a great first step, and every effort is bringing
it closer to excellence!🚀 Next step is to add database interactions to functionality tests. 


