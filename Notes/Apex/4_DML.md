# DML (Data Manipulation Language)

- **150** DML Statements allowed per Apex class
- **10,000** records can be handled per DML

## Operations

1. Insert - insert sObject|sObject[]

    ```
    Account newAcct = new Account(name = 'Acme');
    try {
      insert newAcct;
    } catch (DmlException e) {
    // Process exception here
    }
    ```

2. Update
3. Upsert
4. Delete
5. Undelete
6. Merge

| Database Methods | DML Statement |
|------------------|---------------|
