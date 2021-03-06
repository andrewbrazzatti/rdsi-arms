```
title: ARMS Test Plan
layout: page
tags: ['intro','configGuide']
pageOrder: 5
```
ARMS Test Plan
==============

Version: 1.0 draft 2014-03-25

## Introduction

### Background

The Allocation Request Management System (ARMS) system 
helps manage parts of the process of providing RDSI storage
allocations. It captures the information in a request for storage, and
tracks that request through the process of assessing and (if approved)
provisioning the storage for it.

### Purpose

This is a test plan for ARMS.

### Acceptance criteria

All Web browser tests shall be performed using each of the following
Web browsers:

- Safari 7.0.x running on OS X 10.9.x.
- Chrome (version and platform TBD)
- Internet Explorer (version and platform TBD)
- Opera (version and platform TBD)

All tests shall be performed.

All of the procedures in the tests can be carried out.

None of the checks shall fail.

## **Test 1**: Login failure

### Synopsis

Unsuccessful login.

### Prerequisites

- User not logged in.

### Procedure

1. Go to the login page.
2. If using AAF login, click on the AAF icon.
3. Enter username.
4. Enter an incorrect password for that username.
5. Click login.
6. **Check 1-1**: login was rejected.

### Postconditions

- User not logged in.

## **Test 2**: Login success

### Synopsis

Successful login.

### Prerequisites

- User not logged in.

### Procedure

1. Go to the login page.
2. If using AAF login, click on the AAF icon.
3. Enter username.
4. Enter the password corresponding to that username.
5. Click login.
6. **Check 2-1**: login was successful.

### Postconditions

- User is logged in.

## **Test 3**: Logout

### Synopsis

Loging out.

### Prerequisites

- User is logged in.

### Procedure

1. Click the logout link.
2. **Check 3-1**: the login page is showing.

### Postconditions

- User not logged in.

## **Test 4**: Main Workflow

### Synopsis

A request can be processed according to the main workflow.

Note: this test does not exercise all possible workflow options. For
example, returning a request for resubmission or reopening a rejected
request is not tested. Those other workflow options should be tested
in other tests.

### Prerequisites

- User not logged in.
- Testing roles:

| Role        | Useranme      |   password   | 
|-------------|:-------------:|-------------:|
| requestor   | user          | user         |
| reviewer    | reviewer      | reviewer     |
| assessor    | assessor      | assessor     |
| assessor    | assessor1     | assessor     |
| assessor    | assessor2     | assessor     |
| assessor    | assessor3     | assessor     |
| provisioner | provisioner   | provisioner  |

### Procedure

1. Create request
    1. Login as a requestor.
    2. Click the "New request" button.
    3. Fill in the request form. Minimally provide all the mandatory fields
       and check both declarations.
    4. Click the "Submit request" button.
    5. Click Home.
    6. **Check 4-1**: the new request appears in the "Submitted requests" table.
    7. **Check 4-2**: the status of the new request is "Being reviewed".
    8. Logout.
2. Assessor does not have access to request
    1. Login as an assessor.
    2. **Check 4-3**: the new request does not appear in any of their tables.
    3. Logout.
3. Provisioner does not have access to request
    1. Login as a provisioner.
    2. **Check 4-4**: the new request does not appear in any of their tables.
    3. Logout.
4. Review and start assessment process
    1. Login as a reviewer.
    2. **Check 4-5**: the new request appears in the "Requests to review" table.
    3. Click the edit icon for the request.
    4. **Check 4-6**: the only available actions are "Save and close", "Make
       available for assessment" and "Return to requestor to update".
    5. Go to the "reviewer summary" page.
    6. Select "Approve for ReDS".
    7. Enter a value (e.g. "100 TB") for recommended amount of storage.
    8. Go to the Assessment summary page (e.g. clicking the next button).
    9. **Check 4-7**: there are no entries in the table.
    10. Click the "Make available for assessment" button.
    11. Click home.
    12. **Check 4-8**: the request is no longer in the Requests to review table.
    13. **Check 4-9**: the request is in the "Assessment requests" table.
    14. Logout.
