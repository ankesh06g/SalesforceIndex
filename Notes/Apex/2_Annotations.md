# 2. Annotations

- modifies the way that a method or class is used
- To add an annotation to a method, specify it immediately before the method or class definition

### 2.1 @deprecate

```
@deprecated
  // This method is deprecated. Use myOptimizedMethod(String a, String b) instead.
  global void myMethod(String a) {
   
}
```

### 2.2 @AuraEnabled(cacheable=true)

makes methods available to your Lightning components (both Lightning web components and Aura components).
```
@AuraEnabled(cacheable=true){
  public static List<Account> getAllAccounts(){
    return accounts;
  }
}
```

### 2.2 @Future
To clreat futur methods

### 2.4 @InvocableMethod
Makes method to called from Process Builder and Flows
