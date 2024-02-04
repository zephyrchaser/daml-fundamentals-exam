# daml-fundamentals-exam
The repository contains a final daml project required to pass the daml fundamentals certification

## templates

There are 3 templates in total
- ProjectProposal
- Project
- Accomplishment

### ProjectProposal
This template represents a proposal that could be reviewed and then either rejected with an explanation or approved to create a new project

There are 2 parties in this template:

|Party|Type|
|-----|----|
|proposer|signatory|
|evaluator|observer|

ProjectProposal contains 6 choices
|Choice|nonconsuming|Description|controller|
|------|------------|-----------|----------|
|Propose|yes| creates a contract of type ProjectProposal with some project information | proposer|
|Revise|yes| archieves current proposal and creates a new one with a new unique project information | proposer|
|Cancel|no| archieves current proposal | proposer |
|ProposerAccomplishments|yes| returns text representation of provided accomplishments, if there none will return list with a single text vale "N/A" | evaluator |
|Reject|no| replaces current proposal with the new one, which contains updated note field with the rejection explanation  | proposer |
|Approve|no| creates a contract of type Project with data from proposal | evaluator |

### Project
This template represents a project that is created from the proposal covered above

Similar to the ProjectProposal template, Project template has 2 parties that are both signatories
- evaluator
- proposer

Proect contains 1 consuming choice: Evaluate

|Choice|Description|controller|
|------|-----------|----------|
|Evaluate| either creates an Accomplishment contract if the project is ready to be published or returns the new project with evaluator note of what should be updated | evaluator|

### Accomplishment
This template represents an accomplishment of the project lead

It has a key of type (Party, ProjectInfo) that could be used for fetching and querring. Doesn't have any explicit choices

## Extra notes

To run the project simply run: daml start
To run the tests only, please run: daml test