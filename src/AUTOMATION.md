# Test Automation

Test automation is the use of software to execute test cases, validate results, and provide feedback. 

# Why It Is Important

 It replaces manual testing efforts, particularly for repetitive and time-consuming tasks, thereby enhancing efficiency and accuracy.

# How It Works

1. `Test Case Selection`: Identify test cases suitable for automation, prioritizing those with high execution frequency, critical business logic, or prone to human error.

2. `Tool Selection`: Choose test automation tools that align with project requirements, team expertise, and budget constraints. Consider factors such as ease of use, test coverage, reporting capabilities, and integration with other tools.   

3. `Test Environment Setup`: Establish a stable test environment to ensure reliable test execution.   

4. `Test Script Development`: Create reusable test scripts using appropriate scripting languages and frameworks.

5. `Test Execution and Analysis`: Integrate test automation into the development lifecycle, and analyze test results.s.

6. `Continuous Improvement`: Refine test automation processes to optimize efficiency and effectiveness.

# Automation Tools vs. Frameworks

This table clarifies the distinction between testing automation tools that directly interact with the application and testing automation frameworks that provide structure and support for building those tests.

| FEATURE | TESTING AUTOMATION TOOLS | TESTING AUTOMATION FRAMEWORKS | 
|---------|-----------------------------|--------------------------|
| **PURPOSE** | Provides functionalities to _automate test actions_ | Provides a structure and best practices for _building and managing test scripts_ |
| **FOCUS** | Execution and management of tests | Design and development of test scripts |
| **ABSTRACTION LEVEL** | Lower level - interacts with UI elements directly | Higher level - provides reusable components and libraries | 
| **CUSTOMIZATION** | Limited customization options | Highly customizable based on project needs |
| **EXAMPLES** | Selenium, Appium, SoapUI | Robot Framework,  TestNG,  Playwright |
| **CODING REQUIREMENTS** | May require some coding knowledge | Requires coding knowledge in a specific programming language |
| **COST**| Can be open-source or commercial | Mostly open-source |

## CONCLUSION
By differentiating between testing automation tools and frameworks, testers can select the most suitable option for crafting a reliable and sustainable test suite, ultimately optimizing their testing process.

# Choose the Right Testing Automation Tool

The table compares Selenium, Appium & SoapUI for test automation, highlighting their focus and core functionalities.

