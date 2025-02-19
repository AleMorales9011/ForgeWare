![Image](images/04- Testing- gamer-playing-video-game.jpg)
# ForgeGuard - API Testing
Estimated Time: 2 hours<br>
Tech Stack: Selenium - Java - Cucumber - RestAssured<br>
Keywords: Automation - Testing - QA - BDD<br>
Experience Level: Beginner - Advanced

> Note: This project is a continuation of the project `ForgeGuard - Form Testing`

# Why API Testing
API testing is crucial because it ensures that `Application Programming Interfaces (APIs)` function
correctly, guaranteeing their reliability, performance, security, and overall quality by identifying potential issues
early in the development cycle, minimizing the risk of bugs reaching production and allowing for faster fixes, 
ultimately leading to a better user experience and cost savings.

# Objective
To perform manual(Postman) and automated(RestAssured) API tests to the Notes API
`https://practice.expandtesting.com/notes/api`. These test will:

- Create notes with title and content.
- Categorize notes into different categories.
- Update and delete notes.
- Search notes by title or category.

# Table Of Contents
1.  Why API Testing
2.  Objective
3.  Best Practice Step 1: Understand the API Requirements
4.  Best Practice Step 2: Set Up a Testing Environment
5.  Best Practice Step 3: Perform Functional Testing
6.  Best Practice Step 4: Perform Authentication & Security Testing
7.  Best Practice Step 5: Perform Performance & Load Testing
8.  Best Practice Step 6: Run Regression & Integration Tests
9.  Best Practice Step 7: Monitor & Log API Calls

### Encouragement
You're making great progress—keep up the momentum! 🚀

# 🛠 Best Practice Step 1: Understand the API Requirements
🔹 Review API Documentation

Identify available endpoints, methods (GET, POST, PUT, DELETE), request parameters, and response structures.
Check authorization methods (API key, Bearer token, OAuth, etc.).
🔹 Define the Test Scope

Determine what needs to be tested:
- ✅ Functional Testing (Does it work?)
- ✅ Security Testing (Is it secure?)
- ✅ Performance Testing (Is it fast?)
- ✅ Load Testing (Can it handle traffic?)
- ✅ Integration Testing (Does it work with other systems?)

# 🔄 Best Practice Step 2: Set Up a Testing Environment
🔹 Choose API Testing Tools
- ✔ Postman – Manual and automated API testing.
- ✔ REST Assured – Automated API testing for Java.
- ✔ Newman – Postman CLI runner for automation.
- ✔ JMeter – Load testing for APIs.
- ✔ Cypress/Playwright – API testing within E2E tests.

🔹 Ensure Test Data Availability

If the API interacts with a database, make sure you have test data set up.
Use mock servers (e.g., Postman Mock Server, WireMock) for isolated testing.
🔹 Set Up Authentication & Headers

Store API keys/tokens securely (e.g., environment variables).
Example: Use Postman Environments to manage variables like BASE_URL, TOKEN, USER_ID.

# 🧪 Best Practice Step 3: Perform Functional Testing
🔹 Validate HTTP Methods & Endpoints

Test all supported `request methods` `(GET, POST, PUT, DELETE)`.
Ensure that endpoints return expected responses and status codes:

```
200 OK → Success
201 Created → Resource Created
400 Bad Request → Invalid Request
401 Unauthorized → Missing Token
403 Forbidden → Insufficient Permissions
404 Not Found → Invalid Endpoint
```

🔹 Check Response Data Consistency
- Verify correct data types (string, int, boolean).
- Ensure required fields are present.
- Validate date formats (ISO 8601).
- Test empty or missing fields.

🔹 Validate Error Handling
- Send invalid inputs and verify proper error messages.
- Ensure rate limits are enforced.

# 🔑 Best Practice Step 4: Perform Authentication & Security Testing
🔹 Verify Authentication Mechanisms
- Test login requests and token expiration.
- Try unauthorized requests (no token, wrong token).

🔹 Check for Security Vulnerabilities
- ✔ SQL Injection – Try sending " OR 1=1; -- in input fields.
- ✔ Cross-Site Scripting (XSS) – Test by injecting <script>alert(‘XSS’)</script>.
- ✔ Broken Authentication – Try using expired tokens.

# 🚀 Best Practice Step 5: Perform Performance & Load Testing
🔹 Measure Response Times

Ensure API response time meets SLAs (e.g., < 500ms).
Test different payload sizes.
🔹 Simulate High Traffic

Use JMeter or K6 to send concurrent requests.
Monitor API failures and slowdowns.

# 🔗 Best Practice Step 6: Run Regression & Integration Tests
🔹 Automate API Tests

Write automated test scripts using Postman/Newman, REST Assured, or Cypress.
Integrate with CI/CD pipelines (GitHub Actions, Jenkins, GitLab CI/CD).
🔹 Check API Dependencies

Ensure API integrates well with databases, other APIs, or frontend applications.
Use mock services when dependencies are unavailable.

# 📊 Best Practice Step 7: Monitor & Log API Calls
🔹 Enable Logging
- Use tools like Grafana + Loki, New Relic, or Elastic Stack (ELK) for monitoring.
🔹 Track API Health
- Set up alerts for API failures (e.g., UptimeRobot, Prometheus).

