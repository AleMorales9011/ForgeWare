![banner](images/6.jpg)

# SDLC & Testing

10 minutes

The `Software Development Lifecycle` is a process used to create software that meets the stakeholders' requirements.
It comprises six core phases: `Planning`, `Design`, `Development`, `Testing`, `Deployment`, and `Maintenance`.

Testing & QA throughout the entire SDLC:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/1e9d2107-61f6-4e98-ad4f-14ecb8ef0fdf)

# Testing Throughout the SDLC

|  Planning       |  Design             |  Development        | Testing            | Deployment       | Maintenance        |
|-----------------|---------------------|---------------------|--------------------|------------------|--------------------|
| `Feedback`      | `Feedback`          | Write Test Plan     | `Write` Test Cases | Validation       | `Regression`       |
|                 |                     |                     | `Set up` Test Environment |    Monitoring         |  Monitoring  |
|                 |                     |                     | `Execute` Cases  |                     |        |
|                 |                     |                     | Analysis & Reporting |                  |                    |
|                 |                     |                     | Fix bugs & Retest       |                  |                    |


# Agile Methodologies Differences

- Scrum has a fixed-length Sprint cycle, while Kanban is continuous.
- Scrum has dedicated review and retrospective ceremonies, while Kanban uses daily stand-up meetings for continuous improvement.
- Testing in Scrum is integrated throughout the Sprint, while Kanban testing is continuous throughout the workflow.

# Test Techniques, Types, and Levels

- Execution: manual or automated.
  
- Techniques: Specific methods used to execute tests - White Box, Black Box, Experience-based.

- Types: Categories of testing based on different objectives - Functional, Non-functional.

- Levels: Stages of testing within the software development lifecycle - Unit, Integration, System, Performance, Acceptance, UI.

- Design Strategies: Approaches used to create test cases - a subset of black-box, white-box, and experience-based. (not in the image).

<img width="723" alt="stw test types" src="https://github.com/user-attachments/assets/801d246a-ccbf-4927-920b-57acaaabe740">

# Functional

Evaluates the functions that a component or system should perform.

| LEVEL | DESCRIPTION | 
|-----------|-------------|
| Unit Testing | Tests individual units of code (functions, modules) | 
| Integration Testing | Tests how different units interact with each other.| 
| System Testing | Tests the entire system as a whole. |
| Acceptance Testing | Verifies if the system meets user requirements. | 

# Non-Functional

Evaluates attributes other than functional characteristics of a component or system. It tests “how well the system behaves”.

| LEVEL | DESCRIPTION |
|-----------|-------------|
| Performance Testing | Evaluates system performance under load. | 
| Usability Testing | Evaluates user experience with the software. |
| Mutation Testing | Introduces deliberate errors (mutations) in the code and checks if tests detect them. |
| Capture-Replay Testing | Records user interactions and replays them for regression testing. |

# Black-box 

Also known as `specification-based` techniques. They are based on the behavior of the test object without reference to its internal structure. Therefore, they are independent of how the software is implemented. Consequently, if the implementation changes, but the required behavior stays the same, the test cases are still useful. 

# Example: Decision Table Testing

Decision table testing is a method to identify test cases based on input conditions and their corresponding actions/outputs, especially used for complex requirements.

# Why is it important?

Decision tables provide comprehensive test coverage by considering all input combinations, helping uncover defects while improving test case design efficiency and clarity.

# How It Works

`1. Identify conditions and actions:` Determine the input conditions and potential outputs (actions) based on the system's behavior.

`2. Create a decision table:` Construct a table with conditions as columns and rows representing different combinations of conditions.

`3. Define rules:` Specify the actions to be performed for each combination of conditions.

`4. Design and execute test cases:` Create test cases based on the defined rules, then compare the results with the expected outcomes.

# Limitations
Decision table testing can become impractical for systems with many conditions, leading to an overwhelming number of test cases due to the exponential growth in possible combinations.

