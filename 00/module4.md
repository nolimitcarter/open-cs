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














