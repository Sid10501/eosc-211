---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.0
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Lab Week 2 Reading
EOSC 211 2022

## Python Basics


**Python** is a *high level programming language,* meaning it is comparatively easy for humans to read. Python programs are executed by a *python interpreter,* which takes python code, reads it into a processor (the CPU on your computer, or in our case, a Jupyterhub server) and returns a result. This process is repeated over and over for each line of code, often taking the result of one line and feeding it into the next. 

Python is also *open source*, meaning there are no fees to download/use python, and anyone is free to add to the Python code base. This is a major reason for Python's growing popularity in the scientific community, there are many add ons (called *packages*) developed by other scientists specifically for the type of programming we want to do in this course, with more being added every day!


### Values and Data Types 

| Data Type | Example | 
| --- | --- | 
| String | `'a', "AA",  '2', 'Mercury'` | 
| Integer | `-2, -1, 0, 1, 2, 5, 10` |
| Floating-point number | `1.0, -2.1, 3.1415` | 

#### Strings
Strings are a data-type that contain a sequence or 'string' of letters (although a single character such as `'s'` is still considered a string). Strings can easily be identified by eye as they are enclosed in a set of quotation marks. Strings in Python can be enclosed in single quotes (`''`), double quotes (`""`), or three of each (`'''` or `"""`). Strings enclosed in triple quotes can span multiple lines. 

#### Indexing Strings
Individual characters in a string can be accessed by their position in the string itself using ***indexing***. In Python, we start counting from zero, so the first letter is at position `0` in the string, the second letter at position `1`, the third at `2`, etc... In practice, this looks like the following example:

```{code-cell} ipython3
# make a long string: 
dept = 'Department of Earth, Ocean and Atmospheric Sciences'

print(dept[0])   # character in position 0(1st character)
print(dept[5])   # character in position 5 (6th character)
print(dept[-2])  # second to last character
print(dept[-1])  # last character
```

In addition to indexing, strings support **slicing**, which allows the user to extract a subset of the string between some start and stop indices. In slicing, the first index is always included, and the second index is always excluded.

```{code-cell} ipython3
print(dept[14:19])  # characters from position 14 (inclusive) to position 19 (exclusive)
```

There is also useful default behaviour if the first or last index is omitted:

```{code-cell} ipython3
print(dept[14:])  # omitting the last index slices: prints from 14th character (inclusive) to the end 
print(dept[:10])  # omitting first index slices: prints from first character (inclusive) to the tenth (exclusive)
```

**Note:** Indexing in *lists* and *tuples* follows all the same rules as for strings (see sections below for Lists and Tuples).


#### Numerical data types
The *integer* data type represents whole numbers (meaning they can be written without a fractional component) that can be positive, negative, or zero. The number `1` is an integer, while `1.0` is not because of the presence of the decimal point. 

The *Floating point* data type represents numbers which include a decimal point. 

If you are unsure of which data type a variable falls into, you can use the built-in function `type()` to check and the interpreter will relay back to you what data type the input is. For example:

```{code-cell} ipython3
type('Hello World!')
```

```{code-cell} ipython3
type(1)
```

```{code-cell} ipython3
type(3.1415)
```

### Type casting
Occasionally we want to convert between `int`, `float` and `str` data types. To do this, we use *type converter functions* `int()`, `float()` and `str()`. Like the `print()` and `type()` functions we've seen above, these are type converters are Python *built-in* functions that will come in useful when programming. 

The `int()` function converts the provided argument, either a floating point number or syntactically correct string into an integer data type.

```{code-cell} ipython3
int(1.6)
```

```{code-cell} ipython3
int('2022')
```

Both of the above cells return an `int` data type, the first converting from `float` to `int` and the second cell converting from `str` to `int`. For floating point numbers, the `int()` type converter function discards the decimal portion of the number.

Similarly, the `float()` type converter function converts it's argument, either an integer or syntactically correct string to a floating point data type. `float()` also accepts strings `nan` and `inf` with an optional prefix `-` or `+` for Not a Number (NaN) and positive or negative infinity.

```{code-cell} ipython3
float(1)
```

```{code-cell} ipython3
float('2.718')
```

The above cells return a `float` data type, the first converting from `int` to `float` and the second cell converting from `str` to `float`.

Both the `int` and `float` type converter functions will throw an error if attempting to convert a syntactically incorrect string to the respective integer or floating point data types. 

Finally, the `str()` type converter function converts its argument to a string data type:

```{code-cell} ipython3
str(1)
```

```{code-cell} ipython3
str(2.718)
```

### Math in Python

The Python core contains functionality for doing basic math. Later in the course, we will learn how to *import* further functionality for doing not-so-basic math. The syntax for math in Python is summarized below:

| Operator | Description | Example | Result |
| --- | --- | --- | --- |
| ``` + ``` | addition | ```2 + 3 ``` | ```5``` |
| ``` - ``` | subtraction | ```8 - 6 ``` | ```2``` |
| ``` - ``` | negative number | ```-4``` | ```-4``` |
| ``` * ``` | multiplication | ``` 5 * 2 ``` | ``` 10 ``` |
| ``` / ``` | division | ``` 6 / 3 ``` | ``` 2 ``` |
| ``` ** ```| raises a number to a power | ``` 10**2 ``` | ``` 100 ``` |
| ``` // ```| floor division: division returning the nearest integer | ``` 100//9 ``` | ```11``` |
| ``` %  ```| modulo: returns the remainder after division | ``` 100%9 ``` | ``` 1 ``` |