# White-box
Also known as `structure-based` techniques. They are based on analyzing the test object’s internal structure and processing. As the test cases are dependent on how the software is designed, they can only be created after the design or implementation of the test object. 

# Example: Branch Testing
Branch testing is a white-box testing technique that ensures every possible path through a code's decision points is executed at least once. A decision point is typically an 'if' or 'switch' statement where the program's flow can diverge based on the condition's outcome.   

Branch testing aims to cover all potential branches or outcomes of each decision point, guaranteeing that all reachable code is executed. Any set of test cases achieving 100% branch coverage also achieves 100% statement coverage (but not vice versa).

# Why is Branch Testing Important?
Comprehensive Coverage - testing all branches helps to ensure that all possible code paths are exercised, reducing the likelihood of hidden bugs.   

# How to Use Branch Testing
`1. Identify Decision Points:` Locate all `if`, `switch`, and similar statements in the code.
`2. Determine Branches:` For each decision point, identify the possible outcomes or branches.
`3. Design Test Cases:` Create test cases that specifically target each branch to ensure it's executed.   
`4. Execute Test Cases:` Run the test cases to cover all identified branches.
`5. Measure Coverage:` Calculate the branch coverage percentage to assess test effectiveness.

# Limitation
While high branch coverage is good for testing, 100% branch coverage can still miss verifying the correct behavior of the code if the test cases lack proper assertions or only use trivial input values.

# Experience-based 
They use testers' knowledge and experience to design and implement test cases. Experience-based testing can detect defects that may be missed with black-box and white-box. Hence, they are complementary to the other techniques.

# Example: Error Guessing 

Error Guessing is a software testing strategy where testers use their experience and intuition to `predict potential errors or defects` in an application. It's an informal approach based on the tester's ability to anticipate issues from past encounters with similar systems. 

# Why It Is Important

 Testers can focus on areas that might not be covered by formal test cases, providing a different perspective on the software.   

 # How It Works

Error guessing is a relatively unstructured process. Testers typically follow these steps:   

1. `Analyze the software`: Understand the system's functionality, requirements, and design.
2. `Identify potential problem areas`: Based on experience, intuition, and domain knowledge, guess where errors might occur.   
3. `Design and execute test cases`: Create and run test cases to specifically target these areas.
4. `Report and track defects`: Document found issues and track their resolution.

`Important Note`: While error guessing is valuable, it should not replace structured testing methods. A combination of both approaches is essential for comprehensive test coverage.   

# Bug Reporting

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/a2154d32-a72f-410b-b941-298b9680a1aa)

# API Testing

Application Program Interface (API) testing is a type of software testing that validates the behavior and performance of an application program interface. 

# Why It Is Important

API testing evaluates an API's ability to handle increased load and traffic. Testers can identify bottlenecks, latency issues, and resource constraints to optimize performance and ensure it can handle the expected user load.

# How it Works

1. `Understand the API`: Understand the API's functionalities, endpoints, data formats, authentication methods, and expected behaviors.
2. `Create Test Cases`: Develop test cases covering various scenarios, including positive, negative, boundary value, performance, and security tests.
3. `Set Up Test Environment`: Establish the necessary environment with appropriate tools, data, and API access.
4. `Execute Test Cases`: Run the tests.
5. `Analyze Results`: Evaluate test outcomes, compare actual results with expected results, and generate reports.
6. `Iterate and Improve`: Address identified defects, refine test cases, and automate where feasible.

# API Testing vs. API Method Testing
API testing covers all the testing activities on an API to ensure it functions correctly, reliably, and securely. It includes functional testing, performance testing, security testing, and more. On the other hand, API method testing focuses on testing the individual operations or endpoints of an API, such as creating, reading, updating, and deleting operations on a resource.

To summarize:

- `API testing` is the overall process of evaluating an API.   
- `API method testing` is a specific type of API testing that targets individual API endpoints.

In essence, API method testing is a component of API testing, just as unit testing is a component of software testing.
