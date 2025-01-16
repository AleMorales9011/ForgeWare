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
1. Step 01 Understanding Automation Workflow(Java, Selenium,Cucumber)
2. Step 02 Environment Set Up
3. Step 03 IDE and Plugin Configuration Set Up
4. Step 04 Project Initialization Set Up
5. Step 05 Core Library Installation Set Up
6. Step 06 Basic Selenium Test Set up
7. Step 07 Basic Cucumber Set Up
8. Step 08 Understand Automation Logic: Selenium

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
  Automates browser actions (e.g., opening the login page, filling forms, clicking buttons)

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

1. Environment Setup
2. IDE and Plugin Configuration SetUp
3. Project Initialization SetUp
4. Core Library Installation Setup
5. Basic Selenium Test Setup
6. Basic Cucumber SetUp

# Step 02 Environment Setup

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

# Step 03 IDE and Plugin Configuration
Objective: Set up the development environment.
Tasks:
- Install IntelliJ IDEA or your preferred IDE.
**Without this**: You’ll lack a professional development environment to write, debug, and run your code efficiently,
  making development harder and slower.
- Add the Cucumber for Java Plugin to enable Gherkin and Cucumber support.

> Note: Intellij comes with Java and Maven installed, however, their system-wise installation is needed to be
> able to execute mvn commands from the terminal.

- **Cucumber-java**:
**Without this**: Step definitions written in Java won’t be supported, breaking the connection between feature
files and the automation logic.
- Configure the project JDK in the IDE. IntelliJ automatically does this.

# Step 04 Project Initialization
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

# Step 05 Core Library Installation
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

# Step 06 Basic Selenium Test Setup
Objective: Write and execute initial tests to verify the setup.
Tasks:
- Create a simple Selenium test to open a browser and validate functionality. 
Inside the java directory, a directory with the project name(not mandatory, it can have any name) should exist. This is 
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
The output should show something under the lines of "Build Success". It means Selenium works correctly.

# Step 07 Basic Cucumber Test Setup
- Add a sample Cucumber feature file and step definitions to validate that Cucumber works properly.
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
@sunday                                    # Tags for identifying scenarios. Multiple scenarios can exist in a file.
  Scenario: Sunday isn't Friday            # Scenario name to be able to identify it.
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
- Run scenarios by name:
```
mvn test -Dcucumber.filter.name="Sunday isn't Friday"
```
- Run all scenarios in a file:
```
mvn test -Dcucumber.features=src/test/resources/ForgeGuard/is_it_friday_yet.feature
```
- Run scenarios by tag:
```
mvn test -Dcucumber.filter.tags="@WeekendCheck"
```

# Congratulations! Set Up Completed
Now, the setup is completed and is time start testing.


# Step 08 Understand Automation Logic: Selenium
Selenium is an open source project dedicated to browser automation with several products under its brand, however for 
web browser testing purposes the product used is Selenium WebDriver.

# Selenium Web driver
- Definition: WebDriver is a `high-level Selenium API` that provides a programming interface to interact with web 
- browsers.
- Role: It defines how commands are sent to the browser and manages the communication between your test scripts and the 
- browser-specific driver.

# WebDriver Core 9 Components
The WebDriver is composed by 6 core components, and several subcomponents. They are the building blocks Selenium uses
to interact with the browser, and therefore they are also the building blocks of the `stepdefinitions` file.

- 01 Drivers
  - Options
  - Http client
  - Service
  - Remote web driver
  
- 02 Browsers
  - Chrome
  - Firefox
  - Edge
  
- 03 Waits
  - Implicit
  - Explicit
  - Custom
  
- 04 Elements
  - 4.1 Uploads
  - 4.2 Locators
    - class
    - css
    - id
    - name
    - link text
    - partial link text
    - tag name
    - xpath
  - 4.3 Finders
  - 4.4 Interactions
    - Click
    - Send Keys
    - Clear
    - Submit
    - Select
  - 4.5 Information
    - Is displayed
    - Is enabled
    - Is selected
    - Tag name
    - Size and position
    - Get CSS Value
    - Text Context
    - Fetch Properties or attributes
  
- 05 Interactions
  - Navigation
  - Alerts
  - Cookies
  - Frames
  - Print Pages
  - Windows
  - Virtual Authenticator
  
- 06 Actions
  - Keyboard
  - Mouse
  - Pen


# Selenium Script: 8 Components
When writing a selenium script for web automation there are always 8 basic components involved. Mastering those
guarantees a step-by-step process that can be followed for writing the `stepdefinitions` file. 

1. Start Session:              Initialize the WebDriver
   - WebDriver driver = new ChromeDriver();
2. Take Action:                Perform browser-level actions like navigating to a URL
   - driver.get("www.examples.com");
3. Request Information:        Retrieve details like page title, URL, or cookies
   - driver.getTitle();
4. Waiting Strategy:           Wait for elements to load or be interactable using explicit waits
   - driver.manage().timeouts().implicitlyWait(Duration.ofMillis(500));
5. Find Element:               Locate elements on the page with locators like ID, CSS, or XPath
   - WebElement textBox = driver.findElement(By.name("my-text"));
6. Interact:                   Interact with elements by clicking, typing, or selecting
   - textBox.sendKeys("Selenium")
   - submitButton.click();
7. Request Information:        Extract details like text or attributes from elements
   - message.getText();
8. End Session:                Close the browser and clean up resources
   - driver.quit();
