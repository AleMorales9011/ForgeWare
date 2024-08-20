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

1. Run _FirstScript.java_ (replace FirstScript.java with the name of the test file).

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
    <version>4.x.x</version> (Replace with your desired version)
</dependency>
```
This line tells Maven to download the Selenium Java library, which provides the necessary classes for interacting with web browsers.

In some situations, it's common to use test frameworks like JUnit or TestNG along with Selenium for writing and executing test cases.

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

Inside `src/test/java` create a class to encapsulate the test.




5. `Test Execution and Analysis`: Integrate test automation into the development lifecycle, and analyze test results.s.


6. `Continuous Improvement`: Refine test automation processes to optimize efficiency and effectiveness.



# Test Login Code Example

This example demonstrates a basic login test script using Selenium WebDriver in Java. It opens the URL, finds email and password fields using IDs, enters credentials, and clicks the login button.

```java

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class LoginTest { // Class name changed to follow CamelCase convention

    private WebDriver driver; // Declare driver as a member variable

    @Before
    public void setUp() {
        // Initialize ChromeDriver instance to automate Chrome browser
        driver = new ChromeDriver();
    }

    @Test
    public void loginTestRP() {
        // Open the target URL (replace "url" with the actual URL)
        driver.get(url);

        // Find the email field using its ID and enter the email address
        driver.findElement(By.id("mat-input-0")).sendKeys(email);

        // Find the password field using its ID and enter the password
        driver.findElement(By.id("mat-input-1")).sendKeys(password);

        // Find the login button using its ID and click it
        driver.findElement(By.id("kt_login_signin_submit")).click();
    }

    @After
    public void close() {
        // Close the browser and quit WebDriver resources
        driver.quit();
    }
}
```
# Conclussion
In summary, test automation is essential for improving software quality, efficiency, and speed while reducing costs and risks. 
