# Test Automation

Test automation uses software to execute test cases, validate results, and provide feedback. It replaces manual testing efforts, particularly for repetitive and time-consuming tasks, thereby enhancing efficiency and accuracy.

# How It Works

# 1. Test Case Selection

Identify test cases suitable for automation, prioritizing those with high execution frequency, critical business logic, or prone to human error.

For demonstration, the test case below was created based on the sample URL Selenium provides:

`Test Case: Simple Form Submission with Selenium`

`Test Objective:` Verify that the script successfully fills a text box and submits a form on the Selenium Dev website.

`Pre-Requisites:`

1. Java installed
2. Selenium WebDriver libraries downloaded and configured
3. Chrome browser installed (or another browser supported by Selenium)

`Test Steps:`

1. Run _SeleniumJunitTest.java_ (replace `SeleniumJunitTest.java` with the name of the test file).

2. Verify Chrome opens the URL and script interacts with the "my-text" box, entering "Selenium".

3. Confirm the script clicks the submit button and retrieves a confirmation message.

4. Check that Chrome closes after execution.

`Pass/Fail Criteria:`

- `Pass` if all expected results are observed.
- `Fail` if any are missing or errors occur.

# 2. Tool Selection 

Choose test automation tools or frameworks that align with project requirements, team expertise, and budget constraints. Consider factors such as ease of use, test coverage, reporting capabilities, and integration with other tools.   

- `Tools`: Provides functionalities to _automate test actions_. It interacts with UI elements directly. Examples: Selenium (for web browsers), Appium (for mobile apps), and SoapUI (for SOAP and REST API tests). 

- `Frameworks`: Provides a structure and best practices for _building and managing test scripts_. It provides reusable components and libraries. Examples: Robot Framework, Playwright, TestNG.

# 3. Test Environment Setup

Establish a stable test environment to ensure reliable test execution.   

# 4. Test Script Development

Selenium will be used for demonstration purposes.

# 4.1 Creating a Maven Project (Optional but Recommended):

`Selenium WebDriver` can be used without a dedicated build system. However, using a build system like `Maven` offers advantages such as dependency management and project organization. Here's how to create a Maven project in IntelliJ IDEA Community:

1. Open IntelliJ IDEA Community.
2. Click "New" -> "Project."
3. Select "Maven" and choose a project location. Click "Next."
4. Fill in the "Group ID," "Artifact ID," and "Version." Click "Finish."

# 4.2 Adding Selenium Dependency:

The following dependency should be added to the `pom.xml` file, inside the <dependencies> section:

```xml
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.x.x</version> //Replace with latest version
</dependency>
```
This line tells Maven to download the Selenium Java library, which provides the necessary classes for interacting with web browsers.

In some situations, it's common to use test frameworks like JUnit or TestNG along with Selenium for writing and executing test cases to improve organization and readability. For this script, JUnit was implemented.

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.x.x</version> //Replace with latest version
    <scope>test</scope>
</dependency>
```

# 4.3 Folder Structure

Maven provides a standardized directory structure for Java projects. 

`Core Directories`

1. Directories containing software logic:

- `src/main/java`: Contains the project's main source code.
- `Package`: Organizes code into packages based on functionality or modules.   
- `Classes`: Java classes implementing the application's logic.

- `src/test/java`: Houses the project's test code.
- `Package`: Similar to src/main/java but for test classes.
- `Test classes`: JUnit or TestNG test classes.

2. Other directories:

- `src/main/resources`: Stores configuration files, properties files, and other static resources used during compilation.
- `src/test/resources`: Stores test-specific resources like test data or configuration files.
- `target`: This directory is used by Maven to store generated output, such as compiled classes, test results, and final artifacts (JAR, WAR, etc.).
- `pom.xml`: The project's configuration file, defining dependencies, build process, and other project-related settings.

# 4.4 Build the Script

This example demonstrates the basic test script using Selenium WebDriver in Java. It opens the URL, finds the text box, inserts the credential and clicks the "submit" button.

```java

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;

public class SeleniumJunitTest {

    private WebDriver driver;

    @Before
    public void setUp() {
        // Create a new Chrome WebDriver instance
        driver = new ChromeDriver();

        // Set implicit wait (optional)
        driver.manage().timeouts().implicitlyWait(Duration.ofMillis(500));
    }

    @Test
    public void testSeleniumForm() {
        //  Navigate to the URL being tested
        //  In this case, this is the test URL provided by Selenium
        driver.get("https://www.selenium.dev/selenium/web/web-form.html");

        //  Find the 'text box' and 'button' elements by their locators
        WebElement textBox = driver.findElement(By.name("my-text"));
        WebElement submitButton = driver.findElement(By.cssSelector("button"));

        //  The script will automatically type "Selenium" and click the page button
        textBox.sendKeys("Selenium");
        submitButton.click();

        //  Find the element displaying the message by its ID
        // Wait for message element to be visible (recommended)
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(30));
        WebElement message = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("message")));

        String messageText = message.getText();

    }

    @After
    public void tearDown() {
        //  Close the browser window
        driver.quit();
    }
}
```

# 5. Test Execution and Analysis 
Integrate test automation into the development lifecycle, and analyze test results. Use tools like Jira for bug tracking and report.

# 6. Continuous Improvement
Refine test automation processes to optimize efficiency and effectiveness.

# Conclusion
In summary, test automation is essential for improving software quality, efficiency, and speed while reducing costs and risks. 
