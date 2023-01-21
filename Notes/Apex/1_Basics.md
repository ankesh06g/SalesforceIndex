# 1 Apex Basics

## 1.1 Primitive Datatypes

1. Boolean
2. String
3. Integer
4. Long
5. Decimal
6. Double
7. Date
8. Time
9. Datetime
10. Blob
11. Id

## 1.2 Collections

1. List
2. Set
3. Map

## 1.3 Constant

Use **final** keyword for constants.

## 1.4 Access Mpdifier

| Access Modifier | Within Outer Class | Inner Class | Extended Class | Within Namespace| All |
|-----------------|--------------------|-------------|----------------|-----------------|-----|
|Private          | * | | | | |
|Protected        | * | * | * | | |
|Public           | * | * | * | * | |
|Global           | * | * | * | * | * |

## 1.5 List iteration using for loop

eg:

```
List<String> list = new List<String>();

for(String s : list){
  System.debug(s);
}
```

## 1.6 Method Overloading vs Overriding

**Method Overloading** - In same class, multiple methods with same name but different parameters or return type. Also call **Polymorphism**.
**Method Overriding** - 2 or more class, Same methods name with same parameters and return type.

## 1.7 Static Keyword

1. **Static Variable:**  All object can access the same instance of variable.
2. **Static Methods:** This method can access directly by class name ie. no need to careate objects.

## 1.8 Naming Conventions

1. Class, Interface : Pascal case
2. Method, Variable : Camal case
3. Contanst: Capital Snake case

## 1.9 Constructor

- Name of constructor is same as class name
- Automatically called when object is created
- We can create multiple constructor with diff parameters
- use this(); method to call empty constructor from another constructor
- If you want to execute both empty and parameterized constructor then, Empty constuctor needs to be execurte first

```
puclic class Student{
  Student(){
    System.debug("called empty constructor");
  }
  Student(String a){
    System.debug("called parameterized constructor");
  }
  Student(String a, String b){
    this();
    System.debug("called parameterized constructor");
  }
}
```

## 1.10 Initialization Block

- Similar to constuctor, gets executed when object is created, but you can't accept paramenters.
- can have multiple Initialization blocks
- Normatl Initialization block : Attached to each instance of a class, so doen't share values.
- Static Initialization block: Attached to the class and shared across the org.

```
// Initialization block
{
  // some code 
}

// Static Initialization block
Static {
  // some code 
}
```

## 1.11 Life Cycle of Apex class

1. Static Initialization block
2. Normal Initialization block
3. Constructor

## 1.12 Wraper class or Inner class

**Note:** Static keyword can't be used inside inner class.

```
Calss Student{
  String name;
  Integer Number;
  List<Subject> sub = new List<Subject>();

  puclic addSubject(Sting name, Integer marks){
    Subject s = new Subject(name, marks);
    sub.add(s);
  }

  Class Subject{
    String name;
    Integer marks;
    Subject(String name, Integer marks){
      this.name = name;
      this.marks = marks;
    }
  }
}
```
## 1.13 Best Practices

- Bulkify your data manipulation language (DML) statements and use the built-in Limits methods. For more information about Limits methods, see the resources at the end of this unit.
- Write comments with a good balance between quality and quantity (explain, but don't over-explain). Always provide documentation comments (method and class headers). Provide inline comments only when necessary to clarify complex code.
- Avoid nesting loops within loops.
- Avoid SOQL queries and DML statements inside loops.
- Keep logic out of triggers. (Instead, use a trigger framework.)
- Create relationships between objects to reduce your number of queries.
- Avoid hard coded IDs and constants.
- Increase readability by indenting code and breaking up long lines.
- Break methods into multiple smaller methods if possible, making your code more modular and easier to read and maintain.
- Last but not least: adhere to the security guidelines covered in the Develop Secure Web Apps trail. This includes declaring a sharing keyword for every class, and making efforts to prevent XSS and SQL injection.
