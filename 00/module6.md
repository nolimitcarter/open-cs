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