# Manual Testing with Postman
`About Postman:` Postman is a tool that can be used without much training, both for manual and automation testing of 
APIs. It's easy to automate API tests and group them as a collection so you can chain the tests.

# Step 01 Understand the Notes API requirements
To access the API, first an account and log in using email and password must be created. This will generate an
`authentication token` needed for protected resources. The token must be kept safe for authorization.

# Step 02 Set Up a Testing Environment
Postman project structure is composed by `Workspaces` that contains `collections` that contains the `requests`. For the 
- Tasks:
- Create a collection: 
- Create an Environment: To store variables such as `base_url` and `x-auth-token`(header).
- Create a user to interact with the API.
```bash
POST https://practice.expandtesting.com/notes/api/users/register
```
Body parameters(info that goes along with the request).
```json
{
  "user": "practice",
  "email": "practi1@expandtesting.com",
  "password": "SuperSecurePassword123!"
}
```

# Best Practice Step 3: Perform Functional Testing
After setting environment it's time to test the functionalities.

- Health Check
```
GET
/health-check
Check the health of the API Notes service
```
- Get Profile
```
GET
/users/profile
Retrieve user profile information
```
# Automating API Testing with Rest Assured
"Rest Assured" is an `open-source` Java library primarily used for testing `REST APIs`. It is specifically designed for 
testing REST APIs, which are a common architecture for web services. it integrates seamlessly with Java-based testing
frameworks like JUnit and TestNG.  

# Step 01 RestAssured Set Up
To use `RestAssured` the following dependencies must be added to the `pom.xml` file.
```xml
<dependencies>
    <!-- RestAssured for API Testing -->
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <version>5.3.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JSON Processing -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.15.0</version>
    </dependency>

    <!-- JUnit for Assertions -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.9.2</version>
        <scope>test</scope>
    </dependency>

    <!-- JUnit Engine -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.9.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```
After adding the dependencies to the pom.xml a clean install must be performed so maven could download the new
dependencies.
```bash
mvn clean install -DskipTests # -DskipTest save resources by avoiding test from executing.
```
# Step 02 API feature file
The process for testing API using BDD with cucumber doesn't change. After dependencies are added to the pom.xml file
a feature file must be created with the test scenarios.

```gherkin
Feature: API Tests
  As a tester I want to test the Notes API
  Using the RestAssured Library to make sure I can automate
  this process in the future.

  @api-check
  Scenario: Verify API is running
    When I send a health check request
    Then the response status should be 200

  @api-login
  Scenario: Login
    When I send a login request
    Then the response status must be 200
```
# Step 03 Steps Definitions
After the feature file it's time to develop the step definition file where the actual test logic will live.
```java
package ForgeGuard;

import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import io.restassured.http.ContentType;
import io.restassured.response.Response;


import static io.restassured.RestAssured.given;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class ApiStepDefinitions {
    private Response response; // Instance variable of Response type (RestAssured class containing reponse methods)

    @When("I send a health check request")
    public void i_send_a_health_check_request() {
        response = given() // Method chaining. Each method response depends on the one before.
                .baseUri("https://practice.expandtesting.com/notes/api")
                .when()
                .get("/health-check");
    }

    @Then("the response status should be {int}")
    public void the_response_status_should_be(int expectedStatus) {
        System.out.println("Actual Response Status: " + response.getStatusCode());
        System.out.println("Response Body: " + response.getBody().asString());
        assertEquals(expectedStatus, response.getStatusCode(), "API response status mismatch");
    }

    @When("I send a login request")
    public void i_send_a_login_request() {
        response = given()
                .baseUri("https://practice.expandtesting.com/notes/api")
                .contentType(ContentType.JSON)
                .body("{ \"email\": \"practi1@expandtesting.com\", \"password\": \"SuperSecurePassword123!\" }")
                .when()
                .post("/users/login");
    }

    @Then("the response status must be {int}")
    public void the_response_status_must_be(int expectedStatus) {
        System.out.println("Actual Response Status: " + response.getStatusCode());
        System.out.println("Response Body: " + response.getBody().asString());
        assertEquals(expectedStatus, response.getStatusCode(), "API response status mismatch");
    }

    @When("I request user info")
    public void i_request_user_info() {
        response = given()
                .baseUri("https://practice.expandtesting.com/notes/api")
                .contentType(ContentType.JSON) //Authorization info must be looked for in the API docs.
                .header("x-auth-token", "9f1272d3b3e146089d475a1ee024dc95a6451739c975432ea41d0e2ed76c77a6")
                .body("{ \"email\": \"practi1@expandtesting.com\", \"password\": \"SuperSecurePassword123!\" }")
                .when()
                .get("/users/profile");
    }

    @Then("the response must be {int}")
    public void the_response_must_be(int expectedStatus) {
        System.out.println("Response Status: " + response.getStatusCode());
        System.out.println("Response body: " + response.getBody().asString());
        assertEquals(expectedStatus, response.getStatusCode(), "There is a status mismatch");
    }
}
```
# Conclusion
🎉 Congratulations on finishing the testing project! That’s a huge achievement, be proud of the dedication 
and effort you put into it. 🚀 The API testing project has successfully validated endpoints, ensured data integrity, and
strengthened automation workflows, marking a solid foundation for scalable and reliable API quality assurance. 🚀
