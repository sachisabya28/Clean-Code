Unit tests to code flexible, maintainable, and reusable. 

## Clean Tests

## Single Concept per Test

better rule is that we want to test a single concept in each test function.

This test should be split up into three independent tests
because it tests three independent things.
```
SerialDate d1 = SerialDate.createInstance(31, 5, 2004);
SerialDate d2 = SerialDate.addMonths(1, d1);
assertEquals(30, d2.getDayOfMonth());
assertEquals(6, d2.getMonth());
assertEquals(2004, d2.getYYYY());

SerialDate d3 = SerialDate.addMonths(2, d1);
assertEquals(31, d3.getDayOfMonth());
assertEquals(7, d3.getMonth());
assertEquals(2004, d3.getYYYY());

SerialDate d4 = SerialDate.addMonths(1, SerialDate.addMonths(1, d1));
assertEquals(30, d4.getDayOfMonth());
assertEquals(7, d4.getMonth());
assertEquals(2004, d4.getYYYY());
```


## Clean tests follow five other rules

* Fast Tests should be fast. They should run quickly.
When tests run slow, you won’t want
to run them frequently. If you don’t run them frequently, you won’t find problems early
enough to fix them easily.

* Independent Tests should not depend on each other. One test should not set up the conditions
for the next test

* Repeatable Tests should be repeatable in any environment. You should be able to run the
tests in the production environment, in the QA environment,

* Self-Validating The tests should have a boolean output. Either they pass or fail. You
should not have to read through a log file to tell whether the tests pass. 

* Timely The tests need to be written in a timely fashion. Unit tests should be written just
before the production code that makes them pass.