# Test Case Design Strategies

![image](https://github.com/user-attachments/assets/f4cae73d-8573-4484-9d45-61520511d3fc)

# White-Box

# 1. Statement Coverage Testing
Statement coverage is a design strategy that ensures every line of code in a program is executed at least once during testing. This method focuses on the structure of the code, aiming to cover all statements within it.

# Why it is important:
Statement coverage ensures that every line of code is executed at least once, helping to identify untested code areas and reduce the risk of undiscovered bugs.

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

Decision coverage tests every possible outcome of each decision point (e.g., if, else, switch) in the code.

# Why is it important?

Ensuring all decision paths are tested helps uncover potential defects related to conditional logic.   

# How to use it?

1. Identify decision points in the code.
2. Create test cases to cover both true and false outcomes of each decision.
3. Execute test cases and analyze results.

# 3. Condition Coverage

Condition coverage ensures that each part of a condition in a decision point (e.g., if, else) is evaluated as both true and false at least once.   

# Why is it important?

It helps identify potential errors in complex conditions by testing all possible outcomes of each condition.   

# How to use it?

1. Identify conditions within decision points.
2. Create test cases to evaluate each condition as both true and false.
3. Execute test cases and analyze results.

# Black Box

# 1. Boundary Value Analysis
Boundary value analysis is a testing technique that focuses on input values at the edges of equivalence partitions. It assumes errors are more likely to occur near these boundaries.   

# Why is it important?

By testing boundary values, you can increase the likelihood of finding defects that might be missed by other testing methods.

# How to use it

- Identify input conditions with ranges.
- Determine boundary values (minimum, maximum, just inside/outside).
- Create test cases using these boundary values.   
- Execute test cases and analyze results.

# 2. Equivalence Partitioning

This strategy divides input data into groups (partitions) based on expected output. Instead of testing every possible input value, representative values are selected from each partition and tested. 

# Why is it important?

This approach significantly reduces the number of test cases while maintaining effective test coverage.   

# How to use it:

- Identify input conditions: Determine the input parameters that affect the system's behavior.   
- Create partitions: Divide input values into groups that produce similar outputs.
- Select test values: Choose representative values from each partition to create test cases.   
- Design test cases: Develop test cases to cover all partitions and their boundaries.   

# 3. Specification Analysis

# 4. State Transition
The workflow of an ATM is defined by the following rules:

- The ATM goes into the **WORKING** state with the **TURN ON** action.
- When in the WORKING state, the ATM can:
     1 - **ACCEPT CARD** which switches it to the **CARD ACCEPTED** state.
     2 - Start the **AUTOMATIC TESTING** action which switches it to the **SELF TESTING** state.

- Within CARD ACCEPTED the ATM can:
     1 - CALL POLICE which switches it to the **WAITING POLICE** state.
     2 - PROCESS TRANSACTION which switches it to the TRANSACTION PROCESSED state.

- From the TRANSACTION PROCESSED state the ATM goes into the SELF TESTING state with the PULL CARD action.
- When in the SELF TESTING state, the ATM can either:
     1 - PASS, which switches it to the WORKING STATE.
     2 - FAIL, which switches it to the WAITING SERVICE state.

- From the WAITING SERVICE state, the ATM can either:
     1 - Be SERVICED, which puts the ATM into the WORKING state.
     2 - Be RETESTED, which returns the ATM to the SELF TESTING state.

Prepare the optimal (effective and efficient) set of test cases required to test this workflow.
Cover all state transitions and minimize repeating the same state transitions.

----------
**EXPLANATION**

The question above is about **state transition testing**, a **black-box testing technique** which focuses on evaluating how a software changes when transitioning from one state to another in response to events.

There are **x** important steps to creating optimal State transition tests:

**_1 - Review the specifications/requirements -_** It will help you understand how the system is expected to behave.
**_2 - Identify system states, events, and transitions -_** Identify all the states the system can be in, the events that trigger them and the transitions that are supposed to occur once those events happen.
**_3 - Create state transition diagrams -_** They will provide a clear overview of the software's expected behavior.
**_4 - Derive the test cases -_** Use the state transition diagrams to derive the necessary test cases.
**_5 - Execute and analyze the test results -_** Perform the test cases and record the actual system behavior, then compare the actual results with the expected results. Identify any discrepancies or unexpected behavior. Investigate failed test cases to determine the root cause of the issue.

----------
**ANSWER**

First, let's identify all the states and events/actions that cause the transitions:

**- State Transitions:** WORKING, CARD ACCEPTED, TRANSACTION PROCESSED, SELF TESTING, WAITING SERVICE, WAITING POLICE.

**- Actions** TURN ON, ACCEPT CARD, AUTOMATIC TESTING, CALL POLICE, PROCESS TRANSACTION, PULL CARD, PASS, FAIL, SERVICED, RETESTED.

Second, let's create the State Transition Diagram:

![workflow-diagram](https://github.com/user-attachments/assets/416efd5d-e848-4b5c-a502-3f4504520917)

(I created the diagram with Eraser.io, but you can use other diagram-making tools such as Draw.io or even Canva).

Third, let's define the test cases!

-------

## Defining Test Cases


Let's start by prioritizing the test cases. This is crucial in helping maximize the chances of identifying high-impact defects early in the development cycle.

**:bangbang: High Priority**
**_Test Case 1:_** Normal Operation and Maintenance: Covers core functionalities and system recovery.

**:heavy_exclamation_mark: Medium Priority**
**_Test Case 2:_** Error Handling: Addresses critical error scenarios and system resilience.

**:question_mark: Low Priority**
**_Test Case 3:_** Retest function: While important, this test case covers a subset of the first test case's functionality

Now let's build out the test cases considering the priority order.

>[!IMPORTANT]
> I found TWO WAYS to solve this issue:
> One compromises effectiveness to increase efficiency. The other compromises efficiency to increase effectiveness.
> I'll explain both ways here, but you should always consider what is more important for your organization.

## 01: Effectiveness Over Efficiency 

Before we move on, let's get one thing straight: in no way this is a sloppy test case. As you will see, the it's total score is 80%, because it achieves a 100% EFFECTIVENESS score, meaning it is 100% successful in finding bugs, even if there is a bit of overlap or redundancy in the sets.

### Test Case 1: Normal Operation and Maintenance

Objective: Verify normal ATM operation, maintenance, and recovery.
Steps:

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| ACCEPT CARD | CARD ACCEPTED |
| PROCESS TRANSACTION | TRANSACTION PROCESSED |
| PULL CARD | SELF TESTING |
| PASS | WORKING |
| AUTOMATIC TESTING | SELF TESTING |
| FAIL | WAITING SERVICE |
| SERVICED | WORKING |

### Test Case 2: Error Handling

Objective: Verify ATM behavior in case of a police call.

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| ACCEPT CARD | CARD ACCEPTED |
| CALL POLICE | WAITING POLICE |


### Test Case 3: Retest

Objective: Verify the retest process.

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| AUTOMATIC TESTING | SELF TESTING |
| FAIL | WAITING SERVICE |
| RETESTED | SELF TESTING |

Test suite effectiveness: 100%

Test suite efficiency: 80%

Overall score: 80%

The interesting thing though is that if we remove test cases 02 and 03, we also get 100% effectiveness and 80% efficiency. So the test would look like this:

### Test Case 1: Normal Operation and Maintenance

Objective: Verify normal ATM operation, maintenance, and recovery.
Steps:

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| ACCEPT CARD | CARD ACCEPTED |
| PROCESS TRANSACTION | TRANSACTION PROCESSED |
| PULL CARD | SELF TESTING |
| PASS | WORKING |
| AUTOMATIC TESTING | SELF TESTING |
| FAIL | WAITING SERVICE |
| SERVICED | WORKING |

----------
## 02: Efficiency Over Effectiveness

Here, to increase efficiency while keeping the effectiveness at an acceptable level, we can remove the third test case, which was low priority, and only stick to the first and second cases. 

### Test Case 1: Normal Operation and Maintenance

Objective: Verify normal ATM operation, maintenance, and recovery.
Steps:

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| ACCEPT CARD | CARD ACCEPTED |
| PROCESS TRANSACTION | TRANSACTION PROCESSED |
| PULL CARD | SELF TESTING |
| PASS | WORKING |
| AUTOMATIC TESTING | SELF TESTING |
| FAIL | WAITING SERVICE |
| SERVICED | WORKING |

### Test Case 2: Error Handling

Objective: Verify ATM behavior in case of a police call.

| ACTION | NEXT STATE |
|--------|------------|
| TURN ON | WORKING |
| ACCEPT CARD | CARD ACCEPTED |
| CALL POLICE | WAITING POLICE |

Test suite effectiveness: 90%

Test suite efficiency: 98%

Overall score: 88%

# 5. Use Case
# 6. Error Guessing
# 7. Decision Table
# 8. Combinatorial
# 9. Pairwise
