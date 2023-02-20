# Exception Handling

**As soon as exception thrown complete transation will Rollback.**

``` java
try{
  // Operation
}
catch(Exception e){
  // Catch can be multiple
}
finally{
  // Executes everytime at the end
}
```

## Exception Methods

``` java
try{
  Account accRec = new Account();
  insert accRec;
} catch(Exception e){
  system.debug('Cause '+e.getCause());
  system.debug('Message '+e.getMessage());
  system.debug('Line Number '+e.getLineNumber());
  system.debug('Stack Trace '+e.getStackTraceString ());
} finally {
  System.debug('finally called ');
}
```

## Custom exception

- A custom exception class must extend the system Exception class
- make sure your class name ends with the word Exception, such as “MyException” or “PurchaseException”
- A custom exception class can implement one or many interfaces.

``` java
public class ProcessException extends Exception {

}
```

``` java
try{
  throw new ProcessException('My custom exception');
} catch(Exception e){
  system.debug('Cause '+e.getCause());
  system.debug('Message '+e.getMessage());
  system.debug('Line Number '+e.getLineNumber());
  system.debug('Stack Trace '+e.getStackTraceString ());
} finally {
  System.debug('finally called ');
}
```