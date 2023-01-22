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
