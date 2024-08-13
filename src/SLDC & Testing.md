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

- Design Strategies: Approaches used to create test cases (not in the image).

<img width="723" alt="stw test types" src="https://github.com/user-attachments/assets/801d246a-ccbf-4927-920b-57acaaabe740">

# Functional

Evaluates the functions that a component or system should perform.

| TECHNIQUE | DESCRIPTION | 
|-----------|-------------|
| Unit Testing | Tests individual units of code (functions, modules) | 
| Integration Testing | Tests how different units interact with each other.| 
| System Testing | Tests the entire system as a whole. |
| Acceptance Testing | Verifies if the system meets user requirements. | 

# Non-Functional

Evaluates attributes other than functional characteristics of a component or system. It tests “how well the system behaves”.

| TECHNIQUE | DESCRIPTION |
|-----------|-------------|
| Performance Testing | Evaluates system performance under load. | 
| Usability Testing | Evaluates user experience with the software. |
| Mutation Testing | Introduces deliberate errors (mutations) in the code and checks if tests detect them. |
| Capture-Replay Testing | Records user interactions and replays them for regression testing. |

# Black-box 
Also known as `specification-based` techniques. They are based on the behavior of the test object without reference to its internal structure. Therefore, they are independent of how the software is implemented. Consequently, if the implementation changes, but the required behavior stays the same, the test cases are still useful. 

# White-box
Also known as `structure-based` techniques. They are based on analyzing the test object’s internal structure and processing. As the test cases are dependent on how the software is designed, they can only be created after the design or implementation of the test object. 

# Experience-based 
They use testers' knowledge and experience to design and implement test cases. Experience-based testing can detect defects that may be missed with black-box and white-box. Hence, they are complementary to the other techniques.

# Test Case Design Strategies

![image](https://github.com/user-attachments/assets/f4cae73d-8573-4484-9d45-61520511d3fc)

# White-Box

# 1. Branch Testing
Branch testing is a white-box testing technique that ensures every possible path through a code's decision points is executed at least once. A decision point is typically an 'if' or 'switch' statement where the program's flow can diverge based on the condition's outcome.   

Branch testing aims to cover all poten tial branches or outcomes of each decision point, guaranteeing that all reachable code is executed. Any set of test cases achieving 100% branch coverage also achieves 100% statement coverage (but not vice versa).

# Why is Branch Testing Important?
Comprehensive Coverage - testing all branches helps to ensure that all possible code paths are exercised, reducing the likelihood of hidden bugs.   

# How to Use Branch Testing
`1. Identify Decision Points:` Locate all `if`, `switch`, and similar statements in the code.
`2. Determine Branches:` For each decision point, identify the possible outcomes or branches.
`3. Design Test Cases:` Create test cases that specifically target each branch to ensure it's executed.   
`4. Execute Test Cases:` Run the test cases to cover all identified branches.
`5. Measure Coverage:` Calculate the branch coverage percentage to assess test effectiveness.

# Limitation
"While high branch coverage is good for testing, 100% branch coverage can still miss verifying the correct behavior of the code if the test cases lack proper assertions or only use trivial input values."

# Black Box

# Decision Table Testing

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

# 4. State Transition

State transition testing examines how a system moves from one state to another in response to events, focusing on the system's behavior under different input conditions and sequences. State transition testing is particularly useful for systems with complex state-dependent behavior, such as vending machines, traffic lights, or software with multiple user modes.

# Why is it important?

State transition testing is important for identifying system errors caused by unexpected state changes.

# How It Works 

`1. Review the specifications/requirements:` It will help understand how the system is expected to behave.

`2. Identify system states, events, and transitions:` Identify all the states the system can be in, the events that trigger them, and the transitions that are supposed to occur once those events happen.

`3. Create state transition diagrams:` They will provide a clear overview of the software's expected behavior.

`4. Derive the test cases:` Use the state transition diagrams to derive the necessary test cases.

`5. Execute and analyze the test results:` Perform the test cases and record the actual system behavior, then compare the actual results with the expected results. Identify any discrepancies or unexpected behavior. Investigate failed test cases to determine the root cause of the issue.

# Example Tools

`Selenium`, `Appium`: Can automate interactions with the system to trigger state transitions and verify outcomes.

`JUnit`, `TestNG`: For unit testing and creating test cases based on state transitions.

`Cypress`, `Playwright`: Modern end-to-end testing frameworks that can be used for state-based testing.

# Limitations

State transition testing can be complex and time-consuming for systems with many states and transitions.

# 5. Use Case

Use case testing is a black-box testing technique that focuses on testing the system based on user interactions. It involves deriving test cases from the system's use cases, which describe how users interact with the system to achieve specific goals.

Why is it important?

User-centric: Ensures the system meets user needs and expectations.
Comprehensive testing: Covers various system functionalities and interactions.
Risk reduction: Helps identify potential issues early in the development process.
How to use it?

Identify use cases: Determine the primary functions of the system from the user's perspective.
Create test cases: Develop test cases based on the steps and scenarios outlined in the use cases.
Execute test cases: Perform tests to verify system behavior according to the use cases.
Analyze results: Evaluate test results to identify defects and ensure system functionality.
Use case testing helps to validate the system's behavior from a user's standpoint, increasing the likelihood of delivering a successful product.

# 6. Error Guessing
# 8. Combinatorial
# 9. Pairwise


# Bug Reporting

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/a2154d32-a72f-410b-b941-298b9680a1aa)



