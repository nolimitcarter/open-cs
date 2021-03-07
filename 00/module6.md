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


  