5. Requestor
    1. Login as requestor
    2. **Check 4-10**: status is "Being reviewed" (unchanged)
    3. Logout.
6. Provisioner
    1. Login as provisioner
    2. **Check 4-11**: request does not appear in any of their tables.
    3. Logout.
7. Assessment
    1. Login as an assessor
    2. **Check 4-12**: the request appears in the "Requests to assess" table.
    3. Click on the edit icon for the request.
    4. **Check 4-13**: the only avalable action is "save and close".
    5. **Check 4-14**: the reviewer recommended option is displayed in the "Reviewer recommends" text.
    6. **Check 4-15**: no default recommendation is selected.
    7. Select "Approve for ReDS".
    8. **Check 4-16**: the only avalable action is "save and close" (unchanged).
    9. **Check 4-17**: the recommended size appears in the "Review recommends" text.
    10. **Check 4-18**: no default option is selected for the size.
    11. Select "Agree with recommended size".
    12. Optionally type in a comment.
    13. **Check 4-19**: the only avalable actions are "save and close" and "submit assessment".
    14. Click the "Submit assessment" button.
    15. Click home.
    16. **Check 4-20**: the request no longer appears in the "requests to assess" table.
    17. **Check 4-21**: the request appears in the "assessed requests" table.
    18. Logout.
8. Requestor
    1. Login as requestor.
    2. **Check 4-22**: the status is "Being reviewed" (unchanged).
    3. Logout.
9. Provisioner    
    1. Login as provisioner.
    2. **Check 4-23**: request does not appear in any of their tables.
    3. Logout.
10. Finish assessment process and approve
    1. Login as reviewer.
    2. **Check 4-24**: the request appears in the "Assessment requests" table.
    3. Click the edit icon for the request.
    4. **Check 4-25**: the only available actions are "Save and close" and "Remove from assessment".
    5. Go to the assessments page.
    6. **Check 4-26**: the assessment submitted appears as a row in the table.
    7. Click the "Remove from assessment" button.
    8. Click home.
    9. **Check 4-27**: the request now appears in the "Requests to review" table and does not appear in the "Assessment requests" table.
    10. Click the edit icon for the request.
    11. **Check 4-28**: the only available actions are "Save and close", "make available for assessment" and "Return to requestor to update".
    12. Go to the outcome page.
    13. **Check 4-29**: the decision selected is "Still being processed".
    14. Select "Approve for ReDS" as the decision.
    15. **Check 4-30**: the only available actions are "Save and close" and "Approve and notify provisioning".
    16. Type in an Allocation ID.
    17. Click "Approve and notify provisioning".
    18. Click home.
    19. **Check 4-31**: request has moved to the "Approved requests" table.
    20. Click on the edit icon for the request.
    21. **Check 4-32**: the only avalable actions are "Save and close", "Mark as provisioning complete" and "Reopen".
    20. Logout.
11. Requestor    
    1. Login as requestor.
    2. **Check 4-33**: the status is "Being provisioned".
    3. Logout.
12. Assessor
    4. Login as assessor.
    2. **Check 4-34**: the request no longer appears in any table.
    3. Logout.
13. Provisioning
    1. Login as provisioner.
    2. **Check 4-35**: the request appears in the "Approved requests" table.
    3. Click on the edit icon.
    4. **Check 4-36**: the only available actions are "Save and close" and "Mark as provisioning complete".
    5. Go to the outcome page.
    6. **Check 4-37**: the "Approved for ReDS", allocation ID and any other
       information matches what the provided had entered.
    7. Go to the provisioning page.
    8. Type in a number (e.g. "123") as the provisioning reference.
    9. **Check 4-38**: there is no date for the date provisioned.
    10. Type in some notes.
    11. Click "Mark as provisioning complete".
    12. Click home
    13. **Check 4-39**: the request appears in the "Provisioned requests" table.
    14. Logout.
