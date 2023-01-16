# SObject Class

Namespace: System

Methods:

## 1. Retrieving Field

get() - returns as 'object' value which needs to be typecasted to a primitive datatype.

``` java
List<SObject> contacts = [SELECT Name from Contact];
for(SObject c: contacts){
  System.debug((String)c.get('Name'));
}
```

## 2. Child-to-Parent - getSObject()

``` java
List<SObject> contacts = [SELECT Name, Account.Name from Contact];
for(SObject c: contacts){
  System.debug((String)c.getSObject('Account').get('Name'));
}
```

## 3. Parent-to-Child - getSObjects()

Methods : get(), getSObjects()

``` java
List<SObject> accounts = [SELECT Name, (select name from contacts) from Account];
for(SObject a: accounts){
  System.debug((String)a.get('Name'));
  for(SObject c: a.getSObjects('Contacts')){
    System.debug((String)c.get('Name'));
  } 
}
```

## 4. Creating new record

Methods : put(), putSObject()

``` java
SObject account = (SObject) Type.forName('Account').newInstance();
account.put('Name', 'Sample account');
account.put('Phone', '1234567895');
Insert account;

SObject con = (SObject) Type.forName('Contact').newInstance();
con.put('lastname', 'AcmeCon');
con.putSObject('Account', account);
Insert con;
```

## 5. Clearing SObject

``` java
Account acc = new account(Name = 'Acme');
acc.clear();
Account expected = new Account();
system.assertEquals(expected, acc);
```

## 6. Clone

Only clones fields which are fetched from query.

``` java
Account a = [select id, name from account where id ='0012w00001Gx02LAAR'];
Account b = a.clone();
Insert b; // Clones only name field. Other fields will not clone.
```

