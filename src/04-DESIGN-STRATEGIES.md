# Test Case Design Strategies

| TECHNIQUE | DESCRIPTION | ADVANTAGE | DISADVANTAGE |
|-----------|-------------|-----------|--------------|
| Equivalence Partitioning | Divides input data into valid and invalid categories for testing. | Efficient, covers a wide range of inputs. | May miss edge cases within partitions. |
| Boundary Value Analysis | Tests values at the edges of input and output boundaries. | Effective for finding errors related to data limits. | May neglect logic within boundaries. |
| Decision Table Testing | Creates a table mapping input conditions to expected outputs. | Systematic approach, good for complex decision logic. | Time-consuming to create and maintain tables.|
| State Transition Testing | Tests behavior changes between different system states. | Efficient for state-driven systems, reveals state-related bugs. | Requires a thorough understanding of system states and transitions. |

# 1. Equivalence Partitioning
# 2. Boundary Value Analysis

# Exercise: Interest Rate Calculator Testing

An informational interest rate calculator for a fixed term deposit needs to be tested. For a given deposit amount and client's age, the calculator shows the annual interest rate.

_The following rules apply:_

- The minimum deposit amount is $100
- The maximum deposit amount is $10,000
- The annual interest rate depends on the deposit amount as follows:

| DEPOSIT AMOUNT | INTEREST RATE |
|-------|-----------|
| $100 - $999 | 1% |
| $1,000 - $4,999 | 1.3% | 
| $5,000 - $10,000 | 1.5% |

- Only adults (18 and older) are eligible to open a term deposit account.
- Clients aged 60 and older have a fixed interest rate of 2%.

Define the optimal (effective and efficient) set of boundary test cases for a system that calculates the term's deposit interest.

------------

**Test suite effectivenes:** The effectiveness of a solution is how successful the submitted test cases are at identifying potential bugs in a system.

It is calculated as the percentage of the bugs identified compared to the total potential bugs plus the number of incorrect test cases submitted.

_Formula: BugsFound / (BugsTotal + IncorrectTestCases)_

**Test suite efficiency:** The efficiency of a solution decreases as the number of steps taken to be effective increases.

It is calculated as the percentage of the minimum number of test cases required to find all bugs compared to the number submitted, multiplied by the percentage of bugs found.

_Formula: MinimumTestCases / SubmittedTestCases * BugsFound / BugsTotal_

**Total score:** The total score is calculated as the product of effectiveness and efficiency.

_Formula: Effectiveness * Efficiency_

----------------

I'm going to answer this question in different iterations until I get a 100% total score. The first iteration was on July 23, 2024. However, I didn't document it.

### 2nd iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 18 | 1.5% |
| TC 04 | $10,000 | 18 | 1.5% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $99 | 18 | Unavailable |
| TC 07 | $10,001 | 60 | Unavailable | 
| TC 08 | $5,000 | 17 | Unavailable | 

Test suite effectiveness: 84% - meaning it can identify up to **84% of potential bugs found in the system.**

Test suite efficiency: 100% - we have the **ideal number of test cases** required.

Total score: 84% - the test set is **84% optimal.**

**_Comments:_** Since I'm not covering all limits - such as deposit $100 and age 17 - I believe I could add one more test case to improve effectiveness.

-------------

### 3rd iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 18 | 1.5% |
| TC 04 | $10,000 | 18 | 1.5% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $99 | 18 | Unavailable |
| TC 07 | $10,001 | 60 | Unavailable | 
| TC 08 | $5,000 | 17 | Unavailable | 
| TC 09 | $100 | 17 | Unavailable |

Test suite effectiveness: 84% - meaning it can identify up to **84% of potential bugs found in the system.**

Test suite efficiency: 94% - we have **more test cases** than required.

Total score: 79% - the test set is **79% optimal.**

**_Comments:_** By increasing the number of test cases when compared to the previous iterations, I actually decreased its performance - it didn't impact the effectiveness, and reduced efficiency, so we had more test cases than necessary. That's an issue because inefficient test cases can increase delivery time and costs. This means I'll have to keep a **maximum of 8 test cases and change the other variables: age, deposit and interest rate.**

----------

### 4th iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $99 | 18 | Unavailable |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 18 | 1.5% |
| TC 04 | $10,000 | 18 | 1.5% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 
| TC 07| $5,000 | 17 | Unavailable | 
| TC 08 | $100 | 17 | Unavailable |

Test suite effectiveness: 70% - meaning it can identify up to **70% of potential bugs found in the system.**

Test suite efficiency: 92% - we have **more test cases** than required.

Total score: 64% - the test set is **64% optimal.**

**_Comments:_** This time, the total score was lower even with fewer test cases. So the issue seems to be with the variables in the test cases. Let's change TC 01 back to $100, and TCs 03 and 04 to age 59.

----------

### 5th iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 59 | 1.5% |
| TC 04 | $10,000 | 59 | 1.5% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 
| TC 07| $5,000 | 17 | Unavailable | 
| TC 08 | $100 | 17 | Unavailable |

Test suite effectiveness: 75% - meaning it can identify up to **75% of potential bugs found in the system.**

Test suite efficiency: 99% - we are almost at the ideal number of test cases.

Total score: 74% - the test set is **74% optimal.**

**_Comments:_** Now we changed TC 03 and TC 04 ages to 59, and the total score was lower. We also changed the TC 01 back to $100 with an interest rate of 1%. However, we have two test cases covering 1.5% interest rate and the age 59, so let's change TC 04 to 1%.

----------

### 6th iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 59 | 1.5% |
| TC 04 | $999 | 59 | 1% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 
| TC 07| $5,000 | 17 | Unavailable | 
| TC 08 | $100 | 17 | Unavailable |

