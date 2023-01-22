# Async Apex

>**50 async methods allowed per apex class**

## 1. Future Method

- Runs in it's own thread
- Executes when system resources are free
- Must be static
- Must have void return type
- Parameters must be Primitive data types or collecction of primitive data types
- You can't call any async process[batch,schedule,future,queable] from the Future method.

### When to use?

1. When you have a long-running method and need to prevent delaying an Apex transaction
2. When you make callouts to external Web services
3. To segregate DML operations and bypass the **mixed DML error**

>**Mixed DML Operation Error**
>
> This error comes when you try to perform DML operations on setup and non-setup objects in a single transaction.<br>
> Setup Objects :- ObjectPermissions, PermissionSet, PermissionSetAssignment, QueueSObject, Territory, UserTerritory, UserRole, User

``` java
global class FutureMethodRecordProcessing
{
    @future
    public static void processRecords(List<ID> recordIds)
    {   
         // Get those records based on the IDs
         List<Account> accts = [SELECT Name FROM Account WHERE Id IN :recordIds];
         // Process records
    }
}
```

### Callouts in Future Method

``` java
global class FutureMethodExample
{
    @future(callout=true)
    public static void getStockQuotes(String acctName)
    {   
         // Perform a callout to an external service
    }

}
```

## 2. Batch Apex

Contains 3 methods : Start, Execute, Finish 

Batch Job Status:

1. Holding
2. Queued
3. Preparing
4. Processing
5. Aborted
6. Completed
7. Failed

### When to use?

1. For long-running jobs with large data volumes that need to be performed in batches, such as database maintenance jobs
2. For jobs that need larger query results than regular transactions allow

### 2.1 Start Method

- Executes only once and returns records.

``` java
public (Database.QueryLocator | Iterable<sObject>) start(Database.BatchableContext bc) {}
```

### 2.2 Execute Method

- Must retirn **Void**
- This mehod get executed for no of batches. (total records/batch size)
- Each execute will get new set f gov limits

``` java
public void execute(Database.BatchableContext BC, list<P>){}
```

### 2.3 Finish Method

- Executes only once and after executing all batches
- To send confirmation emails or execute post-processing operations

``` java
public void finish(Database.BatchableContext BC){}
```

### Executing Batch

#### 1. Database.executeBatch

- Takes 2 parameters. Instance and batch size(default 200, range 0-2000)
- The Database.executeBatch method returns the ID of the AsyncApexJob object, which you can use to track the progress of the job.

``` java
MyBatchClass bc = new MyBatchClass();
ID batchprocessid = Database.executeBatch(bc, 10);

AsyncApexJob aaj = [SELECT Id, Status, JobItemsProcessed, TotalJobItems, NumberOfErrors 
                    FROM AsyncApexJob WHERE ID =: batchprocessid ];
```

#### 2. System.scheduleBatch

- Takes 4 parameters. Instance, JobName, TimeInterval, OptionalScopeValue
- The System.scheduleBatch method returns the scheduled job ID (CronTrigger ID) which is used to query CronTrigger to get the status of the corresponding scheduled job.

``` java
MyBatchClass bc = new MyBatchClass();
String cronID = System.scheduleBatch(bc, 'job example', 60);

CronTrigger ct = [SELECT Id, TimesTriggered, NextFireTime
                FROM CronTrigger WHERE Id = :cronID];

// TimesTriggered should be 0 because the job hasn't started yet.
System.assertEquals(0, ct.TimesTriggered);
System.debug('Next fire time: ' + ct.NextFireTime); 
// For example:
// Next fire time: 2013-06-03 13:31:23
```

### Callouts in Batch Apex

``` java
public class SearchAndReplace implements Database.Batchable<sObject>, Database.AllowsCallouts{
  // 3 methods
}
