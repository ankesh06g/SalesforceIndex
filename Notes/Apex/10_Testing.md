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

## Loading static resources

1. Create a .csv
2. Create a static resource for the .csv file:
    1. From Setup, enter Static Resources in the Quick Find box, then select Static Resources.
    2. Click New.
    3. Name your static resource testAccounts.
    4. Choose the file you created.
    5. Click Save.
3. Call Test.loadData in a test method to populate the test accounts.

``` java
@isTest 
private class DataUtil {
    static testmethod void testLoadData() {
        // Load the test accounts from the static resource
        List<sObject> ls = Test.loadData(Account.sObjectType, 'testAccounts');
        // Verify that all 3 test accounts were created
        System.assert(ls.size() == 3);

        // Get first test account
        Account a1 = (Account)ls[0];
        String acctName = a1.Name;
        System.debug(acctName);

        // Perform some testing using the test records
    }
}
```