Test suite effectiveness: 70% - meaning it can identify up to **70% of potential bugs found in the system.**

Test suite efficiency: 92% - we are almost at the ideal number of test cases.

Total score: 64% - the test set is **64% optimal.**

**_Comments:_** That didn't work 😅 Considering that the test efficiency decreased, I'll then remove the TC 08.


----------

### 7th iteration (07/26/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 59 | 1.5% | 
| TC 04 | $999 | 59 | 1% |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 
| TC 07| $5,000 | 17 | Unavailable | 

Test suite effectiveness: 70% - meaning it can identify up to **70% of potential bugs found in the system.** 

Test suite efficiency: 100% - Yeeeyyy, back at 100% efficiency!!
Total score: 70%.

**_Comments:_** Well, although the test suite effectiveness remained the same, the efficiency actually increased! So since the best result we had was the 2nd iteration, let's try to find a mid-term between the 2nd and the 7th iterations.

----------

### 8th iteration (07/27/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 59 | 1.5% | 
| TC 04 | $999 | 17 | Unavailable |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 

Test suite effectiveness: 74% - meaning it can identify up to **74% of potential bugs found in the system.** 

Test suite efficiency: 100% - The efficiency remained at 100% even though I reduced the number of test cases.

Total score: 74%.

**_Comments:_** In this iteration, we managed to increase effectiveness while maintaining high efficiency and having the lowest number of test cases of all iterations. The main difference between iterations 7 and 8 is that for 8 we only tested ages 17 and 59 once, which I believe increased the effectiveness. Let's try to test age 60 only once for the next iteration.

----------

### 9th iteration (07/27/2024)

| TEST CASE ID | DEPOSIT AMOUNT | CLIENT AGE | EXPECTED INTEREST RATE | 
|--------|-----------|--------|-------|
| TC 01 | $100 | 18 | 1% |
| TC 02 | $1,000 | 18 | 1.3% | 
| TC 03 | $5,000 | 59 | 1.5% | 
| TC 04 | $999 | 17 | Unavailable |
| TC 05 | $5,000 | 60 | 2% |
| TC 06 | $10,001 | 60 | Unavailable | 

Test suite effectiveness: 74% - meaning it can identify up to **74% of potential bugs found in the system.** 

Test suite efficiency: 100% - The efficiency remained at 100% even though I reduced the number of test cases.

Total score: 74%.

**_Comments:_** In this iteration, we managed to increase effectiveness while maintaining high efficiency and having the lowest number of test cases of all iterations. The main difference between iterations 7 and 8 is that for 8 we only tested ages 17 and 59 once, which I believe increased the effectiveness. Let's try to test age 60 only once for the next iteration.

# Exercise: Boundary Value and Equivalence Partitioning for Age Algorithm

A Developer needs to write a function for converting age (a whole number), into a life period using the following algorithm:

- If age is **ZERO**, it should return **INVALID**;
- If age is **greater than ZERO and less than 16**, the function should return **CHILD**;
- If age is **greater than or equal to 16**, it should return **ADULT**.

Define the optimal (effective and efficient) set of boundary test cases to test the function.

---------
# EXPLANATION

This question describes a **Boundary value analysis testing technique** - a software testing technique used to identify program defects by focusing on the inputs at the edges of allowable ranges. The idea is that errors are more likely to occur at the boundaries between valid and invalid input values.

The core of BVA is designing test cases that specifically target these boundary values and the values just outside them. This helps identify issues like:

▶️ The program _rejects a valid input_ because it's on the edge of a range.

▶️ The program _does not handle_ unexpected inputs (e.g., negative numbers for age).

▶️ Issues with how the program behaves _when transitioning between partitions_ (e.g., how it handles the value 18 for age).

This technique often comes along with another testing technique called **Equivalence Partitioning**, where you divide the possible input values into groups **(partitions)** where each value within a partition is expected to be treated similarly by the program.

In addition, this question requires a good understanding of **SPECIFICATION ANALYSIS** - understanding the requirements (specifications) is crucial for designing effective test cases. Here, the specification defines how the age-to-life period conversion function should behave based on different age ranges.
 
------------

# SOLUTION

In the question above, we find three partition groups with different boundaries:

| PARTITIONS | BOUNDARY VALUES | CLASSIFICATION |
|---------|-----------|-|
| **PARTITION 01** | 0 (minimum and maximum values) |INVALID |
| **PARTITION 02** | 1 (minimum value), 2 - 14 (middle range), and 15 (maximum value) | CHILD |
| **PARTITION 03** | from 16 (minimum value) on | ADULT |

So below is the `optimal set of boundary test cases` to test the function:

## TEST CASE 01

| AGE | LIFE PERIOD |
|---|----------|
| 0 | INVALID |

## TEST CASE 02

| AGE | LIFE PERIOD |
|---|----------|
| 1 | CHILD |

## TEST CASE 03

| AGE | LIFE PERIOD |
|---|----------|
| 15 | CHILD |

## TEST CASE 04

| AGE | LIFE PERIOD |
|---|----------|
| 16 | ADULT |

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

**_1 - Review the specifications/requirements -_** it will help you understand how the system is expected to behave.
**_2 - Identify system states, events, and transitions -_** Identify all the states the system can be in, the events that trigger them and the transitions that are supposed to occur once those events happen.
**_3 - Create state transition diagrams -_** They will provide a clear overview of the software expected behavior.
**_4 - Derive the test cases -_** Use the state transition diagrams to derive the necessary test cases.
**_5 - Execute and analyze the test results -_** Perform the test cases and record the actual system behavior, then compare the actual results with the expected results. Identify any discrepancies or unexpected behavior.Investigate failed test cases to determine the root cause of the issue.

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
