# Triger

- Static keyword can't be used inside trigger.

## Trigger Events

| Event | new | newMap | old | oldMap|
|---------|-------|------|-------|-------|
|Before Insert   |✅|-|-|-|
|After Insert    |✅|✅|-|-|
|Before Update   |✅|✅|✅|✅|
|After Update    |✅|✅|✅|✅|
|Before Delete   |-|-|✅|✅|
|After Delete    |-|-|✅|✅|
|After Undelete  |✅|✅|-|-

## Context Variables

These variables are contained in the ```System.Trigger``` class.

1. isInsert
2. isUpdate
3. isDelete
4. isBefore
5. isAfter
6. isUndelete
7. new - Returns a list of the new versions of the sObject records. This sObject list is only available in **insert**, **update**, and **undelete** triggers, and the records can only be modified in **before** triggers.
8. newMap - A map of IDs to the new versions of the sObject records. This map is only available in **before update**, **after insert**, **after update**, and **after undelete** triggers.
9. old - This sObject list is only available in **update** and **delete** triggers.
10. oldMap - This map is only available in **update** and **delete** triggers

``` java
Trigger simpleTrigger on Account (after insert) {
    for (Account a : Trigger.new) {
        // Iterate over each sObject
    }

    // This single query finds every contact that is associated with any of the
    // triggering accounts. Note that although Trigger.new is a collection of  
    // records, when used as a bind variable in a SOQL query, Apex automatically
    // transforms the list of records into a list of corresponding Ids.
    Contact[] cons = [SELECT LastName FROM Contact
                      WHERE AccountId IN :Trigger.new];
}
```

- trigger.new and ```trigger.old``` cannot be used in Apex DML operations.
- You can use an object to change its own field values using ```trigger.new```, but only in before triggers. In all after triggers, ```trigger.new``` is not saved, so a runtime exception is thrown.
- ```trigger.old``` is always read-only.
- You cannot delete ```trigger.new```.

>What is a benefit of using an after insert trigger over using a before insert trigger?
> **Ans:** An after insert trigger allows a developer to insert other objects that reference the new record.

## Trigger Exceptions

Triggers can be used to prevent DML operations from occurring by calling the ```addError()``` method on a record or field. When used on ```Trigger.new``` records in insert and update triggers, and on ```Trigger.old``` records in delete triggers, the custom error message is displayed in the application interface and logged.

## Deactivating Trigger

From Setup, open apex atrigger and uncheck isActive checkbox.

## Best practice

1. **One trigger per object** so you don't have to think about the execution order as there is no control over which trigger would be executed first.
2. Logic-less Triggers - use **Helper classes** to handle logic.
3. Code coverage 100%
4. **Handle recursion** - To avoid the recursion on a trigger, make sure your trigger is getting executed only one time. You may encounter the error : 'Maximum trigger depth exceeded', if recursion is not handled well. You can use Static Boolean variable in apex class and check the variable in Apex Trigger IF it is true then execute your logic and make it false so that trigger can not execute Again.

eg. In After Update trigger we are updating some other records.

Solution:

``` java
public class checkRecursive {
  Public static Boolean firstcall=false;
}
```

``` java
Trigger feedback on contact (after update) {
  if(!checkRecursive.firstcall) {
    checkRecursive.firstcall = true;
    Id conId;
    for(contact c:trigger.new){
        conId=c.Id;
    }
    Contact con=[select id, name from contact where id!=:conId limit 1];
    con.email=‘test@gmail.com’;
    Update con;
  }
}
```

> Static in Salesforce are per transaction, so the value will be true only for the current transaction. It will be initialized to true for other transactions. Don't think of static in Java term where static values persist till the class is loaded into memory.

Ref : <https://help.salesforce.com/s/articleView?id=000386331&type=1>
