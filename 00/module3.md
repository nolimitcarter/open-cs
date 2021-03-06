# Week 3 notes of HarvardX's Introduction to Computer Science course

# Topic: Algorithms 

## Big *O*, Big *O* notation, and running times 

* Running times: how long an algorithm takes to run given some size of input. 
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