14. Requestor
    1. Login as the requestor.
    2. **Check 4-40**: the request appears in the "Submitted requests" table (unchanged)
    2. **Check 4-41**: the status of the request is "Ready for use".
    4. Logout.
15. Reviewer
    1. Login as a reviewer.
    2. **Check 4-42**: the request does not appear in any table on the active page.
    3. Click on the provisioned tab.
    4. **Check 4-43**: the request appears in the "Provisioned request" table.
    5. Click on the edit icon for the request.
    6. **Check 4-44**: the only available actions are "Save and close" and "Reopen".
    7. Go to the provisioning tab.
    8. **Check 4-45**: there is a date for the value of the data provisioned, and it is correct.
    9. Click home.
    10. Logout.

### Postconditions

- Request in the provisioned state.
- User not logged in.

## **Test 5**: Draft editing and deleting

### Synopsis

Multiple editing of draft requests and the ability to delete draft
requests.

### Prerequisites

- User not logged in.

### Procedure

1. Create new draft request
    1. Login as a requestor.
    2. Click the "New request" button.
    3. **Check 5-1**: the only available options are "Save and close" and "Delete draft".
    4. Go to the "Allocation details" page.
    5. Fill in an allocation title. This step is optional, but will make
       it easier to identify the request.
    6. Click the "Save and close" button.
    7. Click home.
    8. **Check 5-2**: the new draft request appears in the "Draft requests" table.
    9. Logout.
2. Drafts are not visible to reviewers
    1. Login as a reviewer.
    2. **Check 5-3**: the new draft request does not appear in any table on the active requests page.
    3. Click on the "Provisioned" tab.
    4. **Check 5-4**: the new draft request does not appear in the table.
    5. Click on the "Rejected" tab.
    4. **Check 5-5**: the new draft request does not appear in the table.
    3. Logout.
3. Drafts are not visible to assessors
    1. Login as an asssessor.
    2. **Check 5-6**: the new draft request does not appear in any table.
    3. Logout.
4. Drafts are not visible to provisioners
    1. Login as a provisioner.
    2. **Check 5-7**: the new draft request does not appear in any table.
    3. Logout.
5. Continue editing a draft
    1. Login as the same requestor.
    2. **Check 5-8**: the new draft appears in the "Draft requests" table.
    3. Click the edit icon of the request.
    4. Go to the "Allocation details" page.
    5. Fill in an allocation description.
    6. Click the "Save and close" button.
    7. Click home.
    8. Logout.
6. Delete draft
    1. Login as the same requestor.
    2. **Check 5-9**: the new draft appears in the "Draft requests" table.
    3. Click the edit icon for the request.
    4. Go to the "Allocation details" page.
    5. **Check 5-10**: the new value for description appears.
    6. Click the "Delete draft" button.
    7. Click the "Delete" button on the Confirmation dialog.
    8. **Check 5-11**: the new draft request does not appear in any table.
    9. Logout.

### Postconditions

- User not logged in.

## **Test 6**: Rejecting a request

### Synopsis

Rejecting a request.

### Prerequisites

- User not logged in.

### Procedure

1. Create request
    1. Login as a requestor.
    2. Click the "New request" button.
    3. Fill in the request form. Minimally provide all the mandatory fields
       and check both declarations.
    4. Click the "Submit request" button.
    5. Logout.
2. Reviewer rejects the request
    1. Login as a reviewer.
    2. **Check 6-1**: the request appears in the "Requests to review" table.
    3. Click on the edit icon for the request.
    4. **Check 6-2**: the only available actions are "Save and close", "Make
       available for assessment" and "Return to requestor to update".
    5. Go to the "outcome" page.
    6. **Check 6-3**: the "Still being processed" radio button is selected.
    7. Select the "reject" radio button.
    8. **Check 6-4**: the only available actions are "Save and close" and
       "Reject and notify requestor".
    9. Click the "Reject and notify requestor" button.
    10. Click home.
    11. **Check 6-5**: the request does not appear in any of the tables on the active requests page.
    12. Click on the "Provisioned" tab.
    13. **Check 6-6**: the request does not appear in the table.
    14. Click on the "Rejected" tab.
    15. **Check 6-7**: the request appears in the rejected requests table.
    16. Logout.
