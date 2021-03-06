# Week 3 notes of HarvardX's Introduction to Computer Science course

# Topic: Algorithms 

## Big *O*, Big *O* notation, and running times 

* **Running times**: how long an algorithm takes to run given some size of input. 
  * Common examples of running times: 
  * *O*(n^2)
  * *O*(nlogn)
  * *O*(n)
    * (searching one page at a time, in order)
  * *O*(logn)
    * (dividing the phone book in half each time)
  * *O*(1)
    * An algorithm that takes a constant number of steps, regardless of how big the problem is

## Linear search, binary search 

* If we want to look for the number zero, for example, we would have to open one door at a time, and if we didn't know anything about the numbers behind the doors, the simplest algorithm would be going from left to right. 
  * So, we might write pseudocode for a `linear search` with: 
  ```
  For i from 0 to n-1
    If number behind i'th door
      Return true
  Return false
  ```
    * We would label each of `n` doors from `0` to `n-1`, and check each of them in order.
    * "Return False" is outside the for loop, since we only want to do that after we've looked bind all the doors. 
    * The big O running time for the algorithm would be O(n), and the lower bound, Big Omega, would be Omega(1). 
  * If we know that the numbers behind the doors are sorted, then we can start in the middle, and find our value more efficiently. 
    * For a `binary search` our algorithm might look like: 
    ```
    If no doors
      Return false
    If number behind middle door
      Return true
    Else if number < middle door
      Search left half
    Else if number > middle door
      Search right half
    ```
  * The upper bound for binary search is O(logn), and the lower bound is also Omega(1), if the number we're looking for is in the middle, where we happen to start.
* With 64 light bulbs, we notice that linear search takes much longer than binary search, which only takes a few steps. 

## Sorting

  * If our input is an unsorted list of numbers, there are many algorithms we could use to produce an output of a sorted list, where all the elements are in order.
  * With a sorted list, we can use binary search for efficiency, but it might take more time to write a sorting algorithm for that efficiency, so sometimes we’ll encounter the tradeoff of time it takes a human to write a program compared to the time it takes a computer to run some algorithm. Other tradeoffs we’ll see might be time and complexity, or time and memory usage.

#### Selection Sort

* Take this unsorted order of `6 3 8 5 2 7 4 1` for instance,
  * Going step by step, we can sort the numbers pretty quickly. We would look at each number in the list, remembering the smallest one we've seen so far. This being 1: 
* Now we have `1 3 8 5 3 7 4 6`
  * We would repeat this again, swapping the next: `1 2 3 5 7 4 6`
* After a few more steps, we would have a sorted list.

* This algorithm is called **selection sort**, and we can be a bit more specific with some pseudocode: 
```
For i from 0 n-1
  Find smallest item between i'th item and last item
  Swap smallest item with i'th item
```
  * For this algorithm, we are looking at roughly all *n* elements to find the smallest, and making *n* passes to sort all the elements.
  * More formally, we can use some formulas to show that the biggest factor is indeed n^2. We started with having to look at all *n* elements, then only *n* - 1, then *n* - 2: 
    
    *n* + (*n*-1) + (*n*-2) + ...+1
    
    *n*(*n*+1)/2
    
    (*n*^2+n)/2
    
    *n*^2/2 + n/2
    
    *O*(n^2)
      * Since n^2 is the biggest, or dominant factor, we can say that the algorithm has a running time of *O*(n^2)

### Bubble Sort

* We can try a different algorithm, one where we swap pairs of numbers repeatedly, called **bubble sort**.
* We will look at the first two numbers in `6 3 8 5 2 7 4 1` and swap them so that they are in order: `3 6 8 5 2 7 4 1`
* The next pair, `6` and `8` are in order, so we don't need to swap them. 
* The next pair, `8` and `5`, need to be swapped: `3 6 5 8 2 7 4 1`

* With a **selection sort**, the best case with a sorted list would still take just as many steps as the worst case, since we only check for the smallest number with each pass. 

* The pseudocode for a bubble sort might look like: 
```
Repeat until sorted
  For i from 0 n-2
    If i'th and i+1'th elements out of order
      Swap them
```
  * Since we're comparing the `i'th` and `i+1'th` element, we only need to go up to *n*-2 for `i`. Then we swap the two elements if they're out of order. We can stop as soon as the list is sorted. 
* To determine the running time for a bubble sort, we have *n*-1 comparisons in the loop, and at most *n*-1 loops, so we get *n*^2-2*n*+2 steps total. But the largest factor, or dominant term, is again n^2 as `n` gets larger and larger, so we can say that bubble sort has *O*(*n*^2). So it turns out that fundamentally, insertion sort and bubble sort has the same upper bound for running time.   
* The lower bound for running time here would be Omega(*n), once we look at all the elements once. 
* So our upper bounds for running time that we've seen are: 
  * *O*(*n*^2)
    * selection sort, bubble sort
  * *O*(*n*log*n*)
  * *O*(1)
