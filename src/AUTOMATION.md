# Test Automation

Test automation uses software to execute test cases, validate results, and provide feedback. It replaces manual testing efforts, particularly for repetitive and time-consuming tasks, thereby enhancing efficiency and accuracy.

# How It Works

1. `Test Case Selection`: Identify test cases suitable for automation, prioritizing those with high execution frequency, critical business logic, or prone to human error.

2. `Tool Selection`: Choose test automation tools that align with project requirements, team expertise, and budget constraints. Consider factors such as ease of use, test coverage, reporting capabilities, and integration with other tools.   

3. `Test Environment Setup`: Establish a stable test environment to ensure reliable test execution.   

4. `Test Script Development`: Create reusable test scripts using appropriate scripting languages and frameworks.

5. `Test Execution and Analysis`: Integrate test automation into the development lifecycle, and analyze test results.s.

6. `Continuous Improvement`: Refine test automation processes to optimize efficiency and effectiveness.

# Automation Tools vs. Frameworks

| FEATURE | TESTING AUTOMATION TOOLS | TESTING AUTOMATION FRAMEWORKS | 
|---------|-----------------------------|--------------------------|
| **PURPOSE** | Provides functionalities to _automate test actions_ | Provides a structure and best practices for _building and managing test scripts_ |
| **FOCUS** | Execution and management of tests | Design and development of test scripts |
| **ABSTRACTION LEVEL** | Lower level - interacts with UI elements directly | Higher level - provides reusable components and libraries | 
| **CUSTOMIZATION** | Limited customization options | Highly customizable based on project needs |
| **EXAMPLES** | Selenium, Appium, SoapUI | Robot Framework,  TestNG,  Playwright |
| **CODING REQUIREMENTS** | May require some coding knowledge | Requires coding knowledge in a specific programming language |
| **COST**| Can be open-source or commercial | Mostly open-source |

# CONCLUSION
By differentiating between testing automation tools and frameworks, testers can select the most suitable option for crafting a reliable and sustainable test suite, ultimately optimizing their testing process.


# Test Login Code Example

This example demonstrates a basic login test script using Selenium WebDriver in Java. It opens the URL, finds email and password fields using IDs, enters credentials, and clicks the login button.

```java

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class logintest {

    private WebDriver driver; // Declare driver as a member variable

    @Before
    public void setUp() {
        driver = new ChromeDriver();
    }

    @Test
    public void loginTestRP() {
        driver.get(url);
        driver.findElement(By.id("mat-input-0")).sendKeys(email);
        driver.findElement(By.id("mat-input-1")).sendKeys(password);
        driver.findElement(By.id("kt_login_signin_submit")).click();
    }

    @After
    public void close() {
        driver.quit(); // Use quit() to close browser and WebDriver resources
    }
}
```
