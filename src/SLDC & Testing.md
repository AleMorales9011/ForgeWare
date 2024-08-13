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
| `Feedback`      | Feedback            | `Review`            | Writing Test Cases | Validation       | `Regression`       |
|                 |                     |                     | `Executing` Cases  | Monitoring       | Monitoring         |
|                 |                     |                     | Analysis           |                  |                    |
|                 |                     |                     | Reporting          |                  |                    |

# Execution

1. Design the test case.
2. Set up the test environment.
3. Execute the test.
4. Report results and bugs.
5. Fix bugs and retest.
6. Clean up the test environment.

# AGILE TESTING

The table below compares the Scrum and Kanban frameworks, highlighting key structural differences and the tester's role within each.

# Methodology

The table will have four columns: "Stage", "Scrum", "Kanban", and "Role of "Tester". Rows include aspects like project structure, work planning, and the tester's role (e.g., dedicated testing phase vs. continuous testing throughout).

| STAGE | SCRUM | KANBAN | ROLE OF TESTER |
|-------|------|-----|----|
| Planning | **- Product Backlog refinement:** Testers participate in defining acceptance criteria for user stories. **- Sprint Planning:** Testers estimate testing effort and collaborate on the Sprint Backlog. | **Ongoing process:** Testers collaborate with the team to understand upcoming features and provide input on testability. | Testers help define what "done" means for a user story from a quality perspective. |
| Development | Development team works on the Sprint Backlog. | Work items continuously move through the Kanban board. | Testers actively participate in development discussions to **understand implementation details.** They design and execute test cases based on acceptance criteria. |
| Review & Retrospective (Scrum) | Team showcases completed work from the Sprint in a Sprint Review. **Testers provide feedback** on the quality of the delivered increment. | Daily Stand-up Meetings | **Testers report progress** on testing tasks and identify any blockers. |
| Testing (implicit in Scrum) | No dedicated testing stage. Testing happens throughout the Sprint. | Testing happens throughout the workflow. Testers collaborate with developers to fix bugs promptly. | Testers **execute test cases and identify and report bugs.** They collaborate with developers to ensure quality throughout the process. |
| Release (Scrum) | Potentially shippable product increment at the end of the Sprint. | Continuous Delivery | **Continuously deliver work items** to production as they are completed and tested. |
| Improvement | Sprint Retrospective: The team reflects on the Sprint and **identifies areas for improvement**, including testing practices. | Continuous Improvement: Testers participate in Kanban board optimization and identify ways to improve testing efficiency. | Testers suggest improvements to testing tools, processes, and communication. |

**Key Differences:**

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

# 1. Statement Coverage Testing
Statement coverage ensures every line of code is executed at least once during testing, focusing on covering all statements within the code.

# Why it is important:
Identifying untested code areas helps reduce the risk of undiscovered bugs.

# How it works:
1. Identify statements: All executable statements in the code are identified.
2. Design test cases: Test cases are created to execute each statement at least once.
3. Execute test cases: The test cases are run, and the code coverage tool records which statements were executed.
4. Calculate coverage: The percentage of executed statements compared to the total number of statements is calculated.

# Example:
```Python
def is_even(number):
  if number % 2 == 0:
    return True
  else:
    return False
```

To achieve 100% statement coverage, you would need two test cases: one with an even number and one with an odd number.

# Limitations of Statement Coverage:
1. Ignores logical conditions: It doesn't guarantee that all possible conditions within statements are tested.
2. Doesn't ensure complete testing: High statement coverage doesn't necessarily mean the software is bug-free.

# Additional Considerations:
1. Other coverage metrics: While statement coverage is a starting point, consider using other metrics like branch coverage, condition coverage, and path coverage for more comprehensive testing.
2. Tool support: Many testing frameworks and tools provide code coverage analysis capabilities.

# 2. Decision Coverage

Decision coverage tests every possible outcome of each decision point (typically `if`, `else`, `switch`, or ternary operators) in the code. While it can be applied at other testing levels, its most effective use is at the unit testing stage.

# Why is it important?

Ensuring all decision paths are tested helps uncover potential defects related to conditional logic.   

# How to use it?

`1. Create test cases:` Design test cases to cover all possible outcomes for each decision point identified.

`2. Instrument your code:` Use a code coverage tool to track which parts of the code are executed.

`3. Execute test cases:` Run the test cases with the instrumented code.

`4. Generate coverage report:` The code coverage tool will produce a report indicating which decision points were covered and which were not.

`5. Analyze report:` Review the report to identify areas with low decision coverage and create additional test cases as needed.

# Example tools:

_Unit Tests:_

`Python`: `Coverage.py`

`Java`: `JaCoCo`

`C#`: `Visual Studio Code Coverage`