* And for lower bounds: 
  * *Omega*(*n*^2)
    * selection sort
  * *Omega*(*n* log *n*)
  * *Omega*(*n*)
    * bubble sort
  * *Omega*(log *n*)
  * *Omega*(1)
    * linear search, binary search

* **Recursion** is the ability for a function to call itself. We haven't seen this code yet, but we've seen something in pseudocode in week 0 that we might be able to convert: 
```
1  Pick up phone book
2  Open to middle of phone book
3  Look at page
4  If Smith is on page
5      Call Mike
6  Else if Smith is earlier in book
7      Open to middle of left half of book
8      Go back to line 3
9  Else if Smith is later in book
10     Open to middle of right half of book
11     Go back to line 3
12 Else
13     Quit
```
  * Here, we're using a loop-like instruction to go back to a particular line. 
* We could instead just repeat our entire algorithm on the half of the book we have left:
```
1  Pick up phone book
2  Open to middle of phone book
3  Look at page
4  If Smith is on page
5      Call Mike
6  Else if Smith is earlier in book
7      Search left half of book
8
9  Else if Smith is later in book
10     Search right half of book
11
12 Else
13     Quit
```
  * This seems like a crystal process that will never end, but we're actually changing the input to the function and dividing the problem in half each time, stopping once there's no more book left. 
* In week 1, too, we implemented a "pyramid" of blocks in the following shape: 
```
#
##
###
####
```
* But notice that a pyramid of height 4 is actually a pyramid of height 3, with an extra row of 4 blocks added on. And a pyramid of height 3 is a pyramid of height 2, with an extra row of 3 blocks. A pyramid of height 2 is a pyramid of height 1, with an extra row of 2 blocks. And finally, a pyramid of height 1 is just a single block.
* With this idea in mind, we can write a recursive function to draw pyramid, a function that calls itself to draw a smaller pyramid before adding another row. 

#### Merging Sort

* We can take the idea of recursion to sorting, with another algorithm called **merge sort**. The pseudocode might look like: 
```
If only one number
  Return
Else
  Sort left half of number
  Sort right half of number
  Merge selected halves
```
* We'll best see this in practice with two sorted lists: 
```
3 5 6 8 | 1 2 4 7
```
* We'll **merge** the two lists for a final sorted list by taking the smallest element at the front of each list, one at a time: 
```
3 5 6 8 | _ 2 4 7

1
```
* The 1 on the right side is the smallest between 1 and 3, so we can start our sorted list with it. 
```
3 5 6 8 | _ _ 4 7

1 2
```
* The next smallest number, between 2 and 3, is 2, so we use the 2. 
```
_ 5 6 8 | _ _ 4 7 

1 2 3
```
```
_ 5 6 8 | _ _ _ 7

1 2 3 4
```
```
_ _ 6 8 | _ _ _ 7

1 2 3 4 5 
```
```
_ _ _ 8 | _ _ _ 7

1 2 3 4 5 6
```
```
_ _ _ 8 | _ _ _ _ 

1 2 3 4 5 6 7
```
```
_ _ _ _ | _ _ _ _

1 2 3 4 5 6 7 8
```
  * Now we have a completely different list. 
* We've seen how the final line in our pseudocode can be implemented, and now we'll see how the entire program works: 
```
If only one number
  Return
Else
  Sort left half of number
  Sort right half of number
  Merge sorted halves
```

* Each shelf required *n* steps, and there were only log *n* shelves needed, so we multiply those factors together. Our total running time for binary search is *O*(log *n*): 
  * *O*(*n^2)
    * selection sort, bubble sort
  * *O*(*n* log *n*)
    * merge sort
  * *O*(*n*)
    * linear search
  * *O*(log *n*)
    * binary search 
  *O*(1)

* (Since log *n* is still greater than 1 but less than *n*, *n* log *n* is in between *n* (times 1) and *n*^2.)
* The best case, *Omega*, is still *n* log *n*, since we still have to sort each half first and then merge them together: 
  * *Omega*(n^2)
    * selection sort
  * *Omega*(*n* log *n*)
    * merge sort
  * *Omega*(n)
    * bubble sort
  * *Omega*(log *n*)
  * *Omega*(1)
    * linear search, binary search
* Even though merge sort is likely faster than bubble or selection sort, we did need another shelf, or more memory, to temporarily store our merged lists at each stage. 

Finally, there is another notation, Theta, which we use to describe running times of algorithms if the upper bound and lower bound are the same. For example, merge sort has *Theta*(*n* log *n*) since the best and worst case both require the same number of steps. And selection sort has Theta(n^2):
  * Theta(n^2)
    * selection sort
  * Theta(*n* log *n*)
    * merge sort
  * Theta(*n*)
  * Theta(log *n*)
  * Theta(1)

























