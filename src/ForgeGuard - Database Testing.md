# ForgeGuard - Database Testing
Estimated Time: 2 hours<br>
Tech Stack: Selenium - Java - Cucumber<br>
Keywords: Automation - Testing - QA - BDD<br>
Experience Level: Beginner - Advanced

> Note: This project is a continuation of the project `ForgeGuard - Functionality Testing`

# Why Database Testing
When automating tests for modern applications is crucial to interact with a database to extract and validate data 
following business logic (mostly for fill up forms, and login) since the operations the user will be able to perform in
the app will depend mostly on information from the database. 

# Objective
Create automated test cases using `Selenium`, `Java`, and `Cucumber` that uses a database to interact with an app
using business logic. Around `~90%` of the actions a user perform on any given applications requires some kind of
database interaction.

These tests will:

- Test login with valid credentials.
- Test login with invalid credentials.
- Validate error messages for incorrect input.
- Verify successful redirection after a valid login.

## Encouragement 🏆
Progress in automation testing requires persistence, and each effort lays a solid foundation for future success.

# Table Of Contents

1.  Why Database Testing
2.  Objective
3.  Database Testing
4.  Database Testing With H2
5.  Step 01 Set Up H2 in Your Project
6.  Step 02 Write a Test Scenario
7.  Step 03 Write The Step Definition File
8.  Step 04 Login Test With Database Interaction
9.  

# Database Testing
Database testing is crucial because it verifies the accuracy, consistency, and integrity of data stored within a
database, ensuring the reliability and credibility of an application by identifying issues like missing or duplicate
records, incorrect data types, or inconsistent data relationships, ultimately preventing faulty decision-making based on
inaccurate data.

# Database Testing With H2
`H2 Database:` It's an in-memory, lightweight, and Java-based database ideal for testing purposes. It simulates a real
database environment without needing a full-fledged database installation. Perfect for integration testing where test
data is crucial.

