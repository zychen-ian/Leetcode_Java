###Object Oriented Design

OOD is more about communication, less about writing lots of code, more about drawing diagram, less about giving specific implementation. 

yet, you will still be asked to implement a certain key function sometimes



**S.O.L.I.D** Principles for Object Oriented Design

- **S** - Single-responsiblity principle
- **O** - Open-closed principle
- **L** - Liskov substitution principle
- **I** - Interface segregation principle
- **D** - Dependency Inversion Principle



Reference:

https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design



####Single-responsiblity principle

A class should have one and only one reason to change, meaning that a class should have only one job.

```java
// BAD PRACTICE
public class AreaCalculator {
   private float result;
  
   public float calculateArea(Shape s) {
        
   }
   
   public String printAreaAccuateToOneDecimalPlace() {
       
   }
}
```

```
The problem with the output method is that the AreaCalculator handles the logic to output the data. Therefore, what if the user wanted to output the data as json or something else?

All of that logic would be handled by the AreaCalculator class, this is what SRP frowns against; the AreaCalculator class should only sum the areas of provided shapes, it should not care whether the user wants json or HTML.

To fix this, you can create an SumCalculatorOutputter class and use this to handle whatever logic you need to handle how the sum areas of all provided shapes are displayed.
```



####Open-closed principle

<u>Objects or entities</u> should be open for extension, but closed for modification. This simply means that a class should be <u>easily extendable without modifying the class itself</u>.

````
It means that your classes should be designed such a way that whenever fellow developers wants to change the flow of control in specific conditions in application, all they need to extend your class and override some functions and that’s it.

For example, if you take a look into any good framework like struts or spring, you will see that you can not change their core logic and request processing, BUT you modify the desired application flow just by extending some classes and plugin them in configuration files.
````



```java
// BAD PRACTICE
public class AreaCalculator {
  
   public float calculateArea(Triangle t) {
        
   }
   
   public float calculateArea(Rectangle r) {
        
   }
}

// BAD PRACTICE
public function sum() {
    foreach($this->shapes as $shape) {
        if(is_a($shape, 'Square')) {
            $area[] = pow($shape->length, 2);
        } else if(is_a($shape, 'Circle')) {
            $area[] = pi() * pow($shape->radius, 2);
        }
    }
    return array_sum($area);
}  
```

```
If we wanted the sum method to be able to sum the areas of more shapes, we would have to add more if/else blocks and that goes against the Open-closed principle.

A way we can make this sum method better is to remove the logic to calculate the area of each shape out of the sum method and attach it to the shape's class.

Coding to an interface is an integral part of S.O.L.I.D
```

```java
interface ShapeInterface {
    public function area();
}

class Circle implements ShapeInterface {
    public $radius;

    public function __construct($radius) {
        $this->radius = $radius;
    }

    public function area() {
        return pi() * pow($this->radius, 2);
    }
}  

class AreaCalculator {
    public function sum() {
        foreach($this->shapes as $shape) {
            if(is_a($shape, 'ShapeInterface')) {
                $area[] = $shape->area();
                continue;
            }

            throw new AreaCalculatorInvalidShapeException;
        }

        return array_sum($area);
    } 
}
```





####Liskov substitution principle

All this is stating is that every subclass/derived class should be substitutable for their base/parent class. In other words, as simple as that, a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.

It means that the classes fellow developer created by extending your class should be able to fit in application without failure. I.e. if a fellow developer poorly extended some part of your class and injected into framework/ application then it should not break the application or should not throw fatal **exceptions**.

This can be insured by using strictly following first rule. If your base class is doing one thing strictly, the fellow developer will override only one feature incorrectly in worst case. This can cause some errors in one area, but whole application will not do down.



####Interface Segregation Principle

A client should never be forced to implement an interface that it doesn't use or clients shouldn't be forced to depend on methods they do not use.

