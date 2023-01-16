# Triger

Allows us to perform action before and after changes to salesforce record.

Insert
Update
Delete
Merge
Upsert
Undelete

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
