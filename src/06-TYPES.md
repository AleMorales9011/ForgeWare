# Functional

| TECHNIQUE | DESCRIPTION | ADVANTAGE | DISADVANTAGE |
|-----------|-------------|-----------|--------------|
| Unit Testing | Tests individual units of code (functions, modules) | Isolates and identifies errors early, promotes modular development | Requires good code structure, can be time-consuming for large projects |
| Integration Testing | Tests how different units interact with each other.| Ensures modules work together as expected | Can be complex for large systems, requires well-defined interfaces|
| System Testing | Tests the entire system as a whole. | Catches system-level issues, and identifies integration problems | Time-consuming, can be expensive |
| Acceptance Testing | Verifies if the system meets user requirements. | Ensures system is usable and meets business objectives | Relies on clear requirements, can be subjective based on user interpretation |
| Regression Testing | Ensures changes haven't introduced new bugs. | Protects against regressions after modifications | Can be time-consuming to maintain a large suite of tests, may not cover all edge cases |

# 1. Unit Tests
# Catch Errors With Unit Tests

## JUnit 
JUnit is an open-source Java framework for unit testing. By incorporating JUnit into their workflow, Java programmers can write small, targeted tests that ensure each piece of code functions as intended, ultimately leading to more robust and stable applications.


**Disclaimer:**

This code snippet below showcases a unit test class designed to evaluate the functionality of the _DatabaseConnectionManagementSystem_ class. Let's delve into the code and explore its components.

**Essential Imports:**

The initial lines import the necessary libraries and classes for the testing process:

```java
import org.example.DatabaseConnectionManagementSystem;
import org.example.Pessoa;
import org.junit.jupiter.api.*;

import java.time.LocalDateTime;

```

The next line defines a public test class named DatabaseConnectionManagementSystemTest, which serves as a container for the unit tests assessing the database connection management system.

```java
public class DatabaseConnectionManagementSystemTest {

```

**Test Method Annotations**
JUnit annotations streamline the testing process. Here's a breakdown of the annotations used in this code:

**- @BeforeAll:** It signals a method to run just once before all test cases within a test class are executed.

```java
    @BeforeAll
    static void setupConnection() {
        DatabaseConnectionManagementSystem.startConnection();
    }

```

**- @BeforeEach:** It tells the testing framework to run a specific method before each test case in a class.

```java
    @BeforeEach
    void insertTestData(){
        DatabaseConnectionManagementSystem.insertUserData(new Pessoa("John", LocalDateTime.of(2000,1,1,13,0,53)));
    }
```
**- @AfterEach:** This annotation tells the framework to run a specific method after each test case execution.

```java
    @AfterEach
    void removeTestData(){
        DatabaseConnectionManagementSystem.removeUserData(new Pessoa("John", LocalDateTime.of(2000,1,1,13,0,53)));
    }
```

**- @Test:** annotation in JUnit marks a method as a test case to be executed during the testing process.

```java
    @Test
    void validateReturnData(){
        Assertions.assertTrue(true);
    }

    @Test
    void validateNullData(){
        Assertions.assertNull(null);
    }
```

**- @AfterAll:** It signifies a method to be executed after all test cases within a test class have finished running.

```java
    @AfterAll
    static void endConnection(){
        DatabaseConnectionManagementSystem.endConnection();
    }
}
```

