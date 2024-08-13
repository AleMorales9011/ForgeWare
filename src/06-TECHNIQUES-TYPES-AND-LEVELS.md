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
