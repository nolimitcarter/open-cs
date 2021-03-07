# Week 4 notes of HarvardX's Introduction to Computer Science course

Topic: Memory

## Hexadecimal 

* In module 2 we discussed memory and how each byte has an address, or identifier, so we can refer to where our data are actually stored.
* It turns out, by convention, the address for memory use for the counting system **hexadecimal**, or base-16, where there are 16 digits: 0-9, and A-F as equivalents to 10-15.
* Lets consider a two-digit hexadecimal number: 
```
16^1 16^0
   0    A
```
  * Here, the A in the ones place (since 16^0 = 1) has a decimal value of 10. We can keep counting until `0F`, which is equivalent to 15 in decimal. 
* After `0F`, we need to carry the one, as we would go from 09 to 10 in decimal: 
```
16^1 16^0
   1    0
```
  * Here, the `1` value has a value of 16^1 * 1 = 16, so `10` in hexadecimal is 16 decimal. 
* With two digits, we can have a maximum value of `FF`, or 16^1 * 15 + 16^0 * 15 = 255, which is the same maximum value with 8 bits binary. So two digits in hexadecimal can conveniently represent the value of a byte in binary. (Each digit in hexadecimal, with 16 values, maps to four bits in binary.)
* In writing, we indicate a value is hexadecimal bu prefixing it with `0x`, as in `0x10`, where the value is equal to 16 in decimal, as opposed to 10. 
* Our computer's memory also uses hexadecimal for each address or location.

## Addresses 

* We might create a value `n`, and print it out: 

```
  #include <stdio.h>

  int main(void)
  {
    int n = 50;
    printf("%i\n", n);
  }
```

* In our computer's memory, there are now 4 bytes somewhere that have the binary value of 50, labeled `n`
* It turns out that with the billions of byte in memory, those bytes for the variable `n` starts at some location, which might look something like `0x12345678`. 
* In C, we can actually see the address with the `&` operator, which means "get the address of this variable": 

```
  #include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n);
}
```

* `%p` is the format code for an address.
* The `*` operator, or the dereference operator, lets us "go to" the location that a pointer is pointing to.
* For example, we can print `*&n`, where we "go to" the address of `n`, and that will print out the value of `n`, `50`, since that's the value of the address of `n`: 

```
  #include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%i\n", *&n);
}
```

## Pointers

* A variable that stores an address is called a **pointer**, which we can think of as a value that "points" to a location in memory. In C, pointers can refer to specific types of values. 
* We can use the `*` operator (in an unfortunately confusing way) to declare a variable that we want to be a pointer: 
```
#include <stdio.h>

int main(void)
{
  int n = 50;
  int *p = &n;
  printf("%p\n", p);
}
```
  * Here, we use `int *p` to declare a variable, `p`, that has a type of `*`, a pointer, to a value of type `int`, an integer. Then, we can print its value (an address, something like 0x12345678), or print the *value* at its location with `printf("%i\n", *p);`.
  * Since `p` is a variable itself, it's somewhere in memory, and the value stored there is the address of `n`
  * Modern computer systems are "64-bit", meaning that they use 64 bits to address memory, so a pointer will in reality be 8 bytes, twice as big as an integer of 4 bytes.
* In the real world, we might have a mailbox labeled "p", among many mailboxes with addresses. Inside our mailbox, we can put a value like `0x123`, which is the address of some other mailbox `n`, with the address `0x123`.

## Strings 

* A variable declared with `string s = "HI!";` will be stored one character at a time in memory. And we can access each character with `s[0]`, s[1], s[2], and s[3]: 
```
H    I    !    \0
s[0] s[1] s[2] s[3]
```
  * But it turns out that each character, since it's stored in memory, also has some unique addresses, and 1s is actually just a pointer with the address of the first character: 
  ```
  H     I     !     \0
  0x123 0x124 0x125 0x126
  ```
  * And the variable `s` stores the address of the first character of the string : `s = 0x123`. The value `\0` is the only indicator of the end of the string.
* Since the rest of the characters are in an array, back-to-back, we can start at the address in `s` and continue reading one character at a time from memory until we reach `\0`
* Example: 
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
  string s = "HI!";
  printf("%s\n", s);
}
```

## Pointer Arithmetic 

* **Pointer arithmetic** is mathematical operations on addresses with pointers. 
* We could print out each character in a string by using `char *` directly:
  ```
  #include <stdio.h>

  int main(void)
  {
    char *s = "HI!";
    printf("%c\n", *s);
    printf("%c\n", *(s+1));
    printf("%C\n", *(s+2));
  }
  ```
  * `*s` goes to the address stored in `s`, and `*(s+1)` goes to the location in memory with an address one byte or higher, or the next character. `s[1]` is syntactic sugar for `*(s+1)`, equivalent in function but more human-friendly to read and write.
* We can even try to go to addresses in memory that we shouldn't, like with `*(s+10000)`, and we run our program, we'll get a segmentation fault, or crash as a result of our program touching memory in a segment it shouldn't have. 


## Compare and Copy

* Lets compare to integers from the user: 

```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int i = get_int("i: ");
    int j = get_int("j: ");

    if (i == j)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```
  * We compile and run our program, and it works as we'd expect, with the same values of the two integers giving us "same" and "different" values.
* When we try to compare two strings, we see that the same inputs are causing our program to print "different": 
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    char *s = get_string("s: ");
    char *t = get_string("t: ");

    if (s == t)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```
  * Even when our inputs are the same, we see "different" printed. 
  * Each "string" is a pointer, `char *`, to a different location in memory, where the first character of each string is stored. So even if the characters in the string are the same, this will always print "different". 

