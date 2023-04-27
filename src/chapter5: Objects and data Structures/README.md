# Object and Data structures

## Data Abstraction

Hiding implementation is about abstractions. But, it doesn’t simply make the variables private and </br> 
uses getters and setters to access these variables. Rather it exposes abstract interfaces
that allow its users to manipulate the  </br>
essence of the data, without having to know its implementation. For example:

```
public interface Vehicle {
    double getFuelTankCapacityInGallons();
    double getGallonsOfGasoline();
}
```
```
public interface Vehicle {
double getPercentFuelRemaining();
}
```

## Data/Object Anti-Symmetry

Objects hide
their data behind abstractions and expose functions that operate on that data. Data structure
expose their data and have no meaningful functions.

```
class Square:
    topLeft = 0
    side = 0

class Rectangle:
    topLeft = 0
    height = 0
    width = 0

class Circle {
    center = 
    radius = 0
}

class Geometry:
    double PI = 3.141592653589793;
    def area(shape):
        if (shape.instance(Square)):
        s = Square;
        return s.side * s.side;
        elseif (shape.instance(Square)):
        .....
```

#### Polymorphic Shapes

Procedural code (code using data structures) makes it easy to add new functions without
changing the existing data structures. OO code, on the other hand, makes it easy to add
new classes without changing existing functions.

```
class Square(Shape):
    name    = "Square"
    width   = 0        # A default value 

    def __init__(self, width):
        self.width = width

    def get_area(self):
        return width * width

class Triangle(Shape):
    name    = "Triangle"
    width   = 0
    height  = 0

    def __init__(self, width, height):
        self.width = width
        self.height = height 

    def get_area(self):
        return 0.5 * width * height 
```

## The Law of Demeter

the Law of Demeter says that a method f of a class C should only call
the methods of these:
• C
• An object created by f
• An object passed as an argument to f
• An object held in an instance variable of C

```
Bad practice
outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath()
```


```
Good practice
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

