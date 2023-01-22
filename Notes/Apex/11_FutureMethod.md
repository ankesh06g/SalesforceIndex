# Async Apex

>**50 async methods allowed per apex class**

## Future Method

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
