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
```

## The Law of Demeter