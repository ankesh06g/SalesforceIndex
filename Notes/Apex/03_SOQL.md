# 3. SOQL (Salesforce Object Query Language)

- MAX statement size - 20k char
- MAX where clause size - 4k char

## 3.1 SOQL Vs SQL

- We can only query records, we can't insert or update or delete records using SOQL.
- We can't use * in select statement.
- We can use .(dot) operator
- Join doesn't exist in SOQL. Relationship exist in SOQL.

## 3.2 Parent-to-child

- Limits: **20** Parent-to-child relationship per query.
- **No more than 1 level**:

```
// Parent__c : Name
// Child__c : Name, My_Parent__c(Child Relationship Name:Childrens)
select Id, (select Id, Name from Childrens__r) from  Parent__c
```
Accessing paarent-to-child in Apex:
```
for(Parent__c p: [select Id, Name,(select Id, Name from Childrens__r) from  Parent__c]){
    for(Child__c c:p.Childrens__r){
        System.debug('Parent : ' + p.Name + ' -- Child : '+c.Name);
    }
}
```

**Note:** 'Contacts' is **Child relationship name**, can be found in child object.

## 3.3 Child-to-Parent

- Limits: **55** Child-to-Parent relationship per query.
- **No more than 5 level**: ```select Id, My_Parent__c, My_Parent__r.Name from Child__c``` (3 Levels)

**Note:** 'Owner' is **Field name**

## 3.4 Date Literals

1. TODAY
2. YESTERDAY
3. TOMORROW
4. [LAST/THIS/NEXT]_WEEK
5. [LAST/THIS/NEXT]_MONTH
6. [LAST/THIS/NEXT]_QUARTER
7. [LAST/THIS/NEXT]_YEAR
8. [LAST/NEXT]_N_[WEEK/MONTH/QUARTER/YEAR]:n

## 3.5 Bind Variables

``` java
String nameVar = 'Ankesh';
List<Contact> contacts = [SELECT ID, Name FROM Contact WHERE Name=:nameVar];
```

## 3.6 ALL ROWS

To get all records including deleted and archived records.

```isDeleted = True``` for deleted records.
```isArchived = True``` fro archived records(Doesn't mean deleted, after some time period salesforce automatically moves old data from primary storage to secodary storage. This data is not visible in UI, we have to explicitly query them.)

## 3.7 FIELDS(ALL|STANDARD|CUSTOM)

- Selects all fields of an object. Similar to *.
- FIELDS(STANDARD) is bounded, so can use in Apex;
- FIELDS(ALL) and FIELDS(CUSTOM) condidered as unbounded, hece can't use in apex.
- FIELDS(ALL) and FIELDS(CUSTOM) works in query editor.

## 3.8 Dynamic SOQL Queries

Allows to make a dynamic SOQL query at runtime.

``` java
Integer a = 369;
String stringQuery = 'SELECT ID, Name FROM Contact';
if(a<100){
  stringQuery += 'WHERE Name=\'Ankesh\'';
}

List<Contact> contacts = Database.query(stringQuery);
```

Disadvantage: SOQL Injection
Solution: Use ```String.escapeSingleQuotes(String);```

## 3.9 Aggregate Functions

``` java
AggregateResult[] groupedResult = [SELECT AVG(Anount), MAX(Amount) FROM opportunity];

Double avgAmount = Double.valueOf(groupedResult[0].get('expr0'));
Double maxAmount = Double.valueOf(groupedResult[0].get('expr1'));
```

``` java
AggregateResult[] groupedResult = [SELECT AVG(Anount) avgAmount, MAX(Amount) maxAmount FROM opportunity];

Double avgAmount = Double.valueOf(groupedResult[0].get('avgAmount'));
Double maxAmount = Double.valueOf(groupedResult[0].get('maxAmount'));
```
