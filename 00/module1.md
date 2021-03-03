# Week 2 notes of HarvardX's Introduction to Computer Science course

# Topic: C

## C

* We'll be dealing with C this lesson, take this hello world program for example: 

```
#include <stdio.h>
int main (void)
{
  printf("hello world!");
}
```

## Compiling 

* Compiling - Converting our human readable code to machine code or binary(1's and 0's) that our computer can understand.
* A program called a compiler will take source code as input and produce machine code as output. 

## Functions and Arguments

* Functions are small actions or verbs that we can use in our program to do something, and the inputs to functions are called arguments. 
  * For example, in C, we used the main function to print something to the screen with `printf` (with the f standing for formatted text - didn't know). In C, we pass arguments within parentheses as in `printf("hello world!");`. The double quotes indicate that we cant to print out the letters `hello world!`. 
* Functions can also have two kinds of outputs: 
  * side effects, such as something printed to the screen,
  * and return values, a value that is passed back to our program that we can use or store of later. 

# main, header files

* Header files that end with .h refer to some other set of code, like a library, that we can then use in our program. We include them with lines like `#include <stdio.h>`, for example, for the standard input/output library, which contains the `printf` function.

## Types, format codes,

* There are many data types we can use for our variables, which indicate to the computer what type of data they represent: 
  * `bool`, a boolean expression of either `true` or `false`
  * `char`, a single ASCII character like `a` or `2`
  * `double`, a floating-point value with more digits than a `float`
  * `float`, a floating-pint value, or real number with a decimal value
  * `int`, integers up to a certain size, or # of bits. 
  * `long`, integers with more bits, so they can count higher than an `int`
  * `string`, a string of characters
* For `printf`, too, there are different placeholders for each type: 
  * `%c` for chars
  * `%f` for floats, doubles
  * `%i` for ints
  * `%li` for longs
  * `%s` for strings

## Operators, limitations, truncation 

* Math operators
  * `+`
  * `-`
  * `*`
  * `/`
  * `%` for remainder

## Variables, syntactic sugar

* Variables allow you to assign a value to something. In C, we would write `int counter = 0`
* we can increase the variable with `counter = counter + 1;`, but C also supports syntactic sugar, which would allow us to just write `counter += 1;`. We could even also just write `counter++`, to learn more read C documentation. 

## Conditions 

* We can translate conditions, or "if" blocks, with: 
```
if (x < y)
{
  printf("x is less than y\n");
}
```
  * Notice that in C, we use `{` and `}`, as well as indentation to indicate how lines of code should be nested. 
* We can have "if" and "else" conditions: 
```
if (x < y)
{
  printf("x is greater than y\n");
}
else 
{
  printf("x is not less than y\n");
}
```

## Boolean expressions and Loops

* A forever block in C would be: 
```
while (true)
{
printf("hello world!");
}
```
  * The `while` keyword requires a condition, so we use `true` as the Boolean expression to ensure that our loop will run forever. `while` will tell the computer to check whether the expression evaluates to `true`, and then run the lines inside the curly braces. Then it will repeat that until the expression isn't true anymore. In this case, `true` will always be true, so our loop is an infinite loop. 
* Obviously, we can also do something a certain amount of times with `while`: 
```
int i = 0; * Even though we could start with 1, by convention we should start at 0
while (i < 50)
{
  printf("hello world!\n");
  i++;
}
```

* Finally, more commonly, we can use the `for` keyword: 
```
for (int i = 0; i < 50; i++)
{
  printf("hello, world\n");
}
```
  * First, we create a variable named `i` and set it to 0. Then, we check that `i < 50` every time we reach the top of the loop, before we run any of the code inside. If that expression is true, then we run the code inside. Finally, after we run the code inside, we use `i++` to add one to `i`, and the loop repeats. 
  * The `for` loop makes this example much less complex

* Two different code examples that ultimately get the same result: 

    ```
  #include <stdio.h>
  int main(void)
  {
    for (int i = 0; i < 3; i++)
    {
        printf("meow\n");
    } 
  }
    ```
* We can move the `printf` line to its own function, like so:

  ```
  #include <stdio.h>

  void meow(void) {
  printf("meow\n");
  }
  int main(void)
  {
    for (int i = 0; i < 3; i++)
    {
       meow();
    }
  }
  ```
  * We defined a function, `meow`, above our `main` function.
* Conventionally, our `main` function should be the first function in our program, so we need a few more lines: 
```
#include <stdio.h>
void meow(void);
int main(void)
{
  for (int i = 0; i < 3; i++)
  {
      meow();
  }
}

void meow(void)
{
  printf("meow\n");
}
```
  * In this example, we declared our `meow` function first with a *prototype*, before we used it in `main`, and actually define it after. The compiler reads our source code from top to bottom, so it needs to know that `meow` will exist later in the file. 
* We can even change our `meow` function to take in some input, `n`, and meow `n` times: 
```
#include <stdio.h>
void meow(int n);
int main(void)
{
  meow(3);
}

void meow(int n)
{
  for (int i = 0; i < n; i++)
  {
      printf("meow\n");
  }
}
```
  * The `void` before the `meow` function means that it doesn't return a value, and likewise in `main` we can't do anything with the result of `meow`, so we just call it. 
* The abstraction here leads to better design, since we now have the flexibility to reuse our `meow` function in multiple places in the future.
* Here is another example of abstraction, `get_positive_int.c`: 
```
#include <cs50.h>
#include <stdio.h>
int get_positive_int(void);
int main(void)
{
  int i = get_positive_int();
  printf("%i\n", i);
}
// Prompt user for positive integer
int get_positive_int(void)
{
  int n;
  do
  {
      n = get_int("Positive Integer: ");
  }
  while (n < 1);
  return n;
}
```
  * We have our own function that calls `get_int` repeatedly until we have some integer that's not less than 1. With a do-while loop, our program will do something first, then check some condition, and repeat while the condition is true. A while loop, on the other hand, will check the condition first. 
  * We need to declare our integer `n` outside the d-while loop, since we need to use it after the loop ends. The scope of a variable in C refers to the context, or lines of code, within which it exists. In many cases, this will be the curly braces surrounding the variable. 
  * Notice that the function `get_positive_int` now starts with `int`, indicating that it has a return value of type `int` and in `main` we indeed store it in `i` after calling `get_positive_int()`. In `get_positive_int`, we have a new keyword, `return` to return the value `n` to wherever the function was called.

## Glossary