| FEATURE | SELENIUM | APPIUM | SOAPUI |
|----------|---------|---------|-------|
| **Primary function** | Automate web browsers | Automate mobile apps | Automate web service testing (SOAP & REST) |
| **Focus** | Front-end (user interface) | Mobile app functionality | Back-end (application logic) |
| **Supported Technologies** | Web browsers (Chrome, Firefox, etc.) | Native, hybrid, and web mobile apps | SOAP and REST APIs | 
| **Scripting Languages** | Multiple (Java, Python, C#, Perl, and PHP) | Multiple (Java, Python, JavaScript, Ruby, and C#) | Groovy (primarily) | 
| **Open-source** | Yes | Yes | Free open-source version, paid commercial version with additional features |
| **Learning Curve** | Medium (depends on scripting language) | Medium (depends on scripting language and mobile app development concepts) | Easy to learn for basic testing, a steeper curve for complex scenarios |
| **Ideal Use Case** | Automating web application workflows, regression testing | Automating mobile app functionalities and user journeys | Automating mobile app functionalities and user journeys | Functional testing, performance testing, security testing of web services |
| **Use Case Examples** | Testing login functionality, simulating user interactions, validating web page elements | Testing mobile app features, automating taps, swipes, and gestures | Testing API functionality, sending requests, validating responses |
| **Programming Knowledge** | Requires programming knowledge | Requires programming knowledge | Doesn't require programming knowledge (drag-and-drop interface with scripting option) |
| **Supported Test Types** | Functional testing, regression testing, cross-browser testing, usability testing | Functional testing, regression testing, compatibility testing, installation testing | Functional testing, security testing, performance testing, load testing |
| **Complementary** | Can be used with SoapUI for API testing in conjunction with UI testing | Can be used with Selenium for web UI testing in conjunction with mobile app testing | Can be used with Selenium for comprehensive web application testing (UI & back-end) |

## CONCLUSION

The choice between Selenium, Appium, and SoapUI depends on the target application type and the desired functionalities like browser automation or API testing. All three tools offer robust solutions for test automation within their respective domains.

# SELENIUM 
# Selenium Basics
Selenium WebDriver: Grasp its architecture, how it interacts with browsers, and core commands.
Locators: Master different locator strategies (ID, name, XPath, CSS selector) for efficient element identification.
Web Elements: Learn to interact with various web elements (text boxes, buttons, links, etc.)
Waits: Understand implicit, explicit, and fluent waits to handle asynchronous operations.
Handling Frames and Windows: Practice switching between frames and windows.

# Test Automation Framework
Test Automation Framework Design: Learn about the importance of a good framework structure.
Page Object Model (POM): Implement POM for better code organization and maintainability.
Data-Driven Testing: Parameterize tests with data for efficient test execution.
TestNG or JUnit: Choose a testing framework for test management and reporting.

# Phase 4: Advanced Selenium Topics
Cross-Browser Testing: Explore tools and techniques for testing on different browsers.
Selenium Grid: Learn how to distribute test execution across multiple machines.
Test Automation Best Practices: Follow industry standards for robust and efficient automation.
Continuous Integration (CI): Integrate Selenium tests into CI pipelines.

# Phase 5: Specialization
Performance Testing with Selenium: Combine Selenium with performance testing tools (optional).
Mobile Testing with Selenium: Explore Selenium's capabilities for mobile app testing (optional).
Image-Based Testing: Learn techniques for handling image verification (if required).
Cloud-Based Testing Platforms: Explore platforms like Sauce Labs or BrowserStack (optional).








Introduction Selenium

First Steps in Selenium

Test Case Design: Login
Steps
1.	Open the URL
2.	Find the email field
3.	Write the email
4.	Find the pass field
5.	Write the pass
6.	Find the “Ingresar”button
7.	Click in the “Ingresar”button

Folder structure
Main: Only for software development
Test: Only for test
Pom.xml: For dependencies configuration

Search dependencies 
1.	Go to mvnrepository
2.	Search selenium
3.	Find the last version and copy maven dependency

Selenium dependencies is the VIP
 
Refresh the pom.xml file after modifications

First Test

1.	Invoking Browser
There are two ways to invoke the browser:
-	ChromeDriver driver = new ChromeDriver ();
-	WebDriver driver = new ChromeDriver ();
The difference is that when writing the Chrome driver, the first way, that line may not work in other browsers, since you are only accessing the methods of the Chrome driver class. Classes like FirefoxDriver, ChromeDriver, EdgeDriver, SafariDriver, implement the WebDriver interface. 
That's why the correct way to write that line is as follows:
 
The ChromeDriver class alone cannot lift the Chrome browser to execute Selenium tests, for that you need to invoke the Chromedriver.exe file.

To perform that operation there are two forms:

a.	Write a step to invoke the .exe
System.setProperty ("webdriver.chrome.driver", "path of the .exe on your computer")
To get the .exe you must go to the next website googlechromelabs.github.io/chrome-for-testing/ to download the .exe compatible with your browser. 
Which version download? The one that is equal to the version of your current chrome
b.	Use the incorporated selenium manager of ChromeDriver. This Liberia checks if there is any step to invoke the ChromeDriver. If there is no defined step, connect to the web and download the appropriate controller automatically and place it on the right route.

What is the difference between one form or the other? In the first case, when the ChromeDriver is called, the Selenium Manager will remain deactivated, since we are already giving it a local route to access the browser. Therefore, it will be a slightly faster alternative to the second option, since you will not have to access the web and locate a compatible browser.

Either method is correct.

Troubleshooting steps if you fail to invoke chrome browser with Selenium

If you see any errors in invoking chrome browser, please perform below troubleshooting step to make it work:
	Update your Chrome browser and Selenium version to latest and run again
If it still didn’t work, then add System.setProperty() step and get the exact ChromeDriver version which matches with your Chrome browser version and run again, it will work for sure 😊

2.	Open the URL
1. Invoke the browser using driver.get

2. Use the findElement(By) and sendKeys methods to locate the desired element and perform the typing action on said element.

3.	The sendKeys method will help you simulate writing on an element, so through this method, we will send the user's credentials to log in to RedyPago.
4.	
5.	Remember that all elements on a website do not have to be identified with the same attributes. Some may have id and others may not. In those cases, any of the other options that Selenium accepts could be used as a locator.
6.	
7.	findElement (By.name (""))
8.	findElement (By.class (""))
9.	
10.	In the case of classes, you can find something like this:
11.	
12.	<button class="btn btn-success font-weight-bold py-4 w-100" id="kt_login_signin_submit" style="background-image: linear-gradient(to right,#019c80,#2c6572); background-repeat : no-repeat">Enter</button>
13.	
14.	As you can see, the value of the class attribute is separated by spaces, that means that several classes affect that button. So, which one to select to identify this element? Well, any of them, the one that seems most unique to you.
15.	
16.	3. Click on the Enter button to log in
17.	
18.	Once we have located the button element we only have to use the click method.
1.	Close the browser
There are two ways to close the browser
•	driver.close ()
•	driver.quit ()
But there is a thin line of difference between Close and Quit. Close, will only close the first window that opened to perform the test. Meanwhile, QUIT will close all the associated windows that opened during automation.


Selenium Web Driver Locator

As part of Automation, Selenium Performs actions (such as click, typing) on the Page HTML Elements. The Locators are the way to identify an HTML element on a web page. Selenium WebDriver uses any of the below locators to identify the element on the page and performs the Action.
1.	ID
2.	Xpath
3.	CSS Selector
4.	name
5.	Class Name
6.	Tag Name
7.	Link Text
8.	Partial Link Text

How to extract those locators from each element of the web? You just have to inspect the page and with the pointer activated, select on the web the component to which we want to copy its locator and we will find that information in the Elements tab

 

How to extract those locators from each element of the web? You just have to inspect the page and with the pointer activated, select on the web the component to which we want to copy its locator and we will find that information in the Elements tab.

You should find something like this, depending on the item you select.
<input type="text" placeholder="Username" id= “inputUsername” value=" ">

Once we have this information, we only need to select from there, a locator to use in our tests with Selenium and since the ID attribute is recognized by Selenium, it will be our locator

attribute (Java) = locator (Selenium)

Xpath and CSS Selector
CSS Selector
Ways to create a CSS Selector:
1.	Class Name: tagname.classname Ex: button.signInBtn
2.	Id: tagname#id Ex: input#inputUserName
3.	Without id or class name: tagname[attribute = ‘value’] Ex: input[placeholder=’Username’]

Xpath
Way to create a Xpath:
1.	//tagname[@attribute= ‘value’] Ex: //input[@placeholder=’Username’]
2.	//tagname[@attribute= ‘value’][index] Ex: //input[@placeholder=’Username’][2]
3.	//parent/childTagname Ex: //form/input




