## Classes Should Be Small!

first rule of classes is that they should be small.

## The Single Responsibility Principle


a class or module should have one,
and only one, reason to change. This principle gives us both a definition of responsibility,
and a guidelines for class size. Classes should have one responsibility

## Cohesion
Classes should have a small number of instance variables.
More variables a method manipulates the more cohesive that method is to its class. A class in which each variable is used by each method is maximally cohesive.

When classes lose cohesion, split them!
So breaking a large function into many smaller functions often gives us the opportunity
to split several smaller classes out as well. This gives our program a much better organization
and a more transparent structure.