3. Requestor gets notified of rejection
    1. Login as the requestor.
    2. **Check 6-8**: the request appears in the submitted requests table.
    3. **Check 6-9**: the request's status is "not approved".
    4. Logout.

### Postconditions

- Request in the rejected state.
- User not logged in

## **Test 7**: Reopening a rejected request and approving it

### Synopsis

Reopening a rejected request and approving it.

### Pre-coditions

Perform the procedure for "rejecting a request" test.

### Procedure

1. Reviewer reopens the request
    1. Login as a reviewer.
    2. Click on the "Rejected" tab.
    3. **Check 7-1**: the request appears in the table.
    4. Click the edit icon for the request.
    5. **Check 7-2**: the only available actions are "Save and close" and "Reopen".
    6. Click the "Reopen" button".
    7. Click home.
    8. **Check 7-3**: the request appears in the "Requests to review" table.
    9. Logout.
2. Requestor sees it as being reopened
    1. Login as the requestor.
    2. **Check 7-4**: the status of the request is "being reviewed".
    3. Logout.
3. Reviewer approves the request
    1. Login as a reviewer.
    2. **Check 7-5**: the request appears in the "Requests to review" table.
    3. Click the edit icon of the request.
    4. **Check 7-6**: the only available options are "Save and close"
       and "Reject and notify requestor".
    5. Go to the outcome page.
    6. **Check 7-7**: the decision of "Reject" is selected.
    7. Select "Approved for ReDS" for the decision.
    8. **Check 7-8**: the only available options are "Save and close" and "Approve
       and notify provisioning".
    9. Click the "Approved and notify provisioning" button.
    10. Click home.
    11. **Check 7-9**: the request appears in the "Approved requests" table.
    12. Logout.
4. Requestor sees it as being approved
    1. Login as the requestor.
    2. **Check 7-10**: the status of the request is "Being provisioned".
    3. Logout.
5. Reviewer marks the request as provisioned (i.e. doing the job of the provisioner)
    1. Login as a reviewer.
    2. Click the edit icon of the request.
    3. **Check 7-11**: the only available options are "Save and close", "Mark as provisioning completed" and "Reopen".
    4. Click the "Mark as provisioning completed" button.
    5. Click home.
    7. **Check 7-12**: the request does not appears in any table on the active requests page.
    8. Click the "Provisioned" tab.
    9. **Check 7-13**: the request appears in the table.
    10. Logout.

## **Test 8**: Reopening a provisioned request

### Synopsis

A previously provisioned request is reopened.

### Prerequisites

- Request in the provisioned state.
- User not logged in.

### Procedure

1. Reviewer reopens request
    1. Login as a reviewer.
    2. Click on the "provisioned" tab.
    3. Click on the edit icon of the request.
    4. **Check 8-1**: the only available actions are "Save and close" and "Reopen".
    5. Click on the "Reopen" button.
    6. Click home.
    7. **Check 8-2**: the request appears in the "Requests to review."
    8. Click on the edit icon of the request.
    9. **Check 8-3**: the only available actions are "Save and close" and "Approve and notify provisioning".
    10. Logout.
2. Requestor sees reopened request
    1. Login as the requestor.
    2. **Check 8-4**: the request appears in the "Submitted requests" table.
    3. **Check 8-5**: the status is "Being reviewed".
    4. Logout.  

## **Test 9**: Reopening an approved request

### Synopsis

