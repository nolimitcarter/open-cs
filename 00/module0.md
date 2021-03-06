# Week 1 notes of HarvardX's Introduction to Computer Science course

Topic: Basics & Scratch

## Representing Numbers 

* We might start with the task of taking attendance by counting the number of people in a room. With our right hand, we might raise one finger at a time to represent each person, but we won't be able to count very high. This system is called *unary*, where each digit represents a single value of one. 

* Take three light bulbs for instance, we can turn the on in different patters, and count from 0(all 3 off) to 7(all 3 on). Like so: (none, right, middle, left, right 2, left and right, left 2, all on) 

* Inside modern computers, there are not light bulbs but millions of tiny switches called transistors that can be turned on and off to represent different values. 

* For example, we know the following number in decimal represents one hundred and twenty-three. 
  `1 2 3`
    * The `3` is in the ones column, the `2` is in the tens column, and the `1` is in the hundreds column. 
    * So 123 is 100*1 + 12*2 + 1*3 = 100 + 20 + 3 = 123
    * Each place for a digit represents a power of ten, since there are ten possible digits for each place. The rightmost place is for 10^0, the middle one 10^1, and the leftmost place 10^2. 
    ```
    10^2 10^1 10^0 | 
     1    2    3
    ```
* `$ = #`
* In binary, with just two digits, we have the powers of two for each place value. 
  
  2^2 2^1 2^0 | 
   $   $   $
  * This is equivalent to: 
  
  4 2 1 |  
  $ $ $
* With all the light bulbs or switches off, we would still have a value of 0: 
  
  4 2 1 |
  0 0 0
* Now if we charge the binary value to, say, `0 1 1`, the decimal value would be 3, since we add the 2 and the 1: 
  
  4 2 1 |
  0 1 1
* If we had several more light bulbs, we might have a binary value of `110010`, which would have the equivalent decimal value of `50`: 
  
  32 16  8  4  2  1 |
   1  1  0  0  1  0
  * Notice that `32 + 16 + 2 = 50`. 

## Text

(asciichart.com)

* To represent letters, all we need to do is decide how numbers map to letters. Some humans, many years ago, collectively decided on a standard mapping of numbers to letters. The letter "A", for example, is the number 65, and "B" is 66, and so on. By using context, like whether we're looking at a spreadsheet or an email, different programs can interpret and display the same bits as numbers of text. 

* The standard mapping, ASCII, the American Standard Code for Information Interchange, also included lowercase letters and punctuation. 

* If we received a text message with a patter of bits that had the decimal values `72`, `73`, and `33` those bits would map to the letters HI! Each letter is typically represented with a pattern of eight bits, or a *byte*, so the so the sequence of bits we would receive are `01001000`, and `01001001`, and `00100001`. 
  * We might already be familiar with using bytes as a unit of measurement for data, as in megabytes or gigabytes, for millions or billions of bytes. 
* With eight bits, or one byte, we can have 2^8 or 256 different values (including 0). (The highest value we can count up to would be 255.)
* Other characters, such as letters with accent marks and symbols in other languages are part of a standard called `Unicode`. 
  * When we receive an emoji, our computer is actually just receiving a number in binary that it then maps to the image of the emoji based on the Unicode standard. 
    * For example, the "face with tears of joy/ laughing face" emoji is just the bits `000000011111011000000010`

## Images, Video, and Sounds

* An image, like the picture of the emoji, are made up of colors. 
* With only bits, we can map numbers to colors as well. There are many different systems to represent colors, but a common one is RGB, which represents different colors by indicating the amount of red, free, and blue within each colors. 
* For example, our patter of bits earlier, `72`, `73`, and `33` might indicate the amount of red, green, and blue in a color. (And our program would know those bits map to a color if we opened an image file, as opposed to receiving them in a text message.)
  * Each number might be a byte, with 256 possible values, so with three bytes, we can represent millions of colors. Our three bytes from above would represent a dark shade of yellow. 
* The dots or square, on our screen are called `pixels`, and our images are made up of many thousands or millions of pixels as well. So by using three bytes to represent the color for each pixel, we can create images. We can see pixels in most images  if we were to zoom in.
* The resolution of an image is the number of pixels there are, horizontally and vertically, so a high-resolution image will have more pixels and require more bytes to be stored. 
* Videos are made up of many images, changing multiple times a second to give us the appearance of motion, as an old fashioned flip-book might do.
* Music can be represented with bits too, with mappings of numbers to notes and durations, or more complex mappings of bits to sound frequencies at each moment in time. 
* File formats like JPEG and PNG, or Word or Excel documents, are also based on some standard for representing information with bits. 

## Algorithms

* Humans can follow algorithms too, such as recipes for cooking. When programming a computer, we need to be more precise with our instructions aren't ambiguous or misinterpreted. 
* We might have an application on our phones that store our contacts, with their names and phone numbers sorted alphabetically. The old-school equivalent might be a phone book, a printed copy of names and phone numbers. 
* Our input to the problem of finding someone's number would be the phone book and a name to look for. We might open the book and start from the first page, looking for a name one page at a time. This algorithm would be correct, since we will eventually find the name if it's in the book. 
* We might flip through the book two pages at a time, but this algorithm will not be correct since we might skip the page with our name on it. We can fix this bug, or mistake, by going back one page at a time. This algorithm would be correct, since we eventually find the name if it's in the book. 
* Another algorithm would be opening the phone book to the middle, decide whether our name will be in the left half or the right half of the book(because it is alphabetized), and reduce the size of our problem by half. We can repeat thus until we find our name, dividing the problem in half each time. With 1024 pages to start, we would only need 10 steps of dividing 

## Pseudocode 

* We can write pseudocode, which is a representation of our algorithm in precise English. 
* Example: 
```
1  Pick up phone book
2  Open to middle of phone book 
3  Look at page
4  If person is on page
5    Call person
6  Else if person is earlier in book
7    Open to middle of left half of book
8    Go back to line 3
9  Else if person is later in book
10   Open to middle of right half of book
11   Go back to line 3
12 Else
13   Quit
```
* Within our pseudocode, we can pick out lines that start with verbs or actions which are called functions. 
  * Examples: Pick up, Open to, Look at, Call, Open to, Open to, Quit
* We also have branches that lead to different paths, like forks in the road, which are called conditions.
  * Examples: If, Else if, Else if, Else
* And the questions that decide where we go are called boolean expressions, which eventually result in a value of yes or no, or true or false.
  * Examples: Person is on page, Person is earlier in book, Person is later in book
* Lastly, we have words that create cycles, where can can repeat parts of our program called loops.
  * Examples: Go back to line 3

  ## NOT COVERING SCRATCH ;)

## Vocab Index

* `Unary` - a system where each digit represents a single value of one.
* `Decimal or Base 10` - There are ten different values that a digit can represent.
* `Binary or Base 2` - Base two. Only two possible digits, 0 and 1. Each binary digit is also called a bit. 
* `Byte` - eight bits (with eight bits or one byte, we can have 2^8, or 256 different values).
* `ASCII` - American Standard Code for Information Interchange.
* `Unicode` - Characters such as letters with accent marks and symbols in other languages are part of "this standard"(Unicode) that uses more bits than ASCII to accommodate all the letters/symbols. 