If the test ran correctly, you should see something like this in your debug console:
![image](https://github.com/amandaestevez/SOFTWARE-QA/assets/123298275/26aa2420-9a76-4a9f-b1cc-f99fabea6bdc)

**Summarizing:**
This test class establishes a database connection before any tests are run. It then inserts sample data (a person named John) before each test and removes it afterward. Finally, it closes the connection after all tests are complete. The current test cases themselves require further development to interact with the database functionalities, but the overall structure for unit testing is in place.

## Mockito

Mockito is an open-source framework in Java that lets you create mock objects for unit testing, making your tests more isolated and easier to maintain.

**Disclaimer:**

This code snippet below showcases a unit test class designed to evaluate the functionality of the _ServicoEnvioEmail_ class. This test verifies if the service sets the email format correctly before sending it. Let's delve into the code and explore its components.

**Essential Imports:**

The initial lines import the necessary classes from `email.system.simulation` (containing the email sending logic) and testing libraries from JUnit and Mockito.

```java
package email.system.testing;

import email.system.simulation.*;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.*;
import org.mockito.junit.jupiter.MockitoExtension;
```

The code resides in the `email.system.testing` package.


**- @ExtendWith:** This annotation tells `JUnit` to use the `Mockito` library for creating mock objects during the test.

```java
@ExtendWith(MockitoExtension.class)
public class ServicoEnvioEmailTeste {
```

**- @Mock:** This annotation creates a mock object of the `PlataformaDeEnvio` class. Mocks simulate real objects but allow controlled behavior for testing purposes.

```java
  @Mock
  private PlataformaDeEnvio plataforma;
```

**- @InjectMocks:** This injects the mock `plataforma` object (created with `@Mock`) into the `servico` field. Now `servico`  can interact with the mock platform.

```java
  @InjectMocks
  private ServicoEnvioEmail servico;
```

**- @Captor:** This captures an argument passed to a method during a test. Here, it captures the `Email` object passed to the `enviaEmail` method

```java
  @Captor
  private ArgumentCaptor<Email> emailCaptor;
```

**- @Test:** This annotation marks the following method (`validaSeEmailEstaComDadosCorretos`) as a test case to be executed by JUnit.

Inside the test method:
- Email address, message, and expected format variables are set up.
- The test calls `servico.enviaEmail` to simulate sending an email.
- `Mockito.verify(plataforma).enviaEmail(emailCaptor.capture());:` This line uses Mockito to verify if the enviaEmail method was called on the mock plataforma with the email captured by `emailCaptor`.
- `Assertions.assertEquals(Formato.HTML, emailCapturado.getFormato());:` This asserts (checks) if the captured email object (`emailCapturado`) has its format set to `Formato.HTML`. This verifies the service sets the format correctly.

```java
  @Test
  void validaSeEmailEstaComDadosCorretos() {

    String email = "random@test.com";
    String mensagem = "Hey there!";

    // Simulates sending the email
    servico.enviaEmail(email, mensagem, true);

    // Mockito verifies interaction with the mock
    Mockito.verify(plataforma).enviaEmail(emailCaptor.capture());

    // Asserts the email format
    Email emailCapturado = emailCaptor.getValue();
    Assertions.assertEquals(Formato.HTML, emailCapturado.getFormato());
  }
```

If the test ran correctly, you should see something like this:
  <img width="958" alt="test with mockito" src="https://github.com/amandaestevez/SOFTWARE-QA/assets/123298275/4a88b069-d750-4dba-bc52-38664924e8d3">

**Summarizing:** By leveraging Mockito, this unit test isolates the email-sending service, verifying the email formatting behavior before transmission. This ensures the service adheres to email format specifications, contributing to the overall robustness of the codebase.

## Conclusion

Unit testing serves as a cornerstone for building reliable software. By systematically dissecting code into smaller, testable units, developers can identify and squash bugs early in the development process. 


# 2. Integration
# 3. System

# 4. User Acceptance (UAT)
Select true statements for User Acceptance Testing:

**QUESTIONS**

_1. Who should perform User Acceptance Testing?_
   
   ❌ Developers
   ✅ Customers
   ❌ QA testers
   ❌ Customer support agents

_2. When should User Acceptance Testing be performed?_

   ❌ Before writing integration tests
   ❌ Before system testing
   ❌ Just after important features are implemented
   ✅ After all features have been implemented and otherwise tested

_3. How should User Acceptance Testing be performed?_

 ✅ Using real-life scenarios
 ❌ According to functional tests
 ❌ Using a list of steps that were agreed upon at the start of the project
 ❌ By predicting user behavior.

-----------
**EXPLANATION**

Before diving into the answers, let's understand a few core concepts of UAT.

In this type of testing, the end users and clients will test the software in the "real world" or real-life scenarios/conditions to assess its usability and functionality. 
![image](https://github.com/user-attachments/assets/29297d93-ab43-4a6c-a19d-2ccca6d10b8f) 

UAT ensures the product meets real-world requirements.

There are six different types of UAT:

**- Alpha Testing:** Conducted by internal users or a limited group of external users to identify early-stage issues.
**- Beta Testing:** Involves a larger group of external users who test the product in a real-world environment.
**- Operational Acceptance Testing (OAT):** Verifies the product's ability to function in the actual production environment, including performance, security, and backup procedures.
**- Contract Acceptance Testing (CAT):** Ensures the product meets the contractual specifications and requirements agreed upon with the client.
**- Regulation Acceptance Testing (RAT):** Confirms compliance with industry regulations and standards.
**- Business Acceptance Testing (BAT):** Evaluates if the product meets the business objectives and goals.

--------------
 **ANSWERS**

 _1. Who should perform User Acceptance Testing?_

 **The customers should perform User Acceptance Testing.** These individuals should have a deep understanding of the system's requirements and how it will be used in real-world scenarios. They are the ones who will know if the software suits their needs.

_2. When should User Acceptance Testing be performed?_

**UAT should be performed after all features have been implemented and otherwise tested** to ensure the product is complete and stable for end-user evaluation.

_3. How should User Acceptance Testing be performed?_

**UAT should be conducted using real-life scenarios** to uncover issues that might not be apparent in controlled testing environments.

--------------

Thank you so much for dedicating your time to read this! 

# 5. Regression

# Non-Functional

| TECHNIQUE | DESCRIPTION | ADVANTAGE | DISADVANTAGE |
|-----------|-------------|-----------|--------------|
| Performance Testing | Evaluates system performance under load. | Ensures software meets performance requirements. | Requires specialized tools and expertise, can be complex to set up |
| Usability Testing | Evaluates user experience with the software. | Identifies user interface and interaction issues. | Subjective and requires representative users for testing. |
| Mutation Testing | Introduces deliberate errors (mutations) in the code and checks if tests detect them. | Improves test suite effectiveness, and identifies areas with weak test coverage. | Requires additional code and can be computationally expensive.|
| Capture-Replay Testing | Records user interactions and replays them for regression testing. | Efficient for regression testing, automates repetitive tasks. | May not capture unexpected user behavior. |

## Conclusion
The choice of testing techniques will depend on several factors, such as the size and complexity of the software, the project schedule, and the budget. It is important to use different testing techniques to ensure that software is thoroughly tested.

# 1. Performance
# Implement Performance Tests With JMeter, LoadRunner, And Gatling

This table compares JMeter, LoadRunner, and Gatling for key performance testing considerations.

## Methodology

The table will list JMeter, LoadRunner, and Gatling side-by-side, highlighting factors like compatibility, tes, and other decision points for performance testing.

| FEATURE | JMETER | LOADRUNNER | GATLING |
|---------|-------|----------|----------|
| **Testing Requirements** | Suitable for web applications, database testing, mobile apps, and more. | Extensive for complex enterprise applications | Leans towards modern web applications |
| **Compatibility** | Wide range of protocols (HTTP, FTP, JDBC, etc.) | Primarily HTTP/HTTPS, requires plugins for others | Primarily HTTP/HTTPS, some support for others |
| **Ease of Use** | GUI-based, good for beginners; scripting for advanced users | Complex GUI, requires scripting knowledge | Requires coding in Scala (or Java/Kotlin with plugins) |
| **Community and Support** | Large, active open-source community | Paid support from Micro Focus | Active open-source community, some commercial support options |
| **Testing Features** | Rich set of features including load balancing, thread groups, and assertions | Extensive feature set specifically designed for complex load testing scenarios | Focuses on simulating realistic user behavior with features like scenario building, HTTP client simulation, and integration with tools like Selenium |
| **Scalability and Load Generation** | Highly scalable with distributed testing | Highly scalable, mature solution for large loads | Highly scalable, mature solution for large loads	Designed for high concurrency and scalability |
| **Integration Capabilities** | Can integrate with CI/CD tools with plugins | Extensive integration options with various tools	| Integrates well with DevOps workflows |
| **Reporting & Analysis** | Provides reports and graphs, customizable with plugins	| Comprehensive reporting and dashboards	| Offers clear and visual test results |
| **Cost and Licensing** | Free, open-source |	Paid commercial license |	Free open-source version with limited features, paid options available |
| **Performance Test Types supported** | Load, stress, functional, API, mobile |	Load, stress, volume, spike, concurrent users |	Load, stress, soak, spike | 

## CONCLUSION

By comparing these features, users can select the most suitable performance testing tool based on their specific needs and project requirements.

# 2. Load
# 3. Stress
# 4. Web Performance
# 5. Soak/Endurance
# 6. Usability
# 7. Accessibility
     Visual
     Hearing
     Physical
     Cognitive
# 8 . Security

# Security: Web Application
# CROSS-SITE REQUEST FORGERY (CSRF)

A web application for ordering cat food charges users and places an order when an HTTP GET request is issued to the following URL:

http://www.catsupplies.com/order?brand=xxxxx&quantity=xxxxx

A malicious website could add snippets like this to their site:

```html
<img src="http://www.catsupplies.com/order?brand=xxxxx&quantity=xxxxx">
```

What would help protect against such attacks considering that the web application has the CORS policy that only allows requests from the same site?

(Select all acceptable answers):

**ALTERNATIVES**

:white_check_mark: 1. Switch the endpoint method from HTTP GET to HTTP PUT and move the query parameters into the request body.


:x: 2. Add an additional "token" cookie, without the same site attribute, that is unique per user session and checks if it's correct when visiting the page.


:x: 3. Only accept IPv6 connections.


:white_check_mark: 4. Add an additional "token" HTTP header that is unique per user session and checks if it's correct when visiting the page.


:x: 5. Set the Content-Type header of the returned data to text/html.


--------------------

**EXPLANATION**

This is a Cross-site Request Forgery attack, A.K.A. CSRF or XSRF - it forces users to submit an unwanted request to an application they are **logged in.** 

In this case, the hacker embedded the malicious HTML snippet containing pre-filled data for brand and quantity (of what the user is buying) as an image and distributed the link, mostly through **social engineering.**

When the user accesses this link, the browser automatically sends the order since the link contains a GET request. It is hard for the cat supplies store owner to know about the attack, because the unwanted GET request sends the customer's cookies along, making the purchase seem legit.

--------------------

**_How to avoid this attack?_**


:white_check_mark: 1. Switch the endpoint method from HTTP GET to HTTP PUT and move the query parameters into the request body.

- **CORRECT.** *GET Requests that change state aren't safe in general.* In the cat supplies store case, it changes state because it places an order - altering the *state of the system*: inventory, user account, financial records, etc.

Changing the HTTP method from GET to PUT would make it more difficult for the store to suffer a CSRF attack because the GET method passes the information in the URL, while the PUT method passes the information in the request body.

It's not a foolproof solution, but it adds a layer of security.

--------------------

:x: 2. Add an additional "token" cookie, without the same site attribute, that is unique per user session and checks if it's correct when visiting the page.

- **INCORRECT.** _The token cookie can still be stolen if it doesn't contain the HttpOnly flag_ - a security measure that makes cookies inaccessible via JavaScript. For this alternative, we are considering the flag wouldn't be added since it isn't mentioned anywhere.

In this case, the malicious actor would just need to create a JavaScript function that steals the token (or sensitive information stored in the cookie) and sends it to their server, then add the function as an attribute to the **_img_** element. 

It could look like this:

```html
<img src="http://www.catsupplies.com/order?brand=xxxxx&quantity=xxxxx">
 onload="stealCookieValue()"
```

The **_onload_** event attribute specifies that the **_stealCookieValue()_** function should be triggered after the **_img_** element successfully loads.

**_But how do you set the HttpOnly flag?_**

That depends on the language used on the server side. In Java, for example, you can use the **_javax.servlet.http_** package to create it:

```java
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServletResponse;

public class MyServlet {

    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        
        // Set cookie name and value
        String cookieName = "myToken";
        String cookieValue = "your_token_value";
        
        // Create a cookie object
        Cookie cookie = new Cookie(cookieName, cookieValue);
        
        // Set HttpOnly flag
        cookie.setHttpOnly(true);
        
        // Set expiration time (optional)
        cookie.setMaxAge(60 * 60 * 24); // Expires in 24 hours
        
        // Add cookie to the response
        response.addCookie(cookie);
        
        // ... (rest of your servlet code)
    }
}
```

--------------------

:x: 3. Only accept IPv6 connections.

- **INCORRECT.** _CSRF targets logged-in user sessions, not the servers directly._ This means that if the user is logged in and authorized by the server, the attack will happen no matter the IP version.

--------------------

:white_check_mark: 4. Add an additional "token" HTTP header that is unique per user session and checks if it's correct when visiting the page.

- **CORRECT.** _Upon successful login, the server generates a unique token value, either _a random string_ or _a cryptographic hash_. The generated token is included in the "token" HTTP header when the user makes subsequent requests to the page. The server then receives the request and checks the value of the "token" header, associating it with the user session (e.g., storing it in a database or in-memory cache). If the token value matches the one associated with the user's session, the request is considered valid. Otherwise, the server rejects the request.

--------------------

 :x: 5. Set the Content-Type header of the returned data to text/html.

 -**INCORRECT.** _Just like in the IP version case, the CSRF attack targets user sessions,_ not the server itself. So even if the server returns text/html data, it wouldn't prevent the attack.

## EXERCISE 02: An office supplies web store wants to improve the security of their website. A developer suggested a number of changes.

Which of the changes would improve security?

(Select all acceptable answers.)

✅ 1. Everything on the site should use HTTPS instead of HTTP.

❌ 2. When resetting a user's password, send the user a new password instead of a password reset code.

✅ 3. Set an HTTP-only flag on the session cookie.

✅ 4. Show a CAPTCHA after several failed login attempts.

❌ 5. Replace UUIDs in URLs with sequential IDs.

❌ 6. Session tokens should never expire.

-----------

✅ 1. Everything on the site should use HTTPS instead of HTTP.

- **CORRECT.** _Hypertext Transfer Protocol Secure (HTTPS) is the secure version of HTTP._ It acts like a fortified communication channel between the web browser and a website. HTTPS uses **_Transport Layer Security (TLS)_** to encrypt the data you send and receive, making it unreadable to anyone who might intercept it. This is in contrast to regular HTTP, which transmits data in plain text, leaving it vulnerable to eavesdropping. Therefore, it **makes the website more secure**.

-----------

❌ 2. When resetting a user's password, send the user a new password instead of a password reset code.

**- INCORRECT.** By sending the user a new password, anyone who has access to the user's email will be able to see the new password. Therefore, it is more secure to send a password reset code.

-----------

✅ 3. Set an HTTP-only flag on the session cookie.

- **CORRECT.** The HttpOnly flag is a _security measure that makes cookies inaccessible via JavaScript._ Without this protection, the website could easily suffer a **Cross-site Request Forgery attack**, also known as CSRF - a type of attack where a malicious actor forces users to submit an unwanted request to an application they are logged in.

**_How do you set the HttpOnly flag?_**

The specific method depends on the server-side language you're using. Consult the documentation for your chosen framework or language for detailed instructions.
In Java, for example, you can use the javax.servlet.http package to create it:

```java
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServletResponse;

public class MyServlet {

    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        
        // Set cookie name and value
        String cookieName = "myToken";
        String cookieValue = "your_token_value";
        
        // Create a cookie object
        Cookie cookie = new Cookie(cookieName, cookieValue);
        
        // Set HttpOnly flag
        cookie.setHttpOnly(true);
        
        // Set expiration time (optional)
        cookie.setMaxAge(60 * 60 * 24); // Expires in 24 hours
        
        // Add cookie to the response
        response.addCookie(cookie);
        
        // ... (rest of your servlet code)
    }
}
```

----------

✅ 4. Show a CAPTCHA after several failed login attempts.

**- CORRECT.** The CAPTCHA can help verify that the application is being accessed by real humans, and not under attack. By presenting a CAPTCHA after a certain number of failed login attempts, the website makes it more difficult for automated scripts to crack passwords through brute-force attacks.

------------

❌ 5. Replace UUIDs in URLs with sequential IDs.

**- INCORRECT.** _Sequential IDs would make the website LESS secure._ 

Both sequential IDs and UUIDs are used to identify items in a database. 

E.g. - an e-commerce URL might look like this: 

```http
https://ecommerceurl.com/product_1234
```
_or_ 

```http
https://ecommerceurl.com/product_3a1b2c4d-e5f6-g7h8-i9j0-k1l2m3n4o5p6
```

Where _"product_1234"_ and _"product_3a1b2c4d-e5f6-g7h8-i9j0-k1l2m3n4o5p6"_ are the product identifiers in the e-commerce database.

The difference between them is that:

**_- Sequential IDs:_** As the name says, they follow a sequence of characters, like "1234" or "abcd", which makes the ID more predictable for malicious actors and, therefore, less secure.

**_- UUIDs:_** UUIDs are 128-bit identifiers generated according to a specific standard (RFC 4122) to ensure they are extremely unlikely ever to collide.
They are typically represented as hexadecimal strings with a specific format (e.g., "3a1b2c4d-e5f6-g7h8-i9j0-k1l2m3n4o5p6").

Due to their random nature, UUIDs are very difficult to guess, offering strong protection against unauthorized access.

So changing from UUIDs to Sequential IDs wouldn't help with the security.

------------

❌ 6. Session tokens should never expire.

**- INCORRECT.** _Session Tokens (A.K.A. **cookies**) should ALWAYS expire._ Despite it being much nicer and comfortable to go to your favorite website and not have to log in again because it already recognizes you, session tokens that don't expire can represent a security threat to website users. Here's why:

| Increased Attack Window: A non-expiring token essentially becomes a permanent "key" to your account. If an attacker gains access to this token (through malware, phishing, etc.), they can potentially impersonate you and access your account for an indefinite period.|
|Lost or Stolen Device: If you lose your device or it's stolen, anyone who gains access to it will also have access to your account for as long as the token remains active.|
|Public/Shared Devices: Using a public or shared computer with a non-expiring token poses a risk. Someone else could access your account if they haven't cleared the cookies after their session.|

As a best practice, always implement a reasonable expiration time for session tokens to enhance your website's security.  Consider factors like user behavior and the sensitivity of data when choosing an appropriate expiration duration.  Explore server-side language functionalities to set expiration times for your cookies.

------------

Thank you so much for your time! If you think something is missing or would like to correct/add more information, please feel free to submit a pull request.

See you next time!


      SQL Injection
      Cross-site Scripting
      
# Network Security
## Spoofing Attack on an Email Server

Employees of a company are facing lots of bounced email notifications from email addresses they have never sent messages to. Select the options below which are correct for the given scenario.

Options:

**ALTERNATIVES**

❌ 1. The mailboxes of the company users are full, resulting in bounced emails.

✅ 2. Company email addresses seem to have been spoofed and used for spamming. 

✅ 3. An email authentication method like DKIM can be used to prevent such incidents.

❌ 4. SMTP would prevent such incidents as emails can be sent reliably using it.

❌ 5. Having more than one email server would reduce such email bouncing incidents.

-----------

**EXPLANATION**

This question shows a case of **_email spoofing_**, meaning someone is sending emails pretending to be them through the manipulation of the "from" address in the email header. 

In simple terms, "email spoofing" is a tactic that tricks email users into thinking they have received an email from a source they know or trust, so they will open or respond to it. Basically, the email the receiver "sees" is different from the email that actually sent the spam message.

Spoofing can be considered a form of **_identity theft_** and can involve phishing. However, phishing doesn't necessarily involve spoofing.

In addition, email spoofing itself isn't generally considered hacking, because it doesn't involve breaking into a computer system to gain unauthorized access.

❌ 1. The mailboxes of the company users are full, resulting in bounced emails.

- **INCORRECT.** While some of the mailboxes _could_ be full, some recipient servers have filters that analyze incoming emails to identify possible spamming - if the email triggers the filter, it is rejected.

-----------

✅ 2. Company email addresses seem to have been spoofed and used for spamming. 

- **CORRECT.** _There are clear indications of spoofing._ They have received bounced email notifications from emails they never messaged, which could mean someone added their email address in the RETURN-PATH (used to specify where bounced emails are sent).

-----------

✅ 3. An email authentication method like DKIM can be used to prevent such incidents.

- **CORRECT.** DKIM stands for **_DomainKeys Identified Mail_** and is an authentication system that adds digital signatures to emails to ensure they are from a trusted source and haven't been forged or altered during transmission.

The DKIM can be set manually, but some email providers already handle it for you.

-----------

❌ 4. SMTP would prevent such incidents as emails can be sent reliably using it.

- **INCORRECT.** _Simple Mail Transfer Protocols (SMTP) is designed for efficient email delivery._ It doesn't verify the sender's identity or authentication. Hence, it wouldn't prevent spoofing from happening.

-----------

❌ 5. Having more than one email server would reduce such email bouncing incidents.

- **INCORRECT.** Having more email servers **_wouldn't_** reduce the bounced email notifications because the attacker isn't sending the emails from your email servers. Hence, more email servers wouldn't make a difference in this case.

-----------   

Thank you so much for your time! If you think something is missing or would like to correct/add more information, please feel free to submit a pull request.

See you next time!


## Network Security: IP Protection
# IP Protection

Select the methods that can be used to **hide your public IP address** when making calls to a remote server over the internet.

(Select all acceptable answers.)


✅ 1. A Virtual Private Network.


✅ 2. A Proxy Server.


❌ 3. Using the HTTPS protocol.


❌ 4. The Transport Layer Security protocol.


❌ 5. Spoofing the device's MAC address.

--------

## ANSWERS

The question above inquires about **_IP address security_**.Therefore, it is important to understand what is an IP address.

An Internet Protocol (IP) address is a _unique identifying number_ that identifies a device's connection on a network. It acts like a digital address, allowing devices to find and communicate with each other. The Internet Service Provider (ISP) typically assigns the IP address.

**Fun fact:**

There are two main types of IP addresses:

**_Static IP:_** This type of IP address remains the same even when you disconnect and reconnect to the network. It's usually used for servers or devices that need a permanent online identity.

**_Dynamic IP:_** This is the more common type. Your ISP assigns a dynamic IP address that can change periodically, often when you restart your router or modem.

So, while your IP address can change depending on the network type (home, work, coffee shop), it's not guaranteed to change every time you connect to a different network, especially if you have a static IP.

Now, let's dissect the alternatives!

------------

✅ 1. A Virtual Private Network.

**- CORRECT.** A Virtual Private Network, A.K.A. _VPN_ is a privacy tool that creates a secure tunnel for your internet traffic by encrypting your data and **masking your IP address** with a remote server's IP. Hence, you can use it to hide your own IP.

------------

✅ 2. A Proxy Server.

**- CORRECT.** _A proxy server acts as a middleman between your device and the internet._ When you request a website, it goes to the proxy server first. The proxy server then fetches the website and returns it to you. This way, the website only sees the IP address of the proxy server, not your own. Proxy servers can be _hardware_ or _software_.

------------

❌ 3. Using the HTTPS protocol.

**- INCORRECT.** _Hypertext Transfer Protocol Secure (HTTPS) is the secure version of HTTP._ It acts like a fortified communication channel between your **web browser** and a **website**. HTTPS uses Transport Layer Security (TLS) to encrypt the data you send and receive, making it unreadable to anyone who might intercept it. This is in contrast to regular HTTP, which transmits data in plain text, leaving it vulnerable to eavesdropping.

It's important to note that while HTTPS encrypts your data, **it doesn't hide your IP address.** The website you connect to can still see your IP address.

In addition, the HTTPS protocol is added to a website by the **Website administrator**. Therefore, as a user, the only thing you can do is access websites that have the HTTPS protocol.

------------

❌ 4. The Transport Layer Security protocol.

**- INCORRECT.** The Transport Security Layer protocol - formerly known as Secure Sockets Layer (SSL) - ensures that the data you send over the internet is **encrypted**. Still, it doesn't hide your public IP address.

------------

❌ 5. Spoofing the device's MAC address.

**- INCORRECT.** The MAC address identifies a physical device on a network, not the device's connection on a network. It is encoded by the Network Interface Card (NIC) manufacturer in a piece of hardware called the Network Interface Controller, that connects a computer to a network. Unlike the IP address, which can be dynamic and assigned by your ISP, a MAC address is typically PRIVATE and FIXED.

Since they are two different things, even if you spoof your MAC address, **the IP address will still be visible unless you use a VPN or Proxy Server.**

Minor Point:

It's important to note that MAC addresses _can be spoofed_ (changed) on some devices, though it's not a common practice. 

------------

Thank you so much for your time! If you think something is missing or would like to correct/add more information, please feel free to submit a pull request.

See you next time!


# Prevent Vulnerabilities With Security Testing Techniques

This table provides a concise overview of various security testing techniques, outlining their focus and approach.

##  Methodology
The table will list common security testing techniques in one column, with a corresponding one-sentence description in the next column explaining the technique's target area and testing method.

| TYPE OF TESTING | DESCRIPTION | KEY FOCUS | METHODOLOGY | MOST USED TOOL | 
|---------|---------------|-----------|------------|---------|
| Vulnerability Scanning | Automated process to identify known vulnerabilities in systems, applications, or networks | Finding weaknesses based on predefined patterns | Scans for vulnerabilities in code, configuration, or network devices | Nessus |
| Penetration Testing (Ethical Hacking) | Simulates real-world attacks to identify exploitable vulnerabilities | Uncovering critical security issues an attacker might use | Ethical hackers attempt to gain unauthorized access using various techniques | Kali Linux |
| Security Code Review | Manual examination of code to identify security flaws | Detecting vulnerabilities in code during development | Security professionals analyze code for common coding errors and security weaknesses | N/A (Manual process) |
| SAST (Static Application Security Testing) | Analyzes source code without running the application | Finding vulnerabilities early in the development lifecycle | Examines code for patterns and weaknesses without executing it | Fortify on Demand |
| DAST (Dynamic Application Security Testing) | Tests running applications to identify vulnerabilities | Discovering vulnerabilities during runtime by simulating user interaction | Scans a running application for vulnerabilities by injecting malicious code or data | Burp Suite |
| Risk Assessment | Evaluates the likelihood and impact of potential security threats | Prioritizing security efforts based on potential risks | Analyzes threats, vulnerabilities, and potential consequences | N/A (Framework based) | 
| Security Posture Assessment | Broad evaluation of an organization's overall security posture | Identifying weaknesses across different security controls | Assesses security policies, procedures, and technical controls | SecurityScorecard |

## Conclusion
By strategically utilizing these diverse security testing techniques, organizations can proactively identify and address vulnerabilities, bolstering their overall cyber resilience.



# 9. API
     Validation
     Functional
     UI
     Load
     Security
     Runtime Error/Detection
     Penetration
     Fuzz
     Interoperability
     Tools
# Test APIs With Postman, SoapUI, And JMeter

The table below compares the main differences between Postman, SoapUI, and JMeter for API testing.

## Methodology
The table will list the three tools, their API support, a brief description of their key functionalities, and use case examples.

| FEATURE | POSTMAN | SOAPUI | JMETER |
|--------|--------|---------|---------|
| **Primary Focus** | Functional API Testing | Functional & Non-Functional API Testing | Performance Testing (with Functional Testing capabilities) | 
| **Strength** | User-friendly interface | Advanced testing features | Scalable load testing |
| **API Type Support** | RESTful APIs (primarily), SOAP |	RESTful & SOAP APIs |	RESTful & SOAP APIs |
| **Scripting** | Supports various languages (JavaScript, Groovy etc.)	| Supports Groovy	| Supports various languages (Java, Python etc.) |
| **Collaboration** | Team workspaces, sharing collections | Limited collaboration features | Not designed for collaboration |
| **Cost** | Freemium (Basic features free, Paid plans for advanced features) | Free and Open-Source | Free and Open-Source |
| **Requires Programming Knowledge** | No | Optional, but helpful for advanced features | Yes (Java for advanced scripting) | 
| **Use Case Examples** | * Testing basic functionality of a new REST API  * Sending quick API requests to verify data | * Testing complex SOAP web services  * Automating functional testing with Groovy scripts  * Security testing of APIs | * Simulating high user loads on an API  * Performance testing of a critical API endpoint |

## CONCLUSION
- Postman: Ideal for beginners, quick tests, and collaborative API development.
- SoapUI: Well-suited for complex APIs, functional & non-functional testing, and scripting.
- JMeter: Best for performance testing, load simulations, and integrating with CI/CD pipelines.

For many testers, a combination of these tools might be ideal. Use Postman for exploratory testing and collaboration, SoapUI for complex scenarios, and JMeter for performance testing.

