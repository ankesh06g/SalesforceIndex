# Wokflow Rules

Workflow can

1. **Tasks** — Assign a new task to a user, role, or record owner.
2. **Email Alerts** — Send an email to one or more recipients you specify.
3. **Field Updates** — Update the value of a field on a record. (**updates only parent records from child and itself**)
4. **Outbound Messages** — Send a secure, configurable API message (in **XML format**) to a designated listener.

For example,

- Assign follow-up tasks to a support rep one week after a case is updated
- Send sales management an email alert when a sales rep qualifies a large deal
- Change the Owner field on a contract three days before it expires
- Trigger an outbound API message to an external HR system to initiate the reimbursement process for an approved expense report

Each workflow rule consists of:

1. **Criteria** that cause the workflow rule to run.
2. **Immediate actions** that execute when a record matches the criteria. For example, Salesforce can automatically send an email that notifies the account team when a new high-value opportunity is created.
3. **Time-dependent actions** that queue when a record matches the criteria, and execute according to time triggers. For example, Salesforce can automatically send an email reminder to the account team if a high-value opportunity is still open ten days before the close date.

## Creating Worlflow Rule

1. Select object
2. Name of workflow rule
3. Evaluation criteria: Creted or Created&Edited
4. Rule criteria:
    1. When citeria meet (Select fields and operator, value and filter logic)
    2. Formula
5. Select Immediate actions and Time-dependent actions

## Immediate actions and Time-dependent actions

### 1. Create Task

1. Assign to
2. Subject
3. Due Date field + field Days
4. Status
5. Priority

### 2. Email Alert

1. Select email template
2. Select Recipients **Note:** We can add upto 5 additional email address apart from selected Recipients

### 3. Field Update

1. Select field to be updated and expected value using formula field

### 4. Outbound Messages

1. Select endpoint URL
2. User to send as 
3. Select fields to be send

## Observations

1. Workflow needs to be active
2. We can't add time-dependant actions on Active rule
