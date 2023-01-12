# Process Builder

- It is a poin-and-click tool that lets you easily automate business proceses  and see graphical representation of your process as you build.
- More powerfull than workflow rules as can perform more things

## 3 Components

### 1. Trigger

Trigger gets fired under 3 conditions

1. When a record is created or edited
2. when a platform event msg is recieved
3. When another process invokes it.

### 2. Criteria

A process will have at least one criteria node which decides the conditions under which the actions are executed.

### 3. Actions

It will have at least one automation action. It also have Immidiate and Scheduled actions

1. Creates Record
2. Update Records (**itself + both parent and child records**)
3. Quick Actions
4. Invoke onother process
5. Launch a Flow
6. Email
7. Chatter post
8. Send for Approval
9. Apex (Aura enabled components)

## Limitations

1. Can't delete a record
2. Can't update unrelated records
3. Sheduled Actions are not available for update records trigger
