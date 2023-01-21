# Testing

- **At least 75% code coverage required to deploy code in salesforce.**
- **Test-runner** is a software which takes care of running test cases and calculating code coverage

## What to test?

1. Single Action
2. Bulk Action
3. Positive Behavior
4. Negative Behavior
5. Restricted users (use ```System.runAs(User obj){}```)

``` java
System.runAs(u) {
    // The following code runs as user 'u'
    System.debug('Current User: ' + UserInfo.getUserName());
    System.debug('Current Profile: ' + UserInfo.getProfileId());
}
```

## Assert Methods

- System.assert(a<10);
- System.assert(a<10, "Not less that 10");
- System.assertEquals(a, 10);
- System.assertEquals(a, 10, "Not equal to 10");
- System.assertNotEquals(a, 10);
- System.assertNotEquals(a, 10, "Not equal 10");

## Test Class Methods

### 1. startTest()

Resets governer limits. Use this method when you are testing governor limits.

### 2. stopTest()

Marks the point in your test code when your test ends.

## testSetup()

- No Arguments
- No Return Value
- Only one testSetup method per test class allowed

## seeAllData=true

- Can access org data using this. But this is not recommended.
- Can't use with testSetup method. At a time any one is allowed.

## Test Data Factory

- We can seperate class for test data creation. This class must have isTest annotation.
- Methods inside this class will be mostly static and doesn't contain isTest annotation.