`JavaScript`: `Istanbul`

_Multiple test types:_

`Parasoft Jtest:` This tool is designed for thorough testing, including unit, integration, and other test levels. It offers detailed coverage analysis across different test suites.

`SonarQube:` The platform can integrate with testing tools to provide coverage metrics at different test levels, including unit, integration, and system tests.

# Limitations

This method increases test thoroughness but `may not find all logical errors`, potentially requiring more test cases.

# 3. Condition Coverage

Condition coverage ensures that each part of a condition in a decision point (e.g., if, else) is evaluated as both true and false at least once.   

# Why is it important?

It helps identify potential errors in complex conditions by testing all possible outcomes of each condition.   

# How to use it?

1. Identify conditions within decision points.
2. Create test cases to evaluate each condition as both true and false.
3. Execute test cases and analyze results.

# Decision Coverage vs. Condition Coverage

`Decision coverage` focuses on the overall outcome of a decision (true or false). It ensures that both branches of a decision are executed at least once.   

`Condition coverage` focuses on the individual conditions within a decision. It requires that each part of a condition is evaluated as both true and false at least once.   

Example:

Consider the following code:

```java
if (A && B) {
  // do something
} else {
  // do something else
}
```

Decision coverage would require two test cases: one where A && B is true, and one where A && B is false.

Condition coverage would require four test cases:
- A is true, B is true
- A is true, B is false
- A is false, B is true
- A is false, B is false

Condition coverage is a more detailed testing approach for decision logic. Decision coverage ensures both branches are executed, while condition coverage tests every part of the decision's logic.

# 4. Multiple Condition Coverage (MCC)

MCC is a testing technique that ensures all possible combinations of conditions within a decision point are tested. It's more rigorous than condition coverage, which only requires evaluating each condition as true and false.

# Why is it important?

MCC helps uncover missed defects by finding unexpected condition interactions.

# How it Works

`1. Identify decision points:` Determine the decision points in the code with multiple conditions.

`2. Create truth table:` For each decision point, create a truth table listing all possible combinations of condition values.

`3. Design test cases:` Based on the truth table, design test cases to cover every possible combination of conditions.

`4. Instrument the code:` Use a code coverage tool to instrument your code to track condition execution.

`5. Execute test cases:` Run all the designed test cases.

`6. Generate coverage report:` The code coverage tool will provide a report indicating which condition combinations were covered.

`7. Analyze report:` Review the report to identify uncovered combinations and create additional test cases.

# Limitations
MCC can lead to a significant increase in test cases, especially with multiple conditions. It's often used in safety-critical systems where thorough testing is essential.

# 5. All-Path Coverage
All-path coverage is a software testing technique that aims to execute every possible path through a program's code. This means testing every combination of decisions, loops, and branches.

# Why is it important?
It ensures that all code is exercised, potentially revealing hidden defects.

# How to use it?

`1. Create a control flow graph:` Visualize the program's structure to identify all possible paths.

`2. Determine path count:` Calculate the number of independent paths using cyclomatic complexity.

`3. Design test cases:` Create test cases to cover each identified path.

`4. Execute test cases:` Run the test cases and analyze the results.

# Limitations

All-path coverage is often impractical due to the exponential growth of test cases with increasing code complexity. It's usually applied to small, critical code sections.


# Black Box

# 1. Boundary Value Analysis
Boundary value analysis focuses on input values at the edges of equivalence partitions. It assumes errors are more likely to occur near these boundaries.   

# Why is it important?

It can increase the likelihood of detecting defects missed by other methods.

# How It Works

`1. Identify input ranges:` Determine the input parameters with defined ranges or limits.

`2. Determine boundary values:` Identify the minimum, maximum, and values just inside and outside these boundaries.

`3. Design and execute test cases:` Create and run the test cases using the identified boundary values as input data.

`4. Analyze results:` Compare the actual output with the expected output to identify defects.

# Limitations

Boundary value analysis emphasizes the values at the boundaries and may overlook issues within the interior of the input range.

# 2. Equivalence Partitioning

This strategy divides input data into groups (partitions) based on expected output. Instead of testing every possible input value, representative values are selected from each partition and tested. 

# Why is it important?

This approach significantly reduces the number of test cases while maintaining effective test coverage.   

# How to use it:

`1. Identify input conditions:` Determine the input parameters that affect the system's behavior.   

`2. Create partitions:` Divide input values into groups that produce similar outputs.

`3. Select test values:` Choose representative values from each partition to create test cases.   

`4. Design test cases:` Develop test cases to cover all partitions and their boundaries.   

# Limitations

Since it assumes all values within a partition behave similarly, it might overlook issues that only occur with specific values within that partition.

# 3. Decision Table Testing

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



