# 3. SOQL (Salesforce Object Query Language)

- MAX statement size - 20k char
- MAX where clause size - 4k char

## SOQL Vs SQL

- We can only query records, we can't insert or update or delete records using SOQL.
- We can't use * in select statement.
- We can use .(dot) operator
- Join doesn't exist in SOQL. Relationship exist in SOQL.

## Parent-to-child

- Limits: **20** Parent-to-child relationship per query.
- **No more than 1 level**: ```SELECT Name, (SELECT Contact.Name, FROM Contacts) FROM Account```

**Note:** 'Contacts' is **Child relationship name**, can be found in child object.

## Child-to-Parent

- Limits: **55** Child-to-Parent relationship per query.
- **No more than 5 level**: ```Contact.Account.Owner.Firstname``` (3 Levels)

**Note:** 'Owner' is **Field name**

## Date Literals

1. TODAY
2. YESTERDAY
3. TOMORROW
4. [LAST/THIS/NEXT]_WEEK
5. [LAST/THIS/NEXT]_MONTH
6. [LAST/THIS/NEXT]_QUARTER
7. [LAST/THIS/NEXT]_YEAR
8. [LAST/NEXT]_N_[WEEK/MONTH/QUARTER/YEAR]:n

## Bind Variables

```
String nameVar = 'Ankesh';
List<Contact> contacts = [SELECT ID, Name FROM Contact WHERE Name=:nameVar];
```

## Dynamic SOQL Queries

```
Integer a = 369;
String stringQuery = 'SELECT ID, Name FROM Contact';
if(a<100){
  stringQuery += 'WHERE Name=\'Ankesh\'';
}

List<Contact> contacts = Database.query(stringQuery);
```
