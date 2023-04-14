# Comments

Rules should be followed when writing the comments, and some cases which </br>
writing a comment will be good and other cases will be bad.

* Use of comments is to compensate for our failure to express ourself in
code.
* Inaccurate comments are worse than no comments at all.
* you need to write a comment, think it through and see whether there </br>
isn’t some way to express yourself in the code without using comments.

1. Explain yourself in Code rayher than using comments

```python
// check to see if the employee is eligible for bonus
if employee.hourly_flag and employee.age >65:
    ...
```

Rather create a function that speaks about the code
```python
if employee.is_eligible_for_bonus():
    ...
```

2. Good Comments 
Good comments do not excuse unclear code.

```python
n = get_best_employee() // store the best employee
for i in employee_bonus_list:
    if i == n: // check the best employee is in bonus list
        ...
    ...
```


```python
best_employee = get_best_employee()
for employee_name in employee_bonus_list:
    if employee_name == best_employee: 
        ...
    ...
```

3. can’t write a clear comment, there may be a problem with the code.

4. Provide links to the original source of copied code

/** Converts a Drawable to Bitmap. via https://stackoverflow.com/a/46018816/2219998. */

5. Use comments to mark incomplete implementations ot TODO

// TODO - depreciate pandas implementation of datetime
// we expect this to code to depreciate when we migrate to vanilla Python approach

```python
import pandas as pd

df = pd.DataFrame({'DOB': {0: '26/1/2016', 1: '26/1/2016'}})

```

6. Mandated Comments

required documentation in every function leads to ugly code

```python
* @param  url  an absolute URL giving the base location of the image
* @param  name the location of the image, relative to the url argument
* @return      the image at the specified URL
* @see         Image

```

7. Noise Comments : They provide no new information.

```python
# default constructor called when call initialized
def __init__():
    ....
```