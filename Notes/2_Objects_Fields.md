# Building Blocks

1. Tabs: To access object
2. Profile : collection of settings and permissions
3. Object: Single table
4. Fields : Idividual data point of object
5. Records : Instance of object with field values

**App -> Object -> Tab**

## Creating App

1. New cutom app
2. Select logo
3. Select Tabs and default tab
4. Select pofile

## Creating Object

1. API Name
2. Plural Name
3. Default field and it's dataType

## Creating Tab

1. Select Object
2. Tab Icon
3. Select profile (Default all profile)
4. Select App (Default all apps)

## Creating Field

1. API Name
2. Length
3. Default value/ Fomula
4. Select Profile (Field-Level Security)
5. Select Page Layout

## Creting Pick List

- Either manually type values or **Picklist/Global value set**
- We can also use **Field Dependancy**

## Relationships

### 1. Master-Detail

- Child object can't exist without parent object
- Child object will inherit all the sharing setting and rule from parent object
- Cascad Delete
- You can create a **RollUp-Summery** field on Master record to summerise child records

### 2. Lookup

- Child object can exist without parent object
- No sharing will inherited
- No Cascad delete

## Page Layout

Can be edited by either

- Lightning App Builer (From gear icon)
- Object's Page layouts

## Validation Rule

We can create a validation rule baed on the fields. We can select the error msg and also the position of error msg