# Week 5 notes of HarvardX's Introduction to Computer Science course

Topic: Python 

## Python Basics

* We can write a loop with a variable: 

```
i = 0
while i < 3: 
  print("hello, world")
  i += 1
```

* We can also use a `for` loop, where we can do something for each value in a list: 

```
for i in [0]
  print("cough")
```

  * Lists in Python [0, 1, 2], are like arrays in C. 

* While C is a **strongly typed** language, where we need to specify types, Python is **loosely typed**, where the type is implied by the values.
* Built in data types: 
  * `bool`
  * `float`
  * `int`
  * `str`
* Other types in Python: 
  * `range`, sequence of numbers
  * `list`, sequence of mutable values, or values we can change
  * `tuple`, collection of ordered values like x- and y-coordinates, or longitude and latitude 
  * `dict`, dictionaries, collection of key/value pairs, like a hash table
  * `set`, collection of unique values, or values without duplicates

## Input, Conditions

* We can get input from the user with the `input` function: 
```
answer = input("What's your name? ")
print(f"hello, {answer}")
```

* **cast** = convert

## Improving Meow Program

Basic example; we don't even need a `main` function:

```
print("meow")
print("meow")
print("meow")
```

* We can define a function that we can reuse: 

```
for i in range(3):
    meow()

def meow():
    print("meow")
```
  * But this causes an error when we try to run it: `NameError: name 'meow' is not defined.` We need to define our function before we use it, so we can either move our definition of `meow` to the top, or define a main function first: 

  ```
  def main():
    for i in range(3):
        meow()

def meow():
    print("meow")

main()
  ```

  * Now, by the time we actually call our `main` function, the `meow` function will already have been defined.
* Our functions can take inputs too: 
  ```
  def main():
    meow(3)

def meow(n):
    for i in range(n):
        print("meow")

main()
  ```

  * (takes in parameter `n`, and passes it to `range`)

## Mario 

  * We can print out a row of question marks on the screen: 
  
  ```
  for i in range(4):
    print("?", end="")
  print()
  ``` 
  
  * Here, we don't want the automatic new line, so we can pass a **named argument**, also known as a keyword argument, to the `print` function, which specifies the value for a specific parameter. 
    * **Positional arguments**, are where parameters are set based on their position in the function call. 
  * We also say `end=""` to specify that nothing should be printed at the end of our string. `end` is also an **optional argument**, one we don't need to pass in, with a default value of `\n`, which is why `print` usually adds a new line for us.
* We are also able to multiply strings to get the same effect: `print("?" * 4)`.

* We can also implement nested loops:
  
  ```
  for i in range(3):
    for j in range(3):
      print("#", end="")
    print()
  ```

## Overflow, imprecision 

  * In Python, trying to cause an integer overflow actually won't work: 
  
  ```
  i = 1
  while True:
    print(i)
    i *= 2
  ```

  * Once run, we see larger and larger #s being printed. Python automatically uses more and more memory to store numbers for us inline C, where integers are fixed to a certain number of bytes. 
* Floating-point imprecision, too, still exists, but can be prevented by libraries that can represent decimal values with as many bites as a re needed. 

## Lists, Strings

* We can make a list: 

```
scores = [72, 73, 33]

print("Average: " + str(sum(scores) / len(scores)))
```
  * We can use `sum`, a function built into Python, to add up the values in our list, and divide it by the number of scores, using the `len` function to get the length of the list. Then, we cast the float to a string before we can concatenate and print it. 
  * We can even add the entire express into a formatted string for the same effect: 
  `print(f"Average: {sum(scores) / len(scores)}")`

## Algorithms

* We can implement linear search by just checking each element in a list:
  
  ```
  import sys

  numbers = [4, 6, 8, 2, 7, 5, 0]

  if 0 in numbers: 
    print("Found")
    sys.exit(0)
  
  print("Not Found")
  sys.exit(1)
  ```

  * With `if 0 in numbers:`, we're asking Python to check the list for us.
* A list of strings, too, can be searched with: 

```
names = ["Bill", "Charlie", "Fred", "Joe", "Ron"]

if "Ron" in names:
  print("Found")
else: 
  print("Not found")
```

* If we have a dictionary, a set of key-value pairs, we can also check for a particular key, and look at the value stored for it.
* Swapping two variables can also be done simply by assigning both values at the same time: 

```
x = 1
y = 2

print(f"x is {x}, y is {y}")
x, y = y, x
print(f"x is {x}, y is {y}")
```

  * In Python, we don't have access to pointers, which protects us from making mistakes with memory.

## Files 

* Opening a CSV file:

```
import csv

from cs50 import get_string

file = open("phonebook.csv", "a")

name = get_string("Name: ")
number = get_string("Number: ")

writer = csv.writer(file)
writer.writerow([name, number])

file.close()
```

  * It turns out that Python also has a `csv` library that helps us work with CSV files, so after we open the file for appending, we can call `csv.writer` to create a `writer` from the file, which gives additional functionality, like `writer.writerow` to write a list as a row.
* We can use the `with` keyword, which will close the file for us after we're finished: 

```
...
with open("phonebook.csv", "a") as file:
    writer = csv.writer(file)
    writer.writerow((name, number))
```

* We can open another CSV file, tallying the number of times a value appears: 

```
import csv

houses = {
    "Gryffindor": 0,
    "Hufflepuff": 0,
    "Ravenclaw": 0,
    "Slytherin": 0
}

with open("Sorting Hat (Responses) - Form Responses 1.csv", "r") as file:
    reader = csv.reader(file)
    next(reader)
    for row in reader:
        house = row[1]
        houses[house] += 1

for house in houses:
    print(f"{house}: {houses[house]}")
```

  * We use the `reader` function from the `csv` library, skip the header row with `next(reader)`, and then iterate over each of the rest of the rows. 
  * The second item in each row, `row[1]`, is the string of a house, so we can use that to access the value stored in `houses` for that key, and add one to it. 
  * Finally, we'll print out the count for each house.









