# Step 01 Set Up H2 in Your Project
First step to set up H2 database is to add the H2 dependency to the pom.xml: 
```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.220</version>
    <scope>test</scope>
</dependency>
```
# Step 02 Write a Test Scenario
Next step is to write a configuration file to test the database is working correctly.
```gherkin
Feature: H2 Database Testing
  As a developer
  I want to test the H2 database connection
  So that I can verify that the database operations work as expected

@database-validation
  Scenario: Validate H2 database connection and query
    Given a sample H2 database is initialized
    When a user with ID 1 is queried
    Then the user name should be "John Doe"
```
# Step 03 Write The Step Definition File
This file will execute a test to verify the database works properly.
```java
package ForgeGuard;

import io.cucumber.java.en.*;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class DatabaseSteps { // The DatabaseSteps class in the name of the file and the container for everything in it.

    private Connection connection; // Variable instance of SQL connection.
    private Statement statement;   // Variable instance of SQL queries
    private ResultSet resultSet;   // Variable Instance of the SQL query result.

    @Given("a sample H2 database is initialized") // Cucumber annotation that maps with the feature file step.
    public void a_sample_h2_database_is_initialized() throws Exception { // Method to handle connection.
        // Connect to the H2 database
        connection = DriverManager.getConnection("jdbc:h2:mem:testdb", "sa", ""); // Connects to H2.
        statement = connection.createStatement(); // Creates an object to send SQL queries.

        // Create a sample table and insert data
        statement.execute("CREATE TABLE USERS (ID INT PRIMARY KEY, NAME VARCHAR(255));"); // Execute SQL queries.
        statement.execute("INSERT INTO USERS (ID, NAME) VALUES (1, 'John Doe');"); // Executes SQL queries.
    }

    @When("a user with ID {int} is queried")
    public void a_user_with_id_is_queried(Integer id) throws Exception {
        // Query the database
        resultSet = statement.executeQuery("SELECT * FROM USERS WHERE ID=" + id + ";");
        resultSet.next();
    }

    @Then("the user name should be {string}")
    public void the_user_name_should_be(String expectedName) throws Exception {
        // Validate the result
        String actualName = resultSet.getString("NAME");
        assertEquals(expectedName, actualName);

        // Clean up resources
        resultSet.close();
        statement.close();
        connection.close();
    }
}

```
# Step 04 Login Test With Database Interaction
Next step is to perform a login test querying data from a database. Simulating what will happen in a real life 
situation. This file expands the `000_smoketest_login.feature` including database interactions.
```java
package ForgeGuard;

import io.cucumber.java.en.And;
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

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.time.Duration;


import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class ValidLogin {
    WebDriver driver;
    WebDriverWait wait;
    private String username;
    private String password;

    @Given("I am in the login page")
    public void i_am_on_the_login_page() {
        WebDriverManager.chromedriver().setup();
        ChromeOptions options = new ChromeOptions();
        options.addArguments("--headless", "--disable-gpu", "--window-size=1920,1080");
        driver = new ChromeDriver(options);

        driver.get("https://practice.expandtesting.com/login");

        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
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
    public void i_should_be_redirected_to_the_secure_page() {
        String currentUrl = wait.until(ExpectedConditions.urlContains("secure")) ? driver.getCurrentUrl() : "";
        assertTrue(currentUrl.contains("secure"), "The user is not redirected to the secure page.");

    }

    @Then("I should see a welcome message {string}")
    public void i_should_see_a_welcome_message(String expectedMessage) {
        WebElement welcomeMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("/html/body/main/div[4]/div/h1")));
        assertTrue(welcomeMessage.isDisplayed(), "Welcome message is not displayed");
        assertEquals(expectedMessage, welcomeMessage.getText(), "The message does not match");

        driver.quit();
    }

    @When("I enter the invalid credentials {string} and {string}")
    public void i_enter_the_invalid_credentials(String username, String password) {
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//*[@id=\"username\"]")));
        WebElement passwordField = driver.findElement(By.xpath("//*[@id=\"password\"]"));
        WebElement loginButton = driver.findElement(By.xpath("//*[@id=\"login\"]/button"));
        usernameField.sendKeys(username);
        passwordField.sendKeys(password);
        loginButton.click();
    }

    @Then("I should see an error message {string}")
    public void i_should_see_an_error_message(String expectedMessage) {
        WebElement errorMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("flash")));
        assertTrue(errorMessage.isDisplayed(), "Error message is not displayed");
        assertEquals(expectedMessage, errorMessage.getText(), "Text does not match");

        driver.quit();
    }

    @When("I enter the special character{string}and{string}")
    public void i_enter_the_special_character(String special_one, String special_two) {
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//*[@id=\"username\"]")));
        WebElement passwordField = driver.findElement(By.xpath("//*[@id=\"password\"]"));
        WebElement loginButton = driver.findElement(By.xpath("//*[@id=\"login\"]/button"));
        usernameField.sendKeys(special_one);
        passwordField.sendKeys(special_two);
        loginButton.click();
    }

    @Then("I should see an error{string}")
    public void i_should_see_an_error(String expectedMessage) {
        WebElement errorMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("flash")));
        assertTrue(errorMessage.isDisplayed(), "Error message is not displayed");
        assertEquals(expectedMessage, errorMessage.getText(), "Text does not match");

        driver.quit();
    }

    @When("I query the database for the credentials")
    public void i_query_the_database_for_the_credentials() throws Exception {
        //Step 01 Connection to the database.
        Connection connection = DriverManager.getConnection("jdbc:h2:file:./data/testdb", "sa", "");
        Statement statement = connection.createStatement();
        // Step 02 Create the table if it does not exist.
        statement.execute("CREATE TABLE IF NOT EXISTS USERS (ID INT PRIMARY KEY, NAME VARCHAR(255), PASSWORD VARCHAR(255));");
        // Step 03 Insert data if the table is empty.
        statement.execute("MERGE INTO USERS KEY(ID) VALUES (1, 'practice', 'SuperSecretPassword!');");
        // Step 04 Query the credentials.
        ResultSet resultSet = statement.executeQuery("SELECT NAME, PASSWORD FROM USERS WHERE ID = 1;");
        // Step 05 Move to the first result row.
        resultSet.next();

        // Step 06 Store the credentials in temporary(within the method) variables.
        String username = resultSet.getString("NAME");
        String password = resultSet.getString("PASSWORD");
        // Step 07 Transfer data from local to instance variables so they can be accessed from outside the method.
        this.username = username;
        this.password = password;

    }

    @Then("I should use those credentials to log in")
    public void i_should_use_those_credentials_to_log_in() {
        WebElement usernameField = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//*[@id=\"username\"]")));
        WebElement passwordField = driver.findElement(By.xpath("//*[@id=\"password\"]"));
        WebElement loginButton = driver.findElement(By.xpath("//*[@id=\"login\"]/button"));

        // Step 08 Request the data from the instance variables to log in.
        usernameField.sendKeys(username);
        passwordField.sendKeys(password);
        loginButton.click();

    }

    @And("I should see a message{string}")
    public void i_should_see_a_message(String message) {
        WebElement welcomeMessage = wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("/html/body/main/div[4]/div/h1")));
        assertTrue(welcomeMessage.isDisplayed(), "Welcome message is not displayed");
        assertEquals(message, welcomeMessage.getText(), "The message does not match");

        driver.quit();
    }
}

```
# Conclusion🪘
This `Database Testing project` is a fantastic step forward in combining data management with testing workflows.
Integrating `H2`, `Selenium`, and `Cucumber` demonstrates how dynamic database connections can enhance testing 
efficiency and realism. This success lays a strong foundation for tackling more complex scenarios and ensures 
confidence in your application's functionality. Great work—keep building on this momentum!😊

