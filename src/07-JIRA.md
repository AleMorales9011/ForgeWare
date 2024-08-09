# Manage Tests With Jira and Xray

This repository demonstrates a streamlined approach to software test management utilizing Jira and Xray.

_This description uses **team-managed** project._

## Methodology

**Test Case Management:**
- Leverages Xray issue types for different test case categories
- Utilizes Jira custom fields for capturing detailed test case information.
- Integrates Xray for traceability between requirements and test cases.

**Test Execution:**
- Implements Xray Test Repositories for grouping related test cases for execution.
- Employs Xray Test Runs to manage test execution cycles and record results.
- Employs Xray Test Plans to execute streamlined testing.
  
**Reporting & Analysis:**
- Utilizes Xray reporting features to visualize test coverage and execution progress.


| 1. | SETTING UP XRAY |
|--|----------------|
| 1.1. | Install the Xray app on your Jira instance. |
| 1.2. | Configure Xray by creating new issue types for test cases, pre-conditions, test sets, test plans, and test executions. |
| 1.3. | Map the new issue types to Xray entities. |
| 1.4. | Define covered issue types for defect tracking. |
| 1.5. |Set up test coverage by linking testable items to coverable ones. |

Mapping issue types:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/5b4e0748-64c4-49ac-bc62-b8a6ad2de0d8)


| 2. | CREATING TEST CASES |
|--|--------------------|
| 2.1. | Create new test cases as "Test" issue types. |
| 2.2. | Choose between Manual, Cucumber (BDD), or Generic test types based on your needs. | 
| 2.3. | For Manual tests, define steps and add them sequentially. |
| 2.4. | For Cucumber tests, write test steps in the Gherkin language. |
| 2.5. | For Generic tests, provide a free-form test definition. |

Manual test case example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/2e2b666c-a5c2-46c7-ac47-6af9c1def6fe)

Cucumber test case example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/1e9642f7-aa3f-4c5c-a8e6-e958e82fd81d)

Generic test case example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/79005681-9b95-4b8b-ab60-8fb62c64464e)

| 3. | MANAGING TEST CASES | 
|--|-------|
| 3.1. | Organize test cases within a hierarchical structure using Test Repositories. |
| 3.2. | Create folders and sub-folders to categorize tests. |
| 3.3. |Drag and drop tests into folders or create new ones within the repository. |

Test Repository example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/56bbdcd3-d076-4240-98f9-ccec15d88270)

| 4. | CREATING TEST PLANS |
|--|----------------|
| 4.1. | Define a test plan to group related test cases for execution. |
| 4.2. | Add tests to the test plan by specifying the issue ID. |
| 4.3. |Use the overview of the test plan to make edits. |

Test plans example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/96719c8b-1777-4758-9abe-fca9831fc508)

| 5. | EXECUTING TESTS |
|--|------------------|
| 5.1. | Create a test execution for a specific test plan. |
| 5.2. | Initiate the test execution and record the results (pass/fail). |
| 5.3 | Check the Test Execution menu to evaluate the results. |

Test Execution example:

![image](https://github.com/amandaestevez/softwareqa/assets/123298275/fe9a29be-b4e7-439c-a50b-69da33ec0e65)

## Conclusion
This repository offers a configurable foundation for managing software testing within Jira and Xray, facilitating efficient test case organization, execution, and reporting.

### Sources:

- [How to create and manage test cases with Xray and Jira](https://www.atlassian.com/devops/testing-tutorials/jira-xray-integration-manage-test-cases)
- [Xray Documentation](https://docs.getxray.app/display/XRAY/Test)
- [Xray Steps (Manual Tests)](https://docs.getxray.app/pages/viewpage.action?pageId=62267955#Steps(ManualTests)-DefiningTestSteps)
- [Xray Gherkin (BDD Tests)](https://docs.getxray.app/pages/viewpage.action?pageId=62268093)
- [Gherkin Syntax](https://cucumber.io/docs/gherkin/)
- [Xray Unstructured (Generic) Tests](https://docs.getxray.app/pages/viewpage.action?pageId=62268044)


# 1. Test Case Design
# 2. Recording
# 3. Management