For more complex calculations involving several operators, the python interpreter will perform calculations in the order BEDMAS (brackets, exponents, division/multiplication, addition/subtraction), just like you would do by hand.

+++

### Math With Variables

Just as we can print **values** to the screen, we can assign and reference **variables** within a program. A variable is a *name* that refers to a *value* and is initiated through an **assignment statement**. For example, the circumference $C$ of a circle is given:

$$
C = 2\pi r
$$

where $r$ is the radius of the circle and $\pi = 3.14...$. We can code this equation in python by assigning the variable named `circumference` to a calculated value like so:

```{code-cell} ipython3
# code snippet to calculate the circumference of a spherical planet given some radius: 
radius_of_planet = 6371  # [km]
pi = 3.14 

# calculate the circumference of a sphere using the provided equation:
circumference = 2 * pi * radius_of_planet

# print the output to the screen:
print(circumference)

# print the output in a nicely formatted string: 
print(f'The planet has {circumference = :.2f} km')
```

This example makes three assignments. The first assigns the integer value `6371` to the variable named `radius_of_planet`. The second assigns the floating-point value of `3.14` to the variable `pi`,  and the third assigns the product of the multiplication to the variable `circumference`.


### Lists
Lists are a built-in compound *iterable* data type which are composed of an ordered collection of values. Values in a list are referred to as *items* or *elements*.  Lists can be written as a list of comma-separated values enclosed in square brackets or using the `list()` constructor function. Lists are ordered and mutable, meaning that they maintain the order of their elements, and that they are able to be changed after they are created. Lists can contain items of different data types (meaning any combination of numerical or string data types).

```{code-cell} ipython3
primes = [0, 1, 3, 5, 7, 11]  # a list of integers

the_date = ['Monday', 'June', 27, 2020]  # a list of strings and integers
```

#### List Indexing
Given that lists are *ordered*, we require methods of accessing elements in a list. Items or elements in a list can be accessed by their index (or 'position') in the list, as we saw for strings earlier.   

Say we want to access the fourth number in the list `primes` which was initialized in the section above. Remembering that indexing in Python starts as `0, 1, 2, 3...`, the *fourth* element in the `primes` list therefore has index `3` and can be accessed as:

```{code-cell} ipython3
fourth = primes[3]  # the fourth item in the primes list has index 3

print(f'The fourth item in primes is {fourth}.')
```

Like with strings, *slicing* allows us to extract elements from a list between start and stop positions. Slicing for lists (and tuples) follow the same rules as for strings. e.g.

```{code-cell} ipython3
# primes = [0, 1, 3, 5, 7, 11]  # a list of integers

print(primes[2:5])  # slice from index 2 (inclusive) to index 5 (exclusive)
print(primes[3:])  # slice from index 3 (inclusive) to the end 
print(primes[:3])  # slice from index 0 (inclusive) to 3 (exclusive)
```

#### List Methods
Lists are *mutable* meaning that they can be changed after being created. These changes are facilitated by several built-in list *methods* shown in the below table. 

| Method | Function |
| --- | --- | 
| .append() | Adds an element to the end of the list | 
| .clear()| Deletes the contents of the list | 
| .copy()| Returns a copy of the list|
| .count()| Returns a count of elements with an input value|
| .extend() | Adds elements of an iterable to a list |
| .index() | Returns the first index in the list matching an input value|
| .insert() | Inserts an element at a specified position|
| .pop() | Removes the element at the specified position |
| .remove() | Removes the first element with a specified value |
| .sort()| Sorts the list |
| .reverse() | Reverses the list in place |


Methods are accessed by using a dot-notation after the variable name like so:

```{code-cell} ipython3
primes = [0, 1, 3, 5, 7, 11]  # a list of integers
print('0.  primes: ', primes)
# 1. append the integer `15` to the end of the list
primes.append(15)
print('1.  primes after appending:', primes)

# 2. make a copy of the list: 
primes_cp = primes.copy()
print('2.  primes copy:', primes_cp)

# 3. reverse the copied list: 
primes_cp.reverse()
print('3.  after primes_cp.reverse():', primes_cp)


# 4. zero isn't a prime number so lets remove it from the list: 

# 4a. Remove from original `primes` list based on item *value*: 
#     - Use .remove() method: 
primes.remove(0)  # a. remove the first occurence of `0` from the list
print('4a. after primes.remove(0):', primes)

# 4b. Remove from reversed copy `primes_cp` based on item *index*:
#    - Use .pop() method: 
#    - Note that the zero in `primes_cp` occurs at the last position in the list. 
primes_cp.pop(-1)  # b. remove the last element from the list 
print('4b. after primes_cp.pop(-1):', primes_cp)
```

### Tuples
Tuples are another data structure which are used to group together collections of *items* or *elements*. Like lists, tuples are *ordered* meaning that the order of their elements does not change but unlike lists, tuples are *immutable* (meaning they are not able to be changed after they are created). Indexing for tuples follows all the same rules as strings and lists (detailed above).

As a result of tuples being immutable, there are only a couple built-in methods for tuples: 

| Method | Function 
| --- | --- | 
| .count()| Returns a count of elements with an input value|
| .index() | Returns the first index in the tuple matching an input value|

+++

Tuples are created by enclosing comma separated values in round parantheses or by using the `tuple()` constructor function.

```{code-cell} ipython3
squares = (2,4,9,16)  # a tuple with 4 elements
single = (1, )  # a tuple with 1 element (note the comma)

print(type(squares), type(single))
```

Tuples are immutable, meaning they cannot be changed after initialization: 

```python
>>> squares = (2,4,9,16)  # a tuple with 4 elements
>>> squares[3] = 0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment

```
