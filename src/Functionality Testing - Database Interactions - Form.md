![Image](images/02- Testing- female-programmer-coding-night.jpg)
# Functionality Testing - Database Interactions - Form
Estimated Time: 2 hours<br>
Tech Stack: Selenium - Java - Cucumber - H2<br>
Keywords: Automation - Testing - QA - BDD<br>
Experience Level: Beginner - Advanced

> Note: This project is a continuation of the project `ForgeGuard - Database Testing`

# Why Form Testing
After logins forms are the most used functionality in the web as they serve to get users information to then be able to
apply some business logic. 

# Objective
Create automated test cases using `Selenium`, `Java`, and `Cucumber` that uses a database to get data to fill up a form.
These tests will:

- Test form with valid credentials.
- Test form with invalid credentials.
- Validate error messages for incorrect input.
- Verify successful redirection after form completion.

## Encouragement 🏆
*“Discovering the unexpected is more important than confirming the known.”* 
– George E. P. Box


# Table Of Contents

1.  Why Form Testing
2.  Objective
3.  Step 01 Database Interaction Via Terminal
4.  Step 02 Feature File
5.  Step 03 Steps Definition File
6.  Step 04 Conclusion


# Step 01 Database Interaction via terminal
To interact with form during testing it's possible to pass the form data in the step definitions file like in the 
`ForgeGuard - Database Testing` example. However, commonly in production logic and data don't mix, mostly for security
reason but also practicality if the data is too long.

- Navigate to the H2 jar file:
Normally using maven the file will be at:
```bash
cd ~/.m2/repository/com/h2database/h2/2.2.220
```
- Launching the H2 Shell:
```bash
java -cp h2-2.2.220.jar org.h2.tools.Shell
```
- Connect to the Database:
To connect to the database some information is required including the url, driver, user, and password.
```
URL: jdbc:h2:file:C:/03JOB SEARCH/04ForgeGuard/ForgeGuard/data/testdb # Absolute path
USER: sa
PASSWORD: 
DRIVER:
```
- Querying the database:
Once on the database's shell it's possible to interact with it trough SQL queries such as:
```SQL
SHOW TABLES;
```
- Altering/Modifying tables:
Tables can be modified to keep form data as follows:
```sql
ALTER TABLE USERS ADD (CONTACT_NAME VARCHAR(255), CONTACT_NUMBER VARCHAR(15), PICKUP_DATE DATE, PAYMENT_METHOD VARCHAR(50)); 
```
- Updating rows to fit form data:
```sql
UPDATE USERS SET NAME = 'Jane Doe', CONTACT_NUMBER = '012-5678901', PICKUP_DATE = '2025-03-01', PAYMENT_METHOD = 'credit card' WHERE ID = 2;
```
- Inserting data into the table:
```sql
INSERT INTO USERS (ID, NAME, PASSWORD, CONTACT_NUMBER, PICKUP_DATE, PAYMENT_METHOD)
VALUES (2, 'Jane Doe', 'password123', '012-5678901', '2025-03-01', 'cash on delivery');
```
# Step 02 Feature File
```gherkin
Feature: Form
  As a developer
  I want to be able to extract data from the database
  So I can fill up forms with it

  @form-submission
  Scenario: Form Submission
    Given I am in the form page
    When I extract the information from the database
    When I use the information to fill up the form
    Then I should see the message"Thank you for validating your ticket"
```
# Step 03 Steps Definition File

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
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.time.Duration;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class FormSteps {
    WebDriver driver;
    WebDriverWait wait;
    private String username;
    private String number;
    private String date;
    private String payment;

    @Given("I am in the form page")
    public void i_am_in_the_form_page() {
        WebDriverManager.chromedriver().setup();
        ChromeOptions options = new ChromeOptions();
        options.addArguments("--headless", "--disable-gpu", "--window-size=1920,1080");
        driver = new ChromeDriver(options);

        driver.get("https://practice.expandtesting.com/form-validation");
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
    }

    @When("I extract the information from the database")
    public void i_extract_the_information_from_the_database() throws Exception {

        try (Connection connection = DriverManager.getConnection("jdbc:h2:file:C:/03JOB SEARCH/04ForgeGuard/ForgeGuard/data/testdb", "sa", "");
             Statement statement = connection.createStatement();
             ResultSet resultSet = statement.executeQuery("SELECT * FROM USERS WHERE ID = 2;")) {
            // Connect to the H2 database

            // Execute query to fetch user data
            if (resultSet.next()) {
                // Store the retrieved data into instance variables
                this.username = resultSet.getString("NAME");
                this.number = resultSet.getString("CONTACT_NUMBER");
                this.date = resultSet.getString("PICKUP_DATE");
                this.payment = resultSet.getString("PAYMENT_METHOD");
            } else {
                throw new Exception("No data found in the USERS table.");
            }
        }
    }

    @When("I use the information to fill up the form")
    public void i_use_the_information_to_fill_up_the_form() {
        // Locate the form fields
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("validationCustom01")));
        WebElement numberField = driver.findElement(By.id("validationCustom05"));
        WebElement dateField = driver.findElement(By.name("pickupdate"));
        Select paymentField = new Select(driver.findElement(By.id("validationCustom04")));
        WebElement submitButton = driver.findElement(By.xpath("/html/body/main/div[3]/div/div/div/div/form/div[5]/button"));

        // Fill the form with extracted data
        usernameField.sendKeys(username);
        numberField.sendKeys(number);
        dateField.sendKeys(date);
        paymentField.selectByVisibleText(payment);
        submitButton.click();
    }

    @Then("I should see the message{string}")
    public void i_should_see_the_message(String expectedMessage) {
        // Verify the success message
        WebElement submissionMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("/html/body/main/div[3]/div/div/p")));
        assertEquals(expectedMessage, submissionMessage.getText(), "The message does not match");
        driver.quit();
    }
}

```
# Step 04 Conclusion
The project has been a remarkable journey, showcasing the power of integration between Selenium, Cucumber, and H2 
databases to build a comprehensive and efficient test automation framework. The progress made is a clear indicator of
how dedication and persistence lead to meaningful achievements—this is only the beginning of a promising path in test
automation! Keep up the fantastic work! 🚀