An approved request is reopened (i.e. brought back into the review
state) while it is waiting to be provisioned but before a provisioner
has marked it as provisoned.

### Prerequisites

- Request in the approved state.
- User not logged in.

### Procedure

1. Reviewer reopens request
    1. Login as a reviewer.
    2. **Check 9-1**: the request appears in the "Approved requests" table.
    3. Click on the edit icon of the request.
    4. **Check 9-2**: the only available actions are "Save and close", "Mark as provisioning complete" and "Reopen".
    5. Click on the "Reopen" button.
    6. Click home.
    7. **Check 9-3**: the request appears in the "Requests to review."
    8. Click on the edit icon of the request.
    4. **Check 9-4**: the only available actions are "Save and close" and "Approve and notify provisioning".
    8. Logout.
2. Requestor sees reopened request
    1. Login as the requestor.
    2. **Check 9-5**: the request appears in the "Submitted requests" table.
    3. **Check 9-6**: the status is "Being reviewed".
    4. Logout.  
3. Provisioner no longer sees the request
    1. Login as a provisioner.
    2. **Check 9-7**: the requests does not appear in the "Requests to provision" table.
    3. Click on the "Provisioned" tab.
    4. **Check 9-8**: the requests does not appear in the "Provisioned requests" table.
    5. Logout.

## **Test 10**: Redrafting

### Synopsis

A request needs more information. So the reviewer returns it to the
requestor to provide more information.

### Prerequesites

- Request in the review state.
- User not logged in.

### Process

1. Reviewer returns the request for redrafting
    1. Login as a reviewer.
    2. **Check 10-1**: the request appears in the "Requests to review" table.
    3. Click on the edit icon of the request.
    4. Go to the outcome page.
    5. Select "Still being processed" as the decision (if it is not already selected).
    6. **Check 10-2**: the only available actions are "Save and close", "Make
       available for assessment" and "Return to requestor to update".
    7. Click on the "Return to requestor to update" button.
    8. Click home.
    9. **Check 10-3**: the request appears in the "Draft requests" table.
    10. Logout.
2. Requestor resubmits request
    1. Login as the requestor.
    2. **Check 10-4**: the request appears in the "Returned requests" table.
    3. Click the edit icon of the request.
    4. **Check 10-5**: the only available actions are "Save and close", 
       and "Resubmit request".
    5. Go to the "allocation details" page.
    6. Edit the title.
    7. Click the "Resubmit request" button.
    8. Click home.
    9. **Check 10-6**: the request appears in the "Submitted requests" table.
    9. **Check 10-7**: the status of the request is "Being reviewed".
    10. Logout.
3. Reviewer sees resubmitted request
    1. Login as a reviewer.
    2. **Check 10-8**: the request appears in the "Requests to review" table.
    3. **Check 10-9**: the request shows the new title.
    4. Logout.

## **Test 11**: Reopening a redraft

### Synopsis

Reviewer has returned a request to the requestor to provide more
information, but wants to bring it back under the review process
without waiting for the requestor to resubmit it.

### Prerequesites

- Request in the redraft state.
- User not logged in.

### Procedure

1. Reviewer reopens a returned request
    1. Login as a reviewer.
    2. **Check 11-1**: the request appears in the "Draft requests" table.
    3. Click on the edit icon of the request.
    4. **Check 11-2**: the only available actions are "Save and close" and "Reopen".
    5. Click the "Reopen" button.
    6. Click home.
    7. **Check 11-3**: the request appears in the "Requests to review" table.
    8. Logout.
2. Requestor no longer can resubmit request.
    1. Login as the requestor.
    2. **Check 11-4**: the request appears in the "Submitted requests" table.
    3. **Check 11-5**: the status is "Being reviewed".

## **Test 12**: Multiple assessments

### Synopsis

Multiple assessments are submitted.

### Prerequisites

- At least four assessors are configured in the system.
- Request in the assessment state.
- User not logged in.

### Procedure

