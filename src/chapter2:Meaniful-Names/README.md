# Meaningful names

The name of a variable, function, or class, should answer all the big questions. It
should tell you why it exists, what it does, and how it is used. If a name requires a comment,
then the name does not reveal its intent.

## Use Intention-Revealing Names

```python
int d; // elapsed time in days
```
The name d reveals nothing. It does not evoke a sense of elapsed time, nor of days

int elapsedTimeInDays;
int daysSinceCreation;

```python
def getThem():
    list1 = []
    for i in theList:
        if (x[i] == 4)
        list1.add(x)
    return list1
```

1. What kinds of things are in theList?
2. What is the significance of the zeroth subscript of an item in theList?
3. What is the significance of the value 4?
4. How would I use the list being returned?


```python
def getFlaggedCells():
    flagged_cells = []
    for cell in gameBoard:
        if (cell.isFlagged())
        flaggedCells.append(cell)
    return flaggedCells
```

With these simple name changes, it’s not difficult to understand what’s going on. <br />
This is the power of choosing good names.

## Avoid Disinformation

A truly awful example of disinformative names would be the use of lower-case <br />
L or uppercase O as variable names, especially in combination.

```python
int a = l
if ( O == l )
    a = O1
else
    l = 01
```

must avoid leaving false clues that obscure the meaning of code <br />
hp, aix, and sco would be poor variable names if you are coding <br />
a hypotenuse and hp looks like a good abbreviation, it could be disinformative. 


the variable moneyAmount is indistinguishable from money, <br />
customerInfo is indistinguishable from customer, <br />
accountData is indistinguishable from account, <br />
and theMessage is indistinguishable from message. <br />


- getActiveAccount();
- getActiveAccounts();
- getActiveAccountInfo();

How are the programmers in this project supposed to know which of these functions to call?

Distinguish names in such a way that the reader knows what the differences offer.

## Use Searchable Names

single-letter names can ONLY be used as local variables inside short methods
One might easily grep for MAX_CLASSES_PER_STUDENT, but the number 7 could be more
troublesome


If a variable or constant might be seen or used in multiple places in a body of code, it is <br />
imperative to give it a search-friendly name.

```python
for i in range(50): 
    s += (t[j]*4)/5
```

to

```python
realDaysPerIdealDay = 4
WORK_DAYS_PER_WEEK = 5
int sum = 0
for i in range(NUMBER_OF_TASKS):
    realTaskDays = taskEstimate[j] * realDaysPerIdealDay
    realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK)
    sum += realTaskWeeks
```

## Class names

Classes and objects should have noun or noun phrase names like  <br /> 
Customer, WikiPage, Account, and AddressParser. 
Avoid words like Manager, Processor, Data, or Info in the nameof a class. <br />
A class name should not be a verb. 

Methods should have verb or verb phrase names like postPayment, deletePage, or save.

name = employee.getName()
customer.set_name("mike")
if (paycheck.is_posted())...

Say what you mean. Mean what you say.
Don’t tell little culture-dependent jokes like
eatMyShorts() to mean abort().

## Meaniful context

```python

def printGuessStatistics(candidate, count) 
String number
String verb
String pluralModifier
if (count == 0):
    number = "no"
    verb = "are"
    pluralModifier = "s"
elif (count == 1):
    number = "1"
    verb = "is"
    pluralModifier = ""
else:
    number = Integer.toString(count)
    verb = "are"
    pluralModifier = "s"
guessMessage = String.format(
"There %s %s %s%s", verb, number, candidate, pluralModifier)
print(guessMessage)
```

the method, the meanings of the variables are opaque.
The improvement of context also allows the algorithm to be 
made much cleaner by breaking it into many smaller functions

```python
class GuessStatisticsMessage:
    def __init__():
        number = 0
        verb = ""
        pluralModifier = ""
    def make(candidate, count):
    create_plural_dependent_message_parts(count)
        return "There {} {} {}{}".format(verb, number, candidate, pluralModifier)

    def create_plural_dependent_message_parts(count):
        if (count == 0):
            there_are_no_letters()
        elif (count == 1):
            there_is_one_letter()
        else:
            there_are_many_letters(count)

    def there_are_many_letters(count):
        number = Integer.toString(count)
        verb = "are"
        pluralModifier = "s"

    def there_is_one_letter():
        number = "1"
        verb = "is"
        pluralModifier = ""

    def there_are_no_letters():
        number = "no"
        verb = "are"
        pluralModifier = "s"
```

