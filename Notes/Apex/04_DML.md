# DML (Data Manipulation Language)

- **150** DML Statements allowed per Apex class
- **10,000** records can be handled per DML

## 4.1 Operations

1. Insert - Sysntax: ```insert sObject|sObject[]; ```

  ``` java
  Account newAcct = new Account(name = 'Acme');
  try {
    insert newAcct;
  } catch (DmlException e) {
  // Process exception here
  }
  ```

2. Update
3. Upsert
4. Delete
5. Undelete

  ``` java
  Account[] savedAccts = [SELECT Id, Name FROM Account WHERE Name = 'Universal Containers' ALL ROWS]; 
  try {
      undelete savedAccts;
  } catch (DmlException e) {
      // Process exception here
  }
  ```

6. Merge - The merge statement merges **up to three records of the same sObject** type into one of the records, deleting the others.
  Sysntax: ```merge sObject sObject|sObject[]|ID|ID[]```

  ``` java
  List<Account> ls = new List<Account>{new Account(name='Acme Inc.'),new Account(name='Acme')};
  insert ls;
  Account masterAcct = [SELECT Id, Name FROM Account WHERE Name = 'Acme Inc.' LIMIT 1];
  Account mergeAcct = [SELECT Id, Name FROM Account WHERE Name = 'Acme' LIMIT 1];
  try {
      merge masterAcct mergeAcct;
  } catch (DmlException e) {
      // Process exception here
  }
```

## 4.2 Database

**Database is Class and Namespace also.**


### Database Class

Namespace : System
Methods:

1. countQuery()
2. insert()
3. delete()
4. emptyRecycleBin()
5. getDeleted()
6. getQueryLocator()
7. query()
8. merge()
9. undelete()
10. update()
11. convertLead()

### Database Namespace

Classes:

1. QueryLocator - getQuery(), iterator()
2. QueryLocatorIterator
3. work in progress...

  ``` java
  ```

  ``` java
  String query = 'select id from account';
  System.debug(Database.getQueryLocator(query));

  Database.QueryLocator q = Database.getQueryLocator(query);
  System.debug(q.getQuery());
  Database.QueryLocatorIterator it = q.iterator();
  System.debug(it);

  while(it.hasNext()){
    Account a = (Account)it.next();
    System.debug(a);
  }
  ```
