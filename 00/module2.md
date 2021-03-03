# Week 3 notes of HarvardX's Introduction to Computer Science course

# Topic: Arrays

## Compiling 

* Compiling source code into machine code is actually made up of smaller steps: 
  * preprocessing
  * compiling
  * assembling
  * linking
* Preprocessing generally involves lines that start with a #, like #include. For example, `#include <cs50.h>` will tell us `clang` to look for that header file, since it contains content that we want to include in our program. Then, `clang` will essentially replace the contents of those header files into our program. 
  * For example... 
  ```
  #include <cs50.h>
#include <stdio.h>

int main(void)
{
    string name = get_string("What's your name? ");
    printf("hello, %s\n", name);
}
  ```
* ...will be preprocessed into: 
```
...
string get_string(string prompt);
int printf(string format, ...);
...

int main(void)
{
    string name = get_string("Name: ");
    printf("hello, %s\n", name);
}
```
* This includes the prototypes of all the functions we included, so we can then use them in our code. 
* Compiling takes our source code, in C, and converts it to another type of source code called assembly code, which looks like this: 
```
...
main:                    # @main
    .cfi_startproc
# BB#0:
    pushq    %rbp
.Ltmp0:
    .cfi_def_cfa_offset 16
.Ltmp1:
    .cfi_offset %rbp, -16
    movq    %rsp, %rbp
.Ltmp2:
    .cfi_def_cfa_register %rbp
    subq    $16, %rsp
    xorl    %eax, %eax
    movl    %eax, %edi
    movabsq    $.L.str, %rsi
    movb    $0, %al
    callq    get_string
    movabsq    $.L.str.1, %rdi
    movq    %rax, -8(%rbp)
    movq    -8(%rbp), %rsi
    movb    $0, %al
    callq    printf
    ...
```
  * These instructions are lower-level and is closer to the binary instructions that a computer's processor can directly understand. They generally operate on bytes themselves, as opposed to abstractions like variable names. 
* The next step is to take the assembly code and translate it to instructions in binary by assembling it. The instructions in binary are called machine code, which a computer's CPU can run directly. 
* The last step is *linking*, where previously compiled versions of libraries that we included earlier, like `cs50.c`, are actually combined with the binary of our program. So we end up with one binary file, `a.out` or `hello`, that is the combined machine code for `hello.c`, `cs50.c`, and `stdio.c` (All cs, being in the course IDE of course.)

## Debugging 

* We can use the `printf` function, to print messages and variables to help us debug. 
* Let's take a look at this code: 
```
#include <stdio.h>
int main(void)
{
    // Print 10 hashes
    for (int i = 0; i <= 10; i++)
    {
        printf("#\n");
    }
}
```

* Hmm... We want to print only 10 `#`s, but there are 11. If we didn't know what the problem is (since our program is compiling without any errors, and we now have a logical error), we could add another `printf` temporarily: 
```
#include <stdio.h>
int main(void)
{
    for (int i = 0; i <= 10; i++)
    {
        printf("i is now %i\n", i);
        printf("#\n");
    }
}
```
* Now, we can see that `i` started at 0 and continued to 10, but we should have our `for` loop stop once it's at 10, with `i < 10` instead of `i < 10`. 

## Memory 

* In C, we have different types of variables we can use for storing data, and each of them take up a fixed amount of space. Different computer systems actually vary in the amount of space actually used for each type, but we'll work with the amounts here, used in their IDE: 
  * `bool 1 byte`
  * `char 1 byte`
  * `double 8 bytes`
  * `float 4 bytes`
  * `int 4 bytes`
  * `long 8 bytes`
  * `string ? bytes`
  * etc...
* In C, when we create a variable of type `char`, which will be sized one byte, it will physically be stored in one of those boxes in RAM. An integer, with 4 bytes, will take up four of those boxes. 

## Arrays 
  * Let's say we wanted to take the average of three variables: 
  ```
  #include <stdio.h>

int main(void)
{
    int score1 = 72;
    int score2 = 73;
    int score3 = 33;

    printf("Average: %f\n", (score1 + score2 + score3) / 3.0);
}
  ```
  * We divide by not `3`, but `3.0` so the result is also a float.
  * We can compile and run our program, and see an average printed. 
* While our program is running, the three `int` variables are stored in memory.
  * For example, if each `int` takes up four boxes, representing four bytes, and each byte in turn is made up of eight bits, 0s and 1s stored by electrical components. 
* It turns out, in memory, we can store variables one after another, back-to-back, and access them more easily with loops. In C, a list of values stored one after another contiguously is called an *array*. 
* For our program above, we can use `int scores[3];` to declare an array of three integers instead. 
8 We can also assign and use variables in an array with `scores[0] = 72`. With the brackets, we're indexing into, or going to, the "0th" position in the array. Arrays are always zero-indexed.
* Let's update our program to use an array: 
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int scores[3];
    scores[0] = get_int("Score: ");
    scores[1] = get_int("Score: ");
    scores[2] = get_int("Score: ");

    // Print average
    printf("Average: %f\n", (scores[0] + scores[1] + scores[2]) / 3.0);
}
```
  * Now, we're asking the user for three values, and printing the average as before, but using the values stored in the array. 
* Since we can set and access items in an array based on their position, and that position can also be the value of some variable, we can used a loop: 
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int scores[3];
    for (int i = 0; i < 3; i++)
    {
      scores[i] = get_int("Score: ");
    }

    // Print average
    printf("Average: %f\n", (scores[0] + scores[1] + scores[2]) / 3.0);
}
```
  * Now, instead of hard-coding, or manually specifying each element three times, we use a `for` loop and `i` as the index of each element in the array. 






