1. First assessor makes an assessment
    1. Login as the first assessor:assessor.
    2. Click on the edit icon of the request.
    3. Select the "Accept for ReDS" radio button for the recommendation.
    4. Select the "Accept recommended size" radio button.
    5. Type in a note.
    6. Click the "submit assessment" button.
    7. Click home.
    8. Logout.
2. Second assessor makes an assessment
    1. Login as the second assessor1:assessor.
    2. Click on the edit icon of the request.
    3. Select the "Accept for CDS" radio button for the recommendation.
    4. Select the "Accept recommended size" radio button.
    5. Type in a note.
    6. Click the "submit assessment" button.
    7. Click home.
    8. Logout.
3. Third assessor makes an assessment
    1. Login as the third assessor2:assessor.
    2. Click on the edit icon of the request.
    3. Select the "Reject" radio button for the recommendation.
    4. Select the "Accept recommended size" radio button.
    5. Type in a note.
    6. Click the "submit assessment" button.
    7. Click home.
    8. Logout.
4. Fourth assessor makes an assessment
    1. Login as the fourth assessor3:assessor.
    2. Click on the edit icon of the request.
    3. Select the "Accept for ReDS" radio button for the recommendation.
    4. Select the "Disagree with recommended size" radio button.
    5. Type in a note.
    6. Click the "submit assessment" button.
    7. Click home.
    8. Logout.
5. Reviewer checks assessments
    1. Login as a reviewer.
    2. Click on the edit icon of the request.
    3. Go to the assessments page.
    4. **Check 12-1**: there are four rows in the table of assessments.
    5. **Check 12-2**: each row corresponds to one of the four assessors.
    6. **Check 12-3**: each row matches the values provided by the respective assessors.
    7. Logout.

## **Test 13**: Entering, saving and recalling data

### Synopsis

Data enter is preserved and reappears in the correct places.

### Goals

This test applies this procedure:

1. Set or change the value.
2. **Check 13-1**: the value is preserved.

When applied to all permutations of:

1. Each role
2. Each form accessible by that role.
3. Each editable data field on that form.
4. Each method to navigate away from that form and continue editing.
5. Each method editing or viewing that data field, either:
      1. Returning to that form;
      2. Accessing another form that edits that same data field;
      3. Viewing a read-only version of that data field.

The roles are: requestor, reviewer, assessor and provisioner.

The forms are too many to enumerate here. Examples include: section 1,
section 2, section 3, reviewer's summary and assessment forms.

The editable data fields are too many to enumerate here. Examples
include: title, description and provisioner's notes.

The methods to navigate away from that form and _continue editing_
include: next button, previous button, tabs to the different forms for
that request, save and close button, and all other action
buttons. They do not include the methods to navigate away from that
form and _abort editing_, which include: the top navigation tabs
(e.g. "Home"), logging out, closing the Web brower tab/window,
quitting from the Web browser or turning off the computer.

### Procedure

An efficient implement of this test needs to be developed.

## **Test 14**: Mandatory data fields

### Synopsis

Mandatory data fields must be answered before submission is permitted.

### Prerequesites

- User not logged in.

### Procedure

1. Create request
    1. Login as a requestor.
    2. Click the "New request" button.
    3. Do not fill in any of the mandatory data fields.
    4. Go to the "Declarations" page.
    5. Check the two declarations.
    6. Click the "Submit request" button.
    7. **Check 14-1**: errors are raised.
    8. Click home.
    9. **Check 14-2**: the request appears in the "Draft requests" table.
2. Repeat the following until all mandatory data fields are completed:
    1. Click on the edit icon of the request.
    2. Fill in one or more extra mandatory data field.
    3. **Check 14-3**: errors are raised when all the mandatory data fields are not filled in.
    4. **Check 14-4**: submission successful when all mandatory data fields are filled in.

## Appendix: Future work

- Improve testing workflow so all tests can be performed in sequence.
- Add checks for email notifications.
- Add additional test cases.
