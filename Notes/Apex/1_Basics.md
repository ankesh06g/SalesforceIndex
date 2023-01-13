# Apex

## Primitive Datatypes

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

## Collections

1. List
2. Set
3. Map

## Constant

Use **final** keyword for constants.

## Access Mpdifier

| Access Modifier | Within Outer Class | Inner Class | Extended Class | Within Namespace| All |
|-----------------|--------------------|-------------|----------------|-----------------|-----|
|Private          | * | | | | |
|Protected        | * | * | * | | |
|Public           | * | * | * | * | |
|Global           | * | * | * | * | * |

## List iteration using for loop

eg:

```
List<String> list = new List<String>();

for(String s : list){
  System.debug(s);
}
```

## Method Overloading vs Overriding

**Method Overloading** - In same class, multiple methods with same name but different parameters or return type. Also call **Polymorphism**.
**Method Overriding** - 2 or more class, Same methods name with same parameters and return type.

## Static Keyword

1. **Static Variable:**  All object can access the same instance of variable.
2. **Static Methods:** This method can access directly by class name ie. no need to careate objects.

## Naming Conventions

1. Class, Interface : Pascal case
2. Method, Variable : Camal case
3. Contanst: Capital Snake case

## Constructor

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

## Initialization Block

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

## Life Cycle of Apex class

1. Static Initialization block
2. Normal Initialization block
3. Constructor

## Wraper class or Inner class

```
Calss Studen{
  String name;
  Integer Number;
  List<Subject> sub = new List<Subject>();

  puclic addSucject(Sting name, Integer marks){
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