* For example, our first string might be at address 0x123, our second might be at 0x456, and `s` will have the value of `0x123` pointing at that location, and `t` will have the value of `0x456`, pointing at another location. 
```
            s                 ||              t
  H       I       !     \0    ||      H     I     !    \0
0x123 | 0x124 | 0x25 | 0x126  ||  0x456 0x457 0x498 0x459
```
  * And `get_string`, this whole time, has been returning just a `char *`, or a pointer to the first character of a string from the user. Since we called `get_string` twice, we got two different pointers back.


## Valgrind

**valgrind** is a command-line tool that we can use to run our program and see if it has any **memory leaks**, or memory we've allocated without freeing, which might eventually cause our computer to run out of memory. 

## Garbage values

* Take a look at the following: 

```
int main(void)
{
  int *x;
  int *y;

  x = malloc(sizeof(int));

  *x = 42;
  *y = 13;

  y = x;

  *y = 13;
}
```

* We declare two pointers to integers, `x` and `y`, but don't assign them values. We use `malloc` to allocate enough memory for an integer with `sizeof(int)`, and store it in `x`. `*x = 42` goes to the address `x` points to, and sets the location in memory to the value of 42.
* We can print out garbage values, by declaring an array but not setting any of its values: 

```
  #include <stdio.h>

int main(void)
{
    int scores[3];
    for (int i = 0; i < 3; i++)
    {
        printf("%i\n", scores[i]);
    }
}
```

* When we compile and run this program, we see various values printed. 

## Swap

  * Let's try to swap the values of two integers: 
  
  ```
  #include <stdio.h>

void swap(int a, int b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(x, y);
    printf("x is %i, y is %i\n", x, y);
}

void swap(int a, int b)
{
    int tmp = a;
    a = b;
    b = tmp;
}
  ```
  
  * In the real world, if we had a red liquid in one glass, and a blue liquid in another, and we wanted to swap them, we would need a third glass to temporarily hold one of the liquids, perhaps the red glass. Then we can pour the blue liquid into the first glass, and finally the red liquid from the temporary glass into the second one. 
  * In our `swap` function, we have a third variable to use as temporary storage space as well. We put `a` into `tmp`, and then set `a` to the value of `b`, and finally `b` can be changed to the original value of `a`, now in `tmp`.
* If we tried to use that function in a program, we don't see any changes. It turns out that the `swap` function gets its own variables, `a` and `b` when they are passed in, that are copies of `x` and `y`, and so changing those values doesn't change `x` and `y` in the `main` function.

## Memory layout 

* Within out computer's memory, the different types of data that need to be stored for our program are organized into different sections:

Machine Code |
:-- |
Globals 
Heap(top) & Stack(bot)

  * The **machine code** section is our compiled program's binary code. When we run our program, that code is loaded into the "top" of memory. 
  * Just below, or in the next part of memory, are **global variables** we declare in our program. 
  * The **heap** section is an empty area from where `malloc` can get free memory for our program to use. As well call `malloc`, we start allocating memory from the top down. 
  * The **stack** section is used by functions in our program as they are called, and grows upwards. For example, our `main` function is at the very bottom of the stack and has the local variables `x` and `y`. The `swap` function, when it's called, has its own area of memory that's on top of `main`', with the local variables `a`,`b`, and `tmp`.
* Once the function `swap` returns, the memory it was using is freed for the next function call. `x` and `y` are arguments, so they're copied as `a` and `b` for `swap`, so we don't see our changes back in `main`.

## Graphics

* We can read binary and map them to pixels and colors, to display images and videos. With a finite number of bits in an images files, though, we can only zoom in so far before we start seeing individual pixels. 
  * With artificial intelligence and machine learning, however, we can use algorithms that can generate additional details that weren't there before, by guessing based on other data. 

* This program will open a file and tell us if it's a JPEG file: 
```
#include <stdint.h>
#include <stdio.h>

typedef uint8_t BYTE;

int main(int argc, char *argv[])
{
    // Check usage
    if (argc != 2)
    {
        return 1;
    }

    // Open file
    FILE *file = fopen(argv[1], "r");
    if (!file)
    {
        return 1;
    }

    // Read first three bytes
    BYTE bytes[3];
    fread(bytes, sizeof(BYTE), 3, file);

    // Check first three bytes
    if (bytes[0] == 0xff && bytes[1] == 0xd8 && bytes[2] == 0xff)
    {
        printf("Maybe\n");
    }
    else
    {
        printf("No\n");
    }

    // Close file
    fclose(file);
}
```
  * First we define a `byte` as 8 bits, so we can refer to a byte as a type more easily C.
  * Then, we try to open a file (checking that we indeed get a non-NULL file back), and read the first three bytes from the file with `fread`, into a buffer called `bytes`.
  * We can compare the first three bytes (in hexadecimal) to the three bytes required to begin a JPEG file. If they're the same, then our file is likely to be a JPEG file (though, other types of files may still begin with those bytes.) But if they're not the same, we know it's definitely not a JPEG file. 

