```java
// BAD PRACTICE
public interface Shape {
   public float calculateArea();
   public float calculateVolumn();
}
public class Rectangle implements Shape {  
}
public class Cube implements Shape {  
}
```

```
Any shape we create must implement the calculateVolumn method, but we know that squares are flat shapes and that they do not have volumes, so this interface would force the Square class to implement a method that it has no use of.

Instead you could create another interface called SolidShapeInterface that has the volume contract and solid shapes like cubes e.t.c can implement this interface:
```



```java
interface ShapeInterface {
    public function area();
}

interface SolidShapeInterface {
    public function volume();
}

class Cuboid implements ShapeInterface, SolidShapeInterface {
    public function area() {
        // calculate the surface area of the cuboid
    }

    public function volume() {
        // calculate the volume of the cuboid
    }
}
```

This is a much better approach, but <u>a pitfall to watch out for is when type-hinting these interfaces, instead of using a **ShapeInterface** or a **SolidShapeInterface**.</u>

You can create another interface, maybe **ManageShapeInterface**, and implement it on both the flat and solid shapes, this way you can easily see that it has a single API for managing the shapes. For example:

```java
interface ManageShapeInterface {
    public function calculate();
}

class Square implements ShapeInterface, ManageShapeInterface {
    public function area() { /*Do stuff here*/ }

    public function calculate() {
        return $this->area();
    }
}

class Cuboid implements ShapeInterface, SolidShapeInterface, ManageShapeInterface {
    public function area() { /*Do stuff here*/ }
    public function volume() { /*Do stuff here*/ }

    public function calculate() {
        return $this->area() + $this->volume();
    }
}    
```

Now in **AreaCalculator** class, we can easily <u>replace the call to the **area** method with **calculate**</u> and also check if the object is an instance of the **ManageShapeInterface** and not the **ShapeInterface**.



####Dependency Inversion Principle

Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions. 



```java
// BAD PRACTICE
class PasswordReminder {
    private $dbConnection;

    public function __construct(MySQLConnection $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}
```

```
First the MySQLConnection is the low level module while the PasswordReminder is high level, but according to the definition of D in S.O.L.I.D. which states that Depend on Abstraction not on concretions, this snippet above violates this principle as the PasswordReminder class is being forced to depend on the MySQLConnection class.

Later if you were to change the database engine, you would also have to edit the PasswordReminder class and thus violates Open-close principle.
```

The **PasswordReminder** class should not care what database your application uses, to fix this again we "code to an interface", since high level and low level modules should depend on abstraction, we can create an interface:

The interface has a connect method and the **MySQLConnection** class implements this interface, also instead of directly type-hinting **MySQLConnection** class in the constructor of the **PasswordReminder**, we instead type-hint the interface and no matter the type of database your application uses, the **PasswordReminder** class can easily connect to the database without any problems and **OCP** is not violated.

```java
interface DBConnectionInterface {
    public function connect();
}   

class MySQLConnection implements DBConnectionInterface {
    public function connect() {
        return "Database connection";
    }
}

class PasswordReminder {
    private $dbConnection;

    public function __construct(DBConnectionInterface $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}  
```



Another Example with Good Practice

```java
public class AreaCalculator { // high-level
    public float calculateArea(ShapeInterface s) { // high-level
        return s.area();
    }
}

interface ShapeInterface {
    public float area();
}

public class Rectangle implements ShapeInterface {
    private float length;
    private float width;
    public float area() {...}
}

public class Triangle implements ShapeInterface {
    private float height;
    private float width;
    public float area() {...}
}
```



**5C解题法**

Clarify - 通过和面试官交流，去除题目中的歧义，确定答题范围

Core objects - 确定题目所涉及的类，以及类之间的映射关系                       

Cases - 确定题目中所需要实现的场景和功能                   

Classes - 通过类图的方式，具体填充题目中涉及的类                      

Correctness - 检查自己的设计，是否满足关键点                   



